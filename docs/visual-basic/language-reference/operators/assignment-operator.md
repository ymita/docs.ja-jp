---
title: "= 演算子 (Visual Basic) |Microsoft ドキュメント"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Assign
- vb.=
dev_langs:
- VB
helpviewer_keywords:
- = operator [Visual Basic]
- = assignment statements [Visual Basic]
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
caps.latest.revision: 16
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
ms.openlocfilehash: 47b69a908f12ec36daf2848da6ee4b04895fd3a4
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-visual-basic"></a>= 演算子 (Visual Basic)
変数やプロパティに値を割り当てます。  
  
## <a name="syntax"></a>構文  
  
```  
  
variableorproperty = value  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 書き込み可能な任意の変数または任意のプロパティです。  
  
 `value`  
 任意のリテラル、定数、または式。  
  
## <a name="remarks"></a>コメント  
 等号 (=) の左側にある要素 (`=`) 単純なスカラー変数、プロパティ、または配列の要素にすることができます。 変数やプロパティにすることはできません[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)します。 `=`演算子は、変数に、右側の値またはプロパティの左側に代入します。  
  
> [!NOTE]
>  `=`演算子、比較演算子としても使用します。 詳細については、「[比較演算子](../../../visual-basic/language-reference/operators/comparison-operators.md)します。  
  
## <a name="overloading"></a>オーバーロード  
 `=`比較演算子としてのみ、代入演算子としてではなく、演算子がオーバー ロードできます。 詳細については、次を参照してください。[演算子プロシージャ](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)します。  
  
## <a name="example"></a>例  
 次の例では、代入演算子を示します。 右側の値が左側の変数に割り当てられます。  
  
 [!code-vb[VbVbalrOperators&#9;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/assignment-operator_1.vb)]  
  
## <a name="see-also"></a>関連項目  
 [< = 演算子](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [* = 演算子](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [+ = 演算子](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [-= 演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [/= 演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\= 演算子](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [^ = 演算子](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [ステートメント](../../../visual-basic/programming-guide/language-features/statements.md)   
 [比較演算子](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [読み取り専用](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [ローカル型の推論](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)

