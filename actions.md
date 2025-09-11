# Cosmosfarm Members Actions

이 문서는 Cosmosfarm Members 플러그인에서 사용되는 `do_action` 훅들을 정리한 것입니다. `do_action`은 특정 이벤트가 발생했을 때 사용자 정의 함수를 실행할 수 있도록 합니다.

## 훅 목록 및 예제

### `cosmosfarm_members_admin_menu`
*   **설명**: 관리자 메뉴가 로드될 때 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_admin_menu', 'my_custom_admin_menu_item');
    function my_custom_admin_menu_item() {
        add_menu_page(
            __('My Custom Page', 'textdomain'),
            __('My Custom Page', 'textdomain'),
            'manage_options',
            'my-custom-page',
            'my_custom_page_callback'
        );
    }
    function my_custom_page_callback() {
        echo '<h1>My Custom Admin Page</h1>';
    }
    ```

### `cosmosfarm_members_before_subscription_order_setting_html`
*   **설명**: 구독 주문 설정 HTML 출력 전에 실행됩니다.
*   **파일**: `admin/subscription_order_setting.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_before_subscription_order_setting_html', 'my_custom_before_order_setting_html', 10, 2);
    function my_custom_before_order_setting_html($order, $product) {
        echo '<p>구독 주문 설정 HTML이 시작되기 전입니다. 주문 ID: ' . $order->ID() . '</p>';
    }
    ```

### `cosmosfarm_members_after_subscription_order_setting_html`
*   **설명**: 구독 주문 설정 HTML 출력 후에 실행됩니다.
*   **파일**: `admin/subscription_order_setting.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_after_subscription_order_setting_html', 'my_custom_after_order_setting_html', 10, 2);
    function my_custom_after_order_setting_html($order, $product) {
        echo '<p>구독 주문 설정 HTML이 끝난 후입니다. 상품 ID: ' . $product->ID() . '</p>';
    }
    ```

### `cosmosfarm_members_before_subscription_order_setting`
*   **설명**: 구독 주문 설정 저장 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_before_subscription_order_setting', 'my_custom_before_order_setting_save', 10, 2);
    function my_custom_before_order_setting_save($order, $product) {
        // 주문 설정 저장 전 추가 로직
        error_log('구독 주문 설정 저장 전: ' . $order->ID());
    }
    ```

### `cosmosfarm_members_after_subscription_order_setting`
*   **설명**: 구독 주문 설정 저장 후에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_after_subscription_order_setting', 'my_custom_after_order_setting_save', 10, 2);
    function my_custom_after_order_setting_save($order, $product) {
        // 주문 설정 저장 후 추가 로직
        error_log('구독 주문 설정 저장 후: ' . $order->ID());
    }
    ```

### `cosmosfarm_members_pre_user_required`
*   **설명**: 사용자 필수 정보 확인 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_user_required', 'my_custom_pre_user_required_check', 10, 2);
    function my_custom_pre_user_required_check($current_user, $profile_url) {
        // 사용자 필수 정보 확인 전 추가 로직
        if (empty($current_user->user_phone)) {
            wp_redirect($profile_url . '&missing_phone=true');
            exit;
        }
    }
    ```

### `cosmosfarm_members_user_required`
*   **설명**: 사용자 필수 정보 확인 후에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_user_required', 'my_custom_user_required_checked', 10, 2);
    function my_custom_user_required_checked($current_user, $profile_url) {
        // 사용자 필수 정보 확인 후 추가 로직
        error_log('사용자 필수 정보 확인 완료: ' . $current_user->ID);
    }
    ```

### `cosmosfarm_members_print_purchase_tracking_code`
*   **설명**: 구매 추적 코드를 출력할 때 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_print_purchase_tracking_code', 'my_custom_tracking_code', 10, 1);
    function my_custom_tracking_code($product) {
        echo '<!-- Custom Tracking Code for Product ID: ' . $product->ID() . ' -->';
        echo '<script>console.log("Product purchased: ' . $product->name() . '");</script>';
    }
    ```

