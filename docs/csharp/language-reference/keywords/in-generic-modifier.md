---
title: "in (ジェネリック修飾子) (C# リファレンス) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- contravariance, in keyword [C#]
- in keyword [C#]
ms.assetid: 3a778c36-8aed-4ebe-aa8b-39f4057215b1
caps.latest.revision: 17
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
ms.openlocfilehash: b6c490d14b47aaa527fe2ddb3627ea0a84bfe604
ms.lasthandoff: 03/13/2017

---
# <a name="in-generic-modifier-c-reference"></a>in (ジェネリック修飾子) (C# リファレンス)
ジェネリック型パラメーターの `in` キーワードは、型パラメーターが反変であることを指定します。 `in` キーワードは、ジェネリック インターフェイスとデリゲートで使用できます。  
  
 反変性は、ジェネリック パラメーターによって指定された型よりも弱い派生型を使用できるようにする機能です。 これにより、バリアント インターフェイスを実装するクラスの暗黙の型変換とデリゲート型の暗黙の型変換が可能となります。 ジェネリック型パラメーターの共変性および反変性は参照型ではサポートされますが、値型ではサポートされません。  
  
 型をジェネリック インターフェイスまたはデリゲートで反変として宣言できるのは、メソッド引数の型としてのみ使用され、メソッドの戻り値の型としては使用されない場合です。 `Ref` パラメーターと `out` パラメーターをバリアントにすることはできません。  
  
 反変の型パラメーターを持つインターフェイスを使用すると、そのインターフェイスのメソッドは、インターフェイス型パラメーターによって指定された型よりも弱い派生型の引数を受け取ることができます。 たとえば、.NET Framework 4 の <xref:System.Collections.Generic.IComparer%601> インターフェイスでは T 型が反変なので、`Employee` が `Person` を継承していれば、特別な変換メソッドを使用しなくても `IComparer(Of Person)` 型のオブジェクトを `IComparer(Of Employee)` 型のオブジェクトに割り当てることができます。  
  
 反変のデリゲートには、型は同じでありながらより弱い派生ジェネリック型パラメーターを持つ別のデリゲートを割り当てることができます。  
  
 詳細については、「[共変性と反変性](http://msdn.microsoft.com/library/a58cc086-276f-4f91-a366-85b7f95f38b8)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、反変のジェネリック インターフェイスを宣言、拡張、および実装する方法を示します。 また、このインターフェイスを実装するクラスの暗黙的な変換を使用する方法も示します。  
  
 [!code-cs[csVarianceKeywords#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/in-generic-modifier_1.cs)]  
  
## <a name="example"></a>例  
 次の例では、反変の汎用デリゲートを宣言、インスタンス化、および呼び出す方法を示します。 また、デリゲート型を暗黙的に変換する方法も示します。  
  
 [!code-cs[csVarianceKeywords#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/in-generic-modifier_2.cs)]  
  
## <a name="c-language-specification"></a>C# 言語仕様  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>関連項目  
 [out](../../../csharp/language-reference/keywords/out-generic-modifier.md)   
 [共変性と反変性](http://msdn.microsoft.com/library/a58cc086-276f-4f91-a366-85b7f95f38b8)   
 [修飾子](../../../csharp/language-reference/keywords/modifiers.md)
