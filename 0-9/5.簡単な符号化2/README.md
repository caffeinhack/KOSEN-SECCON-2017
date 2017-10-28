# サンプル
## 問題
> ### [Description]
> ファイルからフラグを探せ

> ### [Problem File]
>  https://score.kosensc2017.tech/contents/problem/6/binary

## 解き方
### 1.base64をデコードする
[このサイト](https://base64encode.uic.jp/)でbase64をデコードします。
そうするとhexのデータが手に入ります。

### 2.デコードしたhexをバイナリファイルにする
さっきのhexデータをテキストとして`hex.txt`に保存して、[このサイト](https://stackoverflow.com/questions/28242813/how-to-convert-a-text-file-to-binary-file-using-linux-commands)を参考にバイナリファイルにします。
```
xxd -r -p hex.txt > binary
```

### 3.バイナリエディタで見る
さっきのデータをghexのデータで見てみると、最初の4バイト（マジックナンバー）が以下のようになりました。

```
4B 50 04 03
```

たしかzipとかのファイルのマジックナンバーが

```
50 4B 03 04
```
だったので、1バイトずつ入れ替えれば正しいflag（？）が手に入るのでないかと推測しました。

### 4.IPythonで1バイトずつ入れ替える
IPythonで以下のようなコードを書いて、1バイト入れ替えさせ（てバイナリに直すとこまでし）ました。

```ipython  
# coding:utf-8

# 一度文字としてすべて扱う
hex_str = '''4b500403...00000000'''
hex_list = list(hex_str)

# 文字数はかる
hex_length = len(hex_list) - 1

# 結果を保存する配列を作る
result = []
for count in range(hex_length + 1):
  result.append('')

# hex_strを一バイトずつ入れ替えて、hex_strに保存
for count in range(hex_length):
  if count % 4  < 2:
    result[count + 2] = hex_list[count]
  else:
    result[count - 2] = hex_list[count]

# resultを連結して文字列に
result = ''.join(result)

# ファイルに保存
_file = open('hex.txt', 'w')
_file.write(result)
_file.close()

# テキストファイルをバイナリに
!xxd -r -p hex.txt > binary
```

### 5.なんのファイルかを調べる
このファイルのマジックナンバーである
```
50 4B 03 04
```
がマジックナンバーであるファイルは多いので（詳しくは[ここ参照](https://en.wikipedia.org/wiki/List_of_file_signatures)）、fileコマンドでなんのファイルであるか調べます。

```
$ file binary
binary: Microsoft Word 2007+
```

どうやらWordのファイルっぽいです。

### 6.Wordファイルを開く
拡張子を変更した後、Google Chromeを使って、Wordファイルを開くと…

```
$ mv binary binary.doc
$ google-chrome-stable binary.doc
```

![Flag!](https://raw.githubusercontent.com/caffeinhack/KOSEN-SECCON-2017/master/0-9/5.%E7%B0%A1%E5%8D%98%E3%81%AA%E7%AC%A6%E5%8F%B7%E5%8C%962/flag.png "Flagをゲットだぜ！")

> SCKOSEN{TEXT_BUT_NOT_PLAIN}

以上のようなflagをゲットできました！
