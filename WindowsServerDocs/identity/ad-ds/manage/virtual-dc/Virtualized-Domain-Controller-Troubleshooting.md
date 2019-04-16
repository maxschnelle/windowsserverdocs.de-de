---
ms.assetid: 249ba1be-b0d3-4a77-99af-3699074a2b6e
title: Virtualisierte Domain Controller Troubleshooting
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 63f96e7a3035bc25f7a7a349acb6bf26f62a2a3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-troubleshooting"></a>Virtualisierte Domain Controller Troubleshooting

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält eine ausführliche Methode für die Problembehandlung bei der virtualisierten Domänencontroller-Funktion.  
  
-   [Problembehandlung für virtualisierte Klonen von Domänencontrollern](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootVDCCloning)  
  
-   [Problembehandlung bei der sichere Wiederherstellung des virtualisierten Domänencontrollers](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootVDCSafeRestore)  
  
## <a name="BKMK_Intro"></a>Einführung in  
Die wichtigste Methode zur Verbesserung Ihrer ist Build eines Testlabors und gründlich untersuchen normalen, funktionierenden Szenarien. Wenn Fehler auftreten, sind diese offensichtlicher und einfacher zu verstehen, da Sie dann ein solides Grundlagenwissen zur Funktionsweise des Heraufstufens. Dies ermöglicht es auch Ihre Analyse- und netzwerkanalysefertigkeiten. Dies gilt für alle verteilten Systeme Technologien, Bereitstellung nicht einfach virtualisierter Domänencontroller.  
  
Die wichtigen Elemente für die erweiterte Fehlerbehandlung bei der Konfiguration des Domänencontrollers sind:  
  
1.  Lineare Analyse in Kombination mit einer Fokussierung und Aufmerksamkeit für Details.  
  
2.  Verstehen der netzwerkerfassungsanalyse  
  
3.  Verstehen der integrierten Protokolle  
  
Die erste und zweite sind Gegenstand des in diesem Thema, aber der dritte kann ausführlich erläutert. Fehlerbehandlung bei virtualisierte Domänencontroller ist eine logische und lineare Methode erforderlich. Der Schlüssel ist das Problem mit den bereitgestellten Daten und nur auf komplexe Tools und Analysen zurückzugreifen, wenn Sie die bereitgestellte Ausgabe und Protokollierung erschöpft haben.  
  
## <a name="BKMK_TshootVDCCloning"></a>Problembehandlung für virtualisierte Klonen von Domänencontrollern  
In diesen Abschnitten behandelt:  
  
-   [Tools zur Problembehandlung](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_Tools)  
  
-   [Optionen für die Protokollierung](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_LoggingOptions)  
  
-   [Allgemeine Methode für die Problembehandlung beim Klonen des Domänencontrollers](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_GeneralMethodology)  
  
-   [Server Core und das Ereignisprotokoll](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_ServerCoreEvents)  
  
-   [Problembehandlung bei bestimmten Problemen](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_SpecificProblems)  
  
Die Problembehandlungsstrategie für das Klonen virtualisierter Domänencontroller folgenden allgemeinen Format:  
  
![Problembehandlung für virtuelle Domänencontroller](media/Virtualized-Domain-Controller-Troubleshooting/ADDS_VDC_TroublehsootingFlowchart.png)  
  
### <a name="BKMK_Tools"></a>Tools zur Problembehandlung  
  
#### <a name="BKMK_LoggingOptions"></a>Optionen für die Protokollierung  
Die integrierten Protokolle sind das wichtigste Tool für die Problembehandlung beim Klonen des Domänencontrollers. Alle diese Protokolle sind aktiviert und standardmäßig für maximale Ausführlichkeit konfiguriert.  
  
|||  
|-|-|  
|**Vorgang**|**Protokoll**|  
|**Das Klonen**|-Ereignis protokoll\system<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\verzeichnisdienst<br />-%systemroot%\debug\dcpromo.log|  
|**Werbung**|-%systemroot%\debug\dcpromo.log<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\verzeichnisdienst<br />-Ereignis protokoll\system<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dateireplikationsdienst<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dfs-Replikation|  
  
#### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Konfiguration des Domänencontrollers  
Verwenden Sie zum Beheben von Problemen, die nicht durch Protokolle erklärt werden die folgenden Tools als Ausgangspunkt verwendet:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   Netzwerkmonitor 3.4  
  
### <a name="BKMK_GeneralMethodology"></a>Allgemeine Methode für die Problembehandlung beim Klonen des Domänencontrollers  
  
1.  Wird die virtuelle Maschine in DS Repair Mode (DSRM) gestartet? Dies weist darauf hin, dass die Problembehandlung erforderlich ist. Verwenden Sie zum Anmelden im Verzeichnisdienst-Wiederherstellungsmodus, **. \Administrator** Konto, und geben Sie das DSRM-Kennwort.  
  
    1.  Überprüfen Sie die Datei Dcpromo.log.  
  
        1.  Erfolgreich erste Schritte beim Klonen, aber fehlgeschlagen Heraufstufen des Domänencontrollers?  
  
        2.  Weisen Fehler auf Probleme mit dem lokalen Domänencontroller oder mit der AD DS-Umgebung hin, z. B. Fehler vom PDC-Emulator zurückgegeben?  
  
    2.  Überprüfen Sie die System- und Verzeichnisdienst-Ereignisprotokolle und der dccloneconfig.xml und CustomDCCloneAllowList.xml  
  
        1.  Muss eine inkompatible Anwendung in der CustomDCCloneAllowList.xml Liste "zulassen"?  
  
        2.  Ist die IP-Adresse oder den Computer entweder dupliziert oder in der Datei dccloneconfig.xml ungültig?  
  
        3.  Ist der Active Directory-Standort in der Datei dccloneconfig.xml ungültig?  
  
        4.  Ist die IP-Adresse nicht in der dccloningconfig.xml festgelegt und kein DHCP-Server verfügbar ist?  
  
        5.  Ist der PDC-Emulator, online und über das RPC-Protokoll verfügbar?  
  
        6.  Ist der Domänencontroller Mitglied der Gruppe "Klonbare Domänencontroller"? Ist die Berechtigung **Domänencontroller die Erstellung eines Klons von sich selbst erlauben** am Domänenstamm für diese Gruppe festgelegt?  
  
        7.  Enthält die Datei Dccloneconfig.xml Syntaxfehler, die eine korrekte Analyse verhindern?  
  
        8.  Wird der Hypervisor unterstützt?  
  
        9. Haben Sie Heraufstufen des Domänencontrollers fehlgeschlagen, nachdem das Klonen erfolgreich begonnen hat?  
  
        10. Wurde die maximale Anzahl von automatisch generierten Domänencontrollernamen (9999) überschritten?  
  
        11. Dies ist die MAC-Adresse dupliziert?  
  
2.  Ist der Hostname des Klons identisch mit dem Quelldomänencontroller?  
  
    1.  Gibt es eine Dccloneconfig.xml-Datei in einem der zulässigen Speicherorte?  
  
3.  Ist die virtuellen Computer im normalen Modus gestartet und das Klonen abgeschlossen, aber funktioniert der Domänencontroller nicht ordnungsgemäß?  
  
    1.  Überprüfen Sie zunächst der Hostnamen auf dem Klon geändert wird. Wenn der Hostname unterscheidet, wurde das Klonen zumindest teilweise abgeschlossen.  
  
    2.  Ist der Domänencontroller eine doppelte IP-Adresse des Quell-Domänencontroller aus der Datei dccloneconfig.xml, sondern war der Quelldomänencontroller offline, während des Klonens?  
  
    3.  Wenn sich der Domänencontroller ankündigt, behandeln Sie das Problem wie alle normales Problem nach dem Heraufstufen, die Sie ohne das Klonen hätten.  
  
    4.  Wenn der Domänencontroller nicht ankündigt, untersuchen Sie die Verzeichnisdienst, System, Anwendung, Replikation und DFS-Replikation-Ereignisprotokolle auf Fehler nach dem Heraufstufen.  
  
#### <a name="disabling-dsrm-boot"></a>Deaktivieren des DSRM-Start  
Nach dem Starten im DSRM aufgrund eines Fehlers, diagnose der Ursache für Fehler und dcpromo.log ist kein Hinweis, dass der Klonvorgang nicht wiederholt werden kann, beheben Sie die Ursache für Fehler und Zurücksetzen die DSRM-Kennzeichen. Ein fehlerhafter Klon gibt allein beim nächsten Neustart nicht in den normalen Modus zurück. Sie müssen die DS-Wiederherstellungsmodus löschen, um das Klonen erneut versuchen. Alle diese Schritte müssen als Administrator mit erhöhten Rechten ausgeführt wird.  
  
##### <a name="removing-dsrm-with-msconfigexe"></a>Entfernen von DSRM mit Msconfig.exe  
Um das DSRM-Start über eine GUI zu aktivieren, verwenden Sie das Systemkonfigurationstool:  
  
1.  Führen Sie msconfig.exe  
  
2.  Auf der **Start** Registerkarte **Startoptionen**, heben Sie die **Abgesicherter Start** (mit der Option bereits ausgewählt **Active Directory-Reparatur** aktiviert)  
  
3.  Klicken Sie auf OK, und starten Sie bei entsprechender Aufforderung neu  
  
##### <a name="removing-dsrm-with-bcdeditexe"></a>Entfernen von DSRM mit Bcdedit.exe  
Um das DSRM-Start über die Befehlszeile zu deaktivieren, verwenden Sie die Startkonfigurationsdaten-Speicher Editor:  
  
1.  Öffnen Sie eine CMD-Eingabeaufforderung und ausführen:  
  
    ```  
    Bcdedit.exe /deletevalue safeboot  
    ```  
  
2.  Starten Sie den Computer mit neu:  
  
    ```  
    Shutdown.exe /t /0 /r  
    ```  
  
> [!NOTE]  
> Bcdedit.exe funktioniert auch in einer Windows PowerShell-Konsole. Die Befehle vorhanden sind:  
>   
> Bcdedit.exe/deletevalue safeboot  
>   
> Computer neu starten  
  
### <a name="BKMK_ServerCoreEvents"></a>Server Core und das Ereignisprotokoll  
Die Ereignisprotokolle enthalten einen Großteil der nützlichen Informationen zu Klonvorgängen für virtualisierte Domänencontroller. Standardmäßig ist eine Windows Server 2012-Computerinstallation eine Server Core-Installation, d. h., es ist keine grafische Benutzeroberfläche und daher keine Möglichkeit, den lokalen Ereignisanzeige-Snap-in ausführen.  
  
So überprüfen Sie die Ereignisprotokolle auf einem Server mit einer Server Core-installation  
  
-   Das Tool Wevtutil.exe lokal ausführen  
  
-   PowerShell-Cmdlet Get-WinEvent lokal ausführen  
  
-   Wenn Sie die Windows-Firewall erweiterte Regeln für die Gruppen "Remote-Ereignisprotokollverwaltung" (oder entsprechende Ports), um eingehende Kommunikation zuzulassen aktiviert haben, können Sie das Ereignisprotokoll Remote über Eventvwr.exe, wevtutil.exe oder Get-Winevent verwalten. Dies kann auf Server Core-Installation mit NETSH.exe, Gruppenrichtlinie oder mit dem neuen Set-NetFirewallRule-Cmdlet in Windows PowerShell 3.0 erfolgen.  
  
> [!WARNING]  
> Versuchen Sie nicht, die grafische Shell wieder auf den Computer hinzufügen, während es im Verzeichnisdienst-Wiederherstellungsmodus befindet. Windows-bereitstellungsstapel (CBS) kann nicht im abgesicherten Modus oder DSRM ordnungsgemäß funktioniert. Versuche, Features oder Rollen im DSRM hinzuzufügen werden nicht abgeschlossen, und lassen Sie den Computer in einem instabilen Zustand, bis er normal gestartet wird. Da ein virtualisierter domänencontrollerklon im Verzeichnisdienst-Wiederherstellungsmodus nicht normal gestartet werden kann und nicht normal werden in den meisten Fällen gestartet sollte ist es unmöglich, die grafische Shell auf sichere Weise hinzufügen. Auf diese Weise wird nicht unterstützt, und lassen Sie mit einem Server nicht mehr verwendet werden.  
  
### <a name="BKMK_SpecificProblems"></a>Problembehandlung bei bestimmten Problemen  
  
#### <a name="events"></a>Ereignisse  
Alle Ereignisse für die beim Klonen von virtualisierten Domänencontroller im Verzeichnisdienste-Ereignisprotokoll des geklonten Domänencontrollers VM schreiben. Die Ereignisprotokolle Anwendung, File Replication Service und DFS-Replikation möglicherweise auch nützliche Problembehandlungsinformationen für fehlgeschlagene Klonvorgänge enthalten. Fehler bei der RPC-Aufruf an den PDC-Emulator sind möglicherweise im Ereignisprotokoll auf dem PDC-Emulator verfügbar.  
  
Im folgenden sind die Windows Server 2012 Klonen-spezifische Ereignisse in das Verzeichnisdienst-Ereignisprotokoll mit Notizen und vorgeschlagenen Lösungen für Fehler.  
  
##### <a name="directory-services-event-log"></a>Verzeichnisdienst-Ereignisprotokoll  
  
