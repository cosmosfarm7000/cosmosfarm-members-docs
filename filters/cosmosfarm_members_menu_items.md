# cosmosfarm_members_menu_items

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members.class.php:785`
- **실행 시점**: WordPress 관리자 메뉴에서 Cosmosfarm Members 관련 메뉴 항목들을 설정할 때 실행됩니다. 플러그인의 관리자 메뉴를 추가하거나 수정할 수 있습니다.
- **인자 정보**:
  - `$menu_items (array)`: 메뉴 항목들의 연관배열. 각 키는 메뉴 슬러그, 값은 메뉴 정보를 담은 배열 (title, url, capability 등)
  - `$menu (object)`: The menu object.
  - `$args (object)`: An object of arguments.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_menu_items', 'my_custom_menu_items', 10, 3);
  function my_custom_menu_items($menu_items, $menu, $args) {
    // 기존 메뉴 항목에 새 항목 추가
    $menu_items['my-new-menu'] = array(
        'title' => __('My New Menu', 'textdomain'),
        'url'   => admin_url('admin.php?page=my-new-menu'),
        'capability' => 'manage_options',
    );
    return $menu_items;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 메뉴 항목 배열을 반환해야 합니다. 각 메뉴 항목은 title, url, capability 등의 키를 포함해야 합니다.
- **관련 훅**: `cosmosfarm_members_header_menu_items`
