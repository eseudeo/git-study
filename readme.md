# Git Study

## Git에 대해서

* 버전관리시스템
* 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템
* git은 빈 디렉토리는 추적하지 않는다.
* 형상관리를 하지 않을 파일은 .gitignore 파일에 추가한다.
* HEAD는 현재 브랜치의 가장 최신 커밋을 의미함
* 기본 원격 저장소를 origin이라고 부른다.

## Git 3단계

* Working Directory (작업트리) : 현재 파일들이 있는 작업트리
* Index (=Stage) : 저장소와 작업트리사이의 영역으로 커밋될 대상이 저장되는 스테이징 영역
* Repository (저장소) : 커밋한 소스가 보관되는 저장소

## Git 용어

* Index (=Stage)
	* 커밋을 실행하기 전의 저장소와 작업트리 사이에 존재하는 공간
	* commit한 이후 push는 안한 상태
	* 등록되지 않은 파일은 commit 되지 않는다.
* Add
	* 파일을 index에 올리는 작업
* Commit
	* 커밋을 하는 행위가 HEAD에 반영한다는 것이다.
	* 파일 or 폴더의 변경사항을 저장
	* 영문/숫자로 이루어진 40자리 고유이름을 가진다.
	* 커밋 위치
		* origin/master
			* 원격 저장소 origin의 브랜치인 master의 위치를 나타내고 있다.
		* origin/HEAD
			* 원격 저장소 origin을 복제해 올 때 다운로드되는 커밋의 위치를 나타낸다.
		* master
			* 로컬 저장소 브랜치인 master의 위치를 나타낸다.
	* 커밋 변경하기
		* `$ git commit --amend`
			* 가장 최근 커밋내용에 내용 수정(설명 뿐만 아니라, 파일도 추가/수정 가능하다.)
		* `$ git checkout --<파일명>`
			* 로컬의 변경 내용을 변경 전 HEAD로 되돌림, 추가한 내용과 변경 내용은 남아있다.(commit만 안한상태)
* 브랜치(branch)
	* 무엇인가?
		* 독립적으로 어떤 작업을 진행하기 위한 개념이다.(독립적으로 개발하는 것)
		* 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있다.
	* master 브랜치
		* 저장소를 처음 만들면, Git은 바로 master 라는 이름의 브랜치를 만들어 둔다. 이 새로운 저장소에 새로운 파일을 추가 한다거나 추가한 파일의 내용을 변경하여 그 내용을 커밋 하는 것은 모두 'master'라는 이름의 브랜치를 통해 처리할 수 있는 일이 된다.
		* 'master' 가 아닌 또 다른 새로운 브랜치를 만들어서 '이제 이 브랜치를 사용할거야!' 라고 선언(체크아웃, checkout) 하지 않는 이상, 이 때의 모든 작업은 'master' 브랜치에서 이루어진다.
	* 통합 브랜치(Master Branch)
		* 언제든지 배포할 수 있는 버전을 만들 수 있어야 하는 브랜치
		* 늘 안정적인 상태를 유지하는 것이 중요!
	* 토픽 브랜치(Feature Branch)
		* 기능 추가나 버그 수정과 같은 단위 작업을 위한 브랜치
		* 통합 브랜치로부터 만들어 내며, 토픽 브랜치에서 특정작업이 완료되면 다시 통합 브랜치에 병합하는 방식으로 진행
		* 피처 브랜치(Feature Branch)라고 부르기도 한다.
	* 사용법
		* 새 브랜치 생성하기
			* `$ git branch feature-A`
			* 새로 만든 브랜치도 지금 작업하고 있던 마지막 커밋을 가리킨다.
		* 브랜치 이동하기
			* `$ git checkout feature-A`
		* 브랜치를 생성하면서 이동하기
			* `$ git checkout -b feature-A`
		* 브랜치 삭제하기
			* `$ git branch -d feature-A`
		* 로컬 브랜치 목록 보기
			* `$ git branch`
		* 리모트 브랜치 목록 보기
			* `$ git branch -r`
			* `$ git push origin <브랜치명>` <- 이렇게 해당 브랜치를 푸쉬 하면 리모트 저장소에 올라간다.
		* 각 브랜치마다 마지막 커밋 메세지 보기
			* `$ git branch -v`
