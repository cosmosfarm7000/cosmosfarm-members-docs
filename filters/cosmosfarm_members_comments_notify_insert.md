# cosmosfarm_members_comments_notify_insert

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_KBoard.class.php:154`
- **실행 시점**: KBoard 게시판에서 댓글 알림을 발송하기 전에 알림 데이터를 필터링합니다. 댓글 작성 시 생성되는 알림의 내용과 대상을 수정할 수 있습니다.
- **인자 정보**:
  - `$notification (array)`: 알림 데이터 배열. 다음과 같은 키를 포함합니다: 'to_user_id'(알림을 받을 사용자 ID), 'title'(알림 제목), 'content'(알림 내용), 'item_type'(알림 유형, 기본값 'default'), 'meta_input'(추가 메타 데이터로 url과 url_name 포함). 이 배열을 수정하여 알림의 내용이나 대상을 변경할 수 있습니다.
  - `$comment_uid (int)`: 새로 달린 댓글의 고유 ID. KBoard에서 댓글을 식별하는 값입니다.
  - `$content_uid (int)`: 댓글이 달린 게시글의 고유 ID. KBoard에서 게시글을 식별하는 값입니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 ID, 제목, 설정 등의 정보를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_comments_notify_insert', 'my_custom_comments_notify_insert', 10, 4);
  function my_custom_comments_notify_insert($notification, $comment_uid, $content_uid, $board) {
      // 특정 게시판에서는 알림 제목 변경
      if ($board->id == 5) {
          $notification['title'] = '[중요] 새로운 댓글이 달렸습니다';
      }
      
      // 알림에 게시글 링크 추가
      $notification['meta_input']['url'] = get_permalink($content_uid);
      $notification['meta_input']['url_name'] = '게시글 보기';
      
      // 관리자에게는 추가 알림
      if (current_user_can('administrator')) {
          $notification['content'] .= ' (관리자 확인 필요)';
      }
      
      return $notification;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 알림 배열을 반환해야 합니다. 알림 데이터를 변경할 때는 사용자 경험과 보안을 고려해야 합니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_display`, `cosmosfarm_members_comments_notify_default`
