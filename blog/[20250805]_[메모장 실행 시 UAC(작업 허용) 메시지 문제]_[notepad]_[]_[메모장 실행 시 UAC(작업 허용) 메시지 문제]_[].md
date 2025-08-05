# 메모장 실행 시 UAC(작업 허용) 메시지 문제 해결

## 문제 요약
Windows에서 메모장(Notepad)을 실행할 때 매번 "이 앱이 디바이스를 변경하도록 허용하시겠습니까?"라는 UAC(User Account Control) 메시지가 나타나는 현상.

## 원인 분석 결과
- 실제 문제의 원인은 **메모장(notepad.exe)**이 아닌, **Notepad++**가 항상 **관리자 권한으로 실행되도록 설정**되어 있었음.
- 해당 설정은 **레지스트리**에서 `RUNASADMIN` 값으로 확인됨.

## 레지스트리 확인 결과
경로:
```
HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers
```

설정 항목:
```
C:\Program Files\Notepad++\notepad++.exe    =>    RUNASADMIN
```
- 이 값은 Notepad++ 실행 시 **항상 관리자 권한으로 실행되도록 강제**함.
- 따라서 UAC 메시지가 **메모장이 아닌 Notepad++ 실행 시** 발생함.

## 해결 방법
### 1. 레지스트리에서 RUNASADMIN 설정 제거
1. `regedit` 실행 (Win + R → regedit)
2. 다음 경로 이동:
   ```
   HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers
   ```
3. 오른쪽 창에서 다음 키 삭제:
   ```
   C:\Program Files\Notepad++\notepad++.exe
   ```
4. 레지스트리 편집기 종료 후 **컴퓨터 재부팅**

### 2. Notepad++ 바로가기 확인 (선택 사항)
- Notepad++ 아이콘 우클릭 → "속성" → "호환성" 탭
- "관리자 권한으로 이 프로그램 실행" 체크 여부 확인 및 해제

## 확인 사항
| 항목                        | 상태                     |
|---------------------------|------------------------|
| 메모장(notepad.exe)       | 정상 실행 (관리자 아님) |
| Notepad++ 실행 시 UAC 메시지 | 관리자 권한 강제 실행됨   |
| 레지스트리 설정 원인 여부     | RUNASADMIN 설정 존재     |

## 결론
- 문제의 직접적인 원인은 **Notepad++의 관리자 권한 실행 설정**
- 레지스트리에서 해당 값을 삭제함으로써 **UAC 메시지 제거 가능**
- 기본 메모장(notepad.exe)은 문제 없음


