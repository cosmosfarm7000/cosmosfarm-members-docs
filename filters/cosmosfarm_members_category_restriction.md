# cosmosfarm_members_category_restriction

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members.class.php:2241`
- **실행 시점**: 게시물 접근 제한을 확인할 때 각 카테고리의 제한 설정을 필터링합니다. 카테고리별 접근 권한을 동적으로 제어할 수 있습니다.
- **인자 정보**:
  - `$category_restriction (string)`: 카테고리의 메타 데이터에서 가져온 접근 제한 설정 값. 가능한 값은 빈 문자열("")로 전체 공개를 의미하거나, "1"로 선택된 사용자 역할만 접근을 허용하는 제한 설정을 의미합니다. 필터 함수에서 이 값을 변경하여 카테고리의 접근 제한을 동적으로 조정할 수 있습니다.
  - `$category (WP_Term)`: 현재 확인 중인 카테고리 객체. term_id, name, slug, description 등의 표준 속성과 함께 카테고리별 메타 데이터를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_category_restriction', 'my_custom_category_restriction_logic', 10, 2);
  function my_custom_category_restriction_logic($category_restriction, $category) {
      // 특정 카테고리(ID: 5)는 항상 제한
      if ($category->term_id === 5) {
          return '1'; // 제한 활성화
      }
      
      // 프리미엄 카테고리는 로그인한 사용자만
      if (strpos($category->slug, 'premium') !== false && !is_user_logged_in()) {
          return '1';
      }
      
      return $category_restriction;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 문자열 값을 반환해야 합니다. 빈 문자열은 제한 없음, "1"은 제한 있음을 의미합니다.
- **관련 훅**: `cosmosfarm_members_page_restriction`
