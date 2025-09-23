# cosmosfarm_members_social_login_callback

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3008`
- **실행 시점**: 소셜 로그인 공급자로부터 콜백을 받은 뒤, 사용자 생성/연동 로직이 완료되고 워드프레스 세션에 로그인하기 직전에 호출됩니다. 신규 회원 가입 및 기존 계정 연동 두 경우 모두 실행됩니다.
- **인자 정보**:
  - `$channel (string)`: 로그인한 소셜 채널 슬러그(예: `naver`, `kakao`).
  - `$profile (object)`: 소셜 API에서 수신한 사용자 프로필 객체. `email`, `nickname`, `picture`, `raw_data` 등을 포함합니다.
  - `$user (WP_User)`: 로그인 또는 생성된 워드프레스 사용자 객체.
  - `$random_password (string)`: 로그인 처리용으로 생성된 임시 비밀번호. 필요 시 알림 메일 등에 활용할 수 있습니다.
- **예제 코드**:
  ```php
  // 콜백 성공 시 감사 로그와 커스텀 메타를 기록한다.
  add_action('cosmosfarm_members_social_login_callback', function ($channel, $profile, $user, $random_password) {
      if (!$user instanceof WP_User) {
          return;
      }

      update_user_meta($user->ID, '_last_social_login_channel', $channel);
      update_user_meta($user->ID, '_last_social_login_at', current_time('mysql'));

      error_log(sprintf('[Social Login] %s (%d) logged in via %s', $user->user_login, $user->ID, $channel));
  }, 10, 4);
  ```
- **주의 사항**:
  - 훅 실행 후 바로 `wp_set_current_user()`와 `wp_set_auth_cookie()`가 호출되므로, 로그인 흐름을 중단하려면 `wp_logout()` 또는 `wp_safe_redirect()`와 `exit`를 사용해야 합니다.
  - `$profile` 객체 구조는 채널별로 다를 수 있으니 속성을 사용할 때 `isset()` 체크를 권장합니다.
  - 비밀번호를 저장하거나 노출할 필요가 없다면 `$random_password`를 로그에 남기지 마세요.
- **관련 훅**: `cosmosfarm_members_pre_social_login`, `cosmosfarm_members_user_social_register`
