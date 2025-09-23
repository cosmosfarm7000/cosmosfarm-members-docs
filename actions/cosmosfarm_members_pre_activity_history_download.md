# cosmosfarm_members_pre_activity_history_download

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:293`
- **실행 시점**: 관리자에서 활동 내역 CSV 다운로드를 시작할 때(`Cosmosfarm_Members_Controller::activity_history_download()`가 nonce를 검증한 직후) 호출됩니다. CSV 헤더와 데이터가 출력되기 전에 실행되므로, 대량 데이터 준비나 헤더 추가를 안정적으로 수행할 수 있습니다.
- **인자 정보**:
  - *(없음)* 추가 인자를 전달하지 않습니다.
- **예제 코드**:

  ```php
  // 다운로드 전에 필터 조건을 강제로 추가한다.
  add_action('cosmosfarm_members_pre_activity_history_download', function () {
      if (!current_user_can('manage_cosmosfarm_members')) {
          wp_die(__('You do not have permission to export activity logs.', 'textdomain'));
      }
  
      // 최근 30일 이내 활동만 CSV로 내보내도록 WHERE 절을 주입한다.
      add_filter('query', function ($query) {
          global $wpdb;
          if (strpos($query, $wpdb->prefix . 'cosmosfarm_members_activity_history') !== false) {
              $condition = "AND activity_history_datetime >= DATE_SUB(NOW(), INTERVAL 30 DAY)";
              $query = str_replace('WHERE 1=1', 'WHERE 1=1 ' . $condition, $query);
          }
          return $query;
      });
  });
  ```
- **주의 사항**:
  - CSV 출력이 바로 이어지므로, `echo`나 `var_dump` 같은 디버그 출력은 파일 형식을 깨뜨릴 수 있습니다.
  - 대량 데이터를 준비하는 경우 `set_time_limit()`이나 캐시 비우기와 충돌하지 않도록 자체적으로 처리 시간을 관리하세요.
  - 다운로드가 보안 민감하므로, 추가 권한 검사를 수행할 때는 `current_user_can('manage_cosmosfarm_members')` 또는 커스텀 capability를 재검증하세요.
- **관련 훅**: `cosmosfarm_members_pre_users_csv_download`, `cosmosfarm_members_pre_users_csv_upload`
