# cosmosfarm_members_users_csv_download_row_data

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 사용자 CSV 다운로드 시 각 사용자의 행 데이터를 필터링합니다.
- **인자 정보**:
  - `$row_data (mixed)`: 파라미터 1
  - `$user (mixed)`: 파라미터 2
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_users_csv_download_row_data', 'my_custom_users_csv_row_data', 10, 2);
    function my_custom_users_csv_row_data($row_data, $user) {
        $row_data['custom_user_status'] = 'Active';
        return $row_data;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
