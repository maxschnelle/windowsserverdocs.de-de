---
title: Überwachen der vorhandenen Last auf dem Remotezugriffsserver
description: Dieses Thema ist Teil des Leitfadens für die Überwachung des Remotezugriffs und Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62fa2895-62ae-42cf-817c-53e06ac2a26c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6d7a5aa7b699f5a8f24c4a36ee8ae314768329b4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446861"
---
# <a name="monitor-the-existing-load-on-the-remote-access-server"></a>Überwachen der vorhandenen Last auf dem Remotezugriffsserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Durch Windows Server 2013 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Der Begriff **Load** bezieht sich auf die Statistiken, die sich auf die Anzahl der Verbindungen auf dem RAS-Server beziehen. Es folgen die Schritte, die zum Nachverfolgen von der Last auf dem RAS-Server erforderlich.  
  
Können Sie die Dashboards für die Überwachung, die in der Verwaltungskonsole auf dem RAS-Server an die Load-Statistiken für den Server verfügbar ist, oder Sie können Leistungsindikatoren zum Nachverfolgen von Statistiken.  
  
> [!NOTE]  
> Sie müssen als Mitglied der Gruppe "Domänen-Admins" oder ein Mitglied der Gruppe "Administratoren" auf jedem Computer angemeldet sein, die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht abschließen können, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Administratoren" ist, versuchen Sie es die Aufgabe auszuführen, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-use-the-monitoring-dashboard-to-monitor-the-remote-access-server-load"></a>Das überwachungsdashboard zum Überwachen der Auslastung des RAS-Servers verwenden  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **DASHBOARD**, um in der **Remotezugriffs-Verwaltungskonsole** zum **Remotezugriffdashboard** zu navigieren.  
  
3.  Beachten Sie, dass das Dashboard für die **Remoteclientstatus** Kachel innerhalb der **Serverstatus** Kachel. Diese Kachel listet Statistiken, wie die Gesamtanzahl der remote verbundenen Clients, die Gesamtzahl der DirectAccess-Clients, die verbunden sind und die maximale Anzahl von Benutzern, die in den letzten 24 Stunden eine Verbindung hergestellt.  
  
4.  Klicken Sie auf **aktualisieren** unter **Aufgaben** im rechten Bereich, den Integritätsstatus neu zu laden. Um das standardmäßige Aktualisierungsintervall ändern möchten, klicken Sie auf **Aktualisierungsintervall konfigurieren** unter **Aufgaben**.  
  
#### <a name="to-use-the-performance-monitor-tool-to-monitor-performance-counters-on-the-remote-access-server"></a>Verwenden Sie das Systemmonitortool zum Überwachen von Leistungsindikatoren auf dem RAS-server  
  
1.  Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und doppelklicken Sie dann auf **Systemmonitor**.  
  
2.  Klicken Sie unter **Leistung**, klicken Sie auf **Systemmonitor**.  
  
3.  Klicken Sie auf die **hinzufügen** Schaltfläche (gekennzeichnet durch ein grünes Symbol für die übergreifende) in der **Systemmonitor** Symbolleiste.  
  
4.  Aus der Liste der **Verfügbare Leistungsindikatoren**, wählen Sie alle Leistungsindikatoren in der **RAS** und **RAmgmtsvc** Kategorien, und klicken Sie dann auf **hinzufügen >>** .  
  
5.  In diesem Fall aus der Liste der **Verfügbare Leistungsindikatoren**, wählen Sie alle Leistungsindikatoren in der **IPsec-Verbindungen** Kategorie, und klicken Sie dann auf **hinzufügen >>.**  
  
6.  Klicken Sie auf **OK** zum Hinzufügen von der ausgewählten Indikatoren in der **Systemmonitor** Konsole für die nachverfolgung.  
  
**Systemmonitor** wird jetzt die ausgewählten Server laden Statistiken grafisch angezeigt.  
  
![Windows PowerShell](../../../media/Monitor-the-existing-load-on-the-Remote-Access-server/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary  
```  
  


