---
title: "[Git] Some errors.."
author: ramraid
date: 2024-10-07 20:00:00 +0800
categories: [Version Control, Git]
tags: [Version Control, Git]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

# Git 오류와 해결법

### err 8

```text
error: RPC failed; curl 92 HTTP/2 stream 0 was not closed cleanly: CANCEL (err 8)
```

HTTP/2의 오류.
HTTP/1.1 로 변경한다.

```text
git config --global http.version HTTP/1.1
```

### GnuTLS recv error (-9)

```text
error: RPC failed; curl 56 GnuTLS recv error (-9): Error decoding the received TLS packet.
error: 3785 bytes of body are still expected
fetch-pack: unexpected disconnect while reading sideband packet
fatal: early EOF
fatal: fetch-pack: invalid index-pack output
```

파일 크기가 postBuffer보다 큰 경우
버퍼 크기를 늘린다.

```text
git config --global http.postBuffer 1048576000
```

### ssh: connect to host gmail.com port 22: Network is unreachable

```text
ssh: connect to host gmail.com port 22: Network is unreachable
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

ssh clone을 시도하는데, public ssh key를 가지지 않을 때
새 public key를 발급받거나 http로 클론 시도