# Git_command

`git init`
- 로컬 저장소 설정(초기화)
- git의 버전 관리를 시작할 디렉토리ㅏ에서 진행

<br>

`git add {fine_name}`
- 변경사항이 있는 파일을 staging area에 추가
- {file_name} 자리에 '.'을 쓰면 모든 파일

<br>

`git commit -m "commit_msg"`
- staging area에 있는 파일들을 저장소에 기록
- 해당 시점의 버전을 생성하고 변경 이력을 남기는 것

<br>

`git status`
- 상태 확인
- git으로 관리하기 위한 파일들이 다 포함되어 있는지

<br>

`git log`, `git log --oneline`
- 버전관리에 대한 로그 확인
- --oneline 옵션 주면 심플버전 확인 가능

<br>

`git config --global -l`
- git.global 설정 정보 보기

<br>

`git commit --amend`
- 커밋메시지나 커밋 전체 수정 가능
- vi모드를 통해 수정

<br>

`git remote add {별칭} {remote_repo_url}`
- 로컬저장소에 원격 저장소 추가
- 별칭 설정 : 원격저장소의 별칭. 보통 origin
- remote_repo_url : repository 주소
- 별칭을 사용해 로컬 저장소 한 개에 여러 원격 저장소 추가 가능

<br>

`git remote -v`
- 리모트 내역 확인

<br>

`git clone {remote_repo_url}`
- 원격 저장소 전체를 복제(다운로드)
- clone을 통해 받은 프로젝트는 이미 init이 되어 있음

<br>

`git push {별칭} {브랜치}`, `git pull {별칭} {브랜치}`
- push : 원격 저장소에 commit 목록을 업로드
- pull : 원격저장소의 변경사항만을 받아옴 (업데이트)