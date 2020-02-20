Title: 'KonoeStudio.Libs.DependencyInjection'
Published: 4/25/2019
Categories: プログラミング
Tags: C#, Nuget
Lead: 自作した.NET C#用の DI コンテナの使い方説明

---

先日、GitHub に自作の C#用 DI コンテナを MIT ライセンスで公開しました。

[![KonoeStudio.Libs.DependencyInjection - GitHub](../img/github/KonoeStudio.Libs.DependencyInjection.png)](https://github.com/18konoe/KonoeStudio.Libs.DependencyInjection)

.NET Framework 4.5 と.NET Standard 2.0 の両対応です。
:::{.alert .alert-warning}
こちらの DI コンテナではコンストラクタにインジェクトするタイプだけをサポートしています。
:::

## 導入

簡単に導入できるように Nuget パッケージで公開しています。
[KonoeStudio.Libs.DependencyInjection - Nuget](https://www.nuget.org/packages/KonoeStudio.Libs.DependencyInjection/)

## Demo 用クラスの紹介

DI コンテナに登録していくクラス達です。

### 1. なにもないクラス

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 3-11 Caption="INoMeanInterface, NoMeanClass" /?>

### 2. なにもないクラスを注入されるクラス（インターフェースなし）

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 13-22 Caption="HaveNoMeanConstructor" /?>

### 3. int と string をコンストラクタから注入できるクラス

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 24-42 Caption="ILiteralConstructor, LiteralConstructor" /?>

### 4. 1 と 3 のクラスをコンストラクタから注入できるクラス

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 43-60 Caption="IDependedConstructor, DependedConstructor" /?>

### 5. 1 と 3 と 4 のクラスと int をコンストラクタから注入できるクラス

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 61-87 Caption="IComplexConstructor, ComplexConstructor" /?>

## Demo1: 基本の登録と調達

はじめに最もシンプルな使い方を説明します。これから Demo 用クラス 2 の`HaveNoMeanConstructor`クラスのインスタンスを調達しようと思います。その時`HaveNoMeanConstructor`クラスのコンストラクタに指定している`INoMeanInterface`インターフェースには`NoMeanClass`クラスのインスタンスを DI コンテナに作ってもらいたいとします。

まず、この DI コンテナの窓口は`DiVendor`クラスのインスタンスです。そしてこの DI コンテナでは調達したいクラスは全て登録する必要があります。今回で言うと内部で要求される`INoMeanInterface`インターフェースを継承する`NoMeanClass`クラスと、`HaveNoMeanConstructor`クラスを`Register`メソッドで登録しておきます。この登録順は前後しても構いません。

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 19-35 /?>

このように書いて実行すると、`haveNoMeanConstructor`には、中に`NoMeanClass`クラスのインスタンスを持った`HaveNoMeanConstructor`クラスのインスタンスが代入されます。

:::{.alert .alert-info}
調達されるインスタンスは、何も設定しなければデフォルトでシングルトンかつ遅延作成されます。`Register`メソッドの引数から変更することが可能です。
:::

また、`DiVendor`を`Dispose`すると、それまでに調達してもらうために作られた全てのインスタンスを破棄するよう試みます。この関数で破棄してもらうには、登録するクラスが`IDisposable`インターフェースを継承している必要があります。

## Demo2: 複雑なクラス構成の対応

より複雑な状況にもある程度対応することができます。コンストラクタに注入する値は、デフォルトの自動解決の他に手動で決めておくことができます。それを実現するには`DiBlueprint`クラスのインスタンスを作成する必要があります。これは`DiArchitect`クラスのインスタンスから`CreateBlueprint<T>`メソッドを使って作成することができます。

`DiBlueprint`クラスにある`AppendArgumentInfo<T>`メソッドをチェインしていくことで、引数の設定を付属させることができます。ここではコンストラクタに int と string を持つ`LiteralConstructor`クラスに、インスタンス生成時に任意の値を代入するよう設定しています。ここで生成された`DiBlueprint`クラスのインスタンスを`Register`メソッドの引数に与えることで、調達時にその内容の通りに動作させることができます。

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 37-71 /?>

## Demo3: null を与えた場合の対応

`DiBlueprint`クラスの`AppendArgumentInfo<T>`メソッドの引数に`null`を与えた場合、DI コンテナが内部でインスタンスを調達する設定となります。実際に`null`を代入したい場合は、第二引数を`true`とすることで、DI コンテナに調達させずに`null`を代入させることができます。

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 73-104 /?>
