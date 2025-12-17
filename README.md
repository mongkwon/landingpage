```mermaid

flowchart TD
  %% 시작 / 종료
  S([퀘스트 시작])
  END([퀘스트 완료])
  FAIL([퀘스트 실패])

  %% 처리 노드
  A[수문 제어실 진입]
  B[퀘스트 제한 시간 3분 시작]
  C[수문 제어 장치 상호작용 가능]
  D[협동으로 전자석 출력 레버 조작]
  E[수문 완전 개방]

  %% 시스템 메시지 (사다리꼴)
  M1[/시스템 메시지: 수문 제어실 진입/]
  M2[/시스템 메시지: 경고 수위 도달까지 남은 시간 03:00/]
  M3[/시스템 메시지: 알파는 커멘더 무전기를 얻었다/]

  %% 조건
  J{3분 이내에 개방했는가?}

  %% 흐름
  S --> A
  A --> M1 --> M2
  M2 --> B --> C --> D --> E
  E --> J

  J -->|Yes| M3 --> END
  J -->|No| FAIL

  %% 스타일 정의
  classDef process fill:#E3F2FD,stroke:#1565C0,color:#000;
  classDef system fill:#E8F5E9,stroke:#2E7D32,color:#000;
  classDef decision fill:#FFF3E0,stroke:#EF6C00,color:#000;
  classDef startend fill:#F3E5F5,stroke:#6A1B9A,color:#000;

  %% 스타일 적용
  class A,B,C,D,E process;
  class M1,M2,M3 system;
  class J decision;
  class S,END,FAIL startend;
