mitaly 프로젝트를 위한 GitHub Actions 스케줄러를 설정하는 방법을 단계별로 안내해 드리겠습니다.

## 1단계: GitHub 레포지토리 준비하기

1. 자신의 GitHub 계정에 로그인합니다.
2. 이미 레포지토리가 있다면 해당 레포지토리로 이동하거나, 새 레포지토리를 생성합니다.
   - 새 레포지토리 생성: GitHub 홈페이지 우측 상단의 '+' 버튼 > 'New repository' 클릭
   - 레포지토리 이름 입력 후 'Create repository' 클릭

## 2단계: 워크플로우 파일 생성하기

1. 레포지토리에서 '.github/workflows' 디렉토리를 생성합니다.
   - 레포지토리 메인 페이지에서 'Add file' > 'Create new file' 클릭
   - 파일 경로에 '.github/workflows/scheduler.yml' 입력

2. 제공해 주신 스케줄러 코드를 복사하여 파일 내용에 붙여넣기 합니다.

## 3단계: API 키 등록하기

1. GitHub 레포지토리의 'Settings' 탭으로 이동합니다.
2. 좌측 메뉴에서 'Secrets and variables' > 'Actions' 클릭
3. 'New repository secret' 버튼 클릭
4. 'Name' 필드에 'SCHEDULER_API_KEY' 입력
5. 'Value' 필드에 mitaly 프로젝트에서 제공받은 API 키를 입력
6. 'Add secret' 버튼 클릭

## 4단계: 워크플로우 커밋 및 확인

1. 스케줄러 파일을 생성한 후 'Commit new file' 버튼을 클릭합니다.
2. GitHub 레포지토리의 'Actions' 탭으로 이동하여 워크플로우가 등록된 것을 확인합니다.

## 5단계: 워크플로우 작동 확인

1. GitHub Actions는 cron 설정에 따라 매일 UTC 기준 자정(00:00)에 자동으로 실행됩니다.
2. 수동으로 테스트하려면:
   - 'Actions' 탭에서 'Call Scheduler' 워크플로우 클릭
   - 우측의 'Run workflow' 드롭다운 버튼 클릭
   - 'Run workflow' 버튼 클릭

## 주의사항

- cron 표현식 "0 0 * * *"은 UTC 시간대 기준으로 매일 자정에 실행됩니다. 한국 시간으로는 오전 9시에 해당합니다.
- API 키는 GitHub Secrets에 안전하게 저장되며, 워크플로우 실행 시에만 접근 가능합니다.
- 워크플로우 실행 결과는 'Actions' 탭에서 확인할 수 있습니다.

이제 매일 지정된 시간에 mitaly.vercel.app/api/scheduler 엔드포인트로 API 키와 함께 POST 요청이 자동으로 전송될 것입니다.
