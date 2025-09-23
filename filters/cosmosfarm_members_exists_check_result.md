# cosmosfarm_members_exists_check_result

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: AJAX를 통해 사용자 메타 정보의 존재 여부를 확인한 후 결과를 필터링합니다.
- **인자 정보**:
  - `$result (array)`: 존재 여부 확인 결과 배열. 'exists'(bool), 'meta_key'(string), 'meta_value'(string), 'message'(string) 키를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_exists_check_result', 'my_custom_exists_check_result');
function my_custom_exists_check_result($result) {
    // 특정 조건에서 존재 여부 확인 결과 변경
    // if (something) { $result->success = false; }
    return $result;
}
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
