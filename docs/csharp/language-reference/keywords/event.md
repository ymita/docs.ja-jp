---
title: "event (C# リファレンス) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- event
- remove
- event_CSharpKeyword
- add
dev_langs:
- CSharp
helpviewer_keywords:
- event keyword [C#]
ms.assetid: 7858fd85-153b-4259-85d0-6aa13c35f174
caps.latest.revision: 28
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
ms.openlocfilehash: 60a6322f8e120c6a443638b4f6e409acdfa0b235
ms.lasthandoff: 03/13/2017

---
# <a name="event-c-reference"></a>event (C# リファレンス)
`event` キーワードを使用し、パブリッシャー クラス内にイベントを宣言します。  
  
## <a name="example"></a>例  
 次の例では、基になるデリゲート型として <xref:System.EventHandler> を使用するイベントを宣言し、発生させる方法について説明します。 完全なコード例については、「[方法 : .NET Framework ガイドラインに準拠したイベントを発行する](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)」を参照してください。完全なコード例では、ジェネリック <xref:System.EventHandler%601> デリゲート型の使用方法、イベント サブスクリプションの実行方法、イベント ハンドラー メソッドの作成方法も確認できます。  
  
 [!code-cs[csrefKeywordsModifiers#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/event_1.cs)]  
  
 イベントは、宣言元 (パブリッシャー クラス) のクラスまたは構造体内でしか呼び出せない特殊なマルチキャスト デリゲートです。 他のクラスまたは構造体がイベントを受信登録した場合、パブリッシャー クラスがイベントを発生させると、他のクラスまたは構造体のイベント ハンドラー メソッドが呼び出されます。 詳細およびコード例については、「[イベント](../../../csharp/programming-guide/events/index.md)」および「[デリゲート](../../../csharp/programming-guide/delegates/index.md)」を参照してください。  
  
 イベントは、[public](../../../csharp/language-reference/keywords/public.md)、[private](../../../csharp/language-reference/keywords/private.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md)、または `protected``internal` としてマークできます。 これらのアクセス修飾子により、クラスのユーザーがイベントにアクセスする方法が定義されます。 詳細については、「[アクセス修飾子](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)」を参照してください。  
  
## <a name="keywords-and-events"></a>キーワードとイベント  
 イベントには次のキーワードが適用されます。  
  
|キーワード|説明|詳細情報|  
|-------------|-----------------|--------------------------|  
|[static](../../../csharp/language-reference/keywords/static.md)|クラスのインスタンスが存在しない場合でも、呼び出し元がいつでもイベントを使用できるようになります。|[静的クラスと静的クラス メンバー](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)|  
|[virtual](../../../csharp/language-reference/keywords/virtual.md)|[override](../../../csharp/language-reference/keywords/override.md) キーワードを使用してイベントの動作をオーバーライドすることを派生クラスに許可します。|[継承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|派生クラスでは、それが仮想ではなくなったことを指定します。||  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|コンパイラはイベント アクセサー ブロックの `add` と `remove` を生成しません。したがって、派生クラスは固有の実装を提供する必要があります。||  
  
 イベントは、[static](../../../csharp/language-reference/keywords/static.md) キーワードを使用して静的イベントとして宣言されることもあります。 その場合、クラスのインスタンスが存在しなくても、呼び出し元がいつでもイベントを使用できるようになります。 詳細については、「[静的クラスと静的クラス メンバー](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)」を参照してください。  
  
 イベントは、[virtual](../../../csharp/language-reference/keywords/virtual.md) キーワードを使用して仮想イベントとしてマークできます。 その場合、派生クラスでは、[override](../../../csharp/language-reference/keywords/override.md) キーワードを使用してイベントの動作をオーバーライドできます。 詳細については、「[継承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)」を参照してください。 仮想イベントをオーバーライドするイベントは、[sealed](../../../csharp/language-reference/keywords/sealed.md) にすることもできます。その場合、派生クラスでは、イベントが仮想でなくなります。 最後に、イベントは [abstract](../../../csharp/language-reference/keywords/abstract.md) として宣言できます。その場合、コンパイラはイベント アクセサー ブロックの `add` と `remove` を生成しません。 したがって、派生クラスごとに固有の実装を提供する必要があります。  
  
## <a name="c-language-specification"></a>C# 言語仕様  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>関連項目  
 [C# リファレンス](../../../csharp/language-reference/index.md)   
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [C# のキーワード](../../../csharp/language-reference/keywords/index.md)   
 [add](../../../csharp/language-reference/keywords/add.md)   
 [remove](../../../csharp/language-reference/keywords/remove.md)   
 [修飾子](../../../csharp/language-reference/keywords/modifiers.md)   
 [方法 : デリゲートを結合する (マルチキャスト デリゲート)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)
