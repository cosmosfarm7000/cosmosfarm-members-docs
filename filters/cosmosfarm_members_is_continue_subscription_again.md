# cosmosfarm_members_is_continue_subscription_again

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4454`
- **실행 시점**: 구독 재결제 프로세스 중, 재결제를 계속 진행할지 여부를 결정할 때 실행됩니다. 이전 주문과 상품 정보를 기반으로 재결제 진행 여부를 필터링할 수 있습니다.
- **인자 정보**:
  - `$is_continue (bool)`: 재결제를 계속할지 여부를 나타내는 불리언 값. 기본적으로 true입니다.
  - `$old_order (Cosmosfarm_Members_Subscription_Order)`: 이전 구독 주문 객체. 주문 상태, 상품 정보 등을 확인할 수 있습니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 재결제 대상 상품 객체. 상품 가격, 유형 등의 정보를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_is_continue_subscription_again', 'my_custom_continue_subscription_again', 10, 3);
  function my_custom_continue_subscription_again($is_continue, $old_order, $product) {
    // 특정 조건에서 재결제 중단
    if ($old_order->get_status() === 'pending') {
        return false; // 이전 주문이 보류 중이면 재결제 중단
    }
    return $is_continue;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 불리언 값을 반환해야 합니다. false를 반환하면 재결제 프로세스가 중단됩니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_price`, `cosmosfarm_members_subscription_again_point_to_apply`
