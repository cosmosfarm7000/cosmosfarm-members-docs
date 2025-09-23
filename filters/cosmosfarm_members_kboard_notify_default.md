# cosmosfarm_members_kboard_notify_default

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_KBoard.class.php`
- **실행 시점**: KBoard 게시판의 알림 기본 설정을 가져올 때 실행됩니다. 게시판별로 알림을 활성화할지 여부를 결정하는 기본값을 필터링할 수 있습니다.
- **인자 정보**:
  - `$default (bool)`: 알림의 기본 활성화 상태. 기본적으로 true 또는 false입니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판 ID, 설정 등의 정보를 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_kboard_notify_default', 'my_custom_kboard_notify_default', 10, 2);
function my_custom_kboard_notify_default($default, $board) {
    // 특정 게시판에서는 알림을 기본적으로 비활성화
    if ($board->id === '123') {
        return false;
    }
    return $default;
}
```

- **주의 사항**: 필터 함수는 반드시 불리언 값을 반환해야 합니다. 이 값은 해당 게시판의 알림 기본 설정으로 사용됩니다.
- **관련 훅**: `cosmosfarm_members_comments_notify_default`
