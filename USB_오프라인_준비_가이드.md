# USB 오프라인 설치 준비 가이드

> 교육 당일 설치 이슈를 현장에서 즉시 해결하기 위한 강사 준비 가이드
> 교육 전날까지 USB 구성 완료 필요

---

## 왜 USB를 준비하는가

코젠바이오텍 교육의 교훈:
> 오전 세션 전체가 Codex Desktop 설치 이슈로 무너졌다.

기업 교육 현장의 현실:
- 회사 네트워크가 GitHub, Claude.ai, pypi.org 등을 차단하는 경우 多
- 관리자 권한 없이 프로그램 설치 불가능한 PC 존재
- 40명이 동시에 다운로드 → 회사 인터넷 속도 저하
- 한 명의 설치 실패가 전체 진행을 막음

**USB 전략 핵심: 인터넷 없이도, 관리자 권한 없이도 돌아가게 만든다.**

---

## USB 구성 목표

```
USB 드라이브 (권장 용량: 16GB 이상)
│
├── 📁 00_자동설치/              ← 클릭 한 번으로 전체 설치
│   ├── 🔧 윈도우_자동설치.bat
│   └── 🔧 맥_자동설치.sh
│
├── 📁 01_포터블앱/              ← 설치 없이 바로 실행
│   ├── 📁 VSCode_Portable/      ← 압축 해제 후 code.exe 실행
│   ├── 📁 Git_Portable/         ← 설치 없이 git 명령어 사용
│   └── 📁 Python_Portable/      ← 제한적이지만 기본 실행 가능
│
├── 📁 02_설치파일_Windows/      ← 일반 설치 파일
│   ├── VSCodeUserSetup-x64-1.xx.x.exe
│   ├── python-3.12.x-amd64.exe
│   ├── Git-2.4x.x-64-bit.exe
│   └── GitHubDesktopSetup-x64.exe
│
├── 📁 03_설치파일_Mac/          ← Mac용 설치 파일
│   ├── VSCode-darwin-universal.zip
│   ├── python-3.12.x-macos11.pkg
│   └── GitHubDesktop-xxx.zip
│
├── 📁 04_Python_패키지/         ← 오프라인 pip 설치용
│   ├── pandas-2.x.x-cp312-*.whl
│   ├── openpyxl-3.x.x-*.whl
│   ├── requests-2.x.x-*.whl
│   └── pdf2zh_packages/
│
├── 📁 05_VSCode_확장/           ← 오프라인 VSCode 확장 설치
│   ├── ms-ceintl.vscode-language-pack-ko-*.vsix  (한국어 팩)
│   └── ms-python.python-*.vsix                   (Python 확장)
│
└── 📁 06_실습레포_미러/         ← 인터넷 없이 레포 받기
    └── vibe-coding-workshop.bundle  ← git bundle 파일
```

---

## STEP 1. VSCode Portable 만들기

설치 없이 USB에서 바로 실행되는 VSCode.
관리자 권한 필요 없음.

### Windows용 VSCode Portable

1. VSCode 공식 다운로드 페이지 접속:
   `https://code.visualstudio.com/#alt-downloads`
2. Windows → `.zip` 버전 다운로드 (User Installer가 아닌 .zip)
3. 다운로드된 `VSCode-win32-x64-1.xx.x.zip` 압축 해제
4. 해제된 폴더 안에 `data` 폴더 생성 (이게 포터블 모드 활성화)
5. USB의 `01_포터블앱/VSCode_Portable/` 폴더로 이동

```
VSCode_Portable/
├── code.exe          ← 이걸 실행
├── data/             ← 이 폴더가 있어야 포터블 모드
└── ... (나머지 파일들)
```

**수강생 안내:**
```
1. USB의 01_포터블앱/VSCode_Portable/ 폴더를 바탕화면에 복사
2. VSCode_Portable 폴더 안의 code.exe 더블클릭
3. VSCode 실행 완료
```

### Mac용 VSCode

Mac은 포터블 버전이 없으므로 `.zip` 압축 해제 후 바로 사용:

