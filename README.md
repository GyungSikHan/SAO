# SAO_Demo
가능해! 오히려 언리얼로 간단한 게임을 만들고 AI 기능을 붙이는 것은 포트폴리오로도 꽤 좋아.

다만 “AI”가 무엇을 의미하느냐에 따라 난이도가 달라져.

1. 게임 적 AI
가장 쉽게 구현 가능해.

예를 들면:

플레이어 발견

플레이어 추적

일정 거리에서 공격

체력이 낮으면 도망

순찰하다가 소리를 들으면 확인

언리얼에서는 보통 다음 기능을 사용해.

Behavior Tree

Blackboard

AI Controller

AI Perception

EQS

NavMesh

너는 이미 Behavior Tree, EQS, Perception을 다뤄봤으니까 이 방향은 충분히 가능해.

2. 생성형 AI NPC 대화
NPC에게 ChatGPT 같은 AI를 붙이는 방식이야.

예를 들면 플레이어가 NPC에게 말을 걸면:

플레이어: 이 근처에 위험한 곳이 있어?
NPC: 북쪽 폐허에는 최근 몬스터가 나타났다고 들었네.

이런 식으로 정해진 대사가 아니라 AI가 답변하도록 만들 수 있어.

구조는 대략:

Unreal Engine
    ↓ 플레이어 입력
C++ 또는 Blueprint
    ↓ HTTP 요청
AI API 서버
    ↓ 답변
Unreal UI에 NPC 대사 출력
보통 언리얼의 FHttpModule을 이용해서 AI API를 호출해.

단, API 키를 게임 클라이언트에 직접 넣으면 유출될 수 있으므로 실제 배포에서는 중간 서버를 두는 게 안전해.

3. AI가 플레이 방식에 반응하는 게임
조금 더 게임다운 방식이야.

예를 들면:

플레이어가 원거리 공격을 자주 사용하면 적이 방패를 듦

회피를 자주 하면 적이 지연 공격을 사용

특정 스킬을 반복하면 카운터 패턴을 선택

플레이 스타일을 분석해 적 난이도를 조절

처음에는 머신러닝까지 갈 필요 없이, 플레이어 행동을 기록한 뒤 점수 기반으로 패턴을 선택하면 돼.

if (PlayerData.RangedAttackCount > 10)
{
    Enemy->UseAntiRangedPattern();
}
이것도 충분히 “적응형 AI”로 설명할 수 있어.

가장 현실적인 간단한 프로젝트
내가 추천하는 건 AI NPC가 있는 작은 던전 게임이야.

게임 흐름:

NPC와 대화

AI NPC가 랜덤 또는 상황에 맞는 퀘스트 제공

던전에 입장

Behavior Tree 기반 적과 전투

전투 결과에 따라 NPC 대사가 달라짐

여기에 들어가는 AI는 두 종류야.

전투 AI: Behavior Tree, EQS, Perception

대화 AI: 생성형 AI API

이렇게 만들면 단순히 “챗봇을 붙였다”가 아니라, 게임 시스템과 AI를 연동했다고 보여줄 수 있어.

처음 만들 때는 아래 정도로 범위를 줄이는 게 좋아.

작은 맵 1개

NPC 1명

적 1종

퀘스트 2~3종

대화 UI

플레이어 상태를 반영하는 NPC 답변

너의 기존 언리얼 프로젝트 경험을 기준으로 보면, 전투 부분은 이미 상당 부분 구현 경험이 있어서 NPC 대화 AI를 추가하는 형태가 가장 현실적이고 결과물도 눈에 띌 거야.


친구가 AI 부트캠프를 진행하고, 끝나서 같이 사이드 프로젝트 해보자는데 게임에 어떤식으로 넣을 수 있는지 모르겠어

visual studio로도 파이선 개발 가능?


응, Visual Studio로 파이썬 개발 가능해!
다만 Visual Studio Code와 Visual Studio는 서로 다른 프로그램이야.

Visual Studio에서 개발하는 방법
Visual Studio Installer를 실행하고:

수정 선택

워크로드에서 Python 개발 체크

설치 완료

Visual Studio에서 새 프로젝트 만들기

Python Application 또는 Python 검색

이렇게 하면 파이썬 프로젝트를 만들 수 있어.

파이썬 자체도 별도로 설치해야 할 수 있고, Visual Studio에서 설치된 Python 인터프리터나 가상환경을 선택해서 사용할 수 있어.

친구와 AI 프로젝트를 한다면
친구가 Python으로 다음을 만들 수 있어.

FastAPI 서버
AI 모델 실행
데이터 분석
생성형 AI API 호출
데이터베이스 연동
예를 들어 FastAPI 서버 코드는 이런 식이야.

from fastapi import FastAPI

app = FastAPI()

@app.post("/analyze")
def analyze_player(data: dict):
    attack_count = data.get("attack_count", 0)
    dodge_count = data.get("dodge_count", 0)

    if dodge_count > attack_count:
        player_type = "defensive"
    else:
        player_type = "aggressive"

    return {
        "player_type": player_type,
        "recommended_pattern": "rush_attack"
    }
언리얼에서 이 서버로 HTTP 요청을 보내면 돼.

언리얼 C++
    ↓ JSON 전송
Python FastAPI
    ↓ AI 분석
JSON 결과 반환
    ↓
언리얼 보스 패턴 변경
Visual Studio와 VS Code 중 추천
친구가 파이썬과 웹·AI 개발을 한다면 보통은 VS Code가 더 가볍고 편해.

프로그램	적합한 용도
Visual Studio	언리얼 C++, C#, 대규모 프로젝트
VS Code	Python, FastAPI, 웹, AI 서버
PyCharm	Python 전문 개발
그래서 둘이 프로젝트를 한다면 보통:

너: Visual Studio + Unreal Engine C++
친구: VS Code + Python + FastAPI
이 구성이 가장 편해. 같은 개발 도구를 쓸 필요는 없고, 언리얼과 Python 서버가 HTTP와 JSON으로 통신하면 돼.

그리고 앞 질문인 RPG와 액션 RPG의 차이는 전투 조작 방식이 가장 커.

일반 RPG: 캐릭터 능력치, 장비, 성장, 선택 등이 중심

액션 RPG: RPG 성장 요소에 실시간 회피·공격·방어·조준 같은 직접 조작을 강조

예: 턴제 명령을 고르는 게임은 RPG에 가깝고, 직접 공격하고 피하는 소울라이크는 액션 RPG에 가까움

너희가 언리얼로 캐릭터를 직접 움직이고 적과 실시간으로 싸우는 게임을 만든다면 보통 액션 RPG라고 부르는 게 맞아.


명령 프롬프트나 AI API같은거 관리는 어떻게 해야됨?? 게임에서

게임 안에서 명령 프롬프트를 직접 조작하는 방식은 보통 개발용이고, 실제 배포에서는 구조를 따로 잡는 게 좋아.

개발 중에는 이렇게 해
친구가 Python 서버를 만든다면 명령 프롬프트나 터미널에서 서버를 실행해.

uvicorn main:app --reload
그러면 Python 서버가 예를 들어 아래 주소에서 실행돼.

http://127.0.0.1:8000
언리얼은 여기에 HTTP 요청을 보내는 거야.

Unreal
  → http://127.0.0.1:8000/analyze
  → Python 서버
  → AI 분석
  → JSON 응답
개발할 때는 보통:

Python 서버 실행

Unreal 실행

Unreal에서 API 호출

로그 확인

이런 식으로 관리해.

게임 배포 때는 3가지 방식이 있어
1. 외부 서버 방식
가장 일반적이야.

게임
  ↓ 인터넷
클라우드 서버
  ↓
Python / FastAPI / AI 모델
장점:

API 키 숨길 수 있음

AI 모델 업데이트 가능

여러 사용자가 같은 서버 사용 가능

단점:

서버 비용 발생

인터넷 필요

서버가 꺼지면 기능도 안 됨

생성형 AI API를 쓸 거라면 거의 이 방식을 사용해야 해.

2. 로컬 Python 서버를 게임과 같이 실행
게임 실행 시 Python 서버도 같이 켜는 방식이야.

예를 들면 Unreal에서 별도 프로세스를 실행할 수 있어.

FPlatformProcess::CreateProc(
    TEXT("PythonServer.exe"),
    nullptr,
    true,
    false,
    false,
    nullptr,
    0,
    nullptr,
    nullptr
);
이때 Python 코드를 PyInstaller 같은 도구로 exe로 만들 수 있어.

pyinstaller --onefile main.py
결과:

Game.exe
PythonServer.exe
게임이 실행되면:

Game.exe 실행
  ↓
PythonServer.exe 자동 실행
  ↓
localhost API 통신
장점:

서버 비용 없음

인터넷 없이도 가능

싱글 게임에 적합

단점:

실행 파일 관리가 복잡함

백신이 오탐할 수 있음

사용자가 프로세스를 종료할 수 있음

모델 파일이 그대로 노출될 수 있음

3. Python 없이 게임 내부에서 직접 처리
AI가 단순 분류나 규칙 기반이라면 굳이 Python 서버가 필요 없을 수도 있어.

예를 들어 플레이어 스타일 분석 정도라면 Unreal C++에서 바로 처리 가능해.

if (RangedAttackCount > MeleeAttackCount)
{
    PlayerType = EPlayerType::Ranged;
}
else
{
    PlayerType = EPlayerType::Melee;
}
또는 학습된 모델을 ONNX로 변환해서 Unreal 내부에서 실행하는 방법도 있어. 다만 이건 처음 프로젝트에는 난이도가 조금 올라가.

AI API 키 관리는 특히 중요해
절대 게임 코드에 API 키를 직접 넣으면 안 돼.

이렇게 하면 위험해.

FString ApiKey = TEXT("sk-xxxx");
패키징된 게임 파일을 뜯으면 키를 찾을 수 있기 때문이야.

