# 🐘 PHP 실무용 문법

> 실무에서 PHP 개발 시 자주 사용하는 문법과 패턴 정리

---

## 📝 1. 기본 문법 (변수·조건·반복)

```php
<?php
// 변수
$name = "홍길동";
$age = 25;

// 조건문
if ($age >= 20) {
    echo "성인";
} else {
    echo "미성년자";
}

// 반복문
for ($i = 0; $i < 5; $i++) {
    echo $i;
}

$items = ["사과", "바나나", "포도"];
foreach ($items as $item) {
    echo $item;
}
```

> 💡 `foreach`는 배열이나 DB결과 처리할 때 거의 항상 쓰임

---

## 📁 2. 배열 & 연관배열

```php
// 일반 배열
$arr = [1, 2, 3];

// 연관 배열 (key-value)
$user = [
    "name" => "홍길동",
    "email" => "hong@test.com"
];

echo $user["name"];
```

> 💡 JSON, DB 결과, 설정값 등을 다룰 때 연관배열을 많이 사용함

---

## 🧩 3. 함수 & include

```php
// 함수 정의
function greet($name = "손님") {
    return "안녕하세요, $name 님!";
}

echo greet("철수");

// 외부 파일 포함
include "config.php";
require "db.php";
```

> 💡 `require`는 실패 시 오류 발생, `include`는 경고만 — 설정 파일은 `require`가 안전

---

## ⚙️ 4. 클래스 & 객체지향

```php
class User {
    public $name;

    public function __construct($name) {
        $this->name = $name;
    }

    public function greet() {
        return "안녕하세요, {$this->name} 님!";
    }
}

$user = new User("영희");
echo $user->greet();
```

> 💡 서비스 로직, 모델, 유틸성 모듈 등은 거의 전부 클래스 기반으로 구현

---

## 💾 5. DB 연동 (PDO)

```php
try {
    $pdo = new PDO("mysql:host=localhost;dbname=test", "root", "");
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    $stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
    $stmt->execute(["email" => "test@test.com"]);
    $result = $stmt->fetchAll(PDO::FETCH_ASSOC);

    print_r($result);
} catch (PDOException $e) {
    echo "DB 오류: " . $e->getMessage();
}
```

> 💡 `PDO`는 보안(SQl Injection 방지)과 확장성 측면에서 실무 기본

---

## 🧪 6. 예외처리 & 에러 핸들링

```php
function divide($a, $b) {
    if ($b === 0) {
        throw new Exception("0으로 나눌 수 없습니다.");
    }
    return $a / $b;
}

try {
    echo divide(10, 0);
} catch (Exception $e) {
    echo "에러: " . $e->getMessage();
}
```

> 💡 예외는 DB, 외부 API 연동 등에서 반드시 사용

---

## 📦 7. Composer & autoload

```bash
# composer.json 생성
composer init
# 외부 패키지 설치
composer require guzzlehttp/guzzle
```

```php
require 'vendor/autoload.php';

$client = new \GuzzleHttp\Client();
```

> 💡 실무에서는 거의 항상 **Composer로 라이브러리 관리** (PSR-4 autoload)

---

## 🌐 8. HTTP 요청/응답 다루기

```php
// GET, POST
$name = $_GET['name'] ?? '손님';
$email = $_POST['email'] ?? '';

// header 설정
header('Content-Type: application/json');

// JSON 응답
echo json_encode(['name' => $name, 'email' => $email]);
```

> 💡 REST API 만들 때 필수

---

## 📌 9. 실무에서 자주 쓰는 유틸

```php
// 날짜
echo date("Y-m-d H:i:s");

// 문자열 처리
echo trim("  hello  ");
echo strtoupper("php");

// 파일
file_put_contents("log.txt", "에러 로그", FILE_APPEND);
```

---

## 📚 10. 네임스페이스 & 파일 구조화

```php
namespace App\Service;

class Mailer {
    public function send() { /* ... */ }
}
```

```php
use App\Service\Mailer;

$mailer = new Mailer();
```

> 💡 대규모 프로젝트에서는 네임스페이스로 구조 분리

---

## ✅ 요약

| 주제 | 설명 |
|---|---|
| 변수/조건/반복 | 로직 구현의 기본 |
| 배열/연관배열 | 데이터 구조 다룸 |
| 함수/클래스 | 재사용 가능한 코드 작성 |
| PDO | 안전한 DB 접근 |
| try/catch | 에러/예외 처리 |
| Composer | 패키지 및 autoload 관리 |
| HTTP | API 요청·응답 처리 |
| 유틸 함수 | 문자열·날짜·파일 등 |
| 네임스페이스 | 대규모 구조화 |
