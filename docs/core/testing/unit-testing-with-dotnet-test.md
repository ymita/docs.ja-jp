---
title: "dotnet テストを使用した .NET Core での単体テスト | Microsoft Docs"
description: "dotnet テストを使用した .NET Core での単体テスト"
keywords: .NET, .NET Core
author: ardalis
ms.author: wiwagn
ms.date: 03/21/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdcdb812-6f13-4f20-9e90-0c0977937142
translationtype: Human Translation
ms.sourcegitcommit: 4a1f0c88fb1ccd6694f8d4f5687431646adbe000
ms.openlocfilehash: 3ca312509d7ba7a7759d1ac294f79cc359419c52
ms.lasthandoff: 03/22/2017

---

# <a name="unit-testing-in-net-core-using-dotnet-test"></a>dotnet テストを使用した .NET Core での単体テスト

このチュートリアルでは、単体テストの概念について学習するためにサンプル ソリューションを段階的に構築する対話型のエクスペリエンスを示します。 構築済みのソリューションを使用してチュートリアルに従う場合は、開始する前に[サンプル コードを参照またはダウンロード](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/unit-testing-using-dotnet-test/)してください。

### <a name="creating-the-source-project"></a>ソース プロジェクトの作成

シェル ウィンドウを開きます。 ソリューションを保持するための *unit-testing-using-dotnet-test* というディレクトリを作成します。 この新しいディレクトリ内に、*PrimeService* ディレクトリを作成します。 現時点のディレクトリ構造は次のようになっています。

```
/unit-testing-using-dotnet-test
    /PrimeService
```

*PrimeService* を現在のディレクトリにし、[`dotnet new classlib`](../tools/dotnet-new.md) を実行してソース プロジェクトを作成します。 *Class1.cs* の名前を *PrimeService.cs* に変更します。 テスト駆動開発 (TDD) を使用するため、`PrimeService` クラスのエラーが発生する実装を作成します。

```csharp
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate) 
        {
            throw new NotImplementedException("Please create a test first");
        } 
    }
}
```

### <a name="creating-the-test-project"></a>テスト プロジェクトの作成

*unit-testing-using-dotnet-test* ディレクトリに戻り、*PrimeServices.Tests* ディレクトリを作成します。 ディレクトリ構造は次のようになります。

```
/unit-testing-using-dotnet-test
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
```

*PrimeService.Tests* ディレクトリを現在のディレクトリにし、[`dotnet new xunit`](../tools/dotnet-new.md) を使用して新しいプロジェクトを作成します。 これで、テスト ライブラリとして xUnit を使用するテスト プロジェクトが作成されます。 生成されたテンプレートで、*PrimeServiceTests.csproj* のテスト ランナーが構成されます。

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0" />
  <PackageReference Include="xunit" Version="2.2.0" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0" />
</ItemGroup>
```

テスト プロジェクトには、単体テストを作成して実行するための、他のパッケージが必要です。 前の手順の `dotnet new` によって、xUnit と xUnit ランナーが追加されています。 ここで、プロジェクトに別の依存関係として `PrimeService` クラス ライブラリを追加します。 次の [`dotnet add reference`](../tools/dotnet-add-reference.md) コマンドを使用します。

```
dotnet add reference ../PrimeService/PrimeService.csproj
```

*PrimeService.Tests.csproj* ファイルを編集することもできます。 最初の `<ItemGroup>` ノードの下で直接、ライブラリ プロジェクトを参照する別の `<ItemGroup>` ノードを追加します。

```xml
<ItemGroup>
  <ProjectReference Include="..\PrimeService\PrimeService.csproj" />
</ItemGroup>
```

全体のファイルは GitHub の[サンプル リポジトリ](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService.Tests.csproj)で確認できます。

最終的なソリューションのレイアウトは次のようになります。

```
/unit-testing-using-mstest
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
        PrimeService
        PrimeServiceTests.csproj
```

## <a name="creating-the-first-test"></a>最初のテストの作成

ライブラリまたはテストを構築する前に、*PrimeService.Tests* ディレクトリで [`dotnet restore`](../tools/dotnet-restore.md) を実行します。 このコマンドにより、各プロジェクトの必要なすべての NuGet パッケージが復元されます。

TDD のアプローチでは、失敗するテストを 1 つ記述することを要求し、それを渡して、プロセスを繰り返します。 *PrimeService.Tests* ディレクトリから *UnitTest1.cs* を削除し、*PrimeService_IsPrimeShould.cs* という名前の新しい C# ファイルを作成します。コンテンツは次のようになります。

```csharp
using Xunit;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;

        public PrimeService_IsPrimeShould()
        {
            _primeService = new PrimeService();
        }

        [Fact]
        public void ReturnFalseGivenValueOf1()
        {
            var result = _primeService.IsPrime(1);

            Assert.False(result, $"1 should not be prime");
        }
    }
}
```

`[Fact]` 属性は、単一のテストとしてメソッドを表します。 [`dotnet test`](../tools/dotnet-test.md) を実行してテストとクラス ライブラリをビルドしてから、テストを実行します。 xUnit テスト ランナーには、テストを実行するためのプログラムのエントリ ポイントが含まれています。 `dotnet test` がテスト ランナーを開始し、テストを含むアセンブリを示すテスト ランナーにコマンド ライン引数を提供します。

テストが失敗します。 実装はまだ作成していません。 このテストを成功させるための最も簡単なコードを `PrimeService` クラスに記述します。

```csharp
public bool IsPrime(int candidate) 
{
    if (candidate == 1) 
    { 
        return false;
    } 
    throw new NotImplementedException("Please create a test first");
} 
```

*PrimeService.Tests* ディレクトリで、`dotnet test` をもう一度実行します。 `dotnet test` コマンドは `PrimeService` プロジェクトのビルドを実行してから、`PrimeService.Tests` プロジェクトのビルドを実行します。 両方のプロジェクトをビルドすると、この単一テストが実行されます。 成功します。

### <a name="adding-more-features"></a>他の機能の追加

テストが成功したので、他のテストも記述してみましょう。 素数に関する、いくつかの単純なケースが他にもあります (0、-1)。 これらは `[Fact]` 属性を使用して新しいテストとして追加できますが、すぐに煩雑になります。 一連の類似のテストを記述できるようになる、他の xUnit 属性があります。  `[Theory]` 属性は同じコードを実行するものの、異なる入力引数が含まれる一連のテストを表します。 `[InlineData]` 属性を使用して、そのような入力の値を指定することができます。 
 
新しいテストを作成する代わりに、この 2 つの属性を活用して、最も小さな素数である 2 未満の複数の値をテストする理論を 1 つ作成しましょう。

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.cs?name=Sample_TestCode)]

`dotnet test` を実行して、これらの 2 つのテストが失敗したとします。 すべてのテストを成功させるために、メソッドの先頭にある `if` 句を変更します。

```csharp
if (candidate < 2)
```

他のテスト、理論、コードをメイン ライブラリに追加して、反復を続けます。 [テストの最終版](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.cs)と[ライブラリの完全な実装](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService/PrimeService.cs)により終了します。

これで、小さなライブラリとそのライブラリの単体テストのセットが構築されました。 新しいパッケージとテストの追加がシームレスになり、アプリケーションの目標を解決するためにほとんどの時間と労力を注げるようにソリューションを構成しました。

