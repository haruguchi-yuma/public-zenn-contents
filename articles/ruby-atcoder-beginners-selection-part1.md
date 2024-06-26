---
title: "Rubyではじめる競技プログラミング入門 ~ AtCoder Beginners Selection編(前半)  ~"
emoji: "✨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Ruby", "競技プログラミング", "AtCoder"]
published: true
---

プログラミング言語Rubyを使って競技プログラミングを始めようシリーズのうちの1つです。AtCoderを始めたいと思った人が**おそらく最初に挑戦**するであろう「[AtCoder Beginners Selection](https://atcoder.jp/contests/abs)」を題材にしてRubyの文法の説明や、問題を解くにあたっての基本的な考え方を説明します。対象者はRubyを始めたばかりの人やRubyはある程度知っているが競技プログラミングをしたことがない方向けの、いわゆる**入門者向け**の記事となっています。


問題は全部で11問ありますが、この記事では前半部分にあたる以下の6問について説明していきます。

1. [PracticeA \- Welcome to AtCoder](https://atcoder.jp/contests/abs/tasks/practice_1)
1. [ABC086A \- Product](https://atcoder.jp/contests/abs/tasks/abc086_a)
1. [ABC081A \- Placing Marbles](https://atcoder.jp/contests/abs/tasks/abc081_a)
1. [ABC081B \- Shift only](https://atcoder.jp/contests/abs/tasks/abc081_b)
1. [ABC087B \- Coins](https://atcoder.jp/contests/abs/tasks/abc087_b)
1. [ABC083B \- Some Sums](https://atcoder.jp/contests/abs/tasks/abc083_b)

:::message
このまま読み進めていくと問題に対する考え方や解答例、解説などが見えてしまいます。まずは自分自身で解いていき行き詰まったりわからなくなったら該当の問題を読んでいくことをおすすめします。
:::

## [PracticeA \- Welcome to AtCoder](https://atcoder.jp/contests/abs/tasks/practice_1)
https://atcoder.jp/contests/abs/tasks/practice_1
### 問題の概要
整数 $a$, $b$, $c$ と文字列 $s$ が与えられるので整数の和と文字列を半角スペースでフォーマットして出力する問題です。


### 考え方
難しい考え方はなく、問題文で問われた通りに実装します。
この問題ではプログラミング言語における入力と出力が理解できてますか？ということが問われています。(多分ね)

### 解答例
:::details 解答例
```ruby
# 入力の受け取り
a = gets.to_i # 整数値として受け取る
c, d = gets.split.map(&:to_i) # 配列に分割して受け取る
s = gets.chomp # 文字列として受け取る

# 出力
puts "#{a + b + c} #{s}"
```
:::

#### <入力ついて>
入出力に関しては、過去記事を参照ください。
https://zenn.dev/haruguchi/articles/ruby-competitive-programming-io
ここでは1問目ということで詳しく説明していきます。

Rubyでは標準入力の受け取りに`gets`メソッドを使うことが多いです。`gets`メソッドは1行分の入力を**文字列として**受け取ります。
1行目の`a = gets.to_i`では`to_i`メソッドで整数に変換していることに注意してください。整数に変換しないと最後の出力で文字列同士の結合となってしまいます。

```ruby
# 🙅ダメな例(文字列のまま足し算してしまうと、、、)
a = "1"
b = "2"
c = "3"

puts "#{a + b + c}"
#=> "123" # 文字列の結合となってしまう
```

2行目は`split`メソッドを使って**空白文字区切り**の配列にしています。`split`メソッドは第1引数に区切り文字を指定できます。引数を省略した場合はデフォルト空白文字で区切るのでそれを利用しています。また`map`メソッドで配列の各要素を整数値(Integer)に変換しています。
 `array.map(&:to_i)` は `array.map { |num| num.to_i }`と等価です。入力例`2 3`の場合は以下のようになります。

```ruby
b, c = gets.split
#=> ["2", "3"] 文字列になる

b, c = gets.split.map(&:to_i)
         ↓
b, c = [2, 3]
b #=> 2
c #=> 3
```

3行目は文字列として入力を受け取っています。AtCoderでは`gets`メソッドで入力を受け取る場合末尾に改行文字`\n`が含まれます。なので`chomp`メソッドを使って末尾の改行文字を削除しています。

```ruby
# 入力 foo　の場合
gets
#=> "foo\n"

# chompを使って改行文字を削除
gets.chomp
#=> "foo"
```

#### <出力について>
最後の行は出力です。
出力には`puts`メソッドを使うことが多いです。Rubyではダブルクォートで囲まれた文字列のなかに`#{}`を埋め込むとカッコの中に式を埋め込むことができます。埋め込んだ式は評価され文字列として埋め込まれます。

```ruby
# 式　1 + 2 は　3に評価される
"#{1 + 2}"
#=> "3"
```
他の方法としては各要素を配列に入れて`join`メソッドで文字列を結合し、フォーマットする方法もあります。

```ruby
# 別の方法
# a = 1, b = 2, c = 3, s = "hello"の場合
puts [a + b + c, s].join(' ')
#=> 6 hello
```

## [ABC086A \- Product](https://atcoder.jp/contests/abs/tasks/abc086_a)
https://atcoder.jp/contests/abs/tasks/abc086_a
### 問題の概要
正整数 $a, b$ が与えられるので $a$ と $b$ の積が奇数ならを、`Odd`偶数なら　`Even`を出力する問題です。

### 考え方
この問題では条件分岐を利用して解きましょう。

### 解答例
:::details 解答例
```ruby
# 入力の受け取り（整数に変換)
a, b = gets.split.map(&:to_i)

if (a * b).odd? # 奇数かどうか判定
  puts 'Odd'
else # 奇数でないなら偶数
  puts 'Even'
end
```
:::
#### <偶数か奇数かの判定(偶奇判定)>
`odd?`メソッド**奇数かどうか**を判定するメソッドで、レシーバの整数が奇数のとき`true`、偶数のとき`false`を返します。もちろん専用のメソッドを使わずに`(a * b) % 2 != 0`として、2で割り切れるかどうかで奇数を判定しても良いです。
また、よく似たメソッドとして偶数を判定するメソッド`even?`もあります。

#### <条件分岐 if式 と 三項演算子>
「Aの場合はこう、それ以外は ......」といった条件分岐に関する処理をするときはif式が使えます。
今回は奇数かどうか条件式で判定し、それ以外(つまり偶数)の場合をelse節の中で処理しています。
```ruby
# if式の書き方
if 条件式
  # true　だった場合の処理
else
  # false　だった場合の処理
end
```


Rubyにおける`if`は文ではなく式なので値を返します。なので、以下のように変数で値を変数で受け取る書き方もできます。(というか実務などではこのように書くことのほうが多い)

```ruby
# a = 1, b = 2 の場合
result =
  if (a * b).odd? # <----------- ここから
    'Odd'
  else
    'Even'
  end             # <----------- ここまで　の結果をresultに代入

p result #=> 'Odd'
```

また三項演算子を使って書くことも可能です。

```ruby
puts (a*b).add? ? 'Odd' : 'Even'
```

三項演算子は`条件式 ? 真の場合の処理 : 偽の場合の処理`という書き方をします。条件式や処理が長い場合は読みにくのでif式を使うことが多いですが、逆に条件式や処理がシンプルな場合は1行でかけるので便利です。競技プログミングでは積極的に使っていきます。

## [ABC081A \- Placing Marbles](https://atcoder.jp/contests/abs/tasks/abc081_a)
https://atcoder.jp/contests/abs/tasks/abc081_a
### 問題の概要
3つのマスには`1`か`0`が書かれていて`1`のマスにはビー玉を置く。ビー玉が置かれたマスの個数を求める問題。

### 考え方
問題文を言い換えると、入力の中に`1`がいくつあるか答える問題です。よって`1`を数えましょう。

### 解答例
:::details 解答例
```ruby
# この場合chompはなくても影響ないが基本的にあると安心
s = gets.chomp
puts s.count('1')
```
:::

`String#count`メソッドは引数に渡した文字列をカウントしてくれます。今回は1をカウントしています。

## [ABC081B \- Shift only](https://atcoder.jp/contests/abs/tasks/abc081_b)
https://atcoder.jp/contests/abs/tasks/abc081_b
### 問題の概要
以下の操作が何回できるかを答える問題。

入力で受け取る$A_{1}, A_{2}, ...... , A_{N}$が
- 全て偶数なら2で割る
- そうでないなら操作終了

### 考え方
言われた通りに実装します。
「**数列の要素が全て偶数か？**」という判定が真(true)の間だけ操作を繰り返し、操作した回数を変数に保存していきましょう。数列に対してループ処理が必要になってきます。本当は計算量とかの考慮も必要ですが、今回は大丈夫なので考えないことにします。

### 解答例
:::details 解答例
```ruby
# 入力
n = gets.to_i
a = gets.split.map(&:to_i)

# 操作回数を記録しておく変数(初期値0)
cnt = 0

# whileは条件式が真の間だけ処理を繰り返す制御構文
while a.all?(&:even?)
  cnt += 1
  a = a.map { |num| num /= 2 } # 全ての要素を2割って変数に代入し直す
end

puts cnt
```
:::
#### < while 条件が真の間繰り返す>
> 「数列の要素が全て偶数か？」という判定が真(true)の間だけ操作を繰り返し、操作した回数を変数に保存していきましょう。

ある条件が真の間処理を繰り返すという場合は`while`が使えます。
```ruby
while 条件式
  # 条件式がtrueの間はずっと繰り返される
end
```

注意点としては条件式がずっと`true`だと無限ループに陥るので**必ずどこかで偽になることを確かめて**から使いましょう。

条件式の部分では`all?`メソッドを使っています。これは配列の全ての要素がtrueであればtrue, そうでなければfalseを返します。ブロックを渡した時はブロックを評価してtrueかどうかをチェックします。
`all?(&:even?)`は`all? { |num| num.even? }`と等価です。なので、解答例では全ての要素が偶数かどうかを調べています。

### 別解
別解として2進法を利用した短い解き方がありますが、自慢したいだけなのでリンクにしておきます。[提出 \#54153491 \- AtCoder Beginners Selection](https://atcoder.jp/contests/abs/submissions/54153491)


## [ABC087B \- Coins](https://atcoder.jp/contests/abs/tasks/abc087_b)
https://atcoder.jp/contests/abs/tasks/abc087_b
### 問題の概要
500円玉を$A$枚、100円玉を$B$枚、50円玉を$C$枚持っていて、ちょうど$X$円にする方法が何通りあるか答える問題。

### 考え方
制約を見ると
>　X は 50 の倍数である

とあるので**ちょうど$X$円にならないパターンは存在しません。**

たとえば、500円玉を2枚、100円玉を3枚、50円玉を4枚持っていて100円にする方法は

- 500円玉2枚だけ使う方法
  - `500 * 2 = 1000円`
- 500円玉1枚、100円玉3枚、 50円玉4枚だけ使う方法
  - `500 + 100 * 3 + 50 * 4 = 500 + 300 + 200 = 1000円`

の2通りがあります。

このように人間であればなんとなく頭を使って直感的に解くことができますが、コンピュータに計算させる時には全てのパターンをコンピュータに調べさせるのが有効です。これを全探索といいます。日常的には総当たりと言われるやつですね。

人間なら時間のかかる総当たりもコンピューターなら比較的早く計算できるので「**全探索できないか？**」は常に頭に入れて考えます。難しい問題になると全探索をすると実行時間制限(2秒が多い)を超えてしまう場合がありいつでも全探索できるとは限りません。そんな時は**計算量**の見積もりが必要になってきますが、これも必要になった時に説明します。

### 解答例
:::details 解答例
```ruby
# 入力の受け取り(整数値に変換)
coin_a, coin_b, coin_c, x = Array.new(4) { gets.split.map(&:to_i) }

# 答えが何通りあるかを表す変数 ans (answerの略)
ans = 0
(0..coin_a).each do |a| # 500円玉が0枚、1枚、2枚, ..., a枚と調べる
  (0..coin_b).each do |b| # 100円玉が0枚、1枚、2枚, ..., b枚と調べる
    (0..coin_c).each do |c| # 100円玉が0枚、1枚、2枚, ..., c枚と調べる
      ans += 1 if 500 * a + 100 * b + 50 * c == x # ちょうどX円となる場合答えを増やす
    end
  end
end

puts ans
```
:::

#### <全探索の方法>
RubyのRangeオブジェクトは文字や整数の範囲を表します。`0..10`なら整数0~10までを表しますし、`'a'..'c'`なら文字列'a'から'c'までを表します。Rangeオブジェクトに対して`each`メソッドを使うとループ処理が行えます。

```ruby
(0..5).each do |num|
 puts num
end

#=> 0
#=> 1
#=> 2
#=> 3
#=> 4
#=> 5
```

ループ処理を入れ子にすることで各硬貨の枚数の組み合わせを全探索します。

```ruby
# 500円玉2枚, 100円玉3枚, 50円玉2枚の場合

(0..2).each do |a|
  (0..3).each do |b|
    (0..2).each do |c|
      p [a, b, c] # わかりやすいように配列に入れてデバッグ
    end
  end
end
# 左から500円玉,100円玉,50円玉の枚数の組み合わせ
#=> [0, 0, 0]
#=> [0, 0, 1]
#=> [0, 0, 2]
#=> [0, 1, 0]
#=> [0, 1, 1]
#=> [0, 1, 2]
#=> [0, 2, 0]
#=> [0, 2, 1]
#=> [0, 2, 2]
#=> [0, 3, 0]
#=> [0, 3, 1]
#=> [0, 3, 2]
#=> [1, 0, 0]
#=> [1, 0, 1]
#=> [1, 0, 2]
#=> [1, 1, 0]
#=> [1, 1, 1]
#=> [1, 1, 2]
#=> [1, 2, 0]
#=> [1, 2, 1]
#=> [1, 2, 2]
#=> [1, 3, 0]
#=> [1, 3, 1]
#=> [1, 3, 2]
#=> [2, 0, 0]
#=> [2, 0, 1]
#=> [2, 0, 2]
#=> [2, 1, 0]
#=> [2, 1, 1]
#=> [2, 1, 2]
#=> [2, 2, 0]
#=> [2, 2, 1]
#=> [2, 2, 2]
#=> [2, 3, 0]
#=> [2, 3, 1]
#=> [2, 3, 2]
```

ループ処理には他にも`upto`メソッドを使うこともできます。

```ruby
0.upto(2) do |a|
  p a
end

#=> 0
#=> 1
#=> 2
```

詳しくはRubyリファレンスマニュアルの繰り返しの項を参照してください。
https://docs.ruby-lang.org/ja/latest/doc/spec=2fcontrol.html

#### <後置if>
if式の別の構文として後置ifというものがあります。
`真のときに実行する式 if 条件式`

今回は`ans += 1 if (合計金額) == x`と合計金額がX円の場合に答えを1増やすという処理をしています。


## [ABC083B \- Some Sums](https://atcoder.jp/contests/abs/tasks/abc083_b)

### 問題の概要
前半最後の問題です。

$1$以上$N$以下の整数のうち、10進法での各桁の和が$A$以上$B$以下であるものの総和を求める問題です。

ちょっと問題文がわかりにくいですね。1つずつ見ていきましょう。

### 考え方
たとえば、問題文の入力例1の`N=20 A=2 B=5`の場合
1以上20以下の整数の各桁の和と条件に一致するかの対応表を作ってみます。

|元の整数| 各桁の和 | 2以上5以下かどうか |
| --- | --- | :-: |
| 1 | 1 | NG |
| 2 | 2 | 🙆‍♀️**OK** |
| 3 | 3 | 🙆‍♀️**OK** |
| 4 | 4 | 🙆‍♀️**OK** |
| 5 | 5 | 🙆‍♀️**OK** |
| 6 | 6 | NG |
| 7 | 7 | NG |
| 8 | 8 | NG |
| 9 | 9 | NG |
| 10 | 1 (= 1 + 0) | NG |
| 11 | 2 (= 1 + 1) | 🙆‍♀️**OK** |
| 12 | 3 (= 1 + 2) | 🙆‍♀️**OK** |
| 13 | 4 (= 1 + 3) | 🙆‍♀️**OK** |
| 14 | 5 (= 1 + 3) | 🙆‍♀️**OK** |
| 15 | 6 (= 1 + 3) | NG |
| 16 | 7 (= 1 + 3) | NG |
| 17 | 8 (= 1 + 3) | NG |
| 18 | 9 (= 1 + 3) | NG |
| 19 |10 (= 1 + 3) | NG |
| 20 | 2 (= 2 + 0) | 🙆‍♀️**OK** |

このように1からNまでの**全てのパターン**を計算し判定すると条件に合う元の整数は`2, 3, 4, 5, 11, 12, 13, 15, 20`であることがわかります。これらの総和を求めると答えが求まります。
これは前回と同じ全探索ですね。

### 解答例
:::details 解答例
```ruby
# 入力の受け取り
n, a, b = gets.split.map(&:to_i)

# A以上B以下の数を入れておくための変数
results = []
# 1からNまでの全探索(ループ)
(1..n).each do |num|
  total = num.digits.sum # 各桁の和を求める
  # A以上B以下であれば配列に挿入
  results << num if a <= total && total <= b
end

puts results.sum
```
:::

#### <各桁に分ける>
整数`123`を`1`と`2`と`3`に分けるにはRubyでは`digits`メソッドが使えます。これは整数を各桁に分けた配列に変換してくれます。注意点としては一の位、十の位、　... という順番になっています。

```ruby
123.digits #=> [3, 2, 1]
```

このメソッドを使わない場合の方法も示しておきます。
整数を10で割ったときの余りが一の位と等しくなることを利用します。
```ruby
num = 123
results = []
while num > 0
  results << num % 10
  num /= 10
end

p results #=> [3, 2, 1]
```

## 最後に
いかがでしたでしょうか？AtCoder Beginners Selectionの前半6問を説明しました。

今回は簡単のため計算量の概念などの説明は省きました。一部のB問題やC問題以降になると実行時間に間に合わせるために計算量を見積もり、効率の良いアルゴリズムを考える問題が出てきます。後半をお楽しみに。
