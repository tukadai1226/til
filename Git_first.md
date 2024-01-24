# Git

### Gitって何のために使うの

ファイルのバージョンを管理するため

### ファイルのバージョンを管理すれば

ファイルの最新の状態がわかる

いつ誰が何を変更したかもわかる

以前の状態に戻せる

### GitHubとは

コードのホスティングサービス。

Gitでファイルの変更履歴をオンラインで扱ってくれるサービス。

**特徴**

プルリクエストで複数人開発

世界中のチームがGitHub上で開発(OSSなど)

### ターミナル頻出コマンド

ディレクトリの移動

```php
cd
```

ディレクトリの内容を表示する。

```php
ls
```

ディレクトリの新規作成

```php
mkdir
```

ファイルの削除

```php
rm
```

ファイルのコピー

```php
cp
```

ファイルの移動とファイル名の変更

```php
mv
```

ファイルの中身を表示

```php
cat
```

### GItのデータの保存の仕組み

Gitはファイル全てをスナップショットで保存している。

注意：差分ではない

!https://i.gyazo.com/8a455d3bfbb499b431e5a9aedfa8c2a4.png

スナップショットで保存しておけば差分の計算をしなくて済む分、早くブランチを切ったりマージする事ができる。

コミットが直前のコミットを記録しているので、コミットを辿ると以前の状態に戻す事ができる。

### ローカル

３つのエリアに分かれている。

ワークツリー　→　ステージ　→ リポジトリ

**ワークツリー**

ファイルを変更したりする手元の作業場のこと

**ステージ**

コミットする変更を準備する場所。

変更が完了したファイルとまだ作業途中のファイルがある場合、変更が完了したファイルをステージに追加することでステージに追加された分だけリポジトリに記録する仕組みになっている。

**リポジトリ**

スナップショットを記録(コミット)する場所

### Gitのデータ構造

ステージに上げるまで

①index.htmlをステージに追加する際はindex.htmlファイルを圧縮した圧縮indx.htmlファイルをリポジトリに保存する。

②圧縮ファイルができたら、今度はステージにあるインデックスというファイルにリポジトリのindex.htmlというファイルの中身は圧縮ファイルだということをマッピングした情報を保存する。(git add)

コミットするまで

③コミットするとインデックスのファイル構成を元にツリー１というファイルがリポジトリに作る。(git commit)

ツリー１はインデックスに記載されているディレクトリーのファイル構成を改めて保存したもの。

④ツリー１が作られるとコミット１を作成する。

コミット１はツリーのファイル名、作成者情報、日付、コミットメッセージが記録される。新しいファイルを追加した場合は一つ前のコミットを親コミットとして記録している。(履歴としてたどれるようにするため)

### Gitのデータ構造のまとめ

- リポジトリに圧縮ファイル、ツリー、コミットファイルを作成することでデータを保存している
- コミットが親コミットを持つことで変更履歴を辿る事ができる
- Gitの本質はデータを圧縮してスナップショットで保存している。

### 補足

Gitオブジェクト

git addやgit commitしたときに作られる圧縮ファイル、ツリーファイル、コミットファイルのことをGitオブジェクトと呼んでいる。

Gitオブジェクトは「.git/objects」ディレクトリの下に保存される。