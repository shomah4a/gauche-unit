このgistは [TDD Advent Calender 2012](http://atnd.org/events/33846), 12/10 のエントリとして書かれたような気がします。昨日、12/9のエントリは [@setoazusa](https://twitter.com/setoazusa) さんの [JUnitテストの実行環境をバージョンアップする時の落とし穴 #tddadventjp – ふぃーるどのーつ@はてな](http://d.hatena.ne.jp/setoazusa/20121209/1355056720) だったそうです。

そう、だれがJSTに従うと言った?

さて、私はいま社内読書会として **計算機プログラムの構造と解釈、通称SICP** ってやつを読んでいて、ちょうど2章がもう少しで終わるかなーというところなんですが、その中ではデータ構造の操作だったりをする手続き(「関数」とは言わない)を作ったりして、それを「accumulatorを使うように直してみよう」みたいな感じで、 **手続きの構造を変更** させられるわけで、もちろんそのときは、 **手続きの入出力が変わらない** ようにしなければならない。ようするに **リファクタリング以外の何者でもない**わけですよ、これは。

ということで、何が必要かって、 **テストコードが必要** ですよね、よく訓練されたおまいらには当然ですね。

という感じで書いたのがコレなので、動かすには、gaucheがインストールされている状態で

```
git clone git://gist.github.com/4251773.git gist-4251773
cd gist-4251773
make test
```

してみてください。テストがこけてれば、makeもこけます。試しに、テストコードの9,10行目のコメントを外してみてください。例外が投げられないという例外が投げられ、makeがこけます：

```scheme
(assert (lazy (assert (+ 1 2) (is 3)))
 (raises "expected: 2, but: was 3")) ; error
```

gaucheにも組み込みでtestなんとかがあるらしいけど、このへんはアレですね、使い慣れた感じのほうがね。再発明とか気にしないの。これは訓練である。これは訓練である。

以上、よろしくお願い致します。

12/11は [@bash0C7](http://twitter.com/bash0C7) 先生による [] ハイプレッシャーを克服するためのテスト駆動開発の重要な「二歩目」(http://d.hatena.ne.jp/bash0C7/20121211/TddAdventJp) です。大変いい話ですね。

ポイントは、raises matcherのときのactualはlazyなんとかにしないといけないっぽいところです?