|||  
|-|-|  
|**Ereignis-ID**|**2160**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Die lokale * <COMPUTERNAME> * ein virtuellen Domänencontrollers klonkonfigurationsdatei gefunden wurde.<br /><br />Klonkonfigurationsdatei für virtuelle Domänencontroller gefunden: %1<br /><br />Das Vorhandensein der virtuellen Domäne klonkonfigurationsdatei weist darauf hin, dass der lokale virtuelle Domänencontroller ein Klon eines anderen virtuellen Domänencontrollers ist. Die * <COMPUTERNAME> * zu klonen gestartet wird.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet. Untersuchen Sie das DSA-Arbeitsverzeichnis, % systemroot%\ntds und Stammverzeichnis alle lokalen oder Wechseldatenträgern Datenträger für die Datei dcclconeconfig.xml.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2161**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Die lokale * <COMPUTERNAME> * klonkonfigurationsdatei für virtuelle Domänencontroller wurde nicht gefunden. Der lokale Computer ist kein geklonter Domänencontroller.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet. Untersuchen Sie das DSA-Arbeitsverzeichnis, % systemroot%\ntds und Stammverzeichnis alle lokalen oder Wechseldatenträgern Datenträger für die Datei dcclconeconfig.xml.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2162**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Fehler beim Klonen des virtuellen Domänencontrollers.<br /><br />Überprüfen Sie in den Systemereignisprotokollen und Weitere Informationen zu Fehlern, die der virtuelle Domänencontroller entsprechen, %systemroot%\debug\dcpromo.log protokollierten Ereignisse.<br /><br />Fehlercode: %1|  
|**Hinweise und Lösungen**|Befolgen Sie die Anleitung Meldung, dieser Fehler ist ein "Catchall".|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2163**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|DsRoleSvc-Dienst wurde gestartet, um das Klonen des lokalen virtuellen Domänencontrollers.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet. Untersuchen Sie das DSA-Arbeitsverzeichnis, % systemroot%\ntds und Stammverzeichnis alle lokalen oder Wechseldatenträgern Datenträger für die Datei dcclconeconfig.xml.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2164**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Starten des DsRoleSvc-Diensts zum Klonen des lokalen virtuellen Domänencontrollers.|  
|**Hinweise und Lösungen**|Überprüfen Sie die diensteinstellungen für den DS-rollenserverdienst (DsRoleSvc), und stellen Sie sicher, dass sein Starttyp auf manuell festgelegt ist. Überprüfen Sie, dass kein Drittanbieterprogramm das Starten dieses Diensts verhindert wird.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2165**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Starten eines Threads, während das Klonen des lokalen virtuellen Domänencontrollers.<br /><br />Fehlercode: % 1<br /><br />Fehler Meldung: %2<br /><br />Thread: %3|  
|**Hinweise und Lösungen**|Wenden Sie sich an Microsoft Product Support|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2166**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*benötigt RPCSS-Dienst zum Initiieren eines Neustarts im Verzeichnisdienst-Wiederherstellungsmodus. Warten RPCSS in den ausgeführten Zustand konnte nicht initialisiert werden kann.<br /><br />Fehlercode: % 1|  
|**Hinweise und Lösungen**|Untersuchen Sie das Systemereignisprotokoll und die diensteinstellungen für den RPC-Serverdienst (Rpcss)|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2167**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Wissens zum virtuellen Domänencontroller konnte nicht initialisiert werden. Finden Sie unter vorherigen Eintrag im Ereignisprotokoll für Details.<br /><br />Zusätzliche Daten<br /><br />Fehler bei der Code: %1|  
|**Hinweise und Lösungen**|Befolgen Sie die Anleitung Meldung, dieser Fehler ist ein "Catchall".|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2168**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Microsoft-Windows-ActiveDirectory_DomainService<br /><br />Der Domänencontroller wird auf einem unterstützten Hypervisor ausgeführt. VM-Generations-ID wird erkannt.<br /><br />Aktuellen Wert der VM-Generations-ID: %1|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2169**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Es gibt keine VM-Generations-ID erkannt. Der Domänencontroller gehostet wird, auf einem physischen Computer, eine Vorgängerversion von Hyper-V oder ein Hypervisor, der die VM-Generation-ID nicht unterstützt<br /><br />Zusätzliche Daten<br /><br />Fehlercode beim Überprüfen der VM-Generations-ID: %1|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn kein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll und überprüfen Sie Hypervisor-Unterstützung Produktdokumentation zu.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2170**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Warnung|  
|**Nachricht**|Eine Änderung der Generations-ID wurde erkannt.<br /><br />In DS (Alter Wert) zwischengespeicherte Generations-ID: %1<br /><br />Generation-ID des virtuellen Computers (neuer Wert): %2<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. *<COMPUTERNAME>*erstellt eine neue Aufruf-ID zur Wiederherstellung des Domänencontrollers. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen der Inhalte einer Active Directory-Domänendienste-Datenbank ist zum Wiederherstellen einer systemstatussicherung, die mit einer sicherungsanwendung von Active Directory-Domänendienste.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn ein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2171**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Keine Änderung der Generations-ID wurde erkannt.<br /><br />In DS (Alter Wert) zwischengespeicherte Generations-ID: %1<br /><br />Generation-ID des virtuellen Computers (neuer Wert): %2|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn nicht ein Klonen beabsichtigt ist, und bei jedem Neustart eines virtualisierten Domänencontrollers angezeigt werden sollte. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2172**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Lesen Sie das MsDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers.<br /><br />MsDS-GenerationId-Attribut Wert: % 1|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn ein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2173**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Fehler beim Lesen des MsDS-GenerationId-Attributs des Computerobjekts des Domänencontrollers. Dies kann darauf zurückzuführen, dass Transaktion Datenbankfehler, oder die Generations-Id in der lokalen Datenbank nicht vorhanden. Das MsDS-GenerationId existiert nicht beim ersten Neustart nach Dcpromo oder der Domänencontroller keines virtuellen Domänencontrollers ist.<br /><br />Zusätzliche Daten<br /><br />Fehler bei der Code: %1|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn ein Klonen beabsichtigt ist, und es ist der erste VM-Neustart, nachdem das Klonen abgeschlossen wurde. Sie können auch auf nicht virtuellen Domänencontrollern ignoriert. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2174**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Der Domänencontroller ist weder ein virtuelles Klon noch eine wiederhergestellte Domänencontroller Momentaufnahme.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn kein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2175**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Klonkonfigurationsdatei für virtuelle Domänencontroller, die auf eine nicht unterstützte Plattform vorhanden ist.|  
|**Hinweise und Lösungen**|Dies tritt auf, wenn eine dccloneconfig.XML-Datei gefunden wird eine VM-Generations-ID wurde nicht gefunden, z. B. wenn eine dccloneconfig.xml-Datei gefunden wird, auf einem physischen Computer oder auf einem Hypervisor, der VM-Generations-ID nicht unterstützt|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2176**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Klonkonfigurationsdatei für virtuelle Domänencontroller wird umbenannt.<br /><br />Zusätzliche Daten<br /><br />Alte Datei: %1<br /><br />Neue Datei: %2|  
|**Hinweise und Lösungen**|Die Umbenennung ist erwartet beim Starten von einer Quelle VM gesichert werden, da die VM-Generations-ID nicht geändert hat. Dadurch wird verhindert, dass den Quelldomänencontroller einen Klonvorgang versucht.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2177**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Fehler beim Umbenennen der klonkonfigurationsdatei für virtuelle Domänencontroller.<br /><br />Zusätzliche Daten<br /><br />Datei: %1<br /><br />Fehler bei der Code: %2 %3|  
|**Hinweise und Lösungen**|Benennen Sie erwartet, wenn eine virtuelle Maschine sichern, Quellcomputers, da die VM-Generations-ID nicht geändert hat. Dadurch wird verhindert, dass den Quelldomänencontroller einen Klonvorgang versucht. Manuell benennen Sie die Datei, und untersuchen Sie installierte Drittanbieterprodukte, die Umbenennung der Datei verhindert werden können.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2178**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Klonkonfigurationsdatei für virtuelle Domänencontroller gefunden, aber die VM-Generations-ID nicht geändert wurde. Der lokale Domänencontroller ist der Quelldomänencontroller. Benennen Sie die Konfigurationsdatei zum Klonen.|  
|**Hinweise und Lösungen**|Wenn eine virtuelle Maschine sichern, Quellcomputers erwartet werden, da der VM-Generations-ID nicht geändert hat. Dadurch wird verhindert, dass den Quelldomänencontroller einen Klonvorgang versucht.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2179**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Das MsDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers wurde der folgende Parameter festgelegt:<br /><br />Generations-ID-Attribut: %1|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2180**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Warnung|  
|**Nachricht**|Fehler beim Festlegen der MsDS-GenerationId-Attributs des Computerobjekts des Domänencontrollers.<br /><br />Zusätzliche Daten<br /><br />Fehler bei der Code: %1|  
|**Hinweise und Lösungen**|Überprüfen Sie das Systemereignisprotokoll und die Datei Dcpromo.log. Suchen nach dem bestimmten Fehler in MS TechNet, MS-Knowledgebase und MS-Blogs, um seine gewöhnliche Bedeutung zu bestimmen und dann die Problembehandlung auf der Basis dieser Ergebnisse.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2182**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Internes Ereignis: der Verzeichnisdienst wurde aufgefordert, einen remote-DSA zu klonen:|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2183**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Internes Ereignis: * <COMPUTERNAME> * die Anforderung zum Klonen der remote Systems-Agent abgeschlossen.<br /><br />Ursprüngliche DC-Name: % 3<br /><br />Des angeforderten Sie Klon-DC: %4<br /><br />Des angeforderten Sie Klon-DC-Website: %5<br /><br />Zusätzliche Daten<br /><br />Fehler beim Wert: %1 %2|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2184**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Erstellen eines Domänencontrollerkontos für den geklonten Domänencontroller.<br /><br />Ursprünglichen DC: %1<br /><br />Zulässige Anzahl geklonter DCS: %2<br /><br />Die maximale Anzahl von DC-Konten, die durch Klonen generiert werden können * <COMPUTERNAME> *wurde überschritten.|  
|**Hinweise und Lösungen**|Ein einzelner Name des Quelldomänencontrollers kann nur automatisch 9.999-Mal generieren, wenn der Domänencontroller nicht herabgestuft werden basierend auf der Benennungskonvention. Verwenden der <computername> Element in der XML-Code, um einen neuen eindeutigen Namen oder der Klon von einem anders benannten Domänencontroller zu generieren.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2191**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*Legen Sie den folgenden Registrierungswert, DNS-Updates zu deaktivieren.<br /><br />Registrierung: %1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können. Der Klonvorgang wird DNS-Updates erneut aktivieren, nachdem das Klonen abgeschlossen ist.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2192**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Festlegen des folgenden Registrierungswerts zum Deaktivieren von DNS-Aktualisierungen.<br /><br />Registrierung: %1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Fehlercode: % 4<br /><br />Fehler Meldung: %5<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die möglicherweise registrierungsaktualisierungen blockieren.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2193**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*Legen Sie den folgenden Registrierungswert auf DNS-Updates zu aktivieren.<br /><br />Registrierung: %1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2194**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Festlegen des folgenden Registrierungswerts zum Aktivieren von DNS-Aktualisierungen.<br /><br />Registrierung: %1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Fehlercode: % 4<br /><br />Fehler Meldung: %5<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die möglicherweise registrierungsaktualisierungen blockieren.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2195**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Fehler beim Festlegen des DSRM-Starts.<br /><br />Fehlercode: % 1<br /><br />Fehler Meldung: %2<br /><br />Wenn Fehler beim Klonen des virtuellen Domänencontrollers oder klonkonfigurationsdatei für virtuelle Domänencontroller wird auf einem nicht unterstützten Hypervisor der lokale Computer für die Problembehandlung im DSRM neu gestartet wird. Fehler bei der Einstellung DSRM-Starts.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die möglicherweise registrierungsaktualisierungen blockieren.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2196**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Fehler beim Herunterfahren Berechtigung zu aktivieren.<br /><br />Fehlercode: % 1<br /><br />Fehler Meldung: %2<br /><br />Wenn Fehler beim Klonen des virtuellen Domänencontrollers oder klonkonfigurationsdatei für virtuelle Domänencontroller wird auf einem nicht unterstützten Hypervisor der lokale Computer für die Problembehandlung im DSRM neu gestartet wird. Fehler beim Herunterfahren Berechtigungen aktivieren.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die Verwendung von Berechtigungen blockiert werden kann.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2197**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Fehler beim Herunterfahren des Systems zu initiieren.<br /><br />Fehlercode: % 1<br /><br />Fehler Meldung: %2<br /><br />Wenn Fehler beim Klonen des virtuellen Domänencontrollers oder klonkonfigurationsdatei für virtuelle Domänencontroller wird auf einem nicht unterstützten Hypervisor der lokale Computer für die Problembehandlung im DSRM neu gestartet wird. Initiiert das Herunterfahren des Systems ist fehlgeschlagen.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die Verwendung von Berechtigungen blockiert werden kann.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2198**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Erstellen oder ändern das folgende geklonte Domänencontrollerobjekt.<br /><br />Zusätzliche Daten:<br /><br />Objekt:<br /><br />%1<br /><br />Fehlerwert: %2<br /><br />%3|  
|**Hinweise und Lösungen**|Suchen nach dem bestimmten Fehler in MS TechNet, MS-Knowledgebase und MS-Blogs, um seine gewöhnliche Bedeutung zu bestimmen und dann die Problembehandlung auf der Basis dieser Ergebnisse.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2199**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*konnte das folgende geklonte Domänencontrollerobjekt erstellen, da das Objekt bereits vorhanden ist.<br /><br />Zusätzliche Daten:<br /><br />Quelldomänencontroller:<br /><br />%1<br /><br />Objekt:<br /><br />%2|  
|**Hinweise und Lösungen**|Überprüfen Sie die Datei dccloneconfig.xml hat kein vorhandenen Domänencontrollers oder dass Kopien der Datei dccloneconfig.xml auf mehreren Klonen verwendet wurden, ohne den Namen zu bearbeiten. Wenn die Kollision immer noch unerwartet ist, bestimmen Sie, welcher Administrator sie heraufgestuft hat. Wenden Sie sich an diese erläutert werden, wenn der vorhandene Domänencontroller herabgestuft, Metadaten des vorhandenen Domänencontrollers bereinigt, oder wenn der Klon einen anderen Namen verwendet werden soll.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2203**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Fehler bei der letzten Klonen virtueller Domänencontroller. Dies ist der erste Neustart nach, und dies sollte daher sein, ein erneut das Klonen. Jedoch keine klonkonfigurationsdatei für virtuelle Domänencontroller vorhanden ist, und virtuelle Computer der Generation-ID Änderung erkannt wird. Start im DSRM gestartet.<br /><br />Fehler beim letzten Klonen virtueller Domänencontroller: %1<br /><br />Klonkonfigurationsdatei für virtuelle Domänencontroller vorhanden ist: %2<br /><br />Änderung der virtuellen Computer der Generation-ID wird erkannt: %3|  
|**Hinweise und Lösungen**|Erwartet, wenn das Klonen zuvor aufgrund von fehlenden oder ungültigen dccloneconfig.xml fehlgeschlagen.|  
  
