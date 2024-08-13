


https://flower0.tistory.com/310

push 까지?

``` bash
git checkout -t <remote>/<branch>

git branch --set-upstream-to=origin/<remote branch> <local branch>

git push origin HEAD:refs/for/<branch name>

```


### 문제상황
로컬로 초기화 할때 remote repo 와 local 이 master로 되어 있어
remote 메인브랜치를 "main" 으로 바꾸고 local도 "main" 으로 바꾸어 push 했지만
이미 origin/master로 트래킹 시켜놓아 바꿔줘야하는 상황