---
title: "Bad configuration option: ssh-rasa..."
emoji: "ð±"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["ssh"]
published: true
---

GitHubã¨ã®sshæ¥ç¶ãã§ãã¦ãããç¢ºèªããããã®ã³ãã³ã
```shell
$ ssh -T git@github.com
```
ãæã¤ã¨ä»¥ä¸ã®ã¨ã©ã¼ãèµ·ããå ´åãããã

```shell
/Users/yoshikitanaka/.ssh/config: line1: Bad configuration option: ssh-rsa
/Users/yoshikitanaka/.ssh/config: terminating, 1 bad configuration options
```

ä»åã®å ´åã¯éµã®è¨­å®ãããã°è§£æ±ºãããã ã£ãã®ã§ãéµã®è¨­å®æ¹æ³ã2éãç´¹ä»ããã

## 1.~/.ssh/configã«éµã¸ã®PATHãè¨­å®

ããã¯~/.ssh/configï¼ãã¼ã ãã£ã¬ã¯ããªã«ãã.sshãã£ã¬ã¯ããªã®configãã¡ã¤ã«ï¼ã«ä»¥ä¸ã®1è¡ãè¿½å ããæ¹æ³ã§ããã
```shell
IdentityFile éµã¸ã®PATHï¼ä¾ï¼~/.ssh/id_rsaï¼
```
## 2.ã³ãã³ãã§ç´æ¥éµã¸ã®PATHãæå®

ããã¯ä»¥ä¸ã®ã¿ã¼ããã«ä¸ã§ä»¥ä¸ã®ã³ãã³ããå¥åãã¦ç´æ¥éµãæå®ããæ¹æ³ã§ããã
```shell
$ ssh-add éµã¸ã®PATHï¼ä¾ï¼~/.ssh/id_rsa ï¼
```

### ã¾ã¨ã
ä»å¾ã®ãããèããã¨1ã¤ç®ã®æ¹æ³ãé¸ãã§ã~/.ssh/configã®ä½¿ãæ¹ã«æ£ããæ¹ãè¯ãããã
ä»¥ä¸ã«åèã«ãªããããªè¨äºãè¼ãã¦ããã
- https://qiita.com/passol78/items/2ad123e39efeb1a5286b
- https://web.kudpc.kyoto-u.ac.jp/manual/ja/install/ssh-add