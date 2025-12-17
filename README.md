```mermaid

flowchart TD

%% ========================
%% 노드 정의
%% ========================

A([시작])
A --> B[수문 제어실 진입]

%% 시스템 메시지 (사다리꼴)
B --> M1[/수문 제어실 진입/]
M1 --> M2[/경고 수위 도달까지 남은 시간 03:00/]

%% 시스템 규칙 적용
M2 --> T[[퀘스트 제한 시간 3분 시작]]

%% 일반 처리 흐름
T --> C[수문 제어 장치 상호작용 가능]
C --> D[협동으로 전자석 출력 레버 조작]
D --> E[수문 완전 개방]

%% 조건 판정
E --> F{3분 이내에 개방했는가?}

%% 성공 처리
F -->|예| R[/알파는 커멘더 무전기를 얻었다/]
R --> G[퀘스트 목표 소거]
G --> H([퀘스트 종료])

%% 실패 처리
F -->|아니오| I([퀘스트 실패])


%% ========================
%% 스타일 정의
%% ========================

%% 시작 / 종료
style A fill:#ffe599,stroke:#d6b656,stroke-width:2px
style H fill:#d9ead3,stroke:#38761d,stroke-width:2px
style I fill:#f4cccc,stroke:#cc0000,stroke-width:2px

%% 일반 처리 노드
style B fill:#fff2cc,stroke:#d6b656,stroke-width:2px
style C fill:#d0e0e3,stroke:#6fa8dc,stroke-width:2px
style D fill:#d0e0e3,stroke:#6fa8dc,stroke-width:2px
style E fill:#d0e0e3,stroke:#6fa8dc,stroke-width:2px
style G fill:#d9ead3,stroke:#38761d,stroke-width:2px

%% 조건 노드
style F fill:#e1f0ff,stroke:#6fa8dc,stroke-width:2px

%% 시스템 메시지 (사다리꼴)
style M1 fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
style M2 fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
style R  fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px

%% 시스템 규칙 적용
style T fill:#fff2cc,stroke:#e69138,stroke-width:2px
style T  fill:#fff2cc,stroke:#e69138,stroke-width:2px
style R  fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px
