---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: -Checkliste – Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fe99487d3a770547af36f69722b442d0e2cbb8b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828291"
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>Prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-adfs1x"></a>Prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x  
Diese Prüfliste enthält die Aufgaben, die erforderlich sind, für die Konfiguration Ihrer Active Directory Federation Services \(AD FS\) Verbunddienst in Windows Server 2012 auf Ansprüche zu nutzen, die von einem AD FS 1. gesendet werden. *X* Verbunddienst.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link zu einer Prozedur gelangen, geben zu diesem Thema zurück, nachdem Sie die Schritte in diesem Verfahren abgeschlossen haben, damit Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Nutzen Sie die Ansprüche von AD FS](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Nutzen Sie die Ansprüche von AD FS](media/icon_checkboxo.gif)|Planen Sie der Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über die ID der Anspruchstyp.|![Nutzen Sie die Ansprüche von AD FS](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Nutzen Sie die Ansprüche von AD FS](media/icon_checkboxo.gif)|Bevor Sie mit einer früheren Version von AD FS interagieren können, müssen Sie zuerst eine Anspruchsanbieter-Vertrauensstellung in der AD FS-Verbunddienst erstellen. **Hinweis**: Sie können keine Vertrauensstellung mit einem AD FS 1. erstellen. *x* Federation Service mithilfe von Verbundmetadaten.<br /><br />Wenn Sie die Vertrauensstellung mit dem Verfahren in den Link auf der rechten Seite einrichten, müssen Sie die folgenden Ansprüche Anbieter Vertrauensstellung Assistenten zum Hinzufügen, um diese Vertrauensstellung einzurichten, die Interoperabilität mit einem AD FS 1. tun. *x* Verbunddienst:<br /><br />1.  Auf der **Auswählen einer Datenquelle** Seite **eingeben von Daten über die abhängige Partei Vertrauensstellung manuell**.<br />2.  Auf der **Profil auswählen** Seite **AD FS 1.0 und 1.1-Profil**.<br />3.  Auf der **-URL konfigurieren** Seite **WS\-URL des passiven Verbunds**, Typ der **Verbunddienst-Endpunkt-URL** gemäß der in der AD FS 1. *X* Verbunddienst des Partners.<br />4.  Auf der **Konfigurieren von Bezeichnern** Seite **Anspruchsanbieter-Vertrauensstellung ID**, Typ der **Verbunddienst-URI** gemäß der in der AD FS 1. *X* Verbunddienst des Partners.|![Nutzen Sie die Ansprüche von AD FS](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen Sie eine Ansprüche Anbieter vertrauen manuell](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)|  
|![Nutzen Sie die Ansprüche von AD FS](media/icon_checkboxo.gif)|Für die Anspruchsanbieter-Vertrauensstellung, die Sie zuvor erstellt haben, müssen Sie eine Anspruchsregel erstellen, dauert die Ansprüche, die eingehende von der AD FS 1.x Federation Service durchlaufen, Filtern und deren Umwandlung in eine namens-ID-Anspruchstyp.<br /><br />Bei der namens-ID-Anspruchstyp, übergeben wurde, gefiltert oder transformiert werden, können als Eingabe für eine andere Regel bzw. Regeln verwendet werden, damit sie verstanden und von der AD FS-Verbunddienst in Windows Server 2012 genutzt werden kann.|![Nutzen Sie die Ansprüche von AD FS](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[erstellen Sie eine Regel zum Senden von AD FS 1.x-kompatibler Anspruch](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![Nutzen Sie die Ansprüche von AD FS](media/icon_checkboxo.gif)|Wenden Sie sich an den Administrator des AD FS 1. *x* Verbunddienst und lassen Sie den Administrator des AD FS 1. *X* Verbunddienst Einrichten einer neuen Ressource Partner Vertrauensstellung. Geben Sie außerdem mit dem Verbund-Dienst-URI der Administrator \(in den Eigenschaften des Verbunddiensts\), die Verbunddienst-Endpunkt-URL und eine exportierte Token\-Zertifikatdatei signieren \(mit nur öffentlicher Schlüssel\). Der Administrator benötigen Folgendes, um die Vertrauensstellung einzurichten.|N\/A|  
  

