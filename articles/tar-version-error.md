---
title: "npm WARN deprecated tar@2.2.2: This version of tar is no longer supported, and will not receive security updates. Please upgrade asap.というエラーの解決法"
emoji: "🐱"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["React.js"]
published: true
---

'''
$ npm i -g create-react-app 
'''
というコマンドを打つと以下のエラーが起きる場合がある。

'''
npm WARN deprecated tar@2.2.2: This version of tar is no longer supported, and will not receive security updates. Please upgrade asap.

changed 67 packages, and audited 68 packages in 703ms

4 packages are looking for funding
  run `npm fund` for details

2 high severity vulnerabilities

Some issues need review, and may require choosing
a different dependency.

Run `npm audit` for details.
'''

これは、
'''
npm i tar      
'''
というコマンドを打つと解決できる。