안전한 구조는:

게임
  ↓
너희 Python 서버
  ↓
OpenAI 또는 다른 AI API
API 키는 Python 서버의 환경 변수에 저장해.

set OPENAI_API_KEY=키값
Python에서는:

import os

api_key = os.getenv("OPENAI_API_KEY")
.env 파일을 쓸 수도 있어.

OPENAI_API_KEY=키값
그리고 .env는 Git에 올리면 안 돼.

.env
너희 프로젝트에 가장 현실적인 방식
너희가 2명이서 작은 싱글 게임을 만든다면 처음에는 이렇게 가는 게 좋아.

개발 중:
Unreal + 로컬 FastAPI 서버

시연할 때:
Unreal 실행 전에 Python 서버 실행

완성 후:
Python 서버를 exe로 패키징하거나
무료 클라우드 서버에 배포
처음부터 게임이 Python 서버를 자동 실행하게 만들 필요는 없어. 우선은 친구가 터미널에서 서버를 켜고, 네가 Unreal에서 HTTP 통신부터 성공시키는 게 제일 안전해.

핵심은 명령 프롬프트 자체를 게임에서 관리하는 게 아니라, Python 서버 프로세스와 API 연결 상태를 관리하는 것이야. 게임에서는 서버가 켜졌는지 확인하고, 요청 실패 시 오류 UI를 보여주면 돼.

AI 서버 연결 실패
AI 기능을 사용할 수 없습니다.
기본 게임 모드로 진행합니다.

아래 내용을 개발 기획서로 만들어줘

자 나는 경식이의 친구 이용진이라고 해. 내가 만들고 싶은건, 소드아트온라인에서 나왔던, 방대한 스토리가 근본이 되서 퀘스트, 스킬, NPC, 아이템 등이 AI 로 자동 생성되면서 엔딩을 보는 게임이야. 물론 작업일정으로 크게는 못하고 줄여야 하겠지만, 미리 정해둔 설정, 예를 들어 100층 보스를 깨면 된다던지, 같은 것들은 두고 해야 더 매력있겠지? 기본적으로 rpg이기도 하고. 제대로 정리는 안되었지만 어떤것 같아?

오, 이건 생각보다 굉장히 재밌는 아이디어야. 근데 'AI가 게임을 만든다'가 아니라 'AI가 세계를 운영한다'는 방향으로 접근하면 훨씬 현실적이고 완성도도 높아질 것 같아.

내가 딱 하나만 바꾸고 싶어.

모든 걸 AI가 생성한다 → AI는 세계관의 규칙 안에서 생성한다.

이 차이가 엄청 커.

내가 생각하는 핵심 컨셉

소드 아트 온라인처럼 "하나의 거대한 세계"가 존재한다.

하지만 개발자가 만드는 것은 세계 전체가 아니라 세계의 법칙(Rules) 이다.

예를 들어

세계관

- 세계수 신앙이 존재한다.
- 마왕은 100층에 있다.
- 인간/엘프/드워프만 존재한다.
- 불 마법은 얼음 지역에서 약해진다.
- 검술은 물리계 스킬이다.
- 희귀 아이템은 전설 NPC가 제작한다.

AI는 이 규칙을 절대 깨지 못한다.

대신

NPC
퀘스트
아이템
스킬
대사
사건

을 계속 만들어낸다.

그러면 플레이할 때마다 세계는 다르지만 설정은 유지된다.

예를 들어

100층을 목표로 한다.

1층에서는

마을 A

NPC
"약초를 구해줘."

가 있을 수도 있고,

다음 플레이에서는

같은 마을

NPC
"딸이 늑대에게 납치됐다."

가 나올 수도 있다.

하지만 둘 다

세계관
↓
지역
↓
현재 몬스터
↓
NPC 성격
↓
AI 생성

으로 만들어진다.

더 중요한 건 "기억"이라고 생각해.

예를 들어

플레이어가

상인을 죽였다.

그러면

AI는

상인의 아들이 복수를 맹세했다.

를 생성할 수도 있다.

10시간 뒤

그 아들이 용병단장이 되어 등장.

할 수도 있고.

즉

AI는 단순 생성이 아니라

세계의 역사를 이어가는 역할

을 한다.

이게 진짜 재밌어.

퀘스트도 연결되어야 한다.

요즘 AI 데모는 대부분

퀘스트 생성

A를 죽여라.

끝.

이다.

이건 금방 질린다.

대신

퀘스트1

광산이 위험하다.

↓

왜?

↓

고블린 등장.

↓

왜?

↓

고블린이 도망쳤다.

↓

왜?

↓

오우거 등장.

↓

왜?

↓

40층 보스가 영향.

이렇게 원인이 이어져야 한다.

그러면 AI가 만든 것 같지 않고

진짜 세계처럼 느껴진다.

NPC도 기억을 가져야 한다.

예를 들어

플레이어가

NPC를 세 번 도와줌.

그러면

신뢰도 증가

↓

새로운 상점 개방

↓

희귀 퀘스트 제공

↓

100층 공략 시 동료 등장

이런 식으로.

LLM이 가장 잘하는 게 관계와 맥락 유지라서 이 부분을 적극 활용하면 좋다.

그런데 현실적으로는...

여기서 가장 위험한 부분이 있어.

처음부터

"AI가 퀘스트, 스킬, NPC, 아이템, 맵, 던전, 밸런스까지 다 만든다."

이렇게 가면 거의 100% 중간에 멈춘다.

왜냐면 각각이 하나의 연구 주제 수준이거든.

내가 추천하는 MVP

처음 버전은 정말 작게 잡는 거야.

5층짜리 던전

↓

최종 보스 존재

↓

마을 1개

↓

NPC 5명

↓

AI가 생성하는 것

- 퀘스트
- NPC 대화
- 아이템 설명
- 일부 스킬

그리고

모든 생성물은 '세계 설정 데이터'를 참조하게 만든다.

이것만 해도 이미 굉장히 인상적인 프로젝트가 된다.

역할 분담도 자연스럽다.

이용진(AI)

세계관 지식베이스(RAG 또는 룰 기반)
퀘스트 생성
NPC 기억 관리
아이템/스킬 생성
생성 결과 검증(설정 위반 방지)

경식(언리얼)

전투
레벨
AI Controller
Behavior Tree
UI
저장 시스템
HTTP 연동
내가 가장 마음에 드는 한 문장

이 프로젝트를 소개할 때는 이렇게 표현하면 훨씬 강렬해.

"플레이어는 고정된 스토리를 소비하는 것이 아니라, AI가 세계의 규칙을 지키며 만들어가는 하나뿐인 역사를 경험한다."

이 문장이 프로젝트의 핵심을 잘 담고 있어.

마지막으로 하나 제안하고 싶은 게 있어. 100층을 처음부터 구현하지 말고, 100층이라는 목표는 '세계관'으로만 존재시키는 거야. 실제 데모는 3~5층만 구현해도 괜찮아. 중요한 건 "100층까지도 같은 원리로 확장될 수 있는 구조"를 보여주는 거지, 층 수를 모두 만드는 게 아니야.

이 방향이라면 단순히 "AI를 붙인 RPG"가 아니라, 'AI가 지속적으로 세계를 운영하는 RPG 엔진'이라는 색깔을 가진 프로젝트가 될 가능성이 충분히 있다고 생각해.

아래처럼 바로 문서에 붙여 넣을 수 있는 형태로 정리했어.

AI 세계 운영형 RPG 개발 기획서
1. 프로젝트 개요
프로젝트명
가칭 AI Tower RPG

장르
싱글 플레이 기반 액션 RPG

개발 형태
2인 사이드 프로젝트

개발 엔진 및 기술
게임 클라이언트: Unreal Engine

게임 로직: C++ / Blueprint

AI 서버: Python / FastAPI

생성형 AI: LLM API 또는 로컬 모델

데이터 저장: JSON, SQLite 또는 경량 데이터베이스

통신 방식: HTTP API / JSON

2. 프로젝트 핵심 소개
본 프로젝트는 고정된 스토리를 따라가는 일반적인 RPG가 아니라, 미리 정해진 세계관과 규칙을 바탕으로 AI가 퀘스트, NPC 대화, 사건, 아이템, 일부 스킬을 생성하며 세계의 역사를 이어가는 RPG를 목표로 한다.

플레이어는 고정된 콘텐츠를 반복해서 소비하는 것이 아니라, 자신의 행동에 따라 변화하는 하나뿐인 세계를 경험한다.

핵심 문장
플레이어는 고정된 스토리를 소비하는 것이 아니라, AI가 세계의 규칙을 지키며 만들어가는 하나뿐인 역사를 경험한다.

3. 프로젝트 목표
본 프로젝트의 최종 목표는 AI가 게임 콘텐츠를 무작위로 생성하는 것이 아니라, 세계관의 규칙과 이전 사건을 기억하면서 일관된 콘텐츠를 생성하도록 만드는 것이다.

개발자는 세계 전체를 직접 제작하지 않는다.

대신 다음 요소를 설계한다.

세계관

세계의 법칙

종족

지역

세력

주요 인물

최종 목표

생성 가능한 콘텐츠의 범위

전투와 성장 규칙

AI가 위반해서는 안 되는 제한 조건

AI는 해당 규칙 안에서 게임 세계를 지속적으로 운영한다.

4. 세계관 기본 설정
세계 구조
게임 세계는 여러 층으로 구성된 거대한 탑이다.

플레이어의 최종 목표는 탑을 공략하고 최상층의 보스를 처치하는 것이다.

전체 세계관에서는 100층까지 존재하는 것으로 설정하지만, 초기 개발 버전에서는 3층에서 5층만 구현한다.

100층이라는 목표는 세계의 규모와 확장성을 표현하기 위한 설정으로 사용한다.

