---
title: DacpGetModuleAddress 구조
ms.date: 01/16/2019
api.name:
- DacpGetModuleAddress Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpGetModuleAddress Structure
helpviewer.keywords:
- DacpGetModuleAddress Structure [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: c0a12ab638adfccfb6406aa495bd3568911ee969
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54619781"
---
# <a name="dacpgetmoduleaddress-structure"></a><span data-ttu-id="e718e-102">DacpGetModuleAddress 구조</span><span class="sxs-lookup"><span data-stu-id="e718e-102">DacpGetModuleAddress Structure</span></span>

<span data-ttu-id="e718e-103">모듈 주소 요청에 대 한 컨테이너를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e718e-103">Defines the container for a module address request.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="e718e-104">구문</span><span class="sxs-lookup"><span data-stu-id="e718e-104">Syntax</span></span>

```
struct DacpGetModuleAddress
{
    CLRDATA_ADDRESS ModulePtr;
};
```

## <a name="members"></a><span data-ttu-id="e718e-105">멤버</span><span class="sxs-lookup"><span data-stu-id="e718e-105">Members</span></span>

| <span data-ttu-id="e718e-106">멤버</span><span class="sxs-lookup"><span data-stu-id="e718e-106">Member</span></span>      | <span data-ttu-id="e718e-107">설명</span><span class="sxs-lookup"><span data-stu-id="e718e-107">Description</span></span>                |
| ----------- | -------------------------- |
| `ModulePtr` | <span data-ttu-id="e718e-108">모듈에 대 한 포인터입니다.</span><span class="sxs-lookup"><span data-stu-id="e718e-108">The pointer to the module.</span></span> |

## <a name="methods"></a><span data-ttu-id="e718e-109">메서드</span><span class="sxs-lookup"><span data-stu-id="e718e-109">Methods</span></span>

| <span data-ttu-id="e718e-110">메서드</span><span class="sxs-lookup"><span data-stu-id="e718e-110">Method</span></span>                                                                                               | <span data-ttu-id="e718e-111">설명</span><span class="sxs-lookup"><span data-stu-id="e718e-111">Description</span></span>                                                                    |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [<span data-ttu-id="e718e-112">요청</span><span class="sxs-lookup"><span data-stu-id="e718e-112">Request</span></span>](../../../../docs/framework/unmanaged-api/debugging/dacpgetmoduleaddress-request-method.md) | <span data-ttu-id="e718e-113">지정 된 런타임 구조에서 구조를 채우는 데 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e718e-113">Performs a request to populate the structure from the given runtime structure.</span></span> |

## <a name="remarks"></a><span data-ttu-id="e718e-114">설명</span><span class="sxs-lookup"><span data-stu-id="e718e-114">Remarks</span></span>

<span data-ttu-id="e718e-115">이 구조는 런타임 내에서 있으며 모든 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e718e-115">This structure lives inside the runtime and is not exposed through any headers or library files.</span></span> <span data-ttu-id="e718e-116">를 사용 하려면 구조를 정의 위에 지정 된 대로 위치 `CLRDATA_ADDRESS` 는 64 비트 부호 없는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="e718e-116">To use it, define the structure as specified above, where `CLRDATA_ADDRESS` is a 64-bit unsigned integer.</span></span>

## <a name="requirements"></a><span data-ttu-id="e718e-117">요구 사항</span><span class="sxs-lookup"><span data-stu-id="e718e-117">Requirements</span></span>
<span data-ttu-id="e718e-118">**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e718e-118">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
<span data-ttu-id="e718e-119">**헤더:** 없음</span><span class="sxs-lookup"><span data-stu-id="e718e-119">**Header:** None</span></span>  
<span data-ttu-id="e718e-120">**라이브러리:** 없음</span><span class="sxs-lookup"><span data-stu-id="e718e-120">**Library:** None</span></span>  
<span data-ttu-id="e718e-121">**.NET Framework 버전:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="e718e-121">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="e718e-122">참고자료</span><span class="sxs-lookup"><span data-stu-id="e718e-122">See also</span></span>
- [<span data-ttu-id="e718e-123">디버깅</span><span class="sxs-lookup"><span data-stu-id="e718e-123">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [<span data-ttu-id="e718e-124">디버깅 구조체</span><span class="sxs-lookup"><span data-stu-id="e718e-124">Debugging Structures</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)