* checkout(선언)
	* 전환
	* 사용법
		* `$ git checkout <브랜치명>/<태그명>` : <브랜치명>으로 전환한다.
		* `$ git checkout -b <새브랜치>` : 새로운 브랜치를 만들면서 전환한다.
		* `$ git checkout --` : 커밋전 파일의 변경 내용을 취소하고 이전 커밋으로 되돌림(커밋하기전의 수정 파일을 )
* HEAD
	* 현재 사용 중인 브랜치의 선두 부분을 나타내는 이름
	* 기본적으로는 'master'의 선두 부분을 나타낸다.
	* 이동
		* HEAD를 이동하면 Branch가 변경
		* ^ or ~1 or ~ : 바로 이전 상태로
		* ^^ or 2 : 2단계 앞으로
	* `$ git reset HEAD --` : 커밋된 파일들을 취소
* stash
	* 파일의 변경 내용을 일시적으로 기록해두는 영역
		* commit 보류
		* 나중에 다시 불러와서 branch 에 commit 할 수 있음
	* stash를 사용하여 작업트리와 인덱스 내에서 아직 커밋하지 않은 변경을 일시적으로 저장해 둘 수 있다.
	* 커밋하지 않은 변경 내용이나 새롭게 추가한 파일이 인덱스와 작업 트리에 남아 있는 채로 다른 브랜치로 전환(checkout)하면, 그 변경 내용은 기존 브랜치가 아닌 전환된 브랜치에서 커밋할 수 있다.
		* 새로운 브랜치를 만들어서 작업하고 있었는데 다른 요청이 들어와서 잠시 브랜치를 변경해야 할 일이 생겼다고 하자. 아직 완료하지 않은 일을 커밋하는 것은 좀 껄끄럽다. 이런 상황에서 커밋하지 않고 나중에 다시 돌아와서 작업을 다시하고 싶을 것이다. 이럴때 git stash로 해결 할수 있다.
		* stash 명령을 사용하면 워킹 디렉토리에서 수정한 파일만 저장한다. 잠시 저장했다가 나중에 다시 적용할 수 있는 것이다.
	* 사용법
		* `$ git stash save` : 현재 작업을 저장하고 branch를  head로 돌린다.
		* `$ git stash list` : 저장되어 있는 stash들 보기
		* `$ git stash pop` : stash를 꺼내와서 적용, stash 들은 stack에 저장된다. 따라서 가장 최근에 save 한 stash가 현재 branch에 적용된다.
		* `$ git stash apply` : pop 과 비슷한 명령어지만 stash list에서 삭제하지 않는다는 점이 다르다.
		* `$ git stash drop` : 필요 없는 stash를 삭제
		* `$ git stash clear` : 전체 stash list를 삭제
