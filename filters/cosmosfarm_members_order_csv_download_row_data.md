# cosmosfarm_members_order_csv_download_row_data

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:2048`
- **실행 시점**: 주문 데이터를 CSV로 다운로드할 때 각 행의 데이터를 구성할 때 실행됩니다. CSV 파일의 각 행에 포함될 데이터를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$row_data (array)`: CSV 행 데이터 배열. 각 키는 컬럼 이름, 값은 해당 셀의 데이터입니다.
  - `$order (Cosmosfarm_Members_Order)`: 주문 객체. 주문 ID, 상태, 상품 정보 등의 데이터를 포함합니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_order_csv_download_row_data', 'my_custom_order_csv_row_data', 10, 2);
  function my_custom_order_csv_row_data($row_data, $order) {
    $row_data['custom_column'] = 'Custom Data for Order ' . $order->ID();
    return $row_data;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 행 데이터 배열을 반환해야 합니다. 반환된 데이터는 CSV 파일의 해당 행에 기록됩니다.
- **관련 훅**: `cosmosfarm_members_order_download_columns`, `cosmosfarm_members_order_download_columns_value`
