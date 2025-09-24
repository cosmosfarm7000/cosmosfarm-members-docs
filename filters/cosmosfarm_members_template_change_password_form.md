# cosmosfarm_members_template_change_password_form

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:211`
- **실행 시점**: 비밀번호 변경 폼 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$action (string)`: 현재 액션 (예: 'change_password').
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_change_password_form', 'my_custom_change_password_form_template', 10, 2);
    function my_custom_change_password_form_template($file_path, $action) {
        return get_stylesheet_directory() . '/cosmosfarm-members/change-password-form.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
