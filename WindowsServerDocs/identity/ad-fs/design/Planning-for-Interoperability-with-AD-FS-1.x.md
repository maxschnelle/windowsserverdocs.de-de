---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: "Planen der Interoperabilität mit AD FS 1.x"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f287261ce6cb56e40385ef4de922045153819a23
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Planen der Interoperabilität mit AD FS 1.x

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Active Directory-Verbunddienste \(AD FS\) Verbundserver unter Windows Server® 2012 können die Interoperabilität mit beiden AD FS 1.0 \ (installiert mit Windows Server2003 R2\) Verbunddienst und AD FS 1.1 \ (installiert mit Windows Server2008 oder Windows Server2008 R2\) Verbunddienst. Eine der folgenden Interoperabilitätskombinationen werden unterstützt:  
  
-   Alle AD FS 1. *x* -Verbunddienste können einen Anspruch, der von einem AD FS-Verbunddienst in Windows Server2012 genutzt werden kann, senden. Weitere Informationen finden Sie unter [Prüfliste: Konfigurieren von AD FS für Ansprüche, die Nutzung von AD FS 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).  
  
-   Alle AD FS-Verbunddienst in Windows Server2012 können einen AD FS 1. senden. *x*\-compatible Anspruch, der von einem AD FS 1. genutzt werden kann. *x* Verbunddienst. Weitere Informationen finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).  
  
-   Alle AD FS-Verbunddienst in Windows Server2012 können einen AD FS 1. senden. *x*\-compatible Anspruch, der von einem oder mehreren Web-Servern, die mit AD FS 1. genutzt werden kann. *x* Claims\-aware Web-Agent. Weitere Informationen finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).  
  
> [!NOTE]  
> AD FS nicht unterstützt oder für die Interoperabilität mit AD FS 1. *x* Windows NT-Token-basierte Web-Agent.  
  
Ein AD FS 1. *x*\-compatible Anspruch ist eine Anforderung, die von einem AD FS-Verbunddienst in Windows Server2012 gesendet und von einem AD FS 1. verarbeitet werden kann. *x* Verbunddienst. Damit ein AD FS 1. *x* Verbunddienst, der eine AD FS-Verbunddienst gesendeten Ansprüche nutzen kann, muss ein Namensbezeichner \(ID\) Anspruchstyp gesendet werden.  
  
## <a name="understanding-the-name-id-claim-type"></a>Grundlegendes zu den Anspruchstyp Name-ID  
Der Name-ID--Anspruchstyp ist die Entsprechung des Anspruchs Identität geben, von AD FS 1. *x* uses. Es muss verwendet werden, wenn für die Interoperabilität mit AD FS 1. werden sollen. *x*. Der Anspruch geben entweder ein AD FS 1. ermöglicht. *x* Verbunddienst oder die AD FS 1. *x* Claims\-aware Web-Agent Ansprüche, die AD FS unter Windows Server2012 sendet, nutzen, solange diese Ansprüche in eines der Formate Name-ID in der folgenden Tabelle gesendet werden.  
  
|Namensbezeichnerformat|Entsprechende URI|  
|------------------|---------------------|  
|AD FS 1. *x* E-Mail-Adresse|http://schemas.xmlsoap.org/claims/EmailAddress|  
|AD FS 1. *x* E-Mail-UPN|http://schemas.xmlsoap.org/claims/UPN|  
|Allgemeiner Name|http://schemas.xmlsoap.org/claims/CommonName|  
|Gruppe|http://schemas.xmlsoap.org/claims/Group|  
  
Es muss nur ein Anspruch im entsprechenden namensbezeichnerformat gesendet werden. Wenn dieses Kriterium erfüllt ist, können viele andere Ansprüche auch gesendet werden, vorausgesetzt, dass sie die in der Tabelle beschriebenen Einschränkungen entsprechen.  
  
> [!NOTE]  
> Ein AD FS 1. *x* Verbunddienst kann nur eingehende Ansprüche interpretieren, die mit den Uniform Resource Identifier \(URI\) von http://schemas.xmlsoap.org/claims/ beginnen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
