# cosmosfarm_members_admin_menu

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:130`
- **실행 시점**: `Cosmosfarm_Members::add_admin_menu()`이 플러그인 고유의 관리자 메뉴와 하위 메뉴를 모두 등록한 직후 트리거됩니다. 이 메서드는 `cosmosfarm-members.php`에서 워드프레스 `admin_menu` 훅에 연결되어 있으므로, 워드프레스가 관리자 메뉴 구조를 구성할 때 마지막 단계에서 실행됩니다.
- **인자 정보**:
  - *(없음)* 이 훅은 추가 인자를 전달하지 않습니다.
- **예제 코드**:

  ```php
  // 플러그인 기본 메뉴가 생성된 뒤 커스텀 하위 메뉴를 추가한다.
  add_action('cosmosfarm_members_admin_menu', function () {
      add_submenu_page(
          'cosmosfarm_members_setting',      // 상위 메뉴 슬러그
          __('Membership Reports', 'textdomain'),
          __('Reports', 'textdomain'),
          'manage_cosmosfarm_members',       // 접근 권한(역할)
          'cosmosfarm_members_reports',
          'my_members_reports_page_render'
      );
  });
  
  function my_members_reports_page_render() {
      echo '<div class="wrap"><h1>' . esc_html__('Reports Dashboard', 'textdomain') . '</h1></div>';
  }
  ```
- **주의 사항**:
  - 관리자 메뉴는 `admin_menu` 단계에서 캐시되므로, 메뉴 변경은 페이지 새로고침 후에 확인할 수 있습니다.
  - 접근 권한은 플러그인이 기본으로 사용하는 `manage_cosmosfarm_members` 능력을 재사용하는 것이 안전합니다. 다른 권한을 지정하면 일부 관리자 계정에서 메뉴가 숨겨질 수 있습니다.
  - 메뉴 위치를 변경하려면 상위 슬러그(`cosmosfarm_members_setting` 등)를 정확히 맞춰야 하며, 잘못 지정하면 워드프레스 기본 설정 메뉴에 추가될 수 있습니다.
- **관련 훅**: `admin_menu`, `admin_init`
