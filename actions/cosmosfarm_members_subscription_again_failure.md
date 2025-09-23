# cosmosfarm_members_subscription_again_failure

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4477`
- **실행 시점**: 반복 결제 재시도(`subscription_again`) 과정에서 사용자 정보가 없거나 결제를 진행할 수 없는 조건이 감지될 때 호출됩니다. 자동 결제 재시도 뿐 아니라 관리자 수동 재시도 실패 시에도 실행됩니다.
- **인자 정보**:
  - `$old_order (Cosmosfarm_Members_Subscription_Order)`: 재시도를 시도한 기존 주문 객체입니다. `ID()`, `user()`, `pay_count()` 등을 참조할 수 있습니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 재시도 대상 구독 상품 객체입니다. `price()`, `subscription_again_price_type()`, `subscription_active()` 등의 정보를 제공합니다.
- **예제 코드**:
  ```php
  // 재결제가 실패하면 슬랙 알림을 보낸다.
  add_action('cosmosfarm_members_subscription_again_failure', function ($old_order, $product) {
      $user = $old_order->user();
      $message = sprintf(
          'Subscription retry failed for order #%d (%s). Product: %s',
          $old_order->ID(),
          $user ? $user->user_login : 'guest',
          $product->title()
      );

      wp_remote_post('https://hooks.slack.com/services/XXX/YYY/ZZZ', array(
          'timeout' => 3,
          'body'    => wp_json_encode(array('text' => $message)),
          'headers' => array('Content-Type' => 'application/json'),
      ));
  }, 10, 2);
  ```
- **주의 사항**:
  - 훅 이후 기본 로직이 오류 메시지를 저장하고 관리자 알림을 표시하므로, 중복 알림을 방지하려면 상태 플래그를 기록해 멱등성을 유지하세요.
  - `$old_order->user()`가 `WP_User`를 반환하지 않을 수 있으니 null 체크 후 사용합니다.
  - 멤버십 해지나 환불 처리는 실패 원인에 따라 적절히 분기하세요.
- **관련 훅**: `cosmosfarm_members_pre_subscription_again`, `cosmosfarm_members_subscription_again_success`, `cosmosfarm_members_subscription_expiry`
