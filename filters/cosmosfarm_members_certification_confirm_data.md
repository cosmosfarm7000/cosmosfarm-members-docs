# cosmosfarm_members_certification_confirm_data

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 아임포트 인증 API에서 인증 데이터를 가져온 후, 해당 데이터를 필터링합니다.
- **인자 정보**:
  - `$certification (object)`: 아임포트 인증 API에서 반환된 인증 데이터 객체. 인증 성공/실패 상태, 사용자 정보, 인증 번호 등의 데이터를 포함합니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_certification_confirm_data', 'my_custom_certification_data');
    function my_custom_certification_data($certification) {
        $certification['custom_data'] = 'some_value';
        return $certification;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
