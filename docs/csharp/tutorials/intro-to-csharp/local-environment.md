---
title: C# 소개 - 개발 도구 익히기
description: 이 문서에서는 머신에서 C# 및 .NET 응용 프로그램을 개발하는 데 사용할 도구의 기본 사항을 소개합니다.
ms.date: 10/23/2018
ms.openlocfilehash: ec7e55fbf2a89a8ec45db956fc575edeb2283f56
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200164"
---
# <a name="become-familiar-with-the-net-development-tools"></a><span data-ttu-id="a75ca-103">.NET 개발 도구 익히기</span><span class="sxs-lookup"><span data-stu-id="a75ca-103">Become familiar with the .NET development tools</span></span>

<span data-ttu-id="a75ca-104">머신에서 자습서를 실행하는 첫 번째 단계는 개발 환경을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-104">The first step in running a tutorial on your machine is to set up a development environment.</span></span>
<span data-ttu-id="a75ca-105">.NET 항목 [Get Started in 10 minutes](https://www.microsoft.com/net/core)(10분 안에 시작)에는 Mac, PC 또는 Linux의 로컬 개발 환경 설정에 대한 지침이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-105">The .NET topic [Get Started in 10 minutes](https://www.microsoft.com/net/core) has instructions for setting up your local development environment on Mac, PC or Linux.</span></span>

<span data-ttu-id="a75ca-106">또는 [.NET Core SDK](https://www.microsoft.com/net/download) 및 [Visual Studio Code](https://code.visualstudio.com/)를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-106">Alternatively, you can install the [.NET Core SDK](https://www.microsoft.com/net/download) and [Visual Studio Code](https://code.visualstudio.com/).</span></span>

## <a name="basic-application-development-flow"></a><span data-ttu-id="a75ca-107">기본 응용 프로그램 개발 흐름</span><span class="sxs-lookup"><span data-stu-id="a75ca-107">Basic application development flow</span></span>

<span data-ttu-id="a75ca-108">[`dotnet new`](../../../core/tools/dotnet-new.md) 명령을 사용하여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-108">You'll create applications using the [`dotnet new`](../../../core/tools/dotnet-new.md) command.</span></span> <span data-ttu-id="a75ca-109">이 명령은 응용 프로그램에 필요한 파일과 자산을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-109">This command generates the files and assets necessary for your application.</span></span> <span data-ttu-id="a75ca-110">C# 소개 자습서에서는 모두 `console` 응용 프로그램 유형을 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-110">The introduction to C# tutorials all use the `console` application type.</span></span> <span data-ttu-id="a75ca-111">기본 사항을 알고 나면 다른 응용 프로그램 유형으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-111">Once you've got the basics, you can expand to other application types.</span></span>

<span data-ttu-id="a75ca-112">사용할 다른 명령은 실행 파일을 빌드하기 위한 [`dotnet build`](../../../core/tools/dotnet-build.md) 및 실행 파일을 실행하기 위한 [`dotnet run`](../../../core/tools/dotnet-run.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-112">The other commands you'll use are [`dotnet build`](../../../core/tools/dotnet-build.md) to build the executable, and [`dotnet run`](../../../core/tools/dotnet-run.md) to run the executable.</span></span>

## <a name="pick-your-turorial"></a><span data-ttu-id="a75ca-113">자습서 선택</span><span class="sxs-lookup"><span data-stu-id="a75ca-113">Pick your turorial</span></span>

<span data-ttu-id="a75ca-114">다음과 같은 자습서 중 하나를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-114">You can start with any of the following tutorials:</span></span>

## <a name="numbers-in-cnumbers-in-csharp-localmd"></a>[<span data-ttu-id="a75ca-115">C#의 숫자</span><span class="sxs-lookup"><span data-stu-id="a75ca-115">Numbers in C#</span></span>](numbers-in-csharp-local.md)

<span data-ttu-id="a75ca-116">[C#의 숫자](numbers-in-csharp-local.md) 자습서에서는 컴퓨터가 숫자를 저장하는 방법과 여러 숫자 형식으로 계산을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-116">In the [Numbers in C#](numbers-in-csharp-local.md) tutorial, you'll learn how computers store numbers and how to perform calculations with different numeric types.</span></span> <span data-ttu-id="a75ca-117">반올림의 기본 사항과 C#을 사용하여 수학 계산을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-117">You'll learn the basics of rounding and how to perform mathematical calculations using C#.</span></span>

<span data-ttu-id="a75ca-118">이 자습서에서는 [Hello World](hello-world.yml) 단원을 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-118">This tutorial assumes that you have finished the [Hello world](hello-world.yml) lesson.</span></span>

## <a name="branches-and-loopsbranches-and-loops-localmd"></a>[<span data-ttu-id="a75ca-119">분기 및 루프</span><span class="sxs-lookup"><span data-stu-id="a75ca-119">Branches and loops</span></span>](branches-and-loops-local.md)

<span data-ttu-id="a75ca-120">[분기 및 루프](branches-and-loops-local.md) 자습서에서는 변수에 저장된 값에 따라 코드 실행의 여러 경로를 선택하는 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-120">The [Branches and loops](branches-and-loops-local.md) tutorial teaches the basics of selecting different paths of code execution based on the values stored in variables.</span></span> <span data-ttu-id="a75ca-121">프로그램에서 결정하고 여러 작업을 선택하는 방법에 대한 기본 사항인 제어 흐름의 기본 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-121">You'll learn the basics of control flow, which is the basis of how programs make decisions and choose different actions.</span></span>

<span data-ttu-id="a75ca-122">이 자습서에서는 [Hello World](hello-world.yml) 및 [C#의 숫자](numbers-in-csharp-local.md) 단원을 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-122">This tutorial assumes that you have finished the [Hello world](hello-world.yml) and [Numbers in C#](numbers-in-csharp-local.md) lessons.</span></span>

## <a name="string-interpolationinterpolated-strings-localmd"></a>[<span data-ttu-id="a75ca-123">문자열 보간</span><span class="sxs-lookup"><span data-stu-id="a75ca-123">String interpolation</span></span>](interpolated-strings-local.md)

<span data-ttu-id="a75ca-124">[문자열 보간](interpolated-strings-local.md) 자습서에서는 문자열에 값을 삽입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-124">The [String interpolation](interpolated-strings-local.md) tutorial shows you how to insert values into a string.</span></span> <span data-ttu-id="a75ca-125">포함된 C# 식을 사용하여 보간된 문자열을 만드는 방법과 결과 문자열의 형식을 제어하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-125">You'll learn how to create an interpolated string with embedded C# expressions and how to control the formatting of the result string.</span></span>

<span data-ttu-id="a75ca-126">이 자습서에서는 [Hello World](hello-world.yml), [C#의 숫자](numbers-in-csharp-local.md) 및 [분기 및 루프](branches-and-loops-local.md) 단원을 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-126">This tutorial assumes that you have finished the [Hello world](hello-world.yml), [Numbers in C#](numbers-in-csharp-local.md), and [Branches and loops](branches-and-loops-local.md) lessons.</span></span>

## <a name="list-collectionarrays-and-collectionsmd"></a>[<span data-ttu-id="a75ca-127">목록 컬렉션</span><span class="sxs-lookup"><span data-stu-id="a75ca-127">List collection</span></span>](arrays-and-collections.md)

<span data-ttu-id="a75ca-128">[목록 컬렉션](arrays-and-collections.md) 단원에서는 데이터 시퀀스를 저장하는 목록 컬렉션 형식을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-128">The [List collection](arrays-and-collections.md) lesson gives you a tour of the List collection type that stores sequences of data.</span></span> <span data-ttu-id="a75ca-129">항목을 추가 및 제거하고, 항목을 검색하고, 목록을 정렬하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-129">You'll learn how to add and remove items, search for items, and sort the lists.</span></span> <span data-ttu-id="a75ca-130">여러 종류의 목록을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-130">You'll explore different kinds of lists.</span></span> 

<span data-ttu-id="a75ca-131">이 자습서에서는 위에 나열된 단원을 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-131">This tutorial assumes that you have finished the lessons listed above.</span></span>

## <a name="introduction-to-classesintroduction-to-classesmd"></a>[<span data-ttu-id="a75ca-132">클래스 소개</span><span class="sxs-lookup"><span data-stu-id="a75ca-132">Introduction to classes</span></span>](introduction-to-classes.md)

<span data-ttu-id="a75ca-133">이 마지막 C# 소개 자습서는 사용자의 로컬 개발 환경 및 .NET Core를 사용하여 사용자의 머신에서만 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-133">This final introduction to C# tutorial is only available to run on your machine, using your own local development environment and .NET Core.</span></span>
<span data-ttu-id="a75ca-134">콘솔 응용 프로그램을 빌드하고 C# 언어의 일부인 기본 개체 지향 기능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a75ca-134">You'll build a console application and see the basic object-oriented features that are part of the C# language.</span></span>