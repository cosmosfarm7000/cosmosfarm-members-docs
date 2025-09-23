# cosmosfarm_members_subscription_again_success

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4748`
- **실행 시점**: 자동 결제 재시도가 성공적으로 완료되어 새 주문이 생성되고 결제 상태가 갱신된 직후 호출됩니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 새로 생성된 재결제 주문 객체입니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 해당 주문과 연결된 상품 객체입니다.
  - `$old_order (Cosmosfarm_Members_Subscription_Order)`: 재결제 이전의 기존 주문 객체입니다.
- **예제 코드**:
  ```php
  // 재결제가 성공한 뒤 외부 CRM에 리포트한다.
  add_action('cosmosfarm_members_subscription_again_success', function ($order, $product, $old_order) {
      $payload = array(
          'new_order_id'   => $order->ID(),
          'old_order_id'   => $old_order->ID(),
          'product_id'     => $product->ID(),
          'user_id'        => $order->user_id(),
          'paid_amount'    => $order->real_price(),
          'pay_count'      => $order->pay_count(),
          'next_schedule'  => $order->subscription_next(),
      );
      wp_remote_post('https://crm.example.com/api/renewal', array(
          'timeout' => 5,
          'body'    => wp_json_encode($payload),
          'headers' => array('Content-Type' => 'application/json'),
      ));
  }, 10, 3);
  ```
- **주의 사항**:
  - 기본 로직이 SMS/이메일/Webhook 알림을 발송하므로, 중복 발송을 피하려면 커스텀 작업에서 상태 플래그를 확인하세요.
  - `$old_order`는 이미 상태가 업데이트된 후 전달되므로, 비교용 데이터가 필요하면 훅 이전에 복제하거나 메타를 기록해 두는 것이 좋습니다.
  - 멱등성을 위해 외부 시스템에 전송할 때 주문 ID를 기준으로 중복을 감지하세요.
- **관련 훅**: `cosmosfarm_members_pre_subscription_again`, `cosmosfarm_members_subscription_again_failure`, `cosmosfarm_members_subscription_expiry`
