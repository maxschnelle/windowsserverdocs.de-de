---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: Bereitstellen von Verbundservern
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 689bd33bc95c2b142dfbe6d0448a604b2971979e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359977"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen an einen Ansprüche unterstützenden AD FS 1. x-Web-Agent

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-claims-aware-web-agent"></a>Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen an einen AD FS 1. x-Claims @ no__t-0aware Web-Agent  
Diese Prüfliste enthält die Aufgaben, die zum Konfigurieren Ihrer Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 Verbunddienst in Windows Server 2012 erforderlich sind, um Ansprüche zu senden, die von einer Anwendung, die von einem Webserver gehostet wird, verstanden werden können. Ausführen des AD FS 1. *x* Claims @ no__t-3aware Web Agent.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn Sie über einen Verweis Link zu einer Prozedur gelangen, kehren Sie zu diesem Thema zurück, nachdem Sie die Schritte in diesem Verfahren ausgeführt haben, damit Sie mit den verbleibenden Aufgaben in dieser Prüfliste fortfahren können.  
  
![configure AD FS to Send Claims @ no__t-1checkprüfliste: Konfigurieren von AD FS für das Senden von Ansprüchen an eine AD FS 1. x-Ansprüche @ no__t-0aware Web-Agent @ no__t-1  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Planen Sie die Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über den Anspruchstyp "Name ID".|![configure AD FS, um die Anspruchs](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planung für die Interoperabilität mit AD FS 1. x](https://technet.microsoft.com/library/ff678040.aspx) zu senden.|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenn Sie dies noch nicht getan haben, verwenden Sie den Link auf der rechten Seite, um zuerst eine Vertrauensstellung der vertrauenden Seite zwischen dem AD FS Verbunddienst in Windows Server 2012 und dem AD FS 1 zu erstellen. *x* -Verbunddienst.|[Prüfliste: Konfigurieren von AD FS, sodass Ansprüche an einen AD FS 1.x-Verbunddienst gesendet werden](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Bevor Sie eine Interoperation mit einer Anwendung erreichen können, die vom AD FS 1 gehostet wird. *x* Claims @ no__t-1aware Web-Agent. Sie müssen zunächst eine Vertrauensstellung der vertrauenden Seite in der AD FS Verbunddienst in Windows Server 2012 mit dem AD FS 1 erstellen. *x* Claims @ no__t-1aware Web-Agent. **Hinweis**: Das Erstellen dieser Vertrauensstellung in der AD FS Verbunddienst entspricht dem Hinzufügen einer neuen **Anwendung** zum AD FS 1. x Verbunddienst \(**Verbunddienst @ no__t-3trust Policy @ no__t-4MY Organization @ no__t-5application**\). Diese Vertrauensstellung der vertrauenden Seite ist erforderlich, da AD FS nicht über einen entsprechenden **Anwendungs** Knoten im eigenen Snap @ no__t-1In verfügt. Es muss jedoch immer noch ein sicherer Kanal für die Anwendung vorhanden sein.<br /><br />Wenn Sie die Vertrauensstellung mithilfe des Verfahrens im Link auf der rechten Seite einrichten, müssen Sie im Assistenten zum Hinzufügen von Vertrauens Stellungen der vertrauenden Seite die folgenden Schritte ausführen, um diese Vertrauensstellung für die Interoperabilität mit einem AD FS 1 einzurichten. *x* Claims @ no__t-1aware Web-Agent:<br /><br />1.  Wählen Sie auf der Seite **Datenquelle auswählen** die Option **Daten über die Vertrauensstellung der vertrauenden Seite manuell eingeben**aus.<br />2.  Wählen Sie auf der Seite **Profil auswählen** die Option **AD FS 1,0-und 1,1-Profil**aus.<br />3.  Geben Sie auf der Seite **URL konfigurieren** unter **WS @ no__t-2federation passive URL**die **Anwendungs-URL** ein, wie in der AD FS 1 definiert. *x* Verbunddienst des Partners.<br />4.  Geben Sie auf der Seite **Bezeichner** **Konfigurieren** unter Vertrauensstellungs-ID die **Anwendungs-URL** ein, wie Sie in der AD FS 1 definiert ist. *x* Claims @ no__t-4aware Web-Agent|![configure AD FS to Send Claims (](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Manuelles Erstellen einer Vertrauensstellung der vertrauenden Seite](../../ad-fs/operations/Create-a-Relying-Party-Trust.md) )|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des Webservers, auf dem die AD FS 1 ausgeführt wird. *x* Claims @ no__t-1aware Web Agent und gibt an, dass der Administrator die Datei "Web. config" Bearbeiten muss, die der Anwendung "Claims @ no__t-2aware" zugeordnet ist. \( unter der Standard Website in Internetinformationsdienste \(iis @ no__t-5 @ no__t-6 auf verweisen Sie den Web-Agent auf den AD FS Verbunddienst.<br /><br />Ersetzen Sie z. b. *myresourcefederationserver* im Tag `<fs> https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>` der Datei "Web. config" durch einen gültigen AD FS Verbund Servernamen.<br /><br />Dies ist erforderlich, damit die Anwendung und der AD FS 1. x-Claims @ no__t-0aware Web-Agent die Ansprüche nutzen können, die von der AD FS Verbunddienst in Windows Server 2012 gesendet werden.|N\/A|  
|![Konfigurieren AD FS zum Senden von Ansprüchen](media/icon_checkboxo.gif)|Auf der Vertrauensstellung der vertrauenden Seite, die Sie zuvor erstellt haben, müssen Sie Anspruchs Regeln erstellen, die eingehende Ansprüche akzeptieren, die aus einem Attribut Speicher extrahiert wurden, und Sie in einen namens-ID-Anspruchstyp übergeben, Filtern oder transformieren, der vom AD FS 1. *x* Claims @ no__t-1aware Web-Agent. **Hinweis**: Stellen Sie vor dem Erstellen dieser Regel sicher, dass der Anspruchs Regel Satz, für den Sie diese Regel erstellen, eine Regel enthält, die zuerst einen Lightweight Directory Access Protocol-\(ldap @ no__t-1-Attribut Anspruch aus einem Attribut Speicher extrahiert. Dieser Anspruch wird als Eingabe für die Regel verwendet, die Sie erstellen, um eine AD FS 1 zu senden. *x*\- kompatibler Anspruch. Weitere Informationen zum Erstellen einer Regel zum Extrahieren eines LDAP-Attributs finden Sie unter [Erstellen einer Regel zum Senden von LDAP-Attributen als Ansprüche](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md).|![configure AD FS zum Senden von Ansprüchen](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Erstellen einer Regel zum Senden eines AD FS 1. x-kompatiblen Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

