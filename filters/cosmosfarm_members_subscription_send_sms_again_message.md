# cosmosfarm_members_subscription_send_sms_again_message

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members.class.php`
- **실행 시점**: 구독 상품의 정기결제 재결제 성공 시 발송되는 SMS 메시지를 필터링합니다.
- **인자 정보**:
  - `$sms (mixed)`: 파라미터 1
  - `$order (mixed)`: 파라미터 2
  - `$product (mixed)`: 파라미터 3
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_send_sms_again_message', 'my_custom_sms_again_message', 10, 3);
    function my_custom_sms_again_message($sms, $order, $product) {
        $sms['content'] = '[재결제 알림] ' . $product->name() . ' 상품 재결제가 완료되었습니다.';
        return $sms;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
