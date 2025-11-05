# Python 基礎 (第7週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。

## 復習

お疲れさまでした。想像していたより皆さんの個性が出ていて、課題を拝見するのはとても楽しかったです。  
大変だったかと思いますがプログラミングの大変さも少し分かってきた頃だと思います。

  
下の水上さんコードは発展的ですが、プログラムで出来ることをよく意識されているので紹介します。
`import`や`def`は**関数**とよばれるものに関連しており、今週学びます。

```{code-block}
import random
import math

def mendel(trials):
    dominant_trait = 0 # 顕性
    recessive_trait = 0 # 潜性
    ratio = 0

    for i in range(trials):
        # 親の遺伝子型（Aa型）を生成
        parent_genotype = "Aa"

        # 子の遺伝子型を決定
        child_genotype = random.choice([parent_genotype[0] + parent_genotype[0],
                                        parent_genotype[0] + parent_genotype[1],
                                        parent_genotype[1] + parent_genotype[0],
                                        parent_genotype[1] + parent_genotype[1]])

        # 子が顕性形質か潜性形質かを判定
        if 'A' in child_genotype:
            dominant_trait += 1
        else:
            recessive_trait += 1

    # 割合の計算
    dominant_ratio = dominant_trait / trials
    recessive_ratio = recessive_trait / trials

    # 比率の計算
    nums = [dominant_trait, recessive_trait]
    print(nums)
    # 結果の対比
    if dominant_trait > recessive_trait:
        d_ratio = dominant_trait / recessive_trait
        r_ratio = 1
    elif dominant_trait < recessive_trait:
        r_ratio = recessive_trait / dominant_trait
        d_ratio =1
    else:
        print("顕性形質と潜性形質の割合は等しいです。")

    return dominant_ratio, recessive_ratio, d_ratio, r_ratio




# 試行回数を指定
num_trials = int(input("試行回数を入力してください>"))

# メンデルの法則に基づいた遺伝子型の割合を計算
dominant_ratio, recessive_ratio, d_ratio, r_ratio = mendel(num_trials)


# 結果の表示
print("顕性形質の割合=", '{:.2f}'.format(dominant_ratio*100),"%")
print("潜性形質の割合=", '{:.2f}'.format(recessive_ratio*100), "%")
print("顕性形質の割合:潜性形質の割合=",  '{:.2f}'.format(d_ratio), "：", '{:.2f}'.format(r_ratio))
```

## 関数

先週までPythonプログラミングの基礎を学んできましたが、ここからはさらに進んでいきます。  
関数とは何でしょうか？

やや数学寄りですが、素朴で直感的なイメージは以下のようなものです。
何かを入れると(入力)、何かが出てくる(出力)ブラックボックスのことを関数と呼びます。

![Function](https://upload.wikimedia.org/wikipedia/commons/3/3b/Function_machine2.svg)

英語の`function`は関数(名詞)という意味以外に、機能する(動詞)という意味を持ちます。  
日本語の「機能」、という意味合いを含んでいることは知っておいていいと思います。
お金を入れると缶が出てくるという意味で、自動販売機は関数っぽいと言えます。そしてそれが自動販売機の機能であるというイメージでしょうか。

概念の説明としては、こんな感じですが、プログラミングでは**何度も**出てくるような処理を関数にします。  
今までも使ってきており、`print()`は関数の1つです。

```{code-block}
nums = [1,2,3,4,5,6,7]

maxnum = -1
for i in nums:
    if i > maxnum:
        maxnum = i

print(maxnum)


nums2 = [1,39,3,10,9,32,8]

maxnum2 = -1
for i in nums2:
    if i > maxnum2:
        maxnum2 = i

print(maxnum2)


nums3 = [37,9,80,21,89,438,4,27,69,8,127,31]

maxnum3 = -1
for i in nums3:
    if i > maxnum3:
        maxnum3 = i

print(maxnum3)
```
何度も同じ処理が出てきています。こういうことが結構あり、書くのが面倒です。  
そしてバグを入れやすくなります。なので`max()`という関数を使い、簡潔に書いてみましょう。

```{code-block}
nums = [1,2,3,4,5,6,7]
maxnum = max(nums)
print(maxnum)

nums2 = [1,39,3,10,9,32,8]
maxnum2 = max(nums2)
print(maxnum2)

nums3 = [37,9,80,21,89,438,4,27,69,8,127,31]
maxnum3 = max(nums3)
print(maxnum3)
```

では、詳しく見ていきましょう。

## 関数の書き方

以下のような型を持っており、`def`というキーワードで始めます。

```{code-block}
def function_name(arguments):
    # ここに何かを書く
    return
```

- `def`は関数を宣言するためのキーワードです。
- `function_name`は関数の名前です。
- `arguments`は関数に渡される値（入力)です。複数の引数を指定する場合は、カンマで区切ります。
- `# ここに何かを書く`は関数が実行するコードを書きます。
- `return`は関数から値を返すためのキーワードです。出力に相当します。

例えば以下のように定義します。

```{code-block}
def add_numbers(num1, num2):
    sum = num1 + num2
    return sum
```

使い方は下のようにします。

```{code-block}
result = add_numbers(5, 3) #入力は5と3
print(result)  # 出力は8
```

**演習**

1. 新しい文字を連結する関数を作成しましょう。
2. 入力は２つの文字列です。
3. ２つをつなげて何か文章を返すようにしましょう。  
例えば、入力が"apple", "orange"で、出力は「入力はappleとorangeです。」のような感じです。
4. 関数の結果を別の変数に入れ (上のresultのように)、それをprint()してください。

## モジュールとimport

誰かが作った関数を使えるようにまとめて、モジュールと呼ぶものを提供してくれることがあります。  

以下を実行しましょう。pillowとrequestsとmatplotlibというものをダウンロードしてインストールします。
```
!pip install pillow requests matplotlib
```

Pillowという画像を加工するモジュール、requestsというウェブの操作をするモジュール、そして画像やグラフの表示を行うmatplotlibというモジュールをダウンロードして使います。

```{code-block}
import requests
from PIL import Image
from io import BytesIO
import matplotlib.pyplot as plt

# 画像のURL
url = "画像のURLをここに入力する"
#url = "https://www.thesprucepets.com/thmb/ZaIDvU4xL65zJWUqESegtCDTv70=/2180x0/filters:no_upscale():strip_icc()/GettyImages-1019461046-7096d0b574c94d0ab320b8b9fcdd5876.jpg"

# 画像をダウンロード
response = requests.get(url)
img = Image.open(BytesIO(response.content))

# 元画像を表示
print("元画像")
plt.imshow(img)
plt.show()

# 画像を100x150にリサイズ
img = img.resize((100, 150))

# 画像を表示
print("リサイズ画像")
plt.imshow(img)
plt.show()
```

**演習**

1. 上のコードを実行してみます。
2. urlという変数に好きな画像を選んでください。
3. リサイズして表示させてみましょう。


今週はここまでです。お疲れさまでした。

```{important}
pillowの他の機能(関数)を使って何か画像を処理して表示させてください。
例えば下のような処理が出来るようです。
```

![original](https://robocrop.realpython.net/?url=https%3A//files.realpython.com/media/buildings-1.9786ca5e657d.jpg&w=960&sig=68b213ecf2f56041319294d2cc04be18df8439ec)

![cropping](https://files.realpython.com/media/pillow_coordinate_crop2.15af40c34f15.png)

![cropped](https://files.realpython.com/media/buildings-3.8aaa8fee17fb.jpg)