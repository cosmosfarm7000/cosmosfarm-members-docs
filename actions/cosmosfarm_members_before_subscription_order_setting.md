# cosmosfarm_members_before_subscription_order_setting

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:603`
- **실행 시점**: 관리자 메뉴에서 구독 주문을 편집할 때 `Cosmosfarm_Members::subscription_order_setting()`이 주문/상품 객체를 로드한 직후, 폼 템플릿(`admin/subscription_order_setting.php`)이 포함되기 전에 호출됩니다. 따라서 화면에 표시될 데이터를 최종 점검하거나 로깅을 남기기에 적합합니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 현재 편집 중인 주문 객체입니다. `ID()`로 포스트 ID, `user()`로 연결된 `WP_User`를 얻을 수 있고, `pay_count()`, `price()`, `next_price()`, `real_price()` 같은 금액 정보와 `subscription_type()`, `subscription_next()`, `subscription_next_format()` 등 구독 상태 메타를 조회할 수 있습니다. 매직 프로퍼티(`$order->buyer_name`, `$order->buyer_email`, `$order->buyer_tel`)는 주문자 정보를 즉시 반환합니다. `set_subscription_role()`, `set_next_price()` 등 세터도 제공하므로 값을 변경할 때는 후속 훅이나 저장 로직과 충돌하지 않도록 주의합니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 주문과 연결된 구독 상품 객체입니다. `product_id()`로 상품 포스트 ID를 확인하고, `price()`, `subscription_first_free()`, `subscription_type()`, `subscription_type_format()`으로 반복 결제 설정을 확인합니다. `fields()`·`option_fields()`는 체크아웃 커스텀 필드 구성을, `option_title()`/`option_subtitle()`은 옵션 라벨 정보를 제공합니다.
- **예제 코드**:
  ```php
  // 구독 주문 편집 시 내부 검증 및 관리자 알림을 추가한다.
  add_action('cosmosfarm_members_before_subscription_order_setting', function ($order, $product) {
      if (!current_user_can('manage_cosmosfarm_members_order')) {
          return;
      }

      // 만료 처리 상태인데 잔액이 남아 있다면 경고 메시지를 표시한다.
      if ($order->subscription_next() === 'expiry' && $order->balance() > 0) {
          add_action('admin_notices', function () use ($order) {
              printf(
                  '<div class="notice notice-warning"><p>%s</p></div>',
                  esc_html(sprintf(__('Order #%d has an outstanding balance.', 'textdomain'), $order->ID()))
              );
          });
      }

      // 요청 파라미터를 사용해 특정 메타를 동기화할 수도 있다.
      if (isset($_GET['sync_membership_role'], $_GET['_wpnonce']) &&
          wp_verify_nonce($_GET['_wpnonce'], 'sync-membership-role-' . $order->ID())) {
          update_post_meta($order->ID(), '_membership_synced_by', get_current_user_id());
      }
  }, 10, 2);
  ```
- **주의 사항**:
  - 이 훅은 화면 렌더링 직전에만 실행되며, 주문 저장 요청(`admin_post_cosmosfarm_members_order_save`) 중에는 실행되지 않습니다. 폼 데이터를 실제로 저장하려면 `admin_post_cosmosfarm_members_order_save` 등 별도의 액션을 활용해야 합니다.
  - `$order` 객체는 세터를 통해 즉시 DB를 수정할 수 있으므로, 다른 저장 루틴과 중복 업데이트가 발생하지 않도록 변경 시점을 명확히 관리해야 합니다.
  - 민감한 작업에 외부 파라미터(`$_GET`)를 활용할 때는 `check_admin_referer()` 또는 `wp_verify_nonce()`로 반드시 검증하십시오.
- **관련 훅**: `cosmosfarm_members_before_subscription_order_setting_html`, `cosmosfarm_members_after_subscription_order_setting_html`, `admin_post_cosmosfarm_members_order_save`
