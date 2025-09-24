# cosmosfarm_members_template_point_list

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:815`
- **실행 시점**: 포인트 내역 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_point_list', 'my_custom_point_list_template');
    function my_custom_point_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/point-list.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
