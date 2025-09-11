# Cosmosfarm Members Filters

이 문서는 Cosmosfarm Members 플러그인에서 사용되는 `apply_filters` 훅들을 정리한 것입니다. `apply_filters`는 특정 값을 변경하거나 필터링할 수 있도록 합니다.

## 훅 목록 및 예제

### `cosmosfarm_members_menu_items`

* **설명**: 관리자 메뉴 항목을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_menu_items', 'my_custom_menu_items');
    function my_custom_menu_items($menu_items) {
        // 기존 메뉴 항목에 새 항목 추가
        $menu_items['my-new-menu'] = array(
            'title' => __('My New Menu', 'textdomain'),
            'url'   => admin_url('admin.php?page=my-new-menu'),
            'capability' => 'manage_options',
        );
        return $menu_items;
    }
    ```

### `cosmosfarm_members_template_social_buttons`

* **설명**: 소셜 버튼 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_social_buttons', 'my_custom_social_buttons_template');
    function my_custom_social_buttons_template($file_path) {
        // 사용자 정의 소셜 버튼 템플릿 경로 반환
        return get_stylesheet_directory() . '/cosmosfarm-members/social-buttons.php';
    }
    ```

### `cosmosfarm_members_register_form_policy_fields`

* **설명**: 회원가입 폼의 정책 필드를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_register_form_policy_fields', 'my_custom_policy_fields');
    function my_custom_policy_fields($fields) {
        // 'policy_privacy' 필드를 제거
        if (($key = array_search('policy_privacy', $fields)) !== false) {
            unset($fields[$key]);
        }
        // 새로운 정책 필드 추가
        $fields[] = 'my_custom_policy';
        return $fields;
    }
    ```

### `wpmem_register_fields_arr`

* **설명**: WP-Members 플러그인의 회원가입 필드를 필터링합니다. (WP-Members 코어 훅)
* **파일**: `class/Cosmosfarm_Members.class.php`, `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('wpmem_register_fields_arr', 'my_custom_wpmem_fields');
    function my_custom_wpmem_fields($fields) {
        // 새로운 필드 추가
        $fields['my_custom_field'] = array(
            'name' => 'my_custom_field',
            'type' => 'text',
            'label' => 'My Custom Field',
            'req' => false,
        );
        return $fields;
    }
    ```

### `cosmosfarm_members_page_restriction_message`

* **설명**: 페이지 제한 메시지를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_page_restriction_message', 'my_custom_restriction_message');
    function my_custom_restriction_message($message) {
        return '<p>이 페이지는 회원 전용입니다. 로그인해주세요!</p>';
    }
    ```

### `cosmosfarm_members_page_restriction_login_message`

* **설명**: 페이지 제한 시 로그인 메시지를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_page_restriction_login_message', 'my_custom_restriction_login_message');
    function my_custom_restriction_login_message($message) {
        return '로그인하여 콘텐츠를 확인하세요.';
    }
    ```

### `cosmosfarm_members_page_restriction_register_message`

* **설명**: 페이지 제한 시 회원가입 메시지를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_page_restriction_register_message', 'my_custom_restriction_register_message');
    function my_custom_restriction_register_message($message) {
        return '회원가입하고 모든 콘텐츠를 이용하세요.';
    }
    ```

### `cosmosfarm_members_page_restriction_permission_message`

* **설명**: 페이지 제한 시 권한 부족 메시지를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_page_restriction_permission_message', 'my_custom_restriction_permission_message');
    function my_custom_restriction_permission_message($message) {
        return '<p>이 페이지를 볼 권한이 없습니다.</p>';
    }
    ```

### `cosmosfarm_members_page_restriction`

* **설명**: 페이지 제한 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_page_restriction', 'my_custom_page_restriction_logic');
    function my_custom_page_restriction_logic($page_restriction) {
        // 특정 조건에서 페이지 제한 해제
        if (is_user_logged_in() && current_user_can('administrator')) {
            return false; // 관리자는 항상 접근 가능
        }
        return $page_restriction;
    }
    ```

### `cosmosfarm_members_page_restriction_content`

* **설명**: 페이지 제한 시 표시될 콘텐츠를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_page_restriction_content', 'my_custom_restriction_content', 10, 2);
    function my_custom_restriction_content($content, $restriction_type) {
        if ($restriction_type === 'page_restriction') {
            return '<div class="custom-restricted-content">' . $content . '</div>';
        }
        return $content;
    }
    ```

### `cosmosfarm_members_category_restriction`

* **설명**: 카테고리 제한 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_category_restriction', 'my_custom_category_restriction_logic', 10, 2);
    function my_custom_category_restriction_logic($category_restriction, $category) {
        // 특정 카테고리(ID: 5)는 항상 제한
        if ($category->term_id === 5) {
            return true;
        }
        return $category_restriction;
    }
    ```

### `wpmem_dialogs`

