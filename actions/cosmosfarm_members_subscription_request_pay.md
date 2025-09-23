# cosmosfarm_members_subscription_request_pay

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:1462`
- **실행 시점**: 관리자 또는 프런트엔드에서 구독 결제 요청이 성공적으로 생성되어 주문 객체가 초기화된 직후 호출됩니다. `Cosmosfarm_Members_Controller::subscription_request_pay()`와 자동 결제 시나리오에서 호출되며, 주문 게시글과 상품 객체가 모두 준비된 상태입니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 생성 또는 갱신된 구독 주문 객체입니다. `ID()`, `user()`, `price()`, `subscription_role()` 등을 이용해 주문 상태를 확인하거나, `set_*` 메서드로 메타를 갱신할 수 있습니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 주문과 연결된 구독 상품 객체입니다. `title()`, `price()`, `subscription_type()`, `earn_points()` 등 상품 정책 정보를 제공합니다.
  - `$custom_data (array)`: 결제 요청 시 제출된 `$_POST` 데이터가 그대로 전달됩니다. 결제 수단, 청구서 정보, 커스텀 체크아웃 필드를 참고할 수 있습니다.
- **예제 코드**:
  ```php
  // 결제 완료 후 외부 ERP 시스템에 주문 정보를 전달한다.
  add_action('cosmosfarm_members_subscription_request_pay', function ($order, $product, $custom_data) {
      $payload = array(
          'order_id'        => $order->ID(),
          'product_id'      => $product->ID(),
          'product_title'   => $product->title(),
          'user_id'         => $order->user_id(),
          'price'           => $order->real_price(),
          'payment_gateway' => isset($custom_data['builtin_pg']) ? sanitize_text_field($custom_data['builtin_pg']) : '',
      );

      wp_remote_post('https://erp.example.com/api/subscription', array(
          'timeout' => 5,
          'headers' => array('Content-Type' => 'application/json'),
          'body'    => wp_json_encode($payload),
      ));
  }, 10, 3);
  ```
- **주의 사항**:
  - 훅은 동일한 결제 요청 과정에서 여러 번 실행될 수 있습니다(모바일/PC, 자동 결제 재시도 등). 멱등성을 유지할 수 있도록 외부 시스템 연동 시 중복 처리 방지 로직을 추가하세요.
  - `$custom_data`에는 사용자 입력이 그대로 포함되므로 신뢰하기 전에 `sanitize_text_field()`, `wp_kses()` 등으로 필터링해야 합니다.
  - 장시간 블로킹 작업은 결제 응답을 지연시킬 수 있으므로, 필요시 `wp_schedule_single_event()`로 비동기 처리하세요.
- **관련 훅**: `cosmosfarm_members_subscription_request_pay_result`, `cosmosfarm_members_subscription_request_pay_user`, `cosmosfarm_members_subscription_request_pay_order_point_to_apply`
