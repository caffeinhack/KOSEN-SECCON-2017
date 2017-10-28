# ファイル名を探せ
## 問題
> ### [Description]
> フラグは簡単だ、ファイル名に隠した。

> ### [Problem File]
> [https://score.kosensc2017.tech/contents/problem/1/q](https://github.com/caffeinhack/KOSEN-SECCON-2017/blob/master/0-9/2.%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%90%8D%E3%82%92%E6%8E%A2%E3%81%9B/q?raw=true)

## 解き方
### 1.ファイルをダウンロードして、そのファイルのあるディレクトリに移動
まずファイルをダウンロードして、そのファイルのあるディレクトリに移動します。

### 2.ファイルを特定して、gzipを解凍
#### a.ファイルの作成
fileコマンドを使って、ファイルの種類を調べます。
```
$ file q
q: gzip compressed data, last modified: Thu Oct 19 04:49:39 2017, from Unix
```
gzipで圧縮されているようです。

#### b.解凍して中身のファイル一覧を確認する
binwalkを使って解凍して、ファイルを見るととんでもなく多いファイルが表示されます。
```
$ binwalk -e q
$ cd _q.extracted
$ ls
0
```
`0`というファイルがあるようですね。

### 2. ファイルを特定して、tarを解凍
#### a.ファイルの作成
fileコマンドを使って、ファイルの種類を調べます。
```
$ file 0
0: POSIX tar archive (GNU)
```
tarで圧縮されているようです。

#### b.解凍して中身のファイル一覧を確認する
binwalkを使って解凍して、最下位ディレクトリでファイルを見るとファイル名がたくさん表示されます。
```
$ binwalk -e 0
$ cd _0.extracted
$ ls
q
$ cd q
$ ls
00akEo0KmEZ2rNDi6ppehmavGAhwN
.
.
.
zZyzeJMVVW6zu7b8nPn3JL9tR1I6T
```
ファイルめっちゃ多い…

### 3.Flagと関係ありそうなファイル名だけを抽出する
問題文的にも、このファイル名にFlagがあるのでしょうけど、これをすべて確認するのは厳しいです。
そこでgrepを使って絞れるかやってみます。

```
$ ls | grep SCKOSEN
SCKOSEN{ki_ha_mori_ni_kakuse}
```

flagゲット！

> SCKOSEN{ki_ha_mori_ni_kakuse}