* **설명**: WP-Members 플러그인의 다이얼로그 메시지를 필터링합니다. (WP-Members 코어 훅)
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('wpmem_dialogs', 'my_custom_wpmem_dialogs');
    function my_custom_wpmem_dialogs($dialogs) {
        $dialogs['login_success'] = '환영합니다! 로그인에 성공했습니다.';
        return $dialogs;
    }
    ```

### `cosmosfarm_members_subscription_send_sms_again_message`

* **설명**: 구독 재결제 SMS 메시지를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_send_sms_again_message', 'my_custom_sms_again_message', 10, 3);
    function my_custom_sms_again_message($sms, $order, $product) {
        $sms['content'] = '[재결제 알림] ' . $product->name() . ' 상품 재결제가 완료되었습니다.';
        return $sms;
    }
    ```

### `cosmosfarm_members_order_subscription_again_result`

* **설명**: 구독 재결제 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_order_subscription_again_result', 'my_custom_subscription_again_result');
    function my_custom_subscription_again_result($result) {
        // 재결제 결과에 따라 추가 로직 수행
        if (!$result->success) {
            error_log('재결제 실패: ' . $result->message);
        }
        return $result;
    }
    ```

### `cosmosfarm_members_order_cancel_result`

* **설명**: 주문 취소 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_order_cancel_result', 'my_custom_order_cancel_result');
    function my_custom_order_cancel_result($result) {
        if ($result->success) {
            error_log('주문 취소 성공!');
        }
        return $result;
    }
    ```

### `cosmosfarm_members_order_download_columns`

* **설명**: 주문 다운로드 시 컬럼 목록을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_order_download_columns', 'my_custom_order_download_columns');
    function my_custom_order_download_columns($columns) {
        $columns['custom_field'] = 'Custom Field';
        return $columns;
    }
    ```

### `cosmosfarm_members_order_download_columns_value`

* **설명**: 주문 다운로드 시 특정 컬럼의 값을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_order_download_columns_value', 'my_custom_order_download_column_value', 10, 3);
    function my_custom_order_download_column_value($column_value, $column_key, $order) {
        if ($column_key === 'custom_field') {
            return get_post_meta($order->ID(), '_custom_order_data', true);
        }
        return $column_value;
    }
    ```

### `cosmosfarm_members_order_csv_download_row_data`

* **설명**: 주문 CSV 다운로드 시 각 행의 데이터를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_order_csv_download_row_data', 'my_custom_order_csv_row_data', 10, 2);
    function my_custom_order_csv_row_data($row_data, $order) {
        $row_data['custom_column'] = 'Custom Data for Order ' . $order->ID();
        return $row_data;
    }
    ```

### `cosmosfarm_members_users_csv_download_columns`

* **설명**: 사용자 CSV 다운로드 시 컬럼 목록을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_users_csv_download_columns', 'my_custom_users_csv_columns');
    function my_custom_users_csv_columns($columns) {
        $columns['user_phone'] = 'Phone Number';
        return $columns;
    }
    ```

### `cosmosfarm_members_users_csv_download_add_usermeta`

* **설명**: 사용자 CSV 다운로드 시 추가할 사용자 메타 필드를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_users_csv_download_add_usermeta', 'my_custom_users_csv_usermeta');
    function my_custom_users_csv_usermeta($add_usermeta) {
        $add_usermeta[] = 'billing_address';
        return $add_usermeta;
    }
    ```

### `cosmosfarm_members_users_csv_download_usermeta_value`

* **설명**: 사용자 CSV 다운로드 시 특정 사용자 메타 필드의 값을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_users_csv_download_usermeta_value', 'my_custom_users_csv_usermeta_value', 10, 3);
    function my_custom_users_csv_usermeta_value($meta_value, $meta_key, $user) {
        if ($meta_key === 'billing_address') {
            return get_user_meta($user->ID, 'billing_address_1', true) . ', ' . get_user_meta($user->ID, 'billing_city', true);
        }
        return $meta_value;
    }
    ```

### `cosmosfarm_members_users_csv_download_row_data`

* **설명**: 사용자 CSV 다운로드 시 각 행의 데이터를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_users_csv_download_row_data', 'my_custom_users_csv_row_data', 10, 2);
    function my_custom_users_csv_row_data($row_data, $user) {
        $row_data['custom_user_status'] = 'Active';
        return $row_data;
    }
    ```

### `cosmosfarm_members_social_login_redirect_to`

* **설명**: 소셜 로그인 후 리다이렉트될 URL을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_social_login_redirect_to', 'my_custom_social_login_redirect', 10, 4);
    function my_custom_social_login_redirect($redirect_to, $profile, $user, $random_password) {
        return home_url('/my-account/');
    }
    ```

### `cosmosfarm_members_get_social_api`

