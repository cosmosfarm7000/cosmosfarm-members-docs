# cosmosfarm_members_use_login_timeout

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 
- **인자 정보**:
  - `$option (mixed)`: 파라미터 1
  - `$option (mixed)`: 파라미터 2
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_use_login_timeout', 'my_custom_login_timeout_setting');
    function my_custom_login_timeout_setting($use_login_timeout) {
        return false; // 로그인 타임아웃 기능 비활성화
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
