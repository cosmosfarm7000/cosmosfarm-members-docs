# cosmosfarm_members_order_admin_field_template

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Subscription_Order.class.php:1598`
- **실행 시점**: 관리자 주문 상세 페이지에서 커스텀 필드 템플릿을 출력할 때 호출됩니다. 필드 유형에 따라 분기하여 추가 입력 필드를 삽입할 수 있습니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 현재 편집 중인 주문 객체입니다.
  - `$field_type (string)`: 필드 유형 (예: 'text', 'select' 등).
  - `$field (array)`: 필드 설정 값.
  - `$field2 (mixed)`: 보조 파라미터.
  - `$field3 (mixed)`: 보조 파라미터.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_order_admin_field_template', 'my_custom_admin_order_field', 10, 5);
  function my_custom_admin_order_field($order, $field_type, $field, $field2, $field3) {
      if ($field_type === 'custom_text') {
          echo '<p>Custom Admin Field: <input type="text" name="custom_order_data" value="' . get_post_meta($order->ID(), 'custom_order_data', true) . '"></p>';
      }
  }
  ```

- **주의 사항**: 관리자 권한 확인을 추가하세요. 필드 추가 시 저장 로직도 함께 구현해야 합니다.
- **관련 훅**: `cosmosfarm_members_order_update_field`