* **설명**: 소셜 API 객체를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_get_social_api', 'my_custom_social_api_object', 10, 2);
    function my_custom_social_api_object($api, $channel) {
        // 특정 채널에 대한 사용자 정의 API 객체 반환
        if ($channel === 'my_custom_social') {
            // return new My_Custom_Social_API();
        }
        return $api;
    }
    ```

### `cosmosfarm_members_use_login_timeout`

* **설명**: 로그인 타임아웃 사용 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`, `class/Cosmosfarm_Members_Security.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_use_login_timeout', 'my_custom_login_timeout_setting');
    function my_custom_login_timeout_setting($use_login_timeout) {
        return false; // 로그인 타임아웃 기능 비활성화
    }
    ```

### `cosmosfarm_members_certification_confirm_data`

* **설명**: 본인 인증 확인 데이터를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_certification_confirm_data', 'my_custom_certification_data');
    function my_custom_certification_data($certification) {
        $certification['custom_data'] = 'some_value';
        return $certification;
    }
    ```

### `cosmosfarm_members_subscription_register_card_result`

* **설명**: 구독 카드 등록 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_register_card_result', 'my_custom_register_card_result');
    function my_custom_register_card_result($result) {
        if (!$result->success) {
            error_log('카드 등록 실패: ' . $result->message);
        }
        return $result;
    }
    ```

### `cosmosfarm_members_pre_subscription_request_pay_result`

* **설명**: 구독 결제 요청 전 결과(유효성 검사 등)를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_pre_subscription_request_pay_result', 'my_custom_pre_pay_result');
    function my_custom_pre_pay_result($result) {
        if (!$result->success) {
            $result->message = '결제 요청 전 검증 실패: ' . $result->message;
        }
        return $result;
    }
    ```

### `cosmosfarm_memebers_after_coupon_calculate_price`

* **설명**: 쿠폰 적용 후 가격을 필터링합니다. (오타 Deprecated: `memebers` → `members`)
* **상태**: Deprecated (vNEXT 유지되나 제거 예정). 새 코드에서는 교정된 훅 사용 권장.
* **대체**: `cosmosfarm_members_after_coupon_calculate_price`
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
// 기존(Deprecated) - 호환용
add_filter('cosmosfarm_memebers_after_coupon_calculate_price', 'my_custom_after_coupon_price', 10, 2);
function my_custom_after_coupon_price($price, $product_id) {
    if ($product_id == 123) {
        $price = $price * 0.9;
    }
    return $price;
}
```

### `cosmosfarm_members_after_coupon_calculate_price`

* **설명**: 쿠폰 적용 후 최종 계산된 가격을 필터링합니다. (교정된 정식 훅명)
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
// 신규 권장 훅 사용
add_filter('cosmosfarm_members_after_coupon_calculate_price', function($price, $product_id){
    if ($product_id == 123) {
        $price -= 500; // 정액 추가 할인
    }
    return $price;
}, 10, 2);
```

### `cosmosfarm_members_subscription_request_pay_result`

* **설명**: 구독 결제 요청 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_request_pay_result', 'my_custom_pay_request_result');
function my_custom_pay_request_result($result) {
    if ($result->success) {
        error_log('결제 요청 성공!');
    }
    return $result;
}
```

### `cosmosfarm_members_subscription_request_pay_user`

* **설명**: 구독 결제 요청 시 사용자 객체를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_request_pay_user', 'my_custom_pay_request_user', 10, 4);
function my_custom_pay_request_user($user, $product, $meta_input, $custom_data) {
    // 결제 요청 시 사용자 정보 변경
    // $user->user_email = 'new_email@example.com';
    return $user;
}
```

### `cosmosfarm_members_subscription_request_pay_order_point_to_apply`

* **설명**: 구독 결제 시 적용될 포인트 잔액을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_request_pay_order_point_to_apply', 'my_custom_pay_point_to_apply', 10, 6);
function my_custom_pay_point_to_apply($mycred_balance, $user_id, $coupon_price, $product, $meta_input, $custom_data) {
    // 사용 가능한 최대 포인트 제한
    $max_points_to_use = 1000;
    return min($mycred_balance, $max_points_to_use);
}
```

### `cosmosfarm_members_is_continue_subscription_again`

* **설명**: 구독 재결제를 계속할지 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_is_continue_subscription_again', 'my_custom_continue_subscription_again', 10, 3);
function my_custom_continue_subscription_again($is_continue, $old_order, $product) {
    // 특정 조건에서 재결제 중단
    if ($old_order->get_status() === 'pending') {
        return false; // 이전 주문이 보류 중이면 재결제 중단
    }
    return $is_continue;
}
```

### `cosmosfarm_members_subscription_pay_count_limit`

* **설명**: 구독 결제 횟수 제한을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_pay_count_limit', 'my_custom_pay_count_limit', 10, 3);
function my_custom_pay_count_limit($pay_count_limit, $old_order, $product) {
    // 특정 상품에 대한 결제 횟수 제한
    if ($product->ID() === 456) {
        return 3; // 최대 3회까지 결제 가능
    }
    return $pay_count_limit;
}
```

