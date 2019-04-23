---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: Szenario implementieren-Aufbewahrung von Informationen auf Dateiservern
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59fd7f0a0a4d9ed8f5cec57b17be21e1aa4cd592
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880251"
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>Szenario: Implementieren der Aufbewahrung von Informationen auf Dateiservern

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aufbewahrungsdauer bezeichnet den Zeitraum, den ein Dokument aufbewahrt werden sollte, bevor es als abgelaufen gilt. Die Aufbewahrungsdauer kann sich je nach Organisation unterscheiden. Sie können Dateien in einem Ordner nach kurzer, mittlerer oder langer Aufbewahrungsdauer klassifizieren und anschließend einen Zeitraum für jede Dauer zuweisen. Sie können eine Datei unbegrenzt aufbewahren, in dem sie ihr eine rechtliche Aufbewahrungspflicht zuweisen.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Die Dateiklassifizierungsinfrastruktur und der Ressourcen-Manager für Dateiserver verwenden Dateiverwaltungsaufgaben und die Dateiklassifizierung, um eine Aufbewahrungsdauer auf einen Satz von Dateien anzuwenden. Sie können einem Ordner eine Aufbewahrungsdauer zuweisen und anschließend eine Dateiverwaltungsaufgabe verwenden, um die Dauer einer zugewiesenen Aufbewahrungsdauer zu konfigurieren. Wenn das Ablaufen der Dateien im Ordner bevorsteht, erhält der Besitzer der Dateien eine E-Mail-Benachrichtigung. Sie können einer Datei auch eine rechtliche Aufbewahrungspflicht zuweisen, damit die Dateiverwaltungsaufgabe das Ablaufen der Datei verhindert.  
  
Sie können Informationen für das Konfigurieren der Aufbewahrungsdauer in [Planen der Aufbewahrung von Informationen auf Dateiservern](assetId:///edf13190-7077-455a-ac01-f534064a9e0c) finden.  
  
Finden Sie Schritte zum Klassifizieren von Dateien für die gesetzliche Aufbewahrungspflicht und zum Konfigurieren einer Aufbewahrungsdauer in [bereitstellen implementieren Aufbewahrung von Informationen auf Dateiservern &#40;Demonstrationsschritte&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md).  
  
> [!NOTE]  
> In diesem Szenario wird nur erörtert, wie ein Dokument für die gesetzliche Aufbewahrungspflicht manuell klassifiziert wird. Allerdings ist es möglich, in Windows Server 2012 auf Dokumente, für die gesetzliche Aufbewahrungspflicht automatisch zu klassifizieren. Eine Möglichkeit, um dies umzusetzen, besteht darin, eine Windows PowerShell-Klassifizierung zu erstellen, in der der Dateibesitzer mit einer Liste von Benutzerkonten verglichen wird, die unter gesetzlicher Aufbewahrungspflicht stehen. Wenn der Dateibesitzer Teil der Benutzerkontoliste ist, für die Datei für die gesetzliche Aufbewahrungspflicht klassifiziert.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------|---------------------------------|  
|[Übersicht über die Ressourcen-Manager](https://technet.microsoft.com/library/hh831701.aspx)|Die Dateiklassifizierungsinfrastruktur ist ein im Ressourcen-Manager für Dateiserver enthaltenes Feature.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|Der Ressourcen-Manager für Dateiserver ist ein in der Serverrolle „Dateidienste“ enthaltenes Feature.|  
  
  


