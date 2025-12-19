# cosmosfarm_members_dodopayments_currencies

DodoPayments에서 지원하는 통화 목록을 필터링합니다.

## 정의 위치

`class/pg/Cosmosfarm_Members_PG_Dodopayments.class.php` - `init()` 메서드

## 설명

DodoPayments PG 초기화 시 허용되는 통화 목록을 수정할 수 있습니다. 기본적으로 USD, EUR, GBP, KRW를 지원하며, 이 필터를 통해 통화를 추가하거나 제거할 수 있습니다.

## 매개변수

| 매개변수 | 타입 | 설명 |
|----------|------|------|
| `$allowed_currencies` | `array` | 허용된 통화 코드 배열 (기본값: `['USD', 'EUR', 'GBP', 'KRW']`) |

## 반환값

| 타입 | 설명 |
|------|------|
| `array` | 수정된 통화 코드 배열 |

## 예제

### 통화 추가

```php
add_filter('cosmosfarm_members_dodopayments_currencies', 'add_jpy_currency');
function add_jpy_currency($currencies) {
    // 일본 엔화 추가
    $currencies[] = 'JPY';
    return $currencies;
}
```

### 특정 통화만 허용

```php
add_filter('cosmosfarm_members_dodopayments_currencies', 'allow_only_usd');
function allow_only_usd($currencies) {
    // USD만 허용
    return array('USD');
}
```

### 통화 제거

```php
add_filter('cosmosfarm_members_dodopayments_currencies', 'remove_krw_currency');
function remove_krw_currency($currencies) {
    // KRW 제거
    $key = array_search('KRW', $currencies);
    if ($key !== false) {
        unset($currencies[$key]);
    }
    return array_values($currencies);
}
```

## 관련 훅

- 없음

## 참고

- DodoPayments는 글로벌 결제를 지원하는 해외 PG입니다.
- 통화 코드는 ISO 4217 표준을 따릅니다.
- 실제 지원 통화는 DodoPayments 계정 설정에 따라 다를 수 있습니다.
