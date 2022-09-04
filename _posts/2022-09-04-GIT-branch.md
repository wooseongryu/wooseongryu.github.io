---
title: "Git"
excerpt: ""

categories:
    - Git
tags:
    - [Git]

toc: true
toc_sticky: true

comments:
  provider: "utterances"
  utterances:
    theme: "github-light" # "github-dark"
    issue_term: "pathname"
    label: "comment" # Optional - must be existing label.

date: 2022-09-04
last_modified_at: 2022-09-04
---
# branch
하나의 코드 관리 흐름을 말한다.    
## branch 명령어
- 브랜치 생성  
git branch [브랜치이름]   
- 브랜치 이동  
git checkout [브랜치이름]  
- 브랜치 조회
git branch
- 브랜치 삭제
git branch -d [브랜치이름]
- 브랜치를 만들면서 해당 브랜치로 이동  
git checkout -b [브랜치이름]

## merge
git merge [현재위치의 브랜치와 합칠 브랜치이름]
### conflict
병합시 두 브랜치의 내용이 달라 충돌이 생길 때는 충돌이 발생한 파일을 열어 병합의 결과가 되었으면 하는 모습대로 코드를 수정하고 다시 커밋을 하면 된다.  
또는 merge를 취소해도 되는데 git merge --abort를 쓰면 된다.  
여러 개의 파일에서 충돌이 나면 하나씩 충돌을 해결해주면 된다.  

## 새로 생성된 브랜치 push
브랜치를 새로 생성하고 나면 tracking connection이 되어있지 않다.  
그래서 추적 관계를 설정해주고 난 뒤에 푸쉬해주면 된다.  

## HEAD와 브랜치의 관계
HEAD -> master -> 커밋
브랜치는 커밋을 가리키고 HEAD는 브랜치를 통해 간접적으로 커밋을 가리킨다.  
merge란 HEAD가 가리키던 커밋에 다른 브랜치가 가리키던 커밋을 합쳐서 새로운 커밋을 만드는 작업이다.  
## git reset과 git checkout 차이
git reset은 헤드가 가리키던 브랜치가 다른 커밋을 가리키도록 한다. 헤드도 결국 간접적으로 다른 커밋을 가리키게되는 효과가 생긴다.  
git checkout은 헤드 자체가 다른 커밋이나 브랜치를 가리키도록 한다. 브랜치를 통하지 않고, 커밋을 직접적으로 가리키는 헤드를 Detached HEAD라고 한다.  
## Fast-forward
한 브랜치 안에서 앞 단계의 커밋으로 머지를 하게 되면 새로운 커밋이 생기는 게 아니라 그냥 브랜치가 이동하게 되는데 이것을 Fast-forward라고 한다.  
한 브랜치에서 갈라져 두 브랜치가 각각 존재할때 머지를 하면 커밋이 새로 생기게 된다. 이런 머지를 3-way-merge라고 한다.   
3-way-merge에서는 근본이되는 브랜치에서 변화가 발생한 것을 우선 채택하여 머지된다. a브랜치에서 갈라진 b, c브랜치가 있을때 b브랜치에만 변경사항이 생기면 b브랜치의 내용으로 머지된다. 만약 b,c브랜치가 모두 변경사항이 생기면 머지시에 충돌이 생기게되고 사용자가 직접 수정을 해야한다.  

# git 협업
## 깃 푸쉬 전에 깃 풀
리모트의 내용과 로컬의 내용이 다르면 푸쉬가 되지 않는다.  
이럴때는 풀을 먼저 해준다. 깃 풀은 리모트에서 가져와서 로컬에 머지하는 과정이다.  
그래서 로컬과 리모트의 최신 내용이 다르면 충돌이 생기는데 해결해 주면 된다.  
그 후에 애드, 커밋 하면 된다.  

## fetch
fetch는 머지를 하지 않고 가져오기만 한다. 리모트 레포지토리에서 가져온 브랜치의 내용을 머지하기 전에 점검해야할 필요가 있을 때 사용한다. 또는 리모트 레포지토리에 브랜치 내용과 내가 작성한 코드를 비교해서 잘못된 부분이 없는지 검토해야 할 때도 사용한다.  
fetch로 가져오고 나서 git diff로 차이를 확인한다. git diff는 커밋 뿐만 아니라 브랜치간의 차이도 볼 수 있다.  