### `cosmosfarm_members_subscription_again_price`

* **설명**: 구독 재결제 가격을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_again_price', 'my_custom_again_price', 10, 3);
function my_custom_again_price($again_price, $old_order, $product) {
    // 재결제 시 5% 할인 적용
    return $again_price * 0.95;
}
```

### `cosmosfarm_members_subscription_again_point_to_apply`

* **설명**: 구독 재결제 시 적용될 포인트 잔액을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_again_point_to_apply', 'my_custom_again_point_to_apply', 10, 5);
function my_custom_again_point_to_apply($mycred_balance, $user_id, $again_price, $old_order, $product) {
    // 재결제 시 포인트 사용을 50%로 제한
    return $mycred_balance * 0.5;
}
```

### `cosmosfarm_members_subscription_again_failure_email_args`

* **설명**: 구독 재결제 실패 이메일 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_again_failure_email_args', 'my_custom_again_failure_email_args');
function my_custom_again_failure_email_args($args) {
    $args['subject'] = '[중요] 구독 재결제 실패 알림';
    return $args;
}
```

### `cosmosfarm_members_subscription_update_result`

* **설명**: 구독 업데이트 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_subscription_update_result', 'my_custom_subscription_update_result');
function my_custom_subscription_update_result($result) {
    if (!$result->success) {
        error_log('구독 업데이트 실패: ' . $result->message);
    }
    return $result;
}
```

### `cosmosfarm_members_exists_check_result`

* **설명**: 존재 여부 확인 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_exists_check_result', 'my_custom_exists_check_result');
function my_custom_exists_check_result($result) {
    // 특정 조건에서 존재 여부 확인 결과 변경
    // if (something) { $result->success = false; }
    return $result;
}
```

### `cosmosfarm_members_notifications_read_result`

* **설명**: 알림 읽음 처리 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_notifications_read_result', 'my_custom_notifications_read_result');
function my_custom_notifications_read_result($result) {
    if ($result->success) {
        error_log('알림 읽음 처리 성공!');
    }
    return $result;
}
```

### `cosmosfarm_members_notifications_unread_result`

* **설명**: 알림 안 읽음 처리 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_notifications_unread_result', 'my_custom_notifications_unread_result');
function my_custom_notifications_unread_result($result) {
    return $result;
}
```

### `cosmosfarm_members_notifications_delete_result`

* **설명**: 알림 삭제 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_notifications_delete_result', 'my_custom_notifications_delete_result');
function my_custom_notifications_delete_result($result) {
    return $result;
}
```

### `cosmosfarm_members_notifications_subnotify_update_result`

* **설명**: 알림 구독 업데이트 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_notifications_subnotify_update_result', 'my_custom_notifications_subnotify_update_result');
function my_custom_notifications_subnotify_update_result($result) {
    return $result;
}
```

### `cosmosfarm_members_notifications_send_result`

* **설명**: 알림 발송 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_notifications_send_result', 'my_custom_notifications_send_result');
function my_custom_notifications_send_result($result) {
    return $result;
}
```

### `cosmosfarm_members_messages_read_result`

* **설명**: 메시지 읽음 처리 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_messages_read_result', 'my_custom_messages_read_result');
function my_custom_messages_read_result($result) {
    return $result;
}
```

### `cosmosfarm_members_messages_unread_result`

* **설명**: 메시지 안 읽음 처리 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_messages_unread_result', 'my_custom_messages_unread_result');
function my_custom_messages_unread_result($result) {
    return $result;
}
```

### `cosmosfarm_members_messages_delete_result`

* **설명**: 메시지 삭제 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_messages_delete_result', 'my_custom_messages_delete_result');
function my_custom_messages_delete_result($result) {
    return $result;
}
```

### `cosmosfarm_members_messages_subnotify_update_result`

* **설명**: 메시지 구독 업데이트 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_messages_subnotify_update_result', 'my_custom_messages_subnotify_update_result');
function my_custom_messages_subnotify_update_result($result) {
    return $result;
}
```

### `cosmosfarm_members_messages_send_result`

* **설명**: 메시지 발송 결과를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_messages_send_result', 'my_custom_messages_send_result');
function my_custom_messages_send_result($result) {
    return $result;
}
```

### `cosmosfarm_members_redeem_point_coupon_redirect`

* **설명**: 포인트 쿠폰 사용 후 리다이렉트될 URL을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Controller.class.php`

```php
add_filter('cosmosfarm_members_redeem_point_coupon_redirect', 'my_custom_point_coupon_redirect', 10, 4);
function my_custom_point_coupon_redirect($redirect_to, $coupon_id, $mycred_coupon, $user_id) {
    return home_url('/my-points/');
}
```

