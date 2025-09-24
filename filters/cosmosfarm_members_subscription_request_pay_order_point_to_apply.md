# cosmosfarm_members_subscription_request_pay_order_point_to_apply

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4128`
- **실행 시점**: 구독 결제 시 적용될 포인트 잔액을 필터링합니다.
- **인자 정보**:
  - `$mycred_balance (float)`: 사용자의 현재 myCRED 포인트 잔액.
  - `$user_id (int)`: 사용자 ID.
  - `$coupon_price (float)`: 쿠폰 적용 후 가격.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
  - `$meta_input (array)`: 메타 입력 데이터.
  - `$custom_data (array)`: 사용자 정의 데이터.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_request_pay_order_point_to_apply', 'my_custom_pay_point_to_apply', 10, 6);
  function my_custom_pay_point_to_apply($mycred_balance, $user_id, $coupon_price, $product, $meta_input, $custom_data) {
    // 사용 가능한 최대 포인트 제한
    $max_points_to_use = 1000;
    return min($mycred_balance, $max_points_to_use);
  }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
