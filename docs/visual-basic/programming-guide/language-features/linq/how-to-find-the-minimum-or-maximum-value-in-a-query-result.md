---
title: "方法: LINQ (Visual Basic) を使用してクエリ結果内の最小値と最大値を検索 |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- max operator [LINQ in Visual Basic]
- aggregate operator [LINQ in Visual Basic]
- aggregate queries
- minimum values [LINQ in Visual Basic]
- min operator [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], minimum and maximum values
- Max property
- maximum values [LINQ in Visual Basic]
- Aggregate clause
- queries [LINQ in Visual Basic], aggregate queries
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 238b763b-7dcd-4b14-8050-b65500a4f71c
caps.latest.revision: 6
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6dc2eecf4cef9a219b7a06cfcc0fdf773e4e1333
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-find-the-minimum-or-maximum-value-in-a-query-result-by-using-linq-visual-basic"></a>方法 : LINQ を使用したクエリ結果内の最小値と最大値の検索 (Visual Basic)
統合言語クエリ (LINQ) により、簡単にデータベース情報にアクセスし、クエリを実行します。  
  
 次の例では、SQL Server データベースに対してクエリを実行する新しいアプリケーションを作成する方法を示します。 このサンプルを使用して結果を得るのための最小値と最大値を決定する、`Aggregate`と`Group By`句。 詳細については、次を参照してください。 [Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)と[グループ By 句](../../../../visual-basic/language-reference/queries/group-by-clause.md)します。  
  
 このトピックの例では、Northwind サンプル データベースを使用します。 開発用コンピューターに Northwind サンプル データベースがないをからダウンロードできます、 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=98088) Web サイトです。 手順については、次を参照してください。[サンプル データベースのダウンロード](https://msdn.microsoft.com/library/bb399411)します。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>データベースへの接続を作成するには  
  
1.  Visual Studio で開きます**サーバー エクスプ ローラー**/**データベース エクスプ ローラー**をクリックして**サーバー エクスプ ローラー**/**データベース エクスプ ローラー**上、**ビュー**メニュー。  
  
2.  右クリック**データ接続**で**サーバー エクスプ ローラー**/**データベース エクスプ ローラー**  をクリックし、**接続の追加**します。  
  
3.  Northwind サンプル データベースに有効な接続を指定します。  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>LINQ to SQL ファイルを含むプロジェクトを追加するのには  
  
1.  Visual Studio での**ファイル** メニューをポイント**新規** をクリックし、**プロジェクト**します。 Visual Basic を選択して**Windows フォーム アプリケーション**プロジェクトの種類として。  
  
2.  **[プロジェクト]** メニューの **[新しい項目の追加]**をクリックします。 選択、 **LINQ to SQL クラス**項目テンプレートです。  
  
3.  そのファイルに `northwind.dbml` という名前を付けます。 **[追加]**をクリックします。 Northwind.dbml ファイルには、オブジェクト リレーショナル デザイナー (O/R デザイナー) が開かれます。  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>O/R デザイナーをクエリにテーブルを追加するには  
  
1.  **サーバー エクスプ ローラー**/**データベース エクスプ ローラー**、Northwind データベースへの接続を展開します。 展開、**テーブル**フォルダーです。  
  
     O/R デザイナーを閉じていた場合は、前に追加した northwind.dbml ファイルをダブルクリックして開くことができます。  
  
2.  Customers テーブルをクリックし、デザイナーの左ペインにドラッグします。 Orders テーブルをクリックし、デザイナーの左ペインにドラッグします。  
  
     デザイナーを新規作成`Customer`と`Order`プロジェクトのオブジェクト。 デザイナーが自動的にテーブル間のリレーションシップを検出し、関連オブジェクトのプロパティの子を作成することに注意してください。 たとえば、IntelliSense が表示されますが、`Customer`オブジェクトには、`Orders`その顧客に関連するすべての発注書のプロパティです。  
  
3.  変更内容を保存してデザイナーを閉じます。  
  
4.  プロジェクトを保存します。  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>データベースを照会し、結果を表示するコードを追加するには  
  
1.  **ツールボックス**、ドラッグ、<xref:System.Windows.Forms.DataGridView>コントロールをプロジェクトの Form1 の既定の Windows フォームにします</xref:System.Windows.Forms.DataGridView>。  
  
2.  コードを追加する Form1 をダブルクリックして、`Load`形式のイベントです。  
  
3.  O/R デザイナーにテーブルを追加したときに、デザイナーが追加、 <xref:System.Data.Linq.DataContext>、プロジェクトのオブジェクト</xref:System.Data.Linq.DataContext>。 このオブジェクトには、個々 のオブジェクトと各テーブルのコレクションだけでなく、それらのテーブルにアクセスするために必要なコードが含まれています。 <xref:System.Data.Linq.DataContext>オブジェクトは、プロジェクトの名前に基づいての .dbml ファイルの名前</xref:System.Data.Linq.DataContext>。 このプロジェクトで、<xref:System.Data.Linq.DataContext>オブジェクトの名前は`northwindDataContext`</xref:System.Data.Linq.DataContext>。  
  
     インスタンスを作成することができます、 <xref:System.Data.Linq.DataContext>O/R デザイナーで指定されたテーブル内のコードとクエリ</xref:System.Data.Linq.DataContext>。  
  
     次のコードを追加、`Load`イベントです。 このコードは、データ コンテキストのプロパティとして公開され、結果を得るのための最小値と最大値を決定するテーブルを照会します。 サンプルでは、彼は使用`Aggregate`、単一の結果のクエリに句と`Group By`の平均値を表示する句の結果をグループ化します。  
  
     [!code-vb[VbLINQToSQLHowTos&#14;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-find-the-minimum-or-maximum-value-in-a-query-result_1.vb)]  
  
4.  F5 キーを押してプロジェクトを実行し、結果を表示します。  
  
## <a name="see-also"></a>関連項目  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [クエリ](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [DataContext メソッド (O/R デザイナー)](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)

