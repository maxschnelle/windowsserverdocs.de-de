---
title: Überwachen des Konfigurationsverteilungsstatus des Remotezugriffsservers
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: de285d13-9e54-4c46-88f0-607182e5e3dc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 459471c87034fbeaf11f9099e643c495a6b75389
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997287"
---
# <a name="monitor-the-configuration-distribution-status-of-the-remote-access-server"></a>Überwachen des Konfigurationsverteilungsstatus des Remotezugriffsservers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

**Hinweis:** Windows Server 2012 kombiniert DirectAccess und RAS-Dienst (RAS) zu einer einzigen Remote Zugriffs Rolle.

Die Remotezugriffs-Verwaltungskonsole vergleicht die Konfigurationsversionen aller überwachten Server, um zu überprüfen, dass sie übereinstimmen und die aktuellste Konfigurationsversion verwenden. Sie zeigt an, ob die aktuellste Konfigurationsversion (die in den Gruppenrichtlinienobjekten angegeben sind) an alle Server verteilt wurde und ob sie erfolgreich sie erfolgreich auf den Servern angewendet wurde.

### <a name="to-use-the-monitoring-dashboard-to-monitor-the-configuration-distribution"></a>So verwenden Sie das Überwachungsdashboard zum Überwachen der Konfigurationsverteilung

1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.

2.  Klicken Sie auf **DASHBOARD**, um in der **Remotezugriffs-Verwaltungskonsole** zum **Remotezugriffdashboard** zu navigieren.

3.  Beachten Sie im Überwachungsdashboard die Kachel **Konfigurationsstatus** oben in der Mitte. Die Kachel zeigt den aktuellen Status der Konfigurationsverteilung an.

In der folgenden Tabelle sind die Meldungen, die von der Kachel **Konfigurationsstatus** generiert werden, ihre Bedeutungen und die erforderliche administrative Aktion (falls vorhanden) aufgeführt.

