# cosmosfarm_members_messages_subnotify_sms_args

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Message.class.php`
- **실행 시점**: 메시지 알림이 발송될 때 SMS 내용을 설정할 때 실행됩니다. 메시지 알림을 SMS로 보낼 때 사용되는 내용을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$sms_args (array)`: SMS 발송에 사용될 인수 배열. 'content' (메시지 내용), 수신자 정보 등의 데이터를 포함합니다.
  - `$message_object (Cosmosfarm_Members_Message)`: 메시지 객체. 메시지 내용, 발신자, 수신자 등의 정보를 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_messages_subnotify_sms_args', 'my_custom_messages_sms_args', 10, 2);
function my_custom_messages_sms_args($sms_args, $message_object) {
    $sms_args['content'] = '[새 메시지] ' . $sms_args['content'];
    return $sms_args;
}
```

- **주의 사항**: 필터 함수는 반드시 SMS 인수 배열을 반환해야 합니다. 'content' 키를 포함하는 배열 구조를 유지해야 합니다.
- **관련 훅**: `cosmosfarm_members_messages_subnotify_email_args`, `cosmosfarm_members_messages_subnotify_alimtalk_args`
