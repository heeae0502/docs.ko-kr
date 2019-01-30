---
title: SqlChars.Stream 속성 (System.Data.SqlTypes)
author: douglaslMS
ms.author: douglasl
ms.date: 12/19/2018
ms.technology:
- dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlChars.Stream
- System.Data.SqlTypes.SqlChars.get_Stream
- System.Data.SqlTypes.SqlChars.set_Stream
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: d756b78a7cdbc12562e474ca3d2c9a1f3529f6bf
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54223054"
---
# <a name="sqlcharsstream-property"></a><span data-ttu-id="05202-102">SqlChars.Stream 속성</span><span class="sxs-lookup"><span data-stu-id="05202-102">SqlChars.Stream Property</span></span>

<span data-ttu-id="05202-103">문자 스트림을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05202-103">Gets or sets the character stream.</span></span> <span data-ttu-id="05202-104">이 속성을 포함 하는 어셈블리에는 SQLAccess.dll friend 관계를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="05202-104">The assembly that contains this property has a friend relationship with SQLAccess.dll.</span></span> <span data-ttu-id="05202-105">SQL Server에서 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05202-105">It's intended for use by SQL Server.</span></span> <span data-ttu-id="05202-106">다른 데이터베이스에 대 한 해당 데이터베이스에서 제공 하는 호스팅 메커니즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05202-106">For other databases, use the hosting mechanism provided by that database.</span></span>

```csharp
internal SqlStreamChars Stream { get; set; }
```

## <a name="property-value"></a><span data-ttu-id="05202-107">속성 값</span><span class="sxs-lookup"><span data-stu-id="05202-107">Property value</span></span>

`System.Data.SqlTypes.SqlStreamChars`\
<span data-ttu-id="05202-108">문자 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="05202-108">The character stream.</span></span>

## <a name="remarks"></a><span data-ttu-id="05202-109">설명</span><span class="sxs-lookup"><span data-stu-id="05202-109">Remarks</span></span>

> [!WARNING]
> <span data-ttu-id="05202-110">`SqlChars.Stream` 속성은 내부용 이며 사용자 코드에서 직접 사용할 하려고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05202-110">The `SqlChars.Stream` property is internal and is not meant to be used directly in your code.</span></span>
>
> <span data-ttu-id="05202-111">Microsoft는 어떤 상황에서 프로덕션 응용 프로그램에서이 속성의 사용을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05202-111">Microsoft does not support the use of this property in a production application under any circumstance.</span></span>

## <a name="requirements"></a><span data-ttu-id="05202-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="05202-112">Requirements</span></span>

<span data-ttu-id="05202-113">**네임스페이스:** <xref:System.Data.SqlTypes></span><span class="sxs-lookup"><span data-stu-id="05202-113">**Namespace:** <xref:System.Data.SqlTypes></span></span>

<span data-ttu-id="05202-114">**어셈블리:** System.Data (System.Data.dll)</span><span class="sxs-lookup"><span data-stu-id="05202-114">**Assembly:** System.Data (in System.Data.dll)</span></span>

<span data-ttu-id="05202-115">**.NET framework 버전:** 2.0부터 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05202-115">**.NET Framework versions:** Available since 2.0.</span></span>