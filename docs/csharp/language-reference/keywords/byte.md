---
title: "byte (C# リファレンス) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- byte
- byte_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- byte keyword [C#]
ms.assetid: 111f1db9-ca32-4f0e-b497-4783517eda47
caps.latest.revision: 19
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
ms.openlocfilehash: 7c522506b4541edb2a81036e93e8872711f849b9
ms.lasthandoff: 03/13/2017

---
# <a name="byte-c-reference"></a>byte (C# リファレンス)
`byte` キーワードは、次の表に示された値を格納する整数型を示します。  
  
|型|範囲|サイズ|.NET Framework 型|  
|----------|-----------|----------|-------------------------|  
|`byte`|0 ～ 255|符号なし 8 ビット整数|<xref:System.Byte?displayProperty=fullName>|  
  
## <a name="literals"></a>リテラル  
 `byte` 変数の宣言と初期化の例を次に示します。  
  
```  
byte myByte = 255;  
```  
  
 上のように宣言すると、整数リテラル `255` は暗黙的に [int](../../../csharp/language-reference/keywords/int.md) から `byte` に変換されます。 整数リテラルが `byte` の範囲を超えると、コンパイル エラーになります。  
  
## <a name="conversions"></a>変換  
 `byte` から [short](../../../csharp/language-reference/keywords/short.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md)、[int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md)、[decimal](../../../csharp/language-reference/keywords/decimal.md) への暗黙の型変換が組み込まれています。  
  
 より大きな記憶領域のサイズを持つ、リテラル以外の数値型を暗黙的に `byte` に変換することはできません。 整数型の記憶域サイズの詳細については、「[整数型の一覧表](../../../csharp/language-reference/keywords/integral-types-table.md)」を参照してください。 たとえば、2 つの `byte` 変数 `x` と `y` があるとします。  
  
```  
  
byte x = 10, y = 20;  
```  
  
 次の代入ステートメントは、代入演算子の右側にある算術式が既定で `int` に評価されるため、コンパイル エラーになります。  
  
```  
// Error: conversion from int to byte:  
byte z = x + y;  
```  
  
 この問題を解決するには、キャストを使用します。  
  
```  
// OK: explicit conversion:  
byte z = (byte)(x + y);  
```  
  
 ただし、次のステートメントは使用できます。このステートメントでは、変換先の変数の記憶領域サイズは元のサイズ以上になります。  
  
```  
int x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 浮動小数点型から `byte` への暗黙の型変換はありません。 たとえば、次のステートメントは、明示的なキャストを使用しない場合、コンパイラ エラーになります。  
  
```  
// Error: no implicit conversion from double:  
byte x = 3.0;   
// OK: explicit conversion:  
byte y = (byte)3.0;  
```  
  
 オーバーロードされたメソッドを呼び出すときは、キャストを使用する必要があります。 たとえば、`byte` パラメーターと [int](../../../csharp/language-reference/keywords/int.md) パラメーターを使用したオーバーロードされたメソッドがあるとします。  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(byte b) {}  
```  
  
 `byte` キャストを使用すると、正しい型が呼び出されます。次に例を示します。  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the byte parameter:  
SampleMethod((byte)5);  
```  
  
 浮動小数点型と整数型の混在する算術式の詳細については、「[float](../../../csharp/language-reference/keywords/float.md)」と「[double](../../../csharp/language-reference/keywords/double.md)」を参照してください。  
  
 暗黙の数値変換規則の詳細については、「[暗黙的な数値変換の一覧表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)」を参照してください。  
  
## <a name="c-language-specification"></a>C# 言語仕様  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Byte>   
 [C# リファレンス](../../../csharp/language-reference/index.md)   
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [C# のキーワード](../../../csharp/language-reference/keywords/index.md)   
 [整数型の一覧表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [組み込み型の一覧表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [暗黙的な数値変換の一覧表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [明示的な数値変換の一覧表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
