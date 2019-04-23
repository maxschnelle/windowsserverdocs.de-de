---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: Bereitstellen von Verbundservern
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32675aa7fb8c7b928bcf80a4d1072fe5eab7cd61
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864081"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims-Aware Web-Agent.

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-claims-aware-web-agent"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims\-aware Web Agent  
Diese Prüfliste enthält die Aufgaben, die erforderlich sind, für die Konfiguration Ihrer Active Directory Federation Services \(AD FS\) Verbunddienst in Windows Server 2012 zum Senden von Ansprüchen, die von einer Anwendung verstanden werden, die von gehostet wird, eine Webserver, die mit der AD FS 1. *x* Ansprüche\-aware Web Agent.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link zu einer Prozedur gelangen, geben zu diesem Thema zurück, nachdem Sie die Schritte in diesem Verfahren abgeschlossen haben, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Konfigurieren von AD FS zum Senden von Ansprüchen](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims\-aware Web Agent**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Planen Sie der Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über die ID der Anspruchstyp.|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenn Sie nicht bereits geschehen, verwenden Sie auf der rechten Seite den Link, um die Anspruchsanbieter-Vertrauensstellung zwischen AD FS-Verbunddienst in Windows Server 2012 und dem AD FS-1. zuerst zu erstellen. *x* Verbunddienst.|[Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem Verbunddienst von AD FS 1.x](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Vor dem erreichen Sie Interoperabilität mit einer Anwendung, die von der AD FS 1. gehostet wird. *x* Ansprüche\-bewusst-Web-Agent, müssen Sie zunächst erstellen eine Vertrauensstellung der vertrauenden Seite in AD FS-Verbunddienst in Windows Server 2012 auf dem AD FS 1. *X* Ansprüche\-aware Web Agent. **Hinweis**: Erstellen diese Vertrauensstellung in der AD FS-Verbunddienst entspricht dem Hinzufügen eines neuen **Anwendung** für den AD FS 1.x Federation Service \( **Verbunddienst\\Vertrauensrichtlinie\\ Meine Organisation\\Anwendung**\). Diese Vertrauensstellung der vertrauenden Seite ist erforderlich, da AD FS kein entsprechendes **Anwendung** Knoten in eine eigene Snap\-in. Sie benötigen jedoch weiterhin einen sicheren Kanal für die Anwendung.<br /><br />Beim Einrichten der Vertrauensstellung mit dem Verfahren in den Link, um das Recht, müssen Sie die folgenden der vertrauenden Seite Party Trust Assistenten zum Hinzufügen, um diese Vertrauensstellung einzurichten, die Interoperabilität mit einem AD FS 1. tun. *x* Ansprüche\-aware Web Agent:<br /><br />1.  Auf der **Auswählen einer Datenquelle** Seite **eingeben von Daten über die abhängige Partei Vertrauensstellung manuell**.<br />2.  Auf der **Profil auswählen** Seite **AD FS 1.0 und 1.1-Profil**.<br />3.  Auf der **-URL konfigurieren** Seite **WS\-URL des passiven Verbunds**, Typ der **Anwendungs-URL** gemäß der in der AD FS 1. *X* Verbunddienst des Partners.<br />4.  Auf der **Konfigurieren von Bezeichnern** Seite **Trust-Bezeichner der vertrauenden Seite**, Typ der **Anwendungs-URL** gemäß der in der AD FS 1. *X* Ansprüche\-aware Web Agent|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[eine verlassen Partei vertrauen manuell erstellen](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenden Sie sich an den Webserver mit dem AD FS-1. der Administrator. *x* Ansprüche\-bewusst Web-Agent und dieser Administrator die Datei "Web.config" zu bearbeiten, die mit den Ansprüchen zugeordnet ist\-unterstützende Anwendung \(unter der Standardwebsite in Internetinformationsdienste Dienste \(IIS\) \) um der Web-Agent auf den AD FS-Verbunddienst zu verweisen.<br /><br />Ersetzen Sie z. B. *Myresourcefederationserver* im Tag `<fs> https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>` der Datei "Web.config" mit einem gültigen AD FS-Server.<br /><br />Dies ist erforderlich, für die Anwendung und die AD FS 1.x Claims\-unterstützender Web-Agent in der Lage, die Ansprüche zu nutzen, die an ihn, aus der AD FS-Verbunddienst in Windows Server 2012 gesendet werden.|N\/A|  
|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Auf die vertrauenden Seite Vertrauensstellung, die Sie zuvor erstellt haben, müssen Sie Anspruchsregeln zu erstellen, werden die eingehenden Ansprüche, die in einem Attributspeicher extrahiert wurden und pass-through-, filtern oder transformieren sie in einem namens-ID-Anspruchstyp, der verstanden und von genutzt werden kann wird, die AD FS 1. *x* Ansprüche\-aware Web Agent. **Hinweis**: Bevor Sie mit dieser Regel erstellen, stellen sicher, dass der Satz von Ansprüchen Regel Sie mit dieser Regel erstellen eine Regel, die es vorangeht, die zuerst ein Lightweight Directory Access Protocol extrahiert \(LDAP\) Attribut Anspruch in einem Attributspeicher. Dieser Anspruch wird als Eingabe für die Regel verwendet werden, die Sie erstellen, um einen AD FS 1. zu senden. *x*\--kompatibler Anspruch. Weitere Informationen zum Erstellen einer Regel zum Extrahieren von einem LDAP-Attribut finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md).|![Konfigurieren von AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen Sie eine Regel zum Senden von AD FS 1.x-kompatibler Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

