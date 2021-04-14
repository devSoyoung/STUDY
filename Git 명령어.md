# Git 명령어 정리

### Branch 생성 & 체크아웃

```bash
$ git branch feature/name && git checkout feature/name
```
- **체크아웃** : 선택한 브랜치로 전환하는 것

#### 체크아웃의 또 다른 기능 - 수정한 파일 되돌리기

```bash
$ git checkout -- [원상복구할 파일]
```

VSCode의 SOURCE CONTROL 메뉴에서  
변경된 파일의 <kbd>되돌리기</kbd>(Discard Changes) 버튼이 수행하는 것과 같음

폴더 - 폴더 안에 들어있는 파일은 path를 쓰기가 번거로우니까  
VSCode의 경우 **Copy Relative Path**로 path를 복사하고 입력하면 됨  
(사실 그냥 되돌리기 버튼 누르는게 제일 나음ㅎㅎ)

### Branch 이름 수정하기
```bash
$ git branch -m [기존 브랜치명] [변경할 브랜치명]
```

### Branch 삭제하기
```bash
$ git branch -d [삭제할 브랜치 이름]
$ git branch --delete [삭제할 브랜치 이름]
```
작업 내역이 남아있는(master에 머지 안 된) 경우, 위 방법으로 삭제 안된다면 강제 삭제 할 수 있다.

```bash
$ git branch -D [삭제할 브랜치 이름]
```

### 변경 내역을 Stage 하기
수정된 파일을 `staged` 상태로 만드는 것은, 커밋을 했을 때 커밋 내역에 해당 파일의 수정을 포함하겠다는 것이다.
```bash
$ git add [파일 이름]
```

모든 수정된 파일을 한 번에 `stage`하고 싶을 때
```bash
$ git add .
```

### Staged 내역을 커밋하기
```bash
$ git commit -m "커밋 메세지"
```
커밋 메세지를 예시와 같이 쓰지 맙시다 🙊

> 커밋 메세지 작성 : https://www.conventionalcommits.org/en/v1.0.0/

#### 로컬 브랜치의 삭제한 내역을 원격 브랜치에 반영하고 싶을 때
```bash
$ git push origin :[삭제한 브랜치 이름]
```

### 바로 이전 커밋 내역 수정하기
수정할 파일을 `git add`로 인덱스에 추가한 다음
```bash
$ git commit --amend
```

커밋 메세지 수정하는 화면이 뜨면 `i`로 수정모드에 진입해 수정하고 `ESC`, `:wq`로 저장 후 종료하면 최근 커밋 내역이 수정된다.

### 이전 커밋 내역 수정하기
```bash
$ git rebase -i HEAD~[돌아갈 커밋의 위치]
```

- **돌아갈 커밋의 위치** = HEAD로부터 몇개나 떨어졌는지  
  ex) `git rebase -i HEAD~3` > 최신 3개의 커밋을 수정할 수 있다.

```
pick 04ac327 첫 번째 커밋
pick eac0fc5 두 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
```

다음과 같이 커밋 목록이 출력되면 수정할 커밋의 `pick` > `e`로 변경하고 저장한다.

```diff
- pick 04ac327 첫 번째 커밋
+ e 04ac327 첫 번째 커밋
```

수정한 내역을 add하고, rebase를 `--continue`해서 종료한다.

```bash
$ git add .
$ git rebase --continue
```

> ⚠️ 이 때 수정한 내역과 이후 작업 내역에 충돌이 있으면 resolve 한 후 `git rebase --continue`를 다시 실행하면 된다.

### 커밋 합치기 🍻
> 맥주 이모지는 술잔을 합치는 것을 표현한 나름의 센스임;

```bash
$ git rebase -i HEAD~3

pick 04ac327 첫 번째 커밋
pick eac0fc5 두 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
```

> 예시로 자꾸 3개만 표시하지만, 합칠 커밋까지 띄워야 할 것..

첫 번째 커밋과 두 번째 커밋을 합치고 싶으면 두 번째 커밋의 `pick` > `s`로 수정하고 저장한다.

#### (응용) 떨어져있는 두 커밋 합치기
> 이게 참 간단한건데, 첨엔 방법을 몰라 눈물을 흘렸따.. 

```bash
$ git rebase -i HEAD~3

pick 04ac327 첫 번째 커밋
pick eac0fc5 두 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
```

여기에서 첫 번째 커밋과 세 번째 커밋을 합치려면, 먼저 순서를 바꾼다 👀

```
pick 04ac327 첫 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
pick eac0fc5 두 번째 커밋
```
> vi에서 수정하기 좀 불편; 고급 vi 스킬 알려줄 스승님 찾아요

이렇게 순서를 바꾼 다음에 합쳐줄 커밋의 `pick`을 `s`로 바꾼다 _(초간단)_

### 커밋 순서 바꾸기
> 바로 위에서 한 내용이라 아주 날로 먹는 느낌이지만

```bash
$ git rebase -i HEAD~3

pick 04ac327 첫 번째 커밋
pick eac0fc5 두 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
```
여기에서 그냥 줄을 통째로 바꿔주면 된다.

```
pick 04ac327 첫 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
pick eac0fc5 두 번째 커밋
```

### 커밋 삭제하기 
```bash
$ git rebase -i HEAD~3

pick 04ac327 첫 번째 커밋
pick eac0fc5 두 번째 커밋
pick c17ec0f 세 번째 커밋 (=제일 최신 커밋)
```

여기에서 두 번째 커밋을 지우려면

```diff
- pick eac0fc5 두 번째 커밋
+ d eac0fc5 두 번째 커밋
```

삭제할 커밋의 `pick` > `d`로 수정한다.
