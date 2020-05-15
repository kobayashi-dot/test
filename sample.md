# サンプルテキスト

コンピュータは同じことを繰り返すのが得意だ。その特性は、プログラミングをしていく上でとても役にたつ。

ここではfor文による繰り返し処理を解説する。

## for文の使い方

Javaで条件を満たしている間、繰り返し処理を行う文。繰り返し文のひとつが、「for文」だ。

for文が他の繰り返し文と異なっているのは、繰り返しのための初期化、条件、更新が書き方で明確にされている点だ。

基本は以下のようになる。

```java
for (初期化; 条件式; 更新) {
  文;
}
```

実際のコードは次のようになる。1から10までの数字を順番に表示するコードだ。

```java
for (int number = 1; number <= 10; number++) {
  System.out.println(number + "回目");
}
```

- 「int number = 1;」でnumberという変数を初期化する（numberに1を代入）
- 「number <= 10;」が条件で、満たしている間繰り返し処理を行う
- 「number++」は1ループごとに1ずつ加える（更新する）

### for文の要素

for文による繰り返しがどのような順序で実行されていくのか、順を追ってみてみよう。最初に初期化が行われ、その後繰り返しとなる。

### 初期化

初期化のコードが最初に1回だけ実行される。基本的に、for文の中で使われる変数の初期化を行う。

- 複数の変数の宣言を書くことができる。
- 複数の初期化のための式を書くこともできる。式は、左から右に実行される。
- 初期化が必要でなければ(for文の外で初期化を行っていれば)、何も書かなくてもよい。

```java
(初期化;) //for文の中か外どちらかで変数の初期化を行う
for ((初期化); 条件式; 更新) {
  文;
}
```

### 繰り返し

初期化コードが実行された後、以下の4項目の繰り返し処理が開始される。

1. 式の評価：条件式がtrueであれば、次の処理が実行される。式がない場合も次の処理が実行される。しかし、条件式がfalseならば、繰り返しは終わる。
1. 文の実行：文が実行される。`continue`, `break`, `return`のいずれかがある場合、対応した処理を行う。
    - `continue`：以降の処理を行わず、3.の処理に移る。
    - `break`：以降の文の処理を行わず、ループ外の処理に移る。
    - `return`:すべての処理を終了する。
1. 更新：複数の更新のための式を書くことができる。この場合の式は、主に繰り返しの中で使われるカウンターなどの変数を更新する式である。式は、左から右に実行される。また、何も書かないこともできる。この場合は、何も更新されない。
1. ループ：ステップ1から繰り返す。

`continue`と`break`と`return`を利用したコードをそれぞれ以下に記す。

continueの場合

```java
int sum = 0;
for (int number = 1; number <= 10; number++) {
  if(number < 10){ //numberが10未満のとき実行される
    continue　//変数を更新してループの最初からを繰り返す
  }
    sum += number;
    System.out.plintln(sum);
}
System.out.plintln("continue");

//結果
10
continue
```

breakの場合

```java
int sum = 0;
for (int number = 1; number <= 10; number++) {
    sum += number;
    System.out.plintln(sum);
    break //1つ外の中括弧で覆われた部分(この場合for文のループ)から抜け出す。
}
System.out.plintln("break");

//結果
1
break
```

returnの場合

```java
int sum = 0;
for (int number = 1; number <= 10; number++) {
    sum += number;
    System.out.plintln(sum);
    return //このメソッドを終了させる。
}
System.out.plintln("return"); //returnとコンソールに表示する部分だがメソッドが終了しているため実行されない。

//結果
1
```

***

例として、for文で1から10までの数の合計を求めるコードを取り上げて、ステップごとに何が起きているかを見る。

```java
int sum = 0;
for (int number = 1; number <= 10; number++) {
    sum += number;
}
```

最初は、sumが0で初期化される。その後からfor文が始まる。繰り返しの1回目だけ初期化が行われ、式の評価、文の実行、更新と続く。最後は繰り返しが11回目のとき、式のnumberが10を超えるので評価がfalseになり、繰り返しは終了する。

| 繰り返し | ステップ |    コード     |   実行結果   |
| :------: | :------: | :-----------: | :----------: |
|  1回目   |  初期化  |  number = 1   |   number→1   |
|          | 式の評価 | number <= 10  |     true     |
|          | 文の実行 | sum += number |   sum:0→1    |
|          |   更新   |   number++    |  number:1→2  |
|  2回目   | 式の評価 | number <= 10  |     true     |
|          | 文の実行 | sum += number |   sum:1→3    |
|          |   更新   |   number++    |  number:2→3  |
|    …     |    …     |       …       |      …       |
|  10回目  | 式の評価 | number <= 10  |     true     |
|          | 文の実行 | sum += number |  sum:45→55   |
|          |   更新   |   number++    | number:10→11 |
|  11回目  | 式の評価 | number <= 10  |    false     |

