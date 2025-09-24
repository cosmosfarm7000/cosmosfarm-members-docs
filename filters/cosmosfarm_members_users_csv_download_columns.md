# cosmosfarm_members_users_csv_download_columns

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 사용자 목록을 CSV로 다운로드할 때 컬럼을 설정할 때 실행됩니다.
- **인자 정보**:
  - `$columns (array)`: CSV 컬럼 배열. 각 키는 컬럼 식별자, 값은 컬럼 표시 이름입니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_users_csv_download_columns', 'my_custom_users_csv_columns');
    function my_custom_users_csv_columns($columns) {
        $columns['user_phone'] = 'Phone Number';
        return $columns;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
