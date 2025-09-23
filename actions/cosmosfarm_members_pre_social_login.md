# cosmosfarm_members_pre_social_login

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2811`
- **실행 시점**: 사용자가 소셜 로그인 채널(`?action=cosmosfarm_members_social_login&channel=...`)을 통해 리다이렉트되기 직전에 호출됩니다. 해당 채널의 API 요청 URL을 가져오기 전에 실행되므로, 리다이렉트 제한이나 사전 검사를 적용할 수 있습니다.
- **인자 정보**:
  - `$channel (string)`: 요청된 소셜 로그인 채널 슬러그(예: `naver`, `kakao`, `facebook`).
- **예제 코드**:
  ```php
  // 특정 채널을 임시로 비활성화한다.
  add_action('cosmosfarm_members_pre_social_login', function ($channel) {
      $blocked = array('facebook');
      if (in_array($channel, $blocked, true)) {
          wp_die(__('Facebook login is temporarily unavailable. Please try another method.', 'textdomain'));
      }
  });
  ```
- **주의 사항**:
  - 훅을 통해 `wp_redirect()`나 `wp_die()`를 호출하면 이후 소셜 로그인 흐름이 중단됩니다. 사용자 안내 메시지를 명확히 제공하세요.
  - 허용된 리다이렉트 URL을 검증할 때는 `wp_validate_redirect()`를 사용해 오픈 리다이렉트 취약점을 방지하세요.
  - 채널 이름은 소문자로 전달되며, 지원하지 않는 채널의 경우 기본적으로 홈으로 리다이렉트됩니다.
- **관련 훅**: `cosmosfarm_members_social_login_callback`, `cosmosfarm_members_user_social_register`
