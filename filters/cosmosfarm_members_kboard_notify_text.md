# cosmosfarm_members_kboard_notify_text

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php`
- **실행 시점**: KBoard 게시판에서 알림 신청 버튼이나 텍스트를 표시할 때 실행됩니다. 알림 관련 텍스트를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$text (string)`: 알림 텍스트. 기본적으로 "Notify me of new comments" 등의 번역된 텍스트입니다.
  - `$content (object)`: KBoard 게시물 객체. 게시물 제목, 내용 등의 정보를 포함합니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판 설정과 정보를 포함합니다.
  - `$builder (object)`: 페이지 빌더 객체. 레이아웃과 관련된 정보를 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_kboard_notify_text', 'my_custom_kboard_notify_text', 10, 4);
function my_custom_kboard_notify_text($text, $content, $board, $builder) {
    return '새로운 댓글 알림 받기';
}
```

- **주의 사항**: 필터 함수는 반드시 문자열을 반환해야 합니다. 반환된 텍스트는 알림 신청 UI에 표시됩니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_text`
