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
