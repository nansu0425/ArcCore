# 📁 프로젝트 디렉터리 구조

이 문서는 `ArcCore` 프로젝트의 전체 디렉터리 구조와 각 폴더 및 파일의 역할을 설명합니다. 프로젝트를 이해하고 탐색하는 데 도움이 되기를 바랍니다.

---

## 📚 프로젝트 최상위 구조

```
ArcCore/
├── Documentation/
├── GameServer/
├── UnityClient/
├── .editorconfig
├── .gitignore
├── LICENSE
└── README.md
```

**최상위 디렉터리 및 파일 설명:**

* **`Documentation/`**: 프로젝트의 상세 설계, 빌드 및 실행 방법, 문제 해결 기록 등 개발 과정 전반에 걸친 문서들을 모아둔 폴더입니다.
* **`GameServer/`**: C++ 기반의 게임 서버 솔루션과 관련된 모든 소스코드, 프로젝트 파일, 리소스 등이 포함된 핵심 폴더입니다.
* **`UnityClient/`**: 서버와 연동되는 Unity 기반의 게임 클라이언트 프로젝트 폴더입니다.
* **`.editorconfig`**: 다양한 코드 에디터/IDE에서 일관된 코딩 스타일(들여쓰기, 인코딩 등)을 유지하기 위한 설정 파일입니다.
* **`.gitignore`**: Git 버전 관리 시스템에서 추적하지 않을 파일 및 폴더를 지정합니다. 빌드 부산물, 임시 파일, 개인 설정 파일 등이 포함됩니다.
* **`LICENSE`**: 프로젝트의 오픈소스 라이선스 정보입니다.
* **`README.md`**: 프로젝트의 개요, 핵심 기술 스택, 주요 기능, 시연 영상 및 연락처 등 프로젝트에 대한 전반적인 소개를 담고 있는 문서입니다.

---

## 📁 `Documentation/` 상세 구조

```
Documentation/
├── Project_Directory.md
├── Architecture_Design.md
├── Database_Schema.md
├── Packet_Protocol.md
├── TroubleShooting_Log.md
├── Test_Strategy.md
├── BuildInstructions.md
└── Requirements_Specification.md
```

**`Documentation/` 폴더 내 문서 설명:**

* **`Project_Directory.md`**: 현재 이 문서입니다. `ArcCore` 프로젝트의 전체적인 디렉터리 구조를 설명합니다.
* **`Architecture_Design.md`**: `ArcCore` 서버의 전체적인 아키텍처 설계, 컴포넌트 간의 관계, 스레드 모델, 데이터 흐름 등에 대한 상세한 설명과 다이어그램을 포함합니다.
* **`Database_Schema.md`**: MySQL 데이터베이스의 스키마 정의, 테이블 구조, 관계형 다이어그램(ERD) 등 데이터베이스 설계에 대한 정보를 제공합니다.
* **`Packet_Protocol.md`**: Google Protobuf를 사용하여 정의된 패킷 구조, 각 패킷의 용도 및 데이터 형식에 대한 상세 설명을 담고 있습니다.
* **`TroubleShooting_Log.md`**: 프로젝트 개발 과정에서 발생했던 주요 기술적 문제들(예: 데드락, 메모리 누수, 성능 병목 등)과 이를 분석하고 해결했던 과정, 그리고 배운 점들을 상세히 기록한 문서입니다.
* **`Test_Strategy.md`**: 단위 테스트, 통합 테스트, 부하 테스트 등 `ArcCore` 프로젝트의 테스트 전략과 수행 결과, 사용된 테스트 도구에 대한 정보를 설명합니다.
* **`BuildInstructions.md`**: `ArcCore` 서버 및 클라이언트 프로젝트를 빌드하고 실행하기 위한 상세한 단계별 지침과 필요한 개발 환경 설정 방법을 안내합니다.
* **`Requirements_Specification.md`**: `ArcCore` 프로젝트의 요구 사항 명세서를 담은 문서로, 기능 요구 사항, 성능 요구 사항 및 시스템 제약 사항 등을 정의합니다.

---

## ⚙️ `GameServer/` 상세 구조

```
GameServer/
├── GameServer.sln
├── Common/
├── Network/
├── PacketProtocol/
├── GameDB/
├── GameLogic/
├── MainServer/
├── DummyClient/
├── Test/
├── Resource/
└── vcpkg.json
```

**`GameServer/` 폴더 내 프로젝트 및 리소스 설명:**

* **`GameServer.sln`**: Visual Studio IDE에서 `ArcCore` 서버 프로젝트들을 관리하고 빌드하기 위한 솔루션 파일입니다.
* **`Common/`**: (Static Library Project) - 서버의 모든 모듈에서 재사용되는 공통 유틸리티 클래스, 스레드 안전한 자료구조(메모리 풀, 오브젝트 풀, LockQueue, Logger 등), 전역 상수 및 매크로 등을 포함하는 기반 라이브러리입니다.
* **`Network/`**: (Static Library Project) - IOCP 기반의 고성능 비동기 네트워크 통신을 전담하는 모듈입니다. 클라이언트 세션 관리, 리스너, 데이터 송수신 버퍼링, 패킷 조립/분해 등의 기능을 구현합니다.
* **`PacketProtocol/`**: (Static Library Project) - Google Protobuf를 사용하여 정의된 `.proto` 파일들과 이를 통해 자동으로 생성된 C++ 패킷 클래스, 그리고 패킷을 효율적으로 처리하기 위한 핸들러 인터페이스 등을 관리합니다.
* **`GameDB/`**: (Static Library Project) - MySQL 데이터베이스와의 연동을 담당하는 모듈입니다. DB 커넥션 풀, 비동기 쿼리 처리, 데이터 매니저 등 게임 데이터의 영속성을 관리하는 로직을 추상화합니다.
* **`GameLogic/`**: (Static Library Project) - `ArcCore` 서버의 핵심 게임 규칙과 상태 변화를 처리하는 모듈입니다. 플레이어 관리, 월드/오브젝트 관리, 스킬 시스템, 인벤토리, NPC 상호작용 등 순수 게임 로직이 여기에 구현됩니다.
* **`MainServer/`**: (Executable Project) - 위에 언급된 모든 정적 라이브러리들을 링크하여 최종적으로 게임 서버를 구동하는 실행 파일 프로젝트입니다. 서버의 진입점(main 함수)과 전역적인 초기화/종료 로직을 포함합니다.
* **`DummyClient/`**: (Executable Project) - `MainServer`의 기능 테스트, 안정성 테스트, 그리고 동시 접속자 환경에서의 부하 테스트를 수행하기 위해 개발된 독립적인 C++ 더미 클라이언트입니다.
* **`Test/`**: (Executable Project) - Google Test 프레임워크를 사용하여 `Common`, `PacketProtocol`, `GameDB` 등 서버의 개별 모듈 및 핵심 기능들의 정확성을 검증하는 단위 테스트 코드를 포함합니다.
* **`Resource/`**: 서버 운영에 필요한 각종 설정 파일(예: DB 접속 정보, 서버 포트 등), 데이터 테이블(예: 아이템 정보, 몬스터 스탯 등) 등을 저장하는 폴더입니다.
* **`vcpkg.json`**: Microsoft Vcpkg 패키지 관리자를 사용하여 프로젝트가 의존하는 외부 라이브러리들(예: spdlog, Protobuf, MySQL Connector 등)의 목록과 버전을 정의하는 파일입니다.

---