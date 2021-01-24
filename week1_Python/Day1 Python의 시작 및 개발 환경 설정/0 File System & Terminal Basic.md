# 0. File System & Terminal Basic

1. **컴퓨터 OS**
Operating System, 운영체제로 소프트웨어가 하드웨어에 연결되기 위해 기반이 되는 시스템
일반적으로 프로그램은 OS에 의존적이기 때문에 OS에 맞춰서 개발
OS를 선택한다는 것은 어떤 개발 환경에서 개발을 실행할 것인가에 대한 선택
2. **파일 시스템**
File System, OS에서 파일을 저장하는 트리구조 저장 체계
- **디렉토리 vs 파일**
디렉토리: 폴더로 불리기도 함 (그릇), 파일과 다른 디렉토리를 포함할 수 있음
파일: 컴퓨터에 정보를 저장하는 논리적인 단위로 파일명과 확장자로 식별됨, 읽기/쓰기/실행 등을 할 수 있음
- **절대경로 vs 상대경로**
경로란 파일의 고유한 위치, 트리구조상 노드의 연결
절대 경로: 루트 디렉토리부터 파일 위치까지의 경로
상대 경로: 현재 있는 디렉토리부터 타깃 파일까지의 경로
(.은 자기 현재 위치한 폴더, ..은 현재 폴더의 앞에 있는 폴더)
3. **터미널**
마우스가 아닌 키보드로 명령을 입력하여 프로그램 실행(CLI / GUI)
Console = Terminal = CMD창
각 터미널에서 프로그램을 작동하는 shell이 존재하고 shell마다 다른 명령어 사용함 (mac이면 bash, zsh)
ex) User/youngin/workspace/test > dir ..\test   ⇒  test 이전의 디렉토리인 workspace 까지를 의미
ex) User/youngin/workspace/test/one-depth> copy ..\..\abc.txt .\  ⇒ ..\..\abc.txt를 현재 위치로 copy 해라