# cosmosfarm_members_template_subscription_product_single_template

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1131`
- **실행 시점**: 정기결제 상품 상세페이지 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$cosmosfarm_members_subscription_product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_subscription_product_single_template', 'my_custom_subscription_product_single_template', 10, 2);
    function my_custom_subscription_product_single_template($file_path, $cosmosfarm_members_subscription_product) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-single-template.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
