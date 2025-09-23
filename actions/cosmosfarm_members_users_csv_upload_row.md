# cosmosfarm_members_users_csv_upload_row

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2581`
- **실행 시점**: 회원 CSV 업로드가 각 행을 처리할 때마다 호출됩니다. 새로운 사용자 생성 케이스와 기존 사용자 업데이트 케이스 두 지점에서 실행됩니다.
- **인자 정보**:
  - `$user_id (int)`: 생성되었거나 업데이트된 워드프레스 사용자 ID입니다.
  - `$row (array)`: 현재 CSV 행 데이터(머리글 키를 기준으로 매핑)가 전달됩니다. 커스텀 필드나 추가 메타 값이 포함될 수 있습니다.
- **예제 코드**:

  ```php
  // 업로드한 사용자에게 환영 이메일을 발송하고 메타를 기록한다.
  add_action('cosmosfarm_members_users_csv_upload_row', function ($user_id, $row) {
      if (!$user_id) {
          return;
      }
  
      $email = get_user_meta($user_id, 'user_email', true) ?: get_userdata($user_id)->user_email;
      if ($email && empty($row['welcome_email_sent'])) {
          wp_mail(
              $email,
              __('CSV Import Completed', 'textdomain'),
              __('Your account information has been updated via CSV import.', 'textdomain')
          );
      }
  
      update_user_meta($user_id, '_csv_imported_at', current_time('mysql'));
  }, 10, 2);
  ```
- **주의 사항**:
  - 훅은 수많은 행에서 반복 호출되므로, 무거운 작업이나 원격 API 호출은 큐로 넘기거나 캐싱해 속도를 유지하세요.
  - `$row`에는 필드 헤더 이름 그대로 값이 들어 있으므로, 존재 여부를 `isset()`으로 확인한 뒤 사용하는 것이 안전합니다.
  - 사용자 메타를 대량 수정할 경우 `update_user_meta()` 호출 수를 줄이기 위해 `update_user_meta` 대신 `update_user_metadata` 등에 한 번에 처리하는 것도 방법입니다.
- **관련 훅**: `cosmosfarm_members_pre_users_csv_upload`, `cosmosfarm_members_pre_order_upload`
