# cosmosfarm_members_template_account_links

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 계정 링크 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$args (array)`: 템플릿에 전달되는 인수 배열.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_account_links', 'my_custom_account_links_template', 10, 2);
    function my_custom_account_links_template($file_path, $args) {
        return get_stylesheet_directory() . '/cosmosfarm-members/account-links.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
