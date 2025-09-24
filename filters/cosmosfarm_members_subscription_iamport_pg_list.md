# cosmosfarm_members_subscription_iamport_pg_list

- **분류**: Filter
- **정의 위치**: `cosmosfarm-members.php:1094`
- **실행 지점**: get_cosmosfarm_members_subscription_iamport_pg_list() 함수 내부에서 `$iamport_pg_list` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$iamport_pg_list (array)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_subscription_iamport_pg_list', function($iamport_pg_list) {
    // 값 수정
    return $iamport_pg_list;
});
  ```

- **주의 사항**: 콜백은 항상 `$iamport_pg_list` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: 없음
