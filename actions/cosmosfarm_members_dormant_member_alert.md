# cosmosfarm_members_dormant_member_alert

- **분류**: Action
- **정의 위치**: `cosmosfarm-members.php`
- **실행 시점**: 휴면 회원에게 알림을 보낼 때 호출됩니다. 추가 알림이나 로깅에 사용됩니다.
- **인자 정보**:
  - `$user (WP_User)`: 휴면 회원 객체입니다.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_dormant_member_alert', 'my_custom_dormant_member_alert', 10, 1);
  function my_custom_dormant_member_alert($user) {
      // 휴면 회원에게 추가 알림 발송 등 로직
      error_log('휴면 회원 알림: ' . $user->user_login);
  }
  ```

- **주의 사항**: 알림 빈도를 조절하여 스팸 방지하세요.
- **관련 훅**: 없음
