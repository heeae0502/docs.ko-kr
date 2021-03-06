---
title: LINQ to XML 개요
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
ms.openlocfilehash: 0481a140541a7f45c682c5150bc1c3d647de90bd
ms.sourcegitcommit: 43d10ef65f0f1fd6c3b515e363bde11a3fcd8d6d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/04/2020
ms.locfileid: "78266900"
---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a>Visual Basic의 LINQ to XML 개요
Visual Basic은 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] XML 리터럴 및 XML 축 속성을 통해 지원을 제공합니다. 이렇게 하면 Visual Basic 코드에서 XML로 작업할 때 친숙하고 편리한 구문을 사용할 수 있습니다. *XML 리터럴을* 사용하면 코드에 XML을 직접 포함할 수 있습니다. *XML 축 속성을* 사용하면 자식 노드, 하위 노드 및 XML 리터럴의 특성에 액세스할 수 있습니다. 자세한 내용은 시각적 기본에서 [XML 리터럴 개요](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md) 및 [XML 액세스](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)를 참조하십시오.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]는 LINQ(언어 통합 쿼리)를 활용하도록 특별히 설계된 메모리 내 XML 프로그래밍 API입니다. LINQ API를 직접 호출할 수 있지만 Visual Basic만 XML 리터럴을 선언하고 XML 축 속성에 직접 액세스할 수 있습니다.  
  
> [!NOTE]
> XML 리터럴 및 XML 축 속성은 ASP.NET 페이지의 선언적 코드에서 지원되지 않습니다. Visual Basic XML 기능을 사용하려면 ASP.NET 응용 프로그램의 코드 숨미기 페이지에 코드를 넣습니다.  
  
 [재생 버튼](./media/overview-of-linq-to-xml/play-video-icon-example.gif) 관련 비디오 데모의 경우 [LINQ에서 XML로 시작하는 방법과 LINQ에서](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-get-started-with-linq-to-xml) [XML로 Excel 스프레드시트를 만드는 방법을 참조하세요.](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-create-excel-spreadsheets-using-linq-to-xml)
  
## <a name="creating-xml"></a>XML 만들기  
 시각적 기본에서 XML 트리를 만드는 방법에는 두 가지가 있습니다. 코드에서 XML 리터럴을 직접 선언하거나 LINQ API를 사용하여 트리를 만들 수 있습니다. 두 프로세스 를 사용하면 코드가 XML 트리의 최종 구조를 반영할 수 있습니다. 예를 들어 다음 코드 예제에서는 XML 요소를 만듭니다.  
  
 [!code-vb[VbXmlSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 자세한 내용은 [시각적 기본에서 XML 만들기를](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)참조하십시오.  
  
## <a name="accessing-and-navigating-xml"></a>XML 액세스 및 탐색  
 Visual Basic은 XML 구조에 액세스하고 탐색하기 위한 XML 축 속성을 제공합니다. 이러한 속성을 사용하면 XML 자식 요소 이름을 지정하여 XML 요소 및 특성에 액세스할 수 있습니다. 또는 요소 및 특성을 탐색하고 찾기 위해 LINQ 메서드를 명시적으로 호출할 수 있습니다. 예를 들어 다음 코드 예제에서는 XML 축 속성을 사용하여 XML 요소의 특성 및 자식 요소를 참조합니다. 코드 예제에서는 LINQ 쿼리를 사용하여 자식 요소를 검색하고 XML 요소로 출력하여 변환을 효과적으로 수행합니다.  
  
 [!code-vb[VbXmlSamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples3.vb#8)]  
  
 자세한 내용은 [시각적 기본에서 XML 액세스 를](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)참조하십시오.  
  
## <a name="xml-namespaces"></a>XML 네임스페이스  
 Visual Basic을 사용하면 문을 사용하여 전역 XML 네임스페이스에 별칭을 지정할 수 있습니다. `Imports` 다음 예제에서는 `Imports` 문을 사용하여 XML 네임스페이스를 가져오는 방법을 보여 주며 있습니다.  
  
 [!code-vb[VbXMLSamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#1)]  
  
 XML 축 속성에 액세스하고 XML 문서 및 요소에 대해 XML 리터럴을 선언할 때 XML 네임스페이스 별칭을 사용할 수 있습니다.  
  
 <xref:System.Xml.Linq.XNamespace> [GetXmlNamespace 연산자](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)를 사용하여 특정 네임스페이스 접두사에 대한 개체를 검색할 수 있습니다.  
  
 자세한 내용은 [가져오기 문(XML 네임스페이스)을](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)참조하십시오.  
  
### <a name="using-xml-namespaces-in-xml-literals"></a>XML 리터럴에서 XML 네임스페이스 사용  
 다음 예제에서는 전역 네임스페이스를 <xref:System.Xml.Linq.XElement> `ns`사용하는 개체를 만드는 방법을 보여 주며 다음과 같은 방법을 보여 주며 있습니다.  
  
 [!code-vb[VbXMLSamples#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#2)]  
  
 Visual Basic 컴파일러는 XML 네임스페이스 별칭을 포함하는 XML 리터럴을 `xmlns` 특성과 함께 XML 네임스페이스를 사용하기 위해 XML 표기법을 사용하는 동등한 코드로 변환합니다. 컴파일할 때 이전 섹션예제의 코드는 기본적으로 다음 예제와 동일한 실행 코드를 생성합니다.  
  
 [!code-vb[VbXMLSamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#3)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a>XML 축 속성에서 XML 네임스페이스 사용  
 XML 리터럴로 선언된 XML 네임스페이스는 XML 축 속성에서 사용할 수 없습니다. 그러나 전역 네임스페이스는 XML 축 속성과 함께 사용할 수 있습니다. 콜론을 사용하여 XML 네임스페이스 접두사를 로컬 요소 이름과 분리합니다. 다음은 예제입니다.  
  
 [!code-vb[VbXMLSamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#4)]  
  
## <a name="see-also"></a>참고 항목

- [Xml](../../../../visual-basic/programming-guide/language-features/xml/index.md)
- [Visual Basic에서 XML 만들기](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Visual Basic에서 XML에 액세스](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
- [Visual Basic에서 XML 조작](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
