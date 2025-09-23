# cosmosfarm_members_messages_subnotify_email_args

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Message.class.php`
- **실행 시점**: 메시지 알림이 발송될 때 이메일 내용을 설정할 때 실행됩니다. 메시지 알림을 이메일로 보낼 때 사용되는 제목과 내용을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$args (array)`: 이메일 발송에 사용될 인수 배열. 'to' (수신자 이메일), 'subject' (제목), 'message' (내용) 등의 키를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_messages_subnotify_email_args', 'my_custom_messages_email_args');
  function my_custom_messages_email_args($args) {
    $args['subject'] = '[새 메시지] ' . $args['subject'];
    return $args;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 이메일 인수 배열을 반환해야 합니다. 'to', 'subject', 'message' 키를 포함하는 배열 구조를 유지해야 합니다.
- **관련 훅**: `cosmosfarm_members_messages_subnotify_sms_args`, `cosmosfarm_members_messages_subnotify_alimtalk_args`
