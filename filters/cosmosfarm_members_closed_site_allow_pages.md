# cosmosfarm_members_closed_site_allow_pages

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Security.class.php`
- **실행 시점**: 폐쇄된 사이트에서 접근 가능한 페이지들을 확인할 때, 기본 허용 페이지 목록을 필터링합니다.
- **인자 정보**:
  - `$allow_pages (array)`: 폐쇄된 사이트에서 접근 가능한 페이지들의 ID 배열. 기본적으로 로그인 페이지, 회원가입 페이지, 계정 페이지의 ID가 포함됩니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_closed_site_allow_pages', 'my_custom_closed_site_allow_pages');
    function my_custom_closed_site_allow_pages($allow_pages) {
        $allow_pages[] = '/custom-maintenance-page/';
        return $allow_pages;
    }
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
