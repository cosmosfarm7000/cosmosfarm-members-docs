# cosmosfarm_members_subscription_expiry

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Subscription_Order.class.php:1620`
- **실행 시점**: 구독 주문이 만료 상태로 전환될 때 호출됩니다. 자동 재시도 실패 후 만료되는 경우와 관리자가 직접 만료 처리하는 경우 모두 실행됩니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 만료된 주문 객체입니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 해당 주문의 상품 객체입니다.
- **예제 코드**:
  ```php
  // 구독 만료 시 CRM에 상태를 동기화한다.
  add_action('cosmosfarm_members_subscription_expiry', function ($order, $product) {
      $payload = array(
          'order_id'   => $order->ID(),
          'product_id' => $product->ID(),
          'user_id'    => $order->user_id(),
          'expired_at' => current_time('mysql'),
      );
      wp_remote_post('https://crm.example.com/api/subscription/expire', array(
          'timeout' => 5,
          'headers' => array('Content-Type' => 'application/json'),
          'body'    => wp_json_encode($payload),
      ));
  }, 10, 2);
  ```
- **주의 사항**:
  - 기본 구현이 사용자 역할을 복원하거나 알림을 발송할 수 있으므로, 추가 작업 시 중복되지 않도록 상태 플래그를 사용하세요.
  - 만료 후에도 결제 재시도가 발생하지 않도록 필요한 메타를 갱신하거나 외부 결제 시스템의 빌링 키를 해지하세요.
  - `$order->subscription_next()` 값이 `'expiry'`로 설정된 상태에서 실행되므로, 이후 상태 변경 시 충돌이 없는지 확인합니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_failure`, `cosmosfarm_members_subscription_again_success`, `cosmosfarm_members_subscription_billing_key_post_delete`
