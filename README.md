# PowerShell icacls 명령어 정리

`icacls`는 파일/폴더의 권한(ACL)을 확인·수정하는 명령어입니다.

## 1. 권한 조회
```powershell
icacls "C:\경로\파일"
```
해당 파일/폴더의 현재 권한 목록을 출력합니다.

## 2. 권한 부여 (/grant)
```powershell
icacls "C:\경로" /grant 사용자명:(권한)
```
- 예: `icacls "C:\data" /grant Users:(R)` → Users에게 읽기 권한 부여
- `:r` 을 붙이면(`/grant:r`) 기존 권한을 대체(replace)합니다.

## 3. 권한 제거 (/remove)
```powershell
icacls "C:\경로" /remove 사용자명
```
- `/remove:g` → 부여(grant)된 권한 제거
- `/remove:d` → 거부(deny)된 권한 제거

## 4. 권한 거부 (/deny)
```powershell
icacls "C:\경로" /deny 사용자명:(권한)
```
특정 사용자의 접근을 명시적으로 차단합니다.

## 5. 하위 항목에 적용 (/T, /C)
```powershell
icacls "C:\경로" /grant Users:(R) /T /C
```
- `/T` → 하위 폴더·파일까지 재귀 적용
- `/C` → 오류가 나도 계속 진행

## 6. 소유권 변경 (/setowner)
```powershell
icacls "C:\경로" /setowner 사용자명
```

## 7. 권한 백업 / 복원
```powershell
icacls "C:\경로" /save acl.txt /T      # 백업
icacls "C:\경로" /restore acl.txt      # 복원
```

## 8. 상속 설정 (/inheritance)
```powershell
icacls "C:\경로" /inheritance:e   # 상속 활성화(enable)
icacls "C:\경로" /inheritance:d   # 상속 비활성화(변환)
icacls "C:\경로" /inheritance:r   # 상속 제거(remove)
```

## 9. 기본 권한으로 초기화 (/reset)
```powershell
icacls "C:\경로" /reset /T
```
상위 폴더로부터 상속된 기본 권한으로 재설정합니다.

---

## 주요 권한 약어
| 약어 | 의미 |
|------|------|
| `F` | 모든 권한 (Full control) |
| `M` | 수정 (Modify) |
| `RX` | 읽기 및 실행 |
| `R` | 읽기 |
| `W` | 쓰기 |
| `D` | 삭제 |
