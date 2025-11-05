# Python 基礎 (第3週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。


## 復習

```{important}
リストの中身が分かっているものの、どこにあるかわからないときがあります。  
上のnew_abcと同じリストがある時に、何番目に2.5があるかをPythonでどうやって知るか、来週までにグーグルやBingのchatなどで調べてきてください。
```

発表を願いします。

```{code-block}
new_abc = [0, 0.5, 1.0, 1.5, 2.0] + [2.5, 3.0]
# 2.5というｔ値を持つ場所(index)を得るためのコード
```

## Collection

先週は配列(リスト)を学びましたが、今週は別の種類の配列である辞書とタプルというものについて学びます。
配列は似たようなデータをまとめるので、collectionといったりもします。

まずは大変良く使う辞書というものを学びます。

## 辞書

```{hint}
日常生活で出てくるシチュエーションを考えながら学んでみてください。楽したいという気持ちが大事です。
```

辞書は配列でindexの代わりに、文字列で指定できるものです。
とりあえず、やってみましょう。

```{code-block}
# bagという辞書型の配列に、重さをグラムで入れたいとします。カバンの中身はお金と、飴と、テッシュと弁当箱とします。
bag = dict()
bag['money'] = 120
bag['candy'] = 3
bag['tissues'] = 10
bag['bento'] = 300
print(bag)
```

リストのように数字ではなくて、文字で中身を引っ張ってこれるのが違いです。  
この特別な文字を**key**と呼び、**key**の値を**value**と呼びます。  
辞書を引くような感じなので、Pythonでは**辞書配列**と呼ばれます。  
他のプログラミング言語では違う名前で呼ばれるので注意してください。

```{code-block}
# いっぺんに書くときはこういう書き方をします。波括弧{ }で括ります。
# {key: value, key: value, ....}

bag = {'money': 120, 'candy': 3, 'tissues':10, 'bento': 300}
print(bag)
```

リストは数字などをゴチャゴチャっとつめこむ感じの配列ですが、一つ欠点がありどこに必要な値があるのか、毎回調べないといけません。  
例えば、学校でクラスの名前を（なんらかの方法で）リストに入れたとします。

```{code-block}
names_arabic = ['Mohammed', 'Mohammed', 'Fatema', 'Ikram', 'Salim', 'Mahmoot', 'Fatema']
```

名前はそれぞれ何回出てくるか調べたいとします。どうやって数えるか?    
一つのやり方は変数を色々作って、数えることでしょうか。

```{code-block}
mohammed_counter = 0
fatema_counter   = 0
ikram_counter    = 0
```

ですが、名前が何種類あるか事前には分かりません。他のクラスでは使えないでしょう。  
例えば、クラスが変わったり、日本の名前に切り替わったらもう使えません。これは面倒くさい。  


```{code-block}
names_japanese = ['Taro', 'Taro', 'Hanako', 'Jiro', 'Hanako', 'Jiro', 'Hanako']
```

こういう時に辞書型は便利です。自動でコンピュータに変数を作ってもらうイメージです。  
print()の中身だけ見てください。

```{code-block}
# ループと条件分岐というものを使います。来週以降に話します。
names_arabic = ['Mohammed', 'Mohammed', 'Fatema', 'Ikram', 'Salim', 'Mahmoot', 'Fatema']
name_counts = dict()
for name in names_arabic :
    if name not in name_counts: 
       name_counts[name] = 1
    else :
       name_counts[name] = name_counts[name] + 1

print(name_counts)

```

```{code-block}
# 違うクラスにも対応が簡単。
names_japanese = ['Taro', 'Taro', 'Hanako', 'Jiro', 'Hanako', 'Jiro', 'Hanako']
name_counts = dict()
for name in names_japanese :
    if name not in name_counts: 
       name_counts[name] = 1
    else :
       name_counts[name] = name_counts[name] + 1

print(name_counts)

```

## リストと配列の違いを感じる

復習から入ります。
リストの中にいれた情報へアクセスするには、鈎カッコ[]を使います。  

>numbers = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]  
>print(numbers[3])

```{important}
numbers[3]の数字はなんですか？
```

辞書の配列も同じで鈎カッコ[]を使います。
> dna = {'a': 1, 't': 4, 'g': 4, 'c': 2}  
> print(dna['a'])

```{note}
dna['a']の数字は1になります。
```

**演習**

1. 新しい辞書配列を作成しましょう。
   dna = {'a': 2, 't': 2, 'g': 4, 'c': 4}  
2. tの数字を表示させてください。
3. aの数字とtの数字の合計を持つ変数**atsum**を作り、その中身を表示させてください。
4. 'u'の数字を表示させてみてください。

## 辞書にkeyがないとき

辞書配列にないものを引こうとしてしまうことがあります。  
例えばuはdnaに存在しません。  
プログラムを書くと、こういう例外的な処理をどうするかよく考えることがあります。  
そういう時に、ない場合はこうしようと決めておくことをデフォルトと呼びます。

```{code-block}
dna = {'a': 2, 't': 2, 'g': 4, 'c': 4}
print(dna['u'])
print(dna.get('a', 0)) #デフォルトの値を０としている
print(dna.get('u', 0)) #デフォルトの値を０としている
```


## タプル

タプル配列は本当にリストに似ています。
違いは**作る**時に `[ ]` ではなく`( )`を使うことだけです。

```{code-block}
num_list  = [1,2,3]
num_tuple = (1,2,3)

print(num_list)
print(num_tuple)
```

タプルとリストの違いは、タプルは１回作ったら変えられません。リストは変えられます。

**演習**
1. 新しいリストとタプル作成しましょう。  
   num_list  = [1,2,3,4,5]  
   num_tuple = (1,2,3,4,5)
2. num_listで「4」を表示させてください。print()です。
3. 4の場所に4の代わりに-4を入れてみましょう。  
num_list[ ] = -4
4. num_listを表示させましょう。
5. num_tupleで「4」を表示させてください。print()です。
5. num_tupleで同じように-4に入れ替えようとしてみてください。  
num_tuple[ ] = -4
  

今週はここまでです。お疲れさまでした。

```{important}
辞書の中身を確認した後、中身を更新したいときがあります。    
bag = {'money': 120, 'candy': 3, 'tissues':10, 'bento': 300}  
上のbagからbentoを削除する方法を、来週までにグーグルやBingのchatなどで調べてきてください。  
下みたいなやり方は**ダメ**です。何故かというと大きなデータになった時に、うまく動きません。  
bag = {'money': 120, 'candy': 3, 'tissues':10}  

bentoだけ削除する方法を探してください。
```