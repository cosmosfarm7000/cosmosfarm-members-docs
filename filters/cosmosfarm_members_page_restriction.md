# cosmosfarm_members_page_restriction

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members.class.php`
- **실행 시점**: 페이지 접근 제한을 확인할 때 실행됩니다. 사용자가 특정 페이지에 접근할 수 있는지 여부를 결정하는 로직을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$page_restriction (bool)`: 페이지 제한 여부. true면 제한됨, false면 제한되지 않음.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_page_restriction', 'my_custom_page_restriction_logic');
  function my_custom_page_restriction_logic($page_restriction) {
    // 특정 조건에서 페이지 제한 해제
    if (is_user_logged_in() && current_user_can('administrator')) {
        return false; // 관리자는 항상 접근 가능
    }
    return $page_restriction;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 불리언 값을 반환해야 합니다. false를 반환하면 페이지 제한이 해제됩니다.
- **관련 훅**: `cosmosfarm_members_page_restriction_content`, `cosmosfarm_members_page_restriction_message`
