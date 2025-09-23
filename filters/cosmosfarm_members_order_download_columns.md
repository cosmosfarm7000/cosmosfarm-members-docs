# cosmosfarm_members_order_download_columns

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 주문 데이터를 다운로드할 때 포함될 컬럼 목록을 설정할 때 실행됩니다. 다운로드 파일에 포함될 컬럼을 추가하거나 제거할 수 있습니다.
- **인자 정보**:
  - `$columns (array)`: 다운로드 컬럼 배열. 각 키는 컬럼 식별자, 값은 컬럼 표시 이름입니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_order_download_columns', 'my_custom_order_download_columns');
function my_custom_order_download_columns($columns) {
    $columns['custom_field'] = 'Custom Field';
    return $columns;
}
```

- **주의 사항**: 필터 함수는 반드시 컬럼 배열을 반환해야 합니다. 반환된 컬럼들은 다운로드 파일의 헤더와 데이터에 반영됩니다.
- **관련 훅**: `cosmosfarm_members_order_download_columns_value`, `cosmosfarm_members_order_csv_download_row_data`
