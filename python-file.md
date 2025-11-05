# Python 基礎 (第8週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。

## 復習

```{important}
pillowの他の機能(関数)を使って何か画像を処理して表示させてください。
例えば下のような処理が出来るようです。
```

何か処理出来ましたか？

## ファイルの読み込み

今週は「ファイル」の読み込みについて学びます。

```{note}
ファイルとは、コンピュータにおけるデータの管理単位の一つで、ストレージ装置（外部記憶装置）などにデータを記録する際に利用者やOSから見て最小の記録単位となるデータのまとまり。(出典: e-words.jp)
```

前回は、画像「ファイル」をインターネットから読み込んでいました。

```{code-block}
response = requests.get(url)
img = Image.open(BytesIO(response.content))
```

厳密に言えば違いますが、`Image.open()`という関数を使って画像データをimgという変数に入れています。
日本語でファイルを「開く」と言いますが、英語だと「open」するというので、`open()`という名前の関数がよく出てきます。

## 遺伝子配列ファイルの読み込み

```{code-block}
file_handle = open("ファイルの場所")
file_handle.close()
```

ファイルをプログラムで開くのはこれだけですが、これだと何もしていないので何も起きません。
1行ずつ読んで行数を数えてみましょう。

```{code-block}
file_handle = open("R9WNI0.fasta")

count = 0
for l in file_handle:
    count = count + 1

file_handle.close()
print(count)
```

```{note}
Fastaと呼ばれる形式のファイルで、名前を書くための行と実際のDNAやアミノ酸の配列を書く行の２つで構成されています。  
行の最初に来る「>」という記号が大変重要で、これがある行は名前やIDを書くものと決まっています。
それ以外の行は全てDNA/RNA/アミノ酸配列を書くための行です。
```

**演習**

1. R9WNI0.fastaというファイルをダウンロードしましょう。
2. これをColabのマシンにアップロードしましょう。
3. 上のコードを実行して何行あるかを確認してください。

## 表データの読み込み

実際の社会や研究ではエクセルのような表形式のデータを扱うことが大変多いです。
これをコンピュータで処理することは便利なので覚えてみましょう。

```{code-block}
file_handle = open("c01.csv", encoding='cp932')

count = 0
for l in file_handle:
    line = l.rstrip()
    count = count + 1
    print(line)

file_handle.close()
print(count)
```

```{note}
こちらはcsvと呼ばれる形式のファイルで、エクセルなどで作った表をコンピュータで読む時によく使われます。  
各列をカンマで区切るので、Comma-Separated Valuesの略でcsvファイルと呼ばれます。
```

読み込んだ文字列を指定した文字で「分割して」、リストにする関数である`split()`という関数を使ってみましょう。


**演習**

1. c01.csvというファイルをメールからダウンロードして、colabにアップロードしてください。
2. 上のコードを実行してみましょう。
3. count = count +1 の下に以下のコードを入れてみてください。  
`retsu = line.split(",");`  
`print(retsu)`
3. retsu全部ではなく、retsuの2列目である「県名」だけを表示させてみてください。


今週はここまでです。お疲れさまでした。

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