* 통합
	* 브랜치 통합에는 merge, rebase를 사용하는 방법의 2가지 종류가 있다.
	* merge
		* 작업이 완료된 토픽 브랜치는 최종적으로 통합 브랜치에 병합된다.
		* 여러개의 브랜치를 하나로 모을수 있다.
		* 사용법
			* `$ git checkout master` : master 브랜치로 이동
			* `$ git merge <브랜치>` : <브랜치>를 현재 브랜치로 통합
			* `$ git merge --no--ff release-0.9.0` : release 브랜치를 merge. no-ff는 히스토리를 명시적으로 만든다.
		* Fast Forward Merge(빨리감기)
			* 분기된 branch만 변경사항이 있을 때
			* Master -> hotfix -> Master
			* non fast-forward 옵션 : hotfix branch가 그대로 남기 때문에 관리상 유용
		* Merge Commit
			* 양쪽 브랜치가 변경 되었을 경우 양쪽의 변경을 가져와서 수정후 merge commit 실행
		* `$ git merge --squash`
			* 해당 브랜치의 커밋 전체를 통합한 커밋 추가
			* 토픽 브랜치 안의 커밋을 한꺼번에 모아 통합 브랜치에 병합할때 사용
	* rebase
		* `$ git rebase <브랜치>` : <브랜치>를 현재 브랜치에 적용
		* 토픽 브랜치가 그대로 통합 브랜치의 끝(HEAD)에 얹혀지는 스타일
		* 각각의 commit 에서 충돌내용을 수정할 필요가 있다.
		* 통합 브랜치의 HEAD는 이전 상태로 그대로 있으나 hotfix branch와 FF Merge를 해서 옮겨 주어야한다.
		* 통합 브랜치에 토픽 브랜치를 불러올 경우 : rebase 한 뒤 merge
		* 충돌 시 취소하려면 `$ git rebase --abort`
		* `$ git rebase -i`
			* 특정 커밋을 다시 쓰거나 다른 커밋과 바꾸기 , 특정 위치 커밋 삭제나 여러 커밋을 하나로 통합도 가능
			* 용도
				* push 하기 전에 커밋내용 정리
				* 이전 커밋에 누락된 파일 추가
				* 알기 쉽게 그룹으로 통합
				* 용도 1 : 커밋 통합하기
					* 사용법
						* `$ git rebase -i HEAD~~` : 마지막 커밋과 마지막 커밋전의 커밋을 통합한다.
						* 두번째 줄의 'pick' 문자를 'squash'로 변경하고 저장,종료 한다.
					* `$ git rebase -i HEAD~5`
						* s(squash)는 이전 커밋과 병합
				* 용도 2 : 커밋 수정하기
					* 사용법
						* `$ git reset -i HEAD~~` : 2단계 전의 커밋을 수정한다.
						* 첫 번째 줄의 'pick' 문자를 'edit'으로 변경하고 저장,종료 한다. ( 그러면 수정할 커밋이 체크아웃된 상태가 된다. )
						* `$ git commit --amend` : 커밋내용을 수정한다.
						* `$ git rebase --continue` : --continue 옵션을 지정하여 커밋 작업이 종료되 었다는 것을 알린다.
			* 취소
				* `$ git reflog`
				* `$ git reset --hard HEAD@{n}`
	* 목적과 운영방침에 따라 구별해서 쓴다.
		* merge
			* 변경 사항이 그대로 남아있기 때문에 이력이 복잡해짐
		* rebase
			* 이력은 단순해지지만, 토픽 브랜치의 commit 이력이 변경됨, 정확한 이력을 남겨야 할 필요가 있을 경우에는 사용하면 안됨
		* 이력을 하나로 모두 모아서 처리하도록 운용한다고 하면 아래와 같이 구별해서 사용할 수 있다.
			* 토픽 브랜치에 통합 브랜치의 최신 코드를 적용할 경우에는 rebase를 사용
			* 통합 브랜치에 토픽 브랜치를 불러올 경우에는 우선 rebase를 한후 merge
* Pull
	* 가져와 병합하기
	* 원격 저장소의 데이터를 로컬 저장소에 가져와 병합하기
	* `$ git pull origin master`
* Fetch
	* 가져오기
	* 원격 저장소의 데이터를 로컬에 가져오기만 하기
	* pull 은 가져와서 병합하는 기능까지 있고, fetch는 원격 저장소의 내용을 확인만 하고 병합은 하고 싶지 않을 때 사용
	* fetch를 실행하면, 원격 저장소의 최신 이력을 확인 할수 있다.
	* 이름 없는 브랜치로 가져온다.
	* `$ git checkout FETCH_HEAD`로 체크아웃 가능
* Push
	* 밀어넣기
	* 로컬 저장소의 데이터를 원격 저장소로 밀어 넣기
	* push 하지 않는 한 원격  저장소에 영향을 주지 않고 자신만의 브랜치에서 자유롭게 작업 할 수 있다.
	* `$ git push origin master` : master 브랜치를 origin 저장소에 push한다.
* Tag(태그)
	* 일반 태그(Lightweight Tag)
		* 이름 정보만
		* `$ git tag <tag-name>`
	* 주석 태그(Anootated Tag)
		* 상세정보 포함(이름,태그에 대한 설명, 서명, 태그를 만든 사람의 이름, 이메일과 태그를 만든 날짜 정보)
		* `$ git tag - a <tag-name>`
		* `$ git tag -am"주석 내용" <tag-name>`
	*  태그 목록
		* `$ git tag`
	* -n 옵션
		* 태그 목록과 주석 내용을 확인할 수 있다.
		* `$ git tag -n`
	* tag 삭제
		* `$ git tag -d <태그명>`
	* `$ git checkout <tag-name>`
		* 특정 상태로 되돌리기
