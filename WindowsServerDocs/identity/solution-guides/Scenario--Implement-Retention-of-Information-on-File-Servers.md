---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: Szenario implementieren der Aufbewahrung von Informationen auf Dateiservern
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 80653fe6d2956b08ee142b2f594648885a250b59
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964852"
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>Scenario: Implement Retention of Information on File Servers

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aufbewahrungsdauer bezeichnet den Zeitraum, den ein Dokument aufbewahrt werden sollte, bevor es als abgelaufen gilt. Die Aufbewahrungsdauer kann sich je nach Organisation unterscheiden. Sie können Dateien in einem Ordner nach kurzer, mittlerer oder langer Aufbewahrungsdauer klassifizieren und anschließend einen Zeitraum für jede Dauer zuweisen. Sie können eine Datei unbegrenzt aufbewahren, in dem sie ihr eine rechtliche Aufbewahrungspflicht zuweisen.  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Die Dateiklassifizierungsinfrastruktur und der Ressourcen-Manager für Dateiserver verwenden Dateiverwaltungsaufgaben und die Dateiklassifizierung, um eine Aufbewahrungsdauer auf einen Satz von Dateien anzuwenden. Sie können einem Ordner eine Aufbewahrungsdauer zuweisen und anschließend eine Dateiverwaltungsaufgabe verwenden, um die Dauer einer zugewiesenen Aufbewahrungsdauer zu konfigurieren. Wenn das Ablaufen der Dateien im Ordner bevorsteht, erhält der Besitzer der Dateien eine E-Mail-Benachrichtigung. Sie können einer Datei auch eine rechtliche Aufbewahrungspflicht zuweisen, damit die Dateiverwaltungsaufgabe das Ablaufen der Datei verhindert.  
  
Sie können Informationen für das Konfigurieren der Aufbewahrungsdauer in [Planen der Aufbewahrung von Informationen auf Dateiservern](assetId:///edf13190-7077-455a-ac01-f534064a9e0c) finden.  
  
Sie finden Schritte zum klassifizierens von Dateien für die gesetzliche Aufbewahrung und zum Konfigurieren einer Beibehaltungs Dauer in bereitstellen [Implementieren der Aufbewahrung von Informationen auf Dateiservern &#40;Demonstrations Schritte&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md).  
  
> [!NOTE]  
> In diesem Szenario wird nur erörtert, wie ein Dokument für die gesetzliche Aufbewahrungspflicht manuell klassifiziert wird. In Windows Server 2012 ist es jedoch möglich, Dokumente für Gesetzliche Aufbewahrungspflicht automatisch zu klassifizieren. Eine Möglichkeit, um dies umzusetzen, besteht darin, eine Windows PowerShell-Klassifizierung zu erstellen, in der der Dateibesitzer mit einer Liste von Benutzerkonten verglichen wird, die unter gesetzlicher Aufbewahrungspflicht stehen. Wenn der Dateibesitzer Teil der Benutzerkontoliste ist, für die Datei für die gesetzliche Aufbewahrungspflicht klassifiziert.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Funktion|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------|---------------------------------|  
|[File Server Resource Manager Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11))|Die Dateiklassifizierungsinfrastruktur ist ein im Ressourcen-Manager für Dateiserver enthaltenes Feature.|  
|[Datei- und Speicherdienste: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831487(v=ws.11))|Der Ressourcen-Manager für Dateiserver ist ein in der Serverrolle „Dateidienste“ enthaltenes Feature.|  
  
  
