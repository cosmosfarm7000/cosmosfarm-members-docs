# cosmosfarm_members_shortcode_users_page_layout

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Page_Builder.class.php:135`
- **실행 시점**: `[cosmosfarm_members_users]` 숏코드가 실행되어 사용자 목록 페이지를 렌더링할 때 실행됩니다. 사용자 목록 페이지의 전체 레이아웃을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$layout (string)`: 사용자 목록 페이지의 HTML 레이아웃.
  - `$page_view_allow (bool)`: 페이지 보기 허용 여부. true면 페이지를 볼 수 있음, false면 제한됨.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_shortcode_users_page_layout', 'my_custom_users_page_layout', 10, 2);
  function my_custom_users_page_layout($layout, $page_view_allow) {
    if ($page_view_allow) {
        return '<div class="custom-users-list">' . $layout . '</div>';
    }
    return '<p>사용자 목록을 볼 수 없습니다.</p>';
  }
  ```

- **주의 사항**: 필터 함수는 반드시 HTML 문자열을 반환해야 합니다. 반환된 레이아웃은 숏코드가 삽입된 페이지에 표시됩니다.
- **관련 훅**: `cosmosfarm_members_shortcode_users_page_view_allow`