* Revert
	* 특정 커밋 내용 삭제
	* 내부적으로 실제 삭제 하는게 아니라, 해당 커밋의 삭제 커밋을 새로 만들어 안전하게 처리 (A라는 커밋을 지우고 싶을 때 A라는 커밋은 그대로 두고 A를 지운 커밋을 하나더 만든다)
	* 사용법
		* `$ git revert HEAD`
* Reset
	* 커밋을 버리고 특정 버전으로 다시 되돌아가기
		* 더 이상 필요 없어진 커밋들을 버릴 수 있다.
		* 명령어 실행 시 어떤 모드로 실행할 지 지정하여 'HEAD' 위치와 인덱스, 작업 트리 내용을 함께 되돌릴지 여부를 선택할 수 있다.
	* 사용법
		* `$ git reset --hard HEAD~`
			* ~ : 1단계 전으로 이동
			* ~~ : 2단계 전으로 이동
		* --soft
			* 커밋만 되돌린다.
			* `$ git reset --soft <복구시점 커밋id>`
		* --mixed
			* 변경한 인덱스의 상태를 원래대로 되돌린다.
			* `$ git reset --mixed <복구시점 커밋id>`
		* --hard
			* 최근의 커밋을 완전히 버리고 이전 상태로 복구
			* `$ git reset --hard <마지막 커밋id>`
	* reset 실행 전의 상태로 되돌리기
		* reset 전의 커밋은 'ORIG_HEAD' 라는 이름으로 참조할 수 있다.
		* `$ git reset --hard ORIG_HEAD`
* Cherry-pick
	* 다른 브랜치의 특정 커밋을 복사하여 현재 브랜치로 가져온다.
	* `$ git cherry-pick <커밋id>`
	* `$ git cherry-pick b989e0f` : 복사하고 싶은 브랜치의 커밋 id
* Log
	* 기본적으로 log가 아니라 식별자 알아보기
	* `$ git log --decorate` 태그 정보를 포함한 이력을 확인
	* -1 이나 -2의 옵션을 출력 로그의 갯수를 지정할 수 있음
* Reflog
	* HEAD의 이동 내역
* Clean
	* 관리대상이 아닌 파일 삭제
* Tip
	* `$ git reset --hard HEAD~` : commit 취소

## Git 명령어  정리

