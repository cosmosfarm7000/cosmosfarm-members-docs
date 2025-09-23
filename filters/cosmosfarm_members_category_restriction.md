# cosmosfarm_members_category_restriction

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members.class.php`
- **실행 시점**: 게시물의 카테고리에 설정된 접근 제한을 확인할 때, 각 카테고리에 대해 제한 여부를 필터링합니다.
- **인자 정보**:
  - `$category_restriction (string)`: 카테고리의 메타 데이터에서 가져온 접근 제한 설정 값. 빈 문자열이거나 특정 제한 값일 수 있습니다.
  - `$category (WP_Term)`: 현재 확인 중인 카테고리 객체. term_id, name, slug 등의 속성을 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_category_restriction', 'my_custom_category_restriction_logic', 10, 2);
    function my_custom_category_restriction_logic($category_restriction, $category) {
        // 특정 카테고리(ID: 5)는 항상 제한
        if ($category->term_id === 5) {
            return true;
        }
        return $category_restriction;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
