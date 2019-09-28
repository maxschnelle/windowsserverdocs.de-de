---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: Planen der Interoperabilität mit AD FS 1.x
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e9f72bd83c90a804749329521a72e3232589c735
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407961"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Planen der Interoperabilität mit AD FS 1.x

Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Verbund Servern, auf denen Windows Server® 2012 ausgeführt wird, können sowohl mit einer AD FS 1,0 \(installiert werden, die mit Windows Server 2003 R2 @ no__t-3 Verbunddienst und AD FS 1,1 \(installiert ist. Windows Server 2008 oder Windows Server 2008 R2 @ no__t-5 Verbunddienst. Eine der folgenden Interoperabilitätskombinationen werden unterstützt:  

-   Alle AD FS 1. *x* Verbunddienst können einen Anspruch senden, der von einem AD FS Verbunddienst in Windows Server 2012 verwendet werden kann. Weitere Informationen finden Sie unter [checkliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1. x @ no__t-0.  

-   Alle AD FS Verbunddienst in Windows Server 2012 können eine AD FS 1 senden. *x*\- kompatibler Anspruch, der von einem AD FS 1 verwendet werden kann. *x* -Verbunddienst. Weitere Informationen finden Sie unter [checkliste: Konfigurieren von AD FS, um Ansprüche an eine AD FS 1. x Verbunddienst @ no__t-0 zu senden.  

-   Alle AD FS Verbunddienst in Windows Server 2012 können eine AD FS 1 senden. *x*\- kompatibler Anspruch, der von einem oder mehreren Webservern genutzt werden kann, auf denen die AD FS 1 ausgeführt wird. *x* Claims @ no__t-3aware Web Agent. Weitere Informationen finden Sie unter [checkliste: Konfigurieren von AD FS für das Senden von Ansprüchen an einen AD FS 1. x Ansprüche unterstützenden Web-Agent @ no__t-0.  

> [!NOTE]  
> AD FS unterstützt oder interagiert nicht mit AD FS 1. *x* Windows NT Token – basierter Web-Agent.  

Eine AD FS 1. *x*\- kompatibler Anspruch ist ein Anspruch, der von einem AD FS Verbunddienst in Windows Server 2012 gesendet und von einem AD FS 1 interpretiert werden kann. *x* -Verbunddienst. Ein AD FS 1. *x* Verbunddienst die von einem Verbunddienst AD FS gesendeten Ansprüche nutzen kann, muss ein namens Bezeichner \(id @ no__t-2-Anspruchstyp gesendet werden.  

## <a name="understanding-the-name-id-claim-type"></a>Grundlegendes zum Namensbezeichner (ID)-Anspruchstyp  
Der Namensbezeichner (ID)-Anspruchstyp ist die Entsprechung des Identitätsanspruchstyps, der von AD FS 1.*x* verwendet wird. Dieser Typ muss verwendet werden, wenn die Interoperabilität mit AD FS 1.*x*gewünscht wird. Der Anspruchstyp Name ID aktiviert entweder eine AD FS 1. *x* Verbunddienst oder die AD FS 1. *x* Claims @ no__t-2aware Web Agent, um Ansprüche zu nutzen, die von AD FS in Windows Server 2012 gesendet werden, solange diese Ansprüche in einem der namens-ID-Formate in der folgenden Tabelle gesendet werden.  


|      Namensbezeichnerformat       |               Entsprechender URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* -E-Mailadresse | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* -E-Mail-UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        Allgemeiner Name        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           Gruppieren           |    http://schemas.xmlsoap.org/claims/Group     |

Es muss nur ein Anspruch im entsprechenden Namensbezeichnerformat gesendet werden. Wenn dieses Kriterium erfüllt ist, können viele andere Ansprüche auch gesendet werden, vorausgesetzt, dass sie den in der Tabelle beschriebenen Einschränkungen entsprechen.  

> [!NOTE]  
> Eine AD FS 1. *x* Verbunddienst kann nur eingehende Anspruchs Typen interpretieren, die mit dem Uniform Resource Identifier \(uri @ no__t-2 von http://schemas.xmlsoap.org/claims/ beginnen.  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
