# cosmosfarm_members_template_login_timeout_popup

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 
- **인자 정보**:
  - `$file_path (mixed)`: 파라미터 1
  - `$login_timeout_url (mixed)`: 파라미터 2
  - `$login_timeout (mixed)`: 파라미터 3
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_template_login_timeout_popup', 'my_custom_login_timeout_popup_template');
    function my_custom_login_timeout_popup_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/login-timeout-popup.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
