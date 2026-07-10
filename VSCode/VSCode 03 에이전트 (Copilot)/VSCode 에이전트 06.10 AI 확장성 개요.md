# VSCode 에이전트 06.10 AI 확장성 개요

## 한줄 요약
VS Code 확장에서는 AI 기능을 붙여서 사용자 맞춤형 도구, MCP 도구, 채팅 참가자, 언어 모델 API 기반 기능을 제공할 수 있습니다.

## 핵심 개념
- Language Model Tool: 에이전트 모드에서 자동으로 호출되는 도구
- MCP Tool: 외부 서비스와 연결해 도메인 특화 기능을 제공
- Chat Participant: 특정 주제에 특화된 채팅 도우미
- Language Model API: 채팅 UI 밖에서도 AI 기능을 직접 통합

## 선택 기준
- VS Code 내부 API와 긴밀히 연동하려면 Language Model Tool 또는 Chat Participant가 적합합니다.
- 외부 서비스나 여러 환경에서 재사용하려면 MCP Tool이 적합합니다.
- 기존 확장 기능에 AI 기능을 넣고 싶으면 Language Model API가 적합합니다.

## 핵심 정리
AI 확장성은 “VS Code 안에서 AI를 확장하는 방식”이며, 도구·서비스·채팅 경험을 모두 커스터마이즈할 수 있습니다.

## 참고
- 공식 문서: https://code.visualstudio.com/api/extension-guides/ai/ai-extensibility-overview
