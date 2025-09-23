# cosmosfarm_members_comments_notify_default

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_KBoard.class.php`
- **실행 시점**: KBoard 게시판에서 댓글 알림의 기본 활성화 여부를 확인할 때 실행됩니다.
- **인자 정보**:
  - `$default (bool)`: 댓글 알림의 기본 활성화 상태. 기본값은 true입니다.
  - `$board (object)`: KBoard 게시판 객체. 게시판의 설정과 정보를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_comments_notify_default', 'my_custom_comments_notify_default', 10, 2);
    function my_custom_comments_notify_default($default, $board) {
        return $default;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