### `cosmosfarm_members_user_data_social_login_first_update`
*   **설명**: 소셜 로그인으로 사용자 데이터가 처음 업데이트될 때 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_user_data_social_login_first_update', 'my_custom_social_login_first_update', 10, 1);
    function my_custom_social_login_first_update($user) {
        // 소셜 로그인으로 사용자 데이터가 처음 업데이트될 때 추가 로직
        update_user_meta($user->ID, 'social_login_first_updated', true);
    }
    ```

### `wp_login`
*   **설명**: 워드프레스 사용자가 로그인할 때 실행됩니다. (워드프레스 코어 훅)
*   **파일**: `class/Cosmosfarm_Members.class.php`, `class/Cosmosfarm_Members_Controller.class.php`, `class/Cosmosfarm_Members_Security.class.php`
*   **예제**:
    ```php
    add_action('wp_login', 'my_custom_login_action', 10, 2);
    function my_custom_login_action($user_login, $user) {
        error_log('사용자 로그인: ' . $user_login . ' (ID: ' . $user->ID . ')');
    }
    ```

### `cosmosfarm_members_pre_activity_history_download`
*   **설명**: 활동 기록 다운로드 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_activity_history_download', 'my_custom_pre_activity_download');
    function my_custom_pre_activity_download() {
        // 활동 기록 다운로드 전 권한 확인 등 추가 로직
        if (!current_user_can('manage_options')) {
            wp_die('활동 기록을 다운로드할 권한이 없습니다.');
        }
    }
    ```

### `cosmosfarm_members_subscription_request_pay`
*   **설명**: 구독 결제 요청 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_request_pay', 'my_custom_subscription_pay_request', 10, 3);
    function my_custom_subscription_pay_request($order, $product, $custom_data) {
        error_log('구독 결제 요청: 주문 ID ' . $order->ID() . ', 상품 ID ' . $product->ID());
        // 외부 결제 시스템 연동 등 추가 로직
    }
    ```

### `cosmosfarm_members_pre_order_download`
*   **설명**: 주문 내역 다운로드 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_order_download', 'my_custom_pre_order_download');
    function my_custom_pre_order_download() {
        // 주문 내역 다운로드 전 추가 로직
        error_log('주문 내역 다운로드 시작');
    }
    ```

### `cosmosfarm_members_pre_order_upload`
*   **설명**: 주문 내역 업로드 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_order_upload', 'my_custom_pre_order_upload');
    function my_custom_pre_order_upload() {
        // 주문 내역 업로드 전 추가 로직
        error_log('주문 내역 업로드 시작');
    }
    ```

### `cosmosfarm_members_pre_users_csv_download`
*   **설명**: 사용자 CSV 다운로드 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_users_csv_download', 'my_custom_pre_users_csv_download');
    function my_custom_pre_users_csv_download() {
        // 사용자 CSV 다운로드 전 추가 로직
        error_log('사용자 CSV 다운로드 시작');
    }
    ```

### `cosmosfarm_members_pre_users_csv_upload`
*   **설명**: 사용자 CSV 업로드 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_users_csv_upload', 'my_custom_pre_users_csv_upload');
    function my_custom_pre_users_csv_upload() {
        // 사용자 CSV 업로드 전 추가 로직
        error_log('사용자 CSV 업로드 시작');
    }
    ```

### `cosmosfarm_members_users_csv_upload_row`
*   **설명**: 사용자 CSV 업로드 시 각 행 처리 후에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_users_csv_upload_row', 'my_custom_users_csv_row_processed', 10, 2);
    function my_custom_users_csv_row_processed($user_id, $row) {
        // 각 사용자 데이터 처리 후 추가 로직
        update_user_meta($user_id, 'csv_uploaded_date', current_time('mysql'));
    }
    ```

### `cosmosfarm_members_pre_social_login`
*   **설명**: 소셜 로그인 처리 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_social_login', 'my_custom_pre_social_login_process', 10, 1);
    function my_custom_pre_social_login_process($channel) {
        // 소셜 로그인 전 추가 로직 (예: 특정 채널 차단)
        if ($channel === 'facebook') {
            wp_die('Facebook 로그인은 현재 지원되지 않습니다.');
        }
    }
    ```

### `cosmosfarm_members_social_login_callback`
*   **설명**: 소셜 로그인 콜백 처리 후에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_social_login_callback', 'my_custom_social_login_callback_after', 10, 4);
    function my_custom_social_login_callback_after($channel, $profile, $user, $random_password) {
        // 소셜 로그인 콜백 후 추가 로직
        error_log('소셜 로그인 성공: ' . $user->user_login . ' (채널: ' . $channel . ')');
    }
    ```