|Schweregrad|Nachricht|Bedeutung|Vorgehensweise|
|--|--|--|
|Erfolg|Die Konfiguration wurde erfolgreich verteilt.|Die Konfiguration in dem Gruppenrichtlinienobjekt wurde erfolgreich auf dem Server angewendet.|Keine Aktion erforderlich.|
|Warnung|Die Konfiguration für den Server [*Servername*] wurde nicht vom Domänencontroller abgerufen. Das GPO ist nicht verknüpft.|Die Konfiguration in dem Gruppenrichtlinienobjekt konnte den Server noch nicht erreichen. Die Ursache für dieses Problem könnte sein, dass das GPO nicht mit dem Server verknüpft ist.|Verknüpfen Sie das GPO mit einem Verwaltungsbereich, der auf den Server angewendet wird, oder exportieren Sie die Einstellungen in einem GPO-Bereitstellungsszenario aus der GPO-Bereitstellung und importieren Sie sie in die Produktions-GPO. Weitere Informationen zu staginggruppen Richtlinien Objekten finden Sie unter Verwalten von Remote Zugriffs-Gruppenrichtlinien Objekten **mit eingeschränkten Berechtigungen** in [Schritt-1-Plan-The-DirectAccess-Infrastructure](../../directaccess/single-server-advanced/da-adv-plan-s1-infrastructure.md). Informationen zu GPO-stagingschritten finden Sie unter Konfigurieren von Remote Zugriffs-Gruppenrichtlinien Objekten **mit eingeschränkten Berechtigungen** in [Schritt 1: Konfigurieren der DirectAccess-Infrastruktur](../../directaccess/single-server-advanced/da-adv-configure-s1-infrastructure.md).|
|Warnung|Die Konfiguration für den Server [*Servername*] wurde nicht vom Domänencontroller abgerufen.|Die Konfiguration in dem Gruppenrichtlinienobjekt konnte den Server noch nicht erreichen.<p>Es kann bis zu 10 Minuten dauern, bis eine neue Konfiguration verteilt wird.|Räumen Sie einen weiteren Zeitraum ein, damit die Richtlinien auf dem Server aktualisiert werden können.|
|Fehler|Die Konfiguration für den Server [*Servername*] wurde nicht vom Domänencontroller abgerufen.|Die Konfiguration in dem GPO konnte den Server nicht erreichen. Und seit der Konfigurationsänderung sind mehr als 10 Minuten vergangen.|Diese Problem kann in einem der folgenden Szenarios auftreten:<p>-Der Server hat keine Verbindung mit der Domäne, um die Richtlinien zu aktualisieren. Sie können "gpupdate/force" auf dem Server ausführen, um eine Richtlinien Aktualisierung zu erzwingen.<br />-GPO-Replikation ist möglicherweise erforderlich, um die aktualisierte Konfiguration abzurufen.<br />-Der Active Directory Standort des RAS-Servers enthält keinen beschreibbaren Domänen Controller.<p>Warten Sie, bis die GPOs mit allen Domänencontrollern repliziert wurden, und verwenden Sie dann das Windows PowerShell-Cmdlet **Set-DAEntryPointDC**, um den Einstiegspunkt dem beschreibbaren Domänencontroller auf dem Remotezugriffsserver zuzuordnen.|
|Warnung|Die Konfiguration für den Server [*Servername*] wurde vom Domänencontroller abgerufen, jedoch noch nicht angewendet.|Die Konfiguration in dem GPO hat den Server erreicht, sie wurde jedoch noch nicht angewendet.<p>Es kann bis zu 15 Minuten dauern, bevor die Konfiguration angewendet wird.|Räumen Sie einen weiteren Zeitraum ein, damit die Konfiguration vollständig auf dem Server angewendet werden kann.|
|Fehler|Die Konfiguration für den Server [*Servername*] wurde vom Domänencontroller abgerufen, kann jedoch nicht angewendet werden.|Die Konfiguration in dem GPO konnte den Server erreichen, sie wurde jedoch nicht erfolgreich angewendet. Außerdem sind seit der Konfigurationsänderungen mehr als 15 Minuten vergangen.|Diese Problem kann in einem der folgenden Szenarios auftreten:<p>1. die Konfiguration wird zurzeit angewendet. Diese Meldung wird als Fehler angezeigt, da zum Abrufen der Konfiguration aus dem GPO möglicherweise ein längerer Zeitraum erforderlich war.<br />    Um diese mögliche Ursache zu bestätigen, verwenden Sie die **Aufgabenplanung** und navigieren Sie zu Microsoft\Windows\RemoteAccess, um zu prüfen, ob **RAConfigTask** aktuell ausgeführt wird.<br />2. Wenn **raconfigtask** zurzeit nicht ausgeführt wird, konnte die Konfiguration möglicherweise nicht auf den Server angewendet werden.<br />    Überprüfen Sie die **Ereignisanzeige** unter dem Remotezugriffsserver-Vorgangskanal, der sich unter \Anwendungs- und Dienstprotokolle\Microsoft\Windows\RemoteAccess-RemoteAccessServer befindet.<br />    Überprüfen Sie den **VORGANGSSTATUS** in der Remotezugriffs-Verwaltungskonsole auf Fehler. Weitere Informationen finden Sie unter [Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md).|
|Fehler|Die Konfiguration für Mehrfachstandortserver wurde vom Domänencontroller abgerufen. Einige Server besitzen abweichende Konfigurationen.|Zwischen den Konfigurationsversionen der Server-GPOs in der Bereitstellung mit mehreren Standorten besteht eine Inkonsistenz.<p>Idealerweise weisen alle Server-GPOs für alle Einstiegspunkte die gleiche globale Konfiguration auf, aus etwaigen Gründen sind sie jedoch nicht synchron.|Das kann vorkommen, wenn durch eine Konfigurationsänderung ein Fehler auftritt und die Änderung nicht erfolgreich zurückgesetzt wird.<p>Sie sollten die GPOs aus einem Sicherungsstatus wiederherstellen, in dem alle Server-GPOs synchronisiert wurden. Informationen zu einem Skript, das Sie verwenden können, finden Sie unter [Sichern und Wiederherstellen der Remote Zugriffs Konfiguration](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6).|