# cosmosfarm_members_subscription_request_pay_user

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 구독 결제 요청 시 사용자 객체를 필터링합니다.
- **인자 정보**:
  - `$user (WP_User)`: WordPress 사용자 객체.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
  - `$meta_input (array)`: 메타 입력 데이터.
  - `$custom_data (array)`: 사용자 정의 데이터.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_request_pay_user', 'my_custom_pay_request_user', 10, 4);
  function my_custom_pay_request_user($user, $product, $meta_input, $custom_data) {
    // 결제 요청 시 사용자 정보 변경
    // $user->user_email = 'new_email@example.com';
    return $user;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
