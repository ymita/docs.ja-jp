---
title: "チュートリアル: Office のプログラミング (C# および Visual Basic) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- Office, programming in Visual Basic and C#
- Office programming [C#]
- Office programming [Visual Basic]
ms.assetid: 519cff31-f80b-4f0e-a56b-26358d0f8c51
caps.latest.revision: 46
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f93a5403660ca850d6650a1a6406395dfa2cc2e5
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-office-programming-c-and-visual-basic"></a>チュートリアル: Office のプログラミング (C# および Visual Basic)
Visual Studio には、Microsoft Office のプログラミングを改善する C# および Visual Basic の新機能が導入されています。 各言語に、他の言語では既に存在する機能が追加されています。  
  
 C# の新機能には、名前付き引数と省略可能な引数、型が `dynamic` の戻り値、COM プログラミングでの `ref` キーワードを省略し、インデックス付きプロパティにアクセスする機能などがあります。 Visual Basic の新機能には、自動実装プロパティ、ラムダ式内のステートメント、コレクション初期化子などがあります。  
  
 両方の言語で、ユーザーのコンピューターにプライマリ相互運用機能アセンブリ (PIA) を配置せずに COM コンポーネントとやり取りするアセンブリを配置できる型情報を埋め込むことができます。 詳細については、「[チュートリアル: マネージ アセンブリからの型の埋め込み](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)」を参照してください。  
  
 このチュートリアルでは、Office プログラミングのコンテキストで新機能を示しますが、これらの多くは一般的なプログラミングにも便利です。 このチュートリアルでは、最初に Excel ブックを作成する Excel アドイン アプリケーションを使用します。 次に、ブックへのリンクを含む Word 文書を作成します。 最後に、PIA の依存関係をオンおよびオフにする方法を示します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを実行するには、コンピューターに Microsoft Office Excel 2013 (またはバージョン 2007 以降) および Microsoft Office Word 2013 (またはバージョン 2007 以降) がインストールされている必要があります。  
  
 
          [!INCLUDE[windowsver](../../../csharp/programming-guide/interop/includes/windowsver_md.md)] よりも前のオペレーティング システムを使用している場合は、[!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] がインストールされていることを確認します。  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-set-up-an-excel-add-in-application"></a>Excel アドイン アプリケーションをセットアップするには  
  
1.  Visual Studio を起動します。  
  
2.  **[ファイル]** メニューの **[新規作成]**をポイントし、 **[プロジェクト]**をクリックします。  
  
3.  **[インストールされたテンプレート]** ペインで、**[Visual Basic]** または **[Visual C#]** を展開し、**[Office]** を展開して、**[2013]** (あるいは **[2010]** または **[2007]**) をクリックします。  
  
4.  **[テンプレート]** ペインで **[Excel 2013 アドイン]** (あるいは **[Excel 2010 アドイン]** または **[Excel 2007 アドイン]**) をクリックします。  
  
5.  **[テンプレート]** ペインの上部で、**[ターゲット フレームワーク]** ボックスに **[.NET Framework 4]** またはそれ以降のバージョンが表示されていることを確認します。  
  
6.  必要に応じて、**[名前]** ボックスにプロジェクトの名前を入力します。  
  
7.  **[OK]** をクリックします。  
  
8.  **ソリューション エクスプローラー**に新しいプロジェクトが表示されます。  
  
### <a name="to-add-references"></a>参照を追加するには  
  
1.  **ソリューション エクスプローラー**で、プロジェクトの名前を右クリックし、**[参照の追加]** をクリックします。 **[参照の追加]** ダイアログ ボックスが表示されます。  
  
2.  **[アセンブリ]** タブの **[コンポーネント名]** 一覧で、**Microsoft.Office.Interop.Excel** バージョン 15.0.0.0 (または Excel 2010 の場合はバージョン 14.0.0.0、Excel 2007 の場合はバージョン 12.0.0.0) を選択し、Ctrl キーを押しながら **Microsoft.Office.Interop.Word** バージョン 15.0.0.0 (または Word 2010 の場合はバージョン 14.0.0.0、Word 2007 の場合はバージョン 12.0.0.0) を選択します。  アセンブリが表示されない場合は、アセンブリがインストールされ、表示されることの確認が必要になることがあります (「[方法: Office のプライマリ相互運用機能アセンブリをインストールする](http://msdn.microsoft.com/library/92948fcc-76c6-4b08-ba63-cab59dd60eb1)」を参照)。  
  
3.  **[OK]** をクリックします。  
  
### <a name="to-add-necessary-imports-statements-or-using-directives"></a>必要な Imports ステートメントまたはディレクティブの使用を追加するには  
  
1.  **ソリューション エクスプローラー**で、**[ThisAddIn.vb]** または **[ThisAddIn.cs]** ファイルを右クリックし、**[コードの表示]** をクリックします。  
  
2.  次の `Imports` ステートメント (Visual Basic) または `using` ディレクティブ (C#) が含まれていない場合は、コード ファイルの先頭に追加します。  
  
     [!code-cs[csOfficeWalkthrough#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_1.cs)]
     [!code-vb[csOfficeWalkthrough#1](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_1.vb)]  
  
### <a name="to-create-a-list-of-bank-accounts"></a>銀行口座の一覧を作成するには  
  
1.  **ソリューション エクスプローラー**で、プロジェクト名を右クリックし、**[追加]** をクリックしてから **[クラス]** をクリックします。 Visual Basic を使用している場合は Account.vb、C# を使用している場合は Account.cs という名前をクラスに付けます。 **[追加]**をクリックします。  
  
2.  `Account` クラスの定義を次のコードに置き換えます。 クラス定義では、Visual Studio 2010 の Visual Basic の新機能である*自動実装プロパティ*を使用します。 詳細については、「[自動実装プロパティ](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)」を参照してください。  
  
     [!code-cs[csOfficeWalkthrough#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_2.cs)]
     [!code-vb[csOfficeWalkthrough#2](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_2.vb)]  
  
3.  2 つの口座を含む `bankAccounts` 一覧を作成するには、次のコードを追加する、ThisAddIn.vb または ThisAddIn.cs の `ThisAddIn_Startup` メソッドに追加します。 リスト宣言では、Visual Studio 2010 の Visual Basic の新機能である*コレクション初期化子*を使用します。 詳細については、「[コレクション初期化子](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)」を参照してください。  
  
     [!code-cs[csOfficeWalkthrough#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_3.cs)]
     [!code-vb[csOfficeWalkthrough#3](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_3.vb)]  
  
### <a name="to-export-data-to-excel"></a>データを Excel にエクスポートするには  
  
1.  同じファイル内で、次のメソッドを `ThisAddIn` クラスに追加します。 このメソッドは、Excel ブックを設定し、データを Excel ブックにエクスポートします。  
  
     [!code-cs[csOfficeWalkthrough#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_4.cs)]
     [!code-vb[csOfficeWalkthrough#4](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_4.vb)]  
  
     C# の 2 つの新しい機能は、このメソッドで使用されます。 これら両方の機能は、Visual Basic で既に存在します。  
  
    -   [Add](http://go.microsoft.com/fwlink/?LinkId=210910) メソッドには、特定のテンプレートを指定する*省略可能なパラメーター*があります。 [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp_dev10_long_md.md)] の新機能であるオプションのパラメーターでは、パラメーターの既定値を使用する場合は、そのパラメーターの引数を省略することができます。 前の例では引数が渡されないため、`Add` は、既定のテンプレートを使用して、新しいブックを作成します。 以前のバージョンの C# では、同等のステートメントには、プレースホルダーの引数 `excelApp.Workbooks.Add(Type.Missing)` が必要です。  
  
         詳細については、「[名前付き引数と省略可能な引数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)」を参照してください。  
  
    -   [Range](http://go.microsoft.com/fwlink/?LinkId=210911) オブジェクトの `Range` および `Offset` プロパティでは*インデックス付きプロパティ*機能を使用します。 この機能では、次の一般的な C# 構文を使用して COM 型からこれらのプロパティを使用することができます。 また、インデックス付きプロパティを使用すると、`Value` プロパティを使用せずに、`Range` オブジェクトの `Value2` プロパティを使用できます。 `Value` プロパティはインデックス付きですが、インデックスはオプションです。 次の例では、省略可能な引数とインデックス付きプロパティは連携しています。  
  
         [!code-cs[csOfficeWalkthrough#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_5.cs)]  
  
         以前のバージョンの言語では、次の特殊な構文が必要です。  
  
         [!code-cs[csOfficeWalkthrough#6](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_6.cs)]  
  
         独自のインデックス付きプロパティを作成することはできません。 この機能では、既存のインデックス付きプロパティの使用のみがサポートされます。  
  
         詳細については、「[方法: COM 相互運用機能を使用したプログラミングでインデックス付きプロパティを使用する](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)」を参照してください。  
  
2.  次のコードを `DisplayInExcel` の末尾に追加して、コンテンツに合わせて列の幅を調整します。  
  
     [!code-cs[csOfficeWalkthrough#7](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_7.cs)]
     [!code-vb[csOfficeWalkthrough#7](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_7.vb)]  
  
     これらの追加機能では、C# 2010 の別の新機能である、[dynamic](../../../csharp/language-reference/keywords/dynamic.md) 型がある場合と同様に Office などの COM ホストから返される `Object` 値の処理を示します。 これは、**[相互運用機能型の埋め込み]** が既定値の `True` に設定されている場合、または同様に、アセンブリが [/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md) コンパイラ オプションによって参照されている場合に発生します。 `dynamic` 型では既に Visual Basic で使用できる遅延バインディングが可能であり、Visual C# 2008 以前のバージョンの言語で必要な明示的なキャストを回避します。  
  
     たとえば、`excelApp.Columns[1]` は `Object` を返し、`AutoFit` は Excel の [Range](http://go.microsoft.com/fwlink/?LinkId=210911) メソッドであるとします。 `dynamic` がない場合、`excelApp.Columns[1]` のインスタンスとして、`Range` によって返されたオブジェクトをキャストしてから、`AutoFit` メソッドを呼び出す必要があります。  
  
     [!code-cs[csOfficeWalkthrough#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_8.cs)]  
  
     相互運用機能型の埋め込みの詳細については、このトピックの後半の「PIA 参照を検索するには」および「PIA の依存関係を復元するには」の手順を参照してください。 `dynamic` の詳細については、「[dynamic (C# リファレンス)](../../../csharp/language-reference/keywords/dynamic.md)」または「[dynamic 型の使用 (C# プログラミング ガイド)](../../../csharp/programming-guide/types/using-type-dynamic.md)」を参照してください。  
  
### <a name="to-invoke-displayinexcel"></a>DisplayInExcel を起動するには  
  
1.  `ThisAddIn_StartUp` メソッドの末尾に、次のコードを追加します。 `DisplayInExcel` に対する呼び出しには、2 つの引数が含まれています。 最初の引数は、処理する口座の一覧の名前です。 2 番目の引数は、データの処理方法を定義する複数行のラムダ式です。 各口座の `ID` 値と `balance` 値が隣接するセルに表示され、残高が 0 より少ない場合、行が赤で表示されます。 複数行のラムダ式は、Visual Basic 2010 の新しい機能です。 詳細については、「[ラムダ式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)」を参照してください。  
  
     [!code-cs[csOfficeWalkthrough#9](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_9.cs)]
     [!code-vb[csOfficeWalkthrough#9](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_9.vb)]  
  
2.  プログラムを実行するには、F5 キーを押します。 口座からのデータを含む Excel ワークシートが表示されます。  
  
### <a name="to-add-a-word-document"></a>Word 文書を追加するには  
  
1.  `ThisAddIn_StartUp` メソッドの末尾に次のコードを追加して、Excel ブックへのリンクを含む Word 文書を作成します。  
  
     [!code-cs[csOfficeWalkthrough#10](../../../csharp/programming-guide/interop/codesnippet/CSharp/walkthrough-office-programming_10.cs)]
     [!code-vb[csOfficeWalkthrough#10](../../../csharp/programming-guide/interop/codesnippet/VisualBasic/walkthrough-office-programming_10.vb)]  
  
     このコードは、COM プログラミングで `ref` キーワードを省略する機能、名前付き引数、省略可能な引数など、C# の新機能のいくつかを示します。 Visual Basic でこれらの機能は既に存在します。 [PasteSpecial](http://go.microsoft.com/fwlink/?LinkId=147099) メソッドには 7 つのパラメーターがあります。これらはすべて省略可能な参照パラメーターとして定義されます。 Visual C# 2010 より前では、意味のある値を渡すことができない場合でも、7 つのパラメーターの引数として使用するオブジェクト変数を定義する必要がありました。 名前付き引数と省略可能な引数を使用すると、アクセスするパラメーターを名前で指定し、これらのパラメーターにのみ引数を渡すことができます。 この例では、引数は、クリップボードのブックへのリンクを作成する必要があること (`Link` パラメーター)、およびリンクがアイコンとして Word 文書に表示されること (`DisplayAsIcon` パラメーター) を示すために渡されます。 Visual C# 2010 では、これらの引数の `ref` キーワードを省略することもできます。 Visual C# 2008 の以下のコード セグメントを Visual C# 2010 で必要な単一の行と比較します。  
  
  
### <a name="to-run-the-application"></a>アプリケーションを実行するには  
  
1.  F5 キーを押してアプリケーションを実行します。 Excel が起動し、`bankAccounts` の 2 つの口座からの情報が格納されたテーブルが表示されます。 Excel テーブルへのリンクを含む Word 文書が表示されます。  
  
### <a name="to-clean-up-the-completed-project"></a>完成したプロジェクトをクリーンアップするには  
  
1.  Visual Studio で、**[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。 それ以外の場合は、コンピューターで Excel を起動するたびにアドインが実行されます。  
  
### <a name="to-find-the-pia-reference"></a>PIA 参照を検索するには  
  
1.  もう一度アプリケーションを実行しますが、**[ソリューションのクリーン]** はクリックしません。  
  
2.  **[スタート]** メニューの **[すべてのプログラム]** をクリックします。 次に、**[Microsoft Visual Studio 2013]** をクリックして、**[Visual Studio Tools]** をクリックし、**[Visual Studio コマンド プロンプト (2013)]** をクリックします。  
  
3.  [Visual Studio コマンド プロンプト (2013)] ウィンドウに「`ildasm`」と入力し、Enter キーを押します。 [IL DASM] ウィンドウが表示されます。  
  
4.  [IL DASM] ウィンドウの **[ファイル]** メニューで **[開く]** をクリックします。 **[Visual Studio 2013]** をダブルクリックし、**[プロジェクト]** をダブルクリックします。 プロジェクトのフォルダーを開き、bin/Debug フォルダーで*プロジェクト名*.dll を見つけます。 *プロジェクト名*.dll をダブルクリックします。 新しいウィンドウに、他のモジュールおよびアセンブリへの参照に加えて、プロジェクトの属性が表示されます。 名前空間 `Microsoft.Office.Interop.Excel` と `Microsoft.Office.Interop.Word` はアセンブリに含まれています。 Visual Studio 2013 の既定では、コンパイラは、参照 PIA からアセンブリに必要な型をインポートします。  
  
     詳細については、「[方法 : アセンブリの内容を表示する](http://msdn.microsoft.com/library/fb7baaab-4c0d-47ad-8fd3-4591cf834709)」を参照してください。  
  
5.  **MANIFEST** アイコンをダブルクリックします。 プロジェクトによって参照される項目を含んでいるアセンブリの一覧を含むウィンドウが表示されます。 `Microsoft.Office.Interop.Excel` および `Microsoft.Office.Interop.Word` は一覧に含まれていません。 プロジェクトに必要な型がアセンブリにインポートされているため、PIA への参照は必要ありません。 これにより、配置が容易になります。 PIA がユーザーのコンピューター上に存在している必要がなく、アプリケーションに特定のバージョンの PIA を配置する必要がないので、すべてのバージョンに必要な API が存在している場合は、複数のバージョンの Office を使用するようにアプリケーションを設計できます。  
  
     PIA の配置が不要になったため、以前のバージョンを含む複数のバージョンの Office で動作する高度なシナリオで、アプリケーションを作成できます。 ただし、これは、コードで、使用している Office のバージョンでは利用できない APIを使用していない場合にのみ機能します。 特定の API が以前のバージョンで利用可能かどうかは常に明確ではないため、以前のバージョンの Office の使用はお勧めできません。  
  
    > [!NOTE]
    >  Office 2003 より前の Office では、PIA は発行されません。 そのため、Office 2002 以前のバージョンの相互運用機能アセンブリを生成する唯一の方法は、COM 参照のインポートです。  
  
6.  マニフェスト ウィンドウとアセンブリ ウィンドウを閉じます。  
  
### <a name="to-restore-the-pia-dependency"></a>PIA の依存関係を復元するには  
  
1.  **ソリューション エクスプローラー**で、**[すべてのファイルを表示]** ボタンをクリックします。 **[参照]** フォルダーを展開し、**[Microsoft.Office.Interop.Excel]** を選択します。 F4 キーを押して **[プロパティ]** ウィンドウを表示します。  
  
2.  **[プロパティ]** ウィンドウで、**[相互運用機能型の埋め込み]** プロパティを **[True]** から **[False]** に変更します。  
  
3.  `Microsoft.Office.Interop.Word` について、この手順の手順 1 と 2 を繰り返します。  
  
4.  C# では、`Autofit` メソッドの最後で `DisplayInExcel` への 2 つの呼び出しをコメント化します。  
  
5.  プロジェクトが正常に実行することを確認するには、F5 キーを押します。  
  
6.  アセンブリ ウィンドウを開くには、前の手順の手順 1 ～ 3 を繰り返します。 `Microsoft.Office.Interop.Word` と `Microsoft.Office.Interop.Excel` は、埋め込まれたアセンブリの一覧には表示されません。  
  
7.  **MANIFEST** アイコンをダブルクリックし、参照アセンブリのリストをスクロールします。 `Microsoft.Office.Interop.Word` と `Microsoft.Office.Interop.Excel` の両方が一覧に表示されています。 アプリケーションが Excel と Word の PIA を参照し、**[相互運用機能型の埋め込み]** プロパティを **[False]** に設定しているため、両方のアセンブリがエンド ユーザーのコンピューター上に存在する必要があります。  
  
8.  Visual Studio で、**[ビルド]** メニューの **[ソリューションのクリーン]** をクリックして、完成したプロジェクトをクリーンアップします。  
  
## <a name="see-also"></a>関連項目  
 [自動実装プロパティ](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [自動実装プロパティ](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)   
 [コレクション初期化子](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [オブジェクト初期化子とコレクション初期化子](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [省略可能なパラメーター](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [位置と名前による引数渡し](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [名前付き引数と省略可能な引数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [事前バインディングと遅延バインディング](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [dynamic 型の使用](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [ラムダ式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [ラムダ式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [方法: COM 相互運用機能を使用したプログラミングでインデックス付きプロパティを使用する](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)   
 [チュートリアル: Microsoft Office アセンブリからの型情報の埋め込み](http://msdn.microsoft.com/library/85b55e05-bc5e-4665-b6ae-e1ada9299fd3)   
 [チュートリアル: マネージ アセンブリからの型の埋め込み](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)   
 [チュートリアル : 初めての Excel 用 VSTO アドインの作成](http://msdn.microsoft.com/library/a855e2be-3ecf-4112-a7f5-ec0f7fad3b5f)   
 [COM 相互運用](../../../visual-basic/programming-guide/com-interop/index.md)   
 [相互運用性](../../../csharp/programming-guide/interop/index.md)
