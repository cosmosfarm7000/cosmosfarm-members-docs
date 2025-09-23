# cosmosfarm_members_users_csv_download_usermeta_value

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 
- **인자 정보**:
  - `$meta_value (mixed)`: 파라미터 1
  - `$meta_key (mixed)`: 파라미터 2
  - `$user (mixed)`: 파라미터 3
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_users_csv_download_usermeta_value', 'my_custom_users_csv_usermeta_value', 10, 3);
    function my_custom_users_csv_usermeta_value($meta_value, $meta_key, $user) {
        if ($meta_key === 'billing_address') {
            return get_user_meta($user->ID, 'billing_address_1', true) . ', ' . get_user_meta($user->ID, 'billing_city', true);
        }
        return $meta_value;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
