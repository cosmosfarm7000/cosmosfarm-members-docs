# cosmosfarm_members_subscription_register_card_result

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3375`
- **실행 시점**: 카드 등록이 완료된 후, 결과가 반환되기 전에 실행됩니다. 결제 수단 등록 과정에서 카드 등록 결과를 필터링할 수 있습니다.
- **인자 정보**:
  - `$result (object|array)`: 카드 등록 결과를 담은 객체 또는 배열입니다. 일반적으로 다음과 같은 속성을 포함합니다:
    - `result (string)`: 등록 결과 상태 ('success' 또는 'error')
    - `message (string)`: 성공 또는 실패에 대한 메시지
    - 기타 PG사별 추가 속성 (예: imp_uid, customer_uid 등)
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_register_card_result', 'my_custom_register_card_result', 10, 1);
  function my_custom_register_card_result($result) {
      // 등록 결과에 따라 추가 처리
      if (isset($result->result) && $result->result === 'success') {
          // 성공 시 추가 로깅 또는 처리
          error_log('카드 등록 성공: ' . $result->message);
          
          // 필요시 결과 수정
          $result->message = '카드가 성공적으로 등록되었습니다.';
      } else {
          // 실패 시 추가 처리
          error_log('카드 등록 실패: ' . $result->message);
      }
      
      return $result;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 $result를 반환해야 합니다. 이 필터를 통해 카드 등록 결과를 변경하거나 추가 처리를 수행할 수 있습니다.
- **관련 훅**: `cosmosfarm_members_subscription_billing_key_pre_delete`, `cosmosfarm_members_subscription_billing_key_post_delete`
