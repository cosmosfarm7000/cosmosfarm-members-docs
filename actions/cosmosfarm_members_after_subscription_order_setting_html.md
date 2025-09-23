# cosmosfarm_members_after_subscription_order_setting_html

- **분류**: Action
- **정의 위치**: `admin/subscription_order_setting.php:487`
- **실행 시점**: 구독 주문 편집 화면에서 기본 폼과 상품 필드 테이블이 모두 출력된 직후, 두 번째 저장 버튼이 렌더링되기 전에 호출됩니다. 화면 하단에 추가 안내나 요약 정보를 붙일 때 적합합니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 현재 편집 중인 주문 객체입니다. `ID()`로 포스트 ID를, `user()`로 연결된 `WP_User`를 가져올 수 있으며 결제 회차(`pay_count()`), 가격(`price()`, `next_price()`, `real_price()`), 구독 상태(`subscription_type()`, `subscription_next()`, `subscription_next_format()`) 등을 조회할 수 있습니다. 매직 프로퍼티(`$order->buyer_name`, `$order->buyer_email`, `$order->buyer_tel`)로 주문자 정보를 바로 출력할 수 있고, `set_subscription_role()`, `set_next_price()` 같은 세터로 값을 갱신할 수도 있으므로 변경 시에는 후속 훅에서 검증이 필요합니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 주문과 연결된 구독 상품 객체입니다. `product_id()`로 상품 포스트 ID를 확인하고, `price()`, `subscription_first_free()`, `subscription_type()`, `subscription_type_format()`으로 반복 결제 정책을 점검합니다. `fields()`와 `option_fields()`는 체크아웃 커스텀 필드 구성을 반환하며, `option_title()`/`option_subtitle()`을 통해 옵션 라벨, `subscription_first_free()` 값으로 무료 체험 기간(`1day`, `7day`, `onetime` 등)을 파악할 수 있습니다.
- **예제 코드**:

  ```php
  // 결제 요약과 내부 체크리스트를 폼 하단에 노출한다.
  add_action('cosmosfarm_members_after_subscription_order_setting_html', function ($order, $product) {
      if (!current_user_can('manage_cosmosfarm_members')) {
          return;
      }
  
      $current_role  = $order->subscription_role();
      $next_schedule = $order->next_subscription_datetime('', 'Y-m-d H:i');
      ?>
      <h2><?php esc_html_e('결제 요약', 'textdomain'); ?></h2>
      <table class="widefat">
          <tbody>
              <tr>
                  <th scope="row"><?php esc_html_e('현재 구독 상태', 'textdomain'); ?></th>
                  <td><?php echo esc_html($order->subscription_next_format()); ?></td>
              </tr>
              <tr>
                  <th scope="row"><?php esc_html_e('다음 결제 예정일', 'textdomain'); ?></th>
                  <td><?php echo esc_html($next_schedule ?: '-'); ?></td>
              </tr>
              <tr>
                  <th scope="row"><?php esc_html_e('부여될 역할', 'textdomain'); ?></th>
                  <td><?php echo esc_html($current_role ?: '-'); ?></td>
              </tr>
              <tr>
                  <th scope="row"><?php esc_html_e('상품 기본 금액', 'textdomain'); ?></th>
                  <td><?php echo esc_html(cosmosfarm_members_currency_format($product->price())); ?></td>
              </tr>
          </tbody>
      </table>
      <?php
  }, 10, 2);
  ```
- **주의 사항**:
  - 관리자 테이블 마크업(`widefat`, `form-table` 등)을 활용하면 워드프레스 기본 스타일과 자연스럽게 어울립니다.
  - 하단에 폼 필드를 추가하면 제출 버튼과 시각적으로 가까워지므로, 필수 입력값인 경우 저장 훅(`cosmosfarm_members_after_subscription_order_setting` 등)에서 검증 로직을 반드시 추가하세요.
  - 페이지 내 스크립트나 스타일을 주입해야 한다면 `admin_enqueue_scripts` 또는 `admin_print_footer_scripts` 훅과 병행해 관리하십시오.
- **관련 훅**: `cosmosfarm_members_before_subscription_order_setting_html`, `cosmosfarm_members_before_subscription_order_setting`, `cosmosfarm_members_after_subscription_order_setting`
