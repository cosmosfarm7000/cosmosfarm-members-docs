# cosmosfarm_members_pre_order_upload

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2080`
- **실행 시점**: 관리자에서 주문 CSV 업로드를 시작할 때(`Cosmosfarm_Members_Controller::order_upload()`가 nonce를 검증한 후) 호출됩니다. 업로드 파일을 읽고 파싱하기 바로 전에 실행됩니다.
- **인자 정보**:
  - *(없음)* 추가 인자를 전달하지 않습니다.
- **예제 코드**:
  ```php
  // 업로드 전에 파일 크기 제한과 확장자를 한 번 더 검사한다.
  add_action('cosmosfarm_members_pre_order_upload', function () {
      if (empty($_FILES['order_upload']['tmp_name'])) {
          wp_die(__('Upload file is missing.', 'textdomain'));
      }

      $size = filesize($_FILES['order_upload']['tmp_name']);
      if ($size > 5 * 1024 * 1024) {
          wp_die(__('CSV file must be smaller than 5MB.', 'textdomain'));
      }

      $ext = strtolower(pathinfo($_FILES['order_upload']['name'], PATHINFO_EXTENSION));
      if (!in_array($ext, array('csv'))) {
          wp_die(__('Only CSV files are supported.', 'textdomain'));
      }
  });
  ```
- **주의 사항**:
  - `header()`로 콘텐츠 타입이 이미 전송되었으므로, 훅 내에서 `wp_redirect()` 등 추가 헤더를 전송하면 경고가 발생할 수 있습니다.
  - 업로드 파일에 직접 접근하므로, `is_uploaded_file()` 사용 여부나 파일 확장자 검증과 같은 보안 로직을 강화하는 용도로 활용하세요.
  - 예외 상황에서 `wp_die()`를 호출하면 업로드 루틴이 중단되며, 사용자는 오류 메시지를 확인하게 됩니다.
- **관련 훅**: `cosmosfarm_members_pre_order_download`, `cosmosfarm_members_users_csv_upload_row`