기본 세계관 규칙 예시
세계는 총 100개의 층으로 구성되어 있다.

최종 보스는 100층에 존재한다.

인간, 엘프, 드워프 종족이 존재한다.

각 층은 독립된 지역과 생태계를 가진다.

세계수 신앙을 믿는 종교 세력이 존재한다.

검술은 물리 계열 스킬로 분류된다.

불 마법은 빙하 지역에서 효과가 감소한다.

전설 등급 아이템은 특정 장인 NPC만 제작할 수 있다.

상위층의 사건은 하위층에 영향을 줄 수 있다.

이미 사망한 NPC는 특별한 설정 없이 다시 등장할 수 없다.

플레이어의 행동은 NPC 관계와 지역 상태에 영향을 준다.

AI는 위와 같은 세계관 규칙을 반드시 따라야 한다.

5. 핵심 게임 콘셉트
5.1 AI가 세계를 운영하는 RPG
AI는 게임의 모든 요소를 자유롭게 생성하지 않는다.

AI는 개발자가 정의한 규칙과 현재 세계 상태를 참고하여 새로운 콘텐츠를 생성한다.

생성 대상은 다음과 같다.

NPC 대화

퀘스트

지역 사건

아이템 이름과 설명

일부 스킬 이름과 효과

NPC 관계 변화

후속 사건

퀘스트 보상

세계 기록

AI는 세계를 새롭게 만드는 역할이 아니라, 이미 존재하는 세계를 운영하고 변화시키는 역할을 맡는다.

5.2 플레이어 행동 기억
게임 세계는 플레이어의 주요 행동을 기록한다.

예시:

특정 NPC를 도와줌

NPC의 부탁을 거절함

상인을 공격함

마을을 위험에서 구함

특정 세력과 협력함

특정 몬스터를 반복적으로 처치함

중요한 아이템을 누구에게 전달함

기록된 행동은 이후 퀘스트, NPC 대화, 관계, 지역 사건에 영향을 준다.

예를 들어 플레이어가 상인을 죽였다면 다음과 같은 사건이 발생할 수 있다.

상인이 사망한다.

마을의 상점 기능이 제한된다.

상인의 가족이 플레이어를 증오한다.

상인의 아들이 복수를 결심한다.

시간이 지난 후 상인의 아들이 용병단장이 되어 등장한다.

해당 용병단이 플레이어를 추적하는 퀘스트가 생성된다.

이처럼 하나의 행동이 장기적인 사건으로 연결되도록 설계한다.

5.3 연속성을 가진 퀘스트
퀘스트는 단순한 반복 임무가 아니라 원인과 결과를 가지도록 한다.

단순 퀘스트 예시:

고블린 5마리 처치

약초 3개 수집

본 프로젝트의 퀘스트는 가능한 경우 세계의 다른 사건과 연결되어야 한다.

예시:

광산에서 몬스터가 나타난다.

조사 결과 고블린이 광산을 점령한 사실을 알게 된다.

고블린은 더 강한 몬스터를 피해 광산으로 도망친 상태다.

해당 몬스터는 상위층 보스의 영향으로 이동했다.

플레이어는 단순히 고블린을 처치할지, 원인을 조사할지 선택한다.

선택에 따라 새로운 사건과 보상이 생성된다.

퀘스트 생성 시 AI는 다음 정보를 참고한다.

현재 층

지역 상태

최근 사건

생존 NPC

NPC 성격

플레이어 평판

이전 퀘스트 결과

현재 등장 가능한 몬스터

상위층과 하위층의 관계

세계관 규칙

6. 주요 게임 시스템
6.1 전투 시스템
기본 전투는 실시간 액션 방식으로 구성한다.

주요 기능:

기본 공격

회피

방어

스킬 사용

체력과 자원 관리

적 AI

보스 패턴

아이템 획득

장비 착용

초기 버전에서는 전투 시스템을 단순화한다.

권장 범위:

무기 1종 또는 2종

기본 공격 콤보

회피

액티브 스킬 2개에서 4개

일반 몬스터 2종에서 3종

보스 1종

6.2 층 공략 시스템
각 층은 하나의 작은 지역으로 구성한다.

층마다 다음 요소를 가진다.

마을 또는 안전 구역

NPC

전투 지역

퀘스트

일반 몬스터

층 보스

다음 층으로 이동하는 조건

초기 데모에서는 총 3층에서 5층을 구현한다.

각 층을 클리어하면 다음 층이 개방되며, 이전 층의 사건과 NPC 관계는 유지된다.

6.3 NPC 시스템
NPC는 기본 설정과 기억 데이터를 가진다.

NPC 데이터 예시:

이름

종족

직업

성격

소속 세력

거주 지역

플레이어 신뢰도

플레이어 적대도

알고 있는 정보

숨기고 있는 정보

이전 대화 기록

주요 사건 기록

현재 상태

생존 여부

NPC 대사는 현재 상태와 기억을 바탕으로 AI가 생성한다.

플레이어가 NPC를 반복해서 도와주면 다음과 같은 변화가 발생할 수 있다.

신뢰도 증가

새로운 대화 개방

상점 할인

비밀 정보 제공

희귀 퀘스트 제공

동료 참여

보스전 지원

6.4 관계 및 평판 시스템
플레이어는 NPC 및 세력과 관계를 형성한다.

관계 수치는 다음과 같이 구성할 수 있다.

신뢰

호감

공포

적대

존경

초기 버전에서는 구현 난이도를 줄이기 위해 신뢰도와 적대도 두 가지 수치만 사용한다.

예시:

신뢰도 70 이상
→ 특별 퀘스트 개방

신뢰도 90 이상
→ 희귀 아이템 제공

적대도 50 이상
→ 거래 거부

적대도 80 이상
→ NPC 또는 용병이 플레이어 공격
AI는 관계 수치를 참고해 대사와 사건을 생성한다.

6.5 아이템 생성 시스템
AI는 세계관과 지역 정보를 바탕으로 아이템의 이름과 설명을 생성한다.

단, 실제 능력치와 등급은 게임 시스템이 결정한다.

AI 생성 대상:

아이템 이름

아이템 설명

제작자 또는 발견 경위

세계관 관련 배경

외형 키워드

게임 시스템 결정 대상:

공격력

방어력

등급

판매 가격

장착 조건

특수 효과 수치

드롭 확률

예시:

{
  "itemType": "Sword",
  "rarity": "Rare",
  "attackPower": 32,
  "effectType": "FireDamage",
  "effectValue": 5
}
AI는 위 데이터를 바탕으로 다음과 같은 텍스트를 생성한다.

잿빛 맹세

화산 지대의 대장장이가 멸망한 고향을 기억하며 제작한 검.
검신에 남은 불씨는 차가운 지역에서 빠르게 사라진다.
이 방식은 AI가 게임 밸런스를 직접 결정하는 문제를 방지한다.

6.6 스킬 생성 시스템
초기 버전에서는 AI가 완전히 새로운 전투 스킬을 직접 구현하지 않는다.

게임에는 미리 제작된 스킬 템플릿이 존재한다.

예시:

단일 대상 공격

범위 공격

돌진 공격

방어 강화

회복

지속 피해

이동 속도 증가

AI는 템플릿을 선택하고 이름, 설명, 속성, 연출 키워드를 생성한다.

예시:

{
  "template": "DashAttack",
  "damageType": "Physical",
  "element": "None",
  "power": 20,
  "cooldown": 8
}
AI 생성 결과:

스킬명: 바람을 가르는 일격

설명: 검을 낮게 내린 채 빠르게 돌진해 전방의 적을 베어낸다.
실제 이동, 공격 판정, 피해량 계산은 언리얼에서 미리 구현된 템플릿을 사용한다.

6.7 세계 기록 시스템
게임에서 발생한 주요 사건을 기록한다.

세계 기록 예시:

플레이어가 마을을 구함

특정 NPC 사망

보스 처치

세력 관계 변화

퀘스트 성공 또는 실패

중요 아이템 획득

지역 상태 변화

모든 대화 내용을 저장하는 대신, 중요한 사건을 요약하여 저장한다.

예시:

{
  "eventId": 142,
  "eventType": "NPCDeath",
  "target": "Merchant_Rodan",
  "cause": "KilledByPlayer",
  "location": "Floor1_Village",
  "result": "ShopClosed",
  "summary": "플레이어가 상인 로단을 공격해 사망시켰다."
}
AI는 새로운 퀘스트와 대사를 생성할 때 최근 기록과 중요 기록을 참고한다.

7. AI 생성 원칙
7.1 AI가 생성하는 요소
NPC 대사

퀘스트 제목과 설명

퀘스트 발생 이유

NPC의 감정 표현

아이템 이름과 설명

일부 스킬 이름과 설명

후속 사건

세계 기록 요약

플레이어 행동에 따른 반응

7.2 AI가 직접 결정하지 않는 요소
플레이어 피해량

몬스터 능력치

아이템 핵심 능력치

게임 경제

드롭 확률

보스 클리어 조건

맵 구조 전체

애니메이션

충돌 판정

저장 데이터 구조

게임 진행 필수 조건

게임의 핵심 규칙과 밸런스는 개발자가 관리한다.

7.3 생성 결과 검증
AI가 생성한 결과는 게임에 바로 적용하지 않는다.

다음 단계를 거쳐 검증한다.

세계관 데이터 전달

현재 게임 상태 전달

AI 콘텐츠 생성

JSON 형식 검증

필수 항목 확인

금지된 종족, 지역, 능력 확인

수치 범위 확인

문제가 없을 경우 게임에 반영

문제가 있으면 재생성 또는 기본 콘텐츠 사용

예시:

세계관에 존재하지 않는 종족 생성
→ 결과 거부

사망한 NPC가 일반 대화에 등장
→ 결과 거부

현재 층에 등장할 수 없는 몬스터 생성
→ 결과 거부

