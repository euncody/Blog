Naver Cloud Platform(NCP)의 **Source Repository**(Git 저장소)에서 사용하는 \*\*Personal Access Token(Git 인증 토큰)\*\*은 다음과 같이 동작합니다:

---

### 🔑 토큰은 사용자 단위

* NCP에서는 **개별 repository마다 토큰을 발급하는 것이 아니라**,
  **사용자 계정 단위로 1개의 Personal Access Token**을 발급받아 사용합니다.
* 이 토큰은 그 계정이 **접근 권한을 가진 모든 repository**에 접근할 수 있습니다.
  (즉, 여러 개의 repo가 있어도 **하나의 토큰으로 전부 접근 가능**)

---

### ⚙️ 사용 방식

* 토큰 발급 후, `git clone`, `git pull`, `git push` 등을 실행할 때
  비밀번호 대신 **토큰을 사용**합니다.
* 예시:

  ```bash
  git clone https://repo.ncloud.com/your-project.git
  Username: <your NCP username>
  Password: <your Personal Access Token>
  ```

---

### 📌 주의할 점

* 토큰은 **비밀번호처럼 취급**해야 하며, 유출 시 모든 repo 접근이 가능하므로 반드시 안전하게 보관해야 합니다.
* 필요하면 토큰을 **재발급 및 폐기**할 수 있습니다.
* 조직에서 여러 계정을 사용하는 경우, **계정별로 별도의 토큰**이 필요합니다. (repo별이 아니라 **계정별**)