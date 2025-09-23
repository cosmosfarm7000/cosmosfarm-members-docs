# cosmosfarm_members_kboard_notify_document_insert

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php`
- **실행 시점**: KBoard 게시판에 새로운 문서가 삽입될 때, 알림 데이터를 생성하기 전에 실행됩니다. 새 게시물 작성 시 발송될 알림의 내용을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$notification (array)`: 알림 데이터 배열. 알림 제목, 내용, 수신자 등의 정보를 포함합니다.
  - `$content_uid (int)`: 삽입된 게시물의 고유 ID
  - `$board_id (int)`: 게시물이 속한 게시판의 ID
  - `$content (object)`: KBoard 게시물 객체. 게시물 제목, 내용 등의 정보를 포함합니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판 설정과 정보를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_kboard_notify_document_insert', 'my_custom_kboard_notify_document_insert', 10, 5);
  function my_custom_kboard_notify_document_insert($notification, $content_uid, $board_id, $content, $board) {
    // 알림 데이터에 추가 정보 삽입
    $notification['custom_data'] = 'document_inserted';
    return $notification;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 알림 데이터 배열을 반환해야 합니다. 알림 데이터의 구조를 변경할 때는 기존 키를 유지하는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_kboard_notify_comments_insert`