허용 범위를 초과한 스킬 피해량
→ 수치 제한 또는 결과 거부
8. 전체 시스템 구조
Unreal Engine
│
├─ 플레이어 행동 기록
├─ NPC 상태 관리
├─ 전투 및 퀘스트 진행
├─ 세계 상태 저장
│
└─ AI 콘텐츠 생성 요청
        ↓
Python FastAPI 서버
        ↓
세계관 규칙 조회
        ↓
NPC 기억 및 사건 기록 조회
        ↓
LLM 요청
        ↓
생성 결과 검증
        ↓
JSON 응답
        ↓
Unreal Engine
        ↓
퀘스트, 대사, 아이템 설명 반영
9. 기본 게임 진행 흐름
플레이어가 게임을 시작한다.

마을에 도착한다.

NPC와 대화한다.

AI가 NPC 상태와 세계 기록을 바탕으로 대사를 생성한다.

NPC가 현재 지역 상황에 맞는 퀘스트를 제공한다.

플레이어가 퀘스트를 수락하거나 거절한다.

전투 지역에서 몬스터를 처치하거나 사건을 조사한다.

퀘스트 결과가 세계 기록에 저장된다.

NPC의 신뢰도와 지역 상태가 변경된다.

변경된 상태를 바탕으로 후속 퀘스트가 생성된다.

층 보스를 처치한다.

다음 층으로 이동한다.

최종 층의 보스를 처치하면 엔딩에 도달한다.

10. MVP 개발 범위
전체 범위
마을 1개

던전 또는 전투 지역 3개

구현 층 3층

일반 NPC 5명

일반 몬스터 2종

층별 보스 또는 최종 보스 1종

무기 1종

기본 공격

회피

스킬 2개에서 4개

인벤토리

퀘스트 UI

NPC 대화 UI

저장 및 불러오기

AI 서버 통신

AI 적용 범위
NPC 대화 생성

퀘스트 제목과 설명 생성

퀘스트 발생 원인 생성

후속 사건 생성

아이템 이름과 설명 생성

NPC 기억 요약

세계 사건 요약

MVP에서 제외하는 기능
100개 층 실제 구현

모든 맵 자동 생성

완전한 스킬 자동 생성

모든 아이템 능력치 자동 생성

음성 생성

실시간 NPC 음성 대화

멀티플레이

대규모 오픈월드

수십 종의 몬스터

AI가 직접 조작하는 전투 로직

복잡한 경제 시뮬레이션

11. 역할 분담
이용진 담당
AI 및 서버
Python 서버 구축

FastAPI 엔드포인트 개발

세계관 데이터 관리

NPC 기억 관리

퀘스트 생성

아이템 설명 생성

스킬 이름 및 설명 생성

LLM API 연동

프롬프트 설계

생성 결과 JSON 변환

생성 결과 검증

데이터베이스 관리

RAG 또는 룰 기반 검색 시스템 개발

경식 담당
Unreal Engine 클라이언트
캐릭터 이동

전투 시스템

적 AI

AI Controller

Behavior Tree

보스전

레벨 제작

NPC 배치

대화 UI

퀘스트 UI

인벤토리 UI

아이템 시스템

저장 및 불러오기

HTTP 통신

JSON 파싱

AI 결과 게임 반영

공동 담당
세계관 설정

층별 콘셉트

게임 밸런스

퀘스트 템플릿

스킬 템플릿

NPC 설정

테스트

버그 수정

프로젝트 문서화

발표 및 시연 영상 제작

12. 개발 일정 예시
1단계: 기획 및 구조 설계
핵심 콘셉트 확정

세계관 규칙 정의

MVP 범위 확정

Unreal과 Python 통신 방식 설계

JSON 데이터 형식 정의

역할 분담 확정

2단계: 기본 프로토타입
플레이어 이동과 전투 구현

몬스터 1종 구현

NPC 대화 UI 구현

Python FastAPI 서버 구축

Unreal HTTP 요청 테스트

AI 대화 결과 출력

3단계: 퀘스트 시스템
퀘스트 데이터 구조 구현

퀘스트 수락 및 완료 처리

AI 퀘스트 생성

생성 결과 검증

NPC 관계 수치 적용

4단계: 세계 기억 시스템
주요 사건 저장

NPC 기억 저장

과거 사건을 반영한 대사 생성

후속 퀘스트 생성

저장 및 불러오기 연동

5단계: 콘텐츠 제작
마을 제작

전투 지역 제작

NPC 5명 제작

몬스터 추가

보스 제작

아이템과 스킬 템플릿 제작

6단계: 완성 및 테스트
AI 응답 실패 처리

생성 결과 오류 검증

전투 밸런스 조정

UI 개선

패키징

플레이 테스트

시연 영상 제작

13. 예상 문제와 대응 방안
문제 1. AI가 세계관에 맞지 않는 내용을 생성할 수 있음
대응:

세계관 규칙을 구조화된 데이터로 관리한다.

생성 결과를 서버에서 검증한다.

허용된 종족, 지역, 아이템, 몬스터 목록을 사용한다.

문제가 발생하면 재생성하거나 기본 콘텐츠를 출력한다.

문제 2. AI 응답 시간이 길어질 수 있음
대응:

대화 시작 전에 일부 콘텐츠를 미리 생성한다.

로딩 UI를 제공한다.

자주 사용하는 대사는 캐싱한다.

API 실패 시 기본 대사를 사용한다.

문제 3. API 비용이 증가할 수 있음
대응:

모든 대화를 AI로 생성하지 않는다.

중요 대화만 AI를 사용한다.

반복되는 결과는 저장 후 재사용한다.

긴 대화 기록 대신 사건 요약을 사용한다.

개발 중에는 저비용 모델이나 로컬 모델을 고려한다.

문제 4. AI가 게임 밸런스를 파괴할 수 있음
대응:

실제 수치는 게임에서 결정한다.

AI는 이름, 설명, 맥락만 생성한다.

스킬과 아이템은 템플릿 기반으로 제한한다.

피해량과 보상 범위를 코드로 제한한다.

문제 5. 개발 범위가 지나치게 커질 수 있음
대응:

실제 구현은 3층으로 제한한다.

마을은 1개만 구현한다.

NPC는 5명으로 제한한다.

AI 생성 범위를 대화와 퀘스트 중심으로 제한한다.

맵과 전투는 개발자가 직접 제작한다.

14. 실패 대응 구조
AI 서버 연결에 실패해도 게임은 실행되어야 한다.

오류 발생 시 다음 방식으로 처리한다.

AI 서버 연결 성공
→ 생성 콘텐츠 사용

AI 서버 연결 실패
→ 미리 작성된 기본 퀘스트와 대화 사용

AI 응답 형식 오류
→ 재요청 1회

재요청 실패
→ 기본 콘텐츠 사용
게임 화면에는 다음과 같은 안내를 표시할 수 있다.

AI 세계 생성 기능에 연결할 수 없습니다.
기본 시나리오 모드로 진행합니다.
15. MVP 완료 조건
다음 조건을 충족하면 MVP가 완성된 것으로 판단한다.

플레이어가 마을과 전투 지역을 이동할 수 있다.

NPC와 대화할 수 있다.

AI가 NPC 대사를 생성한다.

AI가 세계관에 맞는 퀘스트를 생성한다.

플레이어가 퀘스트를 수락하고 완료할 수 있다.

퀘스트 결과가 세계 기록에 저장된다.

이전 행동이 이후 NPC 대사에 반영된다.

NPC 신뢰도에 따라 새로운 대화나 퀘스트가 열린다.

AI가 아이템 이름과 설명을 생성한다.

층 보스를 처치하고 엔딩을 볼 수 있다.

AI 서버가 꺼져도 기본 모드로 게임을 진행할 수 있다.

16. 프로젝트 차별점
일반적인 AI 게임은 NPC와 자유 대화를 하거나 단발성 퀘스트를 생성하는 데 집중하는 경우가 많다.

본 프로젝트는 다음 부분에서 차별점을 가진다.

AI가 세계관 규칙을 지킨다.

플레이어의 행동을 장기적으로 기억한다.

퀘스트 사이에 원인과 결과가 존재한다.

NPC 관계가 게임 진행에 영향을 준다.

이전 사건이 새로운 사건으로 이어진다.

AI가 게임 전체를 만드는 것이 아니라 세계를 운영한다.

실제 게임 밸런스는 개발자가 통제한다.

작은 데모로도 대규모 확장 가능성을 보여줄 수 있다.

17. 최종 방향
본 프로젝트에서 가장 중요한 것은 콘텐츠의 양이 아니다.

실제 100개의 층을 제작하는 것보다, 3개의 층 안에서 플레이어의 행동이 기록되고, NPC가 이를 기억하며, 이전 사건이 새로운 퀘스트로 이어지는 경험을 구현하는 것이 더 중요하다.

최종 프로젝트는 다음과 같은 방향을 목표로 한다.

개발자는 세계를 직접 완성하지 않는다.
개발자는 세계의 법칙을 만든다.
AI는 그 법칙을 지키며 세계의 역사를 이어간다.

이 문서를 기준으로 실제 개발에 들어갈 때는 다음 단계로 세계관 설정서, 기능 명세서, 서버 API 명세서, 일정표를 분리하는 게 좋아.


md로 만들어줘야지 노션에서 사용 가능하게

노션에서 바로 가져올 수 있는 Markdown 파일로 만들었어.

AI_%EC%84%B8%EA%B3%84_%EC%9A%B4%EC%98%81%ED%98%95_RPG_%EA%B0%9C%EB%B0%9C%EA%B8%B0%ED%9A%8D%EC%84%9C.md

노션에서는 가져오기 → Markdown & CSV → 파일 선택으로 불러오면 돼. 


현실적으로 unreal이 나음? unity가 나음?? 지금 개발 문서대로 개발한다면

