# cosmosfarm_members_pre_subscription_request_pay_result

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3454`
- **실행 시점**: 구독 결제 요청을 처리하기 전에 유효성 검사 등의 결과를 필터링할 때 실행됩니다. 결제 요청 전 검증 로직의 결과를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$result (object)`: 결제 요청 전 검증 결과 객체. success (bool), message (string) 등의 속성을 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_pre_subscription_request_pay_result', 'my_custom_pre_pay_result');
  function my_custom_pre_pay_result($result) {
    if (!$result->success) {
        $result->message = '결제 요청 전 검증 실패: ' . $result->message;
    }
    return $result;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 결과 객체를 반환해야 합니다. 결과 객체의 구조를 변경할 때는 success와 message 속성을 유지하는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_subscription_request_pay_result`
