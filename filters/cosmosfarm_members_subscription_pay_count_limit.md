# cosmosfarm_members_subscription_pay_count_limit

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 구독 상품의 결제 횟수 제한을 확인한 후, 결제 횟수 제한을 허용할지 여부를 필터링합니다. 결제 횟수가 상품의 설정된 제한 횟수 이상인 경우 기본적으로 false로 설정되며, 이 값을 필터를 통해 변경할 수 있습니다.
- **인자 정보**:
  - `$pay_count_limit (bool)`: 결제 횟수 제한을 허용할지 여부. true인 경우 결제를 허용하고, false인 경우 결제를 제한합니다. 기본적으로 상품의 결제 횟수 제한을 초과하면 false로 설정됩니다.
  - `$old_order (Cosmosfarm_Members_Subscription_Order)`: 이전 구독 주문 객체로, 결제 횟수 등의 정보를 포함합니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체로, 결제 횟수 제한 설정 등의 정보를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_subscription_pay_count_limit', 'my_custom_pay_count_limit', 10, 3);
function my_custom_pay_count_limit($pay_count_limit, $old_order, $product) {
    // 특정 상품에 대한 결제 횟수 제한
    if ($product->ID() === 456) {
        return 3; // 최대 3회까지 결제 가능
    }
    return $pay_count_limit;
}
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
