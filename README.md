# study-git_action


# Github-action

쉽게 말해서 워크플로우를 자동화 시켜주는 도구다. 자동배포, 린트체크, 자동화 스크립트 처리 등을 할 수 있다.

## Github Actions 개념

### Workflows

최상위 개념
하나 이상의 job으로 구성되고, event에 의해 예약되거나 트리거 될 수 있는 자동화된 프로세스 -- ex) 빌드, 테스트, 패키지, 릴리스 또는 배포
yaml으로 작성되고, .github/workflows 폴더아래에 저장
Events

workflow를 트리거하는 특정 활동
ex) 특정 브랜치 push, pr, cron
Jobs

동일한 runner에서 실행되는 일련의 단계
기본적으로 여러 job이 있는 workflow는 병렬로 실행(순차적으로도 가능)
Steps

job에서 명령을 실행할 수 있는 개별 작업
Actions

job을 생성하는 단계로 결합되는 독립 실행형 명령
workflow의 가장 작은 이식 가능한 구성 요소
github 커뮤니티에서 만든 작업 사용가능
Runners

GitHub Actions 러너 애플리케이션이 설치된 서버
GitHub에서 호스팅하는 러너를 사용하거나 직접 호스팅할 수 있습니다. 러너는 사용 가능한 작업을 수신 대기하고 한 번에 하나의 작업을 실행하고 진행 상황, 로그 및 결과를 다시 GitHub에 보고합니다. GitHub 호스팅 러너는 Ubuntu Linux, Microsoft Windows 및 macOS를 기반으로 하며 워크플로의 각 작업은 새로운 가상 환경에서 실행됩니다. GitHub 호스팅 러너에 대한 자세한 내용은 " GitHub 호스팅 러너 정보 ."를 참조하십시오 . 다른 운영 체제가 필요하거나 특정 하드웨어 구성이 필요한 경우 자체 러너를 호스팅할 수 있습니다. 자체 호스팅 러너에 대한 정보는 " 자신의 러너 호스팅 "을 참조하십시오 .
Github Actions workflow 명령어
먼저 기본 명령어에 대해서 알아야한다.

name: learn-github-actions

GitHub 리포지토리의 작업 탭에 표시될 워크플로의 이름(선택)

on: [push]

워크플로 파일을 자동으로 트리거하는 이벤트를 지정 (ex) push, pull_request)

jobs:

모든 작업을 함께 그룹화

check-bats-version:

섹션 check-bats-version내에 저장된 작업 의 이름을 정의

runs-on: ubuntu-latest

작업이 GitHub에서 호스팅하는 새로운 가상 머신에서 실행됨을 의미

steps:

check-bats-version작업 에서 실행되는 모든 단계를 함께 그룹화 . 이 섹션 아래에 중첩된 각 항목은 별도의 작업 또는 셸 명령입니다.

- uses: actions/checkout@v2

리포지토리를 체크아웃하고 이를 러너에 다운로드하여 코드에 대해 작업(예: 테스트 도구)을 실행할 수 있도록 하는 작업

워크플로가 리포지토리의 코드에 대해 실행되거나 리포지토리에 정의된 작업을 사용할 때마다 체크아웃 작업을 사용해야함

- uses: actions/setup-node@v2 with: node-version: '14'

실행기에 지정된 버전의 소프트웨어 패키지 를 설치 하는 작업을 사용 하여 명령에 액세스

- run: npm install -g bats

run키워드는 job에서 명령을 실행하는 작업을 알려준다.

- run: bats -v

# 참조

- https://ms3864.tistory.com/381
