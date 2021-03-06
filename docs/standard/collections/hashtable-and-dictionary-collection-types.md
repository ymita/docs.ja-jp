---
title: "Hashtable コレクション型と Dictionary コレクション型 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Hashtable class, grouping data in collections
- Hashtable collection type
- hash tables
- grouping data in collections, Hashtable collection type
- hash function
- collections [.NET Framework], Hashtable collection type
ms.assetid: bfc20837-3d02-4fc7-8a8f-c5215b6b7913
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 59aa4bd6160491ac6c6a4f45131531226ec7e58f
ms.lasthandoff: 04/18/2017

---
# <a name="hashtable-and-dictionary-collection-types"></a>Hashtable コレクション型と Dictionary コレクション型
<xref:System.Collections.Hashtable?displayProperty=fullName> クラス、<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> ジェネリック クラス、<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> ジェネリック クラスは <xref:System.Collections.IDictionary?displayProperty=fullName> インターフェイスを実装します。 <xref:System.Collections.Generic.Dictionary%602> ジェネリック クラスは <xref:System.Collections.Generic.IDictionary%602> ジェネリック インターフェイスも実装します。 そのため、これらのコレクション内の各要素は、キーと値のペアになります。  
  
 <xref:System.Collections.Hashtable> オブジェクトは、コレクションの要素を含むバケットで構成されます。 バケットは <xref:System.Collections.Hashtable> に含まれる要素の仮想サブグループで、これを使用することにより、ほとんどのコレクションで検索と取得がより簡単で高速になります。 各バケットは、ハッシュ関数を使用して生成され、要素のキーに基づいている、ハッシュ コードに関連付けられています。  
  
 ジェネリック <xref:System.Collections.Generic.HashSet%601> クラスは、一意の要素を格納するための順序付けられていないコレクションです。  
  
 ハッシュ関数は、キーに基づく数値のハッシュ コードを返すアルゴリズムです。 キーは、格納されているオブジェクトのいくつかのプロパティの値です。 ハッシュ関数は、同じキーに対して常に同じハッシュ コードを返す必要があります。 ハッシュ関数によって 2 つの異なるキーを持つ同一のハッシュ コードを生成することも可能ですが、一意のキーごとに一意のハッシュ コードを生成するハッシュ関数のほうが、ハッシュ テーブルから要素を取得する際により優れたパフォーマンスを実現します。  
  
 <xref:System.Collections.Hashtable> で要素として使用されている各オブジェクトは、<xref:System.Object.GetHashCode%2A> メソッドの実装を使用して、それ自体のハッシュ コードを生成できる必要があります。 ただし、<xref:System.Collections.IHashCodeProvider> 実装をパラメーターの 1 つとして受け入れる <xref:System.Collections.Hashtable> コンストラクターを使用して、<xref:System.Collections.Hashtable> のすべての要素のハッシュ関数を指定することもできます。  
  
 オブジェクトは、<xref:System.Collections.Hashtable> に追加されるとき、そのオブジェクトのハッシュ コードと一致するハッシュ コードに関連付けられたバケットに格納されます。 値が <xref:System.Collections.Hashtable> 内で検索されるとき、その値のハッシュ コードが生成されて、そのハッシュ コードに関連付けられたバケットが検索されます。  
  
 たとえば、文字列のハッシュ関数は、文字列内の各文字の ASCII コードを取得し、それらを加え合わせて 1 つのハッシュ コードを生成することができます。 その場合、文字列「picnic」のハッシュ コードは文字列「basket」のハッシュ コードと異なるので、文字列「picnic」と「basket」は異なるバケットに格納されます。 それに対して、「stressed」と「desserts」は同じハッシュ コードを持つので、同じバケットに格納されます。  
  
 <xref:System.Collections.Generic.Dictionary%602> クラスと <xref:System.Collections.Concurrent.ConcurrentDictionary%602>クラスには、<xref:System.Collections.Hashtable> クラスと同じ機能があります。 特定の種類 (<xref:System.Object> 以外) の <xref:System.Collections.Generic.Dictionary%602> は、値の型として <xref:System.Collections.Hashtable> よりパフォーマンスが優れています。 これは、<xref:System.Collections.Hashtable> の要素の型が <xref:System.Object> であるため、値型を格納したり取得したりすると、ボックス化とボックス化解除が通常発生するためです。 複数のスレッドがコレクションに同時にアクセスする可能性があるときは、<xref:System.Collections.Concurrent.ConcurrentDictionary%602> クラスを使用してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Collections.Hashtable>   
 <xref:System.Collections.IDictionary>   
 <xref:System.Collections.IHashCodeProvider>   
 <xref:System.Collections.Generic.Dictionary%602>   
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>   
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>   
 [ 一般的に使用されるコレクション型](../../../docs/standard/collections/commonly-used-collection-types.md)
