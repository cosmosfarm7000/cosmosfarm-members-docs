# cosmosfarm_members_template_subscription_product_latest

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 정기결제 상품 최신글 템플릿 파일 경로를 설정할 때 실행됩니다.
- **인자 정보**:
  - `$file_path (string)`: 템플릿 파일 경로.
  - `$query (WP_Query)`: WP_Query 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_template_subscription_product_latest', 'my_custom_subscription_product_latest_template', 10, 2);
    function my_custom_subscription_product_latest_template($file_path, $query) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-latest.php';
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
