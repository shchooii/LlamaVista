
# Vista

### 2024 캡스톤 디자인 – Backend

> 코드 없이도 데이터를 분석할 수 있는 AI 웹 서비스

Vista는 사용자가 데이터를 업로드하면  
대규모 언어 모델(LLM)이 자동으로 분석을 수행하고,  
대화형으로 추가 분석까지 가능한 웹 서비스입니다.

본 프로젝트에서 저는 백엔드를 담당했습니다.



# Vista는 무엇을 하는 서비스인가?

일반적인 데이터 분석에는 다음과 같은 과정이 필요합니다.

- Python/R 코딩  
- 라이브러리 설치  
- 시각화 코드 작성  

Vista는 이러한 과정 없이  
**파일 업로드와 자연어 질문만으로 데이터 분석이 가능하도록 설계된 서비스**입니다.

예시:

> "이 데이터에서 중요한 변수는 무엇인가?"  
> "이 컬럼들을 시각화해줘"  
> "요약 보고서를 만들어줘"  

와 같은 요청을 하면  
LLM이 데이터를 해석하고 분석 결과를 제공합니다.



# Demo

<img width="1510" height="820" src="https://github.com/user-attachments/assets/a23cbceb-1aa2-45a5-93d4-b6b8adb73955" />



# 핵심 기능

## 자동 데이터 분석

- 업로드된 파일 기반 자동 분석  
- LLM을 통한 데이터 이해 및 분석 수행  
- 분석 결과 요약 제공  



## 실시간 분석 결과 Streaming

Vista의 핵심 기능은  
**분석 결과를 실시간으로 전달하는 스트리밍 방식**입니다.

사용자는 분석이 완료될 때까지 기다리지 않고,

```

"데이터 컬럼을 확인 중입니다..."
"시각화 이미지를 생성 중입니다..."
"결과를 요약하고 있습니다..."

```

와 같은 진행 상태를 즉시 전달받습니다.

이를 통해 자연스러운 대화형 분석 경험을 제공합니다.



## 대화형 분석 (Thread 기반)

- 이전 대화 맥락 유지  
- 동일 데이터에 대한 추가 질문 가능  
- 분석 히스토리 재사용 가능  



## 자동 시각화 생성

- 그래프 자동 생성  
- 이미지 파일 저장 및 관리  
- 분석 결과와 함께 제공  



# 데이터 관리 방식

Vista는 MongoDB 기반으로  
사용자별 분석 기록을 체계적으로 관리합니다.

## 저장되는 정보

- 사용자 정보  
- 대화 스레드  
- 분석 메시지  
- 생성된 파일 및 이미지  

사용자는 이전 분석을 언제든 다시 확인할 수 있습니다.



# 기술적 특징

Vista Backend의 주요 차별점은  
**WebSocket 없이 HTTP Streaming으로 실시간 응답을 구현한 점**입니다.

## 사용 기술

- FastAPI  
- StreamingResponse  
- Async Generator  

서버가 분석 과정에서 생성되는 결과를  
즉시 클라이언트로 전달하여  
대기 시간을 줄이고 사용자 경험을 개선합니다.



# 주요 API

## 인증

```

/user/register
/user/login

```

## 분석 및 채팅

```

/chat   (Streaming 기반 핵심 API)

```

## 파일 관리

```

/user_file
/file_list

```



# 프로젝트 구조

```

database/   → 데이터베이스 로직
service/    → 인증 처리
vista/      → 분석 및 스트리밍 핵심 로직
static/     → 이미지 및 업로드 파일

````



# 실행 방법

```bash
pip install -r requirements.txt
uvicorn main:app --reload
````



# 역할 (Backend)

* FastAPI 기반 백엔드 전체 개발
* MongoDB 스키마 설계
* API 설계 및 구현
* 비동기 Streaming 기반 실시간 응답 구현
* LLM 결과 저장 및 관리 시스템 구축
* AWS EC2 배포 및 운영



# 저장소

BE: [https://github.com/LlamaVista/LlamaVista/tree/BE](https://github.com/LlamaVista/LlamaVista/tree/BE)
FE: [https://github.com/LlamaVista/LlamaVista/tree/FE](https://github.com/LlamaVista/LlamaVista/tree/FE)
ML: [https://github.com/LlamaVista/LlamaVista/tree/ML](https://github.com/LlamaVista/LlamaVista/tree/ML)



<details>
<summary>데모 영상 보기</summary>

![demo](https://github.com/user-attachments/assets/cfcf3e45-5ed6-4aea-99a9-7f6781637609)

</details>
```
