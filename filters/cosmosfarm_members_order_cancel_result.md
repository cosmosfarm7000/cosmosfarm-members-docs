# cosmosfarm_members_order_cancel_result

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 사용자가 주문을 취소한 후, 취소 결과를 처리할 때 실행됩니다. 주문 취소 성공/실패 상태를 필터링할 수 있습니다.
- **인자 정보**:
  - `$result (object)`: 주문 취소 결과 객체. success (bool), message (string) 등의 속성을 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_order_cancel_result', 'my_custom_order_cancel_result');
function my_custom_order_cancel_result($result) {
    if ($result->success) {
        error_log('주문 취소 성공!');
    }
    return $result;
}
```

- **주의 사항**: 필터 함수는 반드시 결과 객체를 반환해야 합니다. 결과 객체의 구조를 변경할 때는 success와 message 속성을 유지하는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_order_subscription_again_result`
