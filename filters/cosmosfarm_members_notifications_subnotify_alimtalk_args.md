# cosmosfarm_members_notifications_subnotify_alimtalk_args

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Notification.class.php`
- **실행 시점**: 알림이 발송될 때 알림톡 템플릿과 파라미터를 설정할 때 실행됩니다. 알림을 알림톡으로 보낼 때 사용되는 템플릿과 데이터를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$alimtalk_args (array)`: 알림톡 발송에 사용될 인수 배열. templateCode, 파라미터 등의 정보를 포함합니다.
  - `$notification_object (Cosmosfarm_Members_Notification)`: 알림 객체. 알림 내용, 수신자 등의 정보를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_notifications_subnotify_alimtalk_args', 'my_custom_notifications_alimtalk_args', 10, 2);
  function my_custom_notifications_alimtalk_args($alimtalk_args, $notification_object) {
    $alimtalk_args['templateCode'] = 'MY_CUSTOM_NOTIFICATION_TEMPLATE';
    return $alimtalk_args;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 알림톡 인수 배열을 반환해야 합니다. templateCode와 필요한 파라미터를 올바르게 설정해야 합니다.
- **관련 훅**: `cosmosfarm_members_notifications_subnotify_email_args`, `cosmosfarm_members_notifications_subnotify_sms_args`
