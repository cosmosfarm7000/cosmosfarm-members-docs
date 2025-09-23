# cosmosfarm_members_kboard_notify_display

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php`
- **실행 시점**: KBoard 게시판에서 알림 표시 여부를 결정할 때 실행됩니다. 게시물이나 댓글에 대한 알림을 표시할지 여부를 필터링할 수 있습니다.
- **인자 정보**:
  - `$display (bool)`: 알림을 표시할지 여부를 나타내는 불리언 값
  - `$content (object)`: KBoard 게시물 객체. 게시물 제목, 내용 등의 정보를 포함합니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판 설정과 정보를 포함합니다.
  - `$builder (object)`: 페이지 빌더 객체. 레이아웃과 관련된 정보를 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_kboard_notify_display', 'my_custom_kboard_notify_display', 10, 4);
function my_custom_kboard_notify_display($display, $content, $board, $builder) {
    // 특정 게시판(ID: 1)에서는 알림 비활성화
    if ($board->id === '1') {
        return false;
    }
    return $display;
}
```

- **주의 사항**: 필터 함수는 반드시 불리언 값을 반환해야 합니다. false를 반환하면 해당 게시물/댓글에 대한 알림이 표시되지 않습니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_display`
