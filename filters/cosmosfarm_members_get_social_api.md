# cosmosfarm_members_get_social_api

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`
- **실행 시점**: 소셜 로그인 채널에 대한 API 객체를 로드할 때 실행됩니다.
- **인자 정보**:
  - `$api (object|false)`: 소셜 로그인 API 객체. 지원되지 않는 채널인 경우 false입니다.
  - `$channel (string)`: 소셜 로그인 채널 이름 (예: 'naver', 'kakao', 'google', 'facebook', 'twitter', 'apple').
- **예제 코드**:

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

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
