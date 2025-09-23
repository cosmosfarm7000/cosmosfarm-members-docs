# cosmosfarm_members_template_notifications_list_item

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 
- **인자 정보**:
  - `$file_path (mixed)`: 파라미터 1
  - `$item_type (mixed)`: 파라미터 2
  - `$item (mixed)`: 파라미터 3
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_notifications_list_item', 'my_custom_notifications_list_item_template');
    function my_custom_notifications_list_item_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/notifications-list-item.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
