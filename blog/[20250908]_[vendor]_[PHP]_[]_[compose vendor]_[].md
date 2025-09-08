PHP에서 **`vendor`** 라는 건 보통 **Composer**(PHP의 의존성 관리 도구)를 사용할 때 자동으로 생기는 \*\*디렉토리(폴더)\*\*를 말합니다.

---

## 📌 정리하자면

* **Composer**: PHP에서 외부 라이브러리(패키지)를 설치/관리하는 툴
* **`vendor/` 디렉토리**: Composer가 라이브러리를 설치하는 기본 위치

즉, 내가 어떤 라이브러리를 `composer require` 명령어로 설치하면, 그 라이브러리의 소스코드와 필요한 의존성들이 전부 **`vendor/`** 폴더 안에 들어가요.

---

## 📂 구조 예시

```text
my-project/
├── composer.json        ← 내가 설치한 라이브러리 목록과 버전 기록
├── composer.lock        ← 실제 설치된 버전 고정
└── vendor/              ← 라이브러리들이 설치되는 곳
    ├── autoload.php     ← 자동 로딩 설정 파일
    ├── monolog/         ← 설치한 패키지 예시 (로그 관련)
    ├── guzzlehttp/      ← 설치한 패키지 예시 (HTTP 클라이언트)
    └── composer/        ← Composer 내부 관리용 코드
```

---

## 🚀 핵심

1. **`vendor` = 라이브러리 저장소**
   → 내가 설치한 모든 외부 패키지가 이 폴더 안에 들어감

2. **`autoload.php`**
   → `require 'vendor/autoload.php';` 한 줄만 넣으면, 설치된 모든 라이브러리를 자동으로 불러올 수 있음

---

👉 그래서 보통 PHP 프로젝트 코드 맨 위에 이렇게 쓰는 거예요:

```php
<?php
require __DIR__ . '/vendor/autoload.php';

// 이제 composer로 설치한 라이브러리들을 그냥 바로 사용 가능!
```