### `cosmosfarm_members_kboard_notify_display`

* **설명**: KBoard 알림 표시 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`

```php
add_filter('cosmosfarm_members_kboard_notify_display', 'my_custom_kboard_notify_display', 10, 4);
function my_custom_kboard_notify_display($display, $content, $board, $builder) {
    // 특정 게시판(ID: 1)에서는 알림 비활성화
    if ($board->id === '1') {
        return false;
    }
    return $display;
}
```

### `cosmosfarm_members_kboard_notify_text`

* **설명**: KBoard 알림 텍스트를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`

```php
add_filter('cosmosfarm_members_kboard_notify_text', 'my_custom_kboard_notify_text', 10, 4);
function my_custom_kboard_notify_text($text, $content, $board, $builder) {
    return '새로운 댓글 알림 받기';
}
```

### `cosmosfarm_members_kboard_notify_document_insert`

* **설명**: KBoard 문서 삽입 시 알림 데이터를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`

```php
add_filter('cosmosfarm_members_kboard_notify_document_insert', 'my_custom_kboard_notify_document_insert', 10, 5);
function my_custom_kboard_notify_document_insert($notification, $content_uid, $board_id, $content, $board) {
    // 알림 데이터에 추가 정보 삽입
    $notification['custom_data'] = 'document_inserted';
    return $notification;
}
```

### `cosmosfarm_members_kboard_notify_comments_insert`

* **설명**: KBoard 댓글 삽입 시 알림 데이터를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`

```php
add_filter('cosmosfarm_members_kboard_notify_comments_insert', 'my_custom_kboard_notify_comments_insert', 10, 4);
function my_custom_kboard_notify_comments_insert($notification, $comment_uid, $content_uid, $board) {
    $notification['custom_data'] = 'comment_inserted';
    return $notification;
}
```

### `cosmosfarm_members_comments_notify_display`

* **설명**: 댓글 알림 표시 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`

```php
add_filter('cosmosfarm_members_comments_notify_display', 'my_custom_comments_notify_display', 10, 4);
function my_custom_comments_notify_display($display, $content, $board, $builder) {
    return $display;
}
```

### `cosmosfarm_members_comments_notify_text`

* **설명**: 댓글 알림 텍스트를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`

```php
add_filter('cosmosfarm_members_comments_notify_text', 'my_custom_comments_notify_text', 10, 4);
function my_custom_comments_notify_text($text, $content, $board, $builder) {
    return $text;
}
```

### `cosmosfarm_members_comments_notify_insert`

* **설명**: 댓글 삽입 시 알림 데이터를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_comments_notify_insert', 'my_custom_comments_notify_insert', 10, 4);
    function my_custom_comments_notify_insert($notification, $comment_uid, $content_uid, $board) {
        return $notification;
    }
    ```

### `cosmosfarm_members_kboard_notify_default`

* **설명**: KBoard 알림 기본값을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_kboard_notify_default', 'my_custom_kboard_notify_default', 10, 2);
    function my_custom_kboard_notify_default($default, $board) {
        return $default;
    }
    ```

### `cosmosfarm_members_comments_notify_default`

* **설명**: 댓글 알림 기본값을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_KBoard.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_comments_notify_default', 'my_custom_comments_notify_default', 10, 2);
    function my_custom_comments_notify_default($default, $board) {
        return $default;
    }
    ```

### `cosmosfarm_members_messages_subnotify_email_args`

* **설명**: 메시지 알림 이메일 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Message.class.php`

```php
add_filter('cosmosfarm_members_messages_subnotify_email_args', 'my_custom_messages_email_args');
function my_custom_messages_email_args($args) {
    $args['subject'] = '[새 메시지] ' . $args['subject'];
    return $args;
}
```

### `cosmosfarm_members_messages_subnotify_alimtalk_args`

* **설명**: 메시지 알림 알림톡 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Message.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_messages_subnotify_alimtalk_args', 'my_custom_messages_alimtalk_args', 10, 2);
    function my_custom_messages_alimtalk_args($alimtalk_args, $message_object) {
        $alimtalk_args['templateCode'] = 'MY_CUSTOM_MESSAGE_TEMPLATE';
        return $alimtalk_args;
    }
    ```

### `cosmosfarm_members_messages_subnotify_sms_args`

* **설명**: 메시지 알림 SMS 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Message.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_messages_subnotify_sms_args', 'my_custom_messages_sms_args', 10, 2);
    function my_custom_messages_sms_args($sms_args, $message_object) {
        $sms_args['content'] = '[새 메시지] ' . $sms_args['content'];
        return $sms_args;
    }
    ```

### `cosmosfarm_members_notifications_subnotify_email_args`

