## データ型とは

変数に格納するデータの種類のこと。

### データ型はなぜ必要か

コンピュータのリソースを効率よく使うための仕組み。

プログラミングを実行すると、変数の値はコンピューターのメモリに保存される。データ型があることで、このメモリを効率よく使用することができる。

データ型が決まっていればあらかじめメモリのキャパシティを最適に保てる。

| データ型 | bit数 | 値 |
| --- | --- | --- |
| boolean | 1bit | true あるいは false |
| char | 16bit | 文字 |
| byte | 8bit | 整数（扱える範囲は -128～127） |
| short | 16bit | 整数（扱える範囲は-32,768～32,767） |
| int | 32bit | 整数（扱える範囲は-2,147,483,648～2,147,483,647） |
| long | 64bit | 整数（扱える範囲は-9223372036854775808～9223372036854775807） |
| float | 32bit | 小数（精度低） |
| double | 64bit | 小数（精度高） |

## 動的型付け言語と静的型付け言語

### 動的型付け言語

プログラムの実行時に変数のデータ型を決定する方式である。

どのような値が変数に代入されたかによって変数のデータ型が柔軟に変更され、そのデータ型によって処理が行われる。

### 静的型付け言語

変数の型を最初に決定したら変更できない仕組み。

最初に整数として宣言した変数に、文字列として代入しようとするとエラーになる。

処理が高速になったり、データ型の不整合によるエラーを未然に検知できる。

### 変数を理解する

```java
class Main {
  public static void main(String[] args) {
    int radius;
    radius = 5;
    System.out.println(radius * radius * 3.14);
  }
}
```

class Main{・・・}

Mainクラスを定義している。

