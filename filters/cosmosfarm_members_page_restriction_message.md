# cosmosfarm_members_page_restriction_message

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members.class.php:1906`
- **실행 시점**: 페이지가 제한되어 접근할 수 없을 때 표시될 기본 메시지를 설정할 때 실행됩니다. 페이지 제한 시 표시될 메시지를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$message (string)`: 페이지 제한 메시지 HTML. 기본적으로 로그인 유도 메시지를 포함한 HTML입니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_page_restriction_message', 'my_custom_restriction_message');
  function my_custom_restriction_message($message) {
    return '<p>이 페이지는 회원 전용입니다. 로그인해주세요!</p>';
  }
  ```

- **주의 사항**: 필터 함수는 반드시 HTML 문자열을 반환해야 합니다. 반환된 메시지는 제한된 페이지에 표시됩니다.
- **관련 훅**: `cosmosfarm_members_page_restriction_login_message`, `cosmosfarm_members_page_restriction_register_message`
