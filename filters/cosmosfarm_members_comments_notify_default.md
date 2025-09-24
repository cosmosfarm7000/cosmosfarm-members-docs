# cosmosfarm_members_comments_notify_default

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php:167`
- **실행 시점**: KBoard 게시판에서 댓글 알림의 기본 활성화 상태를 필터링합니다. 게시판별로 댓글 알림의 기본 동작을 제어할 수 있습니다.
- **인자 정보**:
  - `$default (bool)`: 댓글 알림의 기본 활성화 상태. 기본값은 true로, 댓글 작성 시 알림이 기본적으로 활성화되어 있음을 의미합니다. false로 변경하면 기본적으로 알림이 비활성화됩니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 ID, 제목, 설정 등의 정보를 포함하며, 특정 게시판에 따라 알림 기본값을 다르게 설정할 때 사용할 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_comments_notify_default', 'my_custom_comments_notify_default', 10, 2);
  function my_custom_comments_notify_default($default, $board) {
      // 특정 게시판에서는 알림 기본 비활성화
      if ($board->id == 5) { // Q&A 게시판
          return false;
      }
      
      // 프리미엄 게시판에서는 알림 기본 활성화
      if (strpos($board->board_name, '프리미엄') !== false) {
          return true;
      }
      
      return $default;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 boolean 값을 반환해야 합니다. true는 알림 기본 활성화, false는 기본 비활성화를 의미합니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_display`, `cosmosfarm_members_comments_notify_insert`
