# cosmosfarm_members_use_login_timeout

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 로그인 타임아웃 기능을 사용할지 여부를 결정할 때 옵션 값을 필터링합니다.
- **인자 정보**:
  - `$use_login_timeout_option_value (string)`: 자동 로그아웃 설정 시간 옵션 값.
  - `$option (Cosmosfarm_Members_Option)`: 코스모스팜 회원관리 옵션 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_use_login_timeout', 'my_custom_login_timeout_setting', 10, 2);
    function my_custom_login_timeout_setting($use_login_timeout_option_value, $option) {
        return false; // 로그인 타임아웃 기능 비활성화
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
