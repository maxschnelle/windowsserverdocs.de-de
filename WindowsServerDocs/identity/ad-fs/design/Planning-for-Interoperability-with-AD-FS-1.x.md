---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: Planen der Interoperabilität mit AD FS 1.x
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9c5f49bd0ee0da9c3b92bad96f16ca310f82c239
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445330"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Planen der Interoperabilität mit AD FS 1.x

Active Directory-Verbunddienste \(AD FS\) -Verbundserver unter Windows Server® 2012 können mit beiden einen AD FS 1.0 zusammenarbeiten \(installiert mit Windows Server 2003 R2\) Verbunddienst und AD FS 1.1 \(installiert mit Windows Server 2008 oder Windows Server 2008 R2\) Verbunddienst. Eine der folgenden Interoperabilitätskombinationen werden unterstützt:  

-   Alle AD FS 1. *x* -Verbunddienste können einen Anspruch, der von einem AD FS-Verbunddienst in Windows Server 2012 genutzt werden kann senden. Weitere Informationen finden Sie unter [Prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).  

-   Alle AD FS-Verbunddienst in Windows Server 2012 kann es sich um einen AD FS 1. senden. *x*\--kompatibler Anspruch, der von einem AD FS 1. genutzt werden kann. *X* Verbunddienst. Weitere Informationen finden Sie unter [Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem Verbunddienst von AD FS 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).  

-   Alle AD FS-Verbunddienst in Windows Server 2012 kann es sich um einen AD FS 1. senden. *x*\--kompatibler Anspruch, die von einer oder mehreren Webservern, die mit dem AD FS-1. genutzt werden kann. *X* Ansprüche\-aware Web Agent. Weitere Informationen finden Sie unter [Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims-Aware Web-Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).  

> [!NOTE]  
> AD FS nicht unterstützt oder Interoperabilität mit dem AD FS 1. *x* Windows NT-Token-basierte Web-Agent.  

Ein AD FS 1. *x*\--kompatibler Anspruch ist, einen Anspruch, der von einem AD FS-Verbunddienst in Windows Server 2012 gesendet und von einem AD FS 1. verstanden werden kann. *X* Verbunddienst. Damit ein AD FS 1. *x* -Verbunddienst nutzen kann die Ansprüche, die von einem AD FS-Verbunddienst gesendet werden, einen Namensbezeichner \(ID\) Anspruch Typ gesendet werden muss.  

## <a name="understanding-the-name-id-claim-type"></a>Grundlegendes zum Namensbezeichner (ID)-Anspruchstyp  
Der Namensbezeichner (ID)-Anspruchstyp ist die Entsprechung des Identitätsanspruchstyps, der von AD FS 1.*x* verwendet wird. Dieser Typ muss verwendet werden, wenn die Interoperabilität mit AD FS 1.*x*gewünscht wird. Der Anspruch der namens-ID geben entweder einen AD FS 1. ermöglicht. *x* -Verbunddienst oder dem AD FS-1.. *X* Ansprüche\-bewusst Web-Agent nutzen Ansprüche, die AD FS unter Windows Server 2012 gesendet werden, solange diese Ansprüche in einem der Formate in der folgenden Tabelle namens-ID gesendet werden.  


|      Namensbezeichnerformat       |               Entsprechender URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* -E-Mailadresse | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* -E-Mail-UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        Allgemeiner Name        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           Gruppieren           |    http://schemas.xmlsoap.org/claims/Group     |

Es muss nur ein Anspruch im entsprechenden Namensbezeichnerformat gesendet werden. Wenn dieses Kriterium erfüllt ist, können viele andere Ansprüche auch gesendet werden, vorausgesetzt, dass sie den in der Tabelle beschriebenen Einschränkungen entsprechen.  

> [!NOTE]  
> Ein AD FS 1. *x* Verbunddienst kann nur eingehende Ansprüche interpretieren, die mit der Uniform Resource Identifier beginnen \(URI\) von http://schemas.xmlsoap.org/claims/.  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
