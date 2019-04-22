---
title: Überwachen des Konfigurationsverteilungsstatus des Remotezugriffsservers
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
ms.assetid: de285d13-9e54-4c46-88f0-607182e5e3dc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3171eb9e9c90d0688fa413b80d9dbbf162e77fe8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818421"
---
# <a name="monitor-the-configuration-distribution-status-of-the-remote-access-server"></a>Überwachen des Konfigurationsverteilungsstatus des Remotezugriffsservers

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Windows Server 2012 werden DirectAccess "und" Remote Access Service (RAS) in einer einzigen remotezugriffsrolle zusammengefasst.  
  
Die Remotezugriffs-Verwaltungskonsole vergleicht die Konfigurationsversionen aller überwachten Server, um zu überprüfen, dass sie übereinstimmen und die aktuellste Konfigurationsversion verwenden. Sie zeigt an, ob die aktuellste Konfigurationsversion (die in den Gruppenrichtlinienobjekten angegeben sind) an alle Server verteilt wurde und ob sie erfolgreich sie erfolgreich auf den Servern angewendet wurde.  
  
### <a name="to-use-the-monitoring-dashboard-to-monitor-the-configuration-distribution"></a>So verwenden Sie das Überwachungsdashboard zum Überwachen der Konfigurationsverteilung  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **DASHBOARD**, um in der **Remotezugriffs-Verwaltungskonsole** zum **Remotezugriffdashboard** zu navigieren.  
  
3.  Beachten Sie im Überwachungsdashboard die Kachel **Konfigurationsstatus** oben in der Mitte. Die Kachel zeigt den aktuellen Status der Konfigurationsverteilung an.  
  
In der folgenden Tabelle sind die Meldungen, die von der Kachel **Konfigurationsstatus** generiert werden, ihre Bedeutungen und die erforderliche administrative Aktion (falls vorhanden) aufgeführt.  
  
