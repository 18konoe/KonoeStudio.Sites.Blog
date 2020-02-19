Title: 'KonoeStudio.Libs.DependencyInjection'
Published: 4/25/2019
Tags: プログラミング
Lead: 自作した.NET C#用のDIコンテナの使い方説明

---

先日、GitHubに自作のC#用DIコンテナをMITライセンスで公開しました。
[KonoeStudio.Libs.DependencyInjection - GitHub](https://github.com/18konoe/KonoeStudio.Libs.DependencyInjection)

.NET Framework 4.5と.NET Standard 2.0の両対応です。
:::{.alert .alert-warning}
こちらのDIコンテナではコンストラクタにインジェクトするタイプだけをサポートしています。
:::

## 導入
簡単に導入できるようにNugetパッケージで公開しています。
[KonoeStudio.Libs.DependencyInjection - Nuget](https://www.nuget.org/packages/KonoeStudio.Libs.DependencyInjection/)

## Demo用クラスの紹介
DIコンテナに登録していくクラス達です。

### 1. なにもないクラス

<?# Gist-embed 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 3-11 Caption="INoMeanInterface, NoMeanClass" /?>
