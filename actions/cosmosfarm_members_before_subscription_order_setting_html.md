# cosmosfarm_members_before_subscription_order_setting_html

- **분류**: Action
- **정의 위치**: `admin/subscription_order_setting.php:20`
- **실행 시점**: 구독 주문 편집 화면에서 기본 주문 폼이 렌더링되기 직전(`Cosmosfarm_Members::subscription_order_setting()`이 주문 객체와 상품 객체를 준비한 뒤) 호출됩니다. 숨겨진 필드와 보안 nonce가 출력된 직후이므로, 커스텀 입력 필드를 UI 상단에 추가할 때 활용할 수 있습니다.
- **인자 정보**:
  - `$order (Cosmosfarm_Members_Subscription_Order)`: 현재 편집 중인 구독 주문 객체입니다. `ID()`로 주문 포스트 ID를 얻고, `user()`로 연결된 `WP_User` 객체와 그 역할 정보를 조회할 수 있습니다. 금액 관련 메서드(`first_price()`, `next_price()`, `real_price()`, `pay_count()` 등)와 구독 상태 메타(`subscription_type()`, `subscription_role()`, `subscription_next()` 등), 그리고 매직 프로퍼티(`$order->buyer_name`, `$order->buyer_email`, `$order->buyer_tel`)도 활용할 수 있습니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 주문과 연결된 구독 상품 객체입니다. `product_id()`로 상품 포스트 ID를 얻고, `fields()`로 등록된 체크아웃 커스텀 필드 구성을 확인할 수 있습니다. 또한 `price()`, `subscription_first_free()`, `subscription_type_format()` 같은 메서드로 반복 결제 정책을 분석하거나, `option_title()`, `option_fields()`로 옵션 구성을 확인할 수 있습니다.
- **예제 코드**:
  ```php
  // 주문 상세 화면 상단에 내부 메모 필드를 추가한다.
  add_action('cosmosfarm_members_before_subscription_order_setting_html', function ($order, $product) {
      if (!current_user_can('manage_cosmosfarm_members')) {
          return; // 권한 확인
      }

      $memo_value = get_post_meta($order->ID(), '_internal_manager_memo', true);
      ?>
      <table class="form-table">
          <tbody>
              <tr>
                  <th scope="row"><label for="internal_manager_memo"><?php esc_html_e('관리자 메모', 'textdomain'); ?></label></th>
                  <td>
                      <textarea id="internal_manager_memo" name="internal_manager_memo" rows="3" class="large-text"><?php echo esc_textarea($memo_value); ?></textarea>
                      <p class="description"><?php esc_html_e('이 메모는 관리자에게만 표시됩니다.', 'textdomain'); ?></p>
                  </td>
              </tr>
          </tbody>
      </table>
      <?php
  }, 10, 2);

  // 저장 로직은 주문 저장 훅에서 처리한다.
  add_action('cosmosfarm_members_before_subscription_order_setting', function ($order) {
      if (!isset($_POST['internal_manager_memo'])) {
          return;
      }
      update_post_meta($order->ID(), '_internal_manager_memo', sanitize_textarea_field($_POST['internal_manager_memo']));
  }, 10, 1);
  ```
- **주의 사항**:
  - 출력하는 HTML은 워드프레스 관리자 스타일을 따르고, `esc_html()`, `esc_attr()` 등을 사용해 안전하게 렌더링하세요.
  - 폼 필드를 추가한 경우 저장 훅(`cosmosfarm_members_before_subscription_order_setting` 등)에서 데이터를 검증 후 저장해야 합니다. 그렇지 않으면 제출해도 값이 유지되지 않습니다.
  - 구독 주문 관리 화면은 `manage_cosmosfarm_members_order` 권한이 있는 관리자만 접근하므로, 추가 UI가 해당 권한자에게 의미가 있는지 확인합니다.
- **관련 훅**: `cosmosfarm_members_after_subscription_order_setting_html`, `cosmosfarm_members_before_subscription_order_setting`, `cosmosfarm_members_after_subscription_order_setting`