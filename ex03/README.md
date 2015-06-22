課題3 (2015/6/22)
================

次は，(新たな関数を書くのではなく) [課題2](../ex02) で作った関数に many-to-one マッチング
(college admission のケース) を扱う機能を加えましょう．

* 提出方法：課題2で作ったリポジトリに「プッシュ」する．
* 締め切り：~~6月27日 (土)~~ 7月4日 (土)


## 多対一マッチング

次のような状況に限定することにしましょう：

* 学生は高々一つの大学に入る．
* 大学にはそれぞれ受け入れ上限がある．
* 各大学は (グループではなく) 学生それぞれに対して選好を持つ．
* とりあえず，学生側から提案するということにしましょう．

### 入力データ

学生の数 `m`，大学の数 `n` として，

* `prop_prefs`: `m` x `(n+1)` の2次元配列

* `resp_prefs`: `n` x `(m+1)` の2次元配列

* `caps`: 長さ `n` の1次元配列  
  `caps[j]` は大学 `j` の受入上限

(`prop_prefs`, `resp_prefs` はいままでの `m_prefs`, `f_prefs` と同じ．)

関数は

```python
def deferred_acceptance(prop_prefs, resp_prefs, caps=None):
    ...
```

のように書いて，`deferred_acceptance(prop_prefs, resp_prefs)` のように
`caps` 引数なしで呼び出されたら一対一としていままでと全く同じように処理するようにする．

### 出力データ

とりあえず以下のようなデータ構造を採用することにしましょう．

`caps` が指定されなければいままで通り

* `prop_matched`: 長さ `m` の1次元配列

* `resp_matched`: 長さ `n` の1次元配列

を返す
(`prop_matched`, `resp_matched` はいままでの `m_matched`, `f_matched` と同じ)．

`caps` が指定されたら次の3つを返す：

* `prop_matched`: 長さ `m` の1次元配列

* `resp_matched`: 長さ `L` の1次元配列  
  大学側が受け入れる学生をすべて列挙する．

* `indptr`: 長さ `n+1` の1次元配列  
  `resp_matched[indptr[j]:indptr[j+1]]` が大学 `j` が受け入れる学生のリスト．

ただし，`L` = `sum(caps)` です．

`indptr` は `np.cumsum(caps)` で得られる長さ `n` の1次元配列の先頭に `0` を加えたものです．
たとえば，

```python
indptr = np.empty(n+1, dtype=int)
indptr[0] = 0
np.cumsum(caps, out=indptr[1:])
```

で作ることができます．


## 単体テスト

[test_matching.py](https://github.com/oyamad/matching/blob/acbf748c1e57e76888ccb393fee4000e9bb92f10/test_matching.py)
に多対一マッチング用のテストを加えました．
作業フォルダにダウンロード，これが通るようにコードを書いていく．
