# cosmosfarm_members_subscription_notification_execute

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:5112`
- **실행 시점**: 구독 알림 발송 설정에 따라 알림이 실제로 전송되기 직전에 호출됩니다. 수신 대상과 제목/본문이 완성된 뒤, 기본 발송 로직(이메일·SMS 등)이 실행되기 전에 후처리를 추가할 수 있습니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 알림과 연결된 주문 객체입니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 해당 알림이 속한 상품 객체입니다.
  - `$subscription_notification (Cosmosfarm_Members_Subscription_Notification)`: 알림 설정 객체로, 채널·조건·템플릿 등의 정보를 포함합니다.
  - `$notification_subject (string)`: 준비된 알림 제목입니다.
  - `$notification_message (string)`: 준비된 알림 본문입니다.
- **예제 코드**:
  ```php
  // 알림 발송 전에 제목을 브랜드 규칙에 맞게 수정한다.
  add_action('cosmosfarm_members_subscription_notification_execute', function ($order, $product, $subscription_notification, &$subject, &$message) {
      $subject = '[Brand] ' . $subject;
      $message .= "\n\n" . __('Need help? Contact support@example.com', 'textdomain');
  }, 10, 5);
  ```
- **주의 사항**:
  - 훅은 기본적으로 제목과 본문의 사본을 전달하며, 참조로 넘겨받을 수 있도록 함수 시그니처를 일치시키면 수정한 값이 그대로 반영됩니다.
  - 발송 채널에 따라 허용 문자 길이가 다르므로, 메시지를 수정할 때는 SMS/알림톡 제한 길이를 고려하세요.
  - 여러 채널에 대해 반복 호출될 수 있으므로, 중복 로깅 또는 외부 API 호출 시 멱등성을 유지하세요.
- **관련 훅**: `cosmosfarm_members_mail_send`, `cosmosfarm_members_send_message`, `cosmosfarm_members_send_notification`
