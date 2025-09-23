# cosmosfarm_members_subscription_order_status_update

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Subscription_Order.class.php:519,529`
- **실행 시점**: 구독 주문 상태가 'paid' 또는 'cancelled'로 업데이트될 때 호출됩니다. 결제 완료 또는 취소 처리 후 상태 동기화 지점입니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 상태가 업데이트된 주문 객체입니다. `ID()`, `user()`, `subscription_type()` 등으로 주문 정보를 조회할 수 있습니다.
  - `$status (string)`: 새로 설정된 상태 값입니다. 'paid' 또는 'cancelled' 중 하나입니다.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_subscription_order_status_update', 'my_custom_order_status_updated', 10, 2);
  function my_custom_order_status_updated($order, $status) {
      // 주문 상태 변경 시 추가 로직
      error_log('주문 ID ' . $order->ID() . ' 상태 변경: ' . $status);
  }
  ```

- **주의 사항**: 이 훅은 상태 업데이트 후에 실행되므로, 변경을 취소하거나 롤백할 수 없습니다. 외부 시스템 동기화나 알림 발송에 적합합니다.
- **관련 훅**: `cosmosfarm_members_subscription_request_pay`, `cosmosfarm_members_subscription_again_success`
