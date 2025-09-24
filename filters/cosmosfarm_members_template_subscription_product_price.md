# cosmosfarm_members_template_subscription_product_price

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:922`
- **실행 시점**: 정기결제 상품 가격 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_subscription_product_price', 'my_custom_subscription_product_price_template', 10, 2);
    function my_custom_subscription_product_price_template($file_path, $product) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-price.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
