# WYE (Where You @) - 유즈케이스 다이어그램

## 전체 유즈케이스 다이어그램

```mermaid
graph TB
    subgraph Actors
        User([회원 사용자])
        ExternalUser([외부 사용자<br/>비회원])
    end
    
    subgraph "인증 및 프로필"
        Login[카카오 로그인]
        Logout[로그아웃]
        ProfileEdit[프로필 수정]
        ProfileView[프로필 보기]
    end
    
    subgraph "친구 및 크루 관리"
        FriendAdd[친구 추가]
        FriendView[친구 목록 보기]
        FriendEdit[친구 정보 수정]
        FriendDelete[친구 삭제]
        CrewCreate[크루 생성]
        CrewView[크루 목록 보기]
        CrewEdit[크루 수정]
        CrewDelete[크루 삭제]
    end
    
    subgraph "약속 관리"
        MeetupCreate[약속 만들기]
        MeetupView[약속 목록 보기]
        MeetupDetail[약속 상세 보기]
        MeetupEdit[약속 수정]
        MeetupDelete[약속 삭제]
        MeetupSort[약속 정렬<br/>생성순/가까운순]
        PastMeetupToggle[지난 약속<br/>보기/숨기기]
        MeetupShare[약속 공유<br/>외부 사용자 초대]
    end
    
    subgraph "참여자 관리"
        ParticipantAdd[참여자 추가]
        ParticipantLocation[출발지 설정]
        ParticipantTransport[교통수단 선택<br/>자동차/대중교통]
        ParticipantEdit[참여자 정보 수정]
        ParticipantDelete[참여자 삭제]
    end
    
    subgraph "장소 추천 및 선택"
        FairPlaceRecommend[공평 거리<br/>장소 추천]
        PlaceSearch[장소 검색<br/>카카오 플레이스]
        PlaceSelect[장소 선택]
        PlaceConfirm[장소 확정]
        DistanceView[참여자별<br/>거리/시간 보기]
    end
    
    subgraph "지도 및 경로"
        MapView[지도 보기]
        RouteDisplay[경로 표시<br/>자동차/대중교통]
        PlaceMarker[약속 장소 마커]
        ParticipantMarker[참여자 출발지 마커]
    end
    
    subgraph "실시간 위치 공유"
        LocationShareStart[위치 공유 시작<br/>약속 1시간 전]
        LocationShareStop[위치 공유 중단]
        RealtimeMapView[실시간 위치<br/>지도 보기]
        OthersLocationView[다른 참여자<br/>위치 확인]
    end
    
    subgraph "길찾기"
        Navigation[카카오맵 길찾기]
        RouteToPlace[출발지→약속장소<br/>경로 안내]
    end
    
    subgraph "알림"
        NotificationView[알림 목록 보기]
        NotificationRead[알림 읽음 처리]
        InviteNotification[약속 초대 알림]
        UpdateNotification[약속 수정 알림]
        LateNotification[지각 알림]
    end
    
    subgraph "준비물 관리"
        ItemAdd[준비물 추가]
        ItemView[준비물 목록 보기]
        ItemDelete[준비물 삭제]
    end
    
    subgraph "외부 사용자 기능"
        ShareLinkAccess[공유 링크 접속]
        ExternalInfo[이름/출발지/<br/>교통수단 입력]
        ExternalMeetupView[약속 정보 확인]
    end
    
    %% 회원 사용자 연결
    User --> Login
    User --> Logout
    User --> ProfileEdit
    User --> ProfileView
    
    User --> FriendAdd
    User --> FriendView
    User --> FriendEdit
    User --> FriendDelete
    
    User --> CrewCreate
    User --> CrewView
    User --> CrewEdit
    User --> CrewDelete
    
    User --> MeetupCreate
    User --> MeetupView
    User --> MeetupDetail
    User --> MeetupEdit
    User --> MeetupDelete
    User --> MeetupSort
    User --> PastMeetupToggle
    User --> MeetupShare
    
    User --> ParticipantAdd
    User --> ParticipantLocation
    User --> ParticipantTransport
    User --> ParticipantEdit
    User --> ParticipantDelete
    
    User --> FairPlaceRecommend
    User --> PlaceSearch
    User --> PlaceSelect
    User --> PlaceConfirm
    User --> DistanceView
    
    User --> MapView
    User --> RouteDisplay
    User --> PlaceMarker
    User --> ParticipantMarker
    
    User --> LocationShareStart
    User --> LocationShareStop
    User --> RealtimeMapView
    User --> OthersLocationView
    
    User --> Navigation
    User --> RouteToPlace
    
    User --> NotificationView
    User --> NotificationRead
    User --> InviteNotification
    User --> UpdateNotification
    User --> LateNotification
    
    User --> ItemAdd
    User --> ItemView
    User --> ItemDelete
    
    %% 외부 사용자 연결
    ExternalUser --> ShareLinkAccess
    ExternalUser --> ExternalInfo
    ExternalUser --> ExternalMeetupView
    
    %% Include 관계
    MeetupCreate -.->|include| ParticipantAdd
    MeetupCreate -.->|include| ParticipantLocation
    MeetupCreate -.->|include| ParticipantTransport
    
    MeetupEdit -.->|include| ParticipantEdit
    MeetupEdit -.->|include| ParticipantDelete
    
    FairPlaceRecommend -.->|include| PlaceSearch
    PlaceConfirm -.->|include| PlaceSelect
    
    RouteDisplay -.->|include| MapView
    RealtimeMapView -.->|include| MapView
    
    Navigation -.->|include| RouteToPlace
    
    %% Extend 관계
    MeetupDetail ..->|extend| FairPlaceRecommend
    MeetupDetail ..->|extend| MapView
    MeetupDetail ..->|extend| RouteDisplay
    MeetupDetail ..->|extend| LocationShareStart
    MeetupDetail ..->|extend| Navigation
    MeetupDetail ..->|extend| ItemAdd
    
    ParticipantAdd ..->|extend| FriendView
    ParticipantAdd ..->|extend| CrewView
    
    style User fill:#e1f5ff
    style ExternalUser fill:#fff4e6
    style Login fill:#d4edda
    style MeetupCreate fill:#fff3cd
    style FairPlaceRecommend fill:#f8d7da
    style LocationShareStart fill:#d1ecf1
    style Navigation fill:#e2e3e5
```

