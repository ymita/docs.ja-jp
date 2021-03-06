---
title: ".NET Framework 4.5.1 におけるランタイムの変更点 | Microsoft ドキュメント"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application compatibility
- runtime changes
- .NET Framework 4.5.1
ms.assetid: da880ad7-ba0a-4368-b340-705e3533c351
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 4e4903c2f25354005f95b3ed8f9728cfe8a0a92e
ms.contentlocale: ja-jp
ms.lasthandoff: 04/18/2017

---
# <a name="runtime-changes-in-the-net-framework-451"></a>.NET Framework 4.5.1 におけるランタイムの変更点
まれに、実行時の変更は [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] または 4.5 を対象とする既存のアプリに影響を与える可能性がありますが、4.51 ランタイムで実行されます。 次の領域の変更が含まれています。  
  
-   [コア](#Core)  
  
-   [Windows Communication Foundation (WCF)](#WCF)  
  
 次の表の [スコープ] 列には、各変更の重要度を指定します。  
  
-   メジャー。 多数のアプリに影響するか、またはコードに大幅な変更が必要な、重大な変更。 ランタイムの変更はこのカテゴリに分類されないことに注意してください。  
  
-   マイナー。 少数のアプリに影響するか、またはコードにわずかな変更が必要な、変更。  
  
-   エッジ。 一般的ではない特定のシナリオでアプリに影響を与える変更。  
  
-   透過。 アプリの開発者やユーザーには大きな影響を及ぼさない変更。 アプリはこの変更のために変更を加える必要はありません。  
  
<a name="Core"></a>   
## <a name="core-runtime-changes"></a>コアでのランタイム変更  
  
|機能|変更|影響|スコープ|  
|-------------|------------|------------|-----------|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> シリアル化|.NET Framework 4.5 で <xref:System.Runtime.Serialization.NetDataContractSerializer> を使ってシリアル化された <xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクトは、タイプが内部変更されたため、.NET Framework 4.5.1 および 4.5.2 では逆シリアル化できません。<br /><br /> この変更は、次のシナリオには適用*されません*。<br /><br /> .NET Framework 4.5 でシリアル化され、[!INCLUDE[net_v46](../../../includes/net-v46-md.md)] で逆シリアル化された <xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクト。 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] の <xref:System.Runtime.Serialization.NetDataContractSerializer> は、このオブジェクトを逆シリアル化することができます。<br /><br /> NET Framework の後のバージョンでシリアル化され、.NET Framework 4.5 で逆シリアル化された <xref:System.Collections.Concurrent.ConcurrentDictionary%602>オブジェクト。 .NET Framework 4.5 の <xref:System.Runtime.Serialization.NetDataContractSerializer> は、このオブジェクトを逆シリアル化することができます。<br /><br /> .NET Framework 4.5 以降の .NET Framework のすべてのバージョン間における <xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクトのシリアル化および逆シリアル化。 この変更は、.NET Framework 4.5 *のみ*でシリアル化したオブジェクトに適用されます。|<xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクトを .NET Framework 4.5 でシリアル化してから、それより後のバージョンの .NET Framework で逆シリアル化する必要がある場合は、2 つの方法で行うことができます。<br /><br /> <xref:System.Runtime.Serialization.DataContractSerializer> または <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> などのシリアライザーを代わりに使用する。<br /><br /> NET Framework 4.5 でシリアル化された <xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクトの逆シリアル化をサポートする [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] にアップグレードする。|マイナー|  
|<xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> クラス|<xref:System.Diagnostics.Tracing.EventListener> は、null が埋め込まれた文字列を切り詰めます。 <xref:System.Diagnostics.Tracing.EventSource> クラスでは null 文字はサポートされていません。|この変更は、<xref:System.Diagnostics.Tracing.EventListener> を使用してプロセス内の <xref:System.Diagnostics.Tracing.EventSource> データを読み取り、null 文字を区切り記号として使用するアプリにのみ影響します。|エッジ|  
|<xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> クラス|ランタイムは次の内容を指定するコントラクトを強制するようになりました。ETW イベント メソッドを定義する <xref:System.Diagnostics.Tracing.EventSource> から派生されたクラスは、イベント ID の後に ETW イベント メソッドが渡されたのと同じ引数を指定して、基底クラス <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A?displayProperty=fullName> メソッドを呼び出す必要があります。|<xref:System.Diagnostics.Tracing.EventListener> がこのコントラクトに違反するイベント ソースのプロセスで <xref:System.Diagnostics.Tracing.EventSource> データを読み取った場合、<xref:System.IndexOutOfRangeException> 例外がスローされます。<br /><br /> 「[軽減策: EventSource.WriteEvent メソッドの呼び出し](../../../docs/framework/migration-guide/mitigation-eventsource-writeevent-method-calls.md)」を参照してください。|マイナー|  
|アプリケーション ドメイン間でのオブジェクトの逆シリアル化|場合によっては、アプリが異なるアプリケーション ベースを持つ複数のアプリ ドメインを使用すると、アプリ ドメイン間で論理呼び出しコンテキストのオブジェクトを逆シリアル化しようとして、例外がスローされます。|この問題は、固有のシナリオで発生します。 詳細と軽減策については、「[軽減策: アプリ ドメイン全体でのオブジェクトの逆シリアル化](../../../docs/framework/migration-guide/mitigation-deserialization-of-objects-across-app-domains.md)」を参照してください。|エッジ|  
|<xref:System.IO.Stream.Dispose%2A?displayProperty=fullName> メソッド|[!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)]アプリでは、[!INCLUDE[wrt](../../../includes/wrt-md.md)] ストリームのアダプターは、<xref:System.IO.Stream.Dispose%2A> メソッドから <xref:System.IO.Stream.FlushAsync%2A> メソッドを呼び出さなくなりました。|この変更は透過的である必要があります。 開発者は次のようなコードを記述して以前の動作を復元できます。<br /><br /> `using (System.IO.Stream stream = GetWindowsRuntimeStream() As Stream)  {     // do something     await stream.FlushAsync();   }`|透過的|  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf-runtime-changes"></a>Windows Communication Foundation (WCF) ランタイム変更  
  
|機能|変更|影響|スコープ|  
|-------------|------------|------------|-----------|  
|[minFreeMemoryPercentageToActiveService](http://msdn.microsoft.com/library/ms731336.aspx) 構成設定|WCF サービスがアクティブになる前にサーバーで使用できる必要のある最小限のメモリを設定します。 これは <xref:System.OutOfMemoryException> 例外を防止することを目的としています。 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] では、この設定は影響しません。 [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] では、設定が確認されます。|Web サーバーで使用できる空きメモリが構成設定によって定義されたパーセンテージよりも小さい場合、例外が発生します。 制約されたメモリ環境で正常に開始し、実行された WCF サービスが今度は失敗することがあります。<br /><br /> 「[軽減策: minFreeMemoryPercentageToActiveService 構成の設定](../../../docs/framework/migration-guide/mitigation-minfreememorypercentagetoactiveservice-configuration-setting.md)」を参照してください。|マイナー|  
  
## <a name="see-also"></a>関連項目  
 [変更の再ターゲット](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-5-1.md)   
 [4.5 のアプリケーションの互換性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [4.5.2 のアプリケーションの互換性](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)