public static void main(String[] args) {

Java プログラムのエントリーポイントであるmainメソッド。このメソッドは、プログラムが実行されるときに最初に呼び出されプログラムの処理がここから始まる。

public: アクセス修飾子で、このメソッドがどの範囲からでもアクセス可能であることを指名している。

static: このメソッドが静的メソッドであることを示している。静的メソッドはインスタンスを作成せず呼び出すことができる。

void: メソッドが返り値を返さないことを示す。mainメソッドは実行されたプログラムの終了を意味する時には戻り値を返さない。

main: メソッドの名前

String[] args: mainメソッドの引数として、文字列の配列(String型の配列) が受け取られる。

argsは変数名でこの配列にはプログラムの起動時に渡されたコマンドライン引数が格納される。

System.out.println: ()で囲んだ中身を出力するメソッド。Rubyでいうputs

int radius; int型の変数radiusを宣言する。

※Java２位は「型推論」と呼ばれる仕組みがあり、宣言に関するコードを省略することができる。

### 型推論を理解する

```java
var 変数名 = 値
```

このようにvarを使用し宣言を行い、初期値を代入する。

この記述をすると値の種類によってデータ型が推論され、推論されたデータ型で宣言が行われる。

```java
System.out.println(((Object)radius).getClass().getSimpleName());
```

データ型を確認するためのコード

## 演算子の種類

| 演算子 | 使い方 | 意味 |
| --- | --- | --- |
| + | a + b | 加算 |
| - | a - b | 減算 |
| * | a * b | 乗算 |
| / | a / b | 除算 |
| % | a % b | 剰余 |

## 比較演算子の種類

| 演算子 | 使い方 | 意味 |
| --- | --- | --- |
| == | a == b | aとbが等しい場合true |
| < | a < b | aがbより小さい場合true |
| > | a > b | aがbより大きい場合true |
| <= | a <= b | aがb以下の場合true |
| >= | a >= b | aがb以上の場合true |
| != | a!= b | aとbが等しくない場合true |

# 配列とリスト

## Rubyの配列との違い

Javaの配列は、格納する要素の数を最初に決める必要があり、かつ後で要素数を変更することができない。

要素を増やす場合は、サイズの大きな配列を新たに作成して元のデータをコピーするか、ArrayListというリストの一種を使用する。

ArrayListは要素の数を変更できる配列のようなもので、ウェブアプリケーション開発でよく使用される。

```java
class Main {
  public static void main(String[] args){
     int[] scores;
    scores = new int[3];

    scores[0] = 1;
    scores[1] = 5;
    scores[2] = 10;

    System.out.println(scores[0]);
    System.out.println(scores[1]);
    System.out.println(scores[2]);
  }
}
```

１、配列の宣言を行う

int型のscoresという配列を宣言する。

２、配列の要素を作成し、配列の中に代入する。

scores  という配列にint型の要素を3つ作成し、int型の配列scoresに代入する。

３、配列の要素に値を代入する。

## 配列のさまざまな記述方法を理解する

### 配列の宣言と同時に要素の作成を行う方法

```java
int[] scores = new int[3];
```

### 配列の宣言時に型推論を使用する方法

```java
var scores = new int[3];
```

### 配列の宣言から値の代入まですべて同時に行う方法

```java
int[] scores = {1,5,10};
```

## ArrayListとは

「可変長配列」を使用するための仕組み。要素数を変更できる配列のこと。

```java
import java.util.ArrayList;

class Main {
  public static void main(String[] args){
     ArrayList<Integer> scores = new ArrayList<Integer>();

    scores.add(1);
    scores.add(5);
    scores.add(10);

    System.out.println(scores.get(0));
    System.out.println(scores.get(1));
    System.out.println(scores.get(2));
  }
}
```

１、ライブラリをインポートする。

```java
import java.util.ArrayList;
```

２、ArrayListの宣言をする。

```java
ArrayList<データ型> scores = new ArrayList<データ型>();
```

３、ArrayListに値を代入する。

```java
scores.add(1);
```

４、ArrayListから要素を取り出す。

```java
scores.get(0)
```

```java
ArrayList<Integer> scores = new ArrayList<Integer>();
```

ここで行なっている動作は２つ

- 整数(integer)を格納するArrayListを「scores」という名称で宣言
- ArrayListの要素を作成

そして代入している。

## Rubyの配列との違い

Javaの配列は、格納する要素の数を最初に決める必要があり、かつ後で要素数を変更することができない。

要素を増やす場合は、サイズの大きな配列を新たに作成して元のデータをコピーするか、ArrayListというリストの一種を使用する。

ArrayListは要素の数を変更できる配列のようなもので、ウェブアプリケーション開発でよく使用される。

```java
class Main {
  public static void main(String[] args){
     int[] scores;
    scores = new int[3];

    scores[0] = 1;
    scores[1] = 5;
    scores[2] = 10;

    System.out.println(scores[0]);
    System.out.println(scores[1]);
    System.out.println(scores[2]);
  }
}
```

１、配列の宣言を行う

int型のscoresという配列を宣言する。

２、配列の要素を作成し、配列の中に代入する。

scores  という配列にint型の要素を3つ作成し、int型の配列scoresに代入する。

３、配列の要素に値を代入する。

## 配列のさまざまな記述方法を理解する

### 配列の宣言と同時に要素の作成を行う方法

```java
int[] scores = new int[3];
```

### 配列の宣言時に型推論を使用する方法

```java
var scores = new int[3];
```

### 配列の宣言から値の代入まですべて同時に行う方法

```java
int[] scores = {1,5,10};
```

## ArrayListとは

「可変長配列」を使用するための仕組み。要素数を変更できる配列のこと。

```java
import java.util.ArrayList;

class Main {
  public static void main(String[] args){
     ArrayList<Integer> scores = new ArrayList<Integer>();

    scores.add(1);
    scores.add(5);
    scores.add(10);

    System.out.println(scores.get(0));
    System.out.println(scores.get(1));
    System.out.println(scores.get(2));
  }
}
```

１、ライブラリをインポートする。

```java
import java.util.ArrayList;
```

２、ArrayListの宣言をする。

```java
ArrayList<データ型> scores = new ArrayList<データ型>();
```

３、ArrayListに値を代入する。

```java
scores.add(1);
```

４、ArrayListから要素を取り出す。

```java
scores.get(0)
```

```java
ArrayList<Integer> scores = new ArrayList<Integer>();
```

ここで行なっている動作は２つ

- 整数(integer)を格納するArrayListを「scores」という名称で宣言
- ArrayListの要素を作成

そして代入している。

## 問１

### パッケージとは

「パッケージ」とは、Javaのクラス(ソースファイル)を目的に合わせてグループ化した単位のことを言う。

通常は、大規模なアプリケーションの開発をする場合に管理を容易にするために使用される。

大規模なプログラムを開発していくと、他のプログラマーが既に作成済みのクラスを利用していく場合があります。そのときに作成したクラスが作成済みのクラスと名前が同じである場合があり、プログラムの中で混在させて使わなければならない時もある。このときに、Javaではパッケージ（package）という仕組みにより、同じ名前であっても自身で作成したクラスと他者の作成したクラスを区別し使用することがでる。
