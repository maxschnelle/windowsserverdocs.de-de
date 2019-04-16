---
ms.assetid: 3ea48a72-20a2-4da4-84e4-26b5728513ce
title: "Planen der Datei Dateizugriffsüberwachung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 65e941f6741298da54186be10bd9c0add115ea14
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="plan-for-file-access-auditing"></a>Planen der Datei Dateizugriffsüberwachung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die Informationen in diesem Thema wird erläutert, die Sicherheit Erweiterungen zur Sicherheitsüberwachung, die in Windows Server2012 und neue eingeführt wurden Überwachungsrichtlinieneinstellungen, die Sie beim Bereitstellen der dynamischen Zugriffssteuerung in Ihrem Unternehmen berücksichtigen sollten. Die tatsächliche Überwachungsrichtlinieneinstellungen, die Sie bereitstellen, hängt von Ihrer Ziele, die Einhaltung von Richtlinien, Überwachung, forensische Analyse und Problembehandlung enthalten kann.  
  
> [!NOTE]  
> Weitere Informationen zum Planen und Bereitstellen einer übergreifenden Sicherheitsüberprüfungsstrategie für Ihr Unternehmen [planen und Bereitstellen von erweiterten Sicherheitsüberwachungsrichtlinien](https://go.microsoft.com/fwlink/?LinkID=191139). Weitere Informationen zum Konfigurieren und Bereitstellen einer Sicherheitsüberwachungsrichtlinie finden Sie unter der [Erweiterte Einstellungen für Sicherheitsüberwachungsrichtlinien Step-by-Step Handbuch](https://go.microsoft.com/fwlink/?LinkID=191141).  
  
Die folgenden Überwachung Sicherheitsfunktionen in Windows Server2012 können zum Erweitern der Überwachung Gesamtsicherheitsstrategie mit der dynamischen Zugriffssteuerung verwendet werden.  
  
-   **Ausdrucksbasierte Überwachungsrichtlinien**. Dynamische Zugriffssteuerung können Sie gezielte Überprüfungsrichtlinien mithilfe von Ausdrücken, die basierend auf Benutzer, Computer und ressourcenansprüchen erstellen. Beispielsweise könnten Sie eine Überwachungsrichtlinie, um alle Lese- und Schreibvorgänge Vorgänge auf Dateien, die von Mitarbeitern, die nicht über eine hochsicherheitsberechtigung verfügen High Business Impact klassifiziert nachzuverfolgen erstellen. Ausdrucksbasierte Überwachungsrichtlinien können direkt für eine Datei oder einen Ordner oder zentral über die Gruppenrichtlinie erstellt werden. Weitere Informationen finden Sie unter [Gruppenrichtlinien mit globaler Objektzugriffsüberwachung](https://go.microsoft.com/fwlink/?LinkId=241498).  
  
-   **Weitere Informationen über die objektzugriffsüberwachung**. Dateizugriffsüberwachung ist nicht mit Windows Server2012. Mit der entsprechenden Überwachungsrichtlinie vorhanden generieren die Windows- und Windows Server-Betriebssysteme ein Überwachungsereignis jedes Mal ein Benutzer auf eine Datei zugreift. Vorhandene dateizugriffsereignisse (4656, 4663) enthalten Informationen zu den Attributen der Datei, die auf die zugegriffen wurde. Diese Informationen kann durch die ereignisprotokollfilterung Tools verwendet werden, können Sie die Identifizierung der wichtigsten Überwachungsereignisse zu. Weitere Informationen finden Sie unter [Handleänderungsüberwachung](https://technet.microsoft.com//library/dd772626(WS.10).aspx) und [Sicherheitskonten-Manager](https://go.microsoft.com/fwlink/?LinkId=241501).  
  
-   **Weitere Informationen aus benutzeranmeldeereignissen**. Mit der entsprechenden Überwachungsrichtlinie vorhanden wird ein Überwachungsereignis jedes Mal, wenn ein Benutzer auf einem Computer lokal oder Remote anmeldet von Windows-Betriebssystemen erzeugen. In Windows Server2012 oder Windows8 überwachen Sie Benutzer- und Geräteansprüche Sicherheitstoken eines Benutzers zugeordnet. Beispiele für können Abteilung, Unternehmen, Projekt und Sicherheit Sicherheitsüberprüfungen sind. Ereignis 4626 enthält Informationen zu diesen Benutzer- und Geräteansprüchen, die durch überwachen, Management-Tools zum Korrelieren von Benutzeranmeldeereignisse mit Objektzugriffsereignissen ereignisfilterung basierend auf Dateiattributen und Benutzerattributen zu ermöglichen genutzt werden können. Weitere Informationen zur benutzeranmeldeüberwachung finden Sie unter [Überwachung der Anmeldung](https://go.microsoft.com/fwlink/?LinkId=241502).  
  
-   **Änderungsnachverfolgung für neue Typen von sicherungsfähigen Objekten**. Nachverfolgen von Änderungen an sicherungsfähigen Objekten kann in den folgenden Szenarios wichtig sein:  
  
    -   **Änderungsnachverfolgung für zentrale Zugriffsrichtlinien und zentrale Zugriffsregeln**. Zentrale Zugriffsrichtlinien und zentrale Zugriffsregeln definieren die zentrale Richtlinie, die zum Steuern des Zugriffs auf kritische Ressourcen verwendet werden kann. Alle Änderungen an diesen kann direkt auf die Dateizugriffsberechtigungen auswirken, die Benutzer auf mehreren Computern gewährt werden. Daher kann Nachverfolgen von Änderungen an zentralen Zugriffsrichtlinien und zentrale Zugriffsregeln wichtig für Ihre Organisation sein. Da zentrale Zugriffsrichtlinien und zentrale Zugriffsregeln in Active Directory-Domänendienste (AD DS) gespeichert sind, können Sie Änderungsversuche, wie Änderungen an anderen sicherungsfähigen Objekten in AD DS überwachen. Weitere Informationen finden Sie unter [Verzeichnisdienstzugriff](https://technet.microsoft.com/library/dd941618(WS.10).aspx).  
  
    -   **Änderungsnachverfolgung für Definitionen im anspruchswörterbuch**. Anspruchsdefinitionen umfassen den anspruchsnamen, Beschreibung und mögliche Werte. Alle Änderungen an der anspruchsdefinition können die Zugriffsberechtigungen für kritische Ressourcen auswirken. Daher kann das Nachverfolgen Änderungen an anspruchsdefinitionen wichtig für Ihre Organisation sein. Wie zentrale Zugriffsrichtlinien und zentrale Zugriffsregeln werden auch anspruchsdefinitionen in AD DS gespeichert; Daher können sie wie alle anderen sicherungsfähigen Objekte in AD DS überwacht werden. Weitere Informationen finden Sie unter [Verzeichnisdienstzugriff](https://technet.microsoft.com/library/dd941618(WS.10).aspx).  
  
    -   **Änderungsnachverfolgung für Dateiattribute**. Dateiattribute bestimmen, welche zentrale Zugriffsregel auf die Datei angewendet. Eine Änderung an den Dateiattributen kann sich potenziell auf die zugriffsbeschränkungen der Datei auswirken. Aus diesem Grund kann es wichtig, dass Änderungen an Dateiattributen nachzuverfolgen sein. Sie können Änderungen an Dateiattributen auf jedem Computer nachverfolgen, durch die Konfiguration der Überwachungsrichtlinie Autorisierung Richtlinie ändern. Weitere Informationen finden Sie unter [autorisierungsrichtlinienänderung](https://go.microsoft.com/fwlink/?LinkId=241504) und [objektzugriffsüberwachung für Dateisysteme](https://go.microsoft.com/fwlink/?LinkId=241505). In Windows Server2012 unterscheidet Ereignis 4911 Dateiattributs-Richtlinienänderungen von anderen Autorisierung Richtlinienänderungsereignisse.  
  
    -   **Änderungsnachverfolgung für die zentrale Zugriffsrichtlinie einer Datei zugeordnet.** Ereignis 4913 zeigt die Sicherheits-IDs (SIDs) von der alten und neuen zentralen Zugriffsrichtlinien an. Jede zentrale Zugriffsrichtlinie verfügt außerdem über einen Anzeigenamen, der mithilfe dieser Sicherheits-ID gesucht werden kann. Weitere Informationen finden Sie unter [autorisierungsrichtlinienänderung](https://go.microsoft.com/fwlink/?LinkId=241504).  
  
    -   **Änderungsnachverfolgung für Benutzer- und Computerattribute**. Wie Dateien Benutzer- und Computerobjekte Attribute aufweisen, und Änderungen an diesen Attributen können sich die Benutzer den Zugriff auf Dateien auswirken. Aus diesem Grund kann es sinnvoll sein, Änderungen an Benutzer- oder Computerattributen nachzuverfolgen sein. Benutzer- und Computerobjekte werden in AD DS gespeichert. aus diesem Grund können Änderungen an ihrer Attribute überwacht werden. Weitere Informationen finden Sie unter [DS-Zugriff](https://go.microsoft.com/fwlink/?LinkId=241508).  
  
-   **Richtlinienänderungsbereitstellung**. Änderungen an zentralen Zugriffsrichtlinien können sich auf die zugriffssteuerungsentscheidungen auf allen Computern auswirken, in denen die Richtlinien durchgesetzt werden. Eine unzureichende Richtlinie könnte mehr Zugriff als gewünscht gewähren, und eine zu restriktive Richtlinie könnte eine übermäßige Anzahl der Anrufe beim Helpdesk generieren. Daher kann äußerst sinnvoll sein, Änderungen an einer zentralen Zugriffsrichtlinie zu überprüfen, bevor die Änderung erzwungen werden. Zu diesem Zweck führt Windows Server2012 das Konzept der "Bereitstellung". Mit der Bereitstellung können Benutzer vorgeschlagene Richtlinienänderungen überprüfen, bevor Sie erzwungen werden. Zum verwenden, werden vorgeschlagene Richtlinien mit den erzwungenen Richtlinien bereitgestellt, aber nicht tatsächlich bereitgestellte Richtlinien gewähren oder Verweigern von Berechtigungen. Windows Server2012 protokolliert stattdessen ein Überwachungsereignis (4818) jedes Mal, wenn das Ergebnis der zugriffsüberprüfung, die die bereitgestellte Richtlinie verwendet vom Ergebnis einer zugriffsüberprüfung unterscheidet, die die erzwungene Richtlinie verwendet.  
  