1. `https://code.visualstudio.com/` → Mac → `.zip` 다운로드
2. 압축 해제 → `Visual Studio Code.app` 파일
3. USB에 포함
4. 수강생 PC 응용 프로그램 폴더로 복사 → 실행

---

## STEP 2. Git Portable 만들기 (Windows)

설치 없이 git 명령어를 사용할 수 있는 포터블 버전.

1. `https://git-scm.com/download/win` 접속
2. `Portable ("thumbdrive edition")` 다운로드
   파일명: `PortableGit-2.4x.x-64-bit.7z.exe`
3. 실행 → 압축 해제 경로를 USB `01_포터블앱/Git_Portable/`로 지정
4. 완료 후 USB에 포터블 Git 완성

**수강생 안내:**
```
1. USB의 01_포터블앱/Git_Portable/git-bash.exe 실행
2. Git Bash 창이 열리면 git 명령어 사용 가능
```

**GitHub Desktop 대신 포터블 Git 사용하는 경우:**
```bash
# 레포 클론
git clone https://github.com/[강사계정]/vibe-coding-workshop

# 변경사항 커밋
git add .
git commit -m "변경 내용"
```

---

## STEP 3. Python 설치 파일 준비

### Windows용 Python 설치 파일

1. `https://python.org/downloads/windows/` 접속
2. `Python 3.12.x - Windows installer (64-bit)` 다운로드
3. USB `02_설치파일_Windows/` 폴더에 복사

**현장 설치 안내 (관리자 권한 없이 설치하는 방법):**
```
1. python-3.12.x-amd64.exe 실행
2. 첫 화면에서:
   ✅ "Add Python to PATH" 체크 (매우 중요!)
   → "Install Now" 대신 "Customize installation" 클릭
3. Optional Features: 기본값 유지 → Next
4. Advanced Options:
   ❌ "Install for all users" 체크 해제  ← 관리자 권한 불필요
   ✅ "Add Python to environment variables" 체크
5. Install 클릭
```

### Mac용 Python 설치 파일

1. `https://python.org/downloads/macos/` 접속
2. `macOS 64-bit universal2 installer` 다운로드 (`.pkg` 파일)
3. USB `03_설치파일_Mac/` 폴더에 복사

---

## STEP 4. Python 패키지 오프라인 다운로드

인터넷 없이 `pip install`이 가능하도록 패키지를 미리 다운로드.

### 인터넷 되는 PC에서 실행 (교육 전날)

```bash
# 패키지 다운로드 전용 폴더 생성
mkdir usb_packages
cd usb_packages

# 필요한 패키지 전체 다운로드 (의존성 포함)
pip download pandas
pip download openpyxl
pip download requests
pip download pillow
pip download pdf2zh
pip download chardet
```

> 각 패키지 + 의존성이 `.whl` 또는 `.tar.gz` 파일로 다운로드됨

다운로드된 파일 전체를 USB `04_Python_패키지/` 폴더로 이동.

### 현장에서 오프라인 설치

```bash
# USB 연결 후 (D: 드라이브 예시)
pip install --no-index --find-links=D:\04_Python_패키지 pandas
pip install --no-index --find-links=D:\04_Python_패키지 openpyxl
pip install --no-index --find-links=D:\04_Python_패키지 pdf2zh
```

---

## STEP 5. VSCode 확장 오프라인 설치 파일 준비

### 필요한 확장 다운로드

1. `https://marketplace.visualstudio.com/` 접속
2. 각 확장 검색 → `Download Extension` 링크 클릭 (`.vsix` 파일 다운로드)

**필수 확장:**

| 확장 이름 | 파일명 예시 | 용도 |
|---------|----------|------|
| Korean Language Pack | `ms-ceintl.vscode-language-pack-ko-1.xx.x.vsix` | VSCode 한국어 UI |
| Python | `ms-python.python-2024.x.x.vsix` | Python 실행/디버그 |
| Prettier | `esbenp.prettier-vscode-10.x.x.vsix` | 코드 자동 정리 |

### 현장에서 오프라인 설치

