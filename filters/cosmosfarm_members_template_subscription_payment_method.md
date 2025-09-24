# cosmosfarm_members_template_subscription_payment_method

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`class/Cosmosfarm_Members_Skin.class.php``
- **실행 시점**: 구독 결제 수단 템플릿 파일 경로를 필터링합니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_subscription_payment_method', 'my_custom_payment_method_template');
  function my_custom_payment_method_template($file_path) {
    return get_stylesheet_directory() . '/cosmosfarm-members/subscription-payment-method.php';
  }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
