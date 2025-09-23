# cosmosfarm_members_send_message

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Message.class.php:136`
- **실행 시점**: 쪽지/메시지(`Cosmosfarm_Members_Message::create()`)가 데이터베이스에 저장되고 알림 설정이 처리된 직후 호출됩니다.
- **인자 정보**:
  - `$message (Cosmosfarm_Members_Message)`: 방금 생성된 메시지 객체입니다. `post_id`, `user_id`, `get_from_user_id()`, `get_to_user_id()` 등의 메서드로 세부 정보를 조회할 수 있습니다.
- **예제 코드**:

  ```php
  // 메시지 생성 후 슬랙 알림을 보낸다.
  add_action('cosmosfarm_members_send_message', function ($message) {
      $payload = array(
          'text' => sprintf(
              'New message from %s to %s: %s',
              get_userdata($message->get_from_user_id())->user_login,
              get_userdata($message->get_to_user_id())->user_login,
              wp_strip_all_tags($message->post->post_title)
          )
      );
      wp_remote_post('https://hooks.slack.com/services/XXX', array(
          'timeout' => 2,
          'body'    => wp_json_encode($payload),
          'headers' => array('Content-Type' => 'application/json'),
      ));
  });
  ```
- **주의 사항**:
  - 메시지 본문에는 HTML이 포함될 수 있으므로, 외부 시스템 전송 시 `wp_strip_all_tags()` 등으로 정제하세요.
  - 알림 중복을 피하려면 수신자 설정(`is_user_subnotify`)과 연동하여 조건을 분기하세요.
- **관련 훅**: `cosmosfarm_members_mail_send`, `cosmosfarm_members_send_notification`
