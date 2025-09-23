# cosmosfarm_members_comments_notify_display

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_KBoard.class.php:117`
- **실행 시점**: KBoard 게시판에서 댓글 알림 옵션 체크박스의 표시 여부를 필터링합니다. 댓글 작성 시 알림 수신 동의 옵션을 표시할지 제어할 수 있습니다.
- **인자 정보**:
  - `$display (bool)`: 댓글 알림 체크박스의 표시 여부. 기본적으로 로그인한 사용자에게만 true로 설정되어 체크박스가 표시되며, 비로그인 사용자의 경우 false입니다. 이 값을 변경하여 특정 조건에서 알림 옵션을 표시하거나 숨길 수 있습니다.
  - `$content (KBContent)`: 현재 게시글 객체. 게시글의 UID, 제목, 내용 등의 정보를 포함하며, 게시글의 특정 속성에 따라 알림 표시 여부를 결정할 때 사용할 수 있습니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 ID, 제목, 설정 등의 정보를 포함합니다.
  - `$builder (object)`: KBoard 빌더 객체. 댓글 폼 빌더 관련 정보를 포함하며, 폼의 구조나 설정에 따라 알림 표시를 조정할 때 사용할 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_comments_notify_display', 'my_custom_comments_notify_display', 10, 4);
  function my_custom_comments_notify_display($display, $content, $board, $builder) {
      // 특정 게시판에서는 알림 옵션 숨김
      if ($board->id == 10) { // 공지사항 게시판
          return false;
      }
      
      // 특정 카테고리의 게시글에서는 알림 옵션 표시
      if (has_term('important', 'category', $content->ID)) {
          return true;
      }
      
      // 관리자에게는 항상 알림 옵션 표시
      if (current_user_can('administrator')) {
          return true;
      }
      
      return $display;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 boolean 값을 반환해야 합니다. true는 체크박스 표시, false는 숨김을 의미합니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_default`, `cosmosfarm_members_comments_notify_insert`