### 無限ループ

初期化、式、更新に何も書かないでおくことができる。そうすると、for文は無限ループになる。つまり、条件が何もないので無限に繰り返される。無限ループの繰り返しを中断する方法は、`break`と`return`だ。

```java
for( ; ; ){
  //実行コード
}
```

## for文のブロック内・外変数

「for文の繰り返し」の「初期化」項目でfor文の中か外どちらかで変数の初期化を行う。と説明したが、違いと使用法を説明する。

### forのブロック内・外変数の扱い方

for文の中で宣言を行った変数は、ブロック内変数として扱われ、for文の外で使用することが出来ない。

Javaのfor文のブロック内で使う変数がどこで宣言できるかというと、以下のようにfor文の初期化、for文のブロック内、for文の外で宣言できる。

```java
[for文の外]
for ( [for文の初期化] ;  ;  ) { // '{'がブロックの始まり
    [for文のブロック内]
}   // '}'がブロックの終わり
```

for文の初期化で宣言された変数を考える。以下のfor文はnを1から10までカウントアップして、最後のnの値をnumberに残すようにしている。

```java
for (int n = 1, number = 0; n <= 5; n++) {
  number = n;
  System.out.println("number:" + number);
}

//結果
number:5
```

以下の場合、変数numberは初期化で宣言した後0が代入され、ブロック内で変数として使われる。この使い方は問題ない。しかし、numberをfor文の繰り返しが終わった後、for文のブロックの外で使おうとするとエラーが起きる。

```java
for (int n = 1,　number = 0; n <= 5; n++) {
    number = n;
}
System.out.println("number:" + number); // この文は、エラーになる。

//結果
エラー
```

for文のブロック内で宣言された変数numberの場合、ブロック内で使うことは可能だが、for文の外で使うことはできない。以下のコードではエラーが起きる。変数numberが有効な範囲(スコープ)は、変数が宣言されたブロック内の残りの部分なのである。

```java
for (int n = 1; n <= 5; n++) {
    int number = n;
}
System.out.println("number:" + number); // この文は、エラーになる

//結果
エラー
```

for文のブロックの中で設定された値の変数をfor文の外で使う場合、for文が始まる前で宣言を行う。以下のようにfor文の前で変数numberを宣言して、for文のブロック内で設定することでfor文内の値をfor文の外に持ち出せる。

```java
int number = 0;
for (int n = 1; n <= 5; n++) {
    number = n;
}
System.out.println("number:" + number);

//結果
numbar:5
```

しかし、ブロック外で変数の宣言を行うとミスが起こりやすくなる。以下は2つのfor文で計算した結果をnumberに格納してそれぞれ表示するという目的で作成したプログラムだ。今回の場合だとnumberに格納されているのは2つ目のループの中身なので全部同じ結果が表示される。

```java
int number = 0;
for (int a = 1; a <= 1; a++) {   //1つ目のループ
    number = a;
}
for (int b = 1; b <= 10; b++) {  //2つ目のループ
    number = b;
}

System.out.println("numberA:" + number); //numberの中身は2つ目のループのもの
System.out.println("numberB:" + number); //numberの中身は2つ目のループのもの

//結果
numbarA:10
numbarB:10
```

2つのfor文で計算した結果を適切に表示するためにはどのようなプログラムにすればいいのか。それを以下に示す。

```java
int number = 0;
for (int a = 1; a <= 1; a++) {
    number = a;
}
System.out.println("numberA:" + number); //numberの中身は1つ目のループのもの

for (int b = 1; b <= 10; b++) {  
    number = b;
}
System.out.println("numberB:" + number); //numberの中身は2つ目のループのもの

//結果
numbarA:1
numbarB:10  
```

## 拡張for文の使い方

中身が分かっている配列(例：`int[] numbers = {1,2,3,4,5}`)やコレクション(例：`List<> numbers = new ArrayList<>()`)のループの場合、拡張for文を利用することでコンパクトに書くことができる。

書き方の基本は以下の通りである。

```java
for (型 変数名:式)
  文;
}
```

### 基本的なfor文を使った配列表示のサンプル

まずは通常のfor文を利用した配列の表示を以下に記す。

```java
int numbers[] = {1, 2, 3};
for (int index = 0; index < numbers.length; index ++) { //lengthメソッドを使いnumbersの長さ分ループさせる。
    System.out.println("number = " + numbers[index]); //配列のindex番目の要素を表示する。
}

//結果
number = 1
number = 2
number = 3

```

