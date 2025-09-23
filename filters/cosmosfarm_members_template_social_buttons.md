# cosmosfarm_members_template_social_buttons

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members.class.php`
- **실행 시점**: 소셜 로그인 버튼 템플릿 파일 경로를 결정합니다.
- **인자 정보**:
  - `$file_path (string)`: 소셜 버튼 템플릿 파일의 절대 경로
  - `$action (string)`: 액션 타입 (예: 'login', 'register')
  - `$redirect_to (string)`: 로그인 후 리다이렉트될 URL
  - `$skin (string)`: 사용 중인 스킨 이름
  - `$file (string)`: 템플릿 파일 이름 (기본값: 'social-buttons')
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_template_social_buttons', 'my_custom_social_buttons_template');
    function my_custom_social_buttons_template($file_path) {
        // 사용자 정의 소셜 버튼 템플릿 경로 반환
        return get_stylesheet_directory() . '/cosmosfarm-members/social-buttons.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
