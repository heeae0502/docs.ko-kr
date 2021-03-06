---
title: 기본 클래스 라이브러리 호환성이 손상되는 변경
description: 기본 클래스 라이브러리인 .NET CoreFx 관련 호환성이 손상되는 변경 목록입니다.
ms.date: 09/20/2019
ms.openlocfilehash: 56a3cf4f4c00a79752d5a98bb086bb9f8c0614b1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79147577"
---
# <a name="corefx-breaking-changes"></a>CoreFx 관련 호환성이 손상되는 변경

CoreFx는 .NET Core에서 사용되는 기본 형식과 기타 일반적인 형식을 제공합니다.

이 페이지에는 다음과 같은 주요 변경 사항이 설명되어 있습니다.

| 주요 변경 내용 | 도입된 버전 |
| - | :-: |
| [버전을 보고하는 API가 이제 파일 버전이 아닌 제품 버전을 보고함](#apis-that-report-version-now-report-product-and-not-file-version) | 3.0 |
| [사용자 지정 EncoderFallbackBuffer 인스턴스는 재귀적으로 대체될 수 없음](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | 3.0 |
| [부동 소수점 서식 및 구문 분석 동작 변경](#floating-point-formatting-and-parsing-behavior-changed) | 3.0 |
| [부동 소수점 구문 분석 작업은 더 이상 실패하거나 OverflowException을 throw하지 않음](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | 3.0 |
| [InvalidAsynchronousStateException이 다른 어셈블리로 이동됨](#invalidasynchronousstateexception-moved-to-another-assembly) | 3.0 |
| [.NET Core 3.0이 잘못된 형식의 UTF-8 바이트 시퀀스를 대체할 때 유니코드 모범 사례를 적용](#net-core-30-follows-unicode-best-practices-when-replacing-ill-formed-utf-8-byte-sequences) | 3.0 |
| [TypeDescriptionProviderAttribute가 다른 어셈블리로 이동됨](#typedescriptionproviderattribute-moved-to-another-assembly) | 3.0 |
| [ZipArchiveEntry가 더 이상 일치하지 않는 항목 크기의 아카이브를 처리하지 않음](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | 3.0 |
| [JSON 직렬 변환기 예외 형식이 JsonException에서 NotSupportedException으로 변경됨](#json-serializer-exception-type-changed-from-jsonexception-to-notsupportedexception) | 3.0 |
| [Utf8JsonWriter에서 (문자열)null의 의미 체계가 변경됨](#change-in-semantics-of-stringnull-in-utf8jsonwriter) | 3.0 |
| [JsonEncodedText.Encode 메서드에 JavaScriptEncoder 인수 추가](#jsonencodedtextencode-methods-have-an-additional-javascriptencoder-argument) | 3.0 |
| [JsonFactoryConverter.CreateConverter 서명이 변경되었습니다.](#jsonfactoryconvertercreateconverter-signature-changed) | 3.0 |
| [JsonElement API 변경 내용](#jsonelement-api-changes) | 3.0 |
| [FieldInfo.SetValue가 초기화 전용 정적 필드에 대해 예외를 throw](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | 3.0 |
| [기본 제공 구조체 형식에 추가된 프라이빗 필드](#private-fields-added-to-built-in-struct-types) | 2.1 |
| [UseShellExecute의 기본값 변경](#change-in-default-value-of-useshellexecute) | 2.1 |
| [macOS의 OpenSSL 버전](#openssl-versions-on-macos) | 2.1 |
| [FileSystemInfo.Attributes가 throw하는 UnauthorizedAccessException](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | 1.0 |

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

***

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

***

[!INCLUDE[JSON serializer exception type changed from JsonException to NotSupportedException](~/includes/core-changes/corefx/3.0/serializer-throws-notsupportedexception.md)]

***

[!INCLUDE[Change in semantics of (string)null in Utf8JsonWriter](~/includes/core-changes/corefx/3.0/change-in-null-in-utf8jsonwriter.md)]

***

[!INCLUDE[JsonEncodedText.Encode methods have an additional JavaScriptEncoder argument](~/includes/core-changes/corefx/3.0/jsonencodedtext-encode-has-additional-argument.md)]

***

[!INCLUDE[JsonFactoryConverter.CreateConverter signature changed](~/includes/core-changes/corefx/3.0/jsonfactoryconverter-createconverter.md)]

***

[!INCLUDE[JsonElement API changes](~/includes/core-changes/corefx/3.0/jsonelement-api-changes.md)]

***

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

***

## <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

***

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

***

## <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***