### 拡張for文を使った配列表示のサンプル

```java
int numbers[] = {1, 2, 3};
for (int number : numbers) {
    System.out.println("number = " + number); //numberに配列の値を代入し、配列の要素数だけnumberの表示を繰り返す。
}

//結果
number = 1
number = 2
number = 3
```

### コレクション(List)のサンプル

このサンプルプログラムは、Listのインスタンスに追加された値を拡張for文ですべて表示している。

```java
List<Integer> numbers = new ArrayList<Integer>(); //List型の変数numbersを宣言しインスタンスを生成する。
for (int number = 1; number <= 10; number++) { //numbersに1から10の値を追加する。
    numbers.add(number);
}

for (int number : numbers) { //numberに配列の値を代入し、配列の要素数だけnumberの表示を繰り返す。
    System.out.println("number = " + number);
}
```

拡張for文は書き方がシンプルになるだけでなく配列の要素数だけ繰り返してくれるので、配列の要素数が変化しても同じ処理を使い回すことができる。

## 二重for文の使い方

for文の中にはfor文を入れ子にして使用することができ、これを使う場面は多い。例えば、多次元配列を出力する際によく使用される。

### for文を入れ子にするメリット

今回は九九の計算結果をfor文を使って出力することにする。
以下は入れ子を用いて作成したプログラムである。

```java
for (int n1 = 1; n1 <= 9; n1++ ){ //n1を1で初期化し9になるまでカウントアップする
    for (int n2 = 1; n2 <= 9; n2++){ //n2を1で初期化し9になるまでカウントアップする
        System.out.print(n1 + "x" + n2 +"=" + (n1 * n2) + " "); //n1*n2の計算式と結果の表示を行う
        }
        System.out.println(""); //改行を行う
}

//結果
1x1=1 1x2=2 1x3=3 1x4=4 1x5=5 1x6=6 1x7=7 1x8=8 1x9=9
2x1=2 2x2=4 2x3=6 2x4=8 2x5=10 2x6=12 2x7=14 2x8=16 2x9=18
3x1=3 3x2=6 3x3=9 3x4=12 3x5=15 3x6=18 3x7=21 3x8=24 3x9=27
4x1=4 4x2=8 4x3=12 4x4=16 4x5=20 4x6=24 4x7=28 4x8=32 4x9=36
5x1=5 5x2=10 5x3=15 5x4=20 5x5=25 5x6=30 5x7=35 5x8=40 5x9=45
6x1=6 6x2=12 6x3=18 6x4=24 6x5=30 6x6=36 6x7=42 6x8=48 6x9=54
7x1=7 7x2=14 7x3=21 7x4=28 7x5=35 7x6=42 7x7=49 7x8=56 7x9=63
8x1=8 8x2=16 8x3=24 8x4=32 8x5=40 8x6=48 8x7=56 8x8=64 8x9=72
9x1=9 9x2=18 9x3=27 9x4=36 9x5=45 9x6=54 9x7=63 9x8=72 9x9=81
```

次に同様のプログラムをfor文の入れ子なしで作成する。

```java
for (int n1 = 1, n2 = 1; n2 <= 9; number2++){ //変数n1を宣言し、初期値の"1"を代入する。変数n2を宣言し、初期値の1を代入する。n2を9になるまでカウントアップする
    System.out.print(n1 + "x" + n2 + "=" + (n1 * n2) + " "); //n1*n2の計算式と結果の表示を行う
}
System.out.println(""); //改行を行う

for (int n1 = 2, n2 = 1; n2 <= 9; number2++){ //変数n1の初期値が"2"になる以外は1つ目のループと同様。以下のループも変数n1の初期値が1ずつ増加して9になるまで同様に続くので省略。
    System.out.print(n1 + "x" + n2 + "=" + (n1 * n2) + " ");
}
System.out.println("");

for (int n1 = 3, n2 = 1; n2 <= 9; number2++){
    System.out.print(n1 + "x" + n2 + "=" + (n1 * n2) + " ");
}
System.out.println("");

//～～省略～～

for (int n1 = 9, n2 = 1; n2 <= 9; number2++){
    System.out.print(n1 + "x" + n2 + "=" + (n1 * n2) + " ");
}
System.out.println("");//改行を行う


//結果
入れ子を用いて計算した場合と同じなので省略。
```

入れ子を用いることでプログラムを大幅に省略出来ることが見て取れる。

## まとめ

ここではJavaのfor文の使い方について説明した。

必ず使用する文法なので確実に理解すること。