## git blame
어떤 파일의 특정 코드를 누가 작성했는지 찾아내기 위한 커맨드이다.  
git blame 파일이름  
git show 커밋아이디 를 하면 누가 작성했는지 알 수 있다.  

## git revert
git revert 커밋아이디 를 하면 이미 리모트 레포지토리에 올라간 커밋을 취소할 수 있다.  
git reset대신 git revert를 쓰는 이유는 리셋을 하면 로컬 레포지토리의 이전 커밋으로 돌아가고 리모트 레포지토리의 리포지토리는 그대로 있으니 더 최신상태가 된다. 그러면 푸쉬를 바로 할 수 없고 풀을 하고 다시 푸쉬를 해야한다. 하지만 git revert를 하면 로컬 레포지토리에서 새로운 커밋을 생성하고 그 커밋에 이전 커밋의 모습을 복구해놓기 때문에 그대로 푸쉬할 수 가 있다.  

## 여러 커밋 취소하기
git revert 커밋아이디1..커밋아이디2  
커밋아이디1 다음부터 커밋아이디2까지를 되돌린다.  

# git reflog
깃 리셋을 한다고 그 이후의 커밋들이 사라지는 건 아니다.  
reflog(reference log)는 헤드가 이때까지 가리켜왔던 커밋들을 기록한 정보다.  
fit reflog로 커밋 아이디를 확인하고 git reset으로 돌아가면 된다.  

# git log 옵션
--all  
모든 브랜치를 보여준다.  
--graph  
커밋 히스토리가 각 브랜치와의 관계가 잘 드러나도록 그래프 형식으로 출력한다.  

# git rebase
커밋을 재배치한다. 두 브랜치가 갈라진 지점 이후부터 한 브랜치에서 했던 커밋들을 다른 브랜치의 최신 커밋 이후로 그대로 이어붙이는 모양의 커밋 히스토리를 만든다.  
git rebase를 하고 충돌이나면 해결을하고 git rebase --continue 를 써서
rebase에서 충돌이나서 진행되지못한 리베이스를 계속 진행한다.  
## merge와 rebase차이
rebase는 새로운 커밋을 만들지 않는다.  
rebase로 만들어진 커밋 히스토리가 더 깔끔하다.  
결과물의 차이는 없다.  
두 브랜치를 합쳤다는 정보가 커밋 히스토리에 남아야 한다면 merge를 쓰면된다.  

# git stash
커밋을 하지 않고 다른 브랜치로 가야하는 상황에 쓰인다.  
작업 내용을 임시 저장한다. working directory에서 작업하던 내용을 깃이 따로 보관해 준다. 그 장소를 stack이라 한다.  
git stash를 실행하면 최근 커밋 이후로 작업했던 내용은 모두 스택에 옮겨지고 working directory내부는 다시 최근 커밋의 상태로 초기화된다.  
git stash list로 확인할 수 있다.  
git stash apply로 다시 불러올 수 있다.  
스택에 테이터를 삭제하려면 git stash drop stash@{숫자} 를 하면 된다.  
apply대신 git stash pop을 쓰면 불러옴과 동시에 drop까지 동시에 적용이 된다.  
pop뒤에 인자를 주지 않으면 가장 최근 내용이 스택에서 제거된다.  
## 잘못된 브랜치에서 작업했을 때
해당 브랜치에서 git stash를하고 올바른 브랜치로 체크아웃한 후 그곳에서 다시 git stash apply stash@{숫자} 를 통해 불러올 수 있다.  

# git cherry-pick
자신이 원하는 작업이 들어있는 커밋들만 가져와서 현재 브랜치에 추가한다.  
git cherry-pick 커밋아이디  

# 여러 커밋을 하나의 커밋으로 만들기
없애고 싶은 커밋 이전으로 리셋을 하는데 mixed나 soft를 옵션으로 쓴다.  
HEAD는 이전 커밋을 가리키지만 working directory는 그대로기 때문에 필요없는 커밋없이 깔끔하게 만들 수 있다.  

# gitignore
.gitignore파일에 무시하고 싶은 파일의 이름을 추가하면 그 파일은 깃으로 관리가 되지 않는다.  