* **설명**: 알림 알림 이메일 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Notification.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_notifications_subnotify_email_args', 'my_custom_notifications_email_args');
    function my_custom_notifications_email_args($args) {
        return $args;
    }
    ```

### `cosmosfarm_members_notifications_subnotify_alimtalk_args`

* **설명**: 알림 알림 알림톡 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Notification.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_notifications_subnotify_alimtalk_args', 'my_custom_notifications_alimtalk_args', 10, 2);
    function my_custom_notifications_alimtalk_args($alimtalk_args, $notification_object) {
        return $alimtalk_args;
    }
    ```

### `cosmosfarm_members_notifications_subnotify_sms_args`

* **설명**: 알림 알림 SMS 인수를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Notification.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_notifications_subnotify_sms_args', 'my_custom_notifications_sms_args', 10, 2);
    function my_custom_notifications_sms_args($sms_args, $notification_object) {
        return $sms_args;
    }
    ```

### `cosmosfarm_members_login_form_user_logged_in`

* **설명**: 로그인 폼에서 사용자가 로그인되어 있을 때의 레이아웃을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Page_Builder.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_login_form_user_logged_in', 'my_custom_logged_in_layout');
    function my_custom_logged_in_layout($layout) {
        return '<p>이미 로그인되어 있습니다. <a href="' . wp_logout_url() . '">로그아웃</a></p>';
    }
    ```

### `cosmosfarm_members_shortcode_users_page_view_allow`

* **설명**: `[cosmosfarm_members_users]` 숏코드 페이지의 보기 허용 여부를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Page_Builder.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_shortcode_users_page_view_allow', 'my_custom_users_page_allow');
    function my_custom_users_page_allow($allow) {
        // 관리자만 사용자 목록 페이지를 볼 수 있도록 제한
        if (!current_user_can('manage_options')) {
            return false;
        }
        return $allow;
    }
    ```

### `cosmosfarm_members_shortcode_users_page_layout`

* **설명**: `[cosmosfarm_members_users]` 숏코드 페이지의 레이아웃을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Page_Builder.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_shortcode_users_page_layout', 'my_custom_users_page_layout', 10, 2);
    function my_custom_users_page_layout($layout, $page_view_allow) {
        if ($page_view_allow) {
            return '<div class="custom-users-list">' . $layout . '</div>';
        }
        return '<p>사용자 목록을 볼 수 없습니다.</p>';
    }
    ```

### `cosmosfarm_members_closed_site_allow_pages`

* **설명**: 사이트 폐쇄 시 허용될 페이지 목록을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Security.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_closed_site_allow_pages', 'my_custom_closed_site_allow_pages');
    function my_custom_closed_site_allow_pages($allow_pages) {
        $allow_pages[] = '/custom-maintenance-page/';
        return $allow_pages;
    }
    ```

### `cosmosfarm_members_template_header`

* **설명**: 헤더 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_header', 'my_custom_header_template');
    function my_custom_header_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/header.php';
    }
    ```

### `cosmosfarm_members_header_menu_items`

* **설명**: 헤더 메뉴 항목을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_header_menu_items', 'my_custom_header_menu_items');
    function my_custom_header_menu_items($menu_items) {
        $menu_items['my-custom-link'] = array(
            'title' => 'Custom Link',
            'url' => '/custom-page/',
            'current' => false,
        );
        return $menu_items;
    }
    ```

### `cosmosfarm_members_header_menu_current_page`

* **설명**: 헤더 메뉴의 현재 페이지를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_header_menu_current_page', 'my_custom_header_current_page', 10, 2);
    function my_custom_header_current_page($current_page, $menu_items) {
        // 특정 URL에 있을 때 'my-custom-link'를 현재 페이지로 설정
        if (strpos($_SERVER['REQUEST_URI'], '/custom-page/') !== false) {
            return 'my-custom-link';
        }
        return $current_page;
    }
    ```

### `cosmosfarm_members_login_redirect_to`

* **설명**: 로그인 후 리다이렉트될 URL을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_login_redirect_to', 'my_custom_login_redirect');
    function my_custom_login_redirect($redirect_to) {
        return home_url('/dashboard/');
    }
    ```

### `cosmosfarm_members_template_login_form`

* **설명**: 로그인 폼 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_login_form', 'my_custom_login_form_template');
    function my_custom_login_form_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/login-form.php';
    }
    ```

### `cosmosfarm_members_template_change_password_form`

* **설명**: 비밀번호 변경 폼 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_change_password_form', 'my_custom_change_password_form_template');
    function my_custom_change_password_form_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/change-password-form.php';
    }
    ```

### `cosmosfarm_members_template_account_links`

* **설명**: 계정 링크 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_account_links', 'my_custom_account_links_template');
    function my_custom_account_links_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/account-links.php';
    }
    ```

### `cosmosfarm_members_template_login_timeout_popup`