|||  
|-|-|  
|Ereignis-ID|2210|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|<COMPUTERNAME> Fehler beim Erstellen von Objekten für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %6<br /><br />Name des geklonten Domänencontrollers: %1<br /><br />Wiederholungsschleife: %2<br /><br />Ausnahmewert: %3<br /><br />Fehlerwert: %4<br /><br />[DSID: %5|  
|Hinweise und Lösungen|Überprüfen Sie die System- und Verzeichnisdienst-Ereignisprotokolle und die dcpromo.log auf Weitere Details für die Klonens.|  
  
|||  
|-|-|  
|Ereignis-ID|2211|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> Objekte für den geklonten Domänencontroller erstellt.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %3<br /><br />Name des geklonten Domänencontrollers: %1<br /><br />Wiederholungsschleife: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2212|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> Schritte zum Erstellen von Objekten für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Klonname: %2<br /><br />Klonsite: %3<br /><br />Geklonter RODC: %4|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2213|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt ein neues KrbTgt-Objekt für das Read-Only Domain Controller cloning.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Guid des neuen KrbTgt-Objekts: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2214|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt ein Computerobjekt für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Ursprünglicher Domänencontroller: %2<br /><br />Geklonter Domänencontroller: %3|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2215|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> den geklonte Domänencontroller wird in der folgenden Website hinzugefügt werden.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Standort: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2216|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt einen Servercontainer für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Servercontainer: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2217|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt ein Serverobjekt für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Serverobjekt: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2218|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt ein NTDS-Einstellungsobjekt für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Objekt: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2219|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt Verbindungsobjekte für den geklonten schreibgeschützten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2220|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> erstellt SYSVOL-Objekte für den geklonten schreibgeschützten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2221|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|<COMPUTERNAME> Fehler beim Generieren eines zufälligen Kennworts für den geklonten Domänencontroller.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Name des geklonten Domänencontrollers: %2<br /><br />Fehler: %3 %4|  
|Hinweise und Lösungen|Überprüfen Sie das Systemereignisprotokoll Detailinformationen zu, warum das Computerkontokennwort nicht erstellt werden konnte.|  
  
|||  
|-|-|  
|Ereignis-ID|2222|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|<COMPUTERNAME> Fehler beim Kennwort für den geklonten Domänencontroller festlegen.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Name des geklonten Domänencontrollers: %2<br /><br />Fehler: %3 %4|  
|Hinweise und Lösungen|Überprüfen Sie das Systemereignisprotokoll Detailinformationen zu, warum das Computerkontokennwort nicht festgelegt werden konnte.|  
  
|||  
|-|-|  
|Ereignis-ID|2223|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|<COMPUTERNAME> Kennwort für das Computerkonto für den geklonten Domänencontroller erfolgreich festgelegt.<br /><br />Zusätzliche Daten:<br /><br />Klon-Id: %1<br /><br />Name des geklonten Domänencontrollers: %2<br /><br />Gesamtanzahl der Wiederholungen: %3|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2224|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|Fehler beim Klonen des virtuellen Domänencontrollers. Die folgenden %1 verwalteten Dienstkonten, die auf dem geklonten Computer vorhanden sind:<br /><br />%2<br /><br />Für das Klonen erfolgreich ist, müssen alle verwalteten Dienstkonten entfernt werden. Dies kann mit dem Remove-ADComputerServiceAccount PowerShell-Cmdlet.|  
|Hinweise und Lösungen|Erwartet bei der Verwendung von eigenständigen MSAs (nicht bei Gruppen-MSA). Führen Sie *nicht* folgen Sie den ereignisratschlag, das Konto entfernen – sie ist falsch geschrieben. Verwenden Sie Uninstall-AdServiceAccount – [https://technet.microsoft.com/library/hh852310](https://technet.microsoft.com/library/hh852310).<br /><br />Eigenständige MSAs zuerst in Windows Server 2008 R2 - wurden in Windows Server 2012 durch Gruppen-MSAs (gMSA) ersetzt. Gmsas bieten Unterstützung für das Klonen.|  
  
|||  
|-|-|  
|Ereignis-ID|2225|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Information|  
|Nachricht|Die zwischengespeicherten geheimen Schlüsseln des folgenden Sicherheitsprinzipals wurden erfolgreich vom lokalen Domänencontroller entfernt:<br /><br />%1<br /><br />Nach dem Klonen eines schreibgeschützten Domänencontrollers, werden geheime Schlüssel, die zuvor auf dem Klonen schreibgeschützten Domänencontroller zwischengespeichert wurden auf dem geklonten Domänencontroller entfernt.|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|2226|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|Fehler bei der zwischengespeicherte geheimen Schlüsseln des folgenden Sicherheitsprinzipals vom lokalen Domänencontroller zu entfernen:<br /><br />%1<br /><br />Fehler: %2 (%3)<br /><br />Nach dem Klonen eines schreibgeschützten Domänencontrollers, geheime Schlüssel, die zuvor zwischengespeichert wurden, auf das Klonen Quelle schreibgeschützten Domänencontroller müssen auf dem Klon entfernt werden, um das Risiko zu verringern, dass ein Angreifer die Anmeldeinformationen von gestohlenen oder kompromittierten Klon erhalten kann. Wenn das Sicherheitsprinzipal ein Konto und geschützt werden sollten, verwenden Sie RootDSE-Vorgang "rodcpurgeaccount" um die geheimen Schlüssel auf dem lokalen Domänencontroller manuell zu löschen.|  
|Hinweise und Lösungen|Überprüfen Sie die System- und Verzeichnisdienst-Ereignisprotokolle auf Weitere Informationen.|  
  
|||  
|-|-|  
|Ereignis-ID|2227|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|Ausnahme beim Versuch, zwischengespeicherte geheime Schlüssel vom lokalen Domänencontroller zu entfernen.<br /><br />Zusätzliche Daten:<br /><br />Ausnahmewert: %1<br /><br />Fehlerwert: %2<br /><br />[DSID: %3<br /><br />Nach dem Klonen eines schreibgeschützten Domänencontrollers, geheime Schlüssel, die zuvor zwischengespeichert wurden, auf das Klonen Quelle schreibgeschützten Domänencontroller müssen auf dem Klon entfernt werden, um das Risiko zu verringern, dass ein Angreifer die Anmeldeinformationen von gestohlenen oder kompromittierten Klon erhalten kann. Wenn einer dieser Sicherheitsprinzipale ein Konto ist sollten geschützt werden, verwenden Sie RootDSE-Vorgang "rodcpurgeaccount" um die geheimen Schlüssel auf dem lokalen Domänencontroller manuell zu löschen.|  
|Hinweise und Lösungen|Überprüfen Sie die System- und Verzeichnisdienst-Ereignisprotokolle auf Weitere Informationen.|  
  
|||  
|-|-|  
|Ereignis-ID|2228|  
|Quelle|Microsoft-Windows-ActiveDirectory_DomainService|  
|Schweregrad|Fehler|  
|Nachricht|Die ID des virtuellen Computers der Generation in Active Directory-Datenbank dieses Domänencontrollers unterscheidet sich von den aktuellen Wert dieses virtuellen Computers. Ein virtueller Domänencontroller klonkonfigurationsdatei (DCCloneConfig.xml) konnte jedoch nicht gefunden werden, damit das Klonen eines Domänencontrollers nicht geklont wurde. Wenn Sie ein Domänencontroller Klonen Vorgang vorgesehen war, stellen Sie sicher, dass eine dccloneconfig.XML-Datei in einem der unterstützten Speicherorte bereitgestellt wird. Darüber hinaus steht die IP-Adresse dieses Domänencontrollers mit IP-Adresse von einem anderen Domänencontroller in Konflikt. Um sicherzustellen, dass keine Unterbrechungen im Dienst auftreten, der Domänencontroller konfiguriert wurde für den Start im DSRM gestartet.<br /><br />Zusätzliche Daten:<br /><br />Doppelte IP-Adresse: %1|  
|Hinweise und Lösungen|Dieser Schutzmechanismus beendet doppelte Domänencontroller, wenn möglich (nicht bei der Verwendung von DHCP, z. B.). Fügen Sie eine gültige DcCloneConfig.xml-Datei hinzu, entfernen Sie die DSRM-Kennzeichen und versuchen Sie erneut das Klonen|  
  
|||  
|-|-|  
|Ereignis-ID|29218|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Fehler beim Klonen des virtuellen Domänencontrollers. Der Klonvorgang konnte nicht abgeschlossen werden, und der geklonten Domänencontroller in Directory Services-Wiederherstellungsmodus (DSRM) neu gestartet wurde.<br /><br />Kontrollkästchen zuvor protokolliert Ereignisse und %systemroot%\debug\dcpromo.log für Weitere Informationen zu Fehlern, finden Sie auf den virtuellen Domänencontroller schlägt der Klonvorgang versucht und davon, ob dieses klonimage wiederverwendet werden kann.<br /><br />Wenn mindestens ein Protokolleintrag darauf hinweist, dass der Klonvorgang nicht wiederholt werden kann, muss das Image auf sichere Art zerstört werden. Andernfalls können Sie die Fehler beheben, die DSRM-Startkennzeichen löschen und normal neu starten; nach dem Neustart wird der Klonvorgang wiederholt.|  
|Hinweise und Lösungen|Überprüfen Sie die System- und Verzeichnisdienst-Ereignisprotokolle und die dcpromo.log auf Weitere Details für die Klonens.|  
  
|||  
|-|-|  
|Ereignis-ID|29219|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Information|  
|Nachricht|Klonen virtueller Domänencontroller wurde erfolgreich abgeschlossen.|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet.|  
  
|||  
|-|-|  
|Ereignis-ID|29248|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Fehler beim Klonen virtueller Domänencontroller Winlogon-Benachrichtigung erhalten. Der zurückgegebene Fehlercode ist %1 (%2).<br /><br />Weitere Informationen zu diesem Fehler finden Sie in %systemroot%\debug\dcpromo.log Fehler, die der virtuelle Domänencontroller entsprechen.|  
|Hinweise und Lösungen|Wenden Sie sich an Microsoft Product Support|  
  
|||  
|-|-|  
|Ereignis-ID|29249|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Klonen virtueller Domänencontroller konnte nicht analysiert werden Konfigurationsdatei des virtuellen Domänencontrollers.<br /><br />Die zurückgegebene HRESULT-Code ist %1.<br /><br />Die Konfigurationsdatei ist: %2<br /><br />Beheben Sie die Fehler in der Konfigurationsdatei, und wiederholen Sie den Klonvorgang.<br /><br />Weitere Informationen zu diesem Fehler finden Sie unter % systemroot%\debug\dcpromo.log.|  
|Hinweise und Lösungen|Überprüfen Sie die Datei dclconeconfig.XML mithilfe eines XML-Editors und die DCCloneConfigSchema.xsd-Schemadatei.|  
  
|||  
|-|-|  
|Ereignis-ID|29250|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Fehler beim Klonen des virtuellen Domänencontrollers. Es gibt Software oder Dienste, die derzeit auf dem geklonten virtuellen Domänencontroller aktiviert, die sind nicht in der Liste zulässiger Anwendungen für das Klonen virtueller Domänencontroller vorhanden.<br /><br />Im folgenden sind die Einträge fehlen:<br /><br />%2<br /><br />%1 (falls vorhanden) wurde als definierte Aufnahmeliste verwendet.<br /><br />Der Klonvorgang kann nicht abgeschlossen werden, wenn nicht Klonbare Anwendungen installiert sind.<br /><br />Bitte führen Sie Active Directory PowerShell-Cmdlet Get-ADDCCloningExcludedApplicationList um zu überprüfen, welche Anwendungen auf dem geklonten Computer installiert, aber nicht in der Zulassungsliste enthalten, und fügen sie die Liste "zulassen" hinzu, wenn sie mit Klonen des virtuellen Domänencontrollers kompatibel sind. Wenn diese Anwendungen nicht mit Klonen des virtuellen Domänencontrollers kompatibel sind, deinstallieren sie vor dem erneuten Versuch der Klonvorgang.<br /><br />Prozess für das Klonen für virtuelle Domänencontroller sucht für die Anwendung zulässige Listendatei CustomDCCloneAllowList.xml, basierend auf der folgenden Reihenfolge. die zuerst gefundene Datei wird verwendet, und alle anderen werden ignoriert:<br /><br />1. der Name des Registrierungswerts: HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters\AllowListFolder<br /><br />2. dasselbe Verzeichnis, in dem der Ordner des DSA-Arbeitsverzeichnis befindet<br /><br />3. %windir%\NTDS<br /><br />4. Wechselmedien Schreib-Lese-Medien in der Reihenfolge des Laufwerkbuchstabens, im Stammverzeichnis des Laufwerks|  
|Hinweise und Lösungen|Führen Sie die Anweisungen in der Meldung|  
  
|||  
|-|-|  
|Ereignis-ID|29251|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Klonen virtueller Domänencontroller konnte die IP-Adressen des geklonten Computers zurücksetzen.<br /><br />Der zurückgegebene Fehlercode ist %1 (%2).<br /><br />Dieser Fehler kann durch die Fehlkonfiguration im Netzwerk Konfigurationsabschnitte in der Konfigurationsdatei der virtuellen Domänencontrollers verursacht werden.<br /><br />Finden Sie in %systemroot%\debug\dcpromo.log für Weitere Informationen zu Fehlern, die beim Klonen eines virtuellen Domänencontrollers zurücksetzen IP-Adressen entsprechen.<br /><br />Informationen zum Zurücksetzen von IP-Adressen auf dem geklonten Computer finden Sie unter https://go.microsoft.com/fwlink/?LinkId=208030|  
|Hinweise und Lösungen|Überprüfen Sie die IP-Informationen in der Datei dccloneconfig.xml gültig ist und die ursprünglichen Quellcomputer nicht duplizieren.|  
  
|||  
|-|-|  
|Ereignis-ID|29253|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Fehler beim Klonen des virtuellen Domänencontrollers. Der geklonte Domänencontroller konnte den Betriebsmaster des primären Domänencontrollers (PDC) in den geklonten Computer Ursprungsdomäne des geklonten Computers finden.<br /><br />Der zurückgegebene Fehlercode ist %1 (%2).<br /><br />Stellen Sie sicher, dass der primäre Domänencontroller in der Ursprungsdomäne des geklonten Computers einem aktiven Domänencontroller zugeordnet ist, online ist und betriebsbereit ist. Stellen Sie sicher, dass der geklonte Computer über die erforderlichen Ports und Protokolle LDAP/RPC-Verbindung mit dem primären Domänencontroller hat.|  
|Hinweise und Lösungen|Überprüfen die geklonten Domänencontroller IP-Adresse und DNS-Informationen festgelegt ist. Verwenden Sie Dcdiag.exe locatorcheck überprüfen, ob der PDCE online ist, verwenden Sie Nltest.exe/Server:* <PDCE> * /DcList:* <domain> * für den gültigen RPC, erhalten Sie eine netzwerkerfassung vom PDCE während das Klonen fehlschlägt, und analysieren Sie den Datenverkehr.|  
  
|||  
|-|-|  
|Ereignis-ID|29254|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Klonen virtueller Domänencontroller konnte nicht an den primären Domänencontroller %1 zu binden.<br /><br />Der zurückgegebene Fehlercode ist %2 (%3).<br /><br />Stellen Sie sicher, dass der primäre Domänencontroller %1 Online und betriebsbereit ist. Stellen Sie sicher, dass der geklonte Computer über die erforderlichen Ports und Protokolle LDAP/RPC-Verbindung mit dem primären Domänencontroller hat.|  
|Hinweise und Lösungen|Überprüfen die geklonten Domänencontroller IP-Adresse und DNS-Informationen festgelegt ist. Verwenden Sie Dcdiag.exe locatorcheck überprüfen, ob der PDCE online ist, verwenden Sie Nltest.exe/Server:* <PDCE> * /DcList:* <domain> * für den gültigen RPC, erhalten Sie eine netzwerkerfassung vom PDCE während das Klonen fehlschlägt, und analysieren Sie den Datenverkehr.|  
  
|||  
|-|-|  
|Ereignis-ID|29255|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Fehler beim Klonen des virtuellen Domänencontrollers.<br /><br />Fehler %2 (%3) beim Versuch zum Erstellen von Objekten auf dem primären Domänencontroller %1 für das Bild geklonten erforderlich.<br /><br />Stellen Sie sicher, dass der geklonte Domänencontroller Privileg zu klonen. Überprüfen Sie nach verwandten Ereignissen im Verzeichnisdienst-Ereignisprotokoll auf dem primären Domänencontroller %1.|  
|Hinweise und Lösungen|Suchen nach dem bestimmten Fehler in MS TechNet, MS-Knowledgebase und MS-Blogs, um seine typische Bedeutung zu bestimmen und dann die Problembehandlung auf der Basis dieser Ergebnisse.|  
  
|||  
|-|-|  
|Ereignis-ID|29256|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Versuch, den Start in den Modus "Verzeichnisdienste wiederherstellen" Flag festgelegt Fehler mit Fehlercode: %1.<br /><br />Finden Sie weitere Informationen zu Fehlern %systemroot%\debug\dcpromo.log.|  
|Hinweise und Lösungen|Überprüfen Sie das Verzeichnisdienstprotokoll und dcpromo.log auf Details. Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die Verwendung von Berechtigungen blockiert werden kann.|  
  
|||  
|-|-|  
|Ereignis-ID|29257|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Klonen virtueller Domänencontroller vorgenommen hat. Versuch, den Computer neu starten, Fehler mit Fehlercode: %1.<br /><br />Starten Sie den Computer, um den Klonvorgang abgeschlossen neu.|  
|Hinweise und Lösungen|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die Verwendung von Berechtigungen blockiert werden kann.|  
  
|||  
|-|-|  
|Ereignis-ID|29264|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|So löschen Sie den Start in den Modus "Verzeichnisdienste wiederherstellen" Flag fehlgeschlagen mit Fehlercode: %1.<br /><br />Finden Sie weitere Informationen zu Fehlern %systemroot%\debug\dcpromo.log.|  
|Hinweise und Lösungen|Überprüfen Sie das Verzeichnisdienstprotokoll und dcpromo.log auf Details. Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die Verwendung von Berechtigungen blockiert werden kann.|  
  
|||  
|-|-|  
|Ereignis-ID|29265|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Information|  
|Nachricht|Klonen virtueller Domänencontroller wurde erfolgreich abgeschlossen. Der virtuelle Domänencontroller klonkonfigurationsdatei %1 wurde in %2 umbenannt.|  
|Hinweise und Lösungen|Nicht zutreffend, ist dies ein Erfolgsereignis.|  
  
|||  
|-|-|  
|Ereignis-ID|29266|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Klonen virtueller Domänencontroller wurde erfolgreich abgeschlossen. Der Versuch, das Umbenennen von virtuellen Domänencontrollern klonkonfigurationsdatei %1 konnte nicht mit Fehlercode: %2 (%3).|  
|Hinweise und Lösungen|Benennen Sie die Datei dccloneconfig.xml manuell um.|  
  
|||  
|-|-|  
|Ereignis-ID|29267|  
|Quelle|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Schweregrad|Fehler|  
|Nachricht|Klonen virtueller Domänencontroller konnte nicht überprüft, ob das Klonen des virtuellen Domänencontrollers Anwendungsliste zugelassen.<br /><br />Der zurückgegebene Fehlercode ist %1 (%2).<br /><br />Dieser Fehler kann verursacht werden durch einen Syntaxfehler können Fehler in der Klon-Datei (die Datei derzeit überprüfte ist: %3). Weitere Informationen zu diesem Fehler finden Sie unter % systemroot%\debug\dcpromo.log.|  
|Hinweise und Lösungen|Führen Sie die Anweisungen im Ereignis.|  
  
##### <a name="error-messages"></a>Fehlermeldungen  
Es gibt keine direkten interaktiven Fehler für fehlgeschlagene Klonen virtualisierter Domänencontroller. Alle kloninformationen werden in den System- und verzeichnisdienstprotokollen und heraufstufung von Domänencontrollern in dcpromo.log protokolliert. Jedoch, wenn der Server im DS-Wiederherstellungsmodus gestartet wird, sollten Sie sofort untersuchen Sie heraufstufen oder Klonen fehlgeschlagen ist.  
  
Die Datei dcpromo.log ist der erste Schritt bei klonfehlern überprüfen sollten. Je nach dem Fehler aufgeführt kann es erforderlich, um die Verzeichnisdienst- und Systemprotokolle für eine weitere Diagnose später zu lesen sein.  
  
#### <a name="known-issues-and-support-scenarios"></a>Bekannte Probleme und Supportszenarien  
Die folgende Liste gängiger Probleme während der Entwicklung von Windows Server 2012. All diese Probleme sind "beabsichtigt" und eine gültige problemumgehung oder eine geeignetere Methode in erster Linie vermeiden. Einige kann in späteren Versionen von Windows Server 2012 behoben werden.  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, DSRM**|  
|**Symptome**|Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet|  
|**Lösung und Hinweise**|Überprüfen Sie alle Schritte gefolgt von Abschnitten bereitstellen virtualisierter Domänencontrollers Abschnitt und [allgemeine Methodik zur Problembehandlung für das Klonen eines Domänencontrollers](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_GeneralMethodology)<br /><br />Beschrieben in KB 2742844.|  
  
|||  
|-|-|  
|**Problem**|**Zusätzliche IP-Leases bei Verwendung von DHCP zum Klonen**|  
|**Symptome**|Nach dem erfolgreichen Klonen eines Domänencontrollers, und mithilfe von DHCP übernimmt der erste Start des Klons eine DHCP-Lease. Wenn der Server umbenannt und als Domänencontroller neu gestartet, dauert es dann eine zweite DHCP-Lease. Die erste IP-Adresse ist nicht freigegeben, und am Ende einer "phantom"-Leases|  
|**Lösung und Hinweise**|Manuell löschen Sie die ungenutzte Adresslease in DHCP, oder lassen sie Sie normal ablaufen. Beschrieben in KB 2742836.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen im DSRM nach sehr langer Verzögerung**|  
|**Symptome**|Das Klonen scheint bei anhalten "Klonen des Domänencontrollers ist zu X% % abgebrochen" für 8 bis 15 Minuten. Danach das Klonen schlägt fehl und wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet.|  
|**Lösung und Hinweise**|Der geklonte Computer eine dynamische IP-Adresse von DHCP oder SLAAC, kann nicht abgerufen werden oder verwendet eine doppelte IP-Adresse oder der primäre Domänencontroller kann nicht gefunden werden. Mehrere vom Klonvorgang Wiederholungsversuche dazu führen, dass die Verzögerung. Beheben Sie das Netzwerkproblem, um das Klonen zuzulassen.<br /><br />Beschrieben in KB 2742844.|  
  
|||  
|-|-|  
|**Problem**|**Das Klonen wird nicht alle Dienstprinzipalnamen neu erstellt**|  
|**Symptome**|Wenn ein Satz von *dreiteiligen* Dienstprinzipalnamen (SPN) enthält sowohl einen NetBIOS-Namen mit einem Port als auch einen ansonsten identischen NetBIOS-Namen ohne einen Port, der Eintrag ohne Port wird nicht mit dem neuen Computernamen neu erstellt. Zum Beispiel:<br /><br />Customspn / DC1: 200 / app1 ungültige Invalid USE OF *wird mit dem neuen Computernamen neu erstellt*<br /><br />Customspn/DC1/app1 Ungültige Verwendung von Symbolen *wird nicht mit dem neuen Computernamen neu erstellt*<br /><br />Vollqualifizierte Namen und SPNs ohne drei Teile werden neu erstellt, unabhängig von Ports. Beispielsweise werden diese erfolgreich auf dem Klon neu erstellt:<br /><br />Customspn / DC1: 202 Invalid USE OF *wird neu erstellt*<br /><br />Customspn/DC1 Invalid ungültige USE OF *wird neu erstellt*<br /><br />customspn/DC1.corp.contoso.com:202 Ungültige Verwendung von Symbolen *wird neu erstellt Namen*<br /><br />customspn/DC1.corp.contoso.com Ungültige Verwendung von Symbolen *wird neu erstellt*|  
|**Lösung und Hinweise**|Dies ist eine Einschränkung der umbenennen Prozess für den Domänencontroller in Windows, nicht nur beim Klonen. Dreiteilige SPNS werden von der benennungslogik in jedem Szenario nicht behandelt. Die meisten Windows enthaltenen Dienste sind betroffen, da sie alle fehlenden SPNs nach Bedarf neu erstellen. Andere Programme erfordern manuelle Eingabe des SPN, um das Problem zu beheben.<br /><br />Beschrieben in KB 2742874.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, Start im DSRM, allgemeine Netzwerkfehler**|  
|**Symptome**|Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet. Es sind allgemeine Netzwerkfehler.|  
|Lösung und Hinweise|Stellen Sie sicher, dass der neue Klon keine doppelte statische MAC-Adresse vom Quelldomänencontroller zugewiesen verfügt; Sie können sehen, wenn ein virtueller Computer statische MAC-Adressen verwendet, durch Ausführen dieses Befehls auf dem hypervisorhost für den Quell- und den geklonten virtuellen Computer:<br /><br />Get-VM - VMName *Test-Vm* & #124; Get-VMNetworkAdapter & #124; fl *<br /><br />Ändern Sie die MAC-Adresse in eine eindeutige statische Adresse, oder wechseln Sie zur Verwendung von dynamischer MAC-Adressen.<br /><br />Beschrieben in KB 2742844.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, Start im DSRM als Duplikat des Quelldomänencontrollers**|  
|**Symptome**|Ein neuer Klon wird ohne Klonen gestartet. Die Datei dccloneconfig.xml wird nicht umbenannt, und der Server startet im DS-Wiederherstellungsmodus. Das Verzeichnisdienst-Ereignisprotokoll zeigt Fehler 2164<br /><br />*<COMPUTERNAME>*Fehler beim Starten des DsRoleSvc-Diensts zum Klonen des lokalen virtuellen Domänencontrollers.|  
|**Lösung und Hinweise**|Überprüfen Sie die diensteinstellungen für den DS-rollenserverdienst (DsRoleSvc), und stellen Sie sicher, dass sein Starttyp auf manuell festgelegt ist. Überprüfen Sie, dass kein Drittanbieterprogramm das Starten dieses Diensts verhindert wird.<br /><br />Weitere Informationen dazu, wie Sie diesen sekundären Domänencontroller freigeben und gleichzeitig sicherstellen, dass Updates ausgehend repliziert werden finden Sie im Microsoft KB-Artikel 2742970.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, Start im DSRM, Fehler 8610**|  
|**Symptome**|Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet. Dcpromo .log wird Fehler 8610 angezeigt (das heißt ERROR_DS_ROLE_NOT_VERIFIED 8610 oder 0x21A2 ist)|  
|**Lösung und Hinweise**|Geschieht, wenn der PDC sichtbar sein kann, aber es wurde keine ausreichende Replikation selbst, um die Rolle zulassen durchgeführt. Wenn z. B. das Klonen gestartet und ein anderer Administrator die Rolle PDCE FSMO zu einem neuen Domänencontroller verschiebt.<br /><br />Beschrieben in KB 2742916.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, Start im DSRM, allgemeine Netzwerkfehler**|  
|**Symptome**|Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet. Es sind allgemeine Netzwerkfehler.|  
|**Lösung und Hinweise**|Stellen Sie sicher, dass der neue Klon keine doppelte statische MAC-Adresse vom Quelldomänencontroller zugewiesen verfügt; Sie können sehen, wenn ein virtueller Computer statische MAC-Adressen verwendet, durch Ausführen dieses Befehls auf dem Hyper-V-Host für die Quell- und den geklonten virtuellen Computer:<br /><br />Get-VM - VMName *Test-Vm* & #124; Get-VMNetworkAdapter & #124; fl *<br /><br />Ändern Sie die MAC-Adresse in eine eindeutige statische Adresse, oder wechseln Sie zur Verwendung von dynamischer MAC-Adressen.<br /><br />Beschrieben in KB 2742844.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, Start im DSRM**|  
|**Symptome**|Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet|  
|**Lösung und Hinweise**|Stellen Sie sicher, dass die Datei dccloneconfig.xml die Schemadefinition enthält (Siehe sampledccloneconfig.xml, Zeile 2):<br /><br />**< D3c:DCCloneConfig xmlns:d3c="uri:microsoft.com:schemas:DCCloneConfig" >**<br /><br />Beschrieben in KB 2742844.|  
  
|||  
|-|-|  
|Problem|**Keine Anmeldeserver verfügbar, fehlerprotokollierung im DSRM**|  
|**Symptome**|Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet. Sie versuchen, sich anmelden, und die Fehlermeldung:<br /><br />**Es sind zurzeit keine Anmeldeserver verfügbar, um die anmeldeanforderung zu warten**|  
|**Lösung und Hinweise**|Stellen Sie sicher, dass Sie mit dem DSRM-Administratorkonto und nicht das Domänenkonto anmelden. Verwenden Sie den Pfeil nach links, und geben Sie einen Benutzernamen:<br /><br />**. \administrator**<br /><br />Beschrieben in KB 2742908.|  
  
|||  
|-|-|  
|**Problem**|**Klonquelle schlägt fehl und im DSRM, Fehler**|  
|**Symptome**|Während des Klonens ist, tritt ein Fehler 8437 "Erstellen von domänencontrollerobjekten auf PDC" (0x20f5)|  
|**Lösung und Hinweise**|Doppelter Computername wurde in DCCloneConfig.xml als Quelle Domänencontroller oder ein vorhandener Domänencontroller festgelegt. Der Computername muss außerdem in den NetBIOS-Namensformat Computer (maximal 15 Zeichen, kein FQDN) sein.<br /><br />Beheben Sie die Datei dccloneconfig.xml, indem Sie einen eindeutigen, gültigen Namen festlegen.<br /><br />Beschrieben in KB 2742959.|  
  
|||  
|-|-|  
|**Problem**|**Neue Addccloneconfigfile-Fehler "Index lag außerhalb des zulässigen Bereichs"**|  
|**Symptome**|Wenn Sie die Cmdlets new-Addccloneconfigfile ausführen, erhalten Sie Fehler:<br /><br />Index lag außerhalb des zulässigen Bereichs. Muss nicht negativ und kleiner als die Größe der Sammlung sein.|  
|**Lösung und Hinweise**|Sie müssen das Cmdlet in einer Windows PowerShell-Konsole mit Administratorrechten ausführen. Dieser Fehler wird durch mangelnden Mitglied der lokalen Administratorengruppe auf dem Computer verursacht.<br /><br />Beschrieben in KB 2742927.|  
  
|||  
|-|-|  
|**Problem**|**Fehler beim Klonen, doppelter Domänencontroller**|  
|**Symptome**|Der Klon wird ohne klonen, dupliziert vorhandenen Domänencontroller gestartet.|  
|**Lösung und Hinweise**|Der Computer kopiert wurde gestartet, aber enthält keine DcCloneConfig.xml-Datei an einem der unterstützten Speicherorte und verfügt nicht über eine doppelte IP-Adresse mit dem Quelldomänencontroller. Der Domänencontroller muss ordnungsgemäß entfernt werden, um Datenverluste zu vermeiden.<br /><br />Beschrieben in KB 2742970.|  
  
|||  
|-|-|  
|**Problem**|**New-ADDCCloneConfigFile schlägt mit der Server ist nicht betriebsbereit Fehler bei der Überprüfung der Quelldomänencontroller ein Mitglied der Klonbare Domänencontroller Domänengruppe ist, wenn kein globaler Katalogserver nicht verfügbar ist.**|  
|**Symptome**|Beim Ausführen von New-ADDCCloneConfigFile zum Erstellen einer dccloneconfig.xml-Datei wird Fehler:<br /><br />Code - der Server ist nicht betriebsbereit|  
|**Lösung und Hinweise**|Überprüfen Sie die Verbindung mit einem globalen Katalogserver von dem Server, in dem Sie New-ADDCCloneConfigFile ausführen, und stellen Sie sicher, dass die Mitgliedschaft in der Quell-Domänencontroller in der Gruppe "Klonbare Domänencontroller" an diesen globalen Katalogserver repliziert wurde.<br /><br />Führen Sie den folgenden Befehl als Mittel leeren des Cache des DC-Locator für Fälle, in denen ein globaler Katalogserver oder ein Domänencontroller kürzlich offline geschaltet wurde haben kann:<br /><br />Code - Nltest/dsgetdc: / gc/force|  
  
### <a name="advanced-troubleshooting"></a>Erweiterte Problembehandlung  
Dieses Modul sucht, um erweiterte Fehlerbehandlung mit *arbeiten* Protokolle als Beispiele mit einer Erklärung der Vorgänge. Wenn Sie verstehen, wie eine erfolgreich virtualisierte Domänencontroller-Operation aussieht, werden Fehler in Ihrer Umgebung offensichtlich. Diese Protokolle werden nach ihrer Quelle, mit aufsteigend in der Reihenfolge dargestellt *erwartet* Ereignisse (auch wenn sie Warnungen und Fehler sind) im Zusammenhang mit einem geklonten Domänencontroller in jedem Protokoll.  
  
#### <a name="cloning-a-domain-controller"></a>Klonen eines Domänencontrollers  
In diesem Beispiel wird der geklonte Domänencontroller DHCP verwendet, um eine IP-Adresse abzurufen, repliziert SYSVOL über FRS oder DFSR (Siehe das entsprechende Protokoll nach Bedarf), ist ein globaler Katalog, und eine leere dccloneconfig.xml-Datei verwendet wird.  
  
##### <a name="directory-services-event-log"></a>Verzeichnisdienst-Ereignisprotokoll  
Das Verzeichnisdienst-Ereignisprotokoll enthält den Großteil der ereignisbasierten Betriebsinformationen beim Klonen. Der Hypervisor ändert die VM-Generations-ID und der NTDS-Dienst bemerkt dies, macht den RID-Pool ungültig und ändert die aufrufkennung. Die neue VM-Generations-ID wird festgelegt, und der Server repliziert Active Directory-Daten eingehend. Der DFSR-Dienst wurde beendet und die Datenbank, die SYSVOL hostet wird gelöscht, wodurch eine nicht autoritative Synchronisierung eingehende. Der hohe USN-Grenzwert wird angepasst.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**2160**|ActiveDirectory_DomainService|Das lokale Active Directory-Domänendienste hat einen virtuellen Domäne klonkonfigurationsdatei gefunden.<br /><br />Der virtuelle Domänencontroller klonkonfigurationsdatei ist finden Sie unter:<br /><br />*<path>*\DCCloneConfig.Xml<br /><br />Das Vorhandensein der virtuellen Domäne klonkonfigurationsdatei weist darauf hin, dass der lokale virtuelle Domänencontroller ein Klon eines anderen virtuellen Domänencontrollers ist. Active Directory-Domänendienste beginnt zu klonen.|  
|**2191**|ActiveDirectory_DomainService|Active Directory-Domänendienste legen Sie den folgenden Registrierungswert, DNS-Updates zu deaktivieren.<br /><br />Registrierungsschlüssel:<br /><br />SYSTEM\CurrentControlSet\Services\Netlogon\Parameters<br /><br />Registrierungswert:<br /><br />UseDynamicDns-Wert<br /><br />Registrierungswertdaten:<br /><br />0<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können. Der Klonvorgang wird DNS-Updates erneut aktivieren, nachdem das Klonen abgeschlossen ist.|  
|**2191**|ActiveDirectory_DomainService|Active Directory-Domänendienste legen Sie den folgenden Registrierungswert, DNS-Updates zu deaktivieren.<br /><br />Registrierungsschlüssel:<br /><br />SYSTEM\CurrentControlSet\Services\Dnscache\Parameters<br /><br />Registrierungswert:<br /><br />RegistrationEnabled<br /><br />Registrierungswertdaten:<br /><br />0<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können. Der Klonvorgang wird DNS-Updates erneut aktivieren, nachdem das Klonen abgeschlossen ist.<br /><br />"Informationen 2/7/2012 3:12:49 PM Microsoft-Windows-ActiveDirectory_DomainService 2191 interne Konfiguration" Active Directory Domain Services legen Sie den folgenden Registrierungswert, DNS-Updates zu deaktivieren.<br /><br />Registrierungsschlüssel:<br /><br />SYSTEM\CurrentControlSet\Services\Tcpip\Parameters<br /><br />Registrierungswert:<br /><br />DisableDynamicUpdate<br /><br />Registrierungswertdaten:<br /><br />1<br /><br />Während des Klonens möglicherweise der lokale Computer den gleichen Computernamen wie die Quellmaschine Klon für kurze Zeit. DNS A- und AAAA-Eintrag Registrierung werden während dieses Zeitraums deaktiviert, sodass Clients Anforderungen an den lokalen Computer, die momentan Klonen senden können. Der Klonvorgang wird DNS-Updates erneut aktivieren, nachdem das Klonen abgeschlossen ist.|  
|**2172**|ActiveDirectory_DomainService|Lesen Sie das MsDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers.<br /><br />Wert des MsDS-GenerationId-Attributs:<br /><br />*<Number>*|  
|**2170**|ActiveDirectory_DomainService|Eine Änderung der Generations-ID wurde erkannt.<br /><br />In DS (Alter Wert) zwischengespeicherte Generations-ID:<br /><br />*<Number>*<br /><br />Generation-ID des virtuellen Computers (neuer Wert):<br /><br />*<Number>*<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Active Directory-Domänendiensten wird eine neue Aufruf-ID zur Wiederherstellung des Domänencontrollers erstellt. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen der Inhalte einer Active Directory-Domänendienste-Datenbank ist zum Wiederherstellen einer systemstatussicherung, die mit einer sicherungsanwendung von Active Directory-Domänendienste.|  
|**1109**|ActiveDirectory_DomainService|Das InvocationID-Attribut für diesen Verzeichnisserver wurde geändert. Die höchste Aktualisierungssequenznummer zum Zeitpunkt der Erstellung der Sicherung lautet wie folgt:<br /><br />InvocationID-Attribut (Alter Wert):<br /><br />*<GUID>*<br /><br />InvocationID-Attribut (neuer Wert):<br /><br />*<GUID>*<br /><br />Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Die Aufrufkennung geändert wird, wenn von einem Sicherungsmedium, ein Verzeichnisserver wiederhergestellt wird eine beschreibbare Anwendungsverzeichnispartition konfiguriert ist, wurde fortgesetzt wurde, nachdem eine Momentaufnahme des virtuellen Computers angewendet wurde, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen ist der Inhalt einer Active Directory-Domänendienste-Datenbank wiederherstellen eine systemstatussicherung, die mit einer Active Directory Domain Services-fähige sicherungsanwendung.|  
|**1000**|ActiveDirectory_DomainService|Start des Microsoft Active Directory-Domänendienste wurde abgeschlossen.|  
|**1394**|ActiveDirectory_DomainService|Alle Probleme, die Updates in die Active Directory-Domänendienste-Datenbank verhinderten, wurden behoben. Neue Updates für die Active Directory-Domänendienste-Datenbank sind erfolgreich. Der Netzwerkanmeldedienst wird neu gestartet.|  
|**2163**|ActiveDirectory_DomainService|DsRoleSvc-Dienst wurde gestartet, um das Klonen des lokalen virtuellen Domänencontrollers.|  
|**326**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul hat eine Datenbank angefügt (1, C:\Windows\NTDS\ntds.dit). (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.016, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000.<br /><br />Cache gespeichert: 1|  
|**103**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.032, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.|  
|**102**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul (6.02.8225.0000 startet) wird eine neue Instanz (0) gestartet.|  
|**105**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.016, [2] 0.000, [3] 0.015, [4] 0.078, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.046, [10] 0.000, [11] 0.000.|  
|**1004**|ActiveDirectory_DomainService|Active Directory-Domänendienste wurden heruntergefahren.|  
|**102**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul (6.02.8225.0000 startet) wird eine neue Instanz (0) gestartet.|  
|**326**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul hat eine Datenbank angefügt (1, C:\Windows\NTDS\ntds.dit). (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.015, [3] 0.016, [4] 0.000, [5] 0.031, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000.<br /><br />Cache gespeichert: 1|  
|**105**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit = 1 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.031, [2] 0.000, [3] 0.000, [4] 0.391, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.000.|  
|**1109**|ActiveDirectory_DomainService|Das InvocationID-Attribut für diesen Verzeichnisserver wurde geändert. Die höchste Aktualisierungssequenznummer zum Zeitpunkt der Erstellung der Sicherung lautet wie folgt:<br /><br />InvocationID-Attribut (Alter Wert):<br /><br />*<GUID>*<br /><br />InvocationID-Attribut (neuer Wert):<br /><br />*<GUID>*<br /><br />Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Die Aufrufkennung geändert wird, wenn von einem Sicherungsmedium, ein Verzeichnisserver wiederhergestellt wird eine beschreibbare Anwendungsverzeichnispartition konfiguriert ist, wurde fortgesetzt wurde, nachdem eine Momentaufnahme des virtuellen Computers angewendet wurde, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen ist der Inhalt einer Active Directory-Domänendienste-Datenbank wiederherstellen eine systemstatussicherung, die mit einer Active Directory Domain Services-fähige sicherungsanwendung.|  
|**1168**|ActiveDirectory_DomainService|Interner Fehler: eine Active Directory-Domänendienste-Fehler ist aufgetreten.<br /><br />Zusätzliche Daten<br /><br />Fehlerwert (dezimal):<br /><br />2<br /><br />Fehlerwert (hexadezimal):<br /><br />2<br /><br />Interne Kennung:<br /><br />7011658|  
|**1110**|ActiveDirectory_DomainService|Werbung für diesen Domänencontroller zu einem globalen Katalog wird für das folgende Intervall verzögert.<br /><br />Intervall (in Minuten):<br /><br />5<br /><br />Diese Verzögerung ist notwendig, so dass die erforderlichen Partitionen vorbereitet werden können, bevor der globale Katalog angekündigt wird. In der Registrierung können Sie die Anzahl der Sekunden angeben, die der Directory System Agent vor dem Heraufstufen des lokalen Domänencontrollers zum globalen Katalog warten soll. Weitere Informationen zum Registrierungswert Global Catalog Delay Advertisement finden Sie in den Resource Kit Distributed Systems Guide|  
|**103**|NTDS-ISAM|NTDS (536) NTDSA: Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.047, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.016, [10] 0.000, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.|  
|**1004**|ActiveDirectory_DomainService|Active Directory-Domänendienste wurden heruntergefahren.|  
|**1539**|ActiveDirectory_DomainService|Active Directory Domain Services konnte die softwarebasierten Datenträgerschreibungscache auf der folgenden Festplatte nicht deaktivieren.<br /><br />Festplatte:<br /><br />"c:"<br /><br />Daten möglicherweise bei einem Systemfehler verloren|  
|**2179**|ActiveDirectory_DomainService|Das MsDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers wurde der folgende Parameter festgelegt:<br /><br />Generations-ID-Attribut:<br /><br />*<Number>*|  
|**2173**|ActiveDirectory_DomainService|Fehler beim Lesen des MsDS-GenerationId-Attributs des Computerobjekts des Domänencontrollers. Dies kann darauf zurückzuführen, dass Transaktion Datenbankfehler, oder die Generations-Id in der lokalen Datenbank nicht vorhanden. Das MsDS-GenerationId existiert nicht beim ersten Neustart nach Dcpromo oder der Domänencontroller keines virtuellen Domänencontrollers ist.<br /><br />Zusätzliche Daten<br /><br />Fehlercode:<br /><br />6|  
|**1000**|ActiveDirectory_DomainService|Starten von Microsoft Active Directory-Domänendienste abgeschlossen. Version 6.2.8225.0|  
|**1394**|ActiveDirectory_DomainService|Alle Probleme, die Updates in die Active Directory-Domänendienste-Datenbank verhinderten, wurden behoben. Neue Updates für die Active Directory-Domänendienste-Datenbank sind erfolgreich. Der Netlogon-Dienst neu gestartet wurde.|  
|**1128**|ActiveDirectory_DomainService|1128 Konsistenzprüfung "eine replikationsverbindung wurde vom folgenden Quellverzeichnisdienst zum lokalen Verzeichnisdienst erstellt.<br /><br />Quellverzeichnisdienst:<br /><br />CN = NTDS Settings,*<Domain Controller DN>*<br /><br />Lokaler Verzeichnisdienst:<br /><br />CN = NTDS Settings,*<Domain Controller DN>*<br /><br />Zusätzliche Daten<br /><br />Grundcode:<br /><br />0 x 2<br /><br />Interne Kennung für Erstellungspunkt:<br /><br />f0a025d|  
|**1999**|ActiveDirectory_DomainService|Der Quellverzeichnisdienst hat die Aktualisierungssequenznummer (USN), das von der zielverzeichnisdienst optimiert. Die Quell- und Zielserver haben eines gemeinsamen Replikationspartners. Der zielverzeichnisdienst ist mit der gemeinsame Replikationspartner, und der Quellverzeichnisdienst mithilfe einer Sicherung dieses Partners installiert wurde.<br /><br />Kennung des Zielverzeichnisdiensts:<br /><br />*<GUID> (<FQDN>)*<br /><br />Kennung des gemeinsamen Verzeichnisdiensts:<br /><br />*<GUID>*<br /><br />Gemeinsame Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Daher wurde der Aktualitätsvektor des zielverzeichnisdienstes mit den folgenden Einstellungen konfiguriert.<br /><br />Vorherige Objekt-Aktualisierungssequenznummer:<br /><br />0<br /><br />Vorherige Eigenschafts-Aktualisierungssequenznummer:<br /><br />0<br /><br />Datenbank-GUID:<br /><br />*<GUID>*<br /><br />Objekt-Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<Number>*|  
  
##### <a name="system-event-log"></a>Systemereignisprotokoll  
Die nächsten Hinweise zu Klonvorgängen befinden sich in das Systemereignisprotokoll. Da der Hypervisor dem Gastcomputer mitteilt, dass er geklont oder aus einer Momentaufnahme wiederhergestellt wurde, wird der Domänencontroller sofort seinen RID-Pool zur Vermeidung von Duplizieren von Sicherheitsprinzipalen später ungültig. Wenn das Klonen Erlöse, verschiedenen erwarteten Vorgängen und Meldungen angezeigt werden, hauptsächlich rund um das Starten und Beenden von Diensten und die dadurch verursachten Fehler. Wenn der System-Ereignisprotokoll Notizen insgesamt das Klonen erfolgreich abgeschlossen.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**16654**|Verzeichnisdienste-SAM|Ein Pool aus kontobezeichnern (RIDs) wurde ungültig gemacht. Dies kann in den folgenden zu erwartenden Fällen auftreten:<br /><br />1. ein Domänencontroller ist von einer Sicherung wiederhergestellt.<br /><br />2. ein Domänencontroller, die auf einem virtuellen Computer wird aus einer Momentaufnahme wiederhergestellt.<br /><br />3. ein Administrator hat den Pool manuell ungültig gemacht|  
|**7036**|Dienststeuerungs-Manager|Der Active Directory-Domänendienste-Dienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Kerberos-Schlüsselverteilungscenter-Dienst wird jetzt ausgeführt.|  
|**3096**|Anmeldedienst|Der primäre Domänencontroller für diese Domäne konnte nicht gefunden werden.|  
|**7036**|Dienststeuerungs-Manager|Die Sicherheitskonten-Manager-Dienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Serverdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Active Directory-Webdienste-Dienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der DFS-Replikationsdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Dateireplikationsdienst wird jetzt ausgeführt.|  
|**14533**|Microsoft-Windows-DfsSvc|DFS hat alle Namespaces erstellt.|  
|**14531**|Microsoft-Windows-DfsSvc|DFS-Server wurde vollständig initialisiert.|  
|**7036**|Dienststeuerungs-Manager|Der DFS-Namespace-Dienst wird jetzt ausgeführt.|  
|**7023**|Dienststeuerungs-Manager|Der standortübergreifende Messagingdienst wurde mit folgendem Fehler beendet:<br /><br />Der angegebene Server kann nicht den angeforderten Vorgang ausführen.|  
|**7036**|Dienststeuerungs-Manager|Der standortübergreifende Messagingdienst hat den Status "beendet" eingegeben.|  
|**5806**|Anmeldedienst|Dynamische Aktualisierungen wurden auf diesem Domänencontroller manuell deaktiviert.<br /><br />BENUTZERAKTION<br /><br />Konfigurieren Sie diesen Domänencontroller zur Verwendung dynamischer Aktualisierungen oder die DNS-Einträge manuell aus der Datei '% SystemRoot%\System32\Config\Netlogon.dns' hinzufügen, der DNS-Datenbank."|  
|**16651**|Verzeichnisdienste-SAM|Die Anforderung für einen neuen Kontenidentifizierungspool ist fehlgeschlagen. Der Vorgang wird wiederholt, bis die Anforderung erfolgreich war. Der Fehler ist<br /><br />Der angeforderte FSMO-Vorgang ist fehlgeschlagen. Der aktuelle FSMO-Inhaber war nicht erreichbar.|  
|**7036**|Dienststeuerungs-Manager|Der DNS-Serverdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der DS-rollenserverdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wird jetzt beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Dateireplikationsdienst wird jetzt beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Kerberos-Schlüsselverteilungscenter-Dienst wird jetzt beendet.|  
|**7036**|Dienststeuerungs-Manager|Der DNS-Serverdienst wird jetzt beendet.|  
|**7036**|Dienststeuerungs-Manager|Die Active Directory Domain Services-Dienst wird jetzt beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wird jetzt ausgeführt.|  
|**7040**|Dienststeuerungs-Manager|Der Starttyp des Diensts Active Directory-Domänendienste wurde von automatischem Start deaktiviert geändert.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wird jetzt beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Dateireplikationsdienst wird jetzt ausgeführt.|  
|**29219**|DirectoryServices-DSROLE-Server|Klonen virtueller Domänencontroller wurde erfolgreich abgeschlossen.|  
|**29223**|DirectoryServices-DSROLE-Server|Dieser Server ist jetzt ein Domänencontroller.|  
|**29265**|DirectoryServices-DSROLE-Server|Klonen virtueller Domänencontroller wurde erfolgreich abgeschlossen. Des virtuellen Domänencontrollers verwendete Konfigurationsdatei C:\Windows\NTDS\DCCloneConfig.xml Klonen wurde in C:\Windows\NTDS\DCCloneConfig.20120207-151533.xml umbenannt.|  
|**1074**|User32|Der Prozess C:\Windows\system32\lsass.exe (DC2) hat den Neustart des Computers DC2 für Benutzer NT AUTHORITY\SYSTEM aus folgendem Grund initiiert: Betriebssystem: Neukonfigurierung (geplant)<br /><br />Grund aus dem Code: 0 x 80020004<br /><br />Herunterfahrtyp: Neustart<br /><br />Kommentar: "|  
  
##### <a name="dcpromolog"></a>DCPROMO. PROTOKOLL  
Dcpromo.log enthält den tatsächlichen heraufstufungsteil des Klonvorgangs, den den Verzeichnisdienst-Ereignisprotokoll nicht beschrieben ist. Da das Protokoll keine Erläuterung, die die Ereignisprotokolleinträge bereitstellt, enthält dieser Abschnitt des Moduls zusätzliche Anmerkungen.  
  
Der Heraufstufungsprozess bedeutet, die der Klonvorgang beginnt, den Domänencontroller von seiner aktuellen Konfiguration bereinigt und erneut heraufgestuft wird die vorhandene AD-Datenbank (ähnlich einer IFM-heraufstufung), und klicken Sie dann repliziert der Domänencontroller eingehende änderungsdeltas von AD und SYSVOL, und das Klonen abgeschlossen ist.  
  
> [!NOTE]  
> Das Protokoll wurde in diesem Modul aus Gründen der besseren Lesbarkeit geändert, indem die Datumsspalte entfernt.  
  
> [!NOTE]  
> Weitere Erläuterung zu dcpromo.log finden Sie in der Grundlagen und Problembehandlung für AD DS vereinfachte Verwaltung in Windows Server 2012.  
>   
> [https://go.microsoft.com/fwlink/p/?LinkId=237244](https://go.microsoft.com/fwlink/p/?LinkId=237244)  
  
-   Starten der klonbasierten heraufstufung  
  
-   Die Verzeichnisdienst-Wiederherstellungsmodus Kennzeichen festgelegt, sodass der Server nicht sichern Sie normalerweise als die ursprüngliche Klon und benennungs- oder verzeichnisdienstkollisionen startet  
  
-   Aktualisieren Sie das Verzeichnisdienst-Ereignisprotokoll  
  
```  
15:14:01 [INFO] vDC Cloneing: Setting Boot into DSRM flag succeeded.  
15:14:01 [WARNING] Cannot get user Token for Format Message: 1725l  
15:14:01 [INFO] vDC Cloning: Created vDCCloningUpdate event.  
15:14:01 [INFO] vDC Cloning: Created vDCCloningComplete event.  
```  
  
-   Beenden Sie den NetLogon-Dienst, sodass der Domänencontroller nicht ankündigt.  
  
```  
15:14:01 [INFO] Stopping service NETLOGON  
15:14:01 [INFO] ControlService(STOP) on NETLOGON returned 1(gle=0)  
15:14:01 [INFO] DsRolepWaitForService: waiting for NETLOGON to enter one of 7 states  
15:14:01 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:02 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=1  
15:14:02 [INFO] DsRolepWaitForService: exiting because NETLOGON entered STOPPED state  
15:14:02 [INFO] DsRolepWaitForService(for any end state) on NETLOGON service returned 0  
15:14:02 [INFO] ControlService(STOP) on NETLOGON returned 0(gle=1062)  
15:14:02 [INFO] Exiting service-stop loop after service NETLOGON entered STOPPED state  
15:14:02 [INFO] StopService on NETLOGON returned 0  
15:14:02 [INFO] Configuring service NETLOGON to 1 returned 0  
15:14:02 [INFO] Updating service status to 4  
15:14:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Überprüfen Sie die Datei dccloneconfig.xml auf administratorspezifische Anpassungen.  
  
-   In diesem Beispiel ist es eine leere Datei, damit alle Einstellungen automatisch generiert werden und automatische IP-Adressierung vom Netzwerk erforderlich ist.  
  
```  
15:14:02 [INFO] vDC Cloning: Clone config file C:\Windows\NTDS\DCCloneConfig.xml is considered to be a blank file (containing 0 bytes)  
15:14:02 [INFO] vDC Cloning: Parsing clone config file C:\Windows\NTDS\DCCloneConfig.xml returned HRESULT 0x0  
```  
  
-   Überprüfen Sie, ob keine Dienste oder Programme installiert, die nicht Teil der DefaultDCCloneAllowList.xml oder customdccloneallowlist.XML enthalten sind  
  
```  
15:14:02 [INFO] vDC Cloning: Checking allowed list:  
15:14:03 [INFO] vDC Cloning: Completed checking allowed list:  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Aktivieren Sie DHCP auf den Netzwerkadaptern, da IP-Informationen nicht vom Administrator angegeben wurde  
  
```  
15:14:03 [INFO] vDC Cloning: Enable DHCP:  
15:14:03 [INFO] WMI Instance: Win32_NetworkAdapterConfiguration.Index=12  
15:14:03 [INFO] Method: EnableDHCP  
15:14:03 [INFO] HRESULT code: 0x0 (0)  
15:14:03 [INFO] Return Value: 0x0 (0)  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Suchen Sie den PDC-emulator  
  
-   Legen Sie den Standort des Klons (in diesem Fall automatisch generiert).  
  
-   Legen Sie den Namen des Klons (in diesem Fall automatisch generiert).  
  
```  
15:14:03 [INFO] vDC Cloning: Found PDC. Name: DC1.root.fabrikam.com  
15:14:04 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:04 [INFO] vDC Cloning: Winlogon UI Notification #1: Domain Controller cloning is at 5% completion...  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #2: Domain Controller cloning is at 10% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Site of the cloned DC: Default-First-Site-Name  
```  
  
-   Erstellen Sie das neue kloncomputerobjekt.  
  
-   Benennen Sie den Klon entsprechend den neuen Namen  
  
```  
15:14:05 [INFO] vDC Cloning: Clone DC objects are created on PDC.  
15:14:05 [INFO] Name of the cloned DC: DC2-CL0001  
15:14:05 [INFO] DsRolepSetRegStringValue on System\CurrentControlSet\Services\NTDS\Parameters\CloneMachineName to DC2-CL0001 returned 0  
15:14:05 [INFO] vDC Cloning: Save CloneMachineName in registry: 0x0 (0)  
```  
  
-   Geben Sie die heraufstufungseinstellungen basierend auf früheren dccloneconfig.xml oder automatischen Generierungsregeln.  
  
```  
15:14:05 [INFO] vDC Cloning: Promotion parameters setting:  
15:14:05 [INFO] DNS Domain Name: root.fabrikam.com  
15:14:05 [INFO] Replica Partner: \\DC1.root.fabrikam.com  
15:14:05 [INFO] Site Name: Default-First-Site-Name  
15:14:05 [INFO] DS Database Path: C:\Windows\NTDS  
15:14:05 [INFO] DS Log Path: C:\Windows\NTDS  
15:14:05 [INFO] SysVol Root Path: C:\Windows\SYSVOL  
15:14:05 [INFO] Account: root.fabrikam.com\DC2-CL0001$  
15:14:05 [INFO] Options: DSROLE_DC_CLONING (0x800400)  
```  
  
-   Starten Sie Werbung  
  
```  
15:14:05 [INFO] Promote DC as a clone  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #3: Domain Controller cloning is at 15% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #4: Domain Controller cloning is at 16% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Validate supplied paths  
15:14:05 [INFO] Validating path C:\Windows\NTDS.  
15:14:05 [INFO] Path is a directory  
15:14:05 [INFO] Path is on a fixed disk drive.  
15:14:05 [INFO] Validating path C:\Windows\NTDS.  
15:14:05 [INFO] Path is a directory  
15:14:05 [INFO] Path is on a fixed disk drive.  
15:14:05 [INFO] Validating path C:\Windows\SYSVOL.  
15:14:05 [INFO] Path is on a fixed disk drive.  
15:14:05 [INFO] Path is on an NTFS volume  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #5: Domain Controller cloning is at 17% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Start the worker task  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #6: Domain Controller cloning is at 20% completion...  
15:14:05 [INFO] Request for promotion returning 0  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #7: Domain Controller cloning is at 21% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Beenden Sie und konfigurieren Sie alle AD DS-verwandten Dienste (NTDS, NTFRS/DFSR, KDC, DNS)  
  
> [!NOTE]  
> Der DNS-Dienst zum Herunterfahren lange braucht wird in diesem Szenario erwartet, wie Active Directory-integrierte Zonen verwendet wird, die nicht mehr verfügbar ist, noch bevor der NTDS-Dienst wurde beendet - waren finden Sie weiter unten in diesem Abschnitt des Moduls beschriebenen DNS-Ereignisse.  
  
```  
15:14:15 [INFO] Stopping service NTDS  
15:14:15 [INFO] Stopping service NtFrs  
15:14:15 [INFO] ControlService(STOP) on NtFrs returned 1(gle=0)  
15:14:15 [INFO] DsRolepWaitForService: waiting for NtFrs to enter one of 7 states  
15:14:15 [INFO] DsRolepWaitForService: QueryServiceStatus on NtFrs returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:16 [INFO] DsRolepWaitForService: QueryServiceStatus on NtFrs returned 1 (gle=0), SvcStatus.dwCS=1  
15:14:16 [INFO] DsRolepWaitForService: exiting because NtFrs entered STOPPED state  
15:14:16 [INFO] DsRolepWaitForService(for any end state) on NtFrs service returned 0  
15:14:16 [INFO] ControlService(STOP) on NtFrs returned 0(gle=1062)  
15:14:16 [INFO] Exiting service-stop loop after service NtFrs entered STOPPED state  
15:14:16 [INFO] StopService on NtFrs returned 0  
15:14:16 [INFO] Configuring service NtFrs to 1 returned 0  
15:14:16 [INFO] Stopping service Kdc  
15:14:16 [INFO] ControlService(STOP) on Kdc returned 1(gle=0)  
15:14:16 [INFO] DsRolepWaitForService: waiting for Kdc to enter one of 7 states  
15:14:16 [INFO] DsRolepWaitForService: QueryServiceStatus on Kdc returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:17 [INFO] DsRolepWaitForService: QueryServiceStatus on Kdc returned 1 (gle=0), SvcStatus.dwCS=1  
15:14:17 [INFO] DsRolepWaitForService: exiting because Kdc entered STOPPED state  
15:14:17 [INFO] DsRolepWaitForService(for any end state) on Kdc service returned 0  
15:14:17 [INFO] ControlService(STOP) on Kdc returned 0(gle=1062)  
15:14:17 [INFO] Exiting service-stop loop after service Kdc entered STOPPED state  
15:14:17 [INFO] StopService on Kdc returned 0  
15:14:17 [INFO] Configuring service Kdc to 1 returned 0  
15:14:17 [INFO] Stopping service DNS  
15:14:17 [INFO] ControlService(STOP) on DNS returned 1(gle=0)  
15:14:17 [INFO] DsRolepWaitForService: waiting for DNS to enter one of 7 states  
15:14:17 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:18 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:19 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:20 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:21 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:22 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:23 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:24 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:25 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:26 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:27 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:28 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:29 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:30 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:31 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:32 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:33 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:34 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:35 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:36 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:37 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:38 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:39 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:40 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:41 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:42 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:43 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:44 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:45 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:46 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:47 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:48 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:49 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:50 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:51 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:52 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:53 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:54 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:55 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:56 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:57 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:58 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:59 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:15:00 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=1  
15:15:00 [INFO] DsRolepWaitForService: exiting because DNS entered STOPPED state  
15:15:00 [INFO] DsRolepWaitForService(for any end state) on DNS service returned 0  
15:15:00 [INFO] ControlService(STOP) on DNS returned 0(gle=1062)  
15:15:00 [INFO] Exiting service-stop loop after service DNS entered STOPPED state  
15:15:00 [INFO] StopService on DNS returned 0  
15:15:00 [INFO] Configuring service DNS to 1 returned 0  
15:15:00 [INFO] ControlService(STOP) on NTDS returned 1(gle=1062)  
15:15:00 [INFO] DsRolepWaitForService: waiting for NTDS to enter one of 7 states  
15:15:00 [INFO] DsRolepWaitForService: QueryServiceStatus on NTDS returned 1 (gle=0), SvcStatus.dwCS=3  
15:15:01 [INFO] DsRolepWaitForService: QueryServiceStatus on NTDS returned 1 (gle=0), SvcStatus.dwCS=1  
15:15:01 [INFO] DsRolepWaitForService: exiting because NTDS entered STOPPED state  
15:15:01 [INFO] DsRolepWaitForService(for any end state) on NTDS service returned 0  
15:15:01 [INFO] ControlService(STOP) on NTDS returned 0(gle=1062)  
15:15:01 [INFO] Exiting service-stop loop after service NTDS entered STOPPED state  
15:15:01 [INFO] StopService on NTDS returned 0  
15:15:01 [INFO] Configuring service NTDS to 1 returned 0  
15:15:01 [INFO] Configuring service NTDS  
15:15:01 [INFO] Configuring service NTDS to 64 returned 0  
15:15:01 [INFO] vDC Cloning: Winlogon UI Notification #8: Domain Controller cloning is at 22% completion...  
15:15:01 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:01 [INFO] vDC Cloning: Winlogon UI Notification #9: Domain Controller cloning is at 25% completion...  
15:15:01 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Erzwingen Sie die NT5DS (NTP)-zeitsynchronisierung mit einem anderen Domänencontroller (normalerweise dem PDCE)  
  
```  
15:15:02 [INFO] Forcing time sync  
```  
  
-   Wenden Sie sich an einem Domänencontroller, der die Quelle das Konto des Quelldomänencontrollers des Klons enthält  
  
-   Löschen Sie alle vorhandenen Kerberos-tickets  
  
```  
15:15:02 [INFO] Searching for a domain controller for the domain root.fabrikam.com that contains the account DC2$  
15:15:02 [INFO] Located domain controller DC1.root.fabrikam.com for domain root.fabrikam.com  
15:15:02 [INFO] vDC Cloning: Winlogon UI Notification #10: Domain Controller cloning is at 26% completion...  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:02 [INFO] Directing kerberos authentication to DC1.root.fabrikam.com returns 0  
15:15:02 [INFO] DsRolepFlushKerberosTicketCache() successfully flushed the Kerberos ticket cache  
15:15:02 [INFO] vDC Cloning: Winlogon UI Notification #11: Domain Controller cloning is at 27% completion...  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:02 [INFO] Using site Default-First-Site-Name for server \\DC1.root.fabrikam.com  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Beenden Sie den NetLogon-Dienst, und legen Sie seinen Starttyp  
  
```  
15:15:02 [INFO] Stopping service NETLOGON  
15:15:02 [INFO] Stopping service NETLOGON  
15:15:02 [INFO] vDC Cloning: Winlogon UI Notification #12: Domain Controller cloning is at 29% completion...  
15:15:02 [INFO] ControlService(STOP) on NETLOGON returned 1(gle=0)  
15:15:02 [INFO] DsRolepWaitForService: waiting for NETLOGON to enter one of 7 states  
15:15:02 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=3  
15:15:03 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=1  
15:15:03 [INFO] DsRolepWaitForService: exiting because NETLOGON entered STOPPED state  
15:15:03 [INFO] DsRolepWaitForService(for any end state) on NETLOGON service returned 0  
15:15:03 [INFO] ControlService(STOP) on NETLOGON returned 0(gle=1062)  
15:15:03 [INFO] Exiting service-stop loop after service NETLOGON entered STOPPED state  
15:15:03 [INFO] StopService on NETLOGON returned 0  
15:15:03 [INFO] Configuring service NETLOGON to 1 returned 0  
15:15:03 [INFO] Stopped NETLOGON  
15:15:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:03 [INFO] vDC Cloning: Winlogon UI Notification #13: Domain Controller cloning is at 30% completion...  
```  
  
-   Konfigurieren Sie die DFSR/NTFRS-Dienste für die automatische Ausführung  
  
-   Löschen Sie ihre vorhandenen Datenbankdateien, um nicht autoritative Synchronisierung von SYSVOL beim nächsten des Dienstes Start zu erzwingen  
  
```  
15:15:03 [INFO] Configuring service DFSR  
15:15:03 [INFO] Configuring service DFSR to 256 returned 0  
15:15:03 [INFO] Configuring service NTFRS  
15:15:03 [INFO] Configuring service NTFRS to 256 returned 0  
15:15:03 [INFO] Removing DFSR Database files for SysVol  
15:15:03 [INFO] Removing FRS Database files in C:\Windows\ntfrs\jet  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edb.log  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edbres00001.jrs  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edbres00002.jrs  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edbtmp.log  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\ntfrs.jdb  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\sys\edb.chk  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\temp\tmp.edb  
15:15:04 [INFO] Created system volume path  
15:15:04 [INFO] Configuring service DFSR  
15:15:04 [INFO] Configuring service DFSR to 128 returned 0  
15:15:04 [INFO] Configuring service NTFRS  
15:15:04 [INFO] Configuring service NTFRS to 128 returned 0  
15:15:04 [INFO] vDC Cloning: Winlogon UI Notification #14: Domain Controller cloning is at 40% completion...  
15:15:04 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   Starten Sie den Heraufstufungsprozess mit der vorhandenen NTDS-Datenbankdatei  
  
-   Wenden Sie sich an den RID-Master  
  
> [!NOTE]  
> Der AD DS-Dienst ist hier nicht tatsächlich installiert, dies ist eine vorversionsinstrumentation im Protokoll  
  
```  
15:15:04 [INFO] Installing the Directory Service  
15:15:04 [INFO] Calling NtdsInstall for root.fabrikam.com  
15:15:04 [INFO] Starting Active Directory Domain Services installation  
15:15:04 [INFO] Validating user supplied options  
15:15:04 [INFO] Determining a site in which to install  
15:15:04 [INFO] Examining an existing forest...  
15:15:04 [INFO] Starting a replication cycle between DC1.root.fabrikam.com and the RID operations master (2008r2-01.root.fabrikam.com), so that the new replica will be able to create users, groups, and computer objects...  
15:15:04 [INFO] Configuring the local computer to host Active Directory Domain Services  
15:15:04 [INFO] EVENTLOG (Warning): NTDS General / Service Control : 1539  
Active Directory Domain Services could not disable the software-based disk write cache on the following hard disk.  
Hard disk:  
c:  
Data might be lost during system failures.  
15:15:10 [INFO] EVENTLOG (Informational): NTDS General / Internal Processing : 2041  
Duplicate event log entries were suppressed.  
See the previous event log entry for details. An entry is considered a duplicate if  
the event code and all of its insertion parameters are identical. The time period for  
this run of duplicates is from the time of the previous event to the time of this event.  
Event Code:  
80000603  
Number of duplicate entries:   
2  
15:15:10 [INFO] EVENTLOG (Informational): NTDS General / Internal Configuration : 2121  
This Active Directory Domain Services server is disabling the Recycle Bin. Deleted objects may not be undeleted at this time.  
```  
  
-   Ändern Sie die vorhandene Aufruf-ID, die in der Datenbank vorhanden waren.  
  
-   Erstellen Sie ein neues NTDS-Einstellungsobjekt für diesen Klon.  
  
-   In AD-objektdelta vom Partner-Domänencontroller repliziert werden  
  
> [!NOTE]  
> Auch wenn alle Objekte als repliziert aufgelistet sind, ist dies nur Metadaten erforderlich, um die Updates zu klassifizieren. Alle unveränderten Objekte in der geklonten NTDS-Datenbank müssen bereits vorhanden und nicht erneut repliziert werden, wie bei der Verwendung der IFM-basierten heraufstufung.  
  
```  
15:15:10 [INFO] EVENTLOG (Informational): NTDS Replication / Replication : 1109  
The invocationID attribute for this directory server has been changed. The highest update sequence number at the time the backup was created is as follows:  
InvocationID attribute (old value):  
24e7b22f-4706-402d-9b4f-f2690f730b40  
InvocationID attribute (new value):  
f74cefb2-89c2-442c-b1ba-3234b0ed62f8  
Update sequence number:  
20520  
The invocationID is changed when a directory server is restored from backup media, is configured to host a writeable application directory partition, has been resumed after a virtual machine snapshot has been applied, after a virtual machine import operation, or after a live migration operation. Virtualized domain controllers should not be restored using virtual machine snapshots. The supported method to restore or rollback the content of an Active Directory Domain Services database is to restore a system state backup made with an Active Directory Domain Services-aware backup application.  
15:15:10 [INFO] EVENTLOG (Error): NTDS General / Internal Processing : 1168  
Internal error: An Active Directory Domain Services error has occurred.  
Additional Data  
Error value (decimal):  
2  
Error value (hexadecimal):  
2  
Internal ID:  
7011658  
15:15:11 [INFO] Creating the NTDS Settings object for this Active Directory Domain Controller on the remote AD DC DC1.root.fabrikam.com...  
15:15:11 [INFO] Replicating the schema directory partition  
15:15:11 [INFO] Replicated the schema container.  
15:15:12 [INFO] Active Directory Domain Services updated the schema cache.  
15:15:12 [INFO] Replicating the configuration directory partition  
15:15:12 [INFO] Replicating data CN=Configuration,DC=root,DC=fabrikam,DC=com: Received 2612 out of approximately 2612 objects and 94 out of approximately 94 distinguished name (DN) values...  
15:15:12 [INFO] Replicated the configuration container.  
15:15:13 [INFO] Replicating critical domain information...  
15:15:13 [INFO] Replicating data DC=root,DC=fabrikam,DC=com: Received 109 out of approximately 109 objects and 35 out of approximately 35 distinguished name (DN) values...  
15:15:13 [INFO] Replicated the critical objects in the domain container.  
```  
  
-   Füllen Sie die Partitionen des globalen Katalogservers nach Bedarf mit fehlenden Aktualisierungen.  
  
-   Führen Sie die kritischen AD DS-Teil der heraufstufung  
  
```  
15:15:13 [INFO] EVENTLOG (Informational): NTDS General / Global Catalog : 1110  
Promotion of this domain controller to a global catalog will be delayed for the following interval.  
Interval (minutes):  
5  
This delay is necessary so that the required directory partitions can be prepared before the global catalog is advertised. In the registry, you can specify the number of seconds that the directory system agent will wait before promoting the local domain controller to a global catalog. For more information about the Global Catalog Delay Advertisement registry value, see the Resource Kit Distributed Systems Guide.  
15:15:14 [INFO] EVENTLOG (Informational): NTDS General / Service Control : 1000  
Microsoft Active Directory Domain Services startup complete, version 6.2.8225.0   
15:15:15 [INFO] Creating new domain users, groups, and computer objects  
15:15:16 [INFO] Completing Active Directory Domain Services installation  
15:15:16 [INFO] NtdsInstall for root.fabrikam.com returned 0  
15:15:16 [INFO] DsRolepInstallDs returned 0  
15:15:16 [INFO] Installed Directory Service  
```  
  
-   Führen Sie die eingehende Replikation von SYSVOL  
  
```  
15:15:16 [INFO] vDC Cloning: Winlogon UI Notification #15: Domain Controller cloning is at 60% completion...  
15:15:16 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] Completed system volume replication  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #16: Domain Controller cloning is at 70% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] SetProductType to 2 [LanmanNT] returned 0  
15:15:18 [INFO] Set the product type  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #17: Domain Controller cloning is at 71% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #18: Domain Controller cloning is at 72% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] Set the system volume path for NETLOGON  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #19: Domain Controller cloning is at 73% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] Replicating non critical information  
15:15:18 [INFO] User specified to not replicate non-critical data  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #20: Domain Controller cloning is at 80% completion...  
15:15:18 [INFO] Stopped the DS  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #21: Domain Controller cloning is at 90% completion...  
15:15:18 [INFO] Configuring service NTDS  
15:15:18 [INFO] Configuring service NTDS to 16 returned 0  
```  
  
-   Aktivieren von DNS-Clientregistrierung  
  
```  
15:15:18 [INFO] vDC Cloning: Set DisableDynamicUpdate reg value to 0 to enable dynamic update records registration.  
15:15:18 [INFO] vDC Cloning: Set UseDynamicDns reg value to 1 to enable dynamic update records registration.  
15:15:18 [INFO] vDC Cloning: Set RegistrationEnabled reg value to 1 to enable dynamic update records registration.  
```  
  
-   Führen Sie die vom DefaultDCCloneAllowList.xml angegebenen SYSPREP-Module <SysprepInformation> Element.  
  
```  
15:15:18 [INFO] vDC Cloning: Running sysprep providers.  
15:15:32 [INFO] vDC Cloning: Completed running sysprep providers.  
```  
  
-   Die heraufstufung des Klonvorgangs ist abgeschlossen  
  
-   Entfernen Sie die DSRM-Startkennzeichen, damit der Server beim nächsten Mal normal gestartet wird.  
  
-   Benennen Sie die Datei dccloneconfig.xml, sodass beim nächsten Start nicht erneut gelesen wird  
  
-   Starten Sie den Computer neu  
  
```  
15:15:32 [INFO] The attempted domain controller operation has completed  
15:15:32 [INFO] Updating service status to 4  
15:15:32 [INFO] DsRolepSetOperationDone returned 0  
15:15:32 [INFO] vDC Cloning: Set vDCCloningComplete event.  
15:15:32 [INFO] vDC Cloneing: Clearing Boot into DSRM flag succeeded.  
15:15:32 [INFO] vDC Cloning: Winlogon UI Notification #22: Cloning Domain Controller succeeded. Now rebooting...  
15:15:33 [INFO] vDC Cloning: Renamed vDC clone configuration file.  
15:15:33 [INFO] vDC Cloning: The old name is: C:\Windows\NTDS\DCCloneConfig.xml  
15:15:33 [INFO] vDC Cloning: The new name is: C:\Windows\NTDS\DCCloneConfig.20120207-151533.xml  
15:15:34 [INFO] vDC Cloning: Release Ipv4 on interface 'Wired Ethernet Connection 2', result=0.  
15:15:34 [INFO] vDC Cloning: Release Ipv6 on interface 'Wired Ethernet Connection 2', result=0.  
15:15:34 [INFO] Rebooting machine  
```  
  
##### <a name="active-directory-web-services-event-log"></a>Active Directory Web Services-Ereignisprotokoll  
Während das Klonen ausgeführt wird, die NTDS. DIT-Datenbank ist oft für längere Zeit offline. Der ADWS-Dienst protokolliert mindestens ein Ereignis für diese. Nach Abschluss des Klonens der ADWS-Dienst startet, Notizen, die es noch nicht gültiges Computerzertifikat noch (es könnte oder möglicherweise nicht, je nach Ihrer Umgebung eine Microsoft PKI mit automatischer Registrierung oder nicht) und startet dann die Instanz für den neuen Domänencontroller.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**1202**|Ereignisse der ADWS-Instanz|Dieser Computer wird nun die angegebene Verzeichnisinstanz gehostet, jedoch Active Directory-Webdiensten konnte nicht gewartet wird. Active Directory-Webdienste wiederholt diesen Vorgang in regelmäßigen Abständen.<br /><br />Der Verzeichnisinstanz: NTDS<br /><br />LDAP-Port der Verzeichnisinstanz: 389<br /><br />SSL-Port der Verzeichnisinstanz: 636|  
|**1000**|Ereignisse der ADWS-Instanz|Active Directory-Webdienste wird gestartet.|  
|**1008**|Ereignisse der ADWS-Instanz|Active Directory-Webdienste wurde Sicherheitsberechtigungen erfolgreich reduziert werden.|  
|**1100**|Ereignisse der ADWS-Instanz|Die Werte in der <appsettings> Abschnitt der Konfigurationsdatei für die Active Directory-Webdienste wurden fehlerfrei geladen.|  
|**1400**|Ereignisse der ADWS-Instanz|ADWS-Zertifikatereignisse "Active Directory-Webdiensten konnte ein Serverzertifikat mit dem angegebenen Zertifikatnamen nicht finden. Die Verwendung von SSL/TLS-Verbindungen ist ein Zertifikat erforderlich. Verwendung von SSL/TLS-Verbindungen, stellen Sie sicher, dass ein gültiges Serverauthentifizierungszertifikat von einer vertrauenswürdigen Zertifizierungsstelle (CA) auf dem Computer installiert ist.<br /><br />Name des Zertifikats:*<Server FQDN>*|  
|**1100**|Ereignisse der ADWS-Instanz|Die Werte in der <appsettings> Abschnitt der Konfigurationsdatei für die Active Directory-Webdienste wurden fehlerfrei geladen.|  
|**1200**|Ereignisse der ADWS-Instanz|Active Directory-Webdiensten bedient jetzt die angegebene Verzeichnisinstanz.<br /><br />Der Verzeichnisinstanz: NTDS<br /><br />LDAP-Port der Verzeichnisinstanz: 389<br /><br />SSL-Port der Verzeichnisinstanz: 636|  
  
##### <a name="dns-server-event-log"></a>DNS-Server-Ereignisprotokoll  
Der DNS-Dienst wird kurze erwartete Ausfälle auftreten, während das Klonen tritt auf, wie der DNS-Dienst noch ausgeführt wird, während die AD DS-Datenbank offline ist. Dies geschieht, wenn Active Directory integrierten DNS verwenden, aber keine standardmäßigen primären oder sekundären DNS verwenden. Diese Fehler werden mehrmals protokolliert. Nach Abschluss des Klonvorgangs ist DNS normal wieder online.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**4013**|DNS-Serverdienst|Der DNS-Server wartet für Active Directory-Domänendienste (AD DS) zu signalisieren, dass die erstsynchronisierung des Verzeichnisses abgeschlossen wurde. Der DNS-Serverdienst kann nicht gestartet, bis die erste Synchronisierung abgeschlossen ist, da wichtige DNS-Daten möglicherweise noch nicht auf diesen Domänencontroller repliziert werden. Ereignisse im Ereignisprotokoll AD DS angeben, dass ein Problem mit DNS-namensauflösung vorhanden ist, sollten Sie die Liste der DNS-Server in den Internetprotokolleigenschaften dieses Computers die IP-Adresse von einem anderen DNS-Server für diese Domäne hinzu. Dieses Ereignis wird protokolliert alle zwei Minuten, bis der AD DS hat signalisiert, dass die erste Synchronisierung erfolgreich abgeschlossen wurde.|  
|**4015**|DNS-Serverdienst|Der DNS-Server ist einen Schwerwiegender Fehler aus dem Active Directory aufgetreten. Überprüfen Sie, dass Active Directory ordnungsgemäß funktioniert. Die erweiterten fehlerdebuginformationen (die eventuell leer ist) ist "" ". Die Ereignisdaten enthalten den Fehlercode.|  
|**4000**|DNS-Serverdienst|Der DNS-Server konnte Active Directory nicht öffnen.  Dieser DNS-Server ist zur Verwendung von Informationen aus dem Verzeichnis für diese Zone konfiguriert und kann die Zone ohne laden.  Überprüfen Sie, dass Active Directory ordnungsgemäß funktioniert, und Laden Sie die Zone. Die Daten enthalten Fehlerinformationen.|  
|**4013**|DNS-Serverdienst|Der DNS-Server wartet für Active Directory-Domänendienste (AD DS) zu signalisieren, dass die erstsynchronisierung des Verzeichnisses abgeschlossen wurde. Der DNS-Serverdienst kann nicht gestartet, bis die erste Synchronisierung abgeschlossen ist, da wichtige DNS-Daten möglicherweise noch nicht auf diesen Domänencontroller repliziert werden. Ereignisse im Ereignisprotokoll AD DS angeben, dass ein Problem mit DNS-namensauflösung vorhanden ist, sollten Sie die Liste der DNS-Server in den Internetprotokolleigenschaften dieses Computers die IP-Adresse von einem anderen DNS-Server für diese Domäne hinzu. Dieses Ereignis wird protokolliert alle zwei Minuten, bis der AD DS hat signalisiert, dass die erste Synchronisierung erfolgreich abgeschlossen wurde.|  
|**2**|DNS-Serverdienst|Der DNS-Server wurde gestartet.|  
|**4**|DNS-Serverdienst|Der DNS-Server hat das Laden von Zonen im Hintergrund beendet. Alle Zonen sind nun für DNS-Aktualisierungen und zonenübertragungen, verfügbar, sofern ihre jeweilige Konfiguration dies zulässt.|  
  
##### <a name="file-replication-service-event-log"></a>Datei Ereignisprotokoll des Dateireplikationsdienstes  
Der Dateireplikationsdienst synchronisiert während des Klonvorgangs nicht autoritativ von einem Partner. Der Klonvorgang erreicht dies durch Löschen der NTFRS-Datenbankdateien und unveränderten Inhalten von SYSVOL zur Verwendung als zuvor per Seeding hinzugefügte Daten. Die zwei Synchronisierungsversuche sind erwartet.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**13562**|NTFRS-Dienst|Im folgenden sehen die Zusammenfassung der Warnungen und Fehler, die vom Dateireplikationsdienst während Konfigurationsinformationen Abfragen der Domäne Domänencontrollers DC2.root.fabrikam.com FRS-Replikatsatz festgelegt werden.<br /><br />Konnte nicht auf einen Domänencontroller binden. Wird beim nächsten Abrufzyklus erneut versuchen.|  
|**13502**|NTFRS-Dienst|Der Dateireplikationsdienst wird angehalten.|  
|**13565**|NTFRS-Dienst|Der Dateireplikationsdienst wird der Systemdatenträger mit Daten von einem anderen Domänencontroller initialisiert. Computer DC2 kann nicht zum Domänencontroller benannt werden, bis dieser Vorgang abgeschlossen ist. Das Systemvolumen wird dann als SYSVOL geteilt werden.<br /><br />Geben Sie Folgendes ein, um die SYSVOL-Freigabe, an der Eingabeaufforderung zu überprüfen:<br /><br />NET share<br /><br />Wenn der Dateireplikationsdienst den Initialisierungsprozess beendet, wird die SYSVOL-Freigabe angezeigt.<br /><br />Die Initialisierung des Systemdatenträgers kann einige Zeit in Anspruch nehmen. Die Zeit hängt von der Datenmenge im Systemdatenträger, der Verfügbarkeit anderer Domänencontroller, und das Intervall der Replikation zwischen Domänencontrollern.|  
|**13501**|NTFRS-Dienst|Der Dateireplikationsdienst wird gestartet.|  
|**13502**|NTFRS-Dienst|Der Dateireplikationsdienst wird angehalten.|  
|**13503**|NTFRS-Dienst|Der Dateireplikationsdienst wurde beendet.|  
|**13565**|NTFRS-Dienst|Der Dateireplikationsdienst wird der Systemdatenträger mit Daten von einem anderen Domänencontroller initialisiert. Computer DC2 kann nicht zum Domänencontroller benannt werden, bis dieser Vorgang abgeschlossen ist. Das Systemvolumen wird dann als SYSVOL geteilt werden.<br /><br />Geben Sie Folgendes ein, um die SYSVOL-Freigabe, an der Eingabeaufforderung zu überprüfen:<br /><br />NET share<br /><br />Wenn der Dateireplikationsdienst den Initialisierungsprozess beendet, wird die SYSVOL-Freigabe angezeigt.<br /><br />Die Initialisierung des Systemdatenträgers kann einige Zeit in Anspruch nehmen. Die Zeit hängt von der Datenmenge im Systemdatenträger, der Verfügbarkeit anderer Domänencontroller, und das Intervall der Replikation zwischen Domänencontrollern.|  
|**13501**|NTFRS-Dienst|Der Dateireplikationsdienst wird gestartet.|  
|**13553**|NTFRS-Dienst|Der Dateireplikationsdienst hinzugefügt erfolgreich. diesen Computer dem folgenden Replikatsatz:<br /><br />"DOMAIN SYSTEMVOLUME (SYSVOL-FREIGABE)"<br /><br />Informationen im Zusammenhang mit diesem Ereignis sind unten angezeigt:<br /><br />DNS-Name des Computers ist*<Domain Controller FQDN>*<br /><br />Set-Mitgliedsname ist*<Domain Controller>*<br /><br />Set-Stammpfad ist*<path>*<br /><br />Pfad des replikatstagingverzeichnisses ist*<path>*<br /><br />Replikatsarbeitsverzeichnisses ist*<path>*|  
|**13520**|NTFRS-Dienst|Der Dateireplikationsdienst hat die vorhandenen Dateien im verschoben <path>auf * <path> *\NtFrs_PreExisting___See_EventLog.<br /><br />Der Dateireplikationsdienst kann löschen Sie die Dateien in * <path> *\NtFrs_PreExisting___See_EventLog jederzeit. Dateien können löschen gespeichert werden, kopieren sie Sie von * <path> *\NtFrs_PreExisting___See_EventLog. Kopieren der Dateien in c:\windows\sysvol\domain kann zu Namenskonflikten führen, wenn die Dateien auf einem anderen replizierenden bereits vorhanden sind.<br /><br />In einigen Fällen kann der Dateireplikationsdienst eine Datei kopieren * <path> *\NtFrs_PreExisting___See_EventLog nach * <path> * anstatt die Datei von einem anderen replizierenden.<br /><br />Speicherplatz zu einem beliebigen Zeitpunkt wiederhergestellt werden kann, durch das Löschen der Dateien in * <path> *\NtFrs_PreExisting___See_EventLog. "|  
|**13508**|NTFRS-Dienst|er Dateireplikationsdienst hat Probleme, die die Replikation von * \\\\ <Domain Controller FQDN> * auf * <Domain Controller> * für * <path> * mithilfe der<br /><br />DNS name *\\\\<Domain Controller FQDN>*. FRS versucht weiterhin.<br /><br />Es folgen einige Ursachen für diese Warnung angezeigt.<br /><br />[1] der Dateireplikationsdienst kann nicht den DNS-Namen ordnungsgemäß auflösen * \\\\ <Domain Controller FQDN> * von diesem Computer.<br /><br />[2] der Dateireplikationsdienst wird nicht ausgeführt, auf * \\\\ <Domain Controller FQDN> *.<br /><br />[3] die Topologieinformationen in den Active Directory Domain Services für dieses Replikat wurde noch nicht auf allen Domänencontrollern repliziert.<br /><br />Einmal pro Verbindung, nachdem das Problem behoben ist angezeigt wird, eine andere Meldung im Ereignisprotokoll, der angibt, dass die Verbindung hergestellt wurde, wird diese Ereignisprotokollnachricht angezeigt.|  
|**13509**|NTFRS-Dienst|Der Dateireplikationsdienst hat die Replikation von aktiviert * \\\\ <Domain Controller FQDN> * auf * <Domain Controller> * für * <Path> * nach wiederholten versuchen.|  
|**13516**|NTFRS-Dienst|Der Dateireplikationsdienst wird nicht mehr durch den Computer verhindert * <Domain Controller> * zu einem Domänencontroller. Der Systemdatenträger wurde erfolgreich initialisiert und wurde der Netlogon-Dienst benachrichtigt, dass der Systemdatenträger jetzt als SYSVOL freigegeben werden kann.<br /><br />Geben Sie "net Share" für die SYSVOL-Freigabe zu überprüfen. "|  
  
##### <a name="dfs-replication-event-log"></a>Ereignisprotokoll der DFS-Replikation  
Die DFSR-Dienste werden während des Klonvorgangs nicht autoritativ von einem Partner synchronisiert. Der Klonvorgang erreicht dies durch Löschen der DFSR-Datenbankdateien und unveränderten Inhalten von SYSVOL zur Verwendung als zuvor per Seeding hinzugefügte Daten. Die zwei Synchronisierungsversuche sind erwartet.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**1004**|DFSR|Der DFS-Replikationsdienst wurde gestartet.|  
|**1314**|DFSR|Der DFS-Replikationsdienst hat Debugprotokolldateien erfolgreich konfiguriert.<br /><br />Weitere Informationen:<br /><br />Pfad der Debugprotokolldatei: C:\Windows\debug|  
|**6102**|DFSR|Der DFS-Replikationsdienst hat den WMI-Anbieter erfolgreich registriert.|  
|**1206**|DFSR|Der DFS-Replikationsdienst wird zum Domänencontroller DC2.corp.contoso.com zum Zugriff auf Konfigurationsinformationen erfolgreich hergestellt.|  
|**1210**|DFSR|Der DFS-Replikationsdienst werden erfolgreich RPC-Listener für eingehende replikationsanforderungen eingerichtet.<br /><br />Weitere Informationen:<br /><br />Port: 0"|  
|**4614**|DFSR|Der DFS-Replikationsdienst hat SYSVOL im lokalen Pfad C:\Windows\SYSVOL\domain und wartet auf die erste Replikation auszuführen. Der replizierte Ordner bleibt in einem ersten Synchronisierungsstatus, bis er mit seinem Partner repliziert wurde. Wenn der Server wurde versucht, die höher gestuft auf einen Domänencontroller, der Domänencontroller nicht ankündigen und als Domänencontroller ausgeführt wird, bis dieses Problem behoben ist. Dies kann vorkommen, wenn der angegebene Partner sich auch in einem ersten Synchronisierungsstatus befindet, oder auf diesem Server oder dem Synchronisierungspartner zugriffsverletzungen aufgetreten sind. Wenn dieses Ereignis während der Migration von SYSVOL aus der Windows-Verwaltungsinstrumentation (File Replication Service, FRS) zur DFS-Replikation aufgetreten ist, werden Änderungen nicht repliziert, bis dieses Problem behoben ist. Dies kann dazu führen, dass den SYSVOL-Ordner auf diesem Server mit anderen Domänencontrollern synchronisiert sind.<br /><br />Weitere Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners:*<GUID>*<br /><br />Replikationsgruppenname: Domain Systemvolume<br /><br />Replikationsgruppenkennung:*<GUID>*<br /><br />Mitgliedskennung:*<GUID>*<br /><br />Read-Only: 0|  
|**4604**|DFSR|Der DFS-Replikationsdienst hat den SYSVOL-replizierten Ordner unter dem lokalen Pfad C:\Windows\SYSVOL\domain erfolgreich initialisiert. Dieses Mitglied hat die erste Synchronisierung von SYSVOL mit Partner dc1.corp.contoso.com abgeschlossen. Um das Vorhandensein der SYSVOL-Freigabe zu überprüfen, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie "" net Share"".<br /><br />Weitere Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners:*<GUID>*<br /><br />Replikationsgruppenname: Domain Systemvolume<br /><br />Replikationsgruppenkennung:*<GUID>*<br /><br />Mitgliedskennung:*<GUID>*<br /><br />Sync-Partner:*<domain controller FQDN>*|  
  
## <a name="BKMK_TshootVDCSafeRestore"></a>Problembehandlung bei der sichere Wiederherstellung des virtualisierten Domänencontrollers  
  
### <a name="tools-for-troubleshooting"></a>Tools zur Problembehandlung  
  
#### <a name="logging-options"></a>Optionen für die Protokollierung  
Die integrierten Protokolle sind das wichtigste Tool für die Behandlung von Problemen mit Domain Controller, sicheren momentaufnahmenwiederherstellung. Alle diese Protokolle sind aktiviert und standardmäßig für maximale Ausführlichkeit konfiguriert.  
  
|||  
|-|-|  
|**Vorgang**|**Protokoll**|  
|**Erstellung der Momentaufnahme**|-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\windows\hyper-V-Worker|  
|**Wiederherstellung einer Momentaufnahme**|-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\verzeichnisdienst<br />-Ereignis protokoll\system<br />-Ereignisanzeige\windows-protokoll\anwendung Ereignis<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dateireplikationsdienst<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dfs-Replikation<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\dns<br />-Ereignis ereignisanzeige\anwendungs- und dienstprotokolle\windows\hyper-V-Worker|  
  
#### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Konfiguration des Domänencontrollers  
Verwenden Sie zum Beheben von Problemen, die nicht durch Protokolle erklärt werden die folgenden Tools als Ausgangspunkt verwendet:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   Netzwerkmonitor 3.4  
  
#### <a name="BKMK_TshhotSafeRestore"></a>Allgemeine Methodik zur Problembehandlung bei der sicheren Wiederherstellung des Domänencontrollers  
  
1.  Wird die sichere momentaufnahmenwiederherstellung erwartet aber Probleme?  
  
    1.  Untersuchen Sie das Verzeichnisdienst-Ereignisprotokoll  
  
        1.  Gibt es momentaufnahmenwiederherstellung Fehler?  
  
        2.  Gibt es AD-Replikationsfehler?  
  
    2.  Überprüfen Sie das Systemereignisprotokoll  
  
        1.  Gibt es Kommunikationsfehler?  
  
        2.  Gibt es AD-Fehler?  
  
2.  Ist die sichere momentaufnahmenwiederherstellung unerwartet?  
  
    1.  Untersuchen Sie Überwachungsprotokolle des Hypervisors, um zu bestimmen, wer oder was einen Rollback verursacht wurde.  
  
    2.  Wenden Sie sich an alle Administratoren des Hypervisors und befragen Sie sie, wer ein Rollback des virtuellen Computers ohne Benachrichtigung ausgeführt.  
  
3.  Ist der Server implementierende USN-rollbackschutz und wiederhergestellt nicht sicher?  
  
    1.  Untersuchen Sie das Verzeichnisdienst-Ereignisprotokoll für eine nicht unterstützten Hypervisor oder Integration services  
  
    2.  Untersuchen Sie das Betriebssystem, und überprüfen Sie die Ausführung von Windows Server 2012?  
  
### <a name="BKMK_TshootSpecificSafeRestore"></a>Problembehandlung bei bestimmten Problemen  
  
#### <a name="events"></a>Ereignisse  
Alle virtualisiert Domain Controller sicheren momentaufnahmenwiederherstellung Ereignisse in das Verzeichnisdienst-Ereignisprotokoll des wiederhergestellten Domänencontrollers VM zu schreiben. Die Ereignisprotokolle der Anwendung, System, File Replication Service und DFS-Replikation möglicherweise auch nützliche Problembehandlungsinformationen für fehlgeschlagene Wiederherstellungsvorgänge enthalten.  
  
Im folgenden finden Sie die Windows Server 2012 safe Restore-spezifische Ereignisse im Verzeichnisdienst-Ereignisprotokoll.  
  
|||  
|-|-|  
|**Ereignis-ID**|**2170**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Warnung|  
|**Nachricht**|Eine Änderung der Generations-ID wurde erkannt.<br /><br />In DS (Alter Wert) zwischengespeicherte Generations-ID: %1<br /><br />Generation-ID des virtuellen Computers (neuer Wert): %2<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. *<COMPUTERNAME>*erstellt eine neue Aufruf-ID zur Wiederherstellung des Domänencontrollers. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen der Inhalte einer Active Directory-Domänendienste-Datenbank ist zum Wiederherstellen einer systemstatussicherung, die mit einer sicherungsanwendung von Active Directory-Domänendienste.|  
|**Hinweise und Lösungen**|Dies ist ein Erfolgsereignis, wenn die Momentaufnahme erwartet war. Wenn dies nicht der Fall ist, untersuchen Sie die Hyper-V-Worker-Ereignisprotokoll, oder wenden Sie sich an den hypervisoradministrator.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2174**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Der Domänencontroller ist weder ein virtuelles Klon noch eine wiederhergestellte Domänencontroller Momentaufnahme.|  
|**Hinweise und Lösungen**|Erwartetes Ereignis beim Starten von physischen Domänencontrollern oder virtualisierten Domänencontrollern, die nicht von einer Momentaufnahme wiederhergestellt|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2181**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Die Transaktion wurde aufgrund der virtuellen Maschine in einem vorherigen Zustand zurückgesetzt wird abgebrochen.  Dies tritt ein, nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Transaktionen verfolgen die VM-Generations-ID ändern|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2185**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*den FRS oder DFSR-Dienst verwendet, um den Ordner "SYSVOL" repliziert wird beendet.<br /><br />Service: %1<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Dies erfolgt durch Beenden der FRS oder DFSR-Dienst verwendet wird, um den Ordner "SYSVOL" repliziert und mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung. Wenn FRS oder DFSR-Dienst neu gestartet wird, wird das Ereignis 2187 protokolliert.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Alle SYSVOL-Daten auf diesem Domänencontroller wird durch die Kopie eines Partnerdomänencontrollers ersetzt.|  
|**Ereignis-ID**|2186|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Beenden des FRS oder DFSR-Diensts zum Replizieren des SYSVOL-Ordners verwendet.<br /><br />Service: %1<br /><br />Fehlercode: % 2<br /><br />Fehler Meldung: %3<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Dies erfolgt durch das Beenden des FRS oder der DFS-Replikationsdienst zum Replizieren des SYSVOL-Ordners verwendet, und starten Sie es dann mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung. *<COMPUTERNAME>*Fehler beim Beenden des aktuellen ausgeführten Diensts und die nicht autoritative Wiederherstellung nicht abgeschlossen werden kann. Führen Sie manuell eine nicht autoritative Wiederherstellung aus.|  
|**Hinweise und Lösungen**|Überprüfen Sie die System-, FRS- und DFSR-Ereignisprotokolle auf Weitere Informationen.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2187**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*der FRS oder DFSR-Dienst verwendet, um den Ordner "SYSVOL" repliziert werden gestartet.<br /><br />Service: %1<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*erforderlich, um eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Dies wurde durch Beenden der FRS oder DFSR-Dienst verwendet wird, um den Ordner "SYSVOL" repliziert und mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung durchgeführt.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Alle SYSVOL-Daten auf diesem Domänencontroller wird durch die Kopie eines Partnerdomänencontrollers ersetzt.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2188**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Starten des FRS oder DFSR-Diensts zum Replizieren des SYSVOL-Ordners verwendet.<br /><br />Service: %1<br /><br />Fehlercode: % 2<br /><br />Fehler Meldung: %3<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden muss. Dies erfolgt durch Beenden der FRS oder DFSR-Dienst zum Replizieren von SYSVOL verwendet und mit geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung. *<COMPUTERNAME>*Fehler beim Starten des FRS oder DFSR-Diensts zum Replizieren des SYSVOL-Ordners verwendet und die nicht autoritative Wiederherstellung nicht abgeschlossen werden kann. Führen Sie eine nicht autoritative Wiederherstellung manuell, und starten Sie den Dienst neu.|  
|**Hinweise und Lösungen**|Überprüfen Sie die System-, FRS- und DFSR-Ereignisprotokolle auf Weitere Informationen.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2189**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*Legen Sie die folgenden Registrierungswerte, während eine nicht autoritative Wiederherstellung der SYSVOL-Replikat initialisiert werden:<br /><br />Registrierung: %1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden muss. Dies erfolgt durch Beenden der FRS oder DFSR-Dienst verwendet wird, um den Ordner "SYSVOL" repliziert und mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Alle SYSVOL-Daten auf diesem Domänencontroller wird durch die Kopie eines Partnerdomänencontrollers ersetzt.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2190**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Legen Sie die folgenden Registrierungswerte während einer nicht autoritativen Wiederherstellung das SYSVOL-Replikat initialisiert werden konnte:<br /><br />Registrierung: %1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Fehlercode: % 4<br /><br />Fehler Meldung: %5<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, der die Domänencontrollerrolle hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden muss. Dies erfolgt durch Beenden der FRS oder DFSR-Dienst verwendet wird, um den Ordner "SYSVOL" repliziert und mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung. *<COMPUTERNAME>*Fehler beim Festlegen der oben stehenden Registrierungswerte und die nicht autoritative Wiederherstellung nicht abgeschlossen werden kann. Führen Sie manuell eine nicht autoritative Wiederherstellung aus.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Anwendung und Systemereignisprotokolle. Überprüfen Sie drittanbieteranwendungen, die möglicherweise registrierungsaktualisierungen blockieren.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2200**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*Initialisiert Replikation, um die Domänencontroller, die aktuellen Stand zu bringen. Wenn die Replikation abgeschlossen ist, wird Ereignis 2201 protokolliert.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Kennzeichnet den Beginn einer eingehenden Replikation.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2201**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*hat die Replikation, um die Domänencontroller, die aktuellen Stand zu bringen.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Kennzeichnet das Ende einer eingehenden Replikation.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2202**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*Fehler bei der Replikation auf den Domänencontroller, auf dem neuesten Stand zu bringen. Der Domänencontroller wird nach der nächsten periodischen Replikation aktualisiert werden.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Ereignisprotokolle Verzeichnisdienste und System. Verwenden Sie repadmin.exe, um eine Replikation, und notieren Sie alle Fehler.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2204**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*eine Änderung der VM-Generations-ID wurde erkannt werden. Die Änderung bedeutet, dass der virtuelle Domänencontroller in einem vorherigen Zustand wiederhergestellt wurde. *<COMPUTERNAME>*führt die folgenden Vorgänge aus, um den wiederhergestellten Domänencontroller vor möglichen datenabweichungen zu schützen und Sicherheitsprinzipale mit doppelten SIDs zu schützen:<br /><br />Erstellen Sie eine neue Aufruf-ID<br /><br />Der aktuelle RID-Pool ungültig<br /><br />Besitz FSMO-Rollen werden am nächsten eingehenden Replikation überprüft werden. Während dieses Fenster sollte die Domänencontroller eine FSMO-Rolle ist diese Rolle nicht möglich.<br /><br />Starten Sie die SYSVOL-Replikation wird wiederhergestellt.<br /><br />Starten der Replikation, um den wiederhergestellten Domänencontroller auf den aktuellen Zustand zu bringen.<br /><br />Ein neuer RID-Pool angefordert.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Das erklärt die verschiedenen Vorgänge zum Zurücksetzen, die als Teil des sicheren Wiederherstellungsvorgangs ausgeführt werden.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2205**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*der aktuelle RID-Pool ungültig, nachdem der virtuelle Domänencontroller in vorherigen Zustand wiederhergestellt wurde.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Der lokale RID-Pool muss zerstört werden, da der Domänencontroller Zeitreise gemacht hat und sie möglicherweise bereits ausgestellt wurde.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2206**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|FEHLER|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim der aktuelle RID-Pool ungültig gemacht, nachdem der virtuelle Domänencontroller in vorherigen Zustand wiederhergestellt wurde.<br /><br />Zusätzliche Daten:<br /><br />Fehlercode: %1<br /><br />Fehlerwert: %2|  
|**Hinweise und Lösungen**|Überprüfen Sie die Ereignisprotokolle Verzeichnisdienste und System. Überprüfen Sie, dass der RID-Master online ist von diesem Server mit Dcdiag.exe/Test: RidManager erreicht werden kann|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2207**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|FEHLER|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Wiederherstellen, nachdem der virtuelle Domänencontroller in vorherigen Zustand wiederhergestellt wurde. Ein Neustart im Verzeichnisdienst-Wiederherstellungsmodus wurde angefordert. Überprüfen Sie vorherige Ereignisse für Weitere Informationen.|  
|**Hinweise und Lösungen**|Überprüfen Sie die Ereignisprotokolle Verzeichnisdienste und System.|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2208**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Information|  
|**Nachricht**|*<COMPUTERNAME>*Gelöschte DFSR-Datenbanken während einer nicht autoritativen Wiederherstellung SYSVOL-Replikat initialisiert werden.|  
|**Hinweise und Lösungen**|Beim Wiederherstellen einer Momentaufnahme erwartet. Dadurch wird sichergestellt, dass DFSR SYSVOL nicht autoritativ von einem Partnerdomänencontroller synchronisiert. Beachten Sie, dass alle anderen von DFSR replizierten Ordner auf demselben Volume wie SYSVOL ebenfalls nicht autoritativ (Domäne synchronisiert, Domänencontroller nicht mit benutzerdefinierten Host empfohlen, dass DFSR auf demselben Volume wie SYSVOL festgelegt).|  
  
|||  
|-|-|  
|**Ereignis-ID**|**2209**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Schweregrad**|Fehler|  
|**Nachricht**|*<COMPUTERNAME>*Fehler beim Löschen der DFSR-Datenbanken.<br /><br />Zusätzliche Daten:<br /><br />Fehlercode: %1<br /><br />Fehlerwert: %2<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>*eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden muss. Für DFSR wird dies durch das Beenden des DFSR-Diensts, löschen die DFSR-Datenbanken und der Dienst neu gestartet. Beim Neustart DFSR wird die Datenbanken und die erstsynchronisierung gestartet.|  
|**Hinweise und Lösungen**|Untersuchen Sie das DFSR-Ereignisprotokoll.|  
  
#### <a name="error-messages"></a>Fehlermeldungen  
Es gibt keine direkten interaktiven Fehler für die sichere momentaufnahmenwiederherstellung für virtualisierte Domänencontroller ist fehlgeschlagen. Alle kloninformationen werden in den Verzeichnisdienst-Ereignisprotokollen. Natürlich manifestieren sich alle kritischen Replikations- oder Werbung Fehler selbst als Symptome an anderer Stelle.  
  
#### <a name="known-issues-and-support-scenarios"></a>Bekannte Probleme und Supportszenarien  
Die [allgemeine Methodik zur Problembehandlung bei der sicheren Wiederherstellung von Domänencontrollern](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootSpecificSafeRestore) helfen beim Beheben der meisten Probleme.  
  
|||  
|-|-|  
|**Problem**|**Neuer Sicherheitsprinzipale kann nicht auf kürzlich sicher wiederhergestellten Domänencontroller erstellt werden.**|  
|**Symptome**|Nach der Wiederherstellung einer Momentaufnahme versucht, auf einen neuen Sicherheitsprinzipal (Benutzer, Computer, Gruppe) auf diesem Fehler fehl mit erstellen:<br /><br />Fehler 0x2010<br /><br />Der Verzeichnisdienst konnte keinen relativen Bezeichner zuweisen.|  
|**Lösung und Hinweise**|Dieses Problem wird durch die wiederhergestellten Computer veraltete Kenntnis der RID-Master-FSMO-Rolle verursacht. Wenn die Rolle auf diesem oder einem anderen Domänencontroller verschoben, nachdem eine Momentaufnahme erstellt wurde und dieses dann wiederhergestellt, haben der wiederhergestellten Domänencontroller keinen Kenntnisse der RID-Master, bis die erste Replikation abgeschlossen ist.<br /><br />Um das Problem zu beheben, können Sie Active Directory-Replikation abgeschlossen an den wiederhergestellten Domänencontroller eingehend. Wenn immer noch nicht funktioniert, überprüfen Sie, dass alle Domänencontroller die korrekte Kenntnis darüber haben, von denen Domänencontroller der RID-Master gehostet.|  
  
|||  
|-|-|  
|**Problem**|**Auf wiederhergestellten Domänencontrollern nicht freigeben SYSVOL, ankündigen**|  
|**Symptome**|Nach der Wiederherstellung einer Momentaufnahme, eine oder mehrere Domänencontroller nicht anzeigen Sysvol nicht freigeben und müssen nicht auf dem neuesten Stand SYSVOL-Inhalte|  
|**Lösung und Hinweise**|Des Domänencontrollers sind ein funktionierendes SYSVOL-Replikat nicht vorhanden, die ordnungsgemäß mit DFSR oder FRS repliziert wird Dieses Problem steht nicht im Zusammenhang mit der sicheren aber wahrscheinlich manifest als sichere Wiederherstellung Problem, da der Kunde das andere Replikationsproblem nicht wiederhergestellte Domänencontroller betrifft beeinflussen nicht bewusst war|  
  
### <a name="advanced-troubleshooting"></a>Erweiterte Problembehandlung  
Dieses Modul sucht, um erweiterte Fehlerbehandlung mit *arbeiten* Protokolle als Beispiele mit einer Erklärung der Vorgänge. Wenn Sie verstehen, wie eine erfolgreich virtualisierte Domänencontroller-Operation aussieht, werden Fehler in Ihrer Umgebung offensichtlich. Diese Protokolle werden nach ihrer Quelle, mit aufsteigend in der Reihenfolge dargestellt *erwartet* Ereignisse im Zusammenhang mit einem geklonten Domänencontroller in jedem Protokoll.  
  
#### <a name="restoring-a-domain-controller-that-replicates-sysvol-using-dfsr"></a>Wiederherstellen eines Domänencontrollers, der SYSVOL über DFSR repliziert  
  
##### <a name="directory-services-event-log"></a>Verzeichnisdienst-Ereignisprotokoll  
Das Verzeichnisdienst-Ereignisprotokoll enthält den Großteil der Betriebsinformationen für die sichere Wiederherstellung. Der Hypervisor ändert die VM-Generations-ID und der NTDS-Dienst bemerkt dies, macht den RID-Pool ungültig und ändert die aufrufkennung. Die neue VM-Generations-ID ist festlegen und der Server repliziert AD-Daten eingehend. Der DFSR-Dienst wurde beendet und die Datenbank, die SYSVOL hostet wird gelöscht, wodurch eine nicht autoritative Synchronisierung eingehende. Der hohe USN-Grenzwert wird angepasst.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**2170**|ActiveDirectory_DomainService|Eine Änderung der Generations-ID wurde erkannt.<br /><br />In DS (Alter Wert) zwischengespeicherte Generations-ID:<br /><br />*<number>*<br /><br />Generation-ID des virtuellen Computers (neuer Wert):<br /><br />*<number>*<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Active Directory-Domänendiensten wird eine neue Aufruf-ID zur Wiederherstellung des Domänencontrollers erstellt. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen der Inhalte einer Active Directory-Domänendienste-Datenbank ist zum Wiederherstellen einer systemstatussicherung, die mit einer Active Directory-Domänendienste-sicherungsanwendung."|  
|**2181**|ActiveDirectory_DomainService|Die Transaktion wurde aufgrund der virtuellen Maschine in einem vorherigen Zustand zurückgesetzt wird abgebrochen.  Dies tritt ein, nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration.|  
|**2204**|ActiveDirectory_DomainService|Active Directory-Domänendienste wurde eine Änderung der VM-Generations-ID erkannt. Die Änderung bedeutet, dass der virtuelle Domänencontroller in einem vorherigen Zustand wiederhergestellt wurde. Active Directory Domain Services, führt die folgenden Vorgänge aus, um den wiederhergestellten Domänencontroller vor möglichen datenabweichungen zu schützen und Sicherheitsprinzipale mit doppelten SIDs zu schützen:<br /><br />Erstellen Sie eine neue Aufruf-ID<br /><br />Der aktuelle RID-Pool ungültig<br /><br />Besitz FSMO-Rollen werden am nächsten eingehenden Replikation überprüft werden. Während dieses Fenster sollte die Domänencontroller eine FSMO-Rolle ist diese Rolle nicht möglich.<br /><br />Starten Sie die SYSVOL-Replikation wird wiederhergestellt.<br /><br />Starten der Replikation, um den wiederhergestellten Domänencontroller auf den aktuellen Zustand zu bringen.<br /><br />Ein neuer RID-Pool angefordert."|  
|**2181**|ActiveDirectory_DomainService|Die Transaktion wurde aufgrund der virtuellen Maschine in einem vorherigen Zustand zurückgesetzt wird abgebrochen.  Dies tritt ein, nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration.|  
|**1109**|ActiveDirectory_DomainService|Das InvocationID-Attribut für diesen Verzeichnisserver wurde geändert. Die höchste Aktualisierungssequenznummer zum Zeitpunkt der Erstellung der Sicherung lautet wie folgt:<br /><br />InvocationID-Attribut (Alter Wert):<br /><br />*<GUID>*<br /><br />InvocationID-Attribut (neuer Wert):<br /><br />*<GUID>*<br /><br />Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Die Aufrufkennung geändert wird, wenn von einem Sicherungsmedium, ein Verzeichnisserver wiederhergestellt wird eine beschreibbare Anwendungsverzeichnispartition konfiguriert ist, wurde fortgesetzt wurde, nachdem eine Momentaufnahme des virtuellen Computers angewendet wurde, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Virtualisierte Domänencontroller sollten nicht mithilfe von Momentaufnahmen des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen ist der Inhalt einer Active Directory-Domänendienste-Datenbank wiederherstellen eine systemstatussicherung, die mit einer Active Directory Domain Services-fähige sicherungsanwendung."|  
|**2179**|ActiveDirectory_DomainService|Das MsDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers wurde der folgende Parameter festgelegt:<br /><br />Generations-ID-Attribut:<br /><br />*<number>*|  
|**2200**|ActiveDirectory_DomainService|Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. Active Directory-Domänendienste initialisiert Replikation, um die Domänencontroller, die aktuellen Stand zu bringen. Wenn die Replikation abgeschlossen ist, wird Ereignis 2201 protokolliert.|  
|**2201**|ActiveDirectory_DomainService|Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. Active Directory-Domänendienste wurde die Replikation, um die Domänencontroller, die aktuellen Stand zu bringen.|  
|**2185**|ActiveDirectory_DomainService|Active Directory Domain Services, beendet den FRS oder DFSR-Dienst zum Replizieren des SYSVOL-Ordners verwendet.<br /><br />Dienstname:<br /><br />DFSR<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. Active Directory-Domänendiensten muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Dies erfolgt durch Beenden der FRS oder DFSR-Dienst verwendet wird, um den Ordner "SYSVOL" repliziert und mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung. Das Ereignis 2187 protokolliert werden, wenn FRS oder DFSR-Dienst neu gestartet wird."|  
|**2208**|ActiveDirectory_DomainService|Active Directory-Domänendiensten gelöscht DFSR-Datenbanken zum Initialisieren des SYSVOL-Replikats während einer nicht autoritativen Wiederherstellung.<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. Active Directory-Domänendiensten muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Für DFSR wird dies durch das Beenden des DFSR-Diensts, löschen die DFSR-Datenbanken und der Dienst neu gestartet. Beim Neustart DFSR wird die Datenbanken und die erstsynchronisierung gestartet. "|  
|**2187**|ActiveDirectory_DomainService|Active Directory Domain Services gestartet, den FRS oder DFSR-Dienst zum Replizieren des SYSVOL-Ordners verwendet wird.<br /><br />Dienstname:<br /><br />DFSR<br /><br />Active Directory wurde erkannt, dass der virtuelle Computer, die der Domänencontroller hostet in einen früheren Zustand zurückversetzt wurde. Active Directory-Domänendienste erforderlich, um eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Dies wurde durch Beenden der FRS oder DFSR-Dienst verwendet wird, um den Ordner "SYSVOL" repliziert und mit den geeigneten Registrierungsschlüsseln und-Werten zum Auslösen der Wiederherstellung durchgeführt. "|  
|**1587**|ActiveDirectory_DomainService|Dieser Verzeichnisdienst wurde wiederhergestellt, oder um eine Anwendungsverzeichnispartition konfiguriert wurde. Daher hat sich seine replikationsidentität geändert. Ein Partner hat replikationsänderungen dabei die alte Identität angefordert. Die ersten Sequenznummer wurde korrigiert.<br /><br />Der zielverzeichnisdienst, der für das folgende Objekt-GUID hat eine USN, der die USN vorangestellt ist, an dem der lokale Verzeichnisdienst vom Sicherungsmedium wiederhergestellt wurde, beginnend Änderungen angefordert wird.<br /><br />Objekt-GUID:<br /><br />*<GUID> (<FQDN of partner domain controller>)*<br /><br />Aktualisierungssequenznummer zur Zeit der Wiederherstellung:<br /><br />*<number>*<br /><br />Daher wurde der Aktualitätsvektor des zielverzeichnisdienstes mit den folgenden Einstellungen konfiguriert.<br /><br />Vorherige Datenbank-GUID:<br /><br />*<GUID>*<br /><br />Vorherige Objekt-Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Vorherige Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Neue Datenbank-GUID:<br /><br />*<GUID>*<br /><br />Neues Objekt-Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Neue Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<number>*|  
  
##### <a name="system-event-log"></a>Systemereignisprotokoll  
Das Systemereignisprotokoll weist darauf hin, die Computer-Zeit, die tritt auf, wenn einen virtueller Computer im Offlinemodus wieder online geschaltet und mit synchronisieren. Der RID-Pool ungültig macht, und der DFSR- oder FRS-Dienst wird neu gestartet.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**1**|Kernel-Allgemein|Die Systemzeit wurde geändert, um *?<now>* von *< snapshot-Datum/Uhrzeit >*.<br /><br />Änderung der Grund: Eine Anwendung oder Systemkomponente hat die Zeit geändert.|  
|**16654**|Verzeichnisdienste-SAM|Ein Pool aus kontobezeichnern (RIDs) wurde ungültig gemacht. Dies kann in den folgenden zu erwartenden Fällen auftreten:<br /><br />1. ein Domänencontroller ist von einer Sicherung wiederhergestellt.<br /><br />2. ein Domänencontroller, die auf einem virtuellen Computer wird aus einer Momentaufnahme wiederhergestellt.<br /><br />3. ein Administrator hat den Pool manuell ungültig gemacht.<br /><br />Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=226247 Weitere Informationen.|  
|**7036**|Dienststeuerungs-Manager|Der DFS-Replikationsdienst wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der DFS-Replikationsdienst wird jetzt ausgeführt.|  
  
##### <a name="application-event-log"></a>Anwendungsereignisprotokoll  
Das Anwendungsereignisprotokoll Notizen zu starten und Beenden der DFSR-Datenbank.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**103**|ESENT|DFSRs (1360) \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.141, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.016, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.|  
|**102**|ESENT|DFSRs (532) \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: das Datenbankmodul (6.02.8189.0000 startet) eine neue Instanz (0) gestartet wird.|  
|**105**|ESENT|DFSRs (532) \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: das Datenbankmodul gestartet wurde, eine neue Instanz (0). (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.000.|  
|||DFSRs (532) \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: das Datenbankmodul eine neue Datenbank erstellt (1, \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db). (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.016, [4] 0.062, [5] 0.000, [6] 0.016, [7] 0.000, [8] 0.000, [9] 0.015, [10] 0.000, [11] 0.000.|  
  
##### <a name="dfs-replication-event-log"></a>Ereignisprotokoll der DFS-Replikation  
Der DFSR-Dienst wurde beendet und die Datenbank, die SYSVOL enthält wird gelöscht, wodurch eine nicht autoritative Synchronisierung eingehende.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**1006**|DFSR|Der DFS-Replikationsdienst wird beendet.|  
|**1008**|DFSR|Der DFS-Replikationsdienst wurde beendet.|  
|**1002**|DFSR|Der DFS-Replikationsdienst wird gestartet.|  
|**1004**|DFSR|Der DFS-Replikationsdienst wurde gestartet.|  
|**1314**|DFSR|Der DFS-Replikationsdienst hat Debugprotokolldateien erfolgreich konfiguriert.<br /><br />Weitere Informationen:<br /><br />Pfad der Debugprotokolldatei: C:\Windows\debug|  
|**6102**|DFSR|Der DFS-Replikationsdienst hat den WMI-Anbieter erfolgreich registriert.|  
|**1206**|DFSR|Der DFS-Replikation erfolgreich hergestellt-Domänencontroller * <domain controller FQDN> * zum Zugriff auf Konfigurationsinformationen.|  
|**1210**|DFSR|Der DFS-Replikationsdienst werden erfolgreich RPC-Listener für eingehende replikationsanforderungen eingerichtet.<br /><br />Weitere Informationen:<br /><br />Port: 0|  
|**4614**|DFSR|Der DFS-Replikationsdienst hat SYSVOL im lokalen Pfad C:\Windows\SYSVOL\domain und wartet auf die erste Replikation auszuführen. Der replizierte Ordner bleibt in einem ersten Synchronisierungsstatus, bis er mit seinem Partner repliziert wurde. Wenn der Server wurde versucht, die höher gestuft auf einen Domänencontroller, der Domänencontroller nicht ankündigen und als Domänencontroller ausgeführt wird, bis dieses Problem behoben ist. Dies kann vorkommen, wenn der angegebene Partner sich auch in einem ersten Synchronisierungsstatus befindet, oder auf diesem Server oder dem Synchronisierungspartner zugriffsverletzungen aufgetreten sind. Wenn dieses Ereignis während der Migration von SYSVOL aus der Windows-Verwaltungsinstrumentation (File Replication Service, FRS) zur DFS-Replikation aufgetreten ist, werden Änderungen nicht repliziert, bis dieses Problem behoben ist. Dies kann dazu führen, dass den SYSVOL-Ordner auf diesem Server mit anderen Domänencontrollern synchronisiert sind.<br /><br />Weitere Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners:*<GUID>*<br /><br />Replikationsgruppenname: Domain Systemvolume<br /><br />Replikationsgruppenkennung:*<GUID>*<br /><br />Mitgliedskennung:*<GUID>*<br /><br />Read-Only: 0|  
|**4604**|DFSR|Der DFS-Replikationsdienst hat den SYSVOL-replizierten Ordner unter dem lokalen Pfad C:\Windows\SYSVOL\domain erfolgreich initialisiert. Dieses Mitglied hat die erste Synchronisierung von SYSVOL mit Partner dc1.corp.contoso.com abgeschlossen. Um das Vorhandensein der SYSVOL-Freigabe zu überprüfen, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie "net Share".<br /><br />Weitere Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners:*<GUID>*<br /><br />Replikationsgruppenname: Domain Systemvolume<br /><br />Replikationsgruppenkennung:*<GUID>*<br /><br />Mitgliedskennung:*<GUID>*<br /><br />Sync-Partner:*<partner domain controller FQDN>*|  
  
#### <a name="restoring-a-domain-controller-that-replicates-sysvol-using-frs"></a>Wiederherstellen eines Domänencontrollers, der SYSVOL über FRS repliziert  
Die Datei Replikation-Ereignisprotokoll wird in diesem Fall anstelle der DFSR-Ereignisprotokoll verwendet. Das Anwendungsereignisprotokoll schreibt auch verschiedene FRS-relevante Ereignisse. Die Verzeichnisdienste und Systemereignisprotokoll Nachrichten sind normalerweise dieselben in derselben Reihenfolge wie zuvor beschriebenen.  
  
##### <a name="file-replication-service-event-log"></a>Datei Ereignisprotokoll des Dateireplikationsdienstes  
Der FRS-Dienst wird beendet und neu gestartet, mit einem D2 BURFLAGS-Wert, um SYSVOL nicht autoritativ zu synchronisieren.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**13502**|NTFRS-DIENST|Der Dateireplikationsdienst wird angehalten.|  
|**13503**|NTFRS-DIENST|Der Dateireplikationsdienst wurde beendet.|  
|**13501**|NTFRS-DIENST|Der Dateireplikationsdienst wird gestartet.|  
|**13512**|NTFRS-DIENST|Der Dateireplikationsdienst hat einen aktivierten datenträgerschreibungs-Cache auf dem Laufwerk mit dem Verzeichnis c:\windows\ntfrs\jet auf dem Computer DC4 erkannt. Der Dateireplikationsdienst kann eventuell nicht wiederhergestellt werden, wenn die Stromzufuhr des Laufwerks unterbrochen wird und wichtige Updates verloren.|  
|**13565**|NTFRS-DIENST|Der Dateireplikationsdienst wird der Systemdatenträger mit Daten von einem anderen Domänencontroller initialisiert. Computer DC4 kann nicht zum Domänencontroller benannt werden, bis dieser Vorgang abgeschlossen ist. Das Systemvolumen wird dann als SYSVOL geteilt werden.<br /><br />Geben Sie Folgendes ein, um die SYSVOL-Freigabe, an der Eingabeaufforderung zu überprüfen:<br /><br />NET share<br /><br />Wenn der Dateireplikationsdienst den Initialisierungsprozess beendet, wird die SYSVOL-Freigabe angezeigt.<br /><br />Die Initialisierung des Systemdatenträgers kann einige Zeit in Anspruch nehmen. Die Zeit hängt von der Datenmenge im Systemdatenträger, der Verfügbarkeit anderer Domänencontroller, und das Intervall der Replikation zwischen Domänencontrollern."|  
|**13520**|NTFRS-DIENST|Der Dateireplikationsdienst hat die vorhandenen Dateien im verschoben * <path> * auf * <path> *\NtFrs_PreExisting___See_EventLog.<br /><br />Der Dateireplikationsdienst kann löschen Sie die Dateien in * <path> *\NtFrs_PreExisting___See_EventLog jederzeit. Dateien können löschen gespeichert werden, kopieren sie Sie von * <path> *\NtFrs_PreExisting___See_EventLog. Kopieren der Dateien in * <path> * kann zu Namenskonflikten führen, wenn die Dateien auf einem anderen replizierenden bereits vorhanden sind.<br /><br />In einigen Fällen kann der Dateireplikationsdienst eine Datei kopieren * <path> *\NtFrs_PreExisting___See_EventLog nach * <path> * anstatt die Datei von einem anderen replizierenden.<br /><br />Speicherplatz zu einem beliebigen Zeitpunkt wiederhergestellt werden kann, durch das Löschen der Dateien in * <path> *\NtFrs_PreExisting___See_EventLog.|  
|**13553**|NTFRS-DIENST|Der Dateireplikationsdienst hinzugefügt erfolgreich. diesen Computer dem folgenden Replikatsatz:<br /><br />"DOMAIN SYSTEMVOLUME (SYSVOL-FREIGABE)"<br /><br />Informationen im Zusammenhang mit diesem Ereignis sind unten angezeigt:<br /><br />DNS-Name des Computers ist "*<domain controller FQDN>*"<br /><br />Set-Mitgliedsname ist "*<domain controller name>*"<br /><br />Set-Stammpfad ist "*<path>*"<br /><br />Pfad des replikatstagingverzeichnisses ist "* <path> * "<br /><br />Replikatsarbeitsverzeichnisses ist "*<path>*"|  
|**13554**|NTFRS-DIENST|Der Dateireplikationsdienst hat die folgenden Verbindungen dem Replikatsatz erfolgreich hinzugefügt:<br /><br />"DOMAIN SYSTEMVOLUME (SYSVOL-FREIGABE)"<br /><br />Von "*<partner domain controller FQDN>*"<br /><br />Um ausgehenden "*<partner domain controller FQDN>*"<br /><br />Weitere Informationen kann in folgenden ereignisprotokollmeldungen angezeigt.|  
|**13516**|NTFRS-DIENST|Der Dateireplikationsdienst wird nicht mehr verhindern, dass den Computer DC4 zum Domänencontroller. Der Systemdatenträger wurde erfolgreich initialisiert und wurde der Netlogon-Dienst benachrichtigt, dass der Systemdatenträger jetzt als SYSVOL freigegeben werden kann.<br /><br />Geben Sie "net Share" für die SYSVOL-Freigabe zu überprüfen.|  
  
##### <a name="application-event-log"></a>Anwendungsereignisprotokoll  
Die FRS-Datenbank beendet und startet und wird aufgrund des D2 BURFLAGS-Vorgangs.  
  
||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**327**|ESENT|NTFRS-Dienst (1424) das Datenbankmodul eine Datenbank (1, c:\windows\ntfrs\jet\ntfrs.jdb) getrennt. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.015, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.516, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.063, [12] 0.000.<br /><br />Cache fortgesetzt: 0|  
|**103**|ESENT|NTFRS-Dienst (1424) das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.016, [12] 0.000, [13] 0.000, [14] 0.047, [15] 0.000.|  
|**102**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul (6.02.8189.0000 startet) eine neue Instanz (0) gestartet wird.|  
|**105**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.062, [10] 0.000, [11] 0.141.|  
|**103**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000, [13] 0.015, [14] 0.000, [15] 0.000.|  
|**102**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul (6.02.8189.0000 startet) eine neue Instanz (0) gestartet wird.|  
|**105**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.078, [10] 0.000, [11] 0.109.|  
|**325**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul eine neue Datenbank (1, c:\windows\ntfrs\jet\ntfrs.jdb) erstellt. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.016, [4] 0.016, [5] 0.000, [6] 0.015, [7] 0.000, [8] 0.000, [9] 0.078, [10] 0.016, [11] 0.000.|  
|**103**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.078, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.125, [10] 0.016, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.|  
|**102**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul (6.02.8189.0000 startet) eine neue Instanz (0) gestartet wird.|  
|**105**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.016, [2] 0.000, [3] 0.000, [4] 0.094, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.032, [10] 0.000, [11] 0.000.|  
|**326**|ESENT|NTFRS-Dienst (3000) das Datenbankmodul hat eine Datenbank (1, c:\windows\ntfrs\jet\ntfrs.jdb) angefügt. (Zeit = 0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.015, [3] 0.000, [4] 0.000, [5] 0.016, [6] 0.015, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000.<br /><br />Cache gespeichert: 1|  
  