### `cosmosfarm_members_delete_account`
*   **설명**: 계정 삭제 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_delete_account', 'my_custom_delete_account_action');
    function my_custom_delete_account_action() {
        // 계정 삭제 시 추가 로직 (예: 관련 데이터 정리)
        $user_id = get_current_user_id();
        delete_user_meta($user_id, 'some_custom_data');
        error_log('사용자 계정 삭제: ' . $user_id);
    }
    ```

### `cosmosfarm_members_pre_subscription_request_pay`
*   **설명**: 구독 결제 요청 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_subscription_request_pay', 'my_custom_pre_subscription_pay', 10, 3);
    function my_custom_pre_subscription_pay($product, $meta_input, $custom_data) {
        // 구독 결제 요청 전 추가 로직 (예: 재고 확인)
        if ($product->stock() <= 0) {
            wp_die('재고가 부족합니다.');
        }
    }
    ```

### `cosmosfarm_members_subscription_again_failure`
*   **설명**: 구독 재결제 실패 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_again_failure', 'my_custom_subscription_again_failed', 10, 2);
    function my_custom_subscription_again_failed($old_order, $product) {
        // 구독 재결제 실패 시 알림 등 추가 로직
        error_log('구독 재결제 실패: 주문 ID ' . $old_order->ID() . ', 상품 ID ' . $product->ID());
    }
    ```

### `cosmosfarm_members_pre_subscription_again`
*   **설명**: 구독 재결제 처리 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_subscription_again', 'my_custom_pre_subscription_again_process', 10, 2);
    function my_custom_pre_subscription_again_process($old_order, $product) {
        // 구독 재결제 전 추가 로직
        error_log('구독 재결제 시도: 이전 주문 ID ' . $old_order->ID());
    }
    ```

### `cosmosfarm_members_subscription_again_success`
*   **설명**: 구독 재결제 성공 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_again_success', 'my_custom_subscription_again_succeeded', 10, 3);
    function my_custom_subscription_again_succeeded($order, $product, $old_order) {
        // 구독 재결제 성공 시 추가 로직
        error_log('구독 재결제 성공: 새 주문 ID ' . $order->ID() . ', 이전 주문 ID ' . $old_order->ID());
    }
    ```

### `cosmosfarm_members_subscription_expiry`
*   **설명**: 구독 만료 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`, `class/Cosmosfarm_Members_Subscription_Order.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_expiry', 'my_custom_subscription_expired', 10, 2);
    function my_custom_subscription_expired($order, $product) {
        // 구독 만료 시 추가 로직 (예: 사용자 등급 변경)
        error_log('구독 만료: 주문 ID ' . $order->ID() . ', 상품 ID ' . $product->ID());
        // remove_user_role($order->get_user_id(), 'subscriber');
    }
    ```

### `cosmosfarm_members_subscription_billing_key_pre_delete`
*   **설명**: 구독 빌링 키 삭제 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_billing_key_pre_delete', 'my_custom_pre_billing_key_delete', 10, 1);
    function my_custom_pre_billing_key_delete($user_id) {
        // 빌링 키 삭제 전 추가 로직
        error_log('빌링 키 삭제 시도: 사용자 ID ' . $user_id);
    }
    ```

### `cosmosfarm_members_subscription_billing_key_post_delete`
*   **설명**: 구독 빌링 키 삭제 후에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_billing_key_post_delete', 'my_custom_post_billing_key_delete', 10, 2);
    function my_custom_post_billing_key_delete($user_id, $bid) {
        // 빌링 키 삭제 후 추가 로직
        error_log('빌링 키 삭제 완료: 사용자 ID ' . $user_id . ', BID: ' . $bid);
    }
    ```

### `cosmosfarm_members_subscription_notification_execute`
*   **설명**: 구독 알림이 실행될 때 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_notification_execute', 'my_custom_subscription_notification_executed', 10, 5);
    function my_custom_subscription_notification_executed($order, $product, $subscription_notification, $notification_subject, $notification_message) {
        // 구독 알림 실행 시 추가 로직
        error_log('구독 알림 실행: 주문 ID ' . $order->ID() . ', 제목: ' . $notification_subject);
    }
    ```

### `cosmosfarm_members_redeem_point_coupon_success`
*   **설명**: 포인트 쿠폰 사용 성공 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Controller.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_redeem_point_coupon_success', 'my_custom_point_coupon_redeemed', 10, 3);
    function my_custom_point_coupon_redeemed($coupon_id, $mycred_coupon, $user_id) {
        // 포인트 쿠폰 사용 성공 시 추가 로직
        error_log('포인트 쿠폰 사용 성공: 사용자 ID ' . $user_id . ', 쿠폰 ID ' . $coupon_id);
    }
    ```

