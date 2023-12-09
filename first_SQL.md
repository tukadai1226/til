### データベースマネジメントシステム(DBMS)

データベースを管理するコンピュータシステムのこと

### データベースが必要な理由

大量のデータから必要なデータを取り出すため

多人数でデータを共有して利用するため

データの保護

## データベースの種類

### リレーショナルデータベース(RDB)

現在最も広く使用されているデータベース

エクセルシートのように列と行からなる２次元の表形式でデータを管理

SQLという専用の言語を使用してデータを操作する。

例）MySQL、MariaDB、PostgreSQL、OracleDB、SQLServer、DB2

### キー・バリュー型データストア(KVS)

検索に使う(Key)と値(Value)の組み合わせだけの簡単なデータを保存する。

例）memachaed、Redis

### オブジェクト指向データベース(OODB)

データとそれを操作する処理をまとめてオブジェクトという単位で管理する。

※現在はあまり使われていない

### XMLデータベース(XMLDB)

インターネット上でやり取りされるデータ形式XMLを、大量かつ高速に扱う事ができる。

※現在はあまり使われていない

## SQL

データベース、テーブル、行や列を扱うための言語をSQLと呼ぶ。SQLは何の略でも無いとされるが、IBMが開発したSEQUELが由来とされる。

```sql
select*from users where age >=20;
```

年齢が20歳以上のユーザーをデータベースから取得するという意味になる。

### 標準SQLと、SQLの方言

**標準SQL**

ISO(国際標準化機構)で定められたSQLのこと。

**SQLの方言**

各データベース製品で、標準SQLへの対応はまちまち。(標準SQLで使える機能が使えない場合がある)

### SQLの記述ルール

1.**大文字、小文字の区別がない**

※小文字で書くのがスタンダード

```sql
select * from users;

SELECT * FROM USERS;

SELEct * fRom UserS;
```

2.**SQL文の最後にはセミコロンをつける**

**3.文字と日付はシングルクォーテーションで囲う**

```sql
select * from users where name = 'Nakamura';

select * from users where created_at >= '2023-01-01- 00:00';
```

**4.単語は半角スペースまたは改行で区切る**

```sql
select * from users;

select
*
form
users;
```

**5.SQLは半角で書く。全角で書くとエラーになる。**

**6.区切りの空白はいくつあっても良い**

## クエリ(query、問い合わせ)

データの検索や更新、削除、抽出などの要求をデータベースに送信すること。

例）ユーザー情報を取得するために、クエリを投げる。

## データ型

データベースでは、テーブルを作成する時に、それぞれの列(カラム・フィールド)に指定した形式のデータしか、入力できないように設定する。

この時指定するデータの形式をデータ型という。

例）数値型、文字列型、日付・時刻型

### 数値型

int型(イント、インテジャー)：整数(-2147483648〜2147483647)

tinyint型(タイニーイント)：とても小さな整数(-128〜127)

float型(フロート)：小さい浮動小数点数(簡単にいうと小数点以下を含む数値を扱うとき)

double(ダブル)普通サイズの浮動小数点数

※実務上

- 整数型はint
- 整数の中でも真偽値を扱いたいときや、127以下の数字を扱う時はtinyint
- 少数を扱う時はdouble型を使う事が多い
- floatはfloatを使う理由が明確に説明できる時は使う

### 文字列型

char型(キャラ)：固定長の文字列255文字まで、文字列を格納するときに指定したながさにスペースが埋め込まれる。例)商品コードで5桁固定”CD123”　定義方法：char(5)

varchar型(バーキャラ)：可変長の文字列255文字まで。例)nakamura@example.com　定義方法：varchar(255)

text型(テキスト)：長い文字列65535文字まで。

※実務上

255文字まではvarcharそれ以上はテキストとする事が多い

### 日付・時刻型

date型(デイト)：日付’1000-01-01’から’9999-12-31’

datetime(デイトタイム)：日付と時刻’1000-01-01　00:00:00.000000’から’9999-12-31 23:59:59:58.999999’

time型(タイム)：時刻’-838:59:59’から’838:59:59’

### SQL文

```sql
use mydb;
```

どのデータベースを使うか指定

```sql
from users;
```

どのテーブル名を使うか指定

```sql
select * from users;
```

どの列を取得するかを指定(今回はすべての列を取得するので*)

```sql
select id, last_name from users;
```

列を指定して取得するSQL文

※アスタリスクを使ってすべての行を取得するよりも、必要な列に絞ってデータを取得する方が高速に実行できる。

```sql
select name as 名前, price as 価格 from products;
```

列に別名をつける(nameカラム名を名前に変える、priceカラムを価格に変える)

※asは省略する事ができる。

```sql
select price * 1.08
```

列の値に対して演算を行う。

### where句

条件を指定して値を取得できる。

```sql
select name,price from products where price >= 9000; 
```

(価格が9800円以上の商品と名前を抽出)

代表的な演算子

```sql
-- 1) products テーブルから全件取得
select * from products;
-- 2) idが1の行を取得
select * from products where id = 1;
-- 3) 名前が「商品0003」の行を取得
select * from products where name = '商品0003';
-- 4) priceが1000より大きい行を取得
select * from products where price > 1000;
-- 5) price が1000より小さい行を取得
select * from products where price < 1000;
-- 6) priceが100でない行を取得
select * from products where price <> 100;
-- 7) 次のようにもかけます。
select * from products where price != 100;
-- 8) idが1か2か3の行を取得
select * from products where id in(1, 2, 3);
-- 9)idが1か2か3ではない行を取得
select * from products where id not in(1, 2, 3);
-- 10)priceがnullではない行を取得
select * from products where price is not null;
-- 11)priceがnullの行を取得
select * from products where price is null;
-- 12)priceが1000から1900の行を取得
select * from products where price between 1000 and 1900;
-- 13)これは次のようandを使っても書ける。andは、論理積。条件AもBも成り立つ時にtrue（真）。
select * from products where price >= 1000 and price <= 1900;
-- 14)or （論理和）も使える。条件Aか条件Bが一つ以上成り立つ場合にtrue
-- 価格が1000円又は2000円の行を取得
select * from products where price = 1000 or price = 2000;
```

### like句

パターンマッチングによる絞り込みができる。

### ワイルドカード文字

- ‘%’：0文字以上の任意の文字列
- ‘_’：任意の1文字

例)

’中%’　’中’で始まる文字列

‘%中%’　’中’を含む文字列

‘%子’　’子’で終わる文字列

‘_ _子’ 何かしらの2文字から始まり、子で終わる文字列

```sql
select * from users where last_name like '%中%';
```

中が含まれている名字を抽出

### limit句

取得件数を制限できる。

```sql
select * from products limit 10;
```

商品を10件取得

```sql
select * from products limit 0,10;
```

商品を0から(1件目から)10件取得

```sql
select * from products limit 10,10;
```

商品を10件目から10件取得

### **注意**

**本番環境で直接データベースを直接操作する場合はlimitを使わず負荷をかけてしまうクエリを送るとデータベースが止まってしまいサービスが止まる恐れがある**。

取得は1000件ぐらいで様子を見るのが無難。１テーブル10万件を超えるあたりからパフォーマンスが低下する。

### コメントアウト

テキストとしてSQL自体は書かれているが、SQLの実行時に書かれていないとみなす。

**用途**

あとで見返したときに困らないようにメモ書きするため。

検証のために一時的に特定のSQLをむこうにしたい。

**種類**

1.「- - 」

その行のテキストを無効にする

1. 「/**/」

囲んだ箇所を無効にする。
