# StringBuilderTemporary

C#では、string同士の足し算だと temporaryでメモリを大量に確保されるため、System.Text.StringBufferの使用する方がパフォーマンス的にもメモリ的にも良いです。

ですが、既に出来上がってしまったものをイチイチ対応するのはとても大変です。
そこで、処理をまともにするコードを簡単に書けるためのクラスを今回用意しました


string str = "aaa" + 20 + "bbbb"; <br />
　　↓<br/>
string str = Sbt.i + "aaa" + 20 + "bbbb"; <br/>
とすることで、処理が大分まともになります。
（内部的にはStringBuilderを利用します。
　operatorで + 演算子の上書き、暗黙的castを書くことで処理向上を行っております)

Sbt.iは、ThreadSafeではありません。あと同じオブジェクトを使いまわします。
そういうケースで使いたい場合は、Sbt.Create()を代わりに使用してください。

# Stringでの加算処理の重さテスト
本プロジェクトには、Stringでの加算処理がドレだけ重いか確認するためにテストケースを用意しました。
testシーンを開いて実行してみてください。Profilerで確認するとドレほど重いかが確認できます。

画面をクリックすることで、今回の Sbt.iを入れるかどうかの変更が可能になっています。
画面中の「sbt Flag」がtrueになることで処理が格段に軽くなるのを確認できるかと思います。
