---
title: 오류 처리 및 오류 보고에 대한 확장 제어
ms.date: 03/30/2017
ms.assetid: 45f996a7-fa00-45cb-9d6f-b368f5778aaa
ms.openlocfilehash: 68f3381e8db9d7c0222720dda335b47e30f57ac7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183676"
---
# <a name="extending-control-over-error-handling-and-reporting"></a>오류 처리 및 오류 보고에 대한 확장 제어
이 샘플에서는 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 사용하여 WCF(Windows 통신 Foundation) 서비스에서 오류 처리 및 오류 보고에 대한 제어를 확장하는 방법을 보여 줍니다. 샘플은 오류를 처리하기 위해 서비스에 추가된 몇 가지 추가 코드로 [시작하기를](../../../../docs/framework/wcf/samples/getting-started-sample.md) 기반으로 합니다. 클라이언트에서는 몇 가지 오류 조건을 발생시키고 서비스에서는 해당 오류를 가로채서 파일에 기록합니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 서비스에서는 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 사용하여 오류를 가로채고, 처리를 수행하고, 오류를 보고하는 방법에 영향을 줄 수 있습니다. 인터페이스에는 구현할 수 있는 두 개의 메서드 <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> 및 <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A>가 있습니다. <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> 메서드를 사용하면 예외에 대한 응답으로 생성되는 오류 메시지를 추가, 수정 또는 제거할 수 있습니다. <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> 메서드를 사용하면 오류가 발생한 경우 오류 처리를 허용하고 추가 오류 처리를 실행할 수 있는지 여부를 제어할 수 있습니다.  
  
 이 샘플에서 `CalculatorErrorHandler` 형식은 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 구현합니다. 먼저  
  
 <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> 메서드에서 `CalculatorErrorHandler`는 c:\logs에 있는 Error.txt 텍스트 파일에 오류 로그를 기록합니다. 샘플에서는 오류를 기록한 후 제거하지 않으므로 해당 오류를 클라이언트에 다시 보고할 수 있습니다.  
  
```csharp
public class CalculatorErrorHandler : IErrorHandler
{
    // Provide a fault. The Message fault parameter can be replaced, or set to
    // null to suppress reporting a fault.

    public void ProvideFault(Exception error, MessageVersion version, ref Message fault)
    {
    }

    // HandleError. Log an error, then allow the error to be handled as usual.
    // Return true if the error is considered as already handled

    public bool HandleError(Exception error)
    {
        using (TextWriter tw = File.AppendText(@"c:\logs\error.txt"))
        {
            if (error != null)
            {
                tw.WriteLine("Exception: " + error.GetType().Name + " - " + error.Message);
            }
            tw.Close();
        }
        return true;
    }
}  
```  
  
 `ErrorBehaviorAttribute`는 서비스에 오류 처리기를 등록하는 데 사용되는 메커니즘입니다. 이 특성에서는 단일 형식 매개 변수를 받습니다. 그 형식은 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 구현해야 하며 비어 있는 public 생성자가 있어야 합니다. 그러면 이 특성에서 해당 오류 처리기 형식의 인스턴스를 만들어 서비스에 설치합니다. 이 작업을 수행하려면 <xref:System.ServiceModel.Description.IServiceBehavior> 인터페이스를 구현한 다음 <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> 메서드를 사용하여 오류 처리기의 인스턴스를 서비스에 추가하면 됩니다.  
  