* 설치와 설정
	* `git config`
		* (Git 최초 설정)[https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%B5%9C%EC%B4%88-%EC%84%A4%EC%A0%95#_first_time]
		* Git을 처음 사용할 때 이름, 이메일 주소, 터미널 색깔, 편집기 등을 설정한다.
	* `git help`
		* 도움말 보기
		* `git help <command>`
			* 해당 명령어에 어떤 옵션이 있고 어떻게 사용하는 지 알려줌
* 프로젝트 가져오기와 생성하기
	* `git init`
		* 현재 디렉토리에 Git 저장소를 생성하고 프로젝트를 버전 관리 할 수 있게 한다.
	* `git clone <저장소주소>`
		* 원격 저장소를 복제하여 저장소를 생성한다.
* 스냅샷 다루기
	* `git add`
		* 디렉토리에서 스테이징 영역(Index)로 컨텐츠를 추가한다. (git commit 명령은 오로지 스테이징 영역만 바라보기 때문에 git add로 추가해줘야한다.)
		* `git add <파일명>`
		* `git add .` or `git add -A` : 모든 파일을 add 한다.
	* `git status`
		* 워킹 디렉토리와 스테이징 영역의 상태를 보여준다.
		* Staging Area 에 파일을 넣고 꺼내는 방법에 대한 힌트도 제공
	* `git diff`
		* 워킹 디렉토리와 스테이징 영역의 차이점을 보여줌
			* `git diff` 명령은 Unstaged 상태인 것들 만 보여줌. 수정한 파일을 모두 스테이징 영역에 넣었다면 `git diff` 명령은 아무것도 출력하지 않는다.
		* `git diff --staged`
			* 커밋하려고 스테이징영역에 넣은 파일의 변경부분을 보여줌(저장소에 커밋한 것과 스테이징영역에 있는 것을 비교)
			* `--cached` 와 같은 옵션
		* `git diff HEAD` : 저장소, 스테이징 영역, 워킹 디렉토리의 차이점을 모두 볼수 있음 (??????????????????????????)
	* `git difftool`
		* 두 트리를 비교하고 싶을 때 사용
		* 외부 diff 도구를 실행함. (git 에 들어있는 기능을 사용하는 것)
	* `git commit`
		* `git add`로 스테이징 영역에 넣은 모든 파일을 커밋한다.
		* 하나의 스냅샷으로 기록
		* `git commit -m"커밋메시지"`
			* 커밋과 커밋메세지를 동시에 처리한다.
		* `git commit -C HEAD -a --amend`
			* 지정한 커밋의 로그 메시지를 다시 사용하여 기존 커밋을 수정한다.
			* -c를 사용하면 기존메시지를 수정할 수 있는 편집기를 실행해 준다.
	* `git reset`
		* 되돌리기 명령
		* `git reset <커밋명>` : 이전 커밋을 수정하기 위해서 사용
		* `git add`로 추가한 파일을 Unstage 하는데 사용
	* `git rm`
		* 스테이징영역이나 워킹디렉토리에 있는 파일을 삭제함
	* `git mv`
		* 파일을 옮기고(이름을 변경하고) 나서 새파일에 `git add` 명령을 실행하고 이전 파일에는 `git rm`을 실행시켜주는 명령임
	* `git clean`
		* 워킹디렉토리에서 필요없는 파일을 삭제한다.
* Branch와 Merge
	* `git branch`
		* 현재 존재하는 브랜치 조회
		* `-r` 옵션을 사용하면 원격저장소의 브랜치를 확인할 수 있음
	* `git branch <브랜치명>`
		* 새로운 브랜치를 만든다.(체크아웃은 하지 않는다)
	* `git branch <브랜치명B> <브랜치명A>`
		* 브랜치명A에서 새로운 브랜치B를 만든다.(git에서 기본 브랜치는 master라는 이름을 사용한다.)
	* `git branch -d <브랜치명>`
		* 브랜치를 삭제한다.
	* `git branch -m <존재하는브랜치명> <새로운브랜치명>`
		* 존재하는 브랜치를 새로운 브랜치로 변경한다. 이미 존재하는 브랜치명이 있을 경우 에러가 나는데 -m 옵션을 사용하면 이미 있는 브랜치의 경우에도 덮어쓴다.
	* `git checkout <브랜치명> / <태그명>`
		* 해당 브랜치나 태그로 작업트리를 변경한다.
	* `git checkout -b <브랜치명>`
		* 새로운 브랜치명을 만들면서 체크아웃을 한다.
	* `git checkout --<파일명>`
		* 아직 스테이징이나 커밋을 하지 않은 파일의 변경내용을 취소하고 이전 커밋상태로 되돌린다.
	* `git merge <브랜치A>`
		* 브랜치A를 현재 체크아웃된 브랜치에 merge 한다.
	* `git mergetool`
		* 외부 Merge Helper를 실행해 준다. Merge 하다가 문제가 생겼을 때 사용한다.
	* `git log`
		* 프로젝트 히스트리를 시간의 역순으로 보여준다.
		* `--pretty', `--oneline` 옵션을 주면 히스토리를 깔끔하게 볼 수 있음
			* `--pretty=format` format 에는 %H, %h, %T 등 여러가지 옵션이 있다.
		* `--decorate` 옵션을 사용하면 브랜치가 어떤 커밋을 가리키는지 확인할 수 있다.
		* `--graph` 옵션을 사용하면 히스토리가 어떻게 진행됬는지 볼 수 있음
	* `git stash`
		* 아직 커밋하지 않은 일을 저장하는 데 사용
	* `git tag`
		* 현재 존재하는 태그 목록 확인
	* `git tag <태그명> <브랜치명>`
		* 브랜치명의 현재 시점에 태그명으로 된 태그를 붙힌다.
* 공유하고 업데이트하기
	* `git fetch`
		* 로컬 데이터베이스에 있는 것을 뺀 리모트 저장소의 모든 것을 가져옴
	* `git pull`
		* `git fetch` 와 `git merge` 명령을 순서대로 실행하는 것
	* `git push`
		* 리모트에는 없지만, 로컬에는 있는 커밋을 계산하고 나서 차이만큼 Push한다.
		* 파라메터를 주지 않으면  origin 저장소에 Push
		* `--dry-run` 옵션을 사용하면 푸싱된 변경사항을 확인 가능
		* 로컬에서 Tag를 달았을 경우 기본적으로 푸싱하지 않기 때문에 `git push origin <태그명>` 이나 모든 태그를 올리기 위해서 `git push origin --tags`를 사용해야 한다.
	* `git remote`
		* 원격 저장소 설정인 리모트의 관리도구다.
		* 원격 저장소의 목록을 확인할 수 있다
		* 긴 URL 대신 'origin' 처럼 이름을 짧게 지을 수 있다.
	* `git remote add <이름> <저장소주소>`
		* 새로운 원격 저장소를 추가한다.
		* `git remote add origin https://meg~~~`
	* `git remote show <이름>`
		* 해당 원격 저장소의 정보를 볼 수 있다.
	* `git remote rm <이름>`
		* 원격 저장소를 제거 한다.
	* `git archive`
		* 프로젝트 스냅샷을 아카이브 파일로 만들어 줌.
		* `git archive --format=tar --prefix=폴더명/ 브랜치혹은태그 | gzip > 파일명.tar.gz`
		*`git archive --format=zip --prefix=폴더명/ 브랜치혹은태그 > 파일명.zip`
	* `git submodule`
		* 연관된 하위 모듈을 확인 할 수 있다.
* 보기와 비교
	* `git show`
		* 태그나 커밋정보를 보여준다.
	* `git shortlog`
		* `git log` 명령의 결과를 요약해서 보여준다.
		* Author 별로 커밋을 묶어서 보여줌
	* `git describe`
		* 커밋과 관련된 정보를 잘 조합해서 사람이 읽을 수 있는 문자로 결과를 만든다.
* Debugging
	* `git bisect`
		* 이진 탐색 알고리즘을 사용해서 버그나 문제가 생긴 커밋을 쉽게 찾을 수 있음
	* `git blame`
		* `git blame <파일명>`
			* 파일의 각 라인을 누가 마지막으로 수정했는지 보여줌
			* 특정 코드에 대해 궁금한 게 있을 때 누구에게 물어야 할지 바로 알 수 있음
		* `git blame -L 10,15 <파일명>
			* 줄 범위를 지정해서 볼 수 있고, 15 대신 +5와 같이 사용할 수 있다.
		* `git balme -M <파일명>
			* -M 옵션을 사용하면 반복되는 패턴을 찾아서 복사하거나 이동된 내용을  찾아준다.
	* `git grep`
		* 소스 코드에서 스트링이나 정규 표현식을 찾을 수 있음(??????????)
* Patch 하기
	* `git cherry-pick`
		* 커밋하나만 가져올 때 사용
		* 현 브랜치의 새 커밋으로 적용
		* `$ git cherry-pick <커밋id>`
		* `$ git cherry-pick b989e0f` : 복사하고 싶은 브랜치의 커밋 id
	* `git rebase`
		* `git rebase <브랜치명>`
			* 브랜치명의 변경사항을 현재 브랜치에 적용
		* `git rebase -i <커밋범위>`
			* -i 옵션으로 대화형 모드로 커밋 순서를 변경하거나 합치는 등의 작업을 할 수 있다.
	* `git revert`
		* `git revert <커밋명>`
			* 기존의 커밋에서 변경한 내용을 취소해서 새로운 커밋을 만든다.

## 참고 사이트

* [누구나 쉽게 이해할 수 있는 Git 입문](https://backlogtool.com/git-guide/kr/)
* [Git Book](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%9E%80%3F)