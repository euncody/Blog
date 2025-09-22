

## 📌 PHP 프로젝트에서 `routes.php`의 역할

### 1. **URL(엔드포인트)과 컨트롤러 매핑**

* 사용자가 브라우저나 클라이언트에서 `http://example.com/employee/list` 를 호출하면
  → `routes.php`에서 해당 URL과 연결된 **Controller::Method** 를 찾아 실행합니다.
* 즉, **“주소창에 들어온 요청을 어떤 PHP 코드로 보낼지 결정하는 지도 역할”** 을 해요.

예:

```php
$app->get('/employee/list', EmployeeController::class . ':list');
```

👉 `/employee/list` 요청이 들어오면 `EmployeeController`의 `list()` 메서드 실행.

---

### 2. **HTTP Method 관리**

* REST API는 보통 메서드별로 동작이 달라요.

  * `GET /employee/{id}` → 직원 조회
  * `POST /employee` → 직원 생성
  * `PUT /employee/{id}` → 직원 수정
  * `DELETE /employee/{id}` → 직원 삭제
* `routes.php`는 URL + Method 조합을 관리하면서 API의 규칙성을 유지합니다.

---

### 3. **미들웨어 연결**

* 인증, 권한 체크, 유효성 검사 같은 공통 로직을 라우트에 붙일 수 있습니다.

```php
$app->group('/employee', function ($group) {
    $group->post('/create', EmployeeController::class . ':create')
          ->add(new ValidationMiddleware([...]));
})->add(JwtAuthMiddleware::class);
```

👉 `/employee/*` 요청 전체에 **JWT 인증 필터** 적용.
👉 `/employee/create` 요청엔 **ValidationMiddleware** 추가.

---

### 4. **API 문서/구조의 근간**

* 프로젝트의 API 설계를 한눈에 볼 수 있는 곳이 `routes.php`입니다.
* Swagger 같은 문서화 툴도 이 파일을 토대로 엔드포인트를 추출해서 `openapi.yml`을 만들 수 있어요.

---

## ✅ 비유

* **`routes.php` = 네비게이션 지도**
* 손님이 주소(URL)를 입력하면, 그 주소가 어느 건물(Controller)이고, 그 건물의 몇 호실(Method)인지 안내해 주는 역할.
