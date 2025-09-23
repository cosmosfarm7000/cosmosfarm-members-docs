# cosmosfarm_members_subscription_billing_key_pre_delete

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4966`
- **실행 시점**: 사용자의 결제 빌링 키를 삭제하기 직전에 호출됩니다. `Cosmosfarm_Members_Controller::subscription_billing_key_delete()`에서 결제 모듈에 삭제 요청을 보내기 전에 실행됩니다.
- **인자 정보**:
  - `$user_id (int)`: 빌링 키가 삭제될 사용자 ID입니다.
- **예제 코드**:

  ```php
  // 빌링 키 삭제 전에 외부 PG에 로그를 남긴다.
  add_action('cosmosfarm_members_subscription_billing_key_pre_delete', function ($user_id) {
      $billing_key = get_user_meta($user_id, 'cosmosfarm_members_subscription_billing_key', true);
      if ($billing_key) {
          error_log(sprintf('[Billing] Pre-delete billing key %s for user #%d', $billing_key, $user_id));
      }
  });
  ```
- **주의 사항**:
  - 빌링 키 삭제를 중단하려면 `wp_die()` 또는 예외 로직을 추가할 수 있지만, 사용자에게 명확한 이유를 설명해야 합니다.
  - 외부 PG API를 호출해 실제 키 삭제를 진행하는 경우, 해당 API 오류를 처리할 준비를 하세요.
- **관련 훅**: `cosmosfarm_members_subscription_billing_key_post_delete`, `cosmosfarm_members_subscription_expiry`