* **설명**: 로그인 타임아웃 팝업 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_login_timeout_popup', 'my_custom_login_timeout_popup_template');
    function my_custom_login_timeout_popup_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/login-timeout-popup.php';
    }
    ```

### `cosmosfarm_members_template_notifications`

* **설명**: 알림 페이지 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_notifications', 'my_custom_notifications_template');
    function my_custom_notifications_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/notifications.php';
    }
    ```

### `cosmosfarm_members_template_notifications_list`

* **설명**: 알림 목록 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_notifications_list', 'my_custom_notifications_list_template');
    function my_custom_notifications_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/notifications-list.php';
    }
    ```

### `cosmosfarm_members_template_notifications_list_item`

* **설명**: 알림 목록 아이템 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_notifications_list_item', 'my_custom_notifications_list_item_template');
    function my_custom_notifications_list_item_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/notifications-list-item.php';
    }
    ```

### `cosmosfarm_members_template_messages`

* **설명**: 메시지 페이지 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_messages', 'my_custom_messages_template');
    function my_custom_messages_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/messages.php';
    }
    ```

### `cosmosfarm_members_template_messages_list`

* **설명**: 메시지 목록 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_messages_list', 'my_custom_messages_list_template');
    function my_custom_messages_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/messages-list.php';
    }
    ```

### `cosmosfarm_members_template_messages_list_item`

* **설명**: 메시지 목록 아이템 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_messages_list_item', 'my_custom_messages_list_item_template');
    function my_custom_messages_list_item_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/messages-list-item.php';
    }
    ```

### `cosmosfarm_members_template_orders`

* **설명**: 주문 페이지 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_orders', 'my_custom_orders_template');
    function my_custom_orders_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/orders.php';
    }
    ```

### `cosmosfarm_members_template_orders_list`

* **설명**: 주문 목록 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_orders_list', 'my_custom_orders_list_template');
    function my_custom_orders_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/orders-list.php';
    }
    ```

### `cosmosfarm_members_template_orders_list_item`

* **설명**: 주문 목록 아이템 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_orders_list_item', 'my_custom_orders_list_item_template');
    function my_custom_orders_list_item_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/orders-list-item.php';
    }
    ```

### `cosmosfarm_members_template_users`

* **설명**: 사용자 페이지 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_users', 'my_custom_users_template');
    function my_custom_users_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/users.php';
    }
    ```

### `cosmosfarm_members_template_users_list`

* **설명**: 사용자 목록 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_users_list', 'my_custom_users_list_template');
    function my_custom_users_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/users-list.php';
    }
    ```

### `cosmosfarm_members_template_users_list_item`

* **설명**: 사용자 목록 아이템 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_users_list_item', 'my_custom_users_list_item_template');
    function my_custom_users_list_item_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/users-list-item.php';
    }
    ```

### `cosmosfarm_members_template_user_profile`

* **설명**: 사용자 프로필 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_user_profile', 'my_custom_user_profile_template');
    function my_custom_user_profile_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/user-profile.php';
    }
    ```

### `cosmosfarm_members_template_point_list`

* **설명**: 포인트 목록 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_point_list', 'my_custom_point_list_template');
    function my_custom_point_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/point-list.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product`

* **설명**: 구독 상품 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product', 'my_custom_subscription_product_template');
    function my_custom_subscription_product_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_title`

* **설명**: 구독 상품 제목 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_title', 'my_custom_subscription_product_title_template');
    function my_custom_subscription_product_title_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-title.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_price`

* **설명**: 구독 상품 가격 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_price', 'my_custom_subscription_product_price_template');
    function my_custom_subscription_product_price_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-price.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_type`

* **설명**: 구독 상품 유형 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_type', 'my_custom_subscription_product_type_template');
    function my_custom_subscription_product_type_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-type.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_first_free`

* **설명**: 구독 상품 첫 달 무료 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_first_free', 'my_custom_subscription_product_first_free_template');
    function my_custom_subscription_product_first_free_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-first-free.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_button`

* **설명**: 구독 상품 버튼 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_button', 'my_custom_subscription_product_button_template');
    function my_custom_subscription_product_button_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-button.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_list`

* **설명**: 구독 상품 목록 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_list', 'my_custom_subscription_product_list_template');
    function my_custom_subscription_product_list_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-list.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_latest`

* **설명**: 최신 구독 상품 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_latest', 'my_custom_subscription_product_latest_template');
    function my_custom_subscription_product_latest_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-latest.php';
    }
    ```

### `cosmosfarm_members_template_subscription_product_single_template`

* **설명**: 단일 구독 상품 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_product_single_template', 'my_custom_subscription_product_single_template');
    function my_custom_subscription_product_single_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-product-single-template.php';
    }
    ```

### `cosmosfarm_members_template_subscription_checkout`

