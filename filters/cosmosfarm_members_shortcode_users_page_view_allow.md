# cosmosfarm_members_shortcode_users_page_view_allow

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Page_Builder.class.php`
- **실행 시점**: `[cosmosfarm_members_users]` 숏코드가 실행될 때 페이지 보기 권한을 확인할 때 실행됩니다. 사용자 목록 페이지에 대한 접근 권한을 제어할 수 있습니다.
- **인자 정보**:
  - `$allow (bool)`: 페이지 보기 허용 여부. 기본적으로 로그인한 사용자에게 true를 반환합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_shortcode_users_page_view_allow', 'my_custom_users_page_allow');
  function my_custom_users_page_allow($allow) {
    // 관리자만 사용자 목록 페이지를 볼 수 있도록 제한
    if (!current_user_can('manage_options')) {
        return false;
    }
    return $allow;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 불리언 값을 반환해야 합니다. false를 반환하면 사용자 목록 페이지가 표시되지 않습니다.
- **관련 훅**: `cosmosfarm_members_shortcode_users_page_layout`
