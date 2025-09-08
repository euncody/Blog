PHP에서 **`basename()`** 함수는 \*\*파일 경로에서 마지막 요소(파일 이름 부분)\*\*만 잘라내는 함수입니다.

---

## 📖 기본 문법

```php
basename(string $path, string $suffix = ""): string
```

* **`$path`**: 파일이나 디렉토리의 전체 경로
* **`$suffix`** *(선택)* : 파일명 끝에 특정 확장자가 있으면 잘라내줌

---

## ✅ 예시

### 1. 기본 사용

```php
echo basename("/var/www/html/index.php");
// 출력: index.php
```

### 2. 확장자 제거

```php
echo basename("/var/www/html/index.php", ".php");
// 출력: index
```

### 3. 디렉토리 이름만 가져오기

```php
echo basename("/var/www/html/");
// 출력: html
```

---

## 📌 활용 포인트

* 업로드된 파일 경로에서 **파일 이름만 추출**할 때 자주 씀
* `$_FILES['file']['name']`과 함께 보안 점검 시 유용
* `dirname()` 함수와 반대 개념 (경로에서 **디렉토리 부분만** 잘라냄)

---

## ⚠️ 주의할 점

* 단순히 문자열에서 마지막 슬래시(`/`) 뒤를 잘라내는 기능이라, **보안 필터링용으로만 쓰면 위험**합니다.
  예: 사용자가 `../../../etc/passwd` 같은 경로를 올릴 수 있으니, `basename()`만 쓰지 말고 추가 검증 필요.

---

👉 정리하면,
`basename()` = **경로 문자열에서 마지막 파일/디렉토리 이름만 가져오는 함수**
