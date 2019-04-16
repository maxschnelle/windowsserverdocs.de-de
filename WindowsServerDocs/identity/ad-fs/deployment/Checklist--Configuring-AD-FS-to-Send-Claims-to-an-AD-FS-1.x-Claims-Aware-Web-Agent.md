---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: Bereitstellen von Verbundservern
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32675aa7fb8c7b928bcf80a4d1072fe5eab7cd61
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>Prüfliste: Konfigurieren von AD FS für die Ansprüche an einen AD FS 1.x Claims-Aware Web Agent gesendet werden

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims\-aware Web agent  
Diese Prüfliste enthält die Aufgaben zum Konfigurieren der Active Directory-Verbunddienste \(AD FS\) Verbunddienst in Windows Server 2012 Ansprüche senden, die von einer Anwendung verstanden werden, die von einem Webserver mit AD FS 1. gehostet wird. *x* Claims\-aware Web-Agent.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der Reihenfolge. Wenn ein Link gelangen Sie zu einem Verfahren in diesem Thema nach Abschluss der Schritte in diesem Verfahren, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Konfigurieren von AD FS zum Senden von Ansprüchen](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims\-aware Web Agent**  
  
||Aufgabe|Referenz zu|  
|-|--------|-------------|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Planen Sie für die Interoperabilität zwischen AD FS unter Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie, dass weitere Informationen zu den Name-ID Typ geltend machen.|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenn Sie nicht bereits geschehen, verwenden Sie den Link auf der rechten Seite zuerst eine Vertrauensstellung der vertrauenden Seite zwischen dem AD FS-Verbunddienst in Windows Server 2012 und die AD FS 1. erstellen. *x* Verbunddienst.|[Prüfliste: Konfigurieren von AD FS für die Ansprüche an einen AD FS 1.x-Verbunddienst gesendet werden](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Vor dem erreichen Sie Interoperabilität mit einer Anwendung, die von der AD FS 1. gehostet wird. *x* Claims\-aware Web-Agent, müssen Sie zuerst erstellen eine Vertrauensstellung der vertrauenden Seite in der AD FS-Verbunddienst in Windows Server 2012 zu AD FS 1. *X* Claims\-aware Web-Agent. **Hinweis:** Erstellen dieser Vertrauensstellung in der AD FS-Verbunddienst entspricht dem Hinzufügen eines neuen **Anwendung** an der AD FS 1.x-Verbunddienst \ (**Federation Service\\Trust Policy\\My Organization\\Application**\). Diese Vertrauensstellung der vertrauenden Seite ist erforderlich, da AD FS keine entsprechende **Anwendung** Knoten im eigenen Snap-in. Sie müssen jedoch noch einen sicheren Kanal für die Anwendung verfügen.<br /><br />Wenn Sie die Vertrauensstellung mithilfe des Verfahrens in der Verknüpfung mit der rechten Seite einrichten, müssen Sie die folgenden Vertrauensstellungen der vertrauenden Seite Party Vertrauensstellung Assistenten zum Hinzufügen, um diese Vertrauensstellung einzurichten, für die Interoperabilität mit einem AD FS 1. tun. *x* Claims\-aware Web-Agent:<br /><br />1. auf die **Auswählen einer Datenquelle** Seite **eingeben von Daten über die Vertrauensstellungen der vertrauenden Seite Partei Vertrauensstellung manuell**.<br />2. auf die **Profil auswählen** Seite **AD FS 1.0- und 1.1-Profil**.<br />3. auf die **URL konfigurieren** Seite unter **URL des passiven WS-Verbund:**, geben die **Anwendungs-URL** gemäß Definition in der AD FS 1. *x* Verbunddienst des Partners.<br />4. auf die **Konfigurieren von Bezeichnern** Seite unter **Bezeichner Vertrauensstellung der vertrauenden Seite**, geben die **Anwendungs-URL** gemäß Definition in der AD FS 1. *x* Claims\-aware Web Agent|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen Sie eine der vertrauenden Seite Party vertrauen manuell](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des Webservers mit der AD FS 1. *x* Claims\-aware Web-Agent und dem Administrator die Datei "Web.config" zu bearbeiten, die mit der Claims\-fähige Anwendung verknüpft ist, haben \ (unter der Standardwebsite in IIS \(IIS\)\) den Web-Agent auf dem AD FS-Verbunddienst zeigen.<br /><br />Ersetzen Sie z. B. *Myresourcefederationserver* im Tag `<fs>https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>` der Datei "Web.config" mit einem gültigen AD FS Federation Server-Namen.<br /><br />Dies ist erforderlich für die Anwendung und die AD FS 1.x Claims\-aware Web Agent können die Ansprüche zu nutzen, die von der AD FS-Verbunddienst in Windows Server 2012 an sie gesendet werden.|N\/A|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Auf der vertrauenden Seite Vertrauensstellung, die Sie zuvor erstellt haben, müssen Sie erstellen Anspruch Regeln, die eingehenden Ansprüche, die aus einem Attributspeicher extrahiert wurden aufnehmen und pass-through, filtern oder transformieren sie in einer-ID werden Anspruchstyp, die verstehen und genutzt werden, von der AD FS 1. *x* Claims\-aware Web-Agent. **Hinweis:** , bevor Sie diese Regel erstellen, stellen Sie sicher, dass der anspruchsregelsatz, in denen Sie diese Regel erstellen, eine Regel, die vor dem stammt, der einen Lightweight Directory Access Protocol \(LDAP\) Attribut Anspruch zunächst aus einem Attributspeicher extrahiert. Dies wird als Eingabe für die Regel verwendet werden, die Sie zum Senden von einem AD FS 1. erstellen. *x*\-compatible Anspruch. Weitere Informationen zum Erstellen einer Regel zum Extrahieren von einem LDAP-Attribut finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md).|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen eine Regel zum Senden von einem AD FS 1.x-kompatiblen Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

