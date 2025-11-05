# Python 基礎 (第5週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。


## 復習

```{important}
Pythonで文字列を比較する方法を調べてきて、紹介してください。 
```

発表を願いします。

```{toggle}
# AI-generated code. Review and use carefully.
# 完全一致の判定
str1 = "Python"
str2 = "Python"
if str1 == str2:
    print("文字列は等しい")
else:
    print("文字列は等しくない")

# 部分文字列の検索
str1 = "Python"
str2 = "I love Python"
if str1 in str2:
    print("str1はstr2の中に存在する")
else:
    print("str1はstr2の中に存在しない")

# 大小の比較
str1 = "Apple"
str2 = "Banana"
if str1 < str2:
    print("str1はstr2より小さい")
else:
    print("str1はstr2より大きい")

```

## Loop and Iteration

先週は条件分岐(ifとインデント)を学びましたが、今週はループというものについて学びます。  
一番プログラミングらしく、ここの理解は最重要です。ここを覚えると実用的になっていきます。  
同じ処理を繰り返し行いたいときに使います。  

## for文
```{hint}
ここが自動化の肝です。繰り返し作業を日常の中でも見つけてみましょう。
```

以下を実行してみましょう。

```{code-block}
for i in range(0,11):
    print(i)
print("Finished.")
```

`range`関数はPythonのループなどでよく使います。`range(start, stop)`でstartの数字からstopまでの
数字が生成されます。stopは**含まれません**。
0からのスタートで良いときはシンプルに`range(stop)`も可能です。

range(start, stop): start ≦ i **<** stop  
range(stop): 0 ≦ i **<** stop

forではリストの処理をよく行います。  

以下を実行してみましょう。

```{code-block}
l = ["virus", "bacteria", "archaea", "amoeba"]
for name in l:
    print(name)
print("Finished.")
```

`l`というリストの中身を1つずつ`name`に入れてブロックに書かれた処理を行っていきます。  
ブロックについては前回学びました。

**演習1**

1. 新しいリストを作成しましょう。
2. forループで中身を１つずつ表示させてください。


## break文

ループを終わらせる方法の一つに`break`というものがあります。  
普通に全部繰り返す必要がないときなどに使ったりします。  

例えばリストに"ATG"という文字列が含まれているかどうか知りたいとします。

```{code-block}
l = ["AAG", "ACG", "GGG", "GCG", "ATG", "TGA"]
flag = False
for triplet in l:
    if triplet == "ATG":
        flag = True
if flag:
    print("あった")
else:
    print("なかった")
print("Finished.")
```

`break`を最後に入れると、場合によっては早く終わります。  

```{code-block}
l = ["AAG", "ACG", "GGG", "GCG", "ATG", "TGA"]
flag = False
for triplet in l:
    if triplet == "ATG":
        flag = True
    if flag:
        break

if flag:
    print("あった")
else:
    print("なかった")
print("Finished.")
```

**演習2**

先程の演習1で作ったループを`if`の条件分岐と`break`文を使って早く終わらせてみてください。

## while
Pythonでは`for`ほどは使いませんが`while`ループというものもあります。  
whileは条件判定をしながら、条件が`True`であり続ける限りブロックを実行します。  

```{code-block}
num = 0
while num < 100:
    num = num + 1
    print("Running")
print("Finished.")
```

これで実行できますが、上と下の違いは分かるでしょうか。

```{code-block}
num = 0
while num < 100:
    num = num + 1
    print("Running")
    num = num - 1
print("Finished.")
```

下の方はは永遠に終わりません。いわゆるバグったコードの例になります。  
numが増えないのでずっと`while`が実行されます。  

こういうものもあると覚えておいていただければ今はいいです。  

## input関数

```{code-block}
while True:
    line = input('> ')
    if line == 'done':
        break
    print(line)
print('Finished')
```

今週はここまでです。お疲れさまでした。

```{important}
上のプログラムは`input`関数と`while`ループと変数を使っています。  
これに加えてリストを使うように改造して、何か小さいプログラムをひとつ作ってきてください。  
来週のこの時間で発表してもらいたいと思います。  
```