현실적으로는 지금 문서대로라면 Unity가 조금 더 유리해.
다만 경식이가 이미 언리얼 경험과 기존 전투 코드를 재사용할 수 있다면 Unreal이 더 현실적이야.

결론
새 프로젝트를 완전히 처음부터 만든다면
Unity 추천

이유는 이 프로젝트의 핵심이 그래픽이나 고급 전투가 아니라:

AI 퀘스트 생성

NPC 기억

HTTP 통신

JSON 처리

저장 시스템

데이터 관리

빠른 프로토타입

이기 때문이야.

이런 데이터 중심 기능은 Unity의 C#이 상대적으로 빠르게 만들기 편해.

경식이가 기존 언리얼 RPG 코드를 가져올 수 있다면
Unreal 추천

경식이는 이미 언리얼에서:

캐릭터 전투

적 AI

Behavior Tree

보스

스킬

UI

저장 시스템

C++/Blueprint

등을 구현한 경험이 있으니까, 새로 Unity를 배우는 시간보다 기존 언리얼 구조를 재활용하는 게 훨씬 빠를 수 있어.

프로젝트 기준 비교
항목	Unreal	Unity
초기 개발 속도	느린 편	빠른 편
AI 서버 HTTP 연동	가능하지만 C++ 코드가 길어짐	C#에서 비교적 간단
JSON 처리	구조체 정의와 변환 필요	비교적 편함
UI 제작	UMG 학습 필요	비교적 빠름
데이터 중심 게임	가능	잘 맞음
액션 전투	강점	직접 구성 필요
고품질 그래픽	강점	상대적으로 추가 작업 필요
빌드 용량	큼	상대적으로 작음
개발 PC 요구사항	높음	상대적으로 낮음
2인 개발 적합성	범위 통제가 중요	비교적 적합
경식이 숙련도	이미 경험 있음	새로 배워야 할 수 있음
Unreal을 사용할 때 문제점
이 문서 그대로 Unreal에서 만들면 생각보다 작업량이 커.

예를 들어 AI가 만든 퀘스트를 적용하려면:

Python 서버 응답
↓
Unreal HTTP 요청
↓
JSON 파싱
↓
USTRUCT 변환
↓
퀘스트 데이터 생성
↓
UI 갱신
↓
저장 데이터 기록
이 구조를 C++로 만들면 클래스와 구조체가 꽤 많이 필요해.

또 언리얼에서는 다음 작업도 무거워질 수 있어.

패키징

레벨 관리

애니메이션

UI

DataAsset와 DataTable

C++ 컴파일

엔진 버전 문제

에셋 관리

AI 실험이 핵심인데, 게임 엔진 작업에 대부분의 시간이 들어갈 위험이 있어.

Unity를 사용할 때 장점
Unity에서는 친구가 사용하는 Python과 직접 연결되는 것은 아니지만, C#으로 서버 통신이나 데이터 처리를 빠르게 만들 수 있어.

예를 들면 AI 서버 통신 구조가 비교적 단순해.

[System.Serializable]
public class QuestResponse
{
    public string title;
    public string description;
    public string targetType;
    public int targetCount;
}
AI 응답을 JSON으로 받아 바로 데이터로 사용할 수 있어.

또한 이 프로젝트에서 중요한:

퀘스트 데이터

NPC 상태

관계 수치

이벤트 기록

저장/불러오기

API 요청

같은 시스템은 Unity와 C#이 꽤 편한 편이야.

하지만 경식이 상황에서는 Unreal이 더 나을 가능성이 큼
가장 중요한 건 엔진 자체의 우열보다 누가 구현할 수 있느냐야.

현재 역할 구조는:

이용진
Python / FastAPI / AI / 데이터베이스

경식
게임 엔진 / 전투 / UI / 연동
이용진은 게임 엔진을 거의 못 다루고, 경식이가 게임 부분 대부분을 담당해야 해.

경식이가 Unreal을 이미 알고 있는데 Unity까지 새로 배우면:

Unity 학습
+
게임 시스템 제작
+
AI 서버 연동
+
콘텐츠 제작
을 동시에 해야 해.

이건 오히려 일정이 더 오래 걸릴 수 있어.

가장 현실적인 선택
내 추천은 Unreal을 사용하되, 기존 문서를 더 줄이는 것이야.

Unreal MVP 범위
층 1개

마을 1개

전투 지역 1개

NPC 3명

일반 몬스터 1종

보스 1종

무기 1종

퀘스트 유형 3개

AI 대화 생성

AI 퀘스트 설명 생성

플레이어 행동 기억 3개 정도

엔딩 1개

현재 문서의 3~5층도 2인 프로젝트에는 많을 가능성이 높아.

AI 프로젝트의 핵심을 보여주려면 층의 개수보다 아래 흐름이 더 중요해.

플레이어가 NPC를 도움
↓
행동이 저장됨
↓
NPC가 다음 대화에서 이를 기억
↓
새로운 퀘스트가 생성됨
↓
퀘스트 결과가 엔딩에 반영됨
이 흐름 하나만 제대로 작동해도 프로젝트의 핵심은 충분히 보여.

최종 판단
기술만 비교하면 Unity가 이 프로젝트에 더 잘 맞는다.

하지만 현재 팀 상황까지 포함하면:

경식이가 기존 언리얼 코드와 경험을 활용할 수 있으므로 Unreal이 더 현실적인 선택이다.

단, 언리얼을 선택한다면 “100층 확장 가능 구조”만 설계하고 실제 구현은 1층짜리 완성된 데모로 줄이는 게 성공 가능성이 가장 높아.


일단 경식이가 C#이나 Unity를 사용 안해봤는데 이거까지 고려하면?

그것까지 고려하면 Unreal이 훨씬 현실적이야.

엔진 자체만 놓고 보면 Unity가 데이터 처리나 빠른 프로토타이핑에 유리한 부분이 있지만, 지금 팀 상황은 이렇잖아.

경식: Unreal과 C++ 경험 있음

이용진: Python·AI 서버 담당

경식: C#과 Unity 경험 없음

게임 엔진 개발자는 사실상 경식 1명

이 상황에서 Unity를 선택하면 경식이가 프로젝트 시작 전에 먼저 배워야 해.

C# 문법
Unity 에디터
GameObject / Component 구조
Prefab
Scene 관리
Animator
NavMesh
UI Toolkit 또는 uGUI
ScriptableObject
직렬화와 저장
UnityWebRequest
빌드 및 패키징
즉, 게임을 만드는 게 아니라 새로운 엔진을 배우는 기간이 추가돼.

현실적인 비교
Unreal 선택
경식이가 이미 아는 것:

캐릭터 이동

액션 전투

애니메이션 몽타주

Behavior Tree

AI Perception

보스 패턴

UMG

DataAsset·DataTable

C++와 Blueprint 연동

패키징 경험

새로 배워야 하는 핵심은:

HTTP 요청

JSON 직렬화·역직렬화

Python 서버 연결

동적 퀘스트 데이터 관리

NPC 기억 저장

즉, AI 연동에 집중할 수 있어.

Unity 선택
새로 배워야 하는 것:

C#

Unity 자체

전투 시스템

애니메이션

적 AI

UI

데이터 관리

저장 시스템

HTTP 연동

빌드

AI 연동은 쉬워질 수 있지만, 그 전에 게임 전체를 다시 배워야 해.

개발 시간 관점
대략적인 작업 흐름을 비교하면 이래.

Unreal

기존 경험 활용
→ 기본 게임 프로토타입
→ Python API 연동
→ AI 퀘스트·NPC 기억 구현
Unity

C# 학습
→ Unity 학습
→ 게임 프로토타입 제작
→ 전투와 AI 제작
→ Python API 연동
→ AI 퀘스트·NPC 기억 구현
Unity가 최종적으로 코드를 짧게 작성할 수 있더라도, 거기까지 도달하는 학습 비용이 더 커.

추천 결정
현재 팀 구성에서는 Unreal을 선택하는 게 맞다.

다만 Unreal을 쓴다고 해서 이전 문서의 모든 기능을 구현하면 안 돼. Unreal은 전투, 애니메이션, 에셋, 레벨 제작에 시간이 많이 들어갈 수 있으므로 AI 기능을 검증하는 데 집중해야 해.

실제 MVP 범위
맵 1개

마을과 던전을 한 레벨 안에 배치

NPC 3명

몬스터 1종

보스 1종

무기 1종

공격, 회피, 스킬 1개

퀘스트 유형 2개

NPC 기억 시스템

AI 대화 생성

AI 퀘스트 생성

행동에 따른 후속 퀘스트 1개

엔딩 1개

이 정도면 핵심 흐름을 보여줄 수 있어.

NPC가 퀘스트 제공
↓
플레이어가 선택
↓
퀘스트 결과 저장
↓
NPC가 결과를 기억
↓
다음 대화와 퀘스트 변화
↓
보스 또는 엔딩 변화
특히 재사용해야 하는 것
경식이가 기존 Unreal 프로젝트에서 시스템을 그대로 복사할 수 있다면 더 유리해.

재사용 후보:

플레이어 캐릭터

이동 및 카메라

공격과 회피

적 기본 클래스

Behavior Tree

보스 체력 UI

상호작용 UI

결과 UI

아이템 구조

반대로 기존 프로젝트 전체를 가져와 수정하면 의존성이 복잡해질 수 있으니, 필요한 시스템만 작은 새 프로젝트로 옮기는 편이 안전해.

최종 판단표
조건	추천
두 사람 모두 엔진 경험 없음	Unity 고려
경식이 Unity 경험 있음	Unity 고려
경식이 Unreal 경험만 있음	Unreal
고품질 액션 전투가 중요함	Unreal
게임보다 AI 웹 데모가 중요함	Unity 또는 웹
실제 플레이 가능한 액션 RPG 목표	Unreal
결국 이 프로젝트의 가장 큰 위험은 엔진 성능이 아니라 범위와 학습 비용이야. 경식이가 Unity와 C#을 처음부터 배우는 순간 프로젝트 위험도가 크게 올라가므로, Unreal로 만들고 콘텐츠 규모를 줄이는 방향이 성공 가능성이 가장 높아.


