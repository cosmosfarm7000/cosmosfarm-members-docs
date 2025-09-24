# cosmosfarm_members_localize_strings

- **분류**: Filter
- **정의 위치**: `cosmosfarm-members.php:539`
- **실행 지점**: cosmosfarm_members_scripts() 함수 내부에서 `$localize` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$localize (mixed)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_localize_strings', function($localize) {
    // 값 수정
    return $localize;
});
  ```

- **주의 사항**: 콜백은 항상 `$localize` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: 없음
