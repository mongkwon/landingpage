```mermaid

flowchart TD

%% ========================
%% 노드 정의 (A와 B가 최상단에 오도록 구조 고정)
%% ========================

A([시작])
A --> B[[팀 평균 거리 & 팀 중심 이동 거리 계산]]

%% 메인 루프
B --> C{근접 && 이동 중인가?}

C -->|예| D[싱크 +1]
C -->|아니오| E[싱크 변화 없음]

D --> F{싱크 = 10?}
E --> F

F -->|예| G[싱크 초기화<br/>하모닉스 아이템 지급]
F -->|아니오| B

G --> H{인벤토리에<br/>아이템 존재?}

H -->|아니오| I[1단계 아이템 생성]
H -->|예| J{현재 단계 < 3?}

J -->|예| K[아이템 단계 +1]
J -->|아니오| L[추가 아이템 폐기]

I --> M[[단계별 이동 속도 & 지속시간 적용]]
K --> M
L --> M

M --> N{플레이어 사망?}

N -->|예| O[아이템 삭제<br/>인벤토리 비우기]
N -->|아니오| B

O --> B


%% ========================
%% 스타일 정의
%% ========================

%% 시작 & 거리 계산 노드 (최상단 강조)
style A fill:#ffe599,stroke:#d6b656,stroke-width:2px
style B fill:#fff2cc,stroke:#d6b656,stroke-width:2px

%% 조건 노드 스타일 (다이아몬드)
style C fill:#e1f0ff,stroke:#6fa8dc,stroke-width:2px
style F fill:#e1f0ff,stroke:#6fa8dc,stroke-width:2px
style H fill:#e1f0ff,stroke:#6fa8dc,stroke-width:2px
style J fill:#e1f0ff,stroke:#6fa8dc,stroke-width:2px
style N fill:#f4cccc,stroke:#cc0000,stroke-width:2px

%% 아이템 생성 & 강화 노드
style I fill:#d9ead3,stroke:#38761d,stroke-width:2px
style K fill:#d9ead3,stroke:#38761d,stroke-width:2px
style L fill:#fce5cd,stroke:#e69138,stroke-width:2px
style G fill:#d9ead3,stroke:#38761d,stroke-width:2px
style M fill:#d0e0e3,stroke:#6fa8dc,stroke-width:2px

%% 사망 처리 노드
style O fill:#f4cccc,stroke:#cc0000,stroke-width:2px
