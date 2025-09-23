# cosmosfarm_members_subscription_register_card_result

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 
- **인자 정보**:
  - `$result (mixed)`: 파라미터 1
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_subscription_register_card_result', 'my_custom_register_card_result');
    function my_custom_register_card_result($result) {
        if (!$result->success) {
            error_log('카드 등록 실패: ' . $result->message);
        }
        return $result;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