Asset 구매하는것도 고려해야됨, Unreal은 경식이가 받아놓은 Asset이 많고 Unity는 전혀 없어



취소

보내기

언리얼 프로젝트 기준으로 소스·Config·Content는 올리고, 빌드 산출물·캐시·Visual Studio 개인 설정은 제외되도록 만들게. AI API 키 유출 방지용 .env도 포함했어.


git에 unreal 프로젝트랑 visual studio 코드 올릴건데 git ignore 만들어줘, 지금은 아래처럼 들어가있음


# Visual Studio 2015 user specific files
.vs/

# Compiled Object files
*.slo
*.lo
*.o
*.obj

# Precompiled Headers
*.gch
*.pch

# Compiled Dynamic libraries
*.so
*.dylib
*.dll

# Fortran module files
*.mod

# Compiled Static libraries
*.lai
*.la
*.a
*.lib

# Executables
*.exe
*.out
*.app
*.ipa

# These project files can be generated by the engine
*.xcodeproj
*.xcworkspace
*.sln
*.suo
*.opensdf
*.sdf
*.VC.db
*.VC.opendb
.vsconfig

# Precompiled Assets
SourceArt/**/*.png
SourceArt/**/*.tga

# Binary Files
Binaries/*
Plugins/**/Binaries/*

# Builds
Build/*

# Whitelist PakBlacklist-<BuildConfiguration>.txt files
!Build/*/
Build/*/**
!Build/*/PakBlacklist*.txt

# Don't ignore icon files in Build
!Build/**/*.ico

# Built data for maps
*_BuiltData.uasset

