# cosmosfarm_members_pre_users_csv_upload

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2484`
- **실행 시점**: 관리자 회원 CSV 업로드(`Cosmosfarm_Members_Controller::users_csv_upload()`)가 시작되어 업로드 파일을 열기 직전에 호출됩니다. 파일 형식 검증이나 사용자 권한 체크를 커스터마이즈할 수 있습니다.
- **인자 정보**:
  - *(없음)* 추가 인자를 전달하지 않습니다.
- **예제 코드**:
  ```php
  // 업로드 전에 첨부된 CSV를 백업 폴더에 저장한다.
  add_action('cosmosfarm_members_pre_users_csv_upload', function () {
      if (empty($_FILES['users_csv_upload']['tmp_name'])) {
          return;
      }
      $backup_dir = WP_CONTENT_DIR . '/uploads/members-csv-backup';
      wp_mkdir_p($backup_dir);
      $filename = wp_unique_filename($backup_dir, basename($_FILES['users_csv_upload']['name']));
      copy($_FILES['users_csv_upload']['tmp_name'], trailingslashit($backup_dir) . $filename);
  });
  ```
- **주의 사항**:
  - 훅 이후 즉시 CSV 파싱이 시작되므로, 파일 핸들에 영향을 주는 작업(삭제, 이동 등)을 수행할 경우 업로드가 실패할 수 있습니다.
  - 대용량 파일 업로드 시 `ini_set('memory_limit', ...)` 호출과 충돌하지 않도록 주의하세요.
  - 업로드 권한을 강화하려면 `current_user_can('manage_cosmosfarm_members')` 등 capability를 재검증하세요.
- **관련 훅**: `cosmosfarm_members_pre_users_csv_download`, `cosmosfarm_members_users_csv_upload_row`
