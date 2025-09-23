# cosmosfarm_members_skin_subscription_checkout_field_template

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1421`
- **실행 시점**: 구독 결제 스킨에서 커스텀 필드(텍스트, 셀렉트 등)를 렌더링하기 직전에 호출됩니다. 필드별 분기 처리를 통해 템플릿을 확장할 수 있습니다.
- **인자 정보**:
  - `$field_type (string)`: 필드 유형. 예: `text`, `select`, `checkbox` 등
  - `$field (array)`: 필드 설정 값(라벨, 이름, 필수 여부 등)
  - `$field2 (mixed)`: 스킨 구현에서 사용하는 보조 파라미터
  - `$field3 (mixed)`: 스킨 구현에서 사용하는 보조 파라미터
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_checkout_field_template', function ($field_type, $field) {
      if ($field_type === 'text' && ($field['name'] ?? '') === 'company_name') {
          printf('<p class="form-field"><label>%s</label><input type="text" name="company_name" class="regular-text"></p>', esc_html__('Company name', 'textdomain'));
      }
  }, 10, 4);
  ```

- **주의 사항**:
  - 필수 입력을 추가한 경우 서버 사이드 검증을 위한 별도 저장/검증 훅도 함께 구성하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_checkout`
