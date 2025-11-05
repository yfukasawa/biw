# Python 基礎 (第13週)

本コンテンツは[深沢研究室](https://c-bio.mine.utsunomiya-u.ac.jp/fukasawa/)でPythonを教えるために作成された演習資料です。

## 復習

### githubを使うのに必要なもの

1. ユーザー名
2. パスワード (Webなどでのログイン時に必要)
3. token (コードをwebにアップロードするときに必要)

### 新しいpythonのインストール(必要な人向け)

Macに入っているPythonが古い場合、以下で書くGUIが動作しません。その場合は、以下の手順で`conda`と呼ばれるソフトを入れるソフトをインストールしましょう。

参考: githubページ  
https://github.com/conda-forge/miniforge

1. ターミナルを開いてください。
2. 以下のコマンド(curlで始まる行とbashで始まる行の2行です)をそれぞれ１行ずつ実行してください。

```{code-block}
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"

bash Miniforge3-$(uname)-$(uname -m).sh
```

3. 終わったら１回ターミナルを終了して、もう１度開くと良いと思います。
4. 左に`(base)`と表示されていたら成功です。

## GUIアプリケーション続き

```{tips}
GUIとは、グラフィカルユーザインターフェース(Graphical User Interface)の略語。  
コンピュータへ出す命令や指示等を、ユーザが画面上で視覚的に捉えて行動を指定できるもので、それまで主流であった命令文を入力して実行する方式(CUI)に比べ、直感的に操作できるのが特長。
(出典: ITトレンド)
```

今まで使ってもらったターミナルのような画面をCUI(Character User Interface)と言います。マウスとかタッチパネルをあまり使わず、キーボードだけで操作するような画面ですね。  
例えば、皆さんのコードをバックアップするgitというソフトはCUI方式のソフトウェアです。

今まで作ってもらったソフトはすべてCUI方式のものです。作るのが簡単だという利点ですね。  
GUIをどうやって書くか、少し触れていきましょう。

## tkinterでボールを描画

今回は、前回の続きで、まずはボールを表示させましょう。

```
def main():
    window = tk.Tk()
    window.geometry("%dx%d" % (window_width, window_height))

    # Windowのタイトル
    window.title("GUI")

    label = tk.Label(window, text="Hello World!")
    label.place(x=0, y=0)

    canvas = tk.Canvas(window, width=canvas_width, height=canvas_height, bg="white")
    canvas.place(x=(window_width-canvas_width)/2, y=(window_height-canvas_height)/2)

    circle = create_circle(canvas, co["x"], co["y"], co["r"], fill="blue")

    window.mainloop()
```

**演習**

1. ボールの位置を変えてください。
2. ボールのサイズを変えてください。
3. 最後に、ボールの色を変えてください。

![tkinter-canvas-ball](canvas_ball.png)

ここまで出来たら一旦、githubにアップロードしてみましょう。　

## ボールを動かす

描画の仕方は色々ありますが、大事な点は画面を高速に描き直していることです。  
1秒間の間に何度も描画をし直すことで、動いているように見せていきます。

こういう時は、ループを使います。  
ボール(circle)を高速に描いて消して描いて消してを繰り返すことで、動いているように見せています。  
`move_circle()`という関数でボールの次の位置を計算しています。

```{code-block}
def main():
    window = tk.Tk()
    window.geometry("%dx%d" % (window_width, window_height))
    
    # Windowのタイトル
    window.title("GUI")

    canvas = tk.Canvas(window, width=canvas_width, height=canvas_height, bg="white")
    canvas.place(x=(window_width-canvas_width)/2, y=(window_height-canvas_height)/2)

    while True:
        # Create a circle
        circle = create_circle(canvas, co["x"], co["y"], co["r"], fill="blue")
        co["x"], co["y"], co["dx"], co["dy"] = move_circle(co["x"], co["y"], co["dx"], co["dy"])
        label = tk.Label(window, text="%d, %d" % (co["x"], co["y"]))
        label.place(x=0, y=0)
        label2 = tk.Label(window, text="%d, %d" % (co["dx"], co["dy"]))
        label2.place(x=0, y=20)

        time.sleep(0.04)
        window.update()
        canvas.delete(circle)
        label.destroy()
        label2.destroy()

    window.mainloop()
```

main()関数の前にmove_circle()関数を書きましょう。  
壁に当たると向きを変えるような仕組みです。

```{code-block}
def create_circle(canvas, x, y, r, **kwargs):
    return canvas.create_oval(x-r, y-r, x+r, y+r, **kwargs)

def move_circle(x, y, dx, dy):
     # 仮の変数に移動後の値を記録
     _x = x + dx
     _y = y + dy
     # 上左右の壁に当たった？
     if _x < 0 or _x > canvas_width:
         dx *= -1
     if _y < 0 or _y > canvas_height:
         dy *= -1
     # 移動内容を反映
     if 0 <= _x <= canvas_width:
         x = _x
     if 0 <= _y <= canvas_height:
         y = _y

     return _x, _y, dx, dy

def main():
    window = tk.Tk()
    window.geometry("%dx%d" % (window_width, window_height))
    
    # Windowのタイトル
    window.title("高速なSamsung")

    canvas = tk.Canvas(window, width=canvas_width, height=canvas_height, bg="white")
    canvas.place(x=(window_width-canvas_width)/2, y=(window_height-canvas_height)/2)
    ....
    ...
    ..
    .
```

**演習**

1. ボールの動きを早くしてください。



```{important}
ボールだけでは面白くないので、何か画像を追加してください。  
追加し表示を確認したら、githubへアップロードをお願いします。  
ここまで終われば、githubのURLを送ってください。  

https://github.com/アカウント名/tkinter-coding.git

```

今週はここまでです。お疲れさまでした。

