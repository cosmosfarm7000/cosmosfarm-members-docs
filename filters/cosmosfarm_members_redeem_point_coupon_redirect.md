# cosmosfarm_members_redeem_point_coupon_redirect

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:5554`
- **실행 시점**: 사용자가 포인트 쿠폰을 사용한 후 리다이렉트될 URL을 결정할 때 실행됩니다. 쿠폰 사용 후 사용자를 보낼 목적지를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$redirect_to (string)`: 쿠폰 사용 후 리다이렉트될 URL.
  - `$coupon_id (int)`: 사용된 쿠폰의 ID.
  - `$mycred_coupon (object)`: MyCred 쿠폰 객체. 쿠폰의 속성과 정보를 포함합니다.
  - `$user_id (int)`: 쿠폰을 사용한 사용자의 ID.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_redeem_point_coupon_redirect', 'my_custom_point_coupon_redirect', 10, 4);
  function my_custom_point_coupon_redirect($redirect_to, $coupon_id, $mycred_coupon, $user_id) {
    return home_url('/my-points/');
  }
  ```

- **주의 사항**: 필터 함수는 반드시 유효한 URL 문자열을 반환해야 합니다. 반환된 URL은 쿠폰 사용 성공 후 사용자를 리다이렉트하는 데 사용됩니다.
- **관련 훅**: `cosmosfarm_members_social_login_redirect_to`
