### Introduction

GIT을 사용중에 SSH 관리 및 동작과 관련해서 궁금증이 생겼습니다.
각 케이스 별로 구분하여 테스트를 진행하면서 GIT에서 SSH를 활용에 대하여 이해도를 높여 보겠습니다.

#### Initial Settings

1. Github A계정의 SSH를 사용중인 PC에서 생성합니다. (A PC(Mac)에서Github A 계정(kshyeon123@gmail.com)의 키를 생성)

2. Github에 Commit을 보낼 프로젝트를 생성합니다.

3. Local 에서 위에 생성된 Remote 프로젝트로 Commit을 보냅니다.

#### TEST Case

- CASE 1 : 아무런 Key를 갖지 않고 Remote에 Push하는 경우 아래와 같은 Permission Denied 에러가 발생합니다.

```
ERROR: Permission to ksheyon123/test__for__git.git denied to shkang124.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

이후, SSH 키를 B계정 (shkang124@coinplug.com)에 추가하면 커밋이 성공합니다.

> 의문점 1: A PC에서 A 및 B 계정 모두 SSH를 등록하지 않으면 Commit을 쏠 수 없었다. 그렇다면 WEMIX.FI에는 B계정에서 어떻게 Commit을 쏠 수 있을까? (WEMIX.FI 프로젝트에 B 계정이 Collaborator 로 등록되어 있고 Home의 .gitconfig 계정은 shkang@coninplug.com)

- CASE 2 : Github 계정이 아니라 Mac의 Public 키를 등록한 경우

**성공! 그리고, SSH-ADD 를 통해서 SSH-AGENT에 해당 키를 등록을 해주어야한다.**

다만, 여전히 SSH에 Public Key를 등록하지 않으면 Commit을 보낼 수가 없다.

- CASE 3 : 한 PC 에서 여러 계정에 Commit

이 방식은 결국 CASE 1, 2 과정으로 해결이 된다. A PC에서 각 계정 별로 사용할 Public키를 생성하고 각 계정의 SSH 탭에 등록하면 된다.

- CASE 4 : 한 계정에 여러 PC에서 Commit
