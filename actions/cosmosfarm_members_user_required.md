# cosmosfarm_members_user_required

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:1695`
- **실행 시점**: `Cosmosfarm_Members::user_required()`가 필수 사용자 정보 검사를 모두 통과한 직후 호출됩니다. 기본 검사에서 누락된 항목이 있을 경우 이 훅까지 도달하지 않으므로, 모든 필수 정보가 충족됐을 때 후속 처리를 연결할 수 있습니다.
- **인자 정보**:
  - `$current_user (WP_User)`: 검사를 통과한 현재 사용자 객체입니다. `ID`, `user_email`, `roles` 등 기본 속성과 `get_user_meta()`를 함께 사용해 추가 정보를 읽거나 갱신할 수 있습니다.
  - `$profile_url (string)`: 플러그인이 사용하는 프로필 편집 URL입니다. 안내 메시지나 추가 액션 링크를 만들 때 재사용할 수 있습니다.
- **예제 코드**:
  ```php
  // 필수 정보 입력을 완료한 사용자를 기록하고 알림 배지를 숨긴다.
  add_action('cosmosfarm_members_user_required', function ($current_user, $profile_url) {
      if (!get_user_meta($current_user->ID, '_required_fields_completed', true)) {
          update_user_meta($current_user->ID, '_required_fields_completed', current_time('mysql'));
      }

      // 대시보드 위젯에서 사용할 트랜지언트를 제거한다.
      delete_transient('members_required_notice_' . $current_user->ID);
  }, 10, 2);
  ```
- **주의 사항**:
  - 이 훅은 매 페이지 뷰마다 실행될 수 있으므로(조건 충족 시), 무거운 작업은 캐싱하거나 비동기 처리로 분리하세요.
  - 프로필 페이지로 다시 리다이렉션하면 무한 루프가 발생할 수 있으므로, 필수 입력 완료 이후에는 리다이렉션 대신 상태 플래그를 기록하는 방식을 권장합니다.
  - 사용자 메타를 업데이트할 때는 다른 워크플로(예: 회원가입, 결제)와 충돌하지 않는 키를 사용하세요.
- **관련 훅**: `cosmosfarm_members_pre_user_required`, `wp_footer`, `wpmem_register_fields_arr`