## 주요 유즈케이스 흐름

### 1. 회원 가입 및 로그인
```mermaid
graph LR
    A[사용자] --> B[카카오 로그인]
    B --> C{첫 로그인?}
    C -->|Yes| D[프로필 생성]
    C -->|No| E[기존 프로필 로드]
    D --> F[홈 화면]
    E --> F
```

### 2. 약속 생성 흐름
```mermaid
graph LR
    A[약속 만들기] --> B[기본 정보 입력<br/>제목/날짜/시간/목적]
    B --> C[참여자 추가]
    C --> D[친구/크루에서 선택]
    D --> E[출발지 설정]
    E --> F[교통수단 선택<br/>자동차/대중교통]
    F --> G{준비물 추가?}
    G -->|Yes| H[준비물 입력]
    G -->|No| I[약속 생성 완료]
    H --> I
    I --> J[참여자에게 알림 발송]
```

### 3. 공평 거리 장소 추천 흐름
```mermaid
graph LR
    A[장소 추천 시작] --> B[Geometric Median<br/>계산]
    B --> C[중심점 기준<br/>장소 검색]
    C --> D[각 장소별<br/>거리 편차 계산]
    D --> E[공평도 순 정렬]
    E --> F[장소 목록 표시]
    F --> G[사용자 장소 선택]
    G --> H[참여자별<br/>거리/시간 표시]
    H --> I[장소 확정]
```

### 4. 실시간 위치 공유 흐름
```mermaid
graph LR
    A[약속 1시간 전] --> B{위치 공유 가능}
    B --> C[위치 공유 시작]
    C --> D[GPS 위치 획득]
    D --> E[10초마다 업데이트]
    E --> F[서버에 저장]
    F --> G[다른 참여자에게<br/>실시간 표시]
    G --> H{약속 종료 or<br/>공유 중단?}
    H -->|No| E
    H -->|Yes| I[위치 공유 종료]
```

### 5. 길찾기 흐름
```mermaid
graph LR
    A[약속 상세] --> B[참여자 선택]
    B --> C{출발지 정보}
    C -->|실시간 위치| D[현재 좌표 사용]
    C -->|저장된 주소| E[주소→좌표 변환]
    E --> F{변환 성공?}
    F -->|주소 검색 성공| G[좌표 획득]
    F -->|주소 검색 실패| H[키워드 검색]
    H --> G
    D --> G
    G --> I[카카오맵 URL 생성<br/>출발지+도착지+교통수단]
    I --> J[카카오맵 앱/웹 열기]
```

### 6. 외부 사용자 참여 흐름
```mermaid
graph LR
    A[약속 주최자] --> B[공유 링크 생성]
    B --> C[외부 사용자에게 전달]
    C --> D[외부 사용자<br/>링크 접속]
    D --> E[이름 입력]
    E --> F[출발지 설정]
    F --> G[교통수단 선택]
    G --> H[약속 정보 확인]
    H --> I[참여자로 추가]
    I --> J[약속 상세 보기]
```

## 액터별 주요 기능 정리

### 회원 사용자
- **계정 관리**: 로그인, 로그아웃, 프로필 수정
- **관계 관리**: 친구 추가/수정/삭제, 크루 생성/수정/삭제
- **약속 관리**: 생성, 수정, 삭제, 정렬, 공유
- **장소 선택**: 공평 거리 추천, 검색, 선택, 확정
- **실시간 기능**: 위치 공유, 실시간 지도, 길찾기
- **알림**: 초대, 수정, 지각 알림 수신
- **준비물**: 추가, 보기, 삭제

### 외부 사용자 (비회원)
- **참여**: 공유 링크로 약속 접속
- **정보 입력**: 이름, 출발지, 교통수단
- **조회**: 약속 정보 확인

## 시스템 경계

### 내부 시스템
- WYE 웹 애플리케이션
- Supabase KV 저장소
- Supabase Edge Functions

### 외부 시스템
- Kakao API (로그인, 지도, 장소 검색, Geocoding)
- Kakao Mobility API (자동차 경로)
- ODsay API (대중교통 경로)
- Browser Geolocation API (위치 정보)

## 비기능적 요구사항

### 성능
- 위치 공유: 10초마다 업데이트
- 토큰 갱신: 만료 5분 전 자동 갱신
- 지도 로딩: 3초 이내

### 보안
- 카카오 OAuth 2.0 인증
- Access Token + Refresh Token 관리
- 위치 정보는 약속 1시간 전부터만 공유

### 사용성
- 모바일 최적화 UI
- 실시간 알림
- 직관적인 장소 추천

### 호환성
- 웹 브라우저 (Chrome, Safari, Edge)
- 카카오맵 앱 연동
- GPS 지원 디바이스
