---
title: "System dependencies"
date: 2022-02-15T11:02:05+06:00
lastmod: 2022-02-15T11:02:05+06:00
weight: 2
draft: false
# search related keywords
keywords: ["setup", "configuration", "requirements"]
---

Self SDK depends on some native libraries to manage encryption [libself_olm](github.com/joinself/olm) and [libself_omemo](github.com/joinself/omemo). Below you'll find the instructions to get them working on your system.

#### Debian/Ubuntu
```
$ curl -O https://download.joinself.com/olm/libself-olm_0.1.17_amd64.deb
$ curl -O https://download.joinself.com/omemo/libself-omemo_0.1.2_amd64.deb
$ apt install libsodium-dev
$ apt install ./libself-olm_0.1.17_amd64.deb ./libself-omemo_0.1.2_amd64.deb
```

#### Redhat/Centos
```
$ rpm -Uvh https://download.joinself.com/olm/libself-olm-0.1.14-1.x86_64.rpm
$ rpm -Uvh https://download.joinself.com/omemo/libself-omemo-0.1.2-1.x86_64.rpm
```

#### Mac (x86_64)

```
$ brew tap joinself/crypto
$ brew install libself-olm libself-omemo
```

#### Mac (m1/arm64)
Brew on M1 macs currently lacks environment variables needed for the sdk to find the `olm` and `omemo` libraries, so you will need to add some additional configuration to your system:

In your `~/.zshrc`, add:
```
export C_INCLUDE_PATH=/opt/homebrew/include/
export LIBRARY_PATH=$LIBRARY_PATH:/opt/homebrew/lib
```

You should then be able to run:
```
$ source ~/.zshrc
$ brew tap joinself/crypto
$ brew install --build-from-source libself-olm libself-omemo
```

Note, you may also need to create `/usr/local/lib` if it does not exist:
```
$ sudo mkdir /usr/local/lib
```
