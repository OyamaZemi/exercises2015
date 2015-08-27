課題4 (2015/7/6)
================

Kandori-Mailath-Rob (KMR) の確率進化モデルのシミュレーションをしてみる．

* 提出方法：GitHub にリポジトリを「プッシュ」する．
* 締め切り：7月16日 (木)

(4年生は昨年度自分が書いたコードに手を入れ，1年間で進化したところを見せる．)


## 準備

[quant-econ.net](http://quant-econ.net/py/index.html) の

* [Finite Markov Chains](http://quant-econ.net/py/finite_markov.html)
* [Object Oriented Programming](http://quant-econ.net/py/python_oop.html)

を読む．


## KMR モデル

[KMR の確率進化動学の説明](http://nbviewer.ipython.org/github/OyamaZemi/exercises2015/blob/master/ex04/KMR_notes.ipynb)


## やること

* KMR モデルの説明をよく読んで，0 期から T-1 期までの X\_t の列を生成し，X\_t(N) の動きをプロットする．
  (epsilon は小さい値に設定し，それに依存して T は大きい値に設定する)．

* また，X\_t そのものだけではなく，X\_t の実現値の頻度分布 \\bar{X}\_t の様子も調べる．
  (\\bar{X}\_t の動きをプロットしたり，\\bar{X}\_{T-1} の分布をヒストグラムにしてみたりする．)

* {X\_t} の定常分布を求めてヒストグラムにする．
  epsilon を小さくしていって，定常分布の変化の様子を見る．


## 方法

* まずは，与えられた利得行列，プレイヤーの数，epsilon に対して遷移行列を構成する方法を考える．

* 遷移行列 (たとえば `P` とする) を用いて
  [QuantEcon.py](https://github.com/QuantEcon/QuantEcon.py) の
  [MarkovChain](http://quanteconpy.readthedocs.org/en/latest/tools/mc_tools.html#quantecon.mc_tools.MarkovChain)
  インスタンス (たとえば `mc` とする) を作る．

  ```python
  import quantecon as qe
  mc = qe.MarkovChain(P)
  ```

* `MarkovChain` クラスのメソッドを使う．
  たとえば `mc.stationary_distributions` とすると定常状態が求められる．

* 最終的には自分でクラス (`KMR` とか) を定義して使ってみる．

* 完成品はたとえば[こんな感じ](http://nbviewer.ipython.org/github/oyamad/stochevolution/blob/master/KMR2x2_example.ipynb)．


## QuantEcon.py の開発バージョンのインストール

いま現在，`MarkovChain.simulate()` の
interface の変更が議論されていますが，まだ `master` にマージされていないので，
先取りして開発バージョンをインストールしましょう．

(2015/8/27追記)
`master` にマージされました．

ターミナルで

```
pip install git+https://github.com/QuantEcon/QuantEcon.py.git
```

と打ちます．
(すでにインストールしている場合は `-U` を加える．)


## 発展

3x3 ゲームもやってみる．

Young の例というのが有名：

```python
[[6, 0, 0],
 [5, 7, 5],
 [0, 5, 8]]
```

Bilingual game:

```python
def bilingual_game(e, a=11, b=0, c=3, d=10):
    payoff_matrix = np.array([[a  , a  , b],
                              [a-e, a-e, d-e],
                              [c  , d  , d]])
    return payoff_matrix
```

`e` を 2.5 くらいから 0 の近くまで小さくしていって標本経路や定常分布の変化の様子を観察する．

* D. Oyama and S. Takahashi,
  "[Contagion and Uninvadability in Local Interaction Games: The Bilingual Game and General Supermodular Games](http://www.oyama.e.u-tokyo.ac.jp/papers/bilingual.html),"
  Journal of Economic Theory 157 (2015), 100-127.


## テンプレート

テンプレートを作ったので参考にしてください．

* [kmr.py](kmr.py)


## 注意

われわれが使っている Python バージョン 2.x では，整数どうしの割り算は小数点以下が切り捨てられて整数になります．
たとえば `1/2` を `0.5` と計算させたければ，ファイルの冒頭で

```python
from __future__ import division
```

と宣言しないといけません．

たとえば
[Python Essentials](http://quant-econ.net/py/python_essentials.html)
参照のこと．