# Configuration files generated by the Editor
Saved/*

# Compiled source files for the engine to use
Intermediate/*
Plugins/**/Intermediate/*

# Cache files for the editor to use
DerivedDataCache/*



지금 프로젝트 기준으로 정리한 파일이야.

UnrealEngine.gitignore 다운로드

프로젝트 루트에 넣고 파일명을 정확히 .gitignore로 바꾸면 돼.

기존 파일과 비교해서 중요한 변경점은 이거야.

Source/, Content/, Config/, .uproject는 Git에 올라감

Binaries/, Intermediate/, Saved/, DerivedDataCache/는 제외

플러그인의 소스와 콘텐츠는 올라가고 생성 폴더만 제외

.sln, .vcxproj 등 언리얼이 다시 생성할 수 있는 Visual Studio 파일은 제외

.vsconfig는 제외하지 않아서 팀원이 필요한 VS 워크로드를 공유할 수 있음

.env는 API 키 보호를 위해 제외

*.uasset, *.umap, *_BuiltData.uasset은 제외하지 않음

특히 기존에 있던 아래 항목은 제거하는 걸 권장해.

*_BuiltData.uasset
이 파일은 맵의 빌드 데이터가 들어갈 수 있어서, 팀원이 프로젝트를 받았을 때 조명이나 맵 상태가 달라질 가능성이 있어.

그리고 이미 Git에 Binaries, Saved, Intermediate가 올라간 상태라면 .gitignore만 추가해도 기존 추적은 계속돼. 한 번 캐시에서 제거해야 해.

git rm -r --cached Binaries Intermediate Saved DerivedDataCache .vs
git add .
git commit -m "chore: update Unreal Engine gitignore"
프로젝트 전체를 새로 정리하려면 다음처럼 해도 돼.

git rm -r --cached .
git add .
git commit -m "chore: apply Unreal Engine gitignore"
두 번째 명령은 실제 파일을 삭제하는 게 아니라 Git 추적 목록을 다시 구성하는 것이야. 


image(550).png
이정도만 올리면 됨?

응, 기본적으로는 저 정도면 맞아.

지금 보이는 것 중 Git에 올려야 하는 핵심은:

Config/

Content/

Source/

.gitignore

.uproject

이 5개가 맞아.

Config, Content, Source가 접혀 있어서 내부를 확인해야 하지만, 보통 언리얼 프로젝트는 이 구성이면 다른 사람이 받아서 프로젝트를 열 수 있어.

.vsconfig는?
올려도 돼. 팀원이 Visual Studio Installer에서 필요한 워크로드를 맞추는 데 도움이 돼.

다만 꼭 필요한 파일은 아니야.

추가로 올라갈 수 있는 항목
프로젝트에 실제로 존재한다면 다음도 올려야 해.

Plugins/

직접 만든 플러그인

프로젝트 전용 플러그인

SourceArt/

원본 이미지나 모델을 팀에서 공유해야 하는 경우

Build/ 내부 아이콘이나 설정 파일

.env.example

AI 서버 환경변수 이름 공유용

Python 서버 폴더

main.py

requirements.txt

서버 코드

단, .env, venv/는 제외

예를 들어 저장소가 이런 형태면 좋아.

SAOProject/
├─ Config/
├─ Content/
├─ Source/
├─ Plugins/
├─ AI_Server/
│  ├─ main.py
│  ├─ requirements.txt
│  └─ .env.example
├─ .gitignore
├─ .vsconfig
└─ SAO.uproject
꼭 확인할 것
Content/에 .uasset, .umap 파일이 실제로 스테이지되는지 확인해.

그리고 Git GUI에서 아래 폴더가 안 보이는 건 정상이어야 해.

Binaries/
Intermediate/
Saved/
DerivedDataCache/
.vs/
저 폴더들이 보이지 않는다면 .gitignore가 제대로 적용된 거야.

마지막으로 Content 용량이 크면 GitHub 일반 Git 제한에 걸릴 수 있으니, 큰 에셋 파일은 Git LFS를 쓰는 게 좋아. 특히 .uasset, .umap, .fbx, .wav가 많으면 LFS를 고려해야 해.


LFS를 어떻게 넣는지 알려줘

언리얼 프로젝트 루트에서 터미널이나 Git Bash를 열고 아래 순서대로 하면 돼.

1. Git LFS 설치 확인
git lfs version
버전이 나오면 설치된 상태야. 안 나오면 Git LFS를 설치한 뒤 한 번만 실행해.

git lfs install
git lfs install은 사용자 계정 기준으로 한 번만 실행하면 돼. 

2. 언리얼 대용량 파일 등록
프로젝트 루트에서 실행:

git lfs track "*.uasset"
git lfs track "*.umap"
추가 원본 파일도 저장소에 올릴 거라면:

git lfs track "*.fbx"
git lfs track "*.wav"
git lfs track "*.mp3"
git lfs track "*.png"
git lfs track "*.tga"
git lfs track "*.psd"
git lfs track을 실행하면 프로젝트 루트에 .gitattributes 파일이 생겨. 이 파일도 반드시 Git에 올려야 팀원에게 같은 LFS 설정이 적용돼. 

언리얼 프로젝트에서는 우선 아래 정도를 추천해.

*.uasset filter=lfs diff=lfs merge=lfs -text
*.umap filter=lfs diff=lfs merge=lfs -text
*.fbx filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.psd filter=lfs diff=lfs merge=lfs -text
*.tga filter=lfs diff=lfs merge=lfs -text
png는 UI 이미지가 많으면 LFS에 넣어도 되지만, 작은 이미지까지 전부 LFS로 관리할 필요는 없어.

3. 생성된 파일 확인
git status
다음처럼 보여야 해.

.gitattributes
Content/...
Source/...
Config/...
SAO.uproject
4. 커밋
git add .gitattributes
git add .
git commit -m "chore: configure Git LFS for Unreal assets"
git push
이미 .uasset을 Git에 추가한 경우
아직 커밋하지 않았다면:

git rm --cached -r Content
git add Content
git commit -m "chore: track Unreal assets with Git LFS"
이미 커밋하고 원격 저장소에도 올린 상태라면 단순히 git lfs track만 해서는 기존 기록이 LFS로 바뀌지 않아. 기존 파일을 LFS로 옮기는 별도 작업이 필요해. GitHub 공식 문서도 기존에 일반 Git으로 추적된 파일은 제거한 뒤 LFS로 다시 추적해야 한다고 안내해. 

필요하면 다음 명령을 사용할 수 있어.

git lfs migrate import --include="*.uasset,*.umap,*.fbx,*.wav,*.psd,*.tga"
단, 이 명령은 Git 커밋 기록을 다시 작성하므로 이미 다른 팀원이 저장소를 받은 상태라면 주의해야 해.

적용됐는지 확인
git lfs ls-files
예시:

abc123 * Content/Characters/Hero.uasset
def456 * Content/Maps/MainMap.umap
이렇게 나오면 정상 적용된 거야.

가장 기본적인 권장 설정은 이것만 해도 충분해.

git lfs install
git lfs track "*.uasset"
git lfs track "*.umap"
git add .gitattributes
git add .
git commit -m "chore: configure Git LFS"
git push


붙여넣은 텍스트 (1)(27).txt
문서
된건가?

응, Git LFS 적용된 상태가 맞아.

git lfs ls-files 결과에 이렇게 파일들이 잔뜩 나오고 있잖아.

34981a5ad2 * Content/StarterContent/Architecture/Floor_400x400.uasset
285c67c63d * Content/StarterContent/Maps/Advanced_Lighting.umap
이 뜻은 해당 .uasset, .umap 파일들이 일반 Git이 아니라 Git LFS 추적 대상으로 등록되었다는 거야. 


이제 마지막으로 아래만 확인하면 돼.

git status
여기서 .gitattributes가 보이면 반드시 같이 커밋해야 해.

git add .gitattributes
git add .
git commit -m "chore: configure Git LFS"
git push
푸시 후 한 번 더 확인:

git lfs ls-files
지금처럼 목록이 나오면 정상이고, GitHub나 GitLab 원격 저장소에서도 LFS 업로드가 진행돼.

추가로 확인하고 싶으면:

git check-attr filter -- Content/StarterContent/Maps/StarterMap.umap
정상이면 대략 이렇게 나와.

Content/StarterContent/Maps/StarterMap.umap: filter: lfs
현재 출력만 보면 LFS 설정 자체는 성공이야. 이제 .gitattributes를 커밋하고 푸시하면 끝이야.


]그러면 이제 팀원한태 내 래포 주소를 주면됨?? https를 주면됨?

응, 이제 팀원에게 저장소 주소를 주면 돼.
처음 공유할 때는 보통 HTTPS 주소가 가장 간단해.

예:

git clone https://github.com/사용자명/저장소명.git
팀원은 순서대로 하면 돼.

git lfs install
git clone https://github.com/사용자명/저장소명.git
클론이 끝나면 LFS 파일도 보통 같이 내려받아져. 혹시 에셋이 포인터 파일처럼 보이거나 제대로 안 받아졌으면:

git lfs pull
저장소가 Private인 경우
주소만 준다고 바로 접근되지는 않아. GitHub 기준으로 팀원을 저장소에 초대해야 해.

Repository
→ Settings
→ Collaborators
→ Add people
→ 팀원 GitHub 계정 추가
팀원이 초대를 수락한 뒤 HTTPS 주소로 클론하면 돼.

HTTPS와 SSH 차이
처음 같이 작업한다면 HTTPS 추천이야.

HTTPS: 설정이 간단하지만 로그인할 때 GitHub 토큰이나 Credential Manager를 사용

SSH: 처음에 SSH 키 등록이 필요하지만 이후 인증이 편함

팀원이 Git을 많이 사용하지 않았다면 HTTPS가 덜 복잡해.

클론 후 Unreal 프로젝트 여는 순서
팀원은 클론한 폴더에서:

.uproject 우클릭

Generate Visual Studio project files

.uproject 실행

C++ 모듈 빌드 요청이 나오면 빌드

필요한 Unreal Engine 버전이 같은지 확인

또는 Visual Studio에서 생성된 .sln을 열고 빌드해도 돼.

같이 알려줘야 하는 정보
저장소 주소와 함께 다음도 전달하는 게 좋아.

Unreal Engine 버전: 5.x.x
Visual Studio 버전: 2022 17.14
Git LFS 필요
기본 브랜치: main
.env 파일은 별도 전달 또는 직접 생성
특히 .env나 AI API 키는 GitHub에 올리면 안 돼. 팀원에게도 실제 키를 코드나 채팅에 그대로 공유하기보다 각자 환경변수로 설정하도록 하는 게 안전해.


Unreal Engine 버전: 5.x.x
Visual Studio 버전: 2022 17.14
Git LFS 필요
기본 브랜치: main
.env 파일은 별도 전달 또는 직접 생성

이런거 문서로 Git에 올려줄려는데 파일로 만들어봐

팀원이 저장소를 받은 뒤 바로 설치하고 실행할 수 있게 README.md로 만들었어.

README.md

프로젝트 최상위 폴더에 넣으면 돼.

SAO/
├─ Config/
├─ Content/
├─ Source/
├─ .gitignore
├─ .gitattributes
├─ .vsconfig
├─ README.md
└─ SAO.uproject
현재 문서의 Unreal Engine 5.x.x 부분은 실제 사용하는 정확한 버전으로 수정해야 해. 예를 들면:

Unreal Engine 5.4.4
그다음 Git에 올리면 돼.

git add README.md
git commit -m "docs: add project setup guide"
git push



라이브러리
/
README.md


# SAO Project

AI가 세계관의 규칙과 플레이어의 행동을 바탕으로 NPC 대화, 퀘스트, 아이템 설명 및 사건을 생성하는 Unreal Engine 기반 액션 RPG 프로젝트입니다.

---

## 개발 환경

| 항목 | 버전 및 설정 |
|---|---|
| Unreal Engine | 5.x.x |
| Visual Studio | Visual Studio 2022 17.14 |
| 기본 브랜치 | `main` |
| Git 대용량 파일 관리 | Git LFS |
| 게임 클라이언트 | Unreal Engine C++ / Blueprint |
| AI 서버 | Python / FastAPI 예정 |

> `Unreal Engine 5.x.x`는 프로젝트에서 실제로 사용하는 정확한 버전으로 수정해 주세요.

---

## 저장소 복제

### 1. Git LFS 설치

프로젝트의 `.uasset`, `.umap` 파일은 Git LFS로 관리합니다.

Git LFS가 설치되어 있는지 확인합니다.

```bash
git lfs version
```

Git LFS가 설치되어 있다면 다음 명령을 실행합니다.

```bash
git lfs install
```

### 2. 저장소 복제

```bash
git clone <REPOSITORY_HTTPS_URL>
cd SAO
```

`<REPOSITORY_HTTPS_URL>`에는 실제 저장소 HTTPS 주소를 입력합니다.

예시:

```bash
git clone https://github.com/username/repository.git
```

### 3. LFS 파일 다운로드 확인

일반적으로 저장소를 복제할 때 LFS 파일도 함께 다운로드됩니다.

에셋이 정상적으로 내려받아지지 않은 경우 다음 명령을 실행합니다.

```bash
git lfs pull
```

LFS로 관리되는 파일은 다음 명령으로 확인할 수 있습니다.

```bash
git lfs ls-files
```

---

## 프로젝트 실행

### 1. Unreal Engine 버전 확인

프로젝트에서 사용하는 Unreal Engine 버전과 동일한 버전을 설치합니다.

버전이 다르면 에셋 또는 C++ 코드 호환 문제가 발생할 수 있습니다.

### 2. Visual Studio 구성

Visual Studio Installer에서 다음 워크로드 및 구성 요소를 설치합니다.

- Desktop development with C++
- Game development with C++
- Visual Studio Tools for Unreal Engine
- Windows 10 SDK 또는 Windows 11 SDK

저장소에 `.vsconfig` 파일이 포함되어 있다면 Visual Studio Installer에서 해당 설정을 사용할 수 있습니다.

### 3. Visual Studio 프로젝트 파일 생성

`SAO.uproject` 파일을 우클릭한 뒤 다음 메뉴를 실행합니다.

```text
Generate Visual Studio project files
```

메뉴가 보이지 않으면 먼저 Unreal Engine을 설치하고 `.uproject` 파일 연결 상태를 확인합니다.

### 4. 프로젝트 빌드

생성된 Visual Studio 솔루션을 열고 다음 구성으로 빌드합니다.

```text
Configuration: Development Editor
Platform: Win64
```

빌드가 완료되면 `SAO.uproject`를 실행합니다.

프로젝트 실행 중 C++ 모듈을 다시 빌드하겠다는 메시지가 표시되면 빌드를 진행합니다.

---

## 환경변수와 API 키

API 키와 개인 환경설정은 Git에 올리지 않습니다.

다음 파일은 `.gitignore`에 포함되어 있습니다.

```text
.env
.env.*
```

팀원이 사용할 환경변수 목록은 `.env.example` 파일로 공유합니다.

예시:

```env
AI_API_KEY=your_api_key_here
AI_SERVER_URL=http://127.0.0.1:8000
```

실제 `.env` 파일은 각자 로컬 환경에서 생성합니다.

```text
.env.example
→ 복사
→ .env로 이름 변경
→ 개인 API 키 입력
```

> 실제 API 키를 GitHub, GitLab, Discord 또는 메신저에 그대로 올리지 마세요.

---

## Git 작업 규칙

### 작업 시작 전

```bash
git checkout main
git pull
```

기능 개발은 별도 브랜치에서 진행하는 것을 권장합니다.

```bash
git checkout -b feature/기능이름
```

예시:

```bash
git checkout -b feature/ai-npc-dialogue
git checkout -b feature/quest-system
git checkout -b fix/player-movement
```

### 변경사항 커밋

```bash
git add .
git commit -m "feat: add AI NPC dialogue"
```

### 원격 저장소에 업로드

```bash
git push -u origin feature/ai-npc-dialogue
```

작업 완료 후 Pull Request 또는 Merge Request를 생성합니다.

---

## 커밋 메시지 규칙

| 접두사 | 용도 |
|---|---|
| `feat` | 새로운 기능 |
| `fix` | 버그 수정 |
| `refactor` | 기능 변화 없는 코드 개선 |
| `chore` | 설정, 빌드, Git 관리 |
| `docs` | 문서 수정 |
| `asset` | 에셋 추가 또는 수정 |
| `test` | 테스트 코드 |

예시:

```text
feat: add quest generation API
fix: resolve NPC dialogue UI error
asset: add village environment assets
docs: update project setup guide
chore: configure Git LFS
```

---

## Git에 포함되는 주요 항목

```text
Config/
Content/
Source/
Plugins/          # 프로젝트 전용 플러그인이 있을 경우
SAO.uproject
.gitignore
.gitattributes
.vsconfig
README.md
```

다음 폴더는 Unreal Engine이 자동 생성하므로 Git에 올리지 않습니다.

```text
Binaries/
DerivedDataCache/
Intermediate/
Saved/
.vs/
```

---

## 주의사항

### Unreal 에셋 충돌

`.uasset`과 `.umap`은 일반 텍스트처럼 자동 병합하기 어렵습니다.

동일한 맵, Blueprint 또는 DataAsset을 두 명이 동시에 수정하지 않도록 작업 전에 담당 파일을 공유합니다.

특히 다음 파일은 동시 수정을 피합니다.

- 레벨 맵
- GameMode Blueprint
- Player Character Blueprint
- 공용 Widget Blueprint
- 공용 DataTable 또는 DataAsset

### 에셋 이동 및 이름 변경

Unreal Editor 밖의 Windows 탐색기에서 `.uasset` 파일을 직접 이동하거나 이름을 변경하지 않습니다.

에셋 이동과 이름 변경은 Unreal Editor의 Content Browser에서 진행합니다.

이동 후에는 폴더를 우클릭하고 다음 작업을 실행합니다.

```text
Fix Up Redirectors in Folder
```

### 엔진 버전 업그레이드

팀원 개인이 임의로 Unreal Engine 버전을 업그레이드하지 않습니다.

엔진 버전 변경은 팀원 간 합의 후 별도 브랜치에서 테스트합니다.

---

## 문제 해결

### 에셋 파일이 작거나 열리지 않는 경우

Git LFS 포인터만 내려받아졌을 수 있습니다.

```bash
git lfs pull
```

### Visual Studio / Visual Studio Code  솔루션이 없는 경우

`.sln` 파일은 Git에서 관리하지 않습니다.

`SAO.uproject`를 우클릭하고 다음 작업을 실행합니다.

```text
Generate Visual Studio project files
```

### 빌드 오류가 발생하는 경우

다음 폴더를 삭제한 뒤 프로젝트 파일을 다시 생성합니다.

```text
Binaries/
Intermediate/
.vs/
```

그 후:

1. `SAO.uproject` 우클릭
2. `Generate Visual Studio project files`
3. Visual Studio에서 `Development Editor / Win64` 빌드

---

## 프로젝트 담당

### Unreal Engine 클라이언트

- 경식
- 전투 시스템
- 캐릭터 및 적 AI
- 레벨 및 UI
- 저장 시스템


### AI 및 서버

- 이용진
- Python / FastAPI
- LLM API 연동
- NPC 기억 관리
- 퀘스트 생성
- 생성 결과 검증
- 데이터베이스 관리
- HTTP 및 JSON 연동

라이브러리
/
README.md


# SAO Project

AI가 세계관의 규칙과 플레이어의 행동을 바탕으로 NPC 대화, 퀘스트, 아이템 설명 및 사건을 생성하는 Unreal Engine 기반 액션 RPG 프로젝트입니다.

---

## 개발 환경

| 항목 | 버전 및 설정 |
|---|---|
| Unreal Engine | 5.x.x |
| Visual Studio | Visual Studio 2022 17.14 |
| 기본 브랜치 | `main` |
| Git 대용량 파일 관리 | Git LFS |
| 게임 클라이언트 | Unreal Engine C++ / Blueprint |
| AI 서버 | Python / FastAPI 예정 |

> `Unreal Engine 5.x.x`는 프로젝트에서 실제로 사용하는 정확한 버전으로 수정해 주세요.

---

## 저장소 복제

### 1. Git LFS 설치

프로젝트의 `.uasset`, `.umap` 파일은 Git LFS로 관리합니다.

Git LFS가 설치되어 있는지 확인합니다.

```bash
git lfs version
```

Git LFS가 설치되어 있다면 다음 명령을 실행합니다.

```bash
git lfs install
```

### 2. 저장소 복제

```bash
git clone <REPOSITORY_HTTPS_URL>
cd SAO
```

`<REPOSITORY_HTTPS_URL>`에는 실제 저장소 HTTPS 주소를 입력합니다.

예시:

```bash
git clone https://github.com/username/repository.git
```

### 3. LFS 파일 다운로드 확인

일반적으로 저장소를 복제할 때 LFS 파일도 함께 다운로드됩니다.

에셋이 정상적으로 내려받아지지 않은 경우 다음 명령을 실행합니다.

```bash
git lfs pull
```

LFS로 관리되는 파일은 다음 명령으로 확인할 수 있습니다.

```bash
git lfs ls-files
```

---

## 프로젝트 실행

### 1. Unreal Engine 버전 확인

프로젝트에서 사용하는 Unreal Engine 버전과 동일한 버전을 설치합니다.

버전이 다르면 에셋 또는 C++ 코드 호환 문제가 발생할 수 있습니다.

### 2. Visual Studio 구성

Visual Studio Installer에서 다음 워크로드 및 구성 요소를 설치합니다.

- Desktop development with C++
- Game development with C++
- Visual Studio Tools for Unreal Engine
- Windows 10 SDK 또는 Windows 11 SDK

저장소에 `.vsconfig` 파일이 포함되어 있다면 Visual Studio Installer에서 해당 설정을 사용할 수 있습니다.

### 3. Visual Studio 프로젝트 파일 생성

`SAO.uproject` 파일을 우클릭한 뒤 다음 메뉴를 실행합니다.

```text
Generate Visual Studio project files
```

메뉴가 보이지 않으면 먼저 Unreal Engine을 설치하고 `.uproject` 파일 연결 상태를 확인합니다.

### 4. 프로젝트 빌드

생성된 Visual Studio 솔루션을 열고 다음 구성으로 빌드합니다.

```text
Configuration: Development Editor
Platform: Win64
```

빌드가 완료되면 `SAO.uproject`를 실행합니다.

프로젝트 실행 중 C++ 모듈을 다시 빌드하겠다는 메시지가 표시되면 빌드를 진행합니다.

---

## 환경변수와 API 키

API 키와 개인 환경설정은 Git에 올리지 않습니다.

다음 파일은 `.gitignore`에 포함되어 있습니다.

```text
.env
.env.*
```

팀원이 사용할 환경변수 목록은 `.env.example` 파일로 공유합니다.

예시:

```env
AI_API_KEY=your_api_key_here
AI_SERVER_URL=http://127.0.0.1:8000
```

실제 `.env` 파일은 각자 로컬 환경에서 생성합니다.

```text
.env.example
→ 복사
→ .env로 이름 변경
→ 개인 API 키 입력
```

> 실제 API 키를 GitHub, GitLab, Discord 또는 메신저에 그대로 올리지 마세요.

---

## Git 작업 규칙

### 작업 시작 전

```bash
git checkout main
git pull
```

기능 개발은 별도 브랜치에서 진행하는 것을 권장합니다.

```bash
git checkout -b feature/기능이름
```

예시:

```bash
git checkout -b feature/ai-npc-dialogue
git checkout -b feature/quest-system
git checkout -b fix/player-movement
```

### 변경사항 커밋

```bash
git add .
git commit -m "feat: add AI NPC dialogue"
```

### 원격 저장소에 업로드

```bash
git push -u origin feature/ai-npc-dialogue
```

작업 완료 후 Pull Request 또는 Merge Request를 생성합니다.

---

## 커밋 메시지 규칙

| 접두사 | 용도 |
|---|---|
| `feat` | 새로운 기능 |
| `fix` | 버그 수정 |
| `refactor` | 기능 변화 없는 코드 개선 |
| `chore` | 설정, 빌드, Git 관리 |
| `docs` | 문서 수정 |
| `asset` | 에셋 추가 또는 수정 |
| `test` | 테스트 코드 |

예시:

```text
feat: add quest generation API
fix: resolve NPC dialogue UI error
asset: add village environment assets
docs: update project setup guide
chore: configure Git LFS
```

---

## Git에 포함되는 주요 항목

```text
Config/
Content/
Source/
Plugins/          # 프로젝트 전용 플러그인이 있을 경우
SAO.uproject
.gitignore
.gitattributes
.vsconfig
README.md
```

다음 폴더는 Unreal Engine이 자동 생성하므로 Git에 올리지 않습니다.

```text
Binaries/
DerivedDataCache/
Intermediate/
Saved/
.vs/
```

---

## 주의사항

### Unreal 에셋 충돌

`.uasset`과 `.umap`은 일반 텍스트처럼 자동 병합하기 어렵습니다.

동일한 맵, Blueprint 또는 DataAsset을 두 명이 동시에 수정하지 않도록 작업 전에 담당 파일을 공유합니다.

특히 다음 파일은 동시 수정을 피합니다.

- 레벨 맵
- GameMode Blueprint
- Player Character Blueprint
- 공용 Widget Blueprint
- 공용 DataTable 또는 DataAsset

### 에셋 이동 및 이름 변경

Unreal Editor 밖의 Windows 탐색기에서 `.uasset` 파일을 직접 이동하거나 이름을 변경하지 않습니다.

에셋 이동과 이름 변경은 Unreal Editor의 Content Browser에서 진행합니다.

이동 후에는 폴더를 우클릭하고 다음 작업을 실행합니다.

```text
Fix Up Redirectors in Folder
```

### 엔진 버전 업그레이드

팀원 개인이 임의로 Unreal Engine 버전을 업그레이드하지 않습니다.

엔진 버전 변경은 팀원 간 합의 후 별도 브랜치에서 테스트합니다.

---

## 문제 해결

### 에셋 파일이 작거나 열리지 않는 경우

Git LFS 포인터만 내려받아졌을 수 있습니다.

```bash
git lfs pull
```

### Visual Studio 솔루션이 없는 경우

`.sln` 파일은 Git에서 관리하지 않습니다.

`SAO.uproject`를 우클릭하고 다음 작업을 실행합니다.

```text
Generate Visual Studio project files
```

### 빌드 오류가 발생하는 경우

다음 폴더를 삭제한 뒤 프로젝트 파일을 다시 생성합니다.

```text
Binaries/
Intermediate/
.vs/
```

그 후:

1. `SAO.uproject` 우클릭
2. `Generate Visual Studio project files`
3. Visual Studio에서 `Development Editor / Win64` 빌드

---

## 프로젝트 담당

### Unreal Engine 클라이언트

- 경식
- 전투 시스템
- 캐릭터 및 적 AI
- 레벨 및 UI
- 저장 시스템

### AI 및 서버

- 이용진
- Python / FastAPI
- LLM API 연동
- NPC 기억 관리
- 퀘스트 생성
- 생성 결과 검증
- 데이터베이스 관리
- HTTP 및 JSON 연동