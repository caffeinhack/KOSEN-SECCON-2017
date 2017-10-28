# 寝坊気味のコンピュータ
## 問題
> ### [Description]
> ここにある通信をキャプチャしたファイルがある。この中から、フラグを見つけ出せ！

> ### [Problem File]
> [https://score.kosensc2017.tech/contents/problem/18/problem.pcapng](https://raw.githubusercontent.com/caffeinhack/KOSEN-SECCON-2017/master/10-19/15.%E5%AF%9D%E5%9D%8A%E6%B0%97%E5%91%B3%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF/problem.pcapng)

## 解き方
### 1.Wiresharkを起動
pcapngファイルをダウンロードして、Wiresharkを起動します。
```
$ wireshark problem.pcapng
```

### 2.HTTPを閲覧
とりあえずフィルタに`http`と入力して、適当なhttpパケット見つけた後、HTTP Streamをかけます。
すると最後の方に以下のようなリクエストとレスポンスを確認できます。

```
GET / HTTP/1.1
Host: 172.27.132.124
Connection: keep-alive
Authorization: Basic YWRtaW46U0NLT1NFTntiYXNpY19pc191bnNlY3VyZX0=
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.102 Safari/537.36 Vivaldi/1.94.971.8
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.8

HTTP/1.1 200 OK
Server: nginx/1.10.3 (Ubuntu)
Date: Fri, 20 Oct 2017 03:23:43 GMT
Content-Type: text/html
Last-Modified: Fri, 20 Oct 2017 03:08:48 GMT
Transfer-Encoding: chunked
Connection: keep-alive
ETag: W/"59e968c0-264"
Content-Encoding: gzip

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

どうやらBasic認証をして、認証が通ったっぽいです。


### 3.base64をデコード
Basic認証はID・パスワードを暗号化せずBase64でデコードして送信するので、今回も
> YWRtaW46U0NLT1NFTntiYXNpY19pc191bnNlY3VyZX0=

の部分を[このサイト](https://base64encode.uic.jp/)でデコードします。

そうすると以下の文字列が出てくるので、
> admin:SCKOSEN{basic_is_unsecure}

flagは
> SCKOSEN{Management_of_IP_numbers_by_peg-dhcp}