```csharp
// This attribute can be used to install a custom error handler for a service.  
public class ErrorBehaviorAttribute : Attribute, IServiceBehavior  
{  
    Type errorHandlerType;  
  
    public ErrorBehaviorAttribute(Type errorHandlerType)  
    {  
        this.errorHandlerType = errorHandlerType;  
    }  
  
    void IServiceBehavior.Validate(ServiceDescription description, ServiceHostBase serviceHostBase)  
    {  
    }  
  
    void IServiceBehavior.AddBindingParameters(ServiceDescription description, ServiceHostBase serviceHostBase, System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints, BindingParameterCollection parameters)  
    {  
    }  
  
    void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
    {  
        IErrorHandler errorHandler;  
  
        try  
        {  
            errorHandler = (IErrorHandler)Activator.CreateInstance(errorHandlerType);  
        }  
        catch (MissingMethodException e)  
        {  
            throw new ArgumentException("The errorHandlerType specified in the ErrorBehaviorAttribute constructor must have a public empty constructor.", e);  
        }  
        catch (InvalidCastException e)  
        {  
            throw new ArgumentException("The errorHandlerType specified in the ErrorBehaviorAttribute constructor must implement System.ServiceModel.Dispatcher.IErrorHandler.", e);  
        }  
  
        foreach (ChannelDispatcherBase channelDispatcherBase in serviceHostBase.ChannelDispatchers)  
        {  
            ChannelDispatcher channelDispatcher = channelDispatcherBase as ChannelDispatcher;  
            channelDispatcher.ErrorHandlers.Add(errorHandler);  
        }
    }  
}  
```  
  
 샘플에서는 계산기 서비스를 구현합니다. 클라이언트에서는 잘못된 값이 있는 매개 변수를 공급하여 고의로 서비스에 두 개의 오류를 일으킵니다. `CalculatorErrorHandler`에서는 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 사용하여 로컬 파일에 오류를 기록한 다음 클라이언트에 다시 보고될 수 있도록 합니다. 클라이언트에서는 0으로 나누기와 argument-out-of-range 조건을 발생시킵니다.  
  
```csharp
try
{  
    Console.WriteLine("Forcing an error in Divide");  
    // Call the Divide service operation - trigger a divide by 0 error.  
    value1 = 22;  
    value2 = 0;  
    result = proxy.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
}  
catch (FaultException e)  
{  
    Console.WriteLine("FaultException: " + e.GetType().Name + " - " + e.Message);  
}  
catch (Exception e)  
{  
    Console.WriteLine("Exception: " + e.GetType().Name + " - " + e.Message);  
}  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 0으로 나누기와 argument-out-of-range 조건이 오류로 보고되는 것을 볼 수 있습니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
Forcing an error in Divide  
FaultException: FaultException - Invalid Argument: The second argument must not be zero.  
Forcing an error in Factorial  
FaultException: FaultException - Invalid Argument: The argument must be greater than zero.  
  
Press <ENTER> to terminate client.  
```  
  
 c:\logs\errors.txt 파일에는 서비스에서 오류에 대해 기록한 정보가 포함되어 있습니다. 서비스가 디렉터리에 쓸 수 있도록 하려면 서비스가 실행 중인 프로세스(일반적으로 ASP.NET 또는 네트워크 서비스)에 디렉터리에 쓸 수 있는 권한이 있는지 확인해야 합니다.  
  
```txt
Fault: Reason = Invalid Argument: The second argument must not be zero.  
Fault: Reason = Invalid Argument: The argument must be greater than zero.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. Windows 통신 기초 [샘플에 대한 일회성 설치 절차를](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)수행했어야 합니다.  
  
2. 솔루션을 빌드하려면 Windows 통신 [기초 샘플 빌드의 지침을 따르십시오.](../../../../docs/framework/wcf/samples/building-the-samples.md)  
  
3. error.txt 파일을 보관할 c:\logs 디렉터리를 만들었는지 확인합니다. 또는 `CalculatorErrorHandler.HandleError`에 사용된 파일 이름을 수정합니다.  
  
4. 단일 또는 교차 컴퓨터 구성에서 샘플을 실행하려면 Windows [통신 기반 샘플 실행의 지침을 따르십시오.](../../../../docs/framework/wcf/samples/running-the-samples.md)  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대한 WCF(Windows 통신 재단) 및 WF(Windows 워크플로우 재단) 샘플로](https://www.microsoft.com/download/details.aspx?id=21459) 이동하여 모든 WCF(Windows 통신 재단) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\ErrorHandling`  
