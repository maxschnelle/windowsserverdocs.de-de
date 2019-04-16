---
ms.assetid: ad3f0480-99f7-428a-ab33-6d165a440840
title: Szenario Get Einsicht in Ihre Daten mittels Klassifizierung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2e5248b5fd5e20b7436de9f796367c018d8ef16e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-get-insight-into-your-data-by-using-classification"></a>Szenario: Erhalten von Einblicken in Ihre Daten mittels Klassifizierung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Abhängigkeit von Daten- und Speicherressourcen weiterhin für die meisten Organisationen zunehmen. IT-Administratoren der wachsende Herausforderung konfrontiert größere und komplexere Speicherinfrastrukturen konfrontiert, während Sie gleichzeitig mit dem verantwortlich, stellen Sie sicher sind,--Gesamtbetriebskosten vernünftiges Maß verwaltet wird. Verwalten von Speicherressourcen ist nicht mehr nur um das Volumen oder die Verfügbarkeit von Daten. Es ist auch zum Erzwingen von Unternehmensrichtlinien und wissen, wie Speicherverbrauch, um eine effiziente Nutzung und Kompatibilität zur Risikominderung aktivieren. Die Dateiklassifizierungsinfrastruktur bietet Einsicht in Ihre Daten, indem klassifizierungsvorgänge automatisiert werden, sodass Sie Ihre Daten effektiver verwalten können. Folgende Klassifizierungsmethoden stehen zur Verfügung, mit der Dateiklassifizierungsinfrastruktur: manuell, programmgesteuert und automatisch. Der Schwerpunkt dieses Themas liegt auf der automatischen Dateiklassifizierungsmethode.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Die Dateiklassifizierungsinfrastruktur verwendet Klassifizierungsregeln zum automatischen prüfen und Klassifizieren von Dateien entsprechend den Inhalt der Datei. Klassifizierungseigenschaften werden zentral in Active Directory definiert, sodass diese Definitionen dateiserverübergreifend in der Organisation freigegeben werden können. Sie können Klassifizierungsregeln erstellen, die Dateien für eine standardmäßige Zeichenfolge hin oder eine Zeichenfolge, die mit einem Muster (regulärer Ausdruck) übereinstimmt. Wenn ein konfigurierter Klassifizierungsparameter in einer Datei gefunden wird, wird diese Datei klassifiziert, wie in der Klassifizierungsregel konfiguriert. Einige Beispiele für Klassifizierungsregeln:  
  
-   Alle Dateien, die die Zeichenfolge "Contoso Confidential" enthält als mit hoher unternehmensauswirkung klassifiziert  
  
-   Klassifizierung einer beliebigen Datei, die mindestens 10 Sozialversicherungsnummern mit persönlich identifizierbaren Informationen enthält.  
  
Wenn eine Datei klassifiziert wird, können Sie eine Datei Verwaltungsaufgabe auszuführende Aktion auf alle Dateien, die eine bestimmte Art und Weise klassifiziert. Die Aktionen in einer Dateiverwaltungsaufgabe zählen das Schützen der Rechte, die der Datei, das Ablaufen der Datei und Ausführen einer benutzerdefinierten Aktion (z.B. das Bereitstellen von Informationen an einen Webdienst) zugeordnet.  
  
Finden Sie Informationen zum Konfigurieren der automatischen Dateiklassifizierung in Planung [Planen der automatischen Dateiklassifizierung](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955).  
  
Finden Sie schrittweise Anleitung zum automatischen Klassifizieren von Dateien in [Bereitstellen der automatischen Dateiklassifizierung & 40; Schrittezur Veranschaulichung & 41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Dieses Szenario ist Teil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_APP"></a>In der Praxis  
Die Dateiklassifizierungsinfrastruktur in Windows Server2012 trägt zur dynamischen Zugriffssteuerung bei, indem unternehmensdatenbesitzer Daten einfach klassifizieren und bezeichnen können. Die in der zentralen Zugriffsrichtlinie gespeicherten Klassifizierungsinformationen können Sie zum Definieren von Zugriffsrichtlinien für Datenklassen, die für das Unternehmen entscheidend sind.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgende Tabelle werden die Features, die in diesem Szenario sind aufgeführt und beschrieben, wie sie unterstützen.  
  
|Funktion|Wie sie dieses Szenario unterstützt|  
|-----------|---------------------------------|  
|[File Server Resource Manager (Übersicht)](https://technet.microsoft.com/library/hh831701.aspx)|Die Dateiklassifizierungsinfrastruktur ist ein Feature, das in File Server Resource Manager enthalten ist.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|File Server Resource Manager ist ein Feature, das mit der Serverrolle Dateidienste enthalten ist.|  
  


