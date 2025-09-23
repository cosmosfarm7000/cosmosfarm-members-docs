# cosmosfarm_members_comments_notify_insert

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_KBoard.class.php`
- **실행 시점**: KBoard 게시판에서 새로운 댓글이 달렸을 때 알림을 보내기 전에 알림 데이터를 필터링합니다.
- **인자 정보**:
  - `$notification (array)`: 알림 데이터 배열. to_user_id, title, content, item_type, meta_input 등의 키를 포함합니다.
  - `$comment_uid (int)`: 새로 달린 댓글의 고유 ID.
  - `$content_uid (int)`: 댓글이 달린 게시글의 고유 ID.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 설정과 정보를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_comments_notify_insert', 'my_custom_comments_notify_insert', 10, 4);
    function my_custom_comments_notify_insert($notification, $comment_uid, $content_uid, $board) {
        return $notification;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
