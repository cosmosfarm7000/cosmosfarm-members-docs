# cosmosfarm_members_order_download_columns_value

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2024`
- **실행 시점**: 주문 데이터를 다운로드할 때 각 컬럼의 값을 설정할 때 실행됩니다. 특정 컬럼에 대한 데이터를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$column_value (string)`: 컬럼의 값. 기본적으로 주문 데이터에서 가져온 값입니다.
  - `$column_key (string)`: 컬럼의 식별자 키.
  - `$order (Cosmosfarm_Members_Order)`: 주문 객체. 주문의 모든 데이터를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_order_download_columns_value', 'my_custom_order_download_column_value', 10, 3);
  function my_custom_order_download_column_value($column_value, $column_key, $order) {
    if ($column_key === 'custom_field') {
        return get_post_meta($order->ID(), '_custom_order_data', true);
    }
    return $column_value;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 컬럼 값을 반환해야 합니다. 반환된 값은 다운로드 파일의 해당 셀에 기록됩니다.
- **관련 훅**: `cosmosfarm_members_order_download_columns`, `cosmosfarm_members_order_csv_download_row_data`
