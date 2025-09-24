# cosmosfarm_members_social_login_redirect_to

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3064`
- **실행 시점**: 사용자가 소셜 로그인을 통해 인증된 후 리다이렉트될 URL을 결정할 때 실행됩니다. 소셜 로그인 성공 후 사용자를 보낼 목적지를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$redirect_to (string)`: 소셜 로그인 후 리다이렉트될 URL.
  - `$profile (array)`: 소셜 프로필 정보 배열. 소셜 플랫폼에서 제공하는 사용자 정보입니다.
  - `$user (WP_User)`: 생성되거나 연결된 WordPress 사용자 객체.
  - `$random_password (string)`: 자동 생성된 임시 비밀번호 (새 사용자인 경우).
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_social_login_redirect_to', 'my_custom_social_login_redirect', 10, 4);
  function my_custom_social_login_redirect($redirect_to, $profile, $user, $random_password) {
    return home_url('/my-account/');
  }
  ```

- **주의 사항**: 필터 함수는 반드시 유효한 URL 문자열을 반환해야 합니다. 반환된 URL은 소셜 로그인 성공 후 사용자를 리다이렉트하는 데 사용됩니다.
- **관련 훅**: `cosmosfarm_members_login_redirect_to`
