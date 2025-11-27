# Vista

### 2024 캡스톤 디자인 – 백엔드 시스템

> **코드 없이 데이터 분석 가능한 웹 서비스**
>
> Vista BE는 사용자가 업로드한 데이터를 기반으로 대규모 언어 모델(LLM)이 자동으로 분석을 수행하고, 대화를 통해 분석을 심화할 수 있는 기능을 제공하는 백엔드 시스템입니다.

✅ FastAPI 기반 REST API
✅ MongoDB 기반 데이터 관리
✅ 비동기 Streaming 처리로 실시간 응답 제공
✅ 자동 시각화 파일 생성 및 관리
✅ Thread 기반 대화 맥락 유지

---

## 🎥 Demo

![demo (online-video-cutter com)](https://github.com/user-attachments/assets/cfcf3e45-5ed6-4aea-99a9-7f6781637609)

---

# ✨ Backend 소개

Vista BE는 다음 기능을 중심으로 설계되었습니다.

* 사용자 업로드 파일 기반 데이터 분석 자동화
* 분석 과정에서 생성된 메시지/시각화/파일 저장
* **LLM 분석 결과를 비동기 Streaming 으로 실시간 제공**
* Thread 기반 대화 맥락 유지 및 재사용
* 사용자별 분석 기록 관리

---

## 🗄 데이터베이스 구조

MongoDB 기반 스키마는 다음 목적을 갖습니다.

* 사용자별 분석 히스토리 보관
* 대화 컨텍스트 유지
* 자동 생성 파일 관리

### 주요 구조

```
users
 ├─ name
 ├─ email
 ├─ hashed_password
 └─ threads[]
      ├─ thread_id
      ├─ name
      ├─ file_name[]
      └─ messages[]
           ├─ role (user/assistant)
           ├─ text
           └─ file_id[]
```

### 특징

✅ Thread 단위로 분석 맥락 유지
✅ 메시지별 파일 연결 가능
✅ 분석 단계별 기록 확인 가능
✅ 해시 기반 비밀번호 저장

---

# 🚀 핵심 기술 – 비동기 Streaming 처리

Vista BE의 가장 큰 차별점은:

> **LLM 분석 결과를 WebSocket 없이 HTTP Streaming 형태로 실시간 제공한다는 점**

사용자는 전체 응답이 생성될 때까지 기다릴 필요 없이,

```
"데이터 컬럼을 확인 중입니다..."
"시각화 이미지를 생성하고 있습니다..."
"분석 결과 요약 중..."
```

과 같이 생성되는 내용을 즉시 전달받습니다.

---

### 구현 방식

FastAPI `StreamingResponse` + `async generator`

```python
@app.post("/chat")
async def chat(request: ChatRequest):
    async def event_stream():
        async for chunk in llm.generate(request):
            yield chunk
            store_in_db(chunk)

    return StreamingResponse(event_stream(), media_type="text/event-stream")
```

### 장점

✅ 응답 체감 속도 향상
✅ 실시간 대화형 분석 경험 제공
✅ 시각화 생성 상태 전달 가능
✅ FE에서 스트림 기반 출력 렌더링 가능

### 처리 흐름

```
사용자 요청
    ↓
FastAPI /chat
    ↓
event_handler (async generator)
    ↓
LLM 호출 및 분석
    ↓
텍스트/상태 Streaming 전송
    ↓
DB 저장
```

---

# 🔌 FastAPI Endpoints

### 인증

```
/user/register
/user/login
```

### 데이터 분석 & 채팅

```
/create
/create_example
/chat              # 비동기 스트리밍 핵심
/chat_list
/store
```

### 파일 관리

```
/user_file
/file_list
```

---

# 🧱 소스코드 구조

```
database/
 └─ users.py          # DB 스키마 및 접근 로직

service/
 ├─ fastapi_auth.py   # 일반 로그인 처리
 └─ google_auth.py    # 구글 로그인 (현재 미활성)

vista/
 ├─ chat.py           # 채팅 및 분석 요청 처리
 ├─ event_handler.py  # Streaming 처리 핵심
 └─ result.py         # LLM 생성 결과 저장

static/
 └─ images / uploads  # 시각화 이미지 및 사용자 파일
```

---

# ⚙️ 실행 방법

```bash
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

---

# 👨‍💻 Role & Contribution

**Frontend** (👨🏻‍💻 [seoungJun](https://github.com/seo-seoungjun))

* 사용자 페이지 디자인(Figma) 및 프론트개발(React.js)
* 데이터베이스 스키마 설계
* API 설계

**BackEnd** (👨🏻‍💻 [shchooii](https://github.com/shchooii))

* 데이터베이스 스키마 설계
* API 설계
* REST API 개발
* 서버 배포 및 관리

**ML** (👨🏻‍💻 [sabin](https://github.com/sabin5105))

* 인공지능 설계 및 개발
* MLOps
* RESTApi 개발

---

# ✅ BE 주요 기여 요약

* FastAPI 기반 백엔드 전체 개발
* MongoDB를 활용한 유저/스레드/메시지 관리
* **비동기 Streaming 기반 실시간 분석 응답 구현**
* LLM 생성 결과(텍스트/이미지) 저장 및 제공 시스템 구축
* AWS EC2 배포 및 운영

---

# 🔗 관련 저장소

[BE](https://github.com/LlamaVista/LlamaVista/tree/BE)
[FE](https://github.com/LlamaVista/LlamaVista/tree/FE)
[ML](https://github.com/LlamaVista/LlamaVista/tree/ML)

---
