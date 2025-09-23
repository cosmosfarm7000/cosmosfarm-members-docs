# cosmosfarm_members_header_menu_current_page

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 헤더 메뉴를 렌더링할 때, 메뉴 항목이 설정된 후 현재 페이지 식별자를 결정하기 전에 실행됩니다.
- **인자 정보**:
  - `$current_page (string|int)`: 현재 페이지의 식별자. 기본적으로는 현재 포스트 ID이거나 특정 페이지(프로필, 주문, 알림 등)에 따라 미리 정의된 값('profile', 'orders', 'notifications' 등)이 설정됩니다.
  - `$menu_items (array)`: 헤더 메뉴 항목들의 배열. 각 항목은 'id', 'url', 'title' 키를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_header_menu_current_page', 'my_custom_header_current_page', 10, 2);
    function my_custom_header_current_page($current_page, $menu_items) {
        // 특정 URL에 있을 때 'my-custom-link'를 현재 페이지로 설정
        if (strpos($_SERVER['REQUEST_URI'], '/custom-page/') !== false) {
            return 'my-custom-link';
        }
        return $current_page;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다. 반환된 값은 헤더 메뉴에서 현재 활성화된 메뉴 항목을 결정하는 데 사용됩니다.
- **관련 훅**: `cosmosfarm_members_header_menu_items` (메뉴 항목 필터링)
