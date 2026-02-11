# Vista

2024 캡스톤 디자인 – Backend

> 코드 없이도 데이터를 분석할 수 있는 AI 웹 서비스

Vista는 사용자가 데이터를 업로드하면  
LLM이 자동으로 분석을 수행하고,  
대화형으로 추가 분석까지 가능한 웹 서비스입니다.

본 프로젝트에서 저는 백엔드를 담당했습니다.



## Vista는 무엇을 하는 서비스인가?

일반적인 데이터 분석에는 다음이 필요합니다.

- Python/R 코딩  
- 라이브러리 설치  
- 시각화 코드 작성  

Vista는  
파일 업로드와 자연어 질문만으로  
데이터 분석이 가능하도록 설계된 서비스입니다.

예시:

> "중요 변수는 무엇인가?"  
> "이 컬럼 시각화해줘"  
> "요약 보고서 만들어줘"  

LLM이 자동으로 분석 결과를 제공합니다.



## Demo

<img width="1510" height="820" src="https://github.com/user-attachments/assets/a23cbceb-1aa2-45a5-93d4-b6b8adb73955" />



## 핵심 기능

### 자동 데이터 분석

- 업로드 파일 기반 분석  
- LLM 데이터 이해 및 분석 수행  
- 요약 결과 제공  

### 실시간 Streaming

분석 진행 상태를 실시간 전달:

```

컬럼 확인 중...
시각화 생성 중...
요약 작성 중...

```

대기 시간을 줄이고  
대화형 분석 경험을 제공합니다.

### 대화형 분석

- 대화 맥락 유지  
- 추가 질문 가능  
- 히스토리 재사용  

### 자동 시각화

- 그래프 자동 생성  
- 이미지 저장 및 관리  



## 데이터 관리

MongoDB 기반으로  
사용자별 분석 기록을 관리합니다.

저장 정보:

- 사용자 정보  
- 대화 스레드  
- 메시지  
- 생성 파일  



## 기술적 특징

WebSocket 없이  
HTTP Streaming 기반 실시간 응답 구현.

사용 기술:

- FastAPI  
- StreamingResponse  
- Async Generator  



## 주요 API

인증

```

/user/register
/user/login

```

분석

```

/chat

```

파일

```

/user_file
/file_list

```



## 프로젝트 구조

```

database/
service/
vista/
static/

````



## 실행 방법

```bash
pip install -r requirements.txt
uvicorn main:app --reload
````



## Backend 역할

* FastAPI 백엔드 개발
* MongoDB 스키마 설계
* API 설계 및 구현
* 비동기 Streaming 구현
* LLM 결과 저장/관리
* AWS EC2 배포 운영



## 저장소

[BE](https://github.com/LlamaVista/LlamaVista/tree/BE), [FE](https://github.com/LlamaVista/LlamaVista/tree/FE), [ML](https://github.com/LlamaVista/LlamaVista/tree/ML)



<details>
<summary>데모 영상 보기</summary>

![demo](https://github.com/user-attachments/assets/cfcf3e45-5ed6-4aea-99a9-7f6781637609)

</details>
