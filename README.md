# ITC (Microsoft Data School 3차 프로젝트)
> **실시간 데이터 기반 암호화폐 모의투자 & 학습 플랫폼**
> ![ITC_발표-PPT_1](https://github.com/user-attachments/assets/480c86ba-53e6-4d25-8f60-8813b0bc1db6)

## 📝 프로젝트 소개 (Overview)

**ITC(Investment Training Crypto)**는 변동성이 큰 암호화폐 시장에서 사용자가 자산 손실의 위험 없이 안전하게 투자를 연습하고 학습할 수 있는 **교육형 모의투자 플랫폼**입니다.

단순한 모의투자를 넘어, **Upbit API 기반의 실시간 트레이딩 환경**과 **과거 데이터 기반의 시나리오 시뮬레이션(폭락장, 급등장 등)**을 제공하여 실전 감각을 키울 수 있습니다. 또한, Azure OpenAI 기반의 뉴스 감정 분석과 RAG 챗봇을 통해 투자 판단력을 기를 수 있도록 돕습니다.

### 🎯 프로젝트 목표
- **안전한 학습 환경:** 실제 자금 손실 없는 투자 경험 제공
- **데이터 기반 의사결정:** 실시간 뉴스 감정 분석 및 기술적 지표 제공
- **금융 리터러시 향상:** 암호화폐 백과사전 및 단계별 온보딩 가이드 제공

---

## 🏗 시스템 아키텍처 (Architecture)

본 프로젝트는 **Azure Cloud** 환경에서 **Microservices Architecture(MSA)**를 지향하여 설계되었습니다.

### 🔹 Infra & Deployment (Azure Kubernetes Service)
![ITC_발표-PPT_7](https://github.com/user-attachments/assets/fcaad519-7b15-44c3-ad90-fa38affa2748)
*이미지 설명: 사용자의 트래픽은 Cloudflare와 Load Balancer를 거쳐 AKS(Azure Kubernetes Service) 상의 각 서비스(Web, Auth, AI)로 분산됩니다.*

* **Compute:** Azure Kubernetes Service (AKS)
* **CI/CD:** Azure DevOps Pipelines (Build & Push Image -> ACR -> AKS Deploy)
* **Security:** Azure Key Vault (시크릿 관리), Keycloak (통합 인증), Cloudflare WAF
* **Database:** MariaDB (User Data), Azure SQL Database (Trading/News), Azure Database for MySQL

### 🔹 Data Pipeline & AI (Hybrid Cloud)
* **ETL:** Airbyte를 활용한 온프레미스 MariaDB ↔ Azure SQL 간 하이브리드 동기화 (CDC 적용)
* **Analytics:** Microsoft Fabric & Power BI를 활용한 대시보드 시각화
* **AI Engine:** Azure OpenAI, AWS Bedrock (Open WebUI Gateway), Azure Speech (TTS)

---

## ✨ 주요 기능 (Key Features)

### 1. 실시간 모의투자 (Real-time Trading)
- **Upbit API & WebSocket**을 활용한 실시간 시세 및 호가창 반영
- 지정가/시장가 매수·매도 지원
- Chart.js 기반의 보조지표(이동평균선 등) 및 캔들 차트 제공
![ITC_발표-PPT_9](https://github.com/user-attachments/assets/3a7d1450-840f-4ec5-95f0-1c553116d2c9)
![ITC_발표-PPT_10](https://github.com/user-attachments/assets/d5d2cb25-b135-48e3-a43a-166ddb4c3e68)
![ITC_발표-PPT_11](https://github.com/user-attachments/assets/b86734fd-c767-466c-a33a-c3eb5ac0b2c1)

### 2. 과거 데이터 시뮬레이션 (Backtesting Simulation)
- **3가지 핵심 시나리오(폭락장, 급등장, 횡보장)** 체험
- 과거 특정 시점의 뉴스 팝업과 차트 흐름을 재현하여 위기 대응 능력 학습
- "만약 그때 투자했다면?" 시나리오 검증
![ITC_발표-PPT_12](https://github.com/user-attachments/assets/d8213006-0a29-4838-b675-d936355609d8)
![ITC_발표-PPT_13](https://github.com/user-attachments/assets/cede8c66-fa6c-4a14-a804-ef4834d0e729)
![ITC_발표-PPT_14](https://github.com/user-attachments/assets/460982aa-00a8-4c76-8496-e47b31fe7a6a)
![ITC_발표-PPT_15](https://github.com/user-attachments/assets/7b0b3f85-76e3-49c7-aadb-f7eaf9ea5473)

### 3. AI 기반 뉴스 분석 & 챗봇 (AI News & RAG Chatbot)
- **Azure Functions & Naver Search API**를 이용한 1시간 단위 뉴스 자동 수집
- **Azure OpenAI**를 활용한 뉴스 기사 감정 분석(긍정/부정/중립) 및 요약
- 사용자 투자 데이터 기반 맞춤형 리포트 분석 및 Q&A 챗봇
![ITC_발표-PPT_16](https://github.com/user-attachments/assets/34fdd656-e32c-4d93-a857-8fd26cf677dc)
![ITC_발표-PPT_17](https://github.com/user-attachments/assets/3110e32f-41a9-4b47-bb5b-a12e6ac890a4)
![ITC_발표-PPT_20](https://github.com/user-attachments/assets/f3cecd7f-6892-454d-a3a0-c31c81a9086a)

### 4. 사용자 편의성 & 보안 (UX & Security)
- **Onboarding Guide:** Azure Speech 기반 TTS 음성 안내로 초기 사용자 적응 지원
- **Dashboard:** 투자 성향, 수익률, 거래 내역을 시각화한 Power BI 리포트
- **Keycloak:** 보안성이 강화된 통합 인증 시스템 (SSO 지원)
![ITC_발표-PPT_21](https://github.com/user-attachments/assets/b2659e71-1c8b-4fc3-b513-acefe96b2afb)
![ITC_발표-PPT_18](https://github.com/user-attachments/assets/0cf516bb-dbcd-4080-99b2-0aba52c34363)
![ITC_발표-PPT_19](https://github.com/user-attachments/assets/2ca92dcc-f39a-4174-8e3d-568c6f9e58f1)
![ITC_발표-PPT_26](https://github.com/user-attachments/assets/4cb558ca-9d81-4cfa-990b-7526ea48ee05)
![ITC_발표-PPT_27](https://github.com/user-attachments/assets/a5ee7e3d-fa43-4fa8-bdc2-11caaf4d2dad)
![ITC_발표-PPT_28](https://github.com/user-attachments/assets/d9452baf-3fbc-4cea-a995-c3442fb21f26)
![ITC_발표-PPT_29](https://github.com/user-attachments/assets/14202e95-345c-4b7a-8ebb-f6c1ab9b6bd3)


## 🛠 기술 스택 (Tech Stack)

| Category | Technologies |
| :--- | :--- |
| **Frontend** | HTML5, CSS3, JavaScript, Chart.js, OpenWebUI |
| **Backend** | Node.js (Express), Python |
| **Database** | MariaDB, Azure SQL Database, Azure Database for MySQL |
| **Cloud & DevOps** | **Azure Kubernetes Service (AKS)**, Azure DevOps, Terraform, Ansible, Docker |
| **Data & AI** | **Microsoft Fabric**, Power BI, Airbyte, **Azure OpenAI**, Azure Speech |
| **Security** | **Keycloak**, Azure Key Vault, Cloudflare |
---
![ITC_발표-PPT_34](https://github.com/user-attachments/assets/c05a5c9b-fe62-4c47-b00d-33beea40223f)
![ITC_발표-PPT_35](https://github.com/user-attachments/assets/e8ef0231-a2f6-4cde-8e77-af1cd04858bd)
![ITC_발표-PPT_37](https://github.com/user-attachments/assets/c559970f-5d21-4b56-bc1b-e48968e0efc1)
![ITC_발표-PPT_38](https://github.com/user-attachments/assets/2f400770-ed54-46ac-9f8f-0e3f39f20e73)
