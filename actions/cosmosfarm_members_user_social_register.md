# cosmosfarm_members_user_social_register

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Social_Login.class.php:44`
- **실행 시점**: 소셜 로그인 채널에서 신규 사용자가 처음 등록되어 워드프레스 사용자로 생성된 직후 호출됩니다.
- **인자 정보**:
  - `$user_id (int)`: 방금 생성된 사용자 ID
  - `$social_login (Cosmosfarm_Members_Social_Login)`: 현재 소셜 로그인 처리 객체. `$social_login->channel`로 채널 식별자(예: `kakao`, `naver`, `google`)를 확인할 수 있습니다.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_user_social_register', function ($user_id, $social_login) {
      update_user_meta($user_id, 'registered_via_social', sanitize_text_field($social_login->channel));
  }, 10, 2);
  ```

- **주의 사항**:
  - 첫 저장 시점이므로 환영 메일 발송, 초기 역할 부여 등의 초기화 로직을 넣기 좋습니다. 단, 로그인 직후 자동 리다이렉트와 충돌하지 않도록 비동기 작업을 고려하세요.
- **관련 훅**: `cosmosfarm_members_pre_social_login`, `cosmosfarm_members_social_login_callback`
