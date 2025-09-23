# cosmosfarm_members_product_admin_field_template

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Subscription_Product.class.php`
- **실행 시점**: 관리자 상품 상세 페이지에서 필드 템플릿을 출력할 때 호출됩니다. 상품 편집 시 커스텀 필드를 추가할 수 있습니다.
- **인자 정보**:
  - `$field_type (string)`: 필드 유형.
  - `$field (array)`: 필드 설정.
  - `$field2 (mixed)`: 보조 파라미터.
  - `$field3 (mixed)`: 보조 파라미터.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_product_admin_field_template', 'my_custom_admin_product_field', 10, 4);
  function my_custom_admin_product_field($field_type, $field, $field2, $field3) {
      if ($field_type === 'custom_checkbox') {
          echo '<p><label><input type="checkbox" name="custom_product_option" value="1"> Custom Product Option</label></p>';
      }
  }
  ```

- **주의 사항**: 상품 저장 시 필드 값 처리 로직을 추가하세요.
- **관련 훅**: 없음
