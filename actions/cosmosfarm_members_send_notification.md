# cosmosfarm_members_send_notification

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Notification.class.php:138`
- **실행 시점**: 알림(`Cosmosfarm_Members_Notification::create()`)이 저장되고 사용자 구독 알림(이메일/SMS/알림톡)이 처리된 직후 호출됩니다.
- **인자 정보**:
  - `$notification (Cosmosfarm_Members_Notification)`: 방금 생성된 알림 객체입니다. `post_id`, `user_id`, `get_from_user_id()`, `get_type()` 등을 통해 세부 정보를 조회할 수 있습니다.
- **예제 코드**:
  ```php
  // 알림 생성 후 외부 모바일 푸시 서비스로 전달한다.
  add_action('cosmosfarm_members_send_notification', function ($notification) {
      $to_user_id = $notification->get_to_user_id();
      $payload = array(
          'title'   => $notification->post->post_title,
          'message' => wp_strip_all_tags($notification->post->post_content),
          'user_id' => $to_user_id,
      );
      wp_remote_post('https://push.example.com/api/send', array(
          'timeout' => 3,
          'body'    => wp_json_encode($payload),
          'headers' => array('Content-Type' => 'application/json'),
      ));
  });
  ```
- **주의 사항**:
  - 알림 본문에는 HTML이 포함될 수 있으므로, 외부 서비스 전송 전에 정제하세요.
  - `is_user_subnotify` 설정에 따라 이메일/SMS가 이미 발송되었을 수 있으니 중복 발송을 피하기 위해 메타 플래그를 사용하세요.
- **관련 훅**: `cosmosfarm_members_mail_send`, `cosmosfarm_members_send_message`, `cosmosfarm_members_subscription_notification_execute`
