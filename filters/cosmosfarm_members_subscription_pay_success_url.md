# cosmosfarm_members_subscription_pay_success_url

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 
- **인자 정보**:
  - `$pay_success_url (mixed)`: 파라미터 1
  - `$product (mixed)`: 파라미터 2
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_subscription_pay_success_url', 'my_custom_pay_success_url', 10, 2);
    function my_custom_pay_success_url($url, $product) {
        return home_url('/payment-success/');
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
