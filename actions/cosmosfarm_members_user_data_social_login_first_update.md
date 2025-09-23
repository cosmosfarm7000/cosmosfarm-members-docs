# cosmosfarm_members_user_data_social_login_first_update

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:1808`
- **실행 시점**: `Cosmosfarm_Members::pre_update_data()`가 실행될 때, 사용자 메타 `social_login_first_update` 값이 존재하면 한 번만 호출됩니다. 소셜 로그인 사용자가 프로필을 처음 저장하는 시점(필수 정보 보완 직후 등)에 트리거되며, 훅 실행 직후 해당 메타는 삭제됩니다.
- **인자 정보**:
  - `$current_user (WP_User)`: 현재 저장 중인 사용자 객체입니다. `ID`, `user_email`, `user_login`, `roles` 등 기본 속성과 `get_user_meta()`를 조합해 추가 데이터를 가져올 수 있습니다. WP_User는 참조로 전달되므로, `set_role()` 같은 메서드를 호출하면 즉시 반영됩니다.
- **예제 코드**:

  ```php
  // 소셜 로그인 사용자가 필수 정보를 처음 저장했을 때 환영 이메일을 발송한다.
  add_action('cosmosfarm_members_user_data_social_login_first_update', function ($current_user) {
      if (!$current_user instanceof WP_User) {
          return;
      }
  
      $email = $current_user->user_email;
      if (!$email) {
          return;
      }
  
      wp_mail(
          $email,
          __('Welcome to our premium membership!', 'textdomain'),
          sprintf(__('Hi %s, your membership profile is now complete. Enjoy premium benefits!', 'textdomain'), $current_user->display_name)
      );
  
      update_user_meta($current_user->ID, '_welcome_mail_sent', current_time('mysql'));
  });
  ```
- **주의 사항**:
  - 훅이 실행된 직후 `social_login_first_update` 메타가 제거되므로, 반복 실행이 필요하면 별도의 사용자 메타 플래그를 사용해 상태를 추적하세요.
  - WP_User 객체는 실시간으로 갱신 중인 데이터가 포함되므로, 아직 데이터베이스에 저장되지 않은 값이 있을 수 있습니다. 필요한 경우 `get_user_meta()`로 최신 값을 직접 조회하세요.
  - 무거운 작업(외부 API 호출 등)은 비동기 큐(`wp_schedule_single_event`)로 넘겨 페이지 저장 속도를 저하시켜지 않도록 합니다.
- **관련 훅**: `cosmosfarm_members_user_data_social_login_update`, `pre_update_data`, `wpmem_post_register_data`
