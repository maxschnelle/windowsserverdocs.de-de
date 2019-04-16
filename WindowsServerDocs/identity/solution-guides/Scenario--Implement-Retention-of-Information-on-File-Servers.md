---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: Szenario implementieren Aufbewahrung von Informationen auf Dateiservern
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59fd7f0a0a4d9ed8f5cec57b17be21e1aa4cd592
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>Szenario: Implementieren der Aufbewahrung von Informationen auf Dateiservern

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Aufbewahrungsdauer bezeichnet den Zeitraum, der ein Dokument sein sollte beibehalten werden, bevor es abläuft. Die Aufbewahrungsdauer kann unterschiedlich sein, abhängig von der Organisation. Sie können Dateien in einem Ordner nach kurzer, mittlerer oder langer Aufbewahrungsdauer klassifizieren und anschließend einen Zeitraum für jede Dauer zuweisen. Möglicherweise möchten eine Datei unbegrenzt aufbewahren, platzieren es rechtliche Aufbewahrungspflicht zuweisen.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Dateiklassifizierungsinfrastruktur und File Server Resource Manager wird mit Dateiverwaltungsaufgaben und die Dateiklassifizierung Aufbewahrungsdauer für einen Satz Dateien angewendet. Sie können in einem Ordner eine Aufbewahrungsdauer zuweisen und dann eine Dateiverwaltungsaufgabe so konfigurieren Sie die Dauer eine zugewiesenen Aufbewahrungsdauer dauern soll. Wenn die Dateien im Ordner sind in Kürze abläuft, erhält der Besitzer der Dateien eine E-Mail-Benachrichtigung. Sie können auch klassifizieren eine Datei als rechtliche Aufbewahrungspflicht zuweisen, damit die Dateiverwaltungsaufgabe nicht die Datei abläuft.  
  
Sie finden die Planungsinformationen für das Konfigurieren der Aufbewahrung in [Planen der Aufbewahrung von Informationen auf Dateiservern](assetId:///edf13190-7077-455a-ac01-f534064a9e0c).  
  
Schrittezum Klassifizieren von Dateien für die gesetzliche Aufbewahrungspflicht und zum Konfigurieren einer Aufbewahrungsdauer in finden [bereitstellen implementieren Aufbewahrung von Informationen auf Dateiservern & 40; Schrittezur Veranschaulichung & 41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md).  
  
> [!NOTE]  
> Dieses Szenario beschreibt nur, wie Sie ein Dokument für die gesetzliche Aufbewahrungspflicht manuell klassifiziert. Allerdings ist es möglich, in Windows Server2012 Dokumente für die gesetzliche Aufbewahrungspflicht automatisch zu klassifizieren. Eine Möglichkeit hierzu ist eine Windows PowerShell-Klassifizierung zu erstellen, die der Dateibesitzer mit einer Liste von Benutzerkonten verglichen wird, die unter gesetzlicher Aufbewahrungspflicht stehen. Wenn der Dateibesitzer Teil der Benutzerkontoliste ist, wird die Datei für die gesetzliche Aufbewahrungspflicht klassifiziert.  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Dieses Szenario ist Teil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgende Tabelle werden die Features, die in diesem Szenario sind aufgeführt und beschrieben, wie sie unterstützen.  
  
|Funktion|Wie sie dieses Szenario unterstützt|  
|-----------|---------------------------------|  
|[File Server Resource Manager (Übersicht)](https://technet.microsoft.com/library/hh831701.aspx)|Die Dateiklassifizierungsinfrastruktur ist ein Feature, das in File Server Resource Manager enthalten ist.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|File Server Resource Manager ist ein Feature, das mit der Serverrolle Dateidienste enthalten ist.|  
  
  


