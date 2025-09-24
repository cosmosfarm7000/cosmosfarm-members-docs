# cosmosfarm_members_subscription_order_again_error_notice

- **분류**: Filter
- **정의 위치**: `cosmosfarm-members.php:620`
- **실행 지점**: cosmosfarm_members_admin_notices() 함수 내부에서 `$error_notice` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$error_notice (mixed)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
  - `$order (mixed)`: 필터 처리에 참고할 수 있는 추가 컨텍스트 값입니다.
  - `$row1 (mixed)`: 필터 처리에 참고할 수 있는 추가 컨텍스트 값입니다.
  - `$row2 (mixed)`: 필터 처리에 참고할 수 있는 추가 컨텍스트 값입니다.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_subscription_order_again_error_notice', function($error_notice, $order, $row1, $row2) {
    // 값 수정
    return $error_notice;
}, 10, 4);
  ```

- **주의 사항**: 콜백은 항상 `$error_notice` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: 없음
