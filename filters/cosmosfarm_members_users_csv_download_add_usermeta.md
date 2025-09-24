# cosmosfarm_members_users_csv_download_add_usermeta

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 사용자 목록을 CSV로 다운로드할 때 추가 usermeta 컬럼을 설정할 때 실행됩니다.
- **인자 정보**:
  - `$add_usermeta (array)`: 추가할 usermeta 키 배열.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_users_csv_download_add_usermeta', 'my_custom_users_csv_usermeta');
    function my_custom_users_csv_usermeta($add_usermeta) {
        $add_usermeta[] = 'billing_address';
        return $add_usermeta;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
