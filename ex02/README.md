課題2 (2015/6/8)
================

受入保留 (Deferred Acceptance) アルゴリズムを実装してみる．

[Wikipedia の記事](http://ja.wikipedia.org/wiki/安定結婚問題)なり原論文

* D. Gale and L.S. Shapley,
  "[College Admissions and the Stability of Marriage](http://www.jstor.org/stable/2312726),"
  American Mathematical Monthly 69 (1962), 9-15

なりをよく読んでコードを書いてみる．

* 最初は one-to-one (結婚のケース) でよいが，最終的には many-to-one (college admission のケース) を扱う．
  (各 college には受入上限がある．)
* アルゴリズムはすでにあるのでただ書くだけだが，入力させるデータの構造をよくよく考える．
* 行く行くは「進振り方式の提案」のようなものに発展させたい．
* 提出方法：GitHub にリポジトリを「プッシュ」する．
* 締め切り：6月20日 (土)


##参考文献
* A.E. Roth,
  "[Deferred Acceptance Algorithms: History, Theory, Practice, and Open Questions](http://link.springer.com/article/10.1007/s00182-008-0117-6),"
  International Journal of Game Theory 36 (2008), 537-569


##データ構造 (2015/6/15)

いろいろなやり方があると思いますが，次のようなデータ構造を採用することにしましょう．

* 男性陣: `[0, 1, ..., m-1]`
* 女性陣: `[0, 1, ..., n-1]`

### 入力データ

* `m_prefs`: `m` x `(n+1)` の2次元配列  
  `m_prefs[i]` には男性 `i` が好きな女性の番号が順番に並べてある．
  ただし，`n` は "unmatched" を意味する．

* `f_prefs`: `n` x `(m+1)` の2次元配列  
  `f_prefs[j]` には女性 `j` が好きな男性の番号が順番に並べてある．
  ただし，`m` は "unmatched" を意味する．

たとえば，`m=4` として，`m_prefs[0]` が `[1, 2, 4, 3, 0]` だとしたら，
男性 `0` は「女性 `1` が一番好き，その次は女性 `2` が好き，その次は match しないのが好き
(女性 `3, 0` とペアになるくらいなら一人でいる方が好き)」であることを意味する．

### 出力データ

* `m_matched`: 長さ `m` の1次元配列  
  `m_matched[i]` は男性 `i` が match する女性の番号か `n` ("unmatched") が入る．
* `f_matched`: 長さ `n` の1次元配列  
  `f_matched[j]` は女性 `j` が match する男性の番号か `m` ("unmatched") が入る．


## 単体テスト

テストを作ったので，それが通るようにコードを書きましょう．

[test_matching.py](https://github.com/oyamad/matching/blob/45f0553515602c10bba55978211374197991c072/test_matching.py)
を作業フォルダにダウンロードする．
前提として

* 関数の名前は `deferred_acceptance`
* コードが書かれているファイルの名前は `matching.py`

となっているので，自分の命名にあわせて上記テスト・ファイルの相当箇所を書きかえるか，
自分の方の名前をテストの想定にあわせるかする．

ターミナルから

```
python test_matching.py
```

と実行する．

まずは `ERROR` が出ないようにする．
それから `FAIL` をつぶしていく．


## ランダム選好リスト

ランダムに選好リストを生成する関数を書いたので必要があれば使ってみてください．  
[matching_tools.py](https://github.com/oyamad/matching/blob/4e766839782aa2edf00d93620ca4d57cba7e667d/matching_tools.py)
を作業フォルダにダウンロードする．

* [使用例](http://nbviewer.ipython.org/github/oyamad/matching/blob/master/random_prefs.ipynb)


## パフォーマンス比較の結果 (2015/6/22)

* [結果](http://nbviewer.ipython.org/github/OyamaZemi/exercises2015/blob/master/ex02/competition.ipynb)