|||||  
|-|-|-|-|  
|Nach Schweregrad|Meldung|Bedeutung|Maßnahme|  
|Erfolgreich|Die Konfiguration wurde erfolgreich verteilt.|Die Konfiguration in dem Gruppenrichtlinienobjekt wurde erfolgreich auf dem Server angewendet.|Keine Aktion erforderlich.|  
|Warnung|Die Konfiguration für den Server [*Servername*] wurde nicht vom Domänencontroller abgerufen. Das GPO ist nicht verknüpft.|Die Konfiguration in dem Gruppenrichtlinienobjekt konnte den Server noch nicht erreichen. Die Ursache für dieses Problem könnte sein, dass das GPO nicht mit dem Server verknüpft ist.|Verknüpfen Sie das GPO mit einem Verwaltungsbereich, der auf den Server angewendet wird, oder exportieren Sie die Einstellungen in einem GPO-Bereitstellungsszenario aus der GPO-Bereitstellung und importieren Sie sie in die Produktions-GPO. Weitere Informationen zu bereitstellungs-GPOs finden Sie unter **Verwalten von Remotezugriffs-Gruppenrichtlinienobjekten mit eingeschränkten Berechtigungen** in [Step-1-Plan-the-DirectAccess-Infrastructure](../../directaccess/single-server-advanced/Step-1-Plan-the-DirectAccess-Infrastructure.md). Schritte zu bereitstellungs-GPOs, finden Sie unter **Konfigurieren von Remotezugriffs-Gruppenrichtlinienobjekten mit eingeschränkten Berechtigungen** in [Schritt 1: Konfigurieren der DirectAccess-Infrastruktur](../../directaccess/single-server-advanced/Step-1-Configuring-DirectAccess-Infrastructure.md).|  
|Warnung|Die Konfiguration für den Server [*Servername*] wurde nicht vom Domänencontroller abgerufen.|Die Konfiguration in dem Gruppenrichtlinienobjekt konnte den Server noch nicht erreichen.<br /><br />Es kann bis zu 10 Minuten dauern, bis eine neue Konfiguration verteilt wird.|Räumen Sie einen weiteren Zeitraum ein, damit die Richtlinien auf dem Server aktualisiert werden können.|  
|Fehler|Die Konfiguration für den Server [*Servername*] wurde nicht vom Domänencontroller abgerufen.|Die Konfiguration in dem GPO konnte den Server nicht erreichen. Und seit der Konfigurationsänderung sind mehr als 10 Minuten vergangen.|Diese Problem kann in einem der folgenden Szenarios auftreten:<br /><br />-Der Server hat keine Verbindung zur Domäne, um die Richtlinien zu aktualisieren. Sie können "Gpupdate/force" ausführen, auf dem Server um eine richtlinienaktualisierung zu erzwingen.<br />-GPO-Replikation müssen möglicherweise die aktualisierte Konfiguration abzurufen.<br />– Es ist kein beschreibbarer Domänencontroller in Active Directory-Standort des RAS-Servers ein.<br /><br />Warten Sie, bis die GPOs mit allen Domänencontrollern repliziert wurden, und verwenden Sie dann das Windows PowerShell-Cmdlet **Set-DAEntryPointDC**, um den Einstiegspunkt dem beschreibbaren Domänencontroller auf dem Remotezugriffsserver zuzuordnen.|  
|Warnung|Die Konfiguration für den Server [*Servername*] wurde vom Domänencontroller abgerufen, jedoch noch nicht angewendet.|Die Konfiguration in dem GPO hat den Server erreicht, sie wurde jedoch noch nicht angewendet.<br /><br />Es kann bis zu 15 Minuten dauern, bevor die Konfiguration angewendet wird.|Räumen Sie einen weiteren Zeitraum ein, damit die Konfiguration vollständig auf dem Server angewendet werden kann.|  
|Fehler|Die Konfiguration für den Server [*Servername*] wurde vom Domänencontroller abgerufen, kann jedoch nicht angewendet werden.|Die Konfiguration in dem GPO konnte den Server erreichen, sie wurde jedoch nicht erfolgreich angewendet. Außerdem sind seit der Konfigurationsänderungen mehr als 15 Minuten vergangen.|Diese Problem kann in einem der folgenden Szenarios auftreten:<br /><br />1.  Die Konfiguration wird aktuell angewendet. Diese Meldung wird als Fehler angezeigt, da zum Abrufen der Konfiguration aus dem GPO möglicherweise ein längerer Zeitraum erforderlich war.<br />    Um diese mögliche Ursache zu bestätigen, verwenden Sie die **Aufgabenplanung** und navigieren Sie zu Microsoft\Windows\RemoteAccess, um zu prüfen, ob **RAConfigTask** aktuell ausgeführt wird.<br />2.  Wenn **RAConfigTask** aktuell nicht ausgeführt wird, konnte die Konfiguration möglicherweise nicht auf den Server angewendet werden.<br />    Überprüfen Sie die **Ereignisanzeige** unter dem Remotezugriffsserver-Vorgangskanal, der sich unter \Anwendungs- und Dienstprotokolle\Microsoft\Windows\RemoteAccess-RemoteAccessServer befindet.<br />    Überprüfen Sie den **VORGANGSSTATUS** in der Remotezugriffs-Verwaltungskonsole auf Fehler. Weitere Informationen finden Sie unter [Überwachen des Betriebsstatus des Remotezugriffsservers und dessen Komponenten](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md).|  
|Fehler|Die Konfiguration für Mehrfachstandortserver wurde vom Domänencontroller abgerufen. Einige Server besitzen abweichende Konfigurationen.|Zwischen den Konfigurationsversionen der Server-GPOs in der Bereitstellung mit mehreren Standorten besteht eine Inkonsistenz.<br /><br />Idealerweise weisen alle Server-GPOs für alle Einstiegspunkte die gleiche globale Konfiguration auf, aus etwaigen Gründen sind sie jedoch nicht synchron.|Das kann vorkommen, wenn durch eine Konfigurationsänderung ein Fehler auftritt und die Änderung nicht erfolgreich zurückgesetzt wird.<br /><br />Sie sollten die GPOs aus einem Sicherungsstatus wiederherstellen, in dem alle Server-GPOs synchronisiert wurden. Weitere Informationen zu einem Skript, das Sie verwenden können, finden Sie unter [sichern und Wiederherstellen der Remotezugriffkonfiguration](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6).|  
  