### `cosmosfarm_members_mail_send`
*   **설명**: 메일 발송 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Mail.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_mail_send', 'my_custom_mail_sent', 10, 2);
    function my_custom_mail_sent($args, $mail_object) {
        // 메일 발송 시 추가 로직 (예: 발송 기록)
        error_log('메일 발송: 수신자 ' . $args['to'] . ', 제목: ' . $args['subject']);
    }
    ```

### `cosmosfarm_members_send_message`
*   **설명**: 메시지 발송 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Message.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_send_message', 'my_custom_message_sent', 10, 1);
    function my_custom_message_sent($message_object) {
        // 메시지 발송 시 추가 로직
        error_log('메시지 발송: 발신자 ' . $message_object->sender_id . ', 수신자 ' . $message_object->receiver_id);
    }
    ```

### `cosmosfarm_members_send_notification`
*   **설명**: 알림 발송 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Notification.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_send_notification', 'my_custom_notification_sent', 10, 1);
    function my_custom_notification_sent($notification_object) {
        // 알림 발송 시 추가 로직
        error_log('알림 발송: 수신자 ' . $notification_object->user_id . ', 내용: ' . $notification_object->content);
    }
    ```

### `cosmosfarm_members_pre_subscription_checkout`
*   **설명**: 구독 결제 페이지 로드 전에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Page_Builder.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_pre_subscription_checkout', 'my_custom_pre_checkout_load', 10, 1);
    function my_custom_pre_checkout_load($product) {
        // 구독 결제 페이지 로드 전 추가 로직
        if (!$product->is_available()) {
            wp_die('이 상품은 현재 구매할 수 없습니다.');
        }
    }
    ```

### `cosmosfarm_members_skin_subscription_product`
*   **설명**: 구독 상품 스킨 템플릿에서 상품 정보 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product', 'my_custom_skin_product_display', 10, 2);
    function my_custom_skin_product_display($skin_object, $product) {
        echo '<div class="my-custom-product-info">';
        echo '<h3>' . $product->name() . '</h3>';
        echo '<p>' . $product->description() . '</p>';
        echo '</div>';
    }
    ```

### `cosmosfarm_members_skin_after_subscription_product`
*   **설명**: 구독 상품 스킨 템플릿에서 상품 정보 출력 후에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_after_subscription_product', 'my_custom_skin_after_product_display', 10, 2);
    function my_custom_skin_after_product_display($skin_object, $product) {
        echo '<p>상품 정보 출력이 완료되었습니다.</p>';
    }
    ```

### `cosmosfarm_members_skin_subscription_product_title`
*   **설명**: 구독 상품 스킨 템플릿에서 상품 제목 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_title', 'my_custom_skin_product_title', 10, 2);
    function my_custom_skin_product_title($skin_object, $product) {
        echo '<h2>' . $product->name() . ' (Custom Title)</h2>';
    }
    ```

### `cosmosfarm_members_skin_subscription_product_price`
*   **설명**: 구독 상품 스킨 템플릿에서 상품 가격 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_price', 'my_custom_skin_product_price', 10, 2);
    function my_custom_skin_product_price($skin_object, $product) {
        echo '<p class="custom-price">가격: ' . $product->price() . '원</p>';
    }
    ```

### `cosmosfarm_members_skin_subscription_product_type`
*   **설명**: 구독 상품 스킨 템플릿에서 상품 유형 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_type', 'my_custom_skin_product_type', 10, 2);
    function my_custom_skin_product_type($skin_object, $product) {
        echo '<span class="custom-product-type">유형: ' . $product->type() . '</span>';
    }
    ```

### `cosmosfarm_members_skin_subscription_product_first_free`
*   **설명**: 구독 상품 스킨 템플릿에서 첫 달 무료 정보 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_first_free', 'my_custom_skin_product_first_free', 10, 2);
    function my_custom_skin_product_first_free($skin_object, $product) {
        if ($product->is_first_free()) {
            echo '<p class="first-free-offer">첫 달 무료!</p>';
        }
    }
    ```

