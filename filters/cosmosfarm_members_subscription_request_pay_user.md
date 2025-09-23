# cosmosfarm_members_subscription_request_pay_user

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 구독 결제 요청 시 사용자 객체를 필터링합니다.
- **인자 정보**:
  - `$user (mixed)`: 파라미터 1
  - `$product (mixed)`: 파라미터 2
  - `$meta_input (mixed)`: 파라미터 3
  - `$custom_data (mixed)`: 파라미터 4
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
