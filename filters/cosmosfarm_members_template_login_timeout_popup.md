# cosmosfarm_members_template_login_timeout_popup

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 로그인 타임아웃 팝업 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$login_timeout_url (string)`: 로그인 타임아웃 시 리다이렉트될 URL.
  - `$login_timeout (int)`: 로그인 타임아웃 시간 (초).
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_login_timeout_popup', 'my_custom_login_timeout_popup_template', 10, 3);
    function my_custom_login_timeout_popup_template($file_path, $login_timeout_url, $login_timeout) {
        return get_stylesheet_directory() . '/cosmosfarm-members/login-timeout-popup.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
