---
title: Model-View-View Model과 함께 이식 가능한 클래스 라이브러리 사용
ms.date: 07/18/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Portable Class Library [.NET Framework], and MVVM
- MVVM, and Portable Class Library
ms.assetid: 41a0b9f8-15a2-431a-bc35-e310b2953b03
ms.openlocfilehash: f5312177b9f437d9b5474d38fca80db6fc45245b
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77123677"
---
# <a name="using-portable-class-library-with-model-view-view-model"></a>Model-View-View Model과 함께 이식 가능한 클래스 라이브러리 사용
.NET Framework [이식 가능한 클래스 라이브러리](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) 를 사용 하 여 MVVM (모델-뷰-뷰 모델) 패턴을 구현 하고 여러 플랫폼에서 어셈블리를 공유할 수 있습니다.

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

 MVVM은 내부 비즈니스 논리에서 사용자 인터페이스를 분리하는 애플리케이션 패턴입니다. Visual Studio 2012의 이식 가능한 클래스 라이브러리 프로젝트에서 모델을 구현 하고 모델 클래스를 볼 수 있으며, 다른 플랫폼에 맞게 사용자 지정 된 뷰를 만들 수 있습니다. 이 접근 방식을 사용 하면 다음 그림과 같이 데이터 모델 및 비즈니스 논리를 한 번만 작성 하 고 .NET Framework, Silverlight, Windows Phone 및 Windows 8.x 스토어 앱에서 해당 코드를 사용할 수 있습니다.

 ![플랫폼 간에 어셈블리를 MVVM 공유 하는 이식 가능한 클래스 라이브러리를 보여 줍니다.](./media/using-portable-class-library-with-model-view-view-model/mvvm-share-assemblies-across-platforms.png)

 이 항목에서는 MVVM 패턴에 대한 일반 정보를 제공 하지 않습니다. 이식 가능한 클래스 라이브러리를 사용하여 MVVM를 구현하는 방법에 대한 정보만 제공 합니다. MVVM에 대한 자세한 내용은 [프리즘 Library 5.0 FOR WPF를 사용하여 MVVM 빠른](https://docs.microsoft.com/previous-versions/msp-n-p/gg430857(v=pandp.40))시작을 참조 하세요.

## <a name="classes-that-support-mvvm"></a>MVVM를 지원하는 클래스
 이식 가능한 클래스 라이브러리 프로젝트에 대해 .NET Framework 4.5, .NET for Windows 8.x 스토어 앱, Silverlight 또는 Windows Phone 7.5를 대상으로 하는 경우 MVVM 패턴을 구현 하는 데 다음 클래스를 사용할 수 있습니다.

- <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType> 클래스

- <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.NotifyCollectionChangedAction?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.NotifyCollectionChangedEventArgs?displayProperty=nameWithType> 클래스

- <xref:System.Collections.Specialized.NotifyCollectionChangedEventHandler?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.DataErrorsChangedEventArgs?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.INotifyDataErrorInfo?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.INotifyPropertyChanged?displayProperty=nameWithType> 클래스

- <xref:System.Windows.Input.ICommand?displayProperty=nameWithType> 클래스

- <xref:System.ComponentModel.DataAnnotations?displayProperty=nameWithType> 네임 스페이스의 모든 클래스

## <a name="implementing-mvvm"></a>MVVM 구현
 MVVM를 구현 하려면 이식 가능한 클래스 라이브러리 프로젝트에서 이식 불가능한 프로젝트를 참조할 수 없으므로 일반적으로 이식 가능한 클래스 라이브러리 프로젝트에 모델 및 뷰 모델을 만듭니다. 모델 및 뷰 모델은 동일한 프로젝트 또는 별도의 프로젝트에 있을 수 있습니다. 별도의 프로젝트를 사용 하는 경우 모델 프로젝트에 뷰 모델 프로젝트의 참조를 추가 합니다.

 모델 및 뷰 모델 프로젝트를 컴파일하고 나면 뷰를 포함 하는 응용 프로그램에서 해당 어셈블리를 참조 합니다. 뷰가 뷰 모델과만 상호 작용 하는 경우 뷰 모델을 포함 하는 어셈블리만 참조 하면 됩니다.

### <a name="model"></a>모델
 다음 예제에서는 이식 가능한 클래스 라이브러리 프로젝트에 있을 수 있는 간소화 된 모델 클래스를 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#1](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customer.cs#1)]
 [!code-vb[PortableClassLibraryMVVM#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customer.vb#1)]

 다음 예제에서는 이식 가능한 클래스 라이브러리 프로젝트의 데이터를 간단 하게 채우고, 검색하고, 업데이트 하는 방법을 보여 줍니다. 실제 앱에서는 WCF (Windows Communication Foundation) 서비스와 같은 소스에서 데이터를 검색 합니다.

 [!code-csharp[PortableClassLibraryMVVM#2](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/customerrepository.cs#2)]
 [!code-vb[PortableClassLibraryMVVM#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerrepository.vb#2)]

### <a name="view-model"></a>모델 보기
 MVVM 패턴을 구현할 때 뷰 모델에 대 한 기본 클래스가 자주 추가 됩니다. 다음 예제에서는 기본 클래스를 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#3](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/viewmodelbase.cs#3)]
 [!code-vb[PortableClassLibraryMVVM#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/viewmodelbase.vb#3)]

 MVVM 패턴을 사용 하는 경우에는 <xref:System.Windows.Input.ICommand> 인터페이스의 구현이 자주 사용 됩니다. 다음 예제에서는 <xref:System.Windows.Input.ICommand> 인터페이스의 구현을 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#4](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/relaycommand.cs#4)]
 [!code-vb[PortableClassLibraryMVVM#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/relaycommand.vb#4)]

 다음 예에서는 간단한 뷰 모델을 보여 줍니다.

 [!code-csharp[PortableClassLibraryMVVM#5](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainpageviewmodel.cs#5)]
 [!code-vb[PortableClassLibraryMVVM#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/portableclasslibrarymvvm/vb/customerviewmodel.vb#5)]  
  
### <a name="view"></a>보기  
 .NET Framework 4.5 앱, Windows 8.x 스토어 앱, Silverlight 기반 앱 또는 Windows Phone 7.5 앱에서 모델 및 뷰 모델 프로젝트를 포함 하는 어셈블리를 참조할 수 있습니다.  그런 다음 뷰 모델과 상호 작용 하는 뷰를 만듭니다. 다음 예제에서는 뷰 모델에서 데이터를 검색 하 고 업데이트 하는 간단한 WPF (Windows Presentation Foundation) 앱을 보여 줍니다. Silverlight, Windows Phone 또는 Windows 8.x 스토어 앱에서 유사한 뷰를 만들 수 있습니다.  
  
 [!code-xaml[PortableClassLibraryMVVM#6](../../../samples/snippets/csharp/VS_Snippets_CLR/portableclasslibrarymvvm/cs/mainwindow.xaml#6)]  
  
## <a name="see-also"></a>참고 항목

- [이식 가능한 클래스 라이브러리](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)
