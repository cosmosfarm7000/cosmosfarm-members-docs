# cosmosfarm_members_init_values_inicis_mobile

- **분류**: Filter
- **정의 위치**: `class/pg/inicis/dialog-mobile.php:17`
- **실행 지점**: 해당 파일 내에서 `$pg` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$pg (mixed)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
  - `$pg (mixed)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_init_values_inicis_mobile', function($pg, $pg) {
    // 값 수정
    return $pg;
}, 10, 2);
  ```

- **주의 사항**: 콜백은 항상 `$pg` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: 없음
