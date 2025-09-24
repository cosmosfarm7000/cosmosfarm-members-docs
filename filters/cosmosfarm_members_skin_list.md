# cosmosfarm_members_skin_list

- **분류**: Filter
- **정의 위치**: `cosmosfarm-members.php:1598`
- **실행 지점**: cosmosfarm_members_skins() 함수 내부에서 `$ist` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$ist (mixed)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_skin_list', function($ist) {
    // 값 수정
    return $ist;
});
  ```

- **주의 사항**: 콜백은 항상 `$ist` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: 없음
