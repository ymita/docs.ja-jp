---
title: "例外の使用 (C# プログラミング ガイド) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
caps.latest.revision: 15
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
ms.openlocfilehash: 8a4bbb2f6d8060cd9196dd510cd89c827c9d697d
ms.lasthandoff: 03/13/2017

---
# <a name="using-exceptions-c-programming-guide"></a>例外の使用 (C# プログラミング ガイド)
C# では、例外と呼ばれるメカニズムを使用して、プログラムの実行時に発生したエラーがプログラムに伝えられます。 例外は、エラーが発生したコードによってスローされ、エラーを修正できるコードによってキャッチされます。 例外をスローできるのは、.NET Framework 共通言語ランタイム (CLR) か、プログラム内のコードです。 スローされた例外は、例外の `catch` ステートメントが見つかるまで呼び出し履歴をさかのぼります。 キャッチされない例外は、システムが提供する汎用の例外ハンドラーによって処理されます。このとき、ダイアログ ボックスが表示されます。  
  
 例外は、<xref:System.Exception> から派生したクラスによって表されます。 このクラスは例外の型を識別し、例外に関する詳細情報が含まれたプロパティを保持します。 例外をスローするには、例外の派生クラスのインスタンスを作成し、必要に応じて例外のプロパティを設定してから、`throw` キーワードを使用してオブジェクトをスローする必要があります。 例:  
  
 [!code-cs[csProgGuideExceptions#1](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_1.cs)]  
  
 例外がスローされると、ランタイムは、現在のステートメントが `try` ブロック内に存在するかどうかを確認します。 存在する場合は、`try` ブロックに関連付けられている `catch` ブロックをチェックして、例外をキャッチできるかどうかを確認します。 通常は、この `Catch` ブロックによって例外の型が指定されます。`catch` ブロックの型が、例外または例外の基底クラスの型と一致する場合、`catch` ブロックはメソッドを処理できます。 例:  
  
 [!code-cs[csProgGuideExceptions#2](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_2.cs)]  
  
 例外をスローするステートメントが `try` ブロックにない場合、または `try` ブロックにそのステートメントが含まれていても、対応する `catch` ブロックが存在しない場合は、ランタイムが呼び出し側のメソッドで `try` ステートメントと `catch` ブロックを探します。 続けて、呼び出し履歴で、対応する `catch` ブロックを探します。 `catch` ブロックが見つかり実行されると、その `catch` ブロックの後にある次のステートメントに制御が渡されます。  
  
 `try` ステートメントには、複数の `catch` ブロックを含めることができます。 例外を処理できる最初の `catch` ステートメントが実行され、その後の `catch` ステートメントは、対応していても無視されます。 そのため、catch ブロックは必ず特殊性が高いもの (または最も派生されたもの) から順に配置する必要があります。 例:  
  
 [!code-cs[csProgGuideExceptions#3](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_3.cs)]  
  
 `catch` ブロックが実行される前に、ランタイムにより `finally` ブロックがチェックされます。 `Finally` ブロックを使用すると、中止された `try` ブロックによって残ることがある、あいまいな状態をクリーンアップできます。また、ランタイムのガベージ コレクターがオブジェクトを終了させるのを待たずに外部リソース (グラフィック ハンドル、データベース接続、ファイル ストリームなど) を解放することもできます。 例:  
  
 [!code-cs[csProgGuideExceptions#4](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_4.cs)]  
  
 `WriteByte()` が例外をスローした場合は、`file.Close()` を呼び出さないと、ファイルを再度開こうとする 2 番目の `try` ブロックのコードが失敗し、ファイルはロックされたままになります。 例外がスローされても `finally` ブロックは実行されるため、上の例の `finally` ブロックではファイルを適切に閉じて、エラーを回避できます。  
  
 例外がスローされた後、対応する `catch` ブロックが呼び出し履歴に見つからない場合は、次のいずれかが発生します。  
  
-   例外がデストラクターの内部で発生した場合、デストラクターは中止され、基本デストラクター (存在する場合) が呼び出されます。  
  
-   呼び出し履歴に静的コンストラクターまたは静的フィールド初期化子が含まれている場合は、<xref:System.TypeInitializationException> がスローされ、新しい例外の <xref:System.Exception.InnerException%2A> プロパティに元の例外が割り当てられます。  
  
-   スレッドの開始位置に到達すると、スレッドは終了します。  
  
## <a name="see-also"></a>関連項目  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [例外と例外処理](../../../csharp/programming-guide/exceptions/index.md)
