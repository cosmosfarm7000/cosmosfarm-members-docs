# cosmosfarm_members_subscription_again_point_to_apply

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 구독 재결제 시 사용자가 사용할 수 있는 포인트 잔액을 계산할 때 실행됩니다. 재결제에서 사용할 포인트 금액을 제한하거나 조정할 수 있습니다.
- **인자 정보**:
  - `$mycred_balance (float)`: 사용자의 현재 포인트 잔액.
  - `$user_id (int)`: 사용자 ID.
  - `$again_price (float)`: 재결제 가격.
  - `$old_order (Cosmosfarm_Members_Order)`: 이전 주문 객체.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_again_point_to_apply', 'my_custom_again_point_to_apply', 10, 5);
  function my_custom_again_point_to_apply($mycred_balance, $user_id, $again_price, $old_order, $product) {
    // 재결제 시 포인트 사용을 50%로 제한
    return $mycred_balance * 0.5;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 숫자(포인트 금액)를 반환해야 합니다. 반환된 값은 재결제 시 실제로 사용할 포인트 금액으로 적용됩니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_price`, `cosmosfarm_members_subscription_again_failure_email_args`
