# cosmosfarm_members_sms_send_data

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Sms.class.php:42`
- **실행 지점**: Cosmosfarm_Members_Sms::send() 메서드 내부에서 `$phone` 값을 필터링할 수 있도록 호출됩니다.
- **파라미터 정보**:
  - `$phone (mixed)`: 필터 적용 전의 기본 값입니다. 반환 시 이 값을 원하는 형태로 수정해 돌려주세요.
  - `$user_id (int)`: 필터 처리에 참고할 수 있는 추가 컨텍스트 값입니다.
- **예제 코드**:
  ```php
  add_filter('cosmosfarm_members_sms_send_data', function($phone, $user_id) {
    // 값 수정
    return $phone;
}, 10, 2);
  ```

- **주의 사항**: 콜백은 항상 `$phone` 값을 반환해야 하며, 가능한 한 원래 자료형을 유지하는 것이 좋습니다.
- **관련 항목**: 없음
