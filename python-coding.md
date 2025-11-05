# Python 基礎 (第6週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。


## 復習

```{important}
上のプログラムは`input`関数と`while`ループと変数を使っています。  
これに加えてリストを使うように改造して、何か小さいプログラムをひとつ作ってきてください。  
来週のこの時間で発表してもらいたいと思います。  
```

発表を願いします。

## コードの参考例

```{toggle}
```{code-block}
lines = []
while True:
    line = input('> ')
    if line == 'done':
        break
    lines.append(line)

for line in lines:
    print(line)

print('Finished')
```

水上さんのコードに感心したので、紹介します。  
来週学ぶ内容も入っておりますので、また来週もう少し詳しく話します。  

```{toggle}
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

郵便番号から住所に変換するプログラム。

```{toggle}
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


## 自分の環境で実行してみる

ターミナルというソフトを実行してみましょう。  
`Finder`を開くと、`アプリケーション`という項目があると思いますが、その中に`ユーテリティ`というフォルダがあります。それを開いてみてください。
その中に`ターミナル`というソフトが入っているので、ダブルクリックで開きましょう。  

![Finder screen](finder_screen.png)

見た目が異なるかもしれませんが、下のような文字だけの画面が出てくるかと思います。

![Finder screen](terminal_screen.png)

```{code-block}
python --version
```

と打ち込んでみましょう。もし`zsh: command not found: python`と出てきた場合は、以下のように3を付けてみてください。

```{code-block}
python3 --version
```

ファイル->ダウンロード->.pyをダウンロードで保存してみましょう。
どこかに保存されましたか？  
では、ターミナルに以下のようにpython/python3と打って、その後に**半角スペース**を入力してください。

```{code-block}
python 
```
これを打った後に、例えば、もしダウンロードというフォルダに保存されたらFinderからその`xxx.py`というファイルをターミナルのウインドウにドラッグしてください。

```{code-block}
python /Users/ユーザー名/Downloads/xxx.py
```

のようになったらオッケーです。Enterを押すと、プログラムがあなたのコンピュータで動くはずです。


今週はここまでです。お疲れさまでした。