* **설명**: 구독 결제 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_checkout', 'my_custom_subscription_checkout_template');
    function my_custom_subscription_checkout_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-checkout.php';
    }
    ```

### `cosmosfarm_members_subscription_pay_success_url`

* **설명**: 구독 결제 성공 후 리다이렉트될 URL을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_pay_success_url', 'my_custom_pay_success_url', 10, 2);
    function my_custom_pay_success_url($url, $product) {
        return home_url('/payment-success/');
    }
    ```

### `cosmosfarm_members_subscription_m_redirect_url`

* **설명**: 모바일 결제 리다이렉트 URL을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_m_redirect_url', 'my_custom_m_redirect_url', 10, 2);
    function my_custom_m_redirect_url($url, $product) {
        return home_url('/mobile-payment-redirect/');
    }
    ```

### `cosmosfarm_members_subscription_checkout_button_display_text`

* **설명**: 구독 결제 버튼의 표시 텍스트를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_checkout_button_display_text', 'my_custom_checkout_button_text', 10, 4);
    function my_custom_checkout_button_text($text, $product, $is_subscription_first_free, $coupon) {
        if ($is_subscription_first_free) {
            return '첫 달 무료로 시작하기';
        }
        return '지금 결제하기';
    }
    ```

### `cosmosfarm_members_subscription_iamport_pg_mid`

* **설명**: 아임포트 PG MID를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_iamport_pg_mid', 'my_custom_iamport_pg_mid', 10, 2);
    function my_custom_iamport_pg_mid($mid, $product) {
        // 특정 상품에 대한 다른 MID 사용
        if ($product->ID() === 789) {
            return 'my_special_mid';
        }
        return $mid;
    }
    ```

### `cosmosfarm_members_subscription_pay_app_scheme`

* **설명**: 구독 결제 앱 스킴을 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_subscription_pay_app_scheme', 'my_custom_pay_app_scheme', 10, 2);
    function my_custom_pay_app_scheme($scheme, $product) {
        return 'mycustomapp://payment';
    }
    ```

### `cosmosfarm_members_template_subscription_checkout_fields`

* **설명**: 구독 결제 필드 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_subscription_checkout_fields', 'my_custom_checkout_fields_template');
    function my_custom_checkout_fields_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/subscription-checkout-fields.php';
    }
    ```

### `cosmosfarm_members_skin_subscription_checkout_field`

* **설명**: 구독 결제 스킨의 필드를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_skin_subscription_checkout_field', 'my_custom_skin_checkout_field');
    function my_custom_skin_checkout_field($field) {
        // 필드 속성 변경
        if ($field->name === 'billing_phone') {
            $field->placeholder = '휴대폰 번호를 입력하세요';
        }
        return $field;
    }
    ```

### `cosmosfarm_members_template_comments_reviews`

* **설명**: 댓글/리뷰 템플릿 파일 경로를 필터링합니다.
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`
* **예제**:

    ```php
    add_filter('cosmosfarm_members_template_comments_reviews', 'my_custom_comments_reviews_template');
    function my_custom_comments_reviews_template($file_path) {
        return get_stylesheet_directory() . '/cosmosfarm-members/comments-reviews.php';
    }
    ```

### `cosmosfarm_members_template_subscription_payment method`

* **설명**: 구독 결제 수단 템플릿 파일 경로를 필터링합니다. (오타 Deprecated: 공백 → `_`)
* **상태**: Deprecated (향후 제거 예정). 새 훅명 사용 권장.
* **대체**: `cosmosfarm_members_template_subscription_payment_method`
* **파일**: `class/Cosmosfarm_Members_Skin.class.php`

```php
// 구(old) - 호환용
add_filter('cosmosfarm_members_template_subscription_payment method', 'my_custom_payment_method_template');

// 신(new) - 권장 사용
add_filter('cosmosfarm_members_template_subscription_payment_method', 'my_custom_payment_method_template');
function my_custom_payment_method_template($file_path) {
    return get_stylesheet_directory() . '/cosmosfarm-members/subscription-payment-method.php';
}
```

### `cosmosfarm_members_alimtalk_template_paremeter`

* **설명**: 알림톡 템플릿 파라미터를 필터링합니다. (오타 Deprecated: `paremeter` → `parameter`)
* **상태**: Deprecated (향후 제거 예정). 새 훅명 사용 권장.
* **대체**: `cosmosfarm_members_alimtalk_template_parameter`
* **파일**: `class/Cosmosfarm_Members_Sms_Nhn.class.php`, `class/Cosmosfarm_Members_Sms_Solapi.php`

```php
// 구(old) - 호환용
add_filter('cosmosfarm_members_alimtalk_template_paremeter', 'my_custom_alimtalk_template_param', 10, 2);

// 신(new) - 권장 사용
add_filter('cosmosfarm_members_alimtalk_template_parameter', 'my_custom_alimtalk_template_param', 10, 2);
function my_custom_alimtalk_template_param($template_parameter, $template_code) {
    $template_parameter['custom_key'] = 'custom_value';
    return $template_parameter;
}
```
