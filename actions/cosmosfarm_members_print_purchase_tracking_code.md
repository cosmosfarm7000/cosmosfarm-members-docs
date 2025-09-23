# cosmosfarm_members_print_purchase_tracking_code

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members.class.php:1751`
- **실행 시점**: 결제 완료 페이지(`subscription_payment_completed_page_id`)에서 기본 추적 스크립트를 출력한 직후 호출됩니다. 페이지가 로드될 때마다 호출되며, URL의 `cosmosfarm_product_id` 파라미터로 식별되는 구독 상품 객체를 전달합니다.
- **인자 정보**:
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 결제한 구독 상품 객체입니다. `ID()`, `price()`, `title()`, `subscription_type()` 등을 사용해 추적 이벤트에 필요한 상품 정보를 가져올 수 있습니다.
- **예제 코드**:

  ```php
  // 결제 완료 페이지에서 사용자 정의 GTM 이벤트를 추가한다.
  add_action('cosmosfarm_members_print_purchase_tracking_code', function ($product) {
      if (!$product->ID()) {
          return;
      }
  
      ?>
      <script>
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
          'event': 'customPurchase',
          'membershipProductId': '<?php echo intval($product->ID()); ?>',
          'membershipProductTitle': '<?php echo esc_js(wp_strip_all_tags($product->title())); ?>',
          'membershipProductPrice': <?php echo intval($product->price()); ?>
      });
      </script>
      <?php
  });
  ```
- **주의 사항**:
  - 이 훅은 프런트엔드에서 `<script>` 태그를 출력할 때 사용되므로, HTML/JS 인코딩(`esc_js`, `esc_html`)을 적절히 적용해 XSS를 방지해야 합니다.
  - `cosmosfarm_product_id`가 비어 있거나 잘못된 경우 `$product->ID()`가 0일 수 있으니 방어 로직을 추가하세요.
  - 외부 스크립트를 비동기 로드하려면 `wp_enqueue_script()`를 사용해 별도 파일로 분리하는 것이 좋습니다.
- **관련 훅**: `wp_footer`, `cosmosfarm_members_print_sign_up_tracking_code`
