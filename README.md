# 대학 동아리 안내 RAG 챗봇

## 1. 서비스 개요
- 교내 중앙동아리, 단과대 소모임, 학회 등의 모집 요강과 회칙, 활동 안내 문서를 기반으로 재학생들에게 맞춤형 동아리 정보와 가입 절차, 원문 출처 URL을 안내하는 RAG 챗봇 서비스

## 2. 워크플로우
- **데이터 준비 흐름**: 원본 문서 및 URL 메타데이터 수집 → 동아리·항목별 텍스트 분할 및 URL 태깅 → 임베딩 생성 (Amazon Bedrock Titan) → 벡터 검색 저장소에 적재 (Amazon OpenSearch Serverless)
- **질문 답변 흐름**: 질문 입력 → 관련 문서 및 URL 검색 → 근거 기반 답변 생성 (Claude 3) → 답변 및 출처 URL 카드 출력 (Amazon DynamoDB 세션 저장)

## 3. AWS 아키텍처
- **웹 프론트엔드**: Amazon S3 + Amazon CloudFront (OAC)
- **백엔드 API**: Amazon API Gateway + AWS Lambda
- **문서·벡터·대화 저장소**: Amazon S3, Amazon OpenSearch Serverless, Amazon DynamoDB
- **임베딩·생성 모델**: Amazon Bedrock (Titan Embeddings / Claude 3)
