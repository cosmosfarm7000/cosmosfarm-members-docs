# cosmosfarm_members_kboard_notify_comments_insert

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php:98`
- **실행 시점**: KBoard 게시판에 댓글이 삽입될 때, 알림 데이터를 생성하기 전에 실행됩니다. 댓글 작성 시 발송될 알림의 내용을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$notification (array)`: 알림 데이터 배열. 알림 제목, 내용, 수신자 등의 정보를 포함합니다.
  - `$comment_uid (int)`: 삽입된 댓글의 고유 ID
  - `$content_uid (int)`: 댓글이 달린 게시물의 고유 ID
  - `$board (object)`: KBoard 게시판 객체. 게시판 설정과 정보를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_kboard_notify_comments_insert', 'my_custom_kboard_notify_comments_insert', 10, 4);
  function my_custom_kboard_notify_comments_insert($notification, $comment_uid, $content_uid, $board) {
    $notification['custom_data'] = 'comment_inserted';
    return $notification;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 알림 데이터 배열을 반환해야 합니다. 알림 데이터의 구조를 변경할 때는 기존 키를 유지하는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_kboard_notify_document_insert`, `cosmosfarm_members_comments_notify_insert`
