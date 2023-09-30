### action이란?

actions 안에 들어가면 list가 나오게 되는데, CI라고 적힌 것이 글쓴이가 만든 action이다.
사용자가 push와 같은 작업을 했을 때, 컴퓨터가 새로 생성되고,
생성된 컴퓨터에서 업무일지를 작성하는 서비스인 air table이라는 서비스로 자동으로 작업을 적어주는 action이다.

git commit -am "add multiply 1h"
git push
로 업로드 시작이 되면
Actions를 리로드하면 커밋이 등록되어있고 지금 구동중이라는 것이 화면에 보인다.
작업이 끝나게 되면 커밋한 내용이 깃허브액션의 runner라는 가상머신에서 구동되서 누가 작업했고, 어떤 작업이었고, 몇시간 일했고 그 업무는 어떤 내용에 대한 것인지 커밋과 
그것에 대한 근거자료에 대한 깃허브 링크가 자동으로 업로드 되는 것을 볼 수 있다.

업무에 방해가 되지 않게 개발자들이 하는 일에 대한 업무를 추적하는데 굉장히 큰 도움을 받을 수 있다.

### 어떻게 action을 사용하는 가

Create a new reposiotory
action-tutorials : Repository name
Public


Actions 탭으로 들어가면 깃허브에서 제공하는 미리 만들어진 템플릿 action들을 선택할 수 있다.
Set up a workflow yourself

action-tutorials/.github/workflows/main.yml : action의 실체이다.

```
name : Hello World :action name"

on : [push] "사용자가 commit했을 때 및의 코드들이 실행이 된다" "[push, pull_request]"

jobs:
  build:

    runs-on: ubuntu-latest "action이 실행됬을 때 구분되는 컴퓨터가 ubuntu였으면 좋겠다"

    steps:
    #- uses: actions/checkout@v2 "#은 해당 줄이 구동되지 않게 주석처리"
    - name: Run pwd "우분투 - 현재 사용위치 알려주는 명령어 run에 대한 step의 이름"
      run: pwd
    - name: Run ls -al
      run: ls-al

```

start commit을 누르면 Create main.yml이 만들어짐
Commit new file

저장소 안에
.github/workflows 폴더 안에 main.yml 파일이 위치하게 된다.

yml이라는 확장자를 가지고 있는 설정파일을 만드는 작업을 한 것

Clone or download : git clone해서 저장소 복제 한 후 폴더 안에 들어가보면 파일 안에 파일들이 생성된 것을 확인할 수 있다.

<버전 수정 후 commit, push 해 보기>

vim main.html
```
<html>
    <body>hi</body>
</html>
</html>
```
git commit -am "hi"
git push

Actions에서 일어나는 일

```
Run pwd "step에서"
/home/runner/work/action-tutorials/action-tutorials  "이런 디렉토리 구조를 가지는 컴퓨터를 우리에게 빌려주었다는 뜻"
```

push, pull request, issue작성 여러가지 사건들이 일어났을 때 github에게 우리가 컴퓨터를 빌려서 자동으로 처리할 수 있다는 것을 보여준다.

Run ls-al 은 아무것도 없는 깡통 컴퓨터

### github가 runner를 빌려줄 때 컴퓨터 안에 action이 실행한 저장소의 github 소스코드가 체크아웃이 되게 하는 방법
New workflow 클릭
Set up a workflow yourself 클릭
github-checkout.yml

```
name: github checkout

on: [push]

jobs:
  build:

  runs-on: ubuntu-latest

  steps:
  - uses: actions/chekcout@v2 "주석처리 해제"

```
