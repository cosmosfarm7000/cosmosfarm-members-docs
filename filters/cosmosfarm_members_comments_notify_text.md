# cosmosfarm_members_comments_notify_text

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php:122`
- **실행 시점**: KBoard 게시판에서 댓글 알림 체크박스의 표시 텍스트를 필터링합니다. 댓글 작성 시 표시되는 알림 동의 문구를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$text (string)`: 댓글 알림 체크박스에 표시될 텍스트. 기본값은 영어로 "Notify me of new comments"이며, 다국어 지원을 위해 __() 함수로 감싸져 있습니다. 이 텍스트를 변경하여 사용자에게 표시될 메시지를 커스터마이징할 수 있습니다.
  - `$content (KBContent)`: 현재 게시글 객체. 게시글의 UID, 제목, 내용 등의 정보를 포함합니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 ID, 제목, 설정 등의 정보를 포함합니다.
  - `$builder (object)`: KBoard 빌더 객체. 댓글 폼 빌더 관련 정보를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_comments_notify_text', 'my_custom_comments_notify_text', 10, 4);
  function my_custom_comments_notify_text($text, $content, $board, $builder) {
      // 게시판별로 다른 텍스트 표시
      if ($board->id == 10) {
          return '이 게시글의 새로운 댓글을 알림으로 받겠습니다.';
      }
      
      // 기본 한국어 텍스트
      return '새로운 댓글 알림을 받겠습니다.';
  }
  ```

- **주의 사항**: 필터 함수는 반드시 문자열을 반환해야 합니다. 다국어 지원을 위해 __() 함수를 사용하는 것을 권장합니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_display`
