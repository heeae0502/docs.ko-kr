---
title: '자습서: 자전거 대여 수요 예측 - 시계열'
description: 이 자습서에서는 시계열 분석 및 ML.NET를 사용하여 자전거 대여 서비스 수요를 예측하는 방법을 보여 줍니다.
ms.date: 10/31/2019
ms.topic: tutorial
ms.custom: mvc
ms.author: luquinta
author: luisquintanilla
ms.openlocfilehash: f30aac5f8467c2410e9008bafea3cf35af3f4e2a
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73425372"
---
# <a name="tutorial-forecast-bike-rental-service-demand-with-time-series-analysis-and-mlnet"></a><span data-ttu-id="6f1af-103">자습서: 시계열 분석 및 ML.NET를 사용하여 자전거 대여 서비스 수요 예측</span><span class="sxs-lookup"><span data-stu-id="6f1af-103">Tutorial: Forecast bike rental service demand with time series analysis and ML.NET</span></span>

<span data-ttu-id="6f1af-104">ML.NET를 통해 SQL Server 데이터베이스에 저장된 데이터에 대한 단일 시계열 분석을 사용하여 자전거 대여 서비스 수요를 예측하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-104">Learn how to forecast demand for a bike rental service using univariate time series analysis on data stored in a SQL Server database with ML.NET.</span></span>

<span data-ttu-id="6f1af-105">이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> * <span data-ttu-id="6f1af-106">문제 이해</span><span class="sxs-lookup"><span data-stu-id="6f1af-106">Understand the problem</span></span>
> * <span data-ttu-id="6f1af-107">데이터베이스에서 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="6f1af-107">Load data from a database</span></span>
> * <span data-ttu-id="6f1af-108">예측 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="6f1af-108">Create a forecasting model</span></span>
> * <span data-ttu-id="6f1af-109">예측 모델 평가</span><span class="sxs-lookup"><span data-stu-id="6f1af-109">Evaluate forecasting model</span></span>
> * <span data-ttu-id="6f1af-110">예측 모델 저장</span><span class="sxs-lookup"><span data-stu-id="6f1af-110">Save a forecasting model</span></span>
> * <span data-ttu-id="6f1af-111">예측 모델 사용</span><span class="sxs-lookup"><span data-stu-id="6f1af-111">Use a forecasting model</span></span>

> [!NOTE]
> <span data-ttu-id="6f1af-112">이 자습서에서는 DatabaseLoader의 미리 보기 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-112">This tutorial uses a preview version of DatabaseLoader.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f1af-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="6f1af-113">Prerequisites</span></span>

- <span data-ttu-id="6f1af-114">“.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="6f1af-114">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) with the ".NET Core cross-platform development" workload installed.</span></span>

## <a name="time-series-forecasting-sample-overview"></a><span data-ttu-id="6f1af-115">시계열 예측 샘플 개요</span><span class="sxs-lookup"><span data-stu-id="6f1af-115">Time series forecasting sample overview</span></span>

<span data-ttu-id="6f1af-116">이 샘플은 단일 스펙트럼 분석이라고 하는 일변량 시계열 분석 알고리즘을 사용하여 자전거 대여 수요를 예측하는 **C# .NET Core 콘솔 애플리케이션**입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-116">This sample is a **C# .NET Core console application** that forecasts demand for bike rentals using a univariate time series analysis algorithm known as Single Spectrum Analysis.</span></span> <span data-ttu-id="6f1af-117">이 샘플의 코드는 GitHub의 [dotnet/machinelearning-samples repository](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-117">The code for this sample can be found on the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand) repository on GitHub.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="6f1af-118">문제 이해</span><span class="sxs-lookup"><span data-stu-id="6f1af-118">Understand the problem</span></span>

