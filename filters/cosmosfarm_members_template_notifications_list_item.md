# cosmosfarm_members_template_notifications_list_item

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:375`
- **실행 시점**: 알림 목록 항목 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$item_type (string)`: 항목 유형 (예: 'notification').
  - `$item (object)`: 알림 항목 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_notifications_list_item', 'my_custom_notifications_list_item_template', 10, 3);
    function my_custom_notifications_list_item_template($file_path, $item_type, $item) {
        return get_stylesheet_directory() . '/cosmosfarm-members/notifications-list-item.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
