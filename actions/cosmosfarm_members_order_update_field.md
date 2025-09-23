# cosmosfarm_members_order_update_field

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Subscription_Order.class.php:1749`
- **실행 시점**: 주문 필드가 업데이트될 때 호출됩니다. 메타 값 변경 후 후처리나 로깅에 사용됩니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 필드가 업데이트된 주문 객체입니다.
  - `$field (string)`: 업데이트된 필드 이름입니다.
  - `$meta_value (mixed)`: 새로 설정된 메타 값입니다.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_order_update_field', 'my_custom_order_field_updated', 10, 3);
  function my_custom_order_field_updated($order, $field, $meta_value) {
      // 주문 필드 업데이트 시 추가 로직
      error_log('주문 ID ' . $order->ID() . ' 필드 업데이트: ' . $field . ' = ' . $meta_value);
  }
  ```

- **주의 사항**: 이 훅은 업데이트 후에 실행되므로, 값 검증은 저장 전 훅에서 수행하세요.
- **관련 훅**: `cosmosfarm_members_order_admin_field_template`
