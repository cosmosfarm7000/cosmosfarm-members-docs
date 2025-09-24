# cosmosfarm_members_template_messages_list_item

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:508`
- **실행 시점**: 메시지 목록 항목 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$item_type (string)`: 항목 유형 (예: 'message').
  - `$item (object)`: 메시지 항목 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_messages_list_item', 'my_custom_messages_list_item_template', 10, 3);
    function my_custom_messages_list_item_template($file_path, $item_type, $item) {
        return get_stylesheet_directory() . '/cosmosfarm-members/messages-list-item.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
