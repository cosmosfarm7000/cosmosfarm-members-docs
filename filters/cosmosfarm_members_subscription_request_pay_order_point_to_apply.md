# cosmosfarm_members_subscription_request_pay_order_point_to_apply

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 구독 결제 시 적용될 포인트 잔액을 필터링합니다.
- **인자 정보**:
  - `$mycred_get_users_balance($user->ID (mixed)`: 파라미터 1
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
