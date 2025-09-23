# cosmosfarm_members_pre_users_csv_download

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2232`
- **실행 시점**: 관리자에서 회원 CSV 다운로드(`Cosmosfarm_Members_Controller::users_csv_download()`)를 수행할 때 파일 핸들을 열기 직전에 호출됩니다. 사용자 목록을 조회하기 전에 필터를 주입하거나 보안 체크를 강화할 수 있습니다.
- **인자 정보**:
  - *(없음)* 추가 인자를 전달하지 않습니다.
- **예제 코드**:

  ```php
  // CSV 내보내기 전에 특정 역할만 허용하고 머리글을 커스터마이즈한다.
  add_action('cosmosfarm_members_pre_users_csv_download', function () {
      if (!current_user_can('list_users')) {
          wp_die(__('You do not have permission to export users.', 'textdomain'));
      }
  
      add_action('pre_user_query', function ($user_query) {
          $user_query->query_vars['role__in'] = array('subscriber', 'customer');
      });
  });
  ```
- **주의 사항**:
  - 훅 이후로는 CSV 응답이 바로 시작되므로, 디버그 출력은 피하세요.
  - `pre_user_query` 같은 필터를 추가한 경우 해당 훅 안에서만 유효하도록 `remove_action()`을 호출하거나 조건문을 사용해 다른 페이지에 영향을 주지 않도록 합니다.
  - 대량 데이터를 처리할 때는 실행 시간과 메모리 제한을 고려하세요.
- **관련 훅**: `cosmosfarm_members_pre_activity_history_download`, `cosmosfarm_members_pre_users_csv_upload`
