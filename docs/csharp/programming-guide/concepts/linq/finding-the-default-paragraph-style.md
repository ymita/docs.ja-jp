---
title: "既定の段落スタイルの検索 (C#) | Microsoft Docs"
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
ms.assetid: be102177-8ab0-444a-b671-7023e555ffdb
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 71aa37ffc086298470b713470afb4c28d3c5fcca
ms.lasthandoff: 03/13/2017


---
# <a name="finding-the-default-paragraph-style-c"></a>既定の段落スタイルの検索 (C#)
「WordprocessingML ドキュメント内の情報の操作」チュートリアルでの最初のタスクは、ドキュメント内にある段落の既定のスタイルを検索することです。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、Office Open XML WordprocessingML ドキュメントを開き、パッケージのドキュメント パーツとスタイル パーツを検索した後、既定のスタイル名を検索するクエリを実行します。 Office Open XML ドキュメント パッケージおよびその構成パーツについて詳しくは、「[Office Open XML WordprocessingML ドキュメントの詳細 (C#)](../../../../csharp/programming-guide/concepts/linq/details-of-office-open-xml-wordprocessingml-documents.md)」をご覧ください。  
  
 このクエリは、値が "paragraph" である `w:style` という名前の属性と、値が "1" である `w:type` という名前の属性を持つ `w:default` という名前のノードを検索します。 これらの属性を持つ XML ノードは 1 つしかないため、このクエリは、<xref:System.Linq.Enumerable.First%2A?displayProperty=fullName> 演算子を使ってコレクションをシングルトンに変換します。 次に、`w:styleId` という名前の属性の値を取得します。  
  
 この例では、WindowsBase アセンブリのクラスを使用します。 また、<xref:System.IO.Packaging?displayProperty=fullName> 名前空間内の型を使用します。  
  
### <a name="code"></a>コード  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship =  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
          docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation =  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
// The following query finds all the paragraphs that have the default style.  
string defaultStyle =   
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
Console.WriteLine("The default style is: {0}", defaultStyle);  
```  
  
### <a name="comments"></a>コメント  
 この例を実行すると、次の出力が生成されます。  
  
```  
The default style is: Normal  
```  
  
## <a name="next-steps"></a>次の手順  
 次の例では、ドキュメント内のすべての段落およびそのスタイルを検索する同様のクエリを記述します。  
  
-   [段落とそのスタイルの取得 (C#)](../../../../csharp/programming-guide/concepts/linq/retrieving-the-paragraphs-and-their-styles.md)  
  
## <a name="see-also"></a>関連項目  
 [チュートリアル: WordprocessingML ドキュメント内のコンテンツの操作](http://msdn.microsoft.com/library/2696355e-4f83-4eaf-91b2-baa721f42fb4)