### `cosmosfarm_members_skin_subscription_product_button`
*   **설명**: 구독 상품 스킨 템플릿에서 상품 버튼 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_button', 'my_custom_skin_product_button', 10, 2);
    function my_custom_skin_product_button($skin_object, $product) {
        echo '<button class="custom-buy-button">지금 구독하기</button>';
    }
    ```

### `cosmosfarm_members_skin_subscription_product_list`
*   **설명**: 구독 상품 목록 스킨 템플릿에서 상품 목록 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_list', 'my_custom_skin_product_list', 10, 2);
    function my_custom_skin_product_list($skin_object, $query) {
        echo '<h3>Custom Product List</h3>';
        while ($query->have_posts()) : $query->the_post();
            $product = new Cosmosfarm_Members_Subscription_Product(get_the_ID());
            echo '<li>' . $product->name() . '</li>';
        endwhile;
        wp_reset_postdata();
    }
    ```

### `cosmosfarm_members_skin_subscription_product_latest`
*   **설명**: 최신 구독 상품 스킨 템플릿에서 상품 목록 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_latest', 'my_custom_skin_product_latest', 10, 2);
    function my_custom_skin_product_latest($skin_object, $query) {
        echo '<h3>Custom Latest Products</h3>';
        while ($query->have_posts()) : $query->the_post();
            $product = new Cosmosfarm_Members_Subscription_Product(get_the_ID());
            echo '<li>' . $product->name() . ' (New!)</li>';
        endwhile;
        wp_reset_postdata();
    }
    ```

### `cosmosfarm_members_skin_subscription_product_single_template`
*   **설명**: 단일 구독 상품 스킨 템플릿에서 상품 정보 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_product_single_template', 'my_custom_skin_single_product_template', 10, 2);
    function my_custom_skin_single_product_template($skin_object, $cosmosfarm_members_subscription_product) {
        echo '<h1>' . $cosmosfarm_members_subscription_product->name() . '</h1>';
        echo '<p>This is a custom single product template.</p>';
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout`
*   **설명**: 구독 결제 스킨 템플릿에서 결제 정보 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_checkout', 'my_custom_skin_checkout_display', 10, 2);
    function my_custom_skin_checkout_display($skin_object, $product) {
        echo '<h2>Custom Checkout for ' . $product->name() . '</h2>';
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout_field_template`
*   **설명**: 구독 결제 스킨 템플릿에서 필드 템플릿 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_checkout_field_template', 'my_custom_skin_checkout_field_template', 10, 4);
    function my_custom_skin_checkout_field_template($field_type, $field, $field2, $field3) {
        if ($field_type === 'text') {
            echo '<p>Custom Text Field: <input type="text" name="' . $field->name . '" value="' . $field->value . '"></p>';
        }
    }
    ```

### `cosmosfarm_members_skin_comments_reviews`
*   **설명**: 댓글/리뷰 스킨 템플릿에서 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Skin.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_comments_reviews', 'my_custom_skin_comments_reviews', 10, 1);
    function my_custom_skin_comments_reviews($skin_object) {
        echo '<h3>Custom Comments & Reviews Section</h3>';
        // 여기에 사용자 정의 댓글/리뷰 목록을 출력
    }
    ```

### `cosmosfarm_members_user_social_register`
*   **설명**: 소셜 계정으로 사용자 등록 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Social_Login.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_user_social_register', 'my_custom_social_user_registered', 10, 2);
    function my_custom_social_user_registered($user_id, $social_login_object) {
        // 소셜 계정으로 사용자 등록 시 추가 로직
        update_user_meta($user_id, 'registered_via_social', $social_login_object->channel);
    }
    ```

### `cosmosfarm_members_subscription_order_status_update`
*   **설명**: 구독 주문 상태 업데이트 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Subscription_Order.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_subscription_order_status_update', 'my_custom_order_status_updated', 10, 2);
    function my_custom_order_status_updated($order_object, $new_status) {
        // 구독 주문 상태 변경 시 추가 로직
        error_log('주문 ID ' . $order_object->ID() . ' 상태 변경: ' . $new_status);
    }
    ```

### `cosmosfarm_members_order_admin_field_template`
*   **설명**: 관리자 주문 상세 페이지에서 필드 템플릿 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Subscription_Order.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_order_admin_field_template', 'my_custom_admin_order_field', 10, 5);
    function my_custom_admin_order_field($order, $field_type, $field, $field2, $field3) {
        if ($field_type === 'custom_text') {
            echo '<p>Custom Admin Field: <input type="text" name="custom_order_data" value="' . get_post_meta($order->ID(), 'custom_order_data', true) . '"></p>';
        }
    }
    ```

### `cosmosfarm_members_order_update_field`
*   **설명**: 주문 필드 업데이트 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Subscription_Order.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_order_update_field', 'my_custom_order_field_updated', 10, 3);
    function my_custom_order_field_updated($order, $field, $meta_value) {
        // 주문 필드 업데이트 시 추가 로직
        error_log('주문 ID ' . $order->ID() . ' 필드 업데이트: ' . $field . ' = ' . $meta_value);
    }
    ```

### `cosmosfarm_members_product_admin_field_template`
*   **설명**: 관리자 상품 상세 페이지에서 필드 템플릿 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Subscription_Product.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_product_admin_field_template', 'my_custom_admin_product_field', 10, 4);
    function my_custom_admin_product_field($field_type, $field, $field2, $field3) {
        if ($field_type === 'custom_checkbox') {
            echo '<p><label><input type="checkbox" name="custom_product_option" value="1"> Custom Product Option</label></p>';
        }
    }
    ```

### `cosmosfarm_members_certification_result`
*   **설명**: 본인 인증 결과 처리 시 실행됩니다.
*   **파일**: `class/api/Cosmosfarm_Members_API_Iamport.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_certification_result', 'my_custom_certification_result', 10, 2);
    function my_custom_certification_result($result, $response) {
        // 본인 인증 결과에 따른 추가 로직
        if ($result->success) {
            error_log('본인 인증 성공: ' . $response->name);
        } else {
            error_log('본인 인증 실패: ' . $response->error_msg);
        }
    }
    ```

### `cosmosfarm_members_dormant_member_alert`
*   **설명**: 휴면 회원 알림 시 실행됩니다.
*   **파일**: `cosmosfarm-members.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_dormant_member_alert', 'my_custom_dormant_member_alert', 10, 1);
    function my_custom_dormant_member_alert($user) {
        // 휴면 회원에게 추가 알림 발송 등 로직
        error_log('휴면 회원 알림: ' . $user->user_login);
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout_form_header`
*   **설명**: 구독 결제 폼 헤더 출력 시 실행됩니다.
*   **파일**: `skin/default/subscription-checkout.php`, `skin/two/subscription-checkout.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_checkout_form_header', 'my_custom_checkout_form_header', 10, 2);
    function my_custom_checkout_form_header($product, $skin) {
        echo '<p>결제 폼 상단에 표시될 사용자 정의 메시지입니다.</p>';
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout_field_before`
*   **설명**: 구독 결제 폼 필드 출력 전에 실행됩니다.
*   **파일**: `skin/default/subscription-checkout.php`, `skin/two/subscription-checkout.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_checkout_field_before', 'my_custom_checkout_field_before', 10, 2);
    function my_custom_checkout_field_before($product, $skin) {
        echo '<!-- 필드 시작 전 -->';
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout_field_after`
*   **설명**: 구독 결제 폼 필드 출력 후에 실행됩니다.
*   **파일**: `skin/default/subscription-checkout.php`, `skin/two/subscription-checkout.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_checkout_field_after', 'my_custom_checkout_field_after', 10, 2);
    function my_custom_checkout_field_after($product, $skin) {
        echo '<!-- 필드 끝난 후 -->';
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout_form_footer`
*   **설명**: 구독 결제 폼 푸터 출력 시 실행됩니다.
*   **파일**: `skin/default/subscription-checkout.php`, `skin/two/subscription-checkout.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_skin_subscription_checkout_form_footer', 'my_custom_checkout_form_footer', 10, 2);
    function my_custom_checkout_form_footer($product, $skin) {
        echo '<p>결제 폼 하단에 표시될 사용자 정의 메시지입니다.</p>';
    }
    ```

### `cosmosfarm_members_order_list_table_nav`
*   **설명**: 주문 목록 테이블 네비게이션 영역에 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Subscription_Order_Table.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_order_list_table_nav', 'my_custom_order_list_nav');
    function my_custom_order_list_nav() {
        echo '<div class="custom-order-nav">추가 네비게이션 링크</div>';
    }
    ```

### `cosmosfarm_members_order_list_table_custom_column`
*   **설명**: 주문 목록 테이블의 사용자 정의 컬럼 출력 시 실행됩니다.
*   **파일**: `class/Cosmosfarm_Members_Subscription_Order_Table.class.php`
*   **예제**:
    ```php
    add_action('cosmosfarm_members_order_list_table_custom_column', 'my_custom_order_list_column', 10, 2);
    function my_custom_order_list_column($column_key, $order) {
        if ($column_key === 'my_custom_column') {
            echo 'Custom Value for Order ID: ' . $order->ID();
        }
    }
    ```
