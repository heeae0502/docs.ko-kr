---
title: XName 개체의 사전 원자화(LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 06ea104b-f44c-4bb2-9c34-889ae025c80d
ms.openlocfilehash: c0e75afa797d2b20f32fc55e6c19d0c1593d174c
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76740786"
---
# <a name="pre-atomization-of-xname-objects-linq-to-xml-visual-basic"></a>LINQ to XML (원자화 of 명령의 xname Objects) (Visual Basic)

LINQ to XML의 성능을 향상시키는 한 가지 방법은 <xref:System.Xml.Linq.XName> 개체를 사전 원자화하는 것입니다. 원자화는 <xref:System.Xml.Linq.XElement> 및 <xref:System.Xml.Linq.XAttribute> 클래스의 생성자를 사용 하 여 XML 트리를 만들기 전에 <xref:System.Xml.Linq.XName> 개체에 문자열을 할당 하는 것을 의미 합니다. 그런 다음 문자열을 생성자에 전달하여 문자열을 <xref:System.Xml.Linq.XName>으로 암시적으로 변환하는 대신 초기화된 <xref:System.Xml.Linq.XName> 개체를 전달합니다.

이렇게 하면 특정 이름이 반복되는 대형 XML 트리를 만드는 경우 성능이 향상됩니다. 이렇게 하려면 XML 트리를 만들기 전에 <xref:System.Xml.Linq.XName> 개체를 선언하고 초기화합니다. 그런 다음 요소 및 특성 이름에 대한 문자열을 지정하는 대신 이 <xref:System.Xml.Linq.XName> 개체를 사용합니다. 이 방법을 사용하면 같은 이름으로 매우 많은 요소 또는 특성을 만드는 경우 상당한 성능상의 이점을 얻을 수 있습니다.

이 방법을 사용할지 여부를 결정하려면 사용자 시나리오를 사전 원자화해 보는 것이 좋습니다.

## <a name="example"></a>예제

다음은 이에 대한 예입니다.

```vb
Dim root1 As XName = "Root"
Dim data As XName = "Data"
Dim id As XName = "ID"

Dim root2 As New XElement(root1, New XElement(data, New XAttribute(id, "1"), "4,100,000"),
                          New XElement(data, New XAttribute(id, "2"), "3,700,000"),
                          New XElement(data, New XAttribute(id, "3"), "1,150,000"))

Console.WriteLine(root2)
```

이 예에서 생성되는 출력은 다음과 같습니다.

```xml
<Root>
  <Data ID="1">4,100,000</Data>
  <Data ID="2">3,700,000</Data>
  <Data ID="3">1,150,000</Data>
</Root>
```

다음 예제에서는 XML 문서가 네임스페이스에 있는 동일한 방법을 보여 줍니다.

```vb
Dim aw As XNamespace = "http://www.adventure-works.com"
Dim root1 As XName = aw + "Root"
Dim data As XName = aw + "Data"
Dim id As XName = "ID"

Dim root2 As New XElement(root1, New XAttribute(XNamespace.Xmlns + "aw", aw),
                          New XElement(data, New XAttribute(id, "1"), "4,100,000"),
                          New XElement(data, New XAttribute(id, "2"), "3,700,000"),
                          New XElement(data, New XAttribute(id, "3"), "1,150,000"))

Console.WriteLine(root2)
```

이 예에서 생성되는 출력은 다음과 같습니다.

```xml
<aw:Root xmlns:aw="http://www.adventure-works.com">
  <aw:Data ID="1">4,100,000</aw:Data>
  <aw:Data ID="2">3,700,000</aw:Data>
  <aw:Data ID="3">1,150,000</aw:Data>
</aw:Root>
```

다음 예제는 실제로 사용될 수 있는 것과 더욱 유사한 코드입니다. 이 예제에서 요소의 내용은 쿼리를 통해 제공됩니다.

```vb
Dim root1 As XName = "Root"
Dim data As XName = "Data"
Dim id As XName = "ID"
  
Dim sw As Stopwatch = Stopwatch.StartNew()
Dim root2 As New XElement(root1, From i In Enumerable.Range(1, 100000)
                                 Select New XElement(data, New XAttribute(ID, i), i * 5))
sw.Stop()
Console.WriteLine($"Time to construct: {sw.ElapsedMilliseconds} milliseconds")
```  

위 예제는 이름이 사전 원자화되지 않은 다음 예제보다 더 나은 성능을 제공합니다.

```vb
Dim sw As Stopwatch = Stopwatch.StartNew()
Dim root As New XElement("Root", From i In Enumerable.Range(1, 100000)
                                 Select New XElement("Data", New XAttribute("ID", i), i * 5))
sw.Stop()
Console.WriteLine($"Time to construct: {sw.ElapsedMilliseconds} milliseconds")
```

## <a name="see-also"></a>참고 항목

- [성능 (LINQ to XML) (Visual Basic)](performance-linq-to-xml.md)
- [원자화 명령의 xname 및 XNamespace 개체 (LINQ to XML) (Visual Basic)](atomized-xname-and-xnamespace-objects-linq-to-xml.md)
