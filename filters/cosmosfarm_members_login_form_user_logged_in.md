# cosmosfarm_members_login_form_user_logged_in

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Page_Builder.class.php`
- **실행 시점**: 로그인 페이지에 접근했을 때 사용자가 이미 로그인되어 있는 경우, 표시될 레이아웃을 필터링할 때 실행됩니다. 로그인 폼 대신 표시될 콘텐츠를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$layout (string)`: 로그인된 사용자에게 표시될 HTML 레이아웃. **초기값은 빈 문자열이며, 필터에서 HTML을 생성하여 반환해야 합니다.**
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_login_form_user_logged_in', 'my_custom_logged_in_layout');
  function my_custom_logged_in_layout($layout) {
    return '<p>이미 로그인되어 있습니다. <a href="' . wp_logout_url() . '">로그아웃</a></p>';
  }
  ```

- **주의 사항**: 필터 함수는 반드시 HTML 문자열을 반환해야 합니다. 반환된 콘텐츠는 로그인 페이지에서 로그인된 사용자에게 표시됩니다.
- **관련 훅**: `cosmosfarm_members_template_login_form`
