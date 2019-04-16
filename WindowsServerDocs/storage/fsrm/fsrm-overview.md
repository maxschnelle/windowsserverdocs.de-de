---
title: "Übersicht über Ressourcen-Manager für Dateiserver (File Server Resource Manager, FSRM)"
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 7/7/2017
description: "Der Ressourcen-Manager für Dateiserver (FSRM) ist ein Tool zum Verwalten und Klassifizieren von Daten auf dem Windows Server-Dateiserver."
ms.openlocfilehash: ddfc0a0f4bede89a3c3a624d4f128717d0f1ac08
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="file-server-resource-manager-fsrm-overview"></a>Übersicht über Ressourcen-Manager für Dateiserver (File Server Resource Manager, FSRM)

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Der Ressourcen-Manager für Dateiserver (FSRM) ist ein Rollendienst unter Windows Server, der Ihnen das Verwalten und Klassifizieren von auf Dateiservern gespeicherten Daten ermöglicht. Der Ressourcen-Manager für Dateiserver umfasst die folgenden Features:
  
-   **Dateiklassifizierungsinfrastruktur** Die Dateiklassifizierungsinfrastruktur bietet Einsicht in Ihre Daten, indem Klassifizierungsvorgänge für eine effektivere Datenverwaltung automatisiert werden. Sie können Dateien klassifizieren und Richtlinien auf der Basis dieser Klassifizierung anwenden. Beispielrichtlinien umfassen die dynamische Zugriffsteuerung zum Einschränken des Dateizugriffs, Dateiverschlüsselung und Dateiablauf. Dateien können anhand von Dateiklassifizierungsregeln oder manuell durch Ändern der Eigenschaften einer ausgewählten Datei oder eines Ordners automatisch klassifiziert werden.  
  
-   **Dateiverwaltungsaufgaben** Mit den Dateiverwaltungsaufgaben können Sie auf Basis der Klassifizierung eine bedingte Richtlinie oder eine Aktion auf Dateien anwenden. Zu den Bedingungen einer Dateiverwaltungsaufgabe zählen der Dateispeicherort, die Klassifizierungseigenschaften, das Erstellungsdatum der Datei, das Datum der letzten Dateiänderung oder das Datum des letzten Dateizugriffs. Zu den möglichen Aktionen für eine Dateiverwaltungsaufgabe gehören die Fähigkeit zum Ablaufen von Dateien, zum Verschlüsseln von Dateien oder zum Ausführen eines benutzerdefinierten Befehls.  
  
-   **Kontingentverwaltung** Mithilfe von Kontingenten können Sie den für ein Volume oder einen Ordner zulässigen Platz beschränken. Außerdem können Kontingente automatisch auf neue, auf einem Volume erstellte Ordner angewendet werden. Sie können außerdem Kontingentvorlagen definieren, die auf neue Volumes oder Ordner angewendet werden können.  
  
-   **Dateiprüfungsverwaltung** Mithilfe von Dateiprüfungen können Sie die Dateitypen steuern, die Benutzer auf einem Dateiserver speichern können. Sie können die Erweiterungen einschränken, die für freigegebene Dateien gespeichert werden können. Sie können beispielsweise eine Dateiprüfung erstellen, die verhindert, dass Dateien mit der Erweiterung %%amp;quot;MP3%%amp;quot; in persönlichen freigegebenen Ordnern auf einem Dateiserver gespeichert werden.  
  
-   **Speicherberichte** Anhand von Speicherberichten können Sie Trends bei der Datenträgerverwendung und die Art der Datenklassifizierung ermitteln. Zudem können Sie eine ausgewählte Benutzergruppe bezüglich Versuchen überwachen, nicht autorisierte Dateien zu speichern.  
  
 Die Features des Ressourcen-Managers für Dateiserver können mit der MMC (Microsoft Management Console) des Ressourcen-Managers für Dateiserver oder mit Windows PowerShell konfiguriert und verwaltet werden.  
  
> [!IMPORTANT]
>  Der Ressourcen-Manager für Dateiserver unterstützt nur Volumes, die mit dem NTFS-Dateisystem formatiert sind. Das ReFS (Resilient File System, Robustes Dateisystem) wird nicht unterstützt.  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle  
 Im Folgenden finden Sie einige praktische Anwendungsfallbeispiele für den Ressourcen-Manager für Dateiserver:  
  
-   Erstellen Sie mit der Dateiklassifizierungsinfrastruktur und dem Szenario für die dynamische Zugriffssteuerung eine Richtlinie, mit der Sie auf Basis der Dateiklassifizierung auf dem Dateiserver Zugriff auf Dateien und Ordner erteilen.  
  
-   Erstellen Sie eine Dateiklassifizierungsregel, mit der beliebige Dateien, die mindestens 10 Sozialversicherungsnummern enthalten, als Dateien mit personenbezogenen Daten gekennzeichnet werden können.  
  
-   Kennzeichnen Sie Dateien, die in den letzten 10Jahren nicht geändert wurden, als abgelaufen.  
  
-   Erstellen Sie ein Kontingent mit 200 MB für das jeweilige Stammverzeichnis der Benutzer, und benachrichtigen Sie sie, wenn sie 180 MB verwenden.  
  
-   Verhindern Sie das Speichern von Musikdateien in persönlichen freigegebenen Ordnern.  
  
-   Planen Sie einen Bericht, der jeden Sonntag um Mitternacht ausgeführt wird und eine Liste mit den Dateien generiert, auf die in den beiden vorherigen Tagen am häufigsten zugegriffen wurde. Damit können Sie die Speicheraktivität am Wochenende ermitteln und Serverausfallzeiten entsprechend einplanen.  

## <a name="see-also"></a>Weitere Informationen:

- [Neues zum Ressourcen-Manager für Dateiserver](https://technet.microsoft.com/library/dn383587.aspx)
- [Dynamische Zugriffssteuerung](https://technet.microsoft.com/library/dn408191(v=ws.11).aspx) 