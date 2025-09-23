# cosmosfarm_members_subscription_request_pay_result

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 구독 결제 요청 결과를 필터링합니다.
- **인자 정보**:
  - `$result (mixed)`: 파라미터 1
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_request_pay_result', 'my_custom_pay_request_result');
  function my_custom_pay_request_result($result) {
    if ($result->success) {
        error_log('결제 요청 성공!');
    }
    return $result;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
