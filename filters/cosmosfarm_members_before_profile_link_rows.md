# cosmosfarm_members_before_profile_link_rows

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Page_Builder.class.php:461`
- **실행 지점**: Cosmosfarm_Members_Page_Builder::member_links_args() 메서드 내부에서 `$rows` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$rows (array)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_before_profile_link_rows', function($rows) {
    // 값 수정
    return $rows;
});
  ```

- **주의 사항**: 콜백은 항상 `$rows` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: `cosmosfarm_members_after_profile_link_rows`