```
VSCode 열기
→ 왼쪽 Extensions 아이콘 클릭 (또는 Ctrl+Shift+X)
→ 우상단 ··· 메뉴 클릭
→ "Install from VSIX..." 클릭
→ USB의 05_VSCode_확장/ 폴더에서 .vsix 파일 선택
→ 설치 완료 후 VSCode 재시작
```

---

## STEP 6. 실습 레포 오프라인 배포

GitHub 접속이 안 될 때 USB로 레포를 나눠주는 방법.

### Bundle 파일 만들기 (인터넷 되는 PC에서)

```bash
# 레포 클론
git clone https://github.com/[강사계정]/vibe-coding-workshop

# bundle 파일 생성 (레포 전체를 파일 1개로 압축)
cd vibe-coding-workshop
git bundle create ../vibe-coding-workshop.bundle --all
```

생성된 `vibe-coding-workshop.bundle` 파일을 USB `06_실습레포_미러/`에 복사.

### 현장에서 bundle로 클론

```bash
# USB의 bundle 파일로 클론 (인터넷 불필요)
git clone D:\06_실습레포_미러\vibe-coding-workshop.bundle vibe-coding-workshop
cd vibe-coding-workshop
git remote set-url origin https://github.com/[강사계정]/vibe-coding-workshop
```

---

## STEP 7. 자동 설치 스크립트

수강생이 USB를 꽂고 이 파일만 실행하면 모두 자동으로 설치됩니다.

### Windows용: `00_자동설치/윈도우_자동설치.bat`

```batch
@echo off
chcp 65001 > nul
echo ============================================
echo  바이브코딩 워크숍 환경 자동 설치
echo ============================================
echo.

:: USB 경로 자동 감지
set "USB=%~dp0.."

:: 1. Python 설치 여부 확인
where python > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] Python 이미 설치됨
    python --version
) else (
    echo [설치 중] Python 설치 시작...
    echo 설치 화면에서 "Add Python to PATH" 체크 후 Install 클릭하세요.
    start /wait "" "%USB%\02_설치파일_Windows\python-3.12.0-amd64.exe"
    echo [완료] Python 설치 완료
)

echo.

:: 2. Git 설치 여부 확인
where git > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] Git 이미 설치됨
    git --version
) else (
    echo [설치 중] Git 설치 시작...
    start /wait "" "%USB%\02_설치파일_Windows\Git-2.43.0-64-bit.exe" /SILENT /NORESTART
    echo [완료] Git 설치 완료
)

echo.

:: 3. GitHub Desktop 설치 여부 확인
if exist "%LOCALAPPDATA%\GitHubDesktop\GitHubDesktop.exe" (
    echo [OK] GitHub Desktop 이미 설치됨
) else (
    echo [설치 중] GitHub Desktop 설치 시작...
    start /wait "" "%USB%\02_설치파일_Windows\GitHubDesktopSetup-x64.exe"
    echo [완료] GitHub Desktop 설치 완료
)

echo.

:: 4. VSCode 설치 여부 확인
where code > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] VSCode 이미 설치됨
) else (
    echo [알림] VSCode가 없습니다.
    echo 포터블 버전을 바탕화면에 복사합니다...
    xcopy /E /I /Y "%USB%\01_포터블앱\VSCode_Portable" "%USERPROFILE%\Desktop\VSCode_Portable"
    echo [완료] 바탕화면의 VSCode_Portable 폴더 안의 code.exe를 실행하세요.
)

echo.

:: 5. Python 필수 패키지 설치
echo [설치 중] Python 패키지 설치...
pip install --no-index --find-links="%USB%\04_Python_패키지" pandas openpyxl requests 2>nul
if %errorlevel% == 0 (
    echo [완료] 패키지 설치 완료 (오프라인)
) else (
    echo [시도 중] 인터넷으로 패키지 설치...
    pip install pandas openpyxl requests
)

echo.

:: 6. 실습 레포 클론
if exist "%USERPROFILE%\Documents\vibe-coding-workshop" (
    echo [OK] 실습 레포 이미 있음
) else (
    echo [복사 중] 실습 레포 복사...
    git clone "%USB%\06_실습레포_미러\vibe-coding-workshop.bundle" "%USERPROFILE%\Documents\vibe-coding-workshop" 2>nul
    if %errorlevel% == 0 (
        echo [완료] 실습 폴더: %USERPROFILE%\Documents\vibe-coding-workshop
    ) else (
        echo [실패] 레포 복사 실패. 강사에게 문의하세요.
    )
)

echo.
echo ============================================
echo  설치 완료! 아래 내용을 확인하세요:
echo ============================================
python --version
git --version
echo.
echo 실습 폴더 위치: %USERPROFILE%\Documents\vibe-coding-workshop
echo.
echo 문제가 있으면 강사에게 알려주세요.
pause
```