<span data-ttu-id="6f1af-119">효율적인 작업을 실행하기 위해 재고 관리는 주요 역할을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-119">In order to run an efficient operation, inventory management plays a key role.</span></span> <span data-ttu-id="6f1af-120">재고가 너무 많은 제품이 있다면 제품이 판매되지 않은 채 진열대에 쌓여 아무런 수익을 창출하지 않는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-120">Having too much of a product in stock means unsold products sitting on the shelves not generating any revenue.</span></span> <span data-ttu-id="6f1af-121">제품 수가 너무 적으면 판매 및 고객 손실이 발생하여 경쟁사에게 고객을 빼앗길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-121">Having too little product leads to lost sales and customers purchasing from competitors.</span></span> <span data-ttu-id="6f1af-122">따라서 가장 적합한 재고 보유량에 대해 끊임없는 질문을 던져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-122">Therefore, the constant question is, what is the optimal amount of inventory to keep on hand?</span></span> <span data-ttu-id="6f1af-123">시계열 분석은 기록 데이터를 보고 패턴을 식별하고 이 정보를 사용하여 나중에 값을 예측하는 방식으로 이러한 질문에 대한 답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-123">Time-series analysis helps provide an answer to these questions by looking at historical data, identifying patterns, and using this information to forecast values some time in the future.</span></span> 

<span data-ttu-id="6f1af-124">이 자습서에서 사용되는 데이터를 분석하는 방법은 일변량 시계열 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-124">The technique for analyzing data used in this tutorial is univariate time-series analysis.</span></span> <span data-ttu-id="6f1af-125">일변량 시계열 분석은 월별 판매량 같은 특정 간격으로 일정 기간의 단일 수치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-125">Univariate time-series analysis takes a look at a single numerical observation over a period of time at specific intervals such as monthly sales.</span></span> 

