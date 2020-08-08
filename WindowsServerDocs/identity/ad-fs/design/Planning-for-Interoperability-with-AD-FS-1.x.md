---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: Planen der Interoperabilität mit AD FS 1.x
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 94313fc185a4f326ad00a95e4c594fd3e696f61a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967607"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Planen der Interoperabilität mit AD FS 1.x

Active Directory-Verbunddienste (AD FS) \( AD FS \) Verbund Servern, auf denen Windows Server 2012 ausgeführt wird, &reg; können sowohl mit einem AD FS 1,0, \( installiert mit Windows Server 2003 R2 \) Verbunddienst, als auch mit einem AD FS 1,1 zusammenarbeiten, das \( mit Windows Server 2008 oder Windows Server 2008 R2 Verbunddienst installiert ist \) . Eine der folgenden Interoperabilitätskombinationen werden unterstützt:

-   Alle AD FS 1. *x* Verbunddienst können einen Anspruch senden, der von einem AD FS Verbunddienst in Windows Server 2012 verwendet werden kann. Weitere Informationen finden Sie unter Prüfliste [: Konfigurieren von AD FS für die Nutzung von Ansprüchen AD FS 1. x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).

-   Alle AD FS Verbunddienst in Windows Server 2012 können eine AD FS 1 senden. *x* \- kompatibler Anspruch, der von einem AD FS 1 verwendet werden kann. *x* -Verbunddienst. Weitere Informationen finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).

-   Alle AD FS Verbunddienst in Windows Server 2012 können eine AD FS 1 senden. *x* \- kompatibler Anspruch, der von einem oder mehreren Webservern genutzt werden kann, auf denen die AD FS 1 ausgeführt wird. *x* -Anspruchs fähiger \- Web-Agent. Weitere Informationen finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).

> [!NOTE]
> AD FS unterstützt oder interagiert nicht mit AD FS 1. *x* Windows NT Token – basierter Web-Agent.

Eine AD FS 1. *x* \- der kompatible Anspruch ist ein Anspruch, der von einem AD FS Verbunddienst in Windows Server 2012 gesendet und von einem AD FS 1 interpretiert werden kann. *x* -Verbunddienst. Ein AD FS 1. *x* Verbunddienst die Ansprüche nutzen können, die von einem AD FS gesendet Verbunddienst, muss ein Bezeichnertyp für die namensbezeichnerid \( \) gesendet werden.

## <a name="understanding-the-name-id-claim-type"></a>Grundlegendes zum Namensbezeichner (ID)-Anspruchstyp
Der Namensbezeichner (ID)-Anspruchstyp ist die Entsprechung des Identitätsanspruchstyps, der von AD FS 1.*x* verwendet wird. Dieser Typ muss verwendet werden, wenn die Interoperabilität mit AD FS 1.*x*gewünscht wird. Der Anspruchstyp Name ID aktiviert entweder eine AD FS 1. *x* Verbunddienst oder die AD FS 1. der in *Anspruch gehende* \- Web-Agent für die Verarbeitung von Ansprüchen, die von AD FS in Windows Server 2012-Sendungen gesendet werden, solange diese Ansprüche in einem der namens-ID-Formate in der folgenden Tabelle gesendet werden.


|      Namensbezeichnerformat       |               Entsprechender URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* -E-Mailadresse | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* -E-Mail-UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        Allgemeiner Name        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           Group           |    http://schemas.xmlsoap.org/claims/Group     |

Es muss nur ein Anspruch im entsprechenden Namensbezeichnerformat gesendet werden. Wenn dieses Kriterium erfüllt ist, können viele andere Ansprüche auch gesendet werden, vorausgesetzt, dass sie den in der Tabelle beschriebenen Einschränkungen entsprechen.

> [!NOTE]
> Eine AD FS 1. *x* Verbunddienst kann nur eingehende Anspruchs Typen interpretieren, die mit dem Uniform Resource Identifier- \( URI \) von beginnen http://schemas.xmlsoap.org/claims/ .

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
