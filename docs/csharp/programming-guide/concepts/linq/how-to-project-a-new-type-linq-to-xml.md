---
title: 새 형식을 프로젝션하는 방법(LINQ to XML)(C#)
ms.date: 07/20/2015
ms.assetid: 48145cf9-1e0b-4e73-bbfd-28fc04800dc4
ms.openlocfilehash: 5205a0c56651271dea0181ed96518c0e9d7f95f3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79168995"
---
# <a name="how-to-project-a-new-type-linq-to-xml-c"></a>새 형식을 프로젝션하는 방법(LINQ to XML)(C#)

이 단원의 다른 예제에서는 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601>의 `string` 및 <xref:System.Collections.Generic.IEnumerable%601>의 `int`로 결과를 반환하는 쿼리를 보여 줍니다. 이러한 결과 형식이 일반적이지만 모든 시나리오에 적합하지는 아닙니다. 대부분의 경우 다른 형식의 <xref:System.Collections.Generic.IEnumerable%601>을 반환하는 쿼리를 작성하려고 할 수 있습니다.

## <a name="example"></a>예제

이 예제에서는 `select` 절에서 개체를 인스턴스화하는 방법을 보여 줍니다. 이 코드에서는 먼저 생성자를 사용하여 새 클래스를 정의한 다음 식이 새 클래스의 새 인스턴스이도록 `select` 문을 수정합니다.

이 예제에서는 XML 문서 [샘플 XML 파일: 일반적인 구매 주문(LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md)을 사용합니다.

```csharp
class NameQty
{
    public string name;
    public int qty;
    public NameQty(string n, int q)
    {
        name = n;
        qty = q;
    }
};

class Program {
    public static void Main()
    {
        XElement po = XElement.Load("PurchaseOrder.xml");
  
        IEnumerable<NameQty> nqList =
            from n in po.Descendants("Item")
            select new NameQty(
                    (string)n.Element("ProductName"),
                    (int)n.Element("Quantity")
                );
  
        foreach (NameQty n in nqList)
            Console.WriteLine(n.name + ":" + n.qty);
    }
}
```

이 예제에서는 <xref:System.Xml.Linq.XContainer.Element%2A>단일 자식 요소를 검색하는 방법(LINQ to XML)(C#)[ 항목에 도입된 ](how-to-retrieve-a-single-child-element-linq-to-xml.md) 메서드를 사용합니다. 또한, 캐스트를 사용하여 <xref:System.Xml.Linq.XContainer.Element%2A> 메서드에서 반환하는 요소의 값을 검색합니다.  

이 예제는 다음과 같은 출력을 생성합니다.

```output
Lawnmower:1
Baby Monitor:2
```