<span data-ttu-id="6f1af-126">이 자습서에서 사용되는 알고리즘은 [SSA(단일 스펙트럼 분석)](http://ssa.cf.ac.uk/zhigljavsky/pdfs/SSA/SSA_encyclopedia.pdf)입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-126">The algorithm used in this tutorial is [Single Spectrum Analysis(SSA)](http://ssa.cf.ac.uk/zhigljavsky/pdfs/SSA/SSA_encyclopedia.pdf).</span></span> <span data-ttu-id="6f1af-127">SSA는 시계열을 주요 구성 요소 집합으로 분리하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-127">SSA works by decomposing a time-series into a set of principal components.</span></span> <span data-ttu-id="6f1af-128">이러한 구성 요소는 추세, 노이즈, 계절성 및 기타 여러 요소에 해당하는 신호의 일부분으로 해석될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-128">These components can be interpreted as the parts of a signal that correspond to trends, noise, seasonality, and many other factors.</span></span> <span data-ttu-id="6f1af-129">그런 다음 이러한 구성 요소가 재구성되어 나중에 값을 예측하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-129">Then, these components are reconstructed and used to forecast values some time in the future.</span></span>

## <a name="create-console-application"></a><span data-ttu-id="6f1af-130">콘솔 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="6f1af-130">Create console application</span></span>

1. <span data-ttu-id="6f1af-131">"BikeDemandForecasting"이라는 새 **C# .NET Core 애플리케이션**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-131">Create a new **C# .NET Core console application** called "BikeDemandForecasting".</span></span>
1. <span data-ttu-id="6f1af-132">**Microsoft.ML** 버전 **1.4.0-preview2** NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-132">Install **Microsoft.ML** version **1.4.0-preview2** NuGet package</span></span>
    1. <span data-ttu-id="6f1af-133">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-133">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span>
    1. <span data-ttu-id="6f1af-134">패키지 소스로 “nuget.org”를 선택하고, **찾아보기** 탭을 선택하고, **Microsoft.ML**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-134">Choose "nuget.org" as the Package source, select the **Browse** tab, search for **Microsoft.ML**.</span></span>
    1. <span data-ttu-id="6f1af-135">**시험판 포함** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-135">Check the **Include prerelease** checkbox.</span></span>
    1. <span data-ttu-id="6f1af-136">**설치** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-136">Select the **Install** button.</span></span>
    1. <span data-ttu-id="6f1af-137">**변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 [라이선스 승인] 대화 상자에서 **동의함** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-137">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the License Acceptance dialog if you agree with the license terms for the packages listed.</span></span>
    1. <span data-ttu-id="6f1af-138">**System.Data.SqlClient** 버전 **4.7.0**, **Microsoft.ML.Experimental** 버전 **0.16.0-preview2**, **Microsoft.ML.TimeSeries** 버전 **1.4.0-preview2**에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-138">Repeat these steps for **System.Data.SqlClient** version **4.7.0**, **Microsoft.ML.Experimental** version **0.16.0-preview2**, and **Microsoft.ML.TimeSeries** version **1.4.0-preview2**.</span></span>

### <a name="prepare-and-understand-the-data"></a><span data-ttu-id="6f1af-139">데이터 준비 및 이해</span><span class="sxs-lookup"><span data-stu-id="6f1af-139">Prepare and understand the data</span></span>

1. <span data-ttu-id="6f1af-140">*데이터* 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-140">Create a directory called *Data*.</span></span>
1. <span data-ttu-id="6f1af-141">[*DailyDemand.mdf* 데이터베이스 파일](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Data/DailyDemand.mdf)을 다운로드하여 *데이터* 디렉터리에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-141">Download the [*DailyDemand.mdf* database file](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Data/DailyDemand.mdf) and save it to the *Data* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="6f1af-142">이 자습서에서 사용되는 데이터는 [UCI 자전거 공유 데이터 세트](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-142">The data used in this tutorial comes from the [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset).</span></span> <span data-ttu-id="6f1af-143">Fanaee-T, Hadi, Gama, Joao, 'Event labeling combining ensemble detectors and background knowledge', Progress in Artificial Intelligence (2013): pp. 1-15, Springer Berlin Heidelberg, [웹 링크](https://link.springer.com/article/10.1007%2Fs13748-013-0040-3).</span><span class="sxs-lookup"><span data-stu-id="6f1af-143">Fanaee-T, Hadi, and Gama, Joao, 'Event labeling combining ensemble detectors and background knowledge', Progress in Artificial Intelligence (2013): pp. 1-15, Springer Berlin Heidelberg, [Web Link](https://link.springer.com/article/10.1007%2Fs13748-013-0040-3).</span></span>

<span data-ttu-id="6f1af-144">원본 데이터 세트에는 계절성 및 날씨에 해당하는 여러 열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-144">The original dataset contains several columns corresponding to seasonality and weather.</span></span> <span data-ttu-id="6f1af-145">간단히 하기 위해 이 자습서에서 사용되는 알고리즘에는 단일 숫자 열의 값만 필요하므로 원본 데이터 세트는 다음 열만 포함하도록 압축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-145">For brevity and because the algorithm used in this tutorial only requires the values from a single numerical column, the original dataset has been condensed to include only the following columns:</span></span>  

- <span data-ttu-id="6f1af-146">**dteday**: 관측 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-146">**dteday**: The date of the observation.</span></span>
- <span data-ttu-id="6f1af-147">**year**: 인코딩된 관측 연도입니다(0=2011, 1=2012).</span><span class="sxs-lookup"><span data-stu-id="6f1af-147">**year**: The encoded year of the observation (0=2011, 1=2012).</span></span>
- <span data-ttu-id="6f1af-148">**cnt**: 해당 일에 대한 총 자전거 대여 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-148">**cnt**: The total number of bike rentals for that day.</span></span>

<span data-ttu-id="6f1af-149">원본 데이터 세트는 SQL Server 데이터베이스에서 다음 스키마를 포함하는 데이터베이스 테이블에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-149">The original dataset is mapped to a database table with the following schema in a SQL Server database.</span></span>

```SQL
CREATE TABLE [Rentals] (
    [RentalDate] DATE NOT NULL,
    [Year] INT NOT NULL,
    [TotalRentals] INT NOT NULL
);
```

<span data-ttu-id="6f1af-150">다음은 데이터 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-150">The following is a sample of the data:</span></span>

| <span data-ttu-id="6f1af-151">RentalDate</span><span class="sxs-lookup"><span data-stu-id="6f1af-151">RentalDate</span></span> | <span data-ttu-id="6f1af-152">Year</span><span class="sxs-lookup"><span data-stu-id="6f1af-152">Year</span></span> | <span data-ttu-id="6f1af-153">TotalRentals</span><span class="sxs-lookup"><span data-stu-id="6f1af-153">TotalRentals</span></span> |
| --- | --- | --- |
|<span data-ttu-id="6f1af-154">1/1/2011</span><span class="sxs-lookup"><span data-stu-id="6f1af-154">1/1/2011</span></span>|<span data-ttu-id="6f1af-155">0</span><span class="sxs-lookup"><span data-stu-id="6f1af-155">0</span></span>|<span data-ttu-id="6f1af-156">985</span><span class="sxs-lookup"><span data-stu-id="6f1af-156">985</span></span>|
|<span data-ttu-id="6f1af-157">1/2/2011</span><span class="sxs-lookup"><span data-stu-id="6f1af-157">1/2/2011</span></span>|<span data-ttu-id="6f1af-158">0</span><span class="sxs-lookup"><span data-stu-id="6f1af-158">0</span></span>|<span data-ttu-id="6f1af-159">801</span><span class="sxs-lookup"><span data-stu-id="6f1af-159">801</span></span>|
|<span data-ttu-id="6f1af-160">1/3/2011</span><span class="sxs-lookup"><span data-stu-id="6f1af-160">1/3/2011</span></span>|<span data-ttu-id="6f1af-161">0</span><span class="sxs-lookup"><span data-stu-id="6f1af-161">0</span></span>|<span data-ttu-id="6f1af-162">1349</span><span class="sxs-lookup"><span data-stu-id="6f1af-162">1349</span></span>|

### <a name="create-input-and-output-classes"></a><span data-ttu-id="6f1af-163">입력 및 출력 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="6f1af-163">Create input and output classes</span></span>

1. <span data-ttu-id="6f1af-164">*Program.cs* 파일을 열고 기존 `using` 문을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-164">Open *Program.cs* file and replace the existing `using` statements with the following:</span></span>

    [!code-csharp [ProgramUsings](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L1-L8)]

1. <span data-ttu-id="6f1af-165">`ModelInput` 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-165">Create `ModelInput` class.</span></span> <span data-ttu-id="6f1af-166">`Program` 클래스 아래에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-166">Below the `Program` class, add the following code.</span></span>

    [!code-csharp [ModelInputClass](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L120-L127)]    

    <span data-ttu-id="6f1af-167">`ModelInput` 클래스에는 다음 열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-167">The `ModelInput` class contains the following columns:</span></span>

    - <span data-ttu-id="6f1af-168">**RentalDate**: 관측 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-168">**RentalDate**: The date of the observation.</span></span>
    - <span data-ttu-id="6f1af-169">**Year**: 인코딩된 관측 연도입니다(0=2011, 1=2012).</span><span class="sxs-lookup"><span data-stu-id="6f1af-169">**Year**: The encoded year of the observation (0=2011, 1=2012).</span></span>
    - <span data-ttu-id="6f1af-170">**TotalRentals**: 해당 일에 대한 총 자전거 대여 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-170">**TotalRentals**: The total number of bike rentals for that day.</span></span>

1. <span data-ttu-id="6f1af-171">새로 만든 `ModelInput` 클래스 아래에 `ModelOutput` 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-171">Create `ModelOutput` class below the newly created `ModelInput` class.</span></span>

    [!code-csharp [ModelOutputClass](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L129-L136)]

    <span data-ttu-id="6f1af-172">`ModelOutput` 클래스에는 다음 열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-172">The `ModelOutput` class contains the following columns:</span></span>

    - <span data-ttu-id="6f1af-173">**ForecastedRentals**: 예측 기간의 예측 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-173">**ForecastedRentals**: The predicted values for the forecasted period.</span></span>
    - <span data-ttu-id="6f1af-174">**LowerBoundRentals**: 예측 기간의 예측 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-174">**LowerBoundRentals**: The predicted minimum values for the forecasted period.</span></span>
    - <span data-ttu-id="6f1af-175">**UpperBoundRentals**: 예측 기간의 예측 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-175">**UpperBoundRentals**: The predicted maximum values for the forecasted period.</span></span>

### <a name="define-paths-and-initialize-variables"></a><span data-ttu-id="6f1af-176">경로 정의 및 변수 초기화</span><span class="sxs-lookup"><span data-stu-id="6f1af-176">Define paths and initialize variables</span></span>

1. <span data-ttu-id="6f1af-177">`Main` 메서드 내에서 데이터의 위치, 연결 문자열 및 학습된 모델을 저장할 위치를 저장하는 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-177">Inside the `Main` method, define variables to store the location of your data, connection string, and where to save the trained model.</span></span>

    [!code-csharp [DefinePaths](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L16-L19)]

1. <span data-ttu-id="6f1af-178">`Main` 메서드에 다음 줄을 추가하여 [`MLContext`](xref:Microsoft.ML.MLContext)의 새로운 인스턴스로 `mlContext` 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-178">Initialize the `mlContext` variable with a new instance of [`MLContext`](xref:Microsoft.ML.MLContext) by adding the following line to the `Main` method.</span></span>

    [!code-csharp [MLContext](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L21)]

    <span data-ttu-id="6f1af-179">[`MLContext`](xref:Microsoft.ML.MLContext) 클래스는 모든 ML.NET 작업의 시작점이며, mlContext를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-179">The [`MLContext`](xref:Microsoft.ML.MLContext) class is a starting point for all ML.NET operations, and initializing mlContext creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="6f1af-180">개념적으로 Entity Framework의 `DBContext`와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-180">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="6f1af-181">데이터 로드</span><span class="sxs-lookup"><span data-stu-id="6f1af-181">Load the data</span></span>

1. <span data-ttu-id="6f1af-182">`ModelInput` 형식의 레코드를 로드하는 `DatabaseLoader`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-182">Create `DatabaseLoader` that loads records of type `ModelInput`.</span></span>

    [!code-csharp [CreateDBLoader](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L23)]

1. <span data-ttu-id="6f1af-183">데이터베이스에서 데이터를 로드하는 쿼리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-183">Define the query to load the data from the database.</span></span>

    [!code-csharp [DefineSQLQuery](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L25)]

    <span data-ttu-id="6f1af-184">ML.NET 알고리즘은 데이터를 [`Single`](xref:System.Single) 형식으로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-184">ML.NET algorithms expect data to be of type [`Single`](xref:System.Single).</span></span> <span data-ttu-id="6f1af-185">따라서 [`Real`](xref:System.Data.SqlDbType) 형식이 아닌 데이터베이스에서 가져온 숫자 값(단정밀도 부동 소수점 값)은 [`Real`](xref:System.Data.SqlDbType)로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-185">Therefore, numerical values coming from the database that are not of type [`Real`](xref:System.Data.SqlDbType), a single-precision floating-point value, have to be converted to [`Real`](xref:System.Data.SqlDbType).</span></span> 

    <span data-ttu-id="6f1af-186">`Year` 및 `TotalRental` 열은 모두 데이터베이스의 정수 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-186">The `Year` and `TotalRental` columns are both integer types in the database.</span></span> <span data-ttu-id="6f1af-187">`CAST` 기본 제공 함수를 사용하여 `Real`로 캐스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-187">Using the `CAST` built-in function, they are both cast to `Real`.</span></span>

1. <span data-ttu-id="6f1af-188">데이터베이스에 연결하고 쿼리를 실행하는 `DatabaseSource`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-188">Create a `DatabaseSource` to connect to the database and execute the query.</span></span>

    [!code-csharp [CreateDBSource](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L27-L29)]

1. <span data-ttu-id="6f1af-189">데이터를 `IDataView`에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-189">Load the data into an `IDataView`.</span></span>

    [!code-csharp [LoadData](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L31)]

1. <span data-ttu-id="6f1af-190">데이터 세트에는 두 개 연도 분량의 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-190">The dataset contains two years worth of data.</span></span> <span data-ttu-id="6f1af-191">첫 번째 연도의 데이터만 학습에 사용되고, 두 번째 연도는 모델에서 생성된 예측과 실제 값을 비교하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-191">Only data from the first year is used for training, the second year is held out to compare the actual values against the forecast produced by the model.</span></span> <span data-ttu-id="6f1af-192">[`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*) 변환을 사용하여 데이터를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-192">Filter the data using the [`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*) transform.</span></span> 

    [!code-csharp [SplitData](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L33-L34)]

    <span data-ttu-id="6f1af-193">첫 번째 연도의 경우 `upperBound` 매개 변수를 1로 설정하여 `Year` 열의 값만 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-193">For the first year, only the values in the `Year` column less than 1 are selected by setting the `upperBound` parameter to 1.</span></span> <span data-ttu-id="6f1af-194">반면 두 번째 연도의 경우 `lowerBound` 매개 변수를 1로 설정하여 1 이상의 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-194">Conversely, for the second year, values greater than or equal to 1 are selected by setting the `lowerBound` parameter to 1.</span></span>

## <a name="define-time-series-analysis-pipeline"></a><span data-ttu-id="6f1af-195">시계열 분석 파이프라인 정의</span><span class="sxs-lookup"><span data-stu-id="6f1af-195">Define time series analysis pipeline</span></span>

1. <span data-ttu-id="6f1af-196">[SsaForecastingEstimator](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator)를 사용하여 시계열 데이터 세트의 값을 예측하는 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-196">Define a pipeline that uses the [SsaForecastingEstimator](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator) to forecast values in a time-series dataset.</span></span>

    [!code-csharp [DefinePipeline](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L36-L45)]

    <span data-ttu-id="6f1af-197">`forecastingPipeline`은 첫 번째 연도와 샘플에 대해 365개의 데이터 요소를 사용하거나 시계열 데이터 세트를 `seriesLength` 매개 변수에 지정된 대로 30일(월별) 간격으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-197">The `forecastingPipeline` takes 365 data points for the first year and samples or splits the time-series dataset into 30-day (monthly) intervals as specified by the `seriesLength` parameter.</span></span> <span data-ttu-id="6f1af-198">이러한 각 샘플은 주별 또는 7일 기간을 통해 분석됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-198">Each of these samples is analyzed through weekly or a 7-day window.</span></span> <span data-ttu-id="6f1af-199">다음 기간에 대한 예측 값을 결정할 때 이전 7일의 값을 사용하여 예측을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-199">When determining what the forecasted value for the next period(s) is, the values from previous seven days are used to make a prediction.</span></span> <span data-ttu-id="6f1af-200">모델은 `horizon` 매개 변수로 정의된 대로 향후 7일의 기간을 예측하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-200">The model is set to forecast seven periods into the future as defined by the `horizon` parameter.</span></span> <span data-ttu-id="6f1af-201">예측은 추측이므로 항상 100% 정확하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-201">Because a forecast is an informed guess, it's not always 100% accurate.</span></span> <span data-ttu-id="6f1af-202">따라서 상한 및 하한으로 정의된 최선 및 최악의 시나리오 값 범위를 파악하고 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-202">Therefore, it's good to know the range of values in the best and worst-case scenarios as defined by the upper and lower bounds.</span></span> <span data-ttu-id="6f1af-203">이 경우 하한 및 상한에 대한 신뢰 수준은 95%로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-203">In this case, the level of confidence for the lower and upper bounds is set to 95%.</span></span> <span data-ttu-id="6f1af-204">신뢰 수준을 적절하게 높이거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-204">The confidence level can be increased or decreased accordingly.</span></span> <span data-ttu-id="6f1af-205">값이 높을수록 원하는 수준의 신뢰도를 얻기 위해 상한 및 하한 간 범위가 넓어집니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-205">The higher the value, the wider the range is between the upper and lower bounds to achieve the desired level of confidence.</span></span> 

1. <span data-ttu-id="6f1af-206">[`Fit`](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator.Fit*) 메서드를 사용하여 모델을 학습하고 이전에 정의된 `forecastingPipeline`에 데이터를 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-206">Use the [`Fit`](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator.Fit*) method to train the model and fit the data to the previously defined `forecastingPipeline`.</span></span>

    [!code-csharp [TrainModel](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L47)]

## <a name="evaluate-the-model"></a><span data-ttu-id="6f1af-207">모델 평가</span><span class="sxs-lookup"><span data-stu-id="6f1af-207">Evaluate the model</span></span>

<span data-ttu-id="6f1af-208">다음 연도의 데이터를 예측하고 실제 값과 비교하여 모델이 얼마나 잘 수행하고 있는지 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-208">Evaluate how well the model performs by forecasting next year's data and comparing it against the actual values.</span></span>

1. <span data-ttu-id="6f1af-209">`Main` 메서드 아래 `Evaluate`라는 새 유틸리티 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-209">Below the `Main` method, create a new utility method called `Evaluate`.</span></span>

    ```csharp
    static void Evaluate(IDataView testData, ITransformer model, MLContext mlContext)
    {
        
    }
    ```

1. <span data-ttu-id="6f1af-210">`Evaluate` 메서드 내에서 학습된 모델과 함께 [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) 메서드를 사용하여 두 번째 연도의 데이터를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-210">Inside the `Evaluate` method, forecast the second year's data by using the [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) method with the trained model.</span></span>

    [!code-csharp [EvaluateForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L62)]

1. <span data-ttu-id="6f1af-211">[`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) 메서드를 사용하여 데이터에서 실제 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-211">Get the actual values from the data by using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) method.</span></span>

    [!code-csharp [GetActualRentals](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L65-L67)]

1. <span data-ttu-id="6f1af-212">[`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) 메서드를 사용하여 예측 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-212">Get the forecast values by using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) method.</span></span>

    [!code-csharp [GetForecastRentals](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L70-L72)]

1. <span data-ttu-id="6f1af-213">일반적으로 오류라고 하는 실제 값과 예측 값의 차이를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-213">Calculate the difference between the actual and forecast values, commonly referred to as the error.</span></span>

    [!code-csharp [CalculateError](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L75)]

1. <span data-ttu-id="6f1af-214">절대 평균 오차 및 제곱 평균 오차 값을 계산하여 성능을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-214">Measure performance by computing the Mean Absolute Error and Root Mean Squared Error values.</span></span>

    [!code-csharp [CalculateMetrics](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L78-L79)]

    <span data-ttu-id="6f1af-215">성능을 평가하기 위해 다음 메트릭이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-215">To evaluate performance, the following metrics are used:</span></span>

    - <span data-ttu-id="6f1af-216">**절대 평균 오차**: 예측이 실제 값과 얼마나 근접한지 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-216">**Mean Absolute Error**: Measures how close predictions are to the actual value.</span></span> <span data-ttu-id="6f1af-217">이 값의 범위는 0과 무한대 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-217">This value ranges between 0 and infinity.</span></span> <span data-ttu-id="6f1af-218">0에 가까울수록 모델의 품질이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-218">The closer to 0, the better the quality of the model.</span></span>
    - <span data-ttu-id="6f1af-219">**제곱 평균 오차**: 모델에서 오류를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-219">**Root Mean Squared Error**: Summarizes thhe error in the model.</span></span> <span data-ttu-id="6f1af-220">이 값의 범위는 0과 무한대 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-220">This value ranges between 0 and infinity.</span></span> <span data-ttu-id="6f1af-221">0에 가까울수록 모델의 품질이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-221">The closer to 0, the better the quality of the model.</span></span>

1. <span data-ttu-id="6f1af-222">메트릭을 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-222">Output the metrics to the console.</span></span>

    [!code-csharp [OutputMetrics](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L82-L85)]

1. <span data-ttu-id="6f1af-223">`Main` 메서드 내에 `Evaluate` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-223">Use the `Evaluate` method inside the `Main` method.</span></span>

    [!code-csharp [EvaluateModel](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L49)]

## <a name="save-the-model"></a><span data-ttu-id="6f1af-224">모델 저장</span><span class="sxs-lookup"><span data-stu-id="6f1af-224">Save the model</span></span>

<span data-ttu-id="6f1af-225">모델에 만족하는 경우 나중에 다른 애플리케이션에서 사용할 수 있도록 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-225">If you're satisfied with your model, save it for later use in other applications.</span></span>

1. <span data-ttu-id="6f1af-226">`Main` 메서드에서 [`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-226">In the `Main` method, create a [`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602).</span></span> <span data-ttu-id="6f1af-227">[`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602)은 단일 예측을 만드는 편리한 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-227">[`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602) is a convenience method to make single predictions.</span></span>

    [!code-csharp [CreateTimeSeriesEngine](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L51)]

1. <span data-ttu-id="6f1af-228">이전에 정의된 `modelPath` 변수에 지정된 대로 `MLModel.zip`이라는 파일에 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-228">Save the model to a file called `MLModel.zip` as specified by the previously defined `modelPath` variable.</span></span> <span data-ttu-id="6f1af-229">[`Checkpoint`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.CheckPoint*) 메서드를 사용하여 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-229">Use the [`Checkpoint`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.CheckPoint*) method to save the model.</span></span>

    [!code-csharp [SaveModel](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L52)]

## <a name="use-the-model-to-forecast-demand"></a><span data-ttu-id="6f1af-230">모델을 사용하여 수요 예측</span><span class="sxs-lookup"><span data-stu-id="6f1af-230">Use the model to forecast demand</span></span>

1. <span data-ttu-id="6f1af-231">`Evaluate` 메서드 아래 `Forecast`라는 새 유틸리티 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-231">Below the `Evaluate` method, create a new utility method called `Forecast`.</span></span>

    ```csharp
    static void Forecast(IDataView testData, int horizon, TimeSeriesPredictionEngine<ModelInput, ModelOutput> forecaster, MLContext mlContext)
    {

    }
    ```

1. <span data-ttu-id="6f1af-232">`Forecast` 메서드 내에서 [`Predict`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.Predict*) 메서드를 사용하여 다음 7일 동안의 대여를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-232">Inside the `Forecast` method, use the [`Predict`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.Predict*) method to forecast rentals for the next seven days.</span></span>

    [!code-csharp [SingleForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L91)]

1. <span data-ttu-id="6f1af-233">7일간의 실제 값과 예측 값을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-233">Align the actual and forecast values for seven periods.</span></span>

    [!code-csharp [GetForecastOutput](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L93-L108)]

1. <span data-ttu-id="6f1af-234">예측 출력을 반복하여 콘솔에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-234">Iterate through the forecast output and display it on the console.</span></span>

    [!code-csharp [DisplayForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L111-L116)]

## <a name="run-the-application"></a><span data-ttu-id="6f1af-235">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="6f1af-235">Run the application</span></span>

1. <span data-ttu-id="6f1af-236">`Main` 메서드 내에서 `Forecast` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-236">Inside the `Main` method, call the `Forecast` method.</span></span>

    [!code-csharp [BuildForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L54)]

1. <span data-ttu-id="6f1af-237">애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-237">Run the application.</span></span> <span data-ttu-id="6f1af-238">아래와 유사한 출력이 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-238">Output similar to that below should appear on the console.</span></span> <span data-ttu-id="6f1af-239">간단히 표시하기 위해 출력이 압축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-239">For brevity, the output has been condensed.</span></span>

    ```text
    Evaluation Metrics
    ---------------------
    Mean Absolute Error: 726.416
    Root Mean Squared Error: 987.658

    Rental Forecast
    ---------------------
    Date: 1/1/2012
    Actual Rentals: 2294
    Lower Estimate: 1197.842
    Forecast: 2334.443
    Upper Estimate: 3471.044

    Date: 1/2/2012
    Actual Rentals: 1951
    Lower Estimate: 1148.412
    Forecast: 2360.861
    Upper Estimate: 3573.309
    ```

<span data-ttu-id="6f1af-240">실제 값 및 예측 값을 검사하면 다음과 같은 관계가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-240">Inspection of the actual and forecasted values shows the following relationships:</span></span>

![실제 및 예측 비교](./media/time-series-demand-forecasting/forecast.png)

<span data-ttu-id="6f1af-242">예측 값이 정확한 대여 수를 예측하지는 않지만 더 좁은 범위의 값을 제공하여 작업에서 리소스 사용을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-242">While the forecasted values are not predicting the exact number of rentals, they provide a more narrow range of values that allows an operation to optimize their use of resources.</span></span> 

<span data-ttu-id="6f1af-243">지금까지</span><span class="sxs-lookup"><span data-stu-id="6f1af-243">Congratulations!</span></span> <span data-ttu-id="6f1af-244">이제 자전거 대여 수요를 예측하는 시계열 기계 학습 모델을 성공적으로 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-244">You've now successfully built a time series machine learning model to forecast bike rental demand.</span></span>

<span data-ttu-id="6f1af-245">[dotnet/samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1af-245">You can find the source code for this tutorial at the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand) repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f1af-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f1af-246">Next steps</span></span>

- [<span data-ttu-id="6f1af-247">ML.NET의 기계 학습 작업</span><span class="sxs-lookup"><span data-stu-id="6f1af-247">Machine learning tasks in ML.NET</span></span>](../resources/tasks.md)
- [<span data-ttu-id="6f1af-248">모델 정확도 향상</span><span class="sxs-lookup"><span data-stu-id="6f1af-248">Improve model accuracy</span></span>](../resources/improve-machine-learning-model-ml-net.md)