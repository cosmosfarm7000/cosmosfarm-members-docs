# cosmosfarm_members_comments_notify_display

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_KBoard.class.php`class/Cosmosfarm_Members_KBoard.class.php``
- **실행 시점**: KBoard 게시판에서 댓글 알림 옵션 체크박스를 표시할지 여부를 결정할 때 실행됩니다.
- **인자 정보**:
  - `$display (bool)`: 댓글 알림 체크박스의 표시 여부. 기본적으로 로그인한 사용자에게만 표시됩니다.
  - `$content (KBContent)`: 현재 게시글 객체. 게시글의 내용과 정보를 포함합니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 설정과 정보를 포함합니다.
  - `$builder (object)`: KBoard 빌더 객체. 폼 빌더 관련 정보를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_comments_notify_display', 'my_custom_comments_notify_display', 10, 4);
function my_custom_comments_notify_display($display, $content, $board, $builder) {
    return $display;
}
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
