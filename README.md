> [!CAUTION]
> コードは配布されていません。

### klzonaka
# Poe Lang - v0.2.0-beta

## 説明
Poe Langへようこそ。

この言語では**Poe**キーワードをメインとした難解プログラミング言語です。

## 注意
コードはまろんが自己満足するために作られています。 配布予定はありません。

Poeプログラムは非常に可読性・記述性が低いため実用性は期待できません。

また現在開発段階であり、 機能は不完全です。

Poe Langは2つのバイトストリーム(入力と出力)のみ存在し、 **エラー出力がありません。**

文法的な間違いは**全てコメントとして無視されます。**

また数値は、 小数点が発生する場合**全て切り捨てられます。**

## 要素
Poe Langは次の要素から成り立ちます:
* **Poe プログラム:** プログラムのメイン処理。
* **ボックス:** 配列。 各要素はundefinedとなっている、 呼び出す際に-1で初期化される。
* **ポインタ:** 前述の配列のどれかの要素を指す。初期化は最も左。
* **バイトストリーム:** 入力と出力。

Poe プログラムは、 以下の実行可能な命令から成りたっています。

**スペース区切り**で入力し、 以下の命令表に存在しないものはコメントとして無視されます。

(スペースの代わりに、 改行を使用することも可能です。)

ループ処理できない命令をループ処理として使おうとすると、 コメントとして無視されます。
### 基本命令
| 命令 | 効果 |ループ可能|
| ---- | ---- |----|
| **wow** | ポインタをインクリメントします。 |true|
| **wowwow** | ポインタをデクリメントします。 |true|
| **poe** | ポインタが指している値をインクリメントします。 |true|
| **poepoe** | ポインタが指している値をデクリメントします。 |true|
| **poe~** | ボックスを正規化し、 出力します。 |false|
| **poepoe~** | ポインタが指している値を正規化し、 出力します。 |false|
| **poe?** | ポインタが指している値のインデックスを出力します。 |false|
| **poepoe?** | ポインタが指している値を出力します。 |false|
| **poe!** | ボックスを出力します。 |false|
| **poepoe!** | ボックスの長さを出力します。 |false|

上記の命令のうち、 ループ可能なものは命令の後ろに**区切りをつけず数値を入力**すると、その命令を回数分ループさせます。

但し、 **ループ回数0は特殊です。** 例えば `poe0 poe!`は呼び出す際に-1で初期化されているため、 ポインタの指す数値が-1となります。

### 特殊命令
| 命令 | 効果 |オフセット指定可能|
| ---- | ---- |----|
| **=>** | ポインタの指す値を、 次のボックスに代入します。 |true|
| **+>** | ポインタの指す値を、 次のボックスに加算します。 |true|
| **->** | ポインタの指す値を、 次のボックスに減算します。 |true|
| **\*>** | ポインタの指す値を、 次のボックスに乗算します。 |true|
| **/>** | ポインタの指す値を、 次のボックスに除算します。 |true|
| **=<** | ポインタの指す値を、 前のボックスに代入します。 |true|
| **+<** | ポインタの指す値を、 前のボックスに加算します。 |true|
| **-<** | ポインタの指す値を、 前のボックスに減算します。 |true|
| **\*<** | ポインタの指す値を、 前のボックスに乗算します。 |true|
| **/<** | ポインタの指す値を、 前のボックスに除算します。 |true|
| **wow=>** | ポインタの指す値を、 次のボックスに代入してからポインタを移動します。|true|
| **wow+>** | ポインタの指す値を、 次のボックスに加算してからポインタを移動します。|true|
| **wow->** | ポインタの指す値を、 次のボックスに減算してからポインタを移動します。|true|
| **wow\*>** | ポインタの指す値を、 次のボックスに乗算してからポインタを移動します。|true|
| **wow/>** | ポインタの指す値を、 次のボックスに除算してからポインタを移動します。|true|
| **wow=<** | ポインタの指す値を、 前のボックスに代入してからポインタを移動します。|true|
| **wow+<** | ポインタの指す値を、 前のボックスに加算してからポインタを移動します。|true|
| **wow-<** | ポインタの指す値を、 前のボックスに減算してからポインタを移動します。|true|
| **wow\*<** | ポインタの指す値を、 前のボックスに乗算してからポインタを移動します。|true|
| **wow/<** | ポインタの指す値を、 前のボックスに除算してからポインタを移動します。|true|
| **>>** | ポインタの指す値分、 先にポインタをステップさせます。 オフセット値を指定した場合指定したインデックスにステップします。 |true|
| **<<** | ポインタの指す値分、 前にポインタをステップさせます。 オフセット値を指定した場合指定したインデックスにステップします。 |true|
| **{** | ポインタが指す値が0なら、対応している `}` の直後にジャンプします。 |false|
| **}** | ポインタが指す値が0でないなら、対応している `{` の直後にジャンプします。 |false|
| **$** | 設定した値分、 ボックスを初期化します。 |required|
| **#** | 設定した値分、 ボックスをゼロクリアします。 |required|

上記の特殊命令は、 記号を利用しているためこのように分類されます。

オフセット指定可能なものは、 命令の後ろに**区切りをつけず数値を入力**すると、 ボックスのオフセット値を変更できます。

例えば、 `$5 poe =>5 poe!`を行うと、 ポインタの指す値がオフセットから5つ進んだ場所に値を代入します。

この場合、 ボックスが初期化されていないと、 ボックスの直下に値を代入してしまう **[ドロップ](https://github.com/klzonaka/Poe-Lang-Documentation?tab=readme-ov-file#%E3%83%89%E3%83%AD%E3%83%83%E3%83%97)** が発生します。 `$` や `#` キーワードでボックスを予め初期化してください。

## Poe Langの実行
このフォルダに、 「index.poe」というファイルを作成してみましょう。

「run.bat」でindex.poeが実行されます。

## 仕様説明
### エラー出力がない
コード内に不要な文字列がある場合、 それはコメントとして無視されます。
エラーを一切スローされません。 例え無限にループする状況になっても、 コードは実行を続けます。
### ドロップ
ボックスは、 サイズが**可変で動的に変化します。**
例えば以下のようにボックスが存在するとします。
```
[10, 50, 25, 40]
     ^^        
```
> [!NOTE]
> ^^ はポインタの位置を指しています。

ポインタの位置はインデックスで**1番目**に存在します。

このポインタを**10番目まで操作して「5」を加算すると次のようになります。**
```
[10, 50, 25, 40, 50]
                                 ^^
```
本来10番目に入るはずの要素が、 ボックス内の直下に入っています。

こうした仕様を**ドロップ**と呼びます。 回避するには `$` `#` を使用して予めボックスを拡張しておきます。

`#10` を行った状態で、 **10番目に「5」を加算すると次のようになります。**
```
[10, 50, 25, 40,  0,  0,  0,  0, 50]
                                 ^^
```
