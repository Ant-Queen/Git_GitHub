# VS Code 음성 지원 정리

## 개요

Visual Studio Code는 `VS Code Speech` 확장을 통해 음성 입력과 음성 채팅을 지원합니다. 음성 기능은 로컬에서 처리되며 인터넷 연결이 없어도 사용할 수 있습니다.

## 시작하기

- 먼저 마켓플레이스에서 `VS Code Speech` 확장을 설치합니다.

## Editor dictation (에디터 받아쓰기)

- 에디터에 음성으로 입력하려면 다음 명령을 사용합니다.
  - `Voice: Start Dictation in Editor` : `Ctrl+Alt+V`
  - `Voice: Stop Dictation in Editor` : `Escape`
- 명령을 실행하면 커서 위치에 작은 마이크 아이콘이 표시되고 음성 입력을 기다립니다.
- `Ctrl+Alt+V`를 눌러 `walky-talky` 모드를 사용할 수 있습니다.
  - 이 모드를 사용하면 키를 누르고 있을 때만 음성 인식이 활성화되고, 키를 놓으면 요청이 자동으로 제출됩니다.
- 이 기능은 SCM 커밋 입력 상자나 PR 리뷰 코멘트 입력 필드처럼 리치 에디터가 사용되는 장소에서도 동작합니다.

## Voice in chat (채팅에서 음성 사용)

- 음성으로 VS Code의 채팅 기능을 사용할 수 있습니다.
- 명령
  - `Chat: Start Voice Chat` : `Ctrl+I`
- 현재 포커스가 에디터에 있으면 인라인 채팅이 시작되고, 그렇지 않으면 Chat 뷰가 열립니다.
- 특정 위치에서 음성 채팅을 시작하려면 다음 명령을 사용합니다.
  - `Chat: Inline Voice Chat`
  - `Chat: Quick Voice Chat`
  - `Chat: Voice Chat in Chat View`
- 음성 채팅이 활성화되면 채팅 입력 필드에 마이크 아이콘이 표시됩니다.
- 음성 입력 후 일시 중지하면 채팅 프롬프트가 자동으로 제출됩니다.
- 제출 대기 시간을 조정하거나 자동 제출을 비활성화하려면 `accessibility.voice.speechTimeout` 설정을 사용합니다.
  - `0`으로 설정하면 자동 제출이 비활성화됩니다.

## 텍스트 음성 변환(TTS)

- 음성 입력이 사용될 때 채팅 응답을 자동으로 읽어주려면 `accessibility.voice.autoSynthesize` 설정을 활성화합니다.
- 응답 옆에 스피커 아이콘이 표시되며, 선택하거나 `Escape` 키를 눌러 음성 출력을 중단할 수 있습니다.

## Walky talky mode (워크키 토키 모드)

- `Ctrl+Alt+V` 또는 `Ctrl+I` 단축키를 눌러 음성 인식을 시작할 수 있습니다.
- 키를 누르고 있는 동안 음성 인식이 유지되고, 키를 놓으면 인식이 중지됩니다.
- 채팅 모드에서는 키를 놓으면 프롬프트가 제출됩니다.

## "Hey Code"

- `accessibility.voice.keywordActivation` 설정을 사용하면 VS Code가 항상 "Hey Code"라는 문구를 듣고 음성 채팅 세션을 시작할 수 있습니다.
- 이 모드가 활성화되면 상태 표시줄에 마이크 아이콘이 표시됩니다.

## 다국어 지원

- `accessibility.voice.speechLanguage` 설정으로 26개 지원 언어 중 하나를 선택할 수 있습니다.
- 기본값 `auto`는 사용 가능한 경우 VS Code 표시 언어를 사용합니다.
- 각 언어는 개별 확장으로 제공됩니다.
- 음성 인식을 처음 시작할 때 선택한 언어에 대한 확장을 설치하라는 메시지가 표시됩니다.

## 다음 단계

- 다른 VS Code 접근성 기능: `https://code.visualstudio.com/docs/configure/accessibility/accessibility`
- VS Code 사용자 인터페이스: `https://code.visualstudio.com/docs/getstarted/userinterface`
- 기본 편집: `https://code.visualstudio.com/docs/editing/codebasics`
- 코드 탐색: `https://code.visualstudio.com/docs/editing/editingevolved`
