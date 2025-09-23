# cosmosfarm_members_pre_user_required

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:1678`
- **실행 시점**: `Cosmosfarm_Members::user_required()`가 워드프레스 `wp_footer` 단계에서 실행될 때, 플러그인 기본 필수 항목 검사에 앞서 호출됩니다. 플러그인 설정(`회원정보 필수입력`)이 활성화되고 사용자가 로그인한 경우에만 트리거되며, 프로필 페이지로 강제 이동시키기 전에 추가 검증을 수행할 수 있습니다.
- **인자 정보**:
  - `$current_user (WP_User)`: 현재 로그인한 사용자 객체입니다. `ID`, `user_email`, `roles` 등의 프로퍼티와 `get( 'field' )`, `has_cap( 'capability' )` 같은 메서드를 활용할 수 있으며, `get_user_meta()`와 조합해 커스텀 메타 값을 확인할 수 있습니다.
  - `$profile_url (string)`: 필수 정보가 누락됐을 때 이동할 프로필 편집 페이지 URL입니다. `add_query_arg()`로 커스텀 파라미터를 붙여 안내 메시지를 띄우는 데 사용할 수 있습니다.
- **예제 코드**:
  ```php
  // 휴대폰 번호가 없으면 프로필 페이지로 강제 이동시켜 필수 입력을 안내한다.
  add_action('cosmosfarm_members_pre_user_required', function ($current_user, $profile_url) {
      if (defined('MY_COMPANY_SKIP_REQUIRED_CHECK')) {
          return; // 특정 상황에서는 검사 생략
      }

      $phone = get_user_meta($current_user->ID, 'mobile_phone', true);
      if (empty($phone)) {
          wp_safe_redirect(add_query_arg('required', 'phone', $profile_url));
          exit;
      }
  }, 10, 2);
  ```
- **주의 사항**:
  - 이미 프로필 편집 화면에 있는 경우 반복 리다이렉션이 발생하지 않도록 `is_page()`나 URL 비교로 예외 처리를 해야 합니다.
  - 이 훅 직후 플러그인 기본 로직이 동일한 필드를 검사하므로, 조건을 변경했다면 `remove_action()` 또는 후속 훅(`cosmosfarm_members_user_required`)에서 일관성을 유지해야 합니다.
  - 리다이렉션 시 `wp_safe_redirect()`와 `exit`를 호출해 헤더 전송이 확실히 마무리되도록 합니다.
- **관련 훅**: `cosmosfarm_members_user_required`, `wp_footer`, `wpmem_register_fields_arr`
