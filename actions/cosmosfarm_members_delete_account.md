# cosmosfarm_members_delete_account

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3167`
- **실행 시점**: 사용자가 탈퇴 링크(`?action=cosmosfarm_members_delete_account`)를 통해 자신의 계정을 삭제할 때 nonce 검증에 성공한 직후 호출됩니다. 이후 워드프레스 기본 `wp_delete_user()` 또는 커스텀 삭제 로직이 실행되기 전에 후속 처리를 추가할 수 있습니다.
- **인자 정보**:
  - *(없음)* 추가 인자를 전달하지 않습니다. 현재 사용자 정보는 `get_current_user_id()`로 조회할 수 있습니다.
- **예제 코드**:

  ```php
  // 탈퇴 전에 데이터를 백업하고 감사 로그를 남긴다.
  add_action('cosmosfarm_members_delete_account', function () {
      $user_id = get_current_user_id();
      if (!$user_id) {
          return;
      }
  
      $user = get_userdata($user_id);
      $backup_dir = WP_CONTENT_DIR . '/uploads/account-backup';
      wp_mkdir_p($backup_dir);
      $filename = trailingslashit($backup_dir) . 'user-' . $user_id . '-' . time() . '.json';
      file_put_contents($filename, wp_json_encode($user));
  
      error_log(sprintf('[Delete Account] %s (%d) requested account deletion.', $user->user_login, $user_id));
  });
  ```
- **주의 사항**:
  - 훅 이후 계정이 삭제되면 사용자 메타 접근이 제한되므로, 필요한 데이터는 훅 안에서 백업하거나 전송해야 합니다.
  - 외부 서비스 연동을 해제하려면 이 훅에서 API 호출을 수행하세요.
  - `wp_die()`로 탈퇴를 차단하면 사용자 경험이 떨어질 수 있으므로, 가급적 안내 메시지와 함께 리다이렉션을 제공합니다.
- **관련 훅**: `cosmosfarm_members_pre_social_login`, `cosmosfarm_members_social_login_callback`
