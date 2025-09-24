# cosmosfarm_members_template_messages

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 메시지 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$to_user_id (int)`: 메시지를 받는 사용자 ID.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_messages', 'my_custom_messages_template', 10, 2);
    function my_custom_messages_template($file_path, $to_user_id) {
        return get_stylesheet_directory() . '/cosmosfarm-members/messages.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
