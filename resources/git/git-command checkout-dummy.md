
https://www.freecodecamp.org/korean/news/git-cekeuause-daehan-seolmyeong-giteseo-beuraencireul-cekeuaus-byeongyeong-ddoneun-jeonhwan-haneun-bangbeob/

**Original article:** [Git Checkout Explained: How to Checkout, Change, or Switch a Branch in Git](https://www.freecodecamp.org/news/git-checkout-explained/)

> `git checkout` 명령어는 브랜치 간 전환 또는 현재 작업 중인 파일들을 복원할 때 사용됩니다. 이 명령에는 여러 가지 옵션이 있지만 이 글에서 다루지 않을 것이며, [git 문서](https://git-scm.com/docs/git-checkout)에서 모든 옵션을 확인할 수 있습니다.

## 특정 커밋으로 체크아웃하는 방법

특정 커밋으로 이동하려면 다음 명령어를 실행하세요.

```bash
git checkout specific-commit-id
```

특정 커밋 ID는 다음 명령을 실행하여 확인할 수 있습니다.

```bash
git log
```

## 기존 브랜치로 체크아웃하는 방법

기존 브랜치로 이동하려면 다음 명령을 실행하세요.

```bash
git checkout BRANCH-NAME
```

보통 Git을 사용할 때, 작업하고 있던 디렉토리에서 커밋되지 않은 변경 사항이 있는 경우 다른 브랜치로 이동할 수 없습니다. 이는 커밋되지 않은 파일들이 손실되기 때문입니다. 이 경우 변경 사항을 처리하기 위해서는 1. 삭제하거나, 2. 커밋하거나, 3. 스태시(Stash: 아직 커밋하지 않은 변경 사항들을 임시로 저장하는 Git의 기능 —옮긴이)해야 합니다.

## 새로운 브랜치로 체크아웃하는 방법

새로운 브랜치 생성과 동시에 해당 브랜치로 이동하는 명령어를 실행하려면 다음과 같이 입력합니다.

```bash
git checkout -b NEW-BRANCH-NAME
```

이 명령어를 실행하면 바로 새로운 브랜치로 전환됩니다.

## 새로운 브랜치로 체크아웃하거나 브랜치를 시작점으로 재설정하는 방법

다음 명령은 새 브랜치를 만드는 것과 유사하지만 `-B` (대문자 B에 주목) 플래그와 선택적인 `START-POINT` 매개변수를 사용합니다.

```bash
git checkout -B BRANCH-NAME START-POINT
```

만약 `BRANCH-NAME`이라는 브랜치가 존재하지 않으면, Git은 `START-POINT`에서 브랜치를 만들고 시작합니다. 만약 `BRANCH-NAME`이라는 브랜치가 이미 존재한다면, Git은 브랜치를 `START-POINT`로 재설정합니다. 이것은 `-f` (force의 약자. 강제로 실행하는 명령어 — 옮긴이) 옵션을 사용하여 `git branch`를 실행하는 것과 동일합니다.

# 체크아웃을 강제로 실행하기

작업 디렉토리의 인덱스가 `HEAD`와 다르면 (즉, 스테이징하지 않은 변경 사항이 있으면), `git checkout` 명령에 `-f` 또는 `--force` 옵션을 전달하여 Git이 브랜치를 전환하도록 강제할 수 있습니다. 기본적으로, 이는 로컬 변경 사항을 삭제하는 데 사용될 수 있습니다.

다음 명령을 실행하면 Git은 병합되지 않은 항목을 무시합니다.

```bash
git checkout -f BRANCH-NAME

# Alternative
git checkout --force BRANCH-NAME
```

# 작업 디렉토리에서 변경 내용 되돌리기

`git checkout` 명령을 사용하여 작업 디렉토리에서 파일을 변경한 내용을 되돌릴 수 있습니다. 이는 파일을 `HEAD`의 버전으로 되돌립니다.

```bash
git checkout -- FILE-NAME
```