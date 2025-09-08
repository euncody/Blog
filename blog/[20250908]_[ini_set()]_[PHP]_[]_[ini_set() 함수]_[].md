## 📌 `ini_set()` 함수란?

* PHP 설정값(`php.ini` 파일에 정의된 설정들)을 \*\*실행 중(runtime)\*\*에 바꿀 수 있게 해주는 함수입니다.
* 즉, 서버 전체 설정을 바꾸는 게 아니라, **현재 실행되는 스크립트에서만 임시로 적용**돼요.

---

## 📖 기본 문법

```php
ini_set(string $option, string|int $value): string|false
```

* `$option`: 바꾸고 싶은 설정 이름 (예: `display_errors`, `memory_limit`)
* `$value`: 설정할 값
* 반환값: 이전에 설정돼 있던 값 (실패하면 `false`)

---

## ✅ 예시들

### 1. 에러 메시지 보이게 하기

```php
ini_set("display_errors", "1"); // 에러 출력 ON
error_reporting(E_ALL);         // 모든 에러 보고
```

### 2. 메모리 제한 늘리기

```php
ini_set("memory_limit", "512M");
```

### 3. 실행 시간 제한 늘리기

```php
ini_set("max_execution_time", "300"); // 300초
```

---

## ⚠️ 주의사항

* 모든 설정이 `ini_set()`으로 변경 가능한 건 아닙니다.
  (`php.ini`에서 **PHP\_INI\_SYSTEM** 같은 권한 레벨이 있는 설정은 변경 불가 → 서버 전체 설정을 바꿔야 함)
* `ini_set()`으로 변경한 설정은 **그 스크립트가 끝나면 원래대로 돌아감**

---

👉 정리하면, `ini_set()`은 **php.ini 수정 권한이 없거나, 특정 스크립트에서만 일시적으로 설정을 바꾸고 싶을 때** 사용하는 함수입니다.
