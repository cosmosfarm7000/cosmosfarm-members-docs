# cosmosfarm_members_page_restriction_content

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members.class.php`
- **실행 시점**: 페이지가 제한되어 접근할 수 없을 때 표시될 콘텐츠를 구성할 때 실행됩니다. 제한된 페이지에 표시될 메시지나 UI를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$content (string)`: 제한 페이지에 표시될 HTML 콘텐츠.
  - `$restriction_type (string)`: 제한 유형. 'page_restriction' 등의 값이 올 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_page_restriction_content', 'my_custom_restriction_content', 10, 2);
  function my_custom_restriction_content($content, $restriction_type) {
    if ($restriction_type === 'page_restriction') {
        return '<div class="custom-restricted-content">' . $content . '</div>';
    }
    return $content;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 HTML 문자열을 반환해야 합니다. 반환된 콘텐츠는 제한된 페이지에 표시됩니다.
- **관련 훅**: `cosmosfarm_members_page_restriction`, `cosmosfarm_members_page_restriction_message`
