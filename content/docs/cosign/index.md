---
title: 'Cosign and CHERI Linux'
date: 2023-04-25T15:14:39+10:00
weight: 10
---

CHERI Linux generated containers are signed using [cosign](https://github.com/sigstore/cosign).  

<!--more-->

To verify the validity of a container before downloading it you can use the commands below:
```
$ cosign verify --key cosign.pub _IMAGE_URI_

Verification for _IMAGE_URI_ --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - The signatures were verified against the specified public key
  - Any certificates were verified against the Fulcio roots.
[{"critical":{"identity":{"docker-reference":"_IMAGE_URI_"},"image":{"docker-manifest-digest":"sha256:e50b98871186ad76bc03cfd380d6c7cd3343cf28b15c836100c09d874462d505"},"type":"cosign container image signature"},"optional":null}]
```
The public key [cosign.pub](cosign.pub) can be retrieved from the same directory of this README.md file.
