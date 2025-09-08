**`$uploaddir`** 과 **`img`** 는 보통 PHP에서 파일 업로드나 이미지 경로를 다룰 때 자주 등장하는 부분입니다. 하나씩 정리해드릴게요.

---

## 1. `$uploaddir`란?

* 업로드한 파일이 실제로 저장될 **서버의 디렉토리 경로**를 변수에 담아두는 것.
* 보통 절대경로 또는 상대경로로 지정합니다.

### 예시

```php
$uploaddir = __DIR__ . '/uploads/';   // 현재 PHP 파일 기준 uploads 폴더
$uploadfile = $uploaddir . basename($_FILES['userfile']['name']);
```

👉 이렇게 하면 업로드된 파일이 **`프로젝트/uploads/파일명`** 으로 저장됩니다.

---

## 2. `img` 폴더란?

* 이미지 파일을 보관하기 위해 따로 만들어두는 폴더입니다.
* 웹에서 접근할 수 있도록 `public`, `htdocs`, `www` 같은 **웹 루트 디렉토리 아래** 두는 경우가 많습니다.

예시 구조:

```
my-project/
├── index.php
├── upload.php
├── uploads/        ← 업로드 전용 (보안상 외부 접근 제한 권장)
└── img/            ← 공개용 이미지 (브라우저에서 접근 가능)
```

---

## 3. 디렉토리 구조 예시 (일반적인 PHP 웹 프로젝트)

```
project-root/
├── public/              ← 웹 루트 (웹서버 문서 루트)
│   ├── index.php
│   ├── img/             ← 이미지 저장소 (브라우저 접근 가능)
│   └── css/             ← 스타일시트
│
├── uploads/             ← 업로드 원본 저장 (웹 접근 차단 권장)
│
├── src/                 ← PHP 소스코드
│   └── upload.php       ← 업로드 처리
│
└── vendor/              ← composer 라이브러리
```

---

## 4. 경로 작성 방법

### (1) 서버에 저장할 경로

```php
$uploaddir = __DIR__ . '/../uploads/';   // PHP 코드 기준 uploads 디렉토리
$uploadfile = $uploaddir . basename($_FILES['userfile']['name']);
move_uploaded_file($_FILES['userfile']['tmp_name'], $uploadfile);
```

### (2) 브라우저에서 접근할 경로

```php
<img src="/img/example.jpg" alt="이미지">
```

👉 즉,

* **실제 저장 경로**: `/var/www/project/uploads/abc.png`
* **웹에서 접근하는 경로**: `https://example.com/img/abc.png`

이렇게 **저장 경로**와 **웹 경로**는 구분하는 게 안전합니다.

---

✅ 정리

* `$uploaddir` = 서버 안에서 파일을 저장할 물리적 디렉토리
* `img` = 클라이언트(브라우저)가 접근할 수 있는 이미지 전용 폴더
* 디렉토리 구조를 나눠서 `uploads`는 서버 내부 보관용, `img`는 공개용으로 쓰면 보안상 더 안전함