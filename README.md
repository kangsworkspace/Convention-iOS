# Convention-iOS

이 문서는 iOS 프로젝트 일관된 코드 스타일을 유지하고,  
AI 클라이언트에게 컨벤션을 명확히 전달하기 위해 작성한 개인 코드 컨벤션입니다.  
(Updated At - 25.07.07)

---

## 목차

1.  [프로젝트 구조 (Project Structure)](#1-프로젝트-구조)
2.  [네이밍 컨벤션 (Naming Convention)](#2-네이밍-컨벤션)
3.  [코딩 스타일 (Coding Style)](#3-코딩-스타일)
4.  [Git & 버전 관리](#4-git--버전-관리)
5.  [문서화 (Documentation)](#5-문서화)
6.  [세부 규칙 (Detailed Rule)](#6-세부-규칙)
      - [6-1. 함수의 파라미터 레이블 사용 규칙](#6-1-함수의-파라미터-레이블-사용-규칙)

---

## 1. 프로젝트 구조

공통적인 폴더링 외 가급적 기능(`Feature`) 기반으로 그룹화합니다.

### SwiftUI
```
AppName/
├── Apps/     // App파일, ContentView(최상단 View), 기타 환경설정 파일들
│   ├── AppNameApp.swift
│   ├── ContentView.swift
│   ├── info.plist
│   └── secrets.swift
│
├── Features/ 기능(Feature) 기반으로 그룹화
│   ├── Login/
│   ├── Home/
│   └── Profile/
│
├── Managers/       // 싱글톤 매니저 (AuthManager, CacheManager)
│
├── Extensions/     // Swift 기본 타입 확장 (커스텀 타입은 해당 타입 폴더에 위치)
│   ├── String+Extensions.swift
│   └── UIColor+Extensions.swift
│
├── Utils/
│   └── Constants.swift
│
└── Resources/
    ├── Images.xcassets
    ├── Icons.xcassets
    └── Font/
        ├── Pretendard-Bold.otf
        └── Pretendard-SemiBold.otf
```

## 2. 네이밍 컨벤션

기본적으로 `Swift API Design Guidelines`를 최대한 따릅니다.

-   **타입 (Class, Struct, Enum, Protocol):** `UpperCamelCase`
    -   `LoginView`, `UserData`
-   **메서드, 함수, 변수, 상수:** `lowerCamelCase`
    -   `func fetchUserData()`, `var userName: String`
-   **파일 이름:** 파일 내 주요 타입의 이름과 일치시킵니다.
    -   `LoginView.swift`

## 3. 코딩 스타일

-   **들여쓰기:** 4 스페이스
-   **`let`:** 변경되지 않는 모든 변수는 `let`으로 선언합니다.
-   **강제 언래핑 (`!`), 강제 캐스팅 (`as!`)** 사용을 지양합니다. `guard let`, `if let`을 사용하세요.
-   **접근 제어:**
    -   `private`, `fileprivate`를 사용하여 접근 범위를 명확히 합니다.
    -   라이브러리 개발이 아닌 경우 'internal'은 생략합니다.
-   **타입 추론:** 변수를 선언할 때 가급적 타입을 명시합니다.
-   **섹션 구분(MARK):**
    - `// MARK: -`를 사용하여 코드 흐름을 논리적으로 구분합니다.
    - `MARK` 주석 사이에는 **위로 두 줄**, **아래로 한 줄**을 띄워 시각적 구분을 명확히 합니다.
  
    예시:

    ```swift

    
    // MARK: - First Step

    private func firstStep() {
        ...    
    }

    
    // MARK: - Second Step

    private func secondStep() {
        ...
    }

    
    // MARK: - Third Step

    private func thirdStep() {
        ...
    }

    ```


## 4. Git & 버전 관리

-   **브랜치 전략:** **Git Flow**를 따릅니다.
    -   `main` (or `master`): 최종 릴리즈된 프로덕션 코드
    -   `develop`: 다음 릴리즈를 위한 개발 브랜치
    -   `feature/{feature-name}`: 기능 개발
    -   `release/{version}`: 릴리즈 준비
    -   `hotfix/{issue-name}`: 긴급 버그 수정
-   **커밋 메시지:** Conventional Commits 규칙을 따릅니다.
    -   `Type: Subject` (e.g., `feat: 로그인 화면 UI 구현`)
    -   **Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore` 등

## 5. 문서화

-   **Swift Documentation Comments (`///`)** 를 사용하여 주요 public API와 복잡한 로직에 대한 설명을 추가합니다.

## 6. 세부 규칙
### **6-1. 함수의 파라미터 레이블 사용 규칙:**
#### 1) 파라미터가 1개일 때
- **명확한 의미 전달이 필요 없다면 레이블을 생략합니다.**
```swift
func update(_ data: UserData)
update(userData)
```

#### 2) 파라미터가 2개 이상일 때
- **각 파라미터에 이름을 붙여 명확하게 전달합니다.**
```swift
func login(id: String, password: String)
login(id: "1234", password: "5678")

func move(from source: IndexPath, to destination: IndexPath)
move(from: a, to: b)
```

#### 3) 전치사 사용
- **의미를 보완할 수 있다면 전치사를 사용합니다.**
```swift
func showToast(at position: CGPoint)
showToast(at: .bottom)

func sendEmail(to address: String)
sendEmail(to: "test@example.com")
```
