# cosmosfarm_members_subscription_update_result

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4874`
- **실행 시점**: 구독 업데이트 결과를 필터링합니다.
- **인자 정보**:
  - `$result (array)`: 구독 업데이트 결과 배열. 'result' (string, 'success' 또는 'error'), 'message' (string), 'order_id' (int), 'subscription_active' (bool) 등의 키를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_update_result', 'my_custom_subscription_update_result');
  function my_custom_subscription_update_result($result) {
    if (isset($result['result']) && $result['result'] === 'success') {
        error_log('구독 업데이트 성공!');
    } else {
        error_log('구독 업데이트 실패: ' . (isset($result['message']) ? $result['message'] : 'Unknown error'));
    }
    return $result;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
