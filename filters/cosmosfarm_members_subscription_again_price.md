# cosmosfarm_members_subscription_again_price

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 구독 재결제 시 적용될 가격을 계산할 때 실행됩니다. 재결제 가격을 할인하거나 조정할 수 있습니다.
- **인자 정보**:
  - `$again_price (float)`: 재결제 가격.
  - `$old_order (Cosmosfarm_Members_Order)`: 이전 주문 객체.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_again_price', 'my_custom_again_price', 10, 3);
  function my_custom_again_price($again_price, $old_order, $product) {
    // 재결제 시 5% 할인 적용
    return $again_price * 0.95;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 숫자(가격)를 반환해야 합니다. 반환된 값은 재결제 시 실제 청구될 금액으로 적용됩니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_point_to_apply`, `cosmosfarm_members_subscription_again_failure_email_args`
