# cosmosfarm_members_pre_order_download

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:1864`
- **실행 시점**: 구독 주문 CSV 다운로드(`Cosmosfarm_Members_Controller::order_download()`)가 시작되어 옵션과 쿼리 파라미터를 파싱한 직후 호출됩니다. 주문 목록을 질의하고 CSV 헤더를 작성하기 전에 실행됩니다.
- **인자 정보**:
  - *(없음)* 추가 인자를 제공하지 않습니다.
- **예제 코드**:

  ```php
  // 다운로드 전에 특정 주문 상태만 강제로 필터링한다.
  add_action('cosmosfarm_members_pre_order_download', function () {
      if (!current_user_can('manage_cosmosfarm_members_order')) {
          wp_die(__('You do not have permission to export orders.', 'textdomain'));
      }
  
      add_filter('pre_get_posts', function ($query) {
          if (!is_admin() || $query->get('post_type') !== 'cosmosfarm_order') {
              return $query;
          }
          $meta_query = $query->get('meta_query') ?: array();
          $meta_query[] = array(
              'key'   => 'subscription_next',
              'value' => 'wait',
          );
          $query->set('meta_query', $meta_query);
          return $query;
      });
  });
  ```
- **주의 사항**:
  - `header()` 호출 후 실행되므로, 불필요한 출력은 CSV 응답을 깨뜨립니다.
  - `pre_get_posts` 필터 등으로 쿼리를 수정할 때는 훅 종료 후 필터를 제거하거나 조건문을 명확히 하여 다른 관리자 화면에 영향을 주지 않도록 합니다.
  - 예상 레코드 수가 많다면 PHP 메모리 제한이나 실행 시간을 별도로 늘리는 것도 고려하세요.
- **관련 훅**: `cosmosfarm_members_pre_activity_history_download`, `cosmosfarm_members_pre_order_upload`
