# cosmosfarm_members_subscription_again_failure_email_args

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4782`
- **실행 시점**: 구독 재결제가 실패한 경우 발송될 이메일 내용을 설정할 때 실행됩니다. 재결제 실패 알림 이메일의 제목과 내용을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$args (array)`: 이메일 발송에 사용될 인수 배열. 'to' (수신자 이메일), 'subject' (제목), 'message' (내용) 등의 키를 포함합니다.
  - `$old_order (Cosmosfarm_Members_Subscription_Order)`: 이전 구독 주문 객체.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 재결제 대상 상품 객체.
  - `$subscribe_result (object)`: 구독 결과 객체 (error_message 속성 포함).
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_again_failure_email_args', 'my_custom_again_failure_email_args', 10, 4);
  function my_custom_again_failure_email_args($args, $old_order, $product, $subscribe_result) {
    $args['subject'] = '[중요] 구독 재결제 실패 알림';
    return $args;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 이메일 인수 배열을 반환해야 합니다. 'to', 'subject', 'message' 키를 포함하는 배열 구조를 유지해야 합니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_price`, `cosmosfarm_members_subscription_again_point_to_apply`
