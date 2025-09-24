# cosmosfarm_members_template_subscription_checkout_fields

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 정기결제 상품 결제 페이지 필드 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$field (object)`: 필드 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_subscription_checkout_fields', 'my_custom_checkout_fields_template', 10, 2);
    function my_custom_checkout_fields_template($file_path, $field) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-checkout-fields.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
