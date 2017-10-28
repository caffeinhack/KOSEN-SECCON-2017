# Web2
## 問題
> ### [Description]
pcapファイルを解析して、隠されたサービスを発見しろ。

> ### [Problem File]
[https://score.kosensc2017.tech/contents/problem/12/hoge.pcap](https://raw.githubusercontent.com/caffeinhack/KOSEN-SECCON-2017/master/20-K2/15.%e9%80%9a%e4%bf%a1%e3%82%92%e8%a7%a3%e6%9e%90%e3%81%97%e3%82%8d)

> ### [Server Address]
http://10.201.1.102

## はじめに
この問題は解けませんでしたが、途中でflagと出会ったので残しておきたいと思います。

## 途中のflagとの出会い方
Wiresharkでhoge.pcapをダウンロードして、Wiresharkで開き、適当なhttp通信にHTTP Streamかけると見つかります。

> SCKOSEN{p0rtkn0cking}
