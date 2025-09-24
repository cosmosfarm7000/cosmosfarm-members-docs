# cosmosfarm_members_header_menu_items

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:137`
- **실행 시점**: 헤더 메뉴 항목들이 기본적으로 설정된 후, 현재 페이지 결정 전에 실행됩니다. 기본 메뉴 항목(프로필, 주문, 알림, 메시지, 회원 목록 등)이 설정된 상태에서 추가/수정/삭제할 수 있습니다.
- **인자 정보**:
  - `$menu_items (array)`: 헤더 메뉴 항목들의 연관 배열. 각 메뉴 항목은 다음과 같은 구조를 가집니다:
    - `'id' (string)`: 메뉴 항목의 고유 식별자
    - `'url' (string)`: 메뉴 항목의 URL
    - `'title' (string)`: 메뉴 항목의 표시 텍스트
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_header_menu_items', 'my_custom_header_menu_items');
  function my_custom_header_menu_items($menu_items) {
    $menu_items['my-custom-link'] = array(
        'title' => 'Custom Link',
        'url' => '/custom-page/',
        'current' => false,
    );
    return $menu_items;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다. 반환된 메뉴 항목 배열은 헤더 메뉴 렌더링에 사용됩니다.
- **관련 훅**: `cosmosfarm_members_header_menu_current_page` (현재 페이지 결정)
