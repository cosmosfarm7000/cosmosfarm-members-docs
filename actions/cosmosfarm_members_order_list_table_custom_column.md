# cosmosfarm_members_order_list_table_custom_column

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Subscription_Order_Table.class.php`
- **실행 시점**: 주문 목록 테이블의 커스텀 컬럼을 출력할 때 호출됩니다. 각 주문 행의 커스텀 컬럼에 콘텐츠를 추가할 수 있습니다.
- **인자 정보**:
  - `$key (string)`: 컬럼 키.
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 주문 객체.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_order_list_table_custom_column', 'my_custom_order_list_column', 10, 2);
  function my_custom_order_list_column($key, $order) {
      if ($key === 'custom_column') {
          echo '<span>커스텀 컬럼 콘텐츠</span>';
      }
  }
  ```

- **주의 사항**: 컬럼 키를 확인하여 올바른 컬럼에만 콘텐츠를 출력하세요.
- **관련 훅**: `cosmosfarm_members_order_list_table_nav`
