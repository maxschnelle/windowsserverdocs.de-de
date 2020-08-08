---
title: Überwachen der vorhandenen Last auf dem Remotezugriffsserver
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 62fa2895-62ae-42cf-817c-53e06ac2a26c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9a04cdff7214fd4d7ef64fba930f282e48dbfa01
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970217"
---
# <a name="monitor-the-existing-load-on-the-remote-access-server"></a>Überwachen der vorhandenen Last auf dem Remotezugriffsserver

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

**Hinweis:** Durch Windows Server 2012 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.

Der Begriff " **Laden** " bezieht sich auf die Statistiken, die sich auf die Anzahl der Verbindungen auf dem RAS-Server beziehen. Es folgen die Schritte, die zum Nachverfolgen der Last auf dem RAS-Server erforderlich sind.

Mithilfe des Überwachungs Dashboards, das in der-Verwaltungskonsole auf dem RAS-Server zur Verfügung steht, können Sie die Auslastungs Statistiken für den Server anzeigen, oder Sie können Leistungsindikatoren verwenden, um die Statistiken zu überwachen.

> [!NOTE]
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.

#### <a name="to-use-the-monitoring-dashboard-to-monitor-the-remote-access-server-load"></a>So verwenden Sie das Überwachungs Dashboard zum Überwachen der Remote Zugriffs Serverauslastung

1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.

2.  Klicken Sie auf **DASHBOARD**, um in der **Remotezugriffs-Verwaltungskonsole** zum **Remotezugriffdashboard** zu navigieren.

3.  Beachten Sie auf dem Dashboard Überwachung die Kachel **Remote Client Status** innerhalb der Kachel **Server Status** . Auf dieser Kachel werden Statistiken wie die Gesamtzahl der verbundenen Remote Clients, die Gesamtzahl der verbundenen DirectAccess-Clients sowie die maximale Anzahl von Benutzern aufgelistet, die in den letzten 24 Stunden eine Verbindung hergestellt haben.

4.  Sie können im rechten Bereich unter **Aufgaben** auf **Aktualisieren** klicken, um den Integritäts Status erneut zu laden. Um das Standard Aktualisierungs Intervall zu ändern, klicken Sie unter **Aufgaben**auf **Aktualisierungs Intervall konfigurieren** .

#### <a name="to-use-the-performance-monitor-tool-to-monitor-performance-counters-on-the-remote-access-server"></a>So verwenden Sie das System Monitor Tool zum Überwachen von Leistungsindikatoren auf dem Remote Zugriffs Server

1.  Klicken Sie auf **Start**, klicken Sie auf **Verwaltung**, und doppelklicken Sie dann auf System **Monitor**.

2.  Klicken Sie unter **Leistung**auf System **Monitor**.

3.  Klicken Sie in der Symbolleiste des System **Monitors** auf die Schaltfläche **Hinzufügen** (durch ein grünes Kreuz Symbol gekennzeichnet).

4.  Wählen Sie in der Liste der **verfügbaren**Leistungsindikatoren alle Indikatoren in den Kategorien **RAS** und **ramgmzvc** aus, und klicken Sie dann auf **>>hinzufügen **.

5.  Wählen Sie erneut in der Liste der **verfügbaren**Leistungsindikatoren alle Indikatoren in der Kategorie **IPSec-Verbindungen** aus, und klicken Sie dann auf **>> hinzufügen.**

6.  Klicken Sie auf **OK** , um die ausgewählten **Leistungsindikatoren** in der System Monitor Konsole für die Überwachung hinzuzufügen.

Der System **Monitor** zeigt nun die ausgewählten Server Lade Statistiken grafisch an.

![Äquivalente Windows PowerShell-Befehle in Windows](../../../media/Monitor-the-existing-load-on-the-Remote-Access-server/PowerShellLogoSmall.gif)***<em>PowerShell</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
PS> Get-RemoteAccessConnectionStatisticsSummary
```



