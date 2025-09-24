# cosmosfarm_members_template_user_profile

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 사용자 프로필 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_user_profile', 'my_custom_user_profile_template');
    function my_custom_user_profile_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/user-profile.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
