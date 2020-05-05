---
layout: post
title:  "AndroidのStorage Access Frameworkを使ったサンプル"
date:   2020-05-05 21:00 +0900
categories: "Java Android"
---
# はじめに
AndroidでUSBメモリに格納したファイルを開くにはどの手段を使うのが正解かを調べた結果、[Storage Access Framework(SAF)](https://developer.android.com/guide/topics/providers/document-provider?hl=JA)を使うのが正解との結論に達したので、サンプルコードを書いて確認しました。

# 背景
お仕事関係でAndroidプログラムを作る必要が発生しました。  
要件の一つにUSBメモリに格納したファイルを開く必要があったので、その方法を調べました。  
Androidのストレージ周りは複雑怪奇・・・。  
内蔵フラッシュでも、外付けストレージ扱いになったりしているのは知っていたけれども、予想以上の複雑さ。

私が調べた限りでは、USBメモリのファイルにアクセスする確実な方法は[SAF](https://developer.android.com/guide/topics/providers/document-provider?hl=JA)しかありませんでした。  
Androidのバージョンアップの度にUSBメモリへのアクセス方法が塞がれているようなので、[SAF](https://developer.android.com/guide/topics/providers/document-provider?hl=JA)を使うべきです。

# サンプルコードのリポジトリ
[githubのリポジトリ](https://github.com/mfujibayashi/AndroidSAFsample)

# サンプルコードの簡単な説明
SAFはMIME Typeでフィルターできます。  
そこで、"Music Open"ボタンと"Image Open"ボタンを用意し、"Music Open"ボタンをタップしたときは`audio/*, video/*`でフィルター、"Image Open"ボタンをタップしたときは`image/*`でフィルターするようにしています。  
コードそのものは、Googleのドキュメントの内容そのままです。

"Music Open"の選択結果をVideo Viewで再生させています。  
また、"Image Open"の選択結果をImage Viewで表示させています。

# AndroidのUI
Video View, Audio Viewの表示切り替えにFragmentを使っています。  
が、あまり理解せずに実装したので、おかしなコードになっている可能性もあります。

# 最後に
AndroidのUI回りと言うか、基礎の部分を理解するためにお薦めの本やWebページはありませんかね。
