# cosmosfarm_members_messages_send_result

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:5509`
- **실행 시점**: 사용자가 메시지를 발송한 후, 발송 결과를 처리할 때 실행됩니다. 메시지 발송 성공/실패 상태를 필터링할 수 있습니다.
- **인자 정보**:
  - `$result (object)`: 메시지 발송 결과 객체. success (bool), message (string) 등의 속성을 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_messages_send_result', 'my_custom_messages_send_result');
  function my_custom_messages_send_result($result) {
    if ($result->success) {
        error_log('메시지 발송 성공!');
    }
    return $result;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 결과 객체를 반환해야 합니다. 결과 객체의 구조를 변경할 때는 success와 message 속성을 유지하는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_messages_read_result`, `cosmosfarm_members_messages_delete_result`
