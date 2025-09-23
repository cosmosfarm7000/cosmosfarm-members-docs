# cosmosfarm_members_subscription_billing_key_post_delete

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4974`
- **실행 시점**: 사용자의 결제 빌링 키가 성공적으로 삭제된 뒤 호출됩니다. 삭제된 빌링 키 값과 사용자 ID가 제공됩니다.
- **인자 정보**:
  - `$user_id (int)`: 빌링 키를 삭제한 사용자 ID입니다.
  - `$bid (string)`: 삭제된 빌링 키 문자열입니다.
- **예제 코드**:
  ```php
  // 빌링 키 삭제 후 외부 결제 시스템에서 토큰을 비활성화한다.
  add_action('cosmosfarm_members_subscription_billing_key_post_delete', function ($user_id, $bid) {
      if (!$bid) {
          return;
      }

      wp_remote_post('https://pg.example.com/api/token/delete', array(
          'timeout' => 5,
          'body'    => array('billing_key' => $bid),
      ));

      update_user_meta($user_id, '_billing_key_deleted_at', current_time('mysql'));
  }, 10, 2);
  ```
- **주의 사항**:
  - 삭제된 빌링 키는 더 이상 복구할 수 없으므로, 외부 시스템과의 동기화를 확실히 완료하세요.
  - 사용자에게 안내 메일이나 SMS를 보내는 경우 중복 발송을 방지하기 위해 메타 플래그를 기록해 두는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_subscription_billing_key_pre_delete`, `cosmosfarm_members_subscription_expiry`
