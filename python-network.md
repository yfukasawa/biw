# Python 基礎 (第9週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。

## 復習

```{important}
このファイルはこのままでは計算できません。例えば７列目は人口(総数)となっていますが、文字としてPythonは認識しています。  

例:   ['"00"', '"全国"', '"大正"', '9', '1920', '""', '55963053', '28044185', '27918868']  

'55963053'は文字です。これを数字としてPythonに認識させましょう。
以下のコードで、変数に整数とし入れる処理を完成させてください。  
  
?の部分を置き換えてみてください。
```

```{code-block}
file_handle = open("c01.csv", encoding='cp932')

count = 0
total = 0
for l in file_handle:
    line = l.rstrip()
    count = count + 1
    retsu = line.split(",")
    if len(retsu) != 9:
        continue
    total_moji = retsu[?]
    #print(total_moji)
    if "人口" in total_moji or "-" in total_moji:
        continue
    total_num  = ???(total_moji)
    total = total + total_num
file_handle.close()

print("人口の総和: %d" % total)
print("行数: %d" % count)
```

埋められましたか？

## ネットワーク

今週は「ネットワーク」の基礎について学びます。

```{note}
コンピュータネットワーク（computer network）とは、コンピュータネットワークとは、複数のコンピュータを信号線や無線で接続し、互いにデータの送受信ができるようにした通信網。通常は3台以上の機器が結ばれたものを指す。(出典: e-words.jp)
```

今の時代、コンピュータのネットワークは生活に欠かせないものになってきました。  
このネットワークを支えているものは「約束(規約)」です。英語でプロトコルと呼ばれるのですが、複数のコンピュータがお互いに決められた約束を守ってデータを送り合える状態にあることが重要です。  
余談ですが、コンピュータやITの世界でプロトコルを決める側にたつことがビジネスでは重視されます。

![Tin_can_telephone](telephone-illustration.png)

もっとも重要なネットワークはインターネットと呼ばれるもので、これはInternet Protocol (IP) と呼ばれる規約で成立しています。IP電話とかIPアドレスという単語はここから来ています。

## HTTP (Hypertext Transfer Protocol)

何でも良いのでテキストエディタを開いて以下を書いてみてください。  
HTMLと呼ばれるもので、こういった基本的な技術がGoogleなどを支えています。

```{code-block}
<HTML>
<html>
  <head>
    <title>ページのタイトル</title>
  </head>
  <body>
    <h1>見出し1</h1>
    <p>段落1</p>
    <h2>見出し2</h2>
    <p>段落2</p>
  </body>
</html>
```
書いたら保存して、ファイルの名前をXXXX.htmlとしてください。(XXXXは好きな文字でいいですが、.htmlは必ずつけてください)  

HTMLというものは、<タグ名>という形をした「タグ」と呼ばれるもので、文字を挟んでいき文章をきれいにするものです。終わる時は</タグ名>で囲みます。上の例だと一番最初と最後に<html></html>で挟んでおり、これがHTMLだと教えています。

**演習**

1. 上のファイルを作りましょう。  
2. <img>というタグを使って、好きな絵を入れてみましょう。  
\<img src="https://...">で入れます。下を参考にしてみてください。
3. ブラウザで確認してみてください。

```{code-block}
<html>
  <head>
    <title>ページのタイトル</title>
  </head>
  <body>
    <img src="https://bix-uu.sakura.ne.jp/logo.png" alt="ロゴ">
    <h1>見出し1</h1>
    <p>段落1</p>
    <h2>見出し2</h2>
    <p>段落2</p>
  </body>
</html>
```

こういったハイパーテキストなどを交換するための約束がHTTPと呼ばれるものです。  
こちらからサーバーに要求 (リクエスト) を行って返ってきたデータを処理する約束のことを言います。  
例えばブラウザで以下のページを開いてみましょう。

>https://qiita.com/

Qiitaは開発者がお互いに情報交換を行うウェブサイトで私も重宝しています。  
ここで、以下のようにsearch?q=htmlとブラウザで追加してみてください。

>https://qiita.com/search?q=html

Qiitaでhtmlと検索すると、実は私達のコンピュータから上のような文字をQiitaのサーバーに送って検索結果を要求しています。なので、自分で直接書いても良いわけです。  
プログラミングを勉強したので分かってきたかと思いますが、?の後ろにq=という文字が見えますね。これ**はqという名前の変数**に何かをいれて、その変数を向こうのサーバーに送っているイメージです。  
?のあとに、サーバーが受け付ける変数名(この場合はq)とその値を指定して送り、ブラウザで表示される通信方法を**GET**と呼びます。

## ブラウザではなくPythonで行う

上のようなGET通信はブラウザだけではなくPythonでもできます。やってみましょう。

```{code-block}
import requests
url = "https://qiita.com/"
parameters = {"q" : "html" }
response = requests.get(url, params=parameters)
print(response)
```

```{note}
上のresponseという変数には実は色々なデータが入っており、それぞれに変数が与えられています。  
このように色々な変数を便利な形でまとめたものをオブジェクトと呼びます。  
```

上のresponceというオブジェクトには複数の変数が入っており、その一つがtextと呼ばれる変数です。  
確認してみましょう。

**演習**

1. 上記のコードをcolabで実行してみてください。
2. print(responce.text)とやってみて、textという**変数**を確認してください。  
- Pythonの話になりますが、「.(ドット)」は意味があり、ドットの左のオブジェクトにあるドットの右の変数や関数にアクセスするという書き方でした。  
- 上の場合は「responce」というオブジェクトにある「text」という変数にアクセスしています。
- この他、response.json()とすると`json()`という関数にアクセスできます。
3. これをresponce.htmlというファイルに保存してください。
```
filename = "responce.html"
fh = open(filename, "w")
fh.write(response.text)
fh.write("\n")
fh.close()
```
4. Colabのスペースに新しいファイルが出来ているはずなので、ダウンロードしてブラウザで開いてみましょう。


### おまけ (郵便番号を取得するプログラム)
```{code-block}
import requests

def get_address_from_postal_code(postal_code):
    response = requests.get(f'http://zipcloud.ibsnet.co.jp/api/search?zipcode={postal_code}')
    data = response.json()

    if data['status'] == 200:
        if data['results'] is None:
          return "Invalid postal code"
        address_data = data['results'][0]
        return f"{address_data['address1']} {address_data['address2']} {address_data['address3']}"
    else:
        return "Invalid postal code"

lines = []
while True:
    line = input('> ')
    if line == 'done':
        break
    address = get_address_from_postal_code(line)
    lines.append(address)

for line in lines:
    print(line)

print('Finished')
```

今週はここまでです。お疲れさまでした。

```{important}
HTMLは文章をキレイにする良い方法ですが、それだとWordなんかでも出来るわけです。  
HTMLとHTTPが革新的だった理由はリンクだと考えています。  
\<A>というリンクを張るタグがあるので、書き方を調べて、Aタグを使ってリンクのあるHTML文書を作成してください。
```
