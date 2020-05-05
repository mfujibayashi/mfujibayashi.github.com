---
layout: posts
title:  "Javaでbyte配列からshort配列、int配列へコピー、その逆のサンプル"
date:   2020-05-01  +0900
categories: "Java"
---
# はじめに

Javaでbyte配列からshort配列、Int配列にコピーする、その逆方向へコピーするコードを書く機会がありました。  
初めは普通にシフト演算で作ったのですが、Javaらしい書き方があるはずだとのことで調べたところ、ByteBufferクラスを使った書き方があることが解りました。

# githubのリポジトリ
[githubのリポジトリ](https://github.com/mfujibayashi/JavaArrayCoppy)

# ポイント
`ByteBuffer.order()`でエンディアンを指定します。  
値を入力するときは、`ByteBuffer.put()`, `ByteBuffer.putShort()`, `ByteBuffer.pusInt()`を使います。  
値を得るときは、`ByteBuffer.get()`, `ByteBuffer.getShort()`, `ByteBuffer.getInt()`を使います。

これでエンディアンを考慮した値のコピーが出来ます。  
例えば、byte配列からInt配列へのコピーは次のようなコードになります。

```java
  public  void copyArrayFromByte(byte[] byteArray, int[] intArray){
    int length = intArray.length;
    int i;

    ByteBuffer buffer = ByteBuffer.allocate(Integer.BYTES*length);
    if(isEndian == Endian.BIG_ENDIAN){
        buffer.order(ByteOrder.BIG_ENDIAN);
    }else{
        buffer.order(ByteOrder.LITTLE_ENDIAN);
    }

    for(i=0; i< length*4; i++){
      buffer.put(byteArray[i]);
    }
    buffer.flip();
    for(i=0; i< length; i++){
      intArray[i] =  buffer.getInt();
    }
  }
```

「ビッグエンディアンは最上位桁がアドレス下位になるので」、みたいなことを思い出さずに済みます。

# サンプルコード

サンプルコードでは配列間コピーをするクラスを作成しています。  
コードを見て直ぐに内容がわかると思うので、参考にしてください。

# 最後に

もうちょっと良い書き方がありそうな気がしています。
