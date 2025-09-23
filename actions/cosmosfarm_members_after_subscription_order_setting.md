# cosmosfarm_members_after_subscription_order_setting

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:607`
- **실행 시점**: 구독 주문 편집 화면이 모두 렌더링된 이후(`admin/subscription_order_setting.php` 템플릿이 완료되고 제출 버튼이 출력된 직후) 호출됩니다. 화면 출력 직후 후처리, 로깅, 비동기 작업 트리거에 적합합니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 방금 표시된 주문 객체입니다. `ID()`, `user()`, `real_price()`, `subscription_next()`, `subscription_next_format()` 등으로 결제 상태를 파악할 수 있으며, `set_*` 계열 메서드로 후속 업데이트를 수행할 수도 있습니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 주문과 연결된 상품 객체입니다. `product_id()`, `price()`, `subscription_first_free()`, `subscription_type()`/`subscription_type_format()`, `fields()` 등으로 상품/필드 구성을 확인할 수 있습니다.
- **예제 코드**:
  ```php
  // 주문 상세 페이지가 렌더링된 뒤 감사 로그와 리마인더 스케줄을 남긴다.
  add_action('cosmosfarm_members_after_subscription_order_setting', function ($order, $product) {
      if (!current_user_can('manage_cosmosfarm_members_order')) {
          return;
      }

      // 감사 로그 남기기
      error_log(sprintf('[Membership] Order #%d viewed by %s', $order->ID(), wp_get_current_user()->user_login));

      // 다음 결제 예정일이 존재하면 관리자용 리마인더 이벤트 예약
      $next_timestamp = strtotime($order->next_subscription_datetime());
      if ($next_timestamp && $next_timestamp > time()) {
          wp_schedule_single_event($next_timestamp - DAY_IN_SECONDS, 'cosmosfarm_members_send_payment_reminder', array($order->ID()));
      }
  }, 10, 2);
  ```
- **주의 사항**:
  - 이 훅은 화면 렌더링 이후에 실행되지만, 여전히 현재 요청 안에서 동작하므로 과도한 처리(원격 HTTP 호출 등)는 `wp_schedule_single_event()`와 같은 비동기 작업으로 넘기는 것이 좋습니다.
  - 주문 저장 로직은 `admin_post_cosmosfarm_members_order_save`에서 처리되므로, 폼 제출값을 검증/저장하려면 해당 액션이나 별도의 필터를 사용해야 합니다.
  - `$order` 객체를 수정하면 관리자에게 즉시 표시되는 데이터가 변경될 수 있습니다. 표시용 데이터만 조정하고, 영구 저장은 전용 세터나 메타 업데이트 함수를 사용해 명확히 수행하세요.
- **관련 훅**: `cosmosfarm_members_before_subscription_order_setting`, `cosmosfarm_members_before_subscription_order_setting_html`, `cosmosfarm_members_after_subscription_order_setting_html`, `admin_post_cosmosfarm_members_order_save`
