---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: "Checkliste – Konfigurieren von AD FS zur Nutzung der Ansprüche von AD FS 1.x"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fe99487d3a770547af36f69722b442d0e2cbb8b1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>Prüfliste: Konfigurieren von AD FS zur Nutzung der Ansprüche von AD FS 1.x

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-ad-fs-1x"></a>Prüfliste: Konfigurieren von AD FS zur Nutzung der Ansprüche von AD FS 1.x  
Diese Prüfliste enthält die Aufgaben zum Konfigurieren der Active Directory-Verbunddienste \(AD FS\) Verbunddienst in Windows Server 2012 Ansprüche zu nutzen, die von einem AD FS 1 gesendet werden. *x* Verbunddienst.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der Reihenfolge. Wenn ein Link gelangen Sie zu einem Verfahren in diesem Thema nach Abschluss der Schritte in diesem Verfahren, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Nutzen Sie Ansprüche von AD FS](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Konfigurieren von AD FS zur Nutzung der Ansprüche von AD FS 1.x**  
  
||Aufgabe|Referenz zu|  
|-|--------|-------------|  
|![Nutzen Sie Ansprüche von AD FS](media/icon_checkboxo.gif)|Planen für die Interoperabilität zwischen AD FS unter Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie, dass weitere Informationen zu den Name-ID Typ geltend machen.|![Nutzen Sie Ansprüche von AD FS](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Nutzen Sie Ansprüche von AD FS](media/icon_checkboxo.gif)|Bevor Sie mit einer früheren Version von AD FS zusammenarbeiten können, müssen Sie zunächst eine Anspruchsanbieter-Vertrauensstellung in der AD FS-Verbunddienst erstellen. **Hinweis:** Sie eine Vertrauensstellung mit einem AD FS 1. können nicht erstellt. *x* Verbunddienst mithilfe von Verbundmetadaten.<br /><br />Wenn Sie die Vertrauensstellung mithilfe des Verfahrens in der Verknüpfung mit der rechten Seite einrichten, müssen Sie die folgenden Ansprüche Anbieter Vertrauensstellung Assistenten zum Hinzufügen, um diese Vertrauensstellung einzurichten, für die Interoperabilität mit einem AD FS 1. tun. *x* Verbunddienst:<br /><br />1. auf die **Auswählen einer Datenquelle** Seite **eingeben von Daten über die Vertrauensstellungen der vertrauenden Seite Partei Vertrauensstellung manuell**.<br />2. auf die **Profil auswählen** Seite **AD FS 1.0- und 1.1-Profil**.<br />3. auf die **URL konfigurieren** Seite unter **URL des passiven WS-Verbund:**, geben die **Endpunkt-URLs des Verbunddiensts** gemäß Definition in der AD FS 1. *x* Verbunddienst des Partners.<br />4. auf die **Konfigurieren von Bezeichnern** Seite unter **Anspruchsanbieter-Vertrauensstellung ID**, geben die **Verbunddienst-URI** gemäß Definition in der AD FS 1. *x* Verbunddienst des Partners.|![Nutzen Sie Ansprüche von AD FS](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Erstellen einer Ansprüche Anbieter vertrauen manuell](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)|  
|![Nutzen Sie Ansprüche von AD FS](media/icon_checkboxo.gif)|Auf der Anspruchsanbieter-Vertrauensstellung, die Sie zuvor erstellt haben, müssen Sie eine Anspruchsregel erstellen, dauert die Ansprüche, die von der AD FS 1.x-Verbunddienst und Pass-through, filtern oder transformieren sie in ein Anspruch ID.<br /><br />Wenn die Name-ID Anspruchstyp gefiltert oder transformiert über übergeben wurde, können als Eingabe für eine andere Regel bzw. Regeln verwendet werden, damit sie verstanden und von der AD FS-Verbunddienst in Windows Server 2012 genutzt werden.|![Nutzen Sie Ansprüche von AD FS](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen eine Regel zum Senden von einem AD FS 1.x-kompatiblen Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![Nutzen Sie Ansprüche von AD FS](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des AD FS 1. *x* Verbunddiensts und den Administrator des AD FS 1. *x* Verbunddienst von eine neue Ressource Partner Vertrauensstellung einrichten. Außerdem bieten dem Administrator mit dem Verbunddienst-URI \ (in der Verbunddienst Properties\), die Endpunkt-URLs des Verbunddiensts und eine exportierte Token\-Signatur Zertifikatdatei \ (mit dem öffentlichen Schlüssel Only\). Der Administrator benötigen diese Elemente, um die Vertrauensstellung einrichten.|N\/A|  
  

