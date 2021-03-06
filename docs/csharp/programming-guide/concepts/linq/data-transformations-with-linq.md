---
title: "LINQ によるデータ変換 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- LINQ [C#], data transformations
- source elements [LINQ in C#]
- joining multiple inputs [LINQ in C#]
- multiple outputs for one output sequence [LINQ in C#]
- subset of source elements [LINQ in C#]
- data sources [LINQ in C#], data transformations
- data transformations [LINQ in C#]
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: f8db095447a2360f275215c5190f479d11288d3c
ms.contentlocale: ja-jp
ms.lasthandoff: 05/10/2017

---
# <a name="data-transformations-with-linq-c"></a>LINQ によるデータ変換 (C#)
[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] で行うことができるのは、データの取得だけではありません。 データ変換のための強力なツールとしても使用できます。 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] クエリを使用することにより、ソース シーケンスを入力として使用し、さまざまな方法で加工して新しい出力シーケンスを作成できます。 要素自体を変更せずに、並べ替えやグループ化してシーケンス自体を変更できます。 しかし、[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] のクエリの最も強力な機能は、新しい型を作成する機能です。 この操作は [select](../../../../csharp/language-reference/keywords/select-clause.md) 句内で行います。 たとえば、次のタスクを実行できます。  
  
-   複数の入力シーケンスを結合して、新しい型の単一の出力シーケンスを作成する。  
  
-   ソース シーケンス内の各要素の単一のプロパティまたは複数のプロパティを構成要素とする出力シーケンスを作成する。  
  
-   ソース データに対して実行した操作の結果を構成要素とする出力シーケンスを作成する。  
  
-   別の形式で出力シーケンスを作成する。 たとえば、SQL の行またはテキスト ファイルのデータを XML に変換できます。  
  
 これらはほんの一例です。 これらの変換を、同じクエリ内でさまざまな方法で組み合わせて使用することもできます。 また、あるクエリの出力シーケンスを別のクエリの入力シーケンスとして使用することもできます。  
  
## <a name="joining-multiple-inputs-into-one-output-sequence"></a>複数の入力を 1 つの出力シーケンスに結合する  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] クエリを使用して、複数の入力シーケンスの要素を含む 1 つの出力シーケンスを作成できます。 次の例は、2 つのインメモリ データ構造を結合する方法を示していますが、ソースが XML、SQL、または DataSet のデータを結合する場合にも同じ基本原則を適用できます。 次の 2 つのクラス型があるとします。  
  
 [!code-cs[CsLINQGettingStarted#7](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_1.cs)]  
  
 クエリの例を次に示します。  
  
 [!code-cs[CSLinqGettingStarted#8](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_2.cs)]  
  
 詳細については、「[join 句](../../../../csharp/language-reference/keywords/join-clause.md)」および「[select 句](../../../../csharp/language-reference/keywords/select-clause.md)」を参照してください。  
  
## <a name="selecting-a-subset-of-each-source-element"></a>各ソース要素のサブセットを選択する  
 ソース シーケンスの各要素のサブセットを選択するには、主に次の 2 つの方法があります。  
  
1.  ソース要素の 1 つのメンバーのみを選択するには、ドット演算を使用します。 次の例で、`Customer` オブジェクトに `City` という文字列を含むいくつかのパブリック プロパティが含まれているとします。 このクエリを実行すると、文字列の出力シーケンスが生成されます。  
  
    ```  
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2.  ソース要素からの複数のプロパティを含む要素を作成するには、名前付きオブジェクトまたは匿名型を指定したオブジェクト初期化子を使用します。 次の例は、匿名型を使用して各 `Customer` 要素の 2 つのプロパティをカプセル化する方法を示しています。  
  
    ```  
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 詳細については、「[オブジェクト初期化子とコレクション初期化子](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)」および「[匿名型](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)」を参照してください。  
  
## <a name="transforming-in-memory-objects-into-xml"></a>インメモリ オブジェクトを XML に変換する  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] クエリを使用すると、インメモリ データ構造、SQL データベース、[!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] データセット、XML ストリーム、または XML ドキュメントの間でデータ変換を簡単に行うことができます。 インメモリ データ構造のオブジェクトを XML 要素に変換する例を次に示します。  
  
 [!code-cs[CsLINQGettingStarted#9](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_3.cs)]  
  
 このコードを実行すると、次の XML 出力が生成されます。  
  
```  
< Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 詳細については、「[C# での XML ツリーの作成 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees-linq-to-xml-2.md)」を参照してください。  
  
## <a name="performing-operations-on-source-elements"></a>ソース要素に対して操作を実行する  
 出力シーケンスには、ソース シーケンスの要素または要素のプロパティが 1 つも含まれない場合があります。 代わりに、ソース要素を入力引数として使用することで計算された値のシーケンスを出力として生成できます。 次の簡単なクエリを実行すると、`double` 型の要素のソース シーケンスに基づく計算を表す値を含む文字列のシーケンスが出力されます。  
  
> [!NOTE]
>  クエリが他のドメインに変換される場合、クエリ式でのメソッド呼び出しはサポートされません。 たとえば、[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] で C# の通常のメソッドを呼び出すことはできません。これは、C# のメソッドのコンテキストが SQL Server にないためです。 ただし、ストアド プロシージャをメソッドにマップして呼び出すことは可能です。 詳細については、「[ストアド プロシージャ](../../../../framework/data/adonet/sql/linq/stored-procedures.md)」を参照してください。  
  
 [!code-cs[CsLINQGettingStarted#10](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_4.cs)]  
  
## <a name="see-also"></a>関連項目  
 [統合言語クエリ (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)   
 [LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml.md)   
 [LINQ クエリ式](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [select 句](../../../../csharp/language-reference/keywords/select-clause.md)
