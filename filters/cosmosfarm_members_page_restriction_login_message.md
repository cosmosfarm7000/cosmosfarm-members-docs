# cosmosfarm_members_page_restriction_login_message

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members.class.php`
- **실행 시점**: 페이지가 제한되어 로그인해야 할 때 표시될 메시지를 설정할 때 실행됩니다. 로그인 유도 메시지를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$message (string)`: 로그인 메시지 텍스트. 기본적으로 "Log in to view this page." 등의 번역된 텍스트입니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_page_restriction_login_message', 'my_custom_restriction_login_message');
  function my_custom_restriction_login_message($message) {
    return '로그인하여 콘텐츠를 확인하세요.';
  }
  ```

- **주의 사항**: 필터 함수는 반드시 문자열을 반환해야 합니다. 반환된 메시지는 제한된 페이지의 로그인 유도 텍스트로 사용됩니다.
- **관련 훅**: `cosmosfarm_members_page_restriction_message`, `cosmosfarm_members_page_restriction_register_message`
