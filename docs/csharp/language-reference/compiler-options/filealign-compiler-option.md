---
title: "-filealign (C# コンパイラ オプション) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /filealign
dev_langs:
- CSharp
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
caps.latest.revision: 14
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
ms.openlocfilehash: 83569fa264ba3ed6e271281885940a70a5354840
ms.lasthandoff: 03/13/2017

---
# <a name="filealign-c-compiler-options"></a>/filealign (C# コンパイラ オプション)
**/filealign** オプションを使用すると、出力ファイル内のセクションのサイズを指定できます。  
  
## <a name="syntax"></a>構文  
  
```  
/filealign:number  
```  
  
## <a name="arguments"></a>引数  
 `number`  
 出力ファイル内のセクションのサイズを指定する値です。 有効値は 512、1024、2048、4096、および 8192 です。 これらの値はバイト単位です。  
  
## <a name="remarks"></a>コメント  
 各セクションは、**/filealign** 値の倍数である境界上にアラインされます。 固定の既定値はありません。 **/filealign** が指定されていない場合、共通言語ランタイムはコンパイル時に既定値を選択します。  
  
 セクションのサイズを指定すると、出力ファイルのサイズに影響します。 セクションのサイズ変更は、比較的小さなデバイスで実行されるプログラムに対して有効な場合があります。  
  
 出力ファイル内のセクションに関する情報を表示するには、[DUMPBIN](https://docs.microsoft.com/cpp/build/reference/dumpbin-options) を使用します。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 開発環境でこのコンパイラ オプションを設定するには  
  
1.  プロジェクトの **[プロパティ]** ページを開きます。  
  
2.  **[ビルド]** プロパティ ページをクリックします。  
  
3.  [詳細設定 **** ] ボタンをクリックします。  
  
4.  **[ファイルの配置]** プロパティを変更します。  
  
 このコンパイラ オプションをプログラムで設定する方法については、「<xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [C# コンパイラのオプション](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB 方法: プロジェクト プロパティと構成設定を変更する](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