### Mac용: `00_자동설치/맥_자동설치.sh`

```bash
#!/bin/bash

echo "============================================"
echo " 바이브코딩 워크숍 환경 자동 설치 (Mac)"
echo "============================================"
echo ""

USB_PATH="$(cd "$(dirname "$0")/.." && pwd)"

# 1. Python 확인
if command -v python3 &> /dev/null; then
    echo "[OK] Python 이미 설치됨"
    python3 --version
else
    echo "[설치 중] Python 설치..."
    open "$USB_PATH/03_설치파일_Mac/python-3.12.0-macos11.pkg"
    echo "설치 완료 후 이 스크립트를 다시 실행하세요."
    exit 1
fi

echo ""

# 2. Git 확인
if command -v git &> /dev/null; then
    echo "[OK] Git 이미 설치됨"
    git --version
else
    echo "[설치 중] Git 설치 (Xcode Command Line Tools)..."
    xcode-select --install
    echo "설치 완료 후 이 스크립트를 다시 실행하세요."
    exit 1
fi

echo ""

# 3. VSCode 확인
if command -v code &> /dev/null; then
    echo "[OK] VSCode 이미 설치됨"
else
    echo "[복사 중] VSCode를 응용 프로그램 폴더로 복사..."
    cp -R "$USB_PATH/03_설치파일_Mac/Visual Studio Code.app" /Applications/
    echo "[완료] VSCode 설치 완료"
fi

echo ""

# 4. Python 패키지
echo "[설치 중] Python 패키지..."
pip3 install --no-index --find-links="$USB_PATH/04_Python_패키지" pandas openpyxl requests 2>/dev/null || \
pip3 install pandas openpyxl requests
echo "[완료] 패키지 설치 완료"

echo ""

# 5. 실습 레포
REPO_PATH="$HOME/Documents/vibe-coding-workshop"
if [ -d "$REPO_PATH" ]; then
    echo "[OK] 실습 레포 이미 있음"
else
    echo "[복사 중] 실습 레포 복사..."
    git clone "$USB_PATH/06_실습레포_미러/vibe-coding-workshop.bundle" "$REPO_PATH"
    echo "[완료] 실습 폴더: $REPO_PATH"
fi

echo ""
echo "============================================"
echo " 설치 완료!"
echo "============================================"
python3 --version
git --version
echo "실습 폴더: $REPO_PATH"
```

---

## STEP 8. 현장 점검 스크립트

교육 시작 전 수강생 PC에서 환경 확인용.

### `환경확인.bat` (Windows)

```batch
@echo off
chcp 65001 > nul
echo =========== 환경 점검 결과 ===========
echo.

:: Python
where python > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] Python:
    python --version
) else (
    echo [X] Python: 미설치 → USB 자동설치 실행 필요
)

:: Git
where git > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] Git:
    git --version
) else (
    echo [X] Git: 미설치 → USB 자동설치 실행 필요
)

:: GitHub Desktop
if exist "%LOCALAPPDATA%\GitHubDesktop\GitHubDesktop.exe" (
    echo [OK] GitHub Desktop: 설치됨
) else (
    echo [X] GitHub Desktop: 미설치
)

:: VSCode
where code > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] VSCode: 설치됨
) else (
    if exist "%USERPROFILE%\Desktop\VSCode_Portable\code.exe" (
        echo [OK] VSCode Portable: 바탕화면에 있음
    ) else (
        echo [X] VSCode: 없음 → USB 포터블 버전 사용
    )
)

:: 실습 레포
if exist "%USERPROFILE%\Documents\vibe-coding-workshop" (
    echo [OK] 실습 레포: 있음
) else (
    echo [X] 실습 레포: 없음 → USB에서 복사 필요
)

:: 인터넷 - Claude.ai
echo.
echo [확인 중] 인터넷 연결...
ping -n 1 claude.ai > nul 2>&1
if %errorlevel% == 0 (
    echo [OK] claude.ai 접속 가능
) else (
    echo [X] claude.ai 접속 불가 → 핫스팟 필요
)

echo.
echo ========================================
echo 문제 있는 항목은 강사에게 알려주세요.
pause
```

---

## USB 준비 체크리스트 (교육 전날)

### 다운로드 필요 파일

```
Windows 설치 파일:
□ VSCodeUserSetup-x64-1.xx.x.exe (약 100MB)
□ python-3.12.x-amd64.exe (약 25MB)
□ Git-2.4x.x-64-bit.exe (약 50MB)
□ GitHubDesktopSetup-x64.exe (약 130MB)

Mac 설치 파일:
□ VSCode-darwin-universal.zip (약 200MB)
□ python-3.12.x-macos11.pkg (약 45MB)

포터블 앱:
□ VSCode .zip 버전 압축 해제 + data 폴더 생성
□ PortableGit-2.4x.x-64-bit.7z.exe 실행 해제

Python 패키지 (pip download로 준비):
□ pandas 및 의존성
□ openpyxl 및 의존성
□ requests 및 의존성

VSCode 확장:
□ Korean Language Pack .vsix
□ Python Extension .vsix

실습 레포:
□ git bundle 파일 생성 완료

스크립트:
□ 윈도우_자동설치.bat 테스트 완료
□ 맥_자동설치.sh 테스트 완료
□ 환경확인.bat 테스트 완료
```

### 현장 배포 순서

```
교육 시작 30분 전:
1. USB를 강사 PC에 먼저 꽂고 파일 확인
2. 보조 강사에게 USB 사본 1개 추가 배포
3. 수강생 입장 시 "PC 켜두고 기다려달라" 안내

교육 시작 시:
1. 전체 공지: "환경확인.bat 실행해보세요"
2. [X] 항목이 있는 분 손들기 → USB 전달
3. 자동설치.bat 실행 안내
4. 설치 중인 분은 강사 화면 같이 보기

설치 완료 후:
1. 전체 환경확인.bat 재실행
2. 전원 [OK] 확인 후 CH1 시작
```

---

## 최후 수단: 브라우저만으로 진행

모든 설치가 실패했을 때 아무것도 설치 없이 진행하는 방법.

| 기능 | 대체 방법 |
|------|---------|
| VSCode | 브라우저판 VSCode: `vscode.dev` |
| Git 클론 | GitHub 웹에서 `Code → Download ZIP` |
| Python 실행 | `https://replit.com` (브라우저 IDE) |
| 파일 편집 | Google Docs 또는 메모장 |
| AI 도구 | Claude.ai, ChatGPT (핫스팟 사용) |

> **브라우저만 있으면 CH1~CH3는 진행 가능합니다.**
> Python이 필요한 CH4(pdf2zh)만 제한됩니다.
> 이 경우 CH4는 웹 버전 번역 도구로 대체합니다.

---

## 준비물 최종 요약

```
USB 안에 반드시 있어야 할 것 (우선순위 순):

1순위 (없으면 교육 불가):
  - 환경확인.bat / .sh
  - 윈도우_자동설치.bat / 맥_자동설치.sh
  - vibe-coding-workshop.bundle (레포 오프라인 배포)

2순위 (설치 안 된 수강생 대응):
  - python-3.12.x-amd64.exe
  - Git-2.4x.x-64-bit.exe
  - VSCode_Portable (압축 해제본)

3순위 (인터넷 차단 환경):
  - 04_Python_패키지/ (pip 오프라인용)
  - 05_VSCode_확장/ (.vsix 파일들)
  - GitHubDesktopSetup-x64.exe
```
