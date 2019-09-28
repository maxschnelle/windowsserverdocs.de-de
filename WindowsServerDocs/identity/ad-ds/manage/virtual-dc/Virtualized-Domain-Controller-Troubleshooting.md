---
ms.assetid: 249ba1be-b0d3-4a77-99af-3699074a2b6e
title: Problembehandlung für virtualisierte Domänencontroller
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 42f9807eb09ff633642a90181b3abfacc00ab76b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71409044"
---
# <a name="virtualized-domain-controller-troubleshooting"></a>Problembehandlung für virtualisierte Domänencontroller

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält eine ausführliche Methode für die Problembehandlung virtualisierter Domänencontroller.  

-   [Problembehandlung beim Klonen virtualisierter Domänen Controller](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootVDCCloning)  

-   [Problembehandlung bei der sicheren Wiederherstellung virtualisierter Domänen Controller](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootVDCSafeRestore)  

## <a name="BKMK_Intro"></a>Einführung  
Die wichtigste Methode zur Verbesserung Ihrer Fehlerbehandlungsfertigkeiten ist der Aufbau eines Testlabors und die gründliche Untersuchung von normalen, funktionierenden Szenarien. Wenn Sie auf Fehler treffen, sind diese offensichtlicher und einfacher zu verstehen, da Sie dann ein solides Grundlagenwissen zur Funktionsweise des Heraufstufens von Domänencontrollern erlangt haben. Auf diese Weise können Sie auch Ihre Analyse- und Netzwerkanalysefertigkeiten weiterentwickeln. Dies gilt für alle Technologien für verteilte Systeme, nicht nur für die Bereitstellung virtualisierter Domänencontroller.  

Die wichtigen Elemente für eine erweiterte Fehlerbehandlung bei der Domänencontrollerkonfiguration sind die folgenden:  

1.  Lineare Analyse in Kombination mit einer Fokussierung und Aufmerksamkeit für Details  

2.  Verstehen der Netzwerkerfassungsanalyse  

3.  Verstehen der integrierten Protokolle  

Der erste und zweite Punkt gehen über den Umfang dieses Themas hinaus, aber der dritte Punkt kann ausführlich erläutert werden. Für die Fehlerbehandlung bei virtualisierte Domänencontroller ist eine logische und lineare Methode erforderlich. Wichtig ist, das Problem mit den bereitgestellten Daten anzugehen und nur auf komplexe Tools und Analysen zurückzugreifen, wenn Sie die bereitgestellte Ausgabe und Protokollierung erschöpft haben.  

## <a name="BKMK_TshootVDCCloning"></a>Problembehandlung beim Klonen virtualisierter Domänen Controller  
In diesen Abschnitten werden folgende Themen behandelt:  

-   [Tools für die Problembehandlung](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_Tools)  

-   [Protokollierungs Optionen](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_LoggingOptions)  

-   [Allgemeine Methodik zur Problembehandlung beim Klonen von Domänen Controllern](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_GeneralMethodology)  

-   [Server Core und das Ereignisprotokoll](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_ServerCoreEvents)  

-   [Problembehandlung bei bestimmten Problemen](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_SpecificProblems)  

Die Problembehandlungsstrategie für das Klonen virtueller Domänencontroller basiert auf dem folgenden allgemeinen Format:  

![Problembehandlung bei Virtual DC](media/Virtualized-Domain-Controller-Troubleshooting/ADDS_VDC_TroublehsootingFlowchart.png)  

### <a name="BKMK_Tools"></a>Tools für die Problembehandlung  

#### <a name="BKMK_LoggingOptions"></a>Protokollierungs Optionen  
Die integrierten Protokolle sind das wichtigste Tool für die Problembehandlung beim Klonen von Domänencontrollern. Alle Protokolle sind standardmäßig für maximale Ausführlichkeit aktiviert und konfiguriert.  

|||  
|-|-|  
|**Vorgang**|**Angezeigt**|  
|**Klon**|-Ereignisviewer\windows-Protokolle\System<br />-Ereignisviewer\anwendungs-und dienstprotokolle\verzeichnisdienst<br />-%systemroot%\debug\dcpromo.log|  
|**Ungs**|-%systemroot%\debug\dcpromo.log<br />-Ereignisviewer\anwendungs-und dienstprotokolle\verzeichnisdienst<br />-Ereignisviewer\windows-Protokolle\System<br />-Ereignisviewer\anwendungs-und dienstprotokolle\datei Replikations Dienst<br />-Ereignisviewer\anwendungs-und dienstprotokolle\dfs-Replikation|  

#### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Domänencontroller-Konfiguration  
Die folgenden Tools dienen als Ausgangspunkt bei der Behandlung von Problemen, die nicht durch Protokolle erklärt werden können:  

-   Dcdiag.exe  

-   Repadmin.exe  

-   Netzwerkmonitor 3.4  

### <a name="BKMK_GeneralMethodology"></a>Allgemeine Methodik zur Problembehandlung beim Klonen von Domänen Controllern  

1.  Wird der virtuelle Computer im Verzeichnisdienst-Wiederherstellungsmodus (DS Repair Mode, DSRM) gestartet? Das ist ein Hinweis, dass eine Problembehandlung erforderlich ist. Zum Anmelden beim DSRM verwenden Sie das Konto **.\Administrator**, und geben Sie das DSRM-Kennwort an.  

    1.  Untersuchen Sie die Datei Dcpromo.log.  

        1.  Waren die ersten Schritte beim Klonen erfolgreich, aber ist das Heraufstufen des Domänencontrollers fehlgeschlagen?  

        2.  Weisen Fehler auf Probleme mit dem lokalen Domänencontroller oder mit der AD DS-Umgebung hin, beispielsweise durch vom PDC-Emulator zurückgegebene Fehler?  

    2.  Untersuchen Sie die System- und Verzeichnisdienst-Ereignisprotokolle sowie die Dateien dccloneconfig.xml und CustomDCCloneAllowList.xml.  

        1.  Muss sich eine inkompatible Anwendung in der CustomDCCloneAllowList.xml-Liste „Zulassen“ befinden?  

        2.  Ist die IP-Adresse oder der Computername in der Datei dccloneconfig.xml entweder dupliziert oder ungültig?  

        3.  Ist der Active Directory-Standort in der Datei dccloneconfig.xml ungültig?  

        4.  Ist die IP-Adresse in der Datei dccloningconfig.xml nicht festgelegt und deshalb kein DHCP-Server verfügbar?  

        5.  Ist der PDC-Emulator online und über das RPC-Protokoll verfügbar?  

        6.  Ist der Domänencontroller Mitglied der Gruppe „Klonbare Domänencontroller“? Ist die Berechtigung **Domänencontroller die Erstellung eines Klons von sich selbst erlauben** am Domänenstamm für diese Gruppe festgelegt?  

        7.  Enthält die Datei Dccloneconfig.xml Syntaxfehler, die eine korrekte Analyse verhindern?  

        8.  Wird der Hypervisor unterstützt?  

        9. Ist das Heraufstufen des Domänencontrollers fehlgeschlagen, nachdem das Klonen erfolgreich begonnen hat?  

        10. Wurde die maximale Anzahl von automatisch generierten Domänencontrollernamen (9999) überschritten?  

        11. Ist die MAC-Adresse dupliziert?  

2.  Ist der Hostname des Klons derselbe wie der des Quelldomänencontrollers?  

    1.  Ist eine Dccloneconfig.xml-Datei an einem der zulässigen Speicherorte vorhanden?  

3.  Wird der virtuelle Computer im normalen Modus gestartet und ist das Klonen abgeschlossen, aber der Domänencontroller funktioniert nicht ordnungsgemäß?  

    1.  Überprüfen Sie zunächst, ob der Hostname auf dem Klon geändert wurde. Wenn sich der Hostname unterscheidet, wurde das Klonen zumindest teilweise abgeschlossen.  

    2.  Hat der Domänencontroller eine duplizierte IP-Adresse des Quelldomänencontrollers aus der Datei dccloneconfig.xml, aber war der Quelldomänencontroller während des Klonens offline?  

    3.  Wenn sich der Domänencontroller ankündigt, behandeln Sie das Problem als ein normales Problem nach dem Heraufstufen, das Sie auch ohne das Klonen hätten.  

    4.  Wenn sich der Domänencontroller nicht ankündigt, untersuchen Sie die Verzeichnisdienst-, System-, Anwendungs-, Dateireplikations- und DFS-Replikationsereignisprotokolle auf Fehler nach dem Heraufstufen.  

#### <a name="disabling-dsrm-boot"></a>Deaktivieren des DSRM-Starts  
Nach dem Starten im DSRM aufgrund eines Fehlers, diagnostizieren Sie die Fehlerursache. Wenn die dcpromo.log-Datei nicht darauf hinweist, dass das Klonen nicht erneut versucht werden, beheben Sie die Fehlerursache, und setzen Sie das DSRM-Kennzeichen zurück. Ein fehlerhafter Klon kehrt nicht von allein beim nächsten Neustart in seinen normalen Modus zurück, sondern Sie müssen das DSRM-Startkennzeichen löschen, um den Klonvorgang erneut auszuführen. Für all diese Schritte ist eine Ausführung als erweiterter Administrator erforderlich.  

##### <a name="removing-dsrm-with-msconfigexe"></a>Entfernen von DSRM mit Msconfig.exe  
Verwenden Sie das Systemkonfigurationstool, um den DSRM-Start über eine GUI zu deaktivieren:  

1.  Führen Sie msconfig.exe aus.  

2.  Deaktivieren Sie auf der Registerkarte **Start** unter **Startoptionen** die Option **Abgesicherter Start** (diese Option ist bereits mit der **Active Directory-Reparatur** aktiviert).  

3.  Klicken Sie auf OK, und starten Sie nach Aufforderung neu.  

##### <a name="removing-dsrm-with-bcdeditexe"></a>Entfernen von DSRM mit Bcdedit.exe  
Verwenden Sie den Editor für den Startkonfigurationsdaten-Speicher, um den DSRM-Start über die Befehlszeile zu deaktivieren:  

1.  Öffnen Sie eine CMD-Eingabeaufforderung, und führen Sie den folgenden Befehl aus:  

    ```  
    Bcdedit.exe /deletevalue safeboot  
    ```  

2.  Starten Sie den Computer mit dem folgenden Befehl neu:  

    ```  
    Shutdown.exe /t /0 /r  
    ```  

> [!NOTE]  
> Bcdedit.exe funktioniert auch in einer Windows PowerShell-Konsole. Dabei werden die folgenden Befehle verwendet:  
>   
> Bcdedit.exe /deletevalue safeboot  
>   
> Restart-computer  

### <a name="BKMK_ServerCoreEvents"></a>Server Core und das Ereignisprotokoll  
Die Ereignisprotokolle enthalten einen Großteil der nützlichen Informationen zu den Vorgängen beim Klonen des virtuellen Domänencontrollers. Standardmäßig ist eine Windows Server 2012-Computerinstallation eine Serverkerninstallation, was bedeutet, dass es keine grafische Benutzeroberfläche und damit keine Möglichkeit gibt, das lokale Snap-In „Ereignisanzeige“ auszuführen.  

So überprüfen Sie die Ereignisprotokolle auf einem Server mit einer Serverkerninstallation:  

-   Führen Sie das Tool Wevtutil.exe lokal aus.  

-   Führen Sie das PowerShell-Cmdlet Get-WinEvent lokal aus.  

-   Wenn Sie die erweiterten Windows-Firewallregeln für die Gruppen "Remote-Ereignisprotokoll Verwaltung" (oder entsprechende Ports) aktiviert haben, um eingehende Kommunikation zuzulassen, können Sie das Ereignisprotokoll Remote mithilfe von eventvwr. exe, wevtutil. exe oder Get-WinEvent verwalten. Die kann auf Serverkerninstallationen mithilfe von NETSH.exe, der Gruppenrichtlinie oder dem neuen Cmdlet Set-NetFirewallRule in Windows PowerShell 3.0 durchgeführt werden.  

> [!WARNING]  
> Versuchen Sie nicht, die grafische Shell wieder zum Computer hinzuzufügen, während dieser sich im DSRM befindet. Der Windows-Bereitstellungsstapel (CBS) kann im abgesicherten Modus oder DSRM nicht ordnungsgemäß betrieben werden. Versuche, Features oder Rollen im DSRM hinzuzufügen, werden nicht abgeschlossen und lassen den Computer in einem instabilen Zustand zurück, bis er normal gestartet wird. Da ein virtualisierter Domänencontrollerklon im DSRM in den meisten Fällen nicht normal gestartet werden kann, ist es unmöglich, die grafische Shell auf sichere Weise hinzuzufügen. Eine solche Vorgehensweise wird nicht unterstützt und führt möglicherweise dazu, dass Ihr Server unbrauchbar ist.  

### <a name="BKMK_SpecificProblems"></a>Problembehandlung bei bestimmten Problemen  

#### <a name="events"></a>Ereignisse  
Alle Ereignisse beim Klonen eines virtualisierten Domänencontroller werden in das Verzeichnisdienst-Ereignisprotokoll des geklonten virtuellen Domänencontrollercomputers geschrieben. Das Anwendungs-, Dateireplikationsdienst- und DFS-Replikationsereignisprotokoll enthält möglicherweise auch nützliche Problembehandlungsinformationen für fehlgeschlagene Klonvorgänge. Fehler bei RPC-Aufrufen an den PDC-Emulator sind möglicherweise im Ereignisprotokoll auf dem PDC-Emulator verfügbar.  

Im Folgenden sind die klonspezifischen Windows Server 2012-Ereignisse im Verzeichnisdienst-Ereignisprotokoll mit Notizen und vorgeschlagenen Lösungen für Fehler aufgeführt.  

##### <a name="directory-services-event-log"></a>Verzeichnisdienst-Ereignisprotokoll  

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                            |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                          **2160**                                                                                                                                                                                                          |
|        **Quelle**        |                                                                                                                                                                                      Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                       |
|       **Zunehmen**       |                                                                                                                                                                                                       Informationen                                                                                                                                                                                                        |
|       **Nachricht**        | Der lokale *<COMPUTERNAME>* hat eine Klon Konfigurationsdatei für virtuelle Domänen Controller gefunden.<br /><br />Fundstelle der Klonkonfigurationsdatei: %1<br /><br />Das Vorliegen einer Klonkonfigurationsdatei lässt darauf schließen, dass der lokale virtuelle Domänencontroller ein Klon eines anderen virtuellen Domänencontrollers ist. Der *<COMPUTERNAME>* wird gestartet, um sich selbst zu klonen. |
| **Hinweise und Lösung** |                                                                                                                  Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist. Überprüfen Sie das DSA-Arbeitsverzeichnis, %systemroot%\ntds, und den Stamm aller lokalen oder Wechseldatenträger auf die Datei dcclconeconfig.xml.                                                                                                                  |

|                          |                                                                                                                                                                                          |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                         **2161**                                                                                         |
|        **Quelle**        |                                                                     Microsoft-Windows-ActiveDirectory_DomainService                                                                      |
|       **Zunehmen**       |                                                                                      Informationen                                                                                       |
|       **Nachricht**        |                         Der lokale *<COMPUTERNAME>* hat die Klon Konfigurationsdatei für den virtuellen Domänen Controller nicht gefunden. Folglich ist der lokale Computer kein geklonter Domänencontroller.                          |
| **Hinweise und Lösung** | Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist. Überprüfen Sie das DSA-Arbeitsverzeichnis, %systemroot%\ntds, und den Stamm aller lokalen oder Wechseldatenträger auf die Datei dcclconeconfig.xml. |

|||  
|-|-|  
|**Ereignis-ID**|**2162**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Fehler beim Klonen des virtuellen Domänencontrollers.<br /><br />Überprüfen Sie die in den Systemereignisprotokollen und in %systemroot%\debug\dcpromo.log protokollierten Ereignisse, um weitere Informationen zum Versuch des Klonens eines virtuellen Domänencontrollers zu erhalten.<br /><br />Fehlercode: %1|  
|**Hinweise und Lösung**|Befolgen Sie die Anweisungen in der Meldung, dieser Fehler ist ein „catchall“.|  

|||  
|-|-|  
|**Ereignis-ID**|**2163**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Der DsRoleSvc-Dienst zum Klonen des lokalen virtuellen Domänencontrollers wurde gestartet.|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist. Überprüfen Sie das DSA-Arbeitsverzeichnis, %systemroot%\ntds, und den Stamm aller lokalen oder Wechseldatenträger auf die Datei dcclconeconfig.xml.|  

|                          |                                                                                                                                                                                                   |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                             **2164**                                                                                              |
|        **Quelle**        |                                                                          Microsoft-Windows-ActiveDirectory_DomainService                                                                          |
|       **Zunehmen**       |                                                                                               Fehler                                                                                               |
|       **Nachricht**        |                                               *<COMPUTERNAME>* konnte den dsrolesvc-Dienst nicht starten, um den lokalen virtuellen Domänen Controller zu klonen.                                                |
| **Hinweise und Lösung** | Untersuchen Sie die Diensteinstellungen für den DS-Rollenserverdienst (DsRoleSvc), und stellen Sie sicher, dass der Starttyp auf normal festgelegt ist. Vergewissern Sie sich, dass kein Drittanbieterprogramm das Starten dieses Diensts verhindert. |

|                          |                                                                                                                                                                                     |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                      **2165**                                                                                       |
|        **Quelle**        |                                                                   Microsoft-Windows-ActiveDirectory_DomainService                                                                   |
|       **Zunehmen**       |                                                                                        Fehler                                                                                        |
|       **Nachricht**        | *<COMPUTERNAME>* konnte während des Klonens des lokalen virtuellen Domänen Controllers keinen Thread starten.<br /><br />Fehlercode:%1<br /><br />Fehlermeldung:%2<br /><br />Name des Threads:%3 |
| **Hinweise und Lösung** |                                                                          Wenden Sie sich an den Microsoft-Produktsupport.                                                                          |

|                          |                                                                                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                          **2166**                                                                           |
|        **Quelle**        |                                                       Microsoft-Windows-ActiveDirectory_DomainService                                                       |
|       **Zunehmen**       |                                                                            Fehler                                                                            |
|       **Nachricht**        | *<COMPUTERNAME>* benötigt den RPCSS-Dienst, um einen Neustart in DSRM zu initiieren. Fehler beim Warten auf das Initialisieren des RPCSS-Diensts bis zum Erreichen eines Ausführungsstatus.<br /><br />Fehlercode:%1 |
| **Hinweise und Lösung** |                                    Untersuchen Sie die Systemereignisprotokolle und die Diensteinstellungen für den RPC-Serverdienst (Rpcss)                                     |

|                          |                                                                                                                                                                            |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                  **2167**                                                                                  |
|        **Quelle**        |                                                              Microsoft-Windows-ActiveDirectory_DomainService                                                               |
|       **Zunehmen**       |                                                                                   Fehler                                                                                    |
|       **Nachricht**        | das Wissen des virtuellen Domänen Controllers konnte von *<COMPUTERNAME>* nicht initialisiert werden. Weitere Informationen finden Sie im letzten Ereignisprotokolleintrag.<br /><br />Weitere Daten<br /><br />Fehlercode:%1 |
| **Hinweise und Lösung** |                                                           Befolgen Sie die Anweisungen in der Meldung, dieser Fehler ist ein „catchall“.                                                           |

|||  
|-|-|  
|**Ereignis-ID**|**2168**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Microsoft-Windows-ActiveDirectory_DomainService<br /><br />Der Domänencontroller wird auf einem unterstützten Hypervisor ausgeführt. Eine VM-Generations-ID wurde erkannt.<br /><br />Aktueller Wert der VM-Generations-ID: %1|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|**Ereignis-ID**|**2169**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Es wurde keine VM-Generations-ID erkannt. Der Host des Domänencontrollers ist ein physischer Computer, eine ältere Version von Hyper-V oder ein Hypervisor, der VM-Generations-IDs nicht unterstützt.<br /><br />Weitere Daten<br /><br />Fehlercode beim Überprüfen der VM-Generations-ID:%1|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis, wenn kein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll, und lesen Sie die Produktsupportdokumentation zum Hypervisor noch einmal durch.|  

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                              **2170**                                                                                                                                                                                                                                                                                                                                                              |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                          Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                           |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                              Warnung                                                                                                                                                                                                                                                                                                                                                               |
|       **Nachricht**        | Es wurde keine Änderung der Generations-ID erkannt.<br /><br />Zwischengespeicherte Generations-ID (DS, alter Wert):%1<br /><br />Aktuelle Generations-ID des virtuellen Computers (neuer Wert):%2<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. *<COMPUTERNAME>* erstellt eine neue Aufruf-ID, um den Domänen Controller wiederherzustellen. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                                                      Dies ist ein Erfolgsereignis, wenn ein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll.                                                                                                                                                                                                                                                                                                                       |

|||  
|-|-|  
|**Ereignis-ID**|**2171**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Es wurde keine Änderung der Generations-ID erkannt.<br /><br />Zwischengespeicherte Generations-ID (DS, alter Wert):%1<br /><br />Aktuelle Generations-ID des virtuellen Computers (neuer Wert):%2|  
|**Hinweise und Lösung**|Dies ist eine Erfolgsmeldung, wenn kein Klonen beabsichtigt ist, die bei jedem Neustart eines virtualisierten Domänencontrollers angezeigt werden sollte. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  

|||  
|-|-|  
|**Ereignis-ID**|**2172**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Das msDS-GenerationId-Attribut des Domänencontrollers wurde gelesen.<br /><br />Wert des msDS-GenerationId-Attributs:%1|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis, wenn ein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  

|||  
|-|-|  
|**Ereignis-ID**|**2173**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Fehler beim Lesen des msDS-GenerationId-Attributs des Computerobjekts des Domänencontrollers. Mögliche Ursachen sind, dass eine Datenbanktransaktion nicht korrekt ausgeführt wurde oder dass die Generations-ID in der lokalen Datenbank nicht vorhanden ist. Zu bedenken ist auch, dass beim ersten Neustart nach einem DCPromo-Vorgang noch kein msDS-GenerationId-Attribut vorhanden ist.<br /><br />Weitere Daten<br /><br />Fehlercode:%1|  
|**Hinweise und Lösung**|Dies ist eine Erfolgsnachricht, wenn ein Klonen beabsichtigt ist und es sich um den ersten Neustart des virtuellen Computers nach dem Klonen handelt. Auf nicht virtuellen Domänencontrollern kann sie ignoriert werden. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  

|||  
|-|-|  
|**Ereignis-ID**|**2174**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Der Domänencontroller ist weder ein Klon noch eine wiederhergestellte Momentaufnahme eines virtuellen Domänencontrollers.|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis, wenn kein Klonen beabsichtigt ist. Andernfalls untersuchen Sie das Systemereignisprotokoll.|  

|||  
|-|-|  
|**Ereignis-ID**|**2175**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Die Konfigurationsdatei zum Klonen des virtuellen Domänencontrollers befindet sich auf einer nicht unterstützten Plattform.|  
|**Hinweise und Lösung**|Zu dieser Meldung kommt es, wenn eine dccloneconfig.xml-Datei, aber keine VM-Generations-ID gefunden wird, beispielsweise wenn eine dccloneconfig.xml-Datei auf einem physischen Computer oder einem Hypervisor gefunden wird, der die VM-Generations-ID nicht unterstützt.|  

|||  
|-|-|  
|**Ereignis-ID**|**2176**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Die Klonkonfigurationsdatei für virtuelle Domänencontroller wurde umbenannt.<br /><br />Weitere Daten<br /><br />Bisheriger Dateiname:%1<br /><br />Neuer Dateiname:%2|  
|**Hinweise und Lösung**|Die Umbenennung ist erwartet, wenn eine Sicherung eines virtuellen Quellcomputers gestartet wird, da sich die VM-Generations-ID nicht geändert hat. Dies verhindert, dass der Quelldomänencontroller einen Klonvorgang versucht.|  

|||  
|-|-|  
|**Ereignis-ID**|**2177**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Fehler beim Umbenennen der Konfigurationsdatei zum Klonen des virtuellen Domänencontrollers.<br /><br />Weitere Daten<br /><br />Dateiname:%1<br /><br />Fehlercode:%2 %3|  
|**Hinweise und Lösung**|Der Umbenennungsversuch ist erwartet, wenn eine Sicherung eines virtuellen Quellcomputers gestartet wird, da sich die VM-Generations-ID nicht geändert hat. Dies verhindert, dass der Quelldomänencontroller einen Klonvorgang versucht. Nennen Sie die Datei manuell um, und untersuchen Sie installierte Drittanbieterprodukte, die möglicherweise die Umbenennung der Datei verhindern.|  

|||  
|-|-|  
|**Ereignis-ID**|**2178**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Eine Klonkonfigurationsdatei für virtuelle Domänencontroller wurde erkannt, doch die VM-Generations-ID wurde nicht geändert. Der lokale Domänencontroller ist der Quelldomänencontroller für den Klonvorgang. Benennen Sie die Klonkonfigurationsdatei um.|  
|**Hinweise und Lösung**|Erwartet, wenn eine Sicherung eines virtuellen Quellcomputers gestartet wird, da sich die VM-Generations-ID nicht geändert hat. Dies verhindert, dass der Quelldomänencontroller einen Klonvorgang versucht.|  

|||  
|-|-|  
|**Ereignis-ID**|**2179**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Für das msDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers wurde der folgende Parameter festgelegt:<br /><br />Generations-ID-Attribut:%1|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|**Ereignis-ID**|**2180**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Warnung|  
|**Nachricht**|Fehler beim Festlegen des Attributs "msDS-GenerationId" für das Computerobjekt des Domänencontrollers.<br /><br />Weitere Daten<br /><br />Fehlercode:%1|  
|**Hinweise und Lösung**|Untersuchen Sie das Systemereignisprotokoll und die Datei Dcpromo.log. Suchen Sie unter MS TechNet, in der MS Knowledge Base und in MS-Blogs nach dem bestimmten Fehler, um seine gewöhnliche Bedeutung zu bestimmen und ihn dann auf der Basis dieser Ergebnisse zu behandeln.|  

|||  
|-|-|  
|**Ereignis-ID**|**2182**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Internes Ereignis: Der Verzeichnisdienst wurde aufgefordert, einen Remote-DSA zu klonen:|  
|**Hinweise und Lösung**|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|                          |                                                                                                                                                                                                                                                                   |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                             **2183**                                                                                                                              |
|        **Quelle**        |                                                                                                          Microsoft-Windows-ActiveDirectory_DomainService                                                                                                          |
|       **Zunehmen**       |                                                                                                                           Informationen                                                                                                                           |
|       **Nachricht**        | Internes Ereignis: *<COMPUTERNAME>* hat die Anforderung zum Klonen des Remote Verzeichnis System-Agents abgeschlossen.<br /><br />Name des ursprünglichen DC:%3<br /><br />Name des angeforderten Klon-DC:%4<br /><br />Standort des angeforderten Klon-DC:%5<br /><br />Weitere Daten<br /><br />Fehlerwert:%1 %2 |
| **Hinweise und Lösung** |                                                                                                     Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.                                                                                                      |

|                          |                                                                                                                                                                                                                                                                                                  |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                             **2184**                                                                                                                                             |
|        **Quelle**        |                                                                                                                         Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                          |
|       **Zunehmen**       |                                                                                                                                              Fehler                                                                                                                                               |
|       **Nachricht**        | Fehler beim Erstellen eines Domänen Controller Kontos für den geklonten Domänen Controller *<COMPUTERNAME>* .<br /><br />Name des ursprünglichen DC: %1<br /><br />Zulässige Anzahl geklonter DCs:%2<br /><br />Der Grenzwert für die Anzahl der Domänen Controller Konten, die durch Klonen von <em> @ no__t-1 @ no__t-2generiert werden können, wurde überschritten. |
| **Hinweise und Lösung** |              Der Name eines einzigen Quelldomänencontrollers kann basieren auf der Benennungskonvention nur 9.999-mal automatisch generiert werden, wenn die Domänencontroller nicht herabgestuft werden. Verwenden Sie das Elemente <computername> in der XML, um einen neuen eindeutigen Namen zu generieren oder von einem Domänencontroller mit einem anderen Namen zu klonen.              |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                **2191**                                                                                                                                                                                                                                                                |
|        **Quelle**        |                                                                                                                                                                                                                                            Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                             |
|       **Zunehmen**       |                                                                                                                                                                                                                                                             Informationen                                                                                                                                                                                                                                                              |
|       **Nachricht**        | *<COMPUTERNAME>* legen Sie den folgenden Registrierungs Wert fest, um DNS-Updates zu deaktivieren.<br /><br />Registrierungswert:%1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. Nach dem Klonen werden DNS-Aktualisierungen vom Klonprozess wieder aktiviert. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                        Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.                                                                                                                                                                                                                                        |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                        **2192**                                                                                                                                                                                                                                                         |
|        **Quelle**        |                                                                                                                                                                                                                                     Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                     |
|       **Zunehmen**       |                                                                                                                                                                                                                                                          Fehler                                                                                                                                                                                                                                                          |
|       **Nachricht**        | *<COMPUTERNAME>* konnte den folgenden Registrierungs Wert nicht festlegen, um DNS-Updates zu deaktivieren.<br /><br />Registrierungswert:%1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Fehlercode: %4<br /><br />Fehlermeldungen: %5<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. |
| **Hinweise und Lösung** |                                                                                                                                                                                                  Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise Registrierungsaktualisierungen blockieren.                                                                                                                                                                                                  |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                        **2193**                                                                                                                                                                                                                         |
|        **Quelle**        |                                                                                                                                                                                                     Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                     |
|       **Zunehmen**       |                                                                                                                                                                                                                      Informationen                                                                                                                                                                                                                      |
|       **Nachricht**        | *<COMPUTERNAME>* legen Sie den folgenden Registrierungs Wert fest, um DNS-Updates zu aktivieren.<br /><br />Registrierungswert:%1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. |
| **Hinweise und Lösung** |                                                                                                                                                                                                Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.                                                                                                                                                                                                 |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                        **2194**                                                                                                                                                                                                                                                        |
|        **Quelle**        |                                                                                                                                                                                                                                    Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                     |
|       **Zunehmen**       |                                                                                                                                                                                                                                                         Fehler                                                                                                                                                                                                                                                          |
|       **Nachricht**        | *<COMPUTERNAME>* konnte den folgenden Registrierungs Wert nicht zum Aktivieren von DNS-Updates festlegen.<br /><br />Registrierungswert:%1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Fehlercode: %4<br /><br />Fehlermeldungen: %5<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. |
| **Hinweise und Lösung** |                                                                                                                                                                                                 Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise Registrierungsaktualisierungen blockieren.                                                                                                                                                                                                  |

|||  
|-|-|  
|**Ereignis-ID**|**2195**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Fehler beim Festlegen des DSRM-Starts.<br /><br />Fehlercode:%1<br /><br />Fehlermeldung:%2<br /><br />Wenn beim Klonen eines virtuellen Domänencontrollers Fehler auftreten oder wenn der Hypervisor mit der Klonkonfigurationsdatei nicht unterstützt wird, wird der lokale Computer zur Problembehandlung im Verzeichnisdienst-Wiederherstellungsmodus (DSRM) neu gestartet. Der DSRM-Start konnte jedoch nicht festgelegt werden.|  
|**Hinweise und Lösung**|Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise Registrierungsaktualisierungen blockieren.|  

|||  
|-|-|  
|**Ereignis-ID**|**2196**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Fehler beim Aktivieren des Rechts zum Herunterfahren.<br /><br />Fehlercode:%1<br /><br />Fehlermeldung:%2<br /><br />Wenn beim Klonen eines virtuellen Domänencontrollers Fehler auftreten oder wenn der Hypervisor mit der Klonkonfigurationsdatei nicht unterstützt wird, wird der lokale Computer zur Problembehandlung im Verzeichnisdienst-Wiederherstellungsmodus (DSRM) neu gestartet. Das Recht zum Herunterfahren konnte jedoch nicht aktiviert werden.|  
|**Hinweise und Lösung**|Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise die Verwendung von Berechtigungen blockieren.|  

|||  
|-|-|  
|**Ereignis-ID**|**2197**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Fehler beim Initiieren des Herunterfahrens.<br /><br />Fehlercode:%1<br /><br />Fehlermeldung:%2<br /><br />Wenn beim Klonen eines virtuellen Domänencontrollers Fehler auftreten oder wenn der Hypervisor mit der Klonkonfigurationsdatei nicht unterstützt wird, wird der lokale Computer zur Problembehandlung im Verzeichnisdienst-Wiederherstellungsmodus (DSRM) neu gestartet. Das Herunterfahren des Systems konnte jedoch nicht initiiert werden.|  
|**Hinweise und Lösung**|Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise die Verwendung von Berechtigungen blockieren.|  

|                          |                                                                                                                                                                                   |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                     **2198**                                                                                      |
|        **Quelle**        |                                                                  Microsoft-Windows-ActiveDirectory_DomainService                                                                  |
|       **Zunehmen**       |                                                                                       Fehler                                                                                       |
|       **Nachricht**        | Fehler beim Erstellen oder Ändern des folgenden geklonten DC-Objekts durch *<COMPUTERNAME>* .<br /><br />Weitere Daten:<br /><br />Objekt:<br /><br />%1<br /><br />Fehlerwert: %2<br /><br />%3 |
| **Hinweise und Lösung** |               Suchen Sie unter MS TechNet, in der MS Knowledge Base und in MS-Blogs nach dem bestimmten Fehler, um seine gewöhnliche Bedeutung zu bestimmen und ihn dann auf der Basis dieser Ergebnisse zu behandeln.               |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                   **2199**                                                                                                                                                                                                                   |
|        **Quelle**        |                                                                                                                                                                                               Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                |
|       **Zunehmen**       |                                                                                                                                                                                                                    Fehler                                                                                                                                                                                                                     |
|       **Nachricht**        |                                                                                                                     Fehler beim Erstellen des folgenden geklonten DC-Objekts durch *<COMPUTERNAME>* , da das Objekt bereits vorhanden ist.<br /><br />Weitere Daten:<br /><br />Quelldomänencontroller:<br /><br />%1<br /><br />Objekt:<br /><br />%2                                                                                                                     |
| **Hinweise und Lösung** | Vergewissern Sie sich, dass in der Datei dccloneconfig.xml kein vorhandener Domänencontroller angegeben ist und dass keine Kopien der Datei dccloneconfig.xml auf mehreren Klonen verwendet wurden, ohne den Namen zu bearbeiten. Wenn die Kollision immer noch unerwartet ist, legen Sie fest, welcher Administrator sie heraufgestuft hat. Wenden Sie sich an den Administrator, um zu besprechen, ob der vorhandene Domänencontroller herabgestuft, die Metadaten des vorhandenen Domänencontrollers bereinigt oder der Klon einen anderen Namen verwenden sollte. |

|||  
|-|-|  
|**Ereignis-ID**|**2203**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Fehler|  
|**Nachricht**|Fehler beim Klonen des letzten virtuellen Domänencontrollers. Dies ist der erste Neustart nach dem Fehler, daher sollte der Klonvorgang nun wiederholt werden. Es ist jedoch weder eine Konfigurationsdatei für das Klonen von virtuellen Domänencontrollern noch eine Änderung der VM-Generations-ID vorhanden. Starten Sie im DSRM.<br /><br />Fehler beim Klonen des letzten virtuellen Domänencontrollers:%1<br /><br />Die Konfigurationsdatei zum Klonen des virtuellen Domänencontrollers ist vorhanden:%2<br /><br />Eine Änderung der VM-Generations-ID wird erkannt:%3|  
|**Hinweise und Lösung**|Erwartet, wenn das Klonen zuvor aufgrund einer fehlenden oder ungültigen dccloneconfig.xml-Datei fehlgeschlagen ist.|  

|||  
|-|-|  
|Ereignis-ID|2210|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|<COMPUTERNAME> konnte keine Objekte für den geklonten Domänencontroller erstellen.<br /><br />Weitere Daten:<br /><br />Klon-ID: %6<br /><br />Name des geklonten Domänencontrollers: %1<br /><br />Wiederholungsschleife: %2<br /><br />Ausnahmewert: %3<br /><br />Fehlerwert: %4<br /><br />DSID: %5|  
|Hinweise und Lösungen|Überprüfen Sie die System- und Verzeichnisdienstprotokolle sowie die Datei dcpromo.log auf weitere Details für das Fehlschlagen des Klonens.|  

|||  
|-|-|  
|Ereignis-ID|2211|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> hat Objekte für den geklonten Domänencontroller erstellt.<br /><br />Weitere Daten:<br /><br />Klon-ID: %3<br /><br />Name des geklonten Domänencontrollers: %1<br /><br />Wiederholungsschleife: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2212|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> hat mit der Erstellung von Objekten für den geklonten Domänencontroller begonnen.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Klonname: %2<br /><br />Klonsite: %3<br /><br />Geklonter RODC: %4|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2213|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> hat ein neues KrbTgt-Objekt für das Klonen schreibgeschützter Domänencontroller erstellt.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />GUID des neuen KrbTgt-Objekts: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2214|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> erstellt ein Computerobjekt für den geklonten Domänencontroller.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Ursprünglicher Domänencontroller: %2<br /><br />Geklonter Domänencontroller: %3|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2215|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> fügen den geklonten Domänencontroller in der folgenden Site hinzu.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Website: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2216|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> erstellt einen Servercontainer für den geklonten Domänencontroller.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Servercontainer: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2217|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> erstellt ein Serverobjekt für den geklonten Domänencontroller.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Serverobjekt: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2218|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> erstellt ein Objekt mit NTDS-Einstellungen für den geklonten Domänencontroller.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Objekt: %2|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2219|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> erstellt Verbindungsobjekte für den geklonten schreibgeschützten Domänencontroller.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2220|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> erstellt SYSVOL-Objekte für den geklonten schreibgeschützten Domänencontroller.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2221|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|<COMPUTERNAME> konnte kein zufälliges Kennwort für den geklonten Domänencontroller erstellen.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Name des geklonten Domänencontrollers: %2<br /><br />Fehler: %3 %4|  
|Hinweise und Lösungen|Untersuchen Sie das Systemereignisprotokoll auf weitere Details für die Gründe, aus denen das Computerkontokennwort nicht erstellt werden konnte.|  

|||  
|-|-|  
|Ereignis-ID|2222|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|<COMPUTERNAME> konnte kein Kennwort für den geklonten Domänencontroller festlegen.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Name des geklonten Domänencontrollers: %2<br /><br />Fehler: %3 %4|  
|Hinweise und Lösungen|Untersuchen Sie das Systemereignisprotokoll auf weitere Details für die Gründe, aus denen das Computerkontokennwort nicht festgelegt werden konnte.|  

|||  
|-|-|  
|Ereignis-ID|2223|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|<COMPUTERNAME> hat das Computerkontokennwort für den geklonten Domänencontroller festgelegt.<br /><br />Weitere Daten:<br /><br />Klon-ID: %1<br /><br />Name des geklonten Domänencontrollers: %2<br /><br />Gesamtanzahl der Wiederholungen: %3|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2224|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Klonen des virtuellen Domänencontrollers. Die folgenden %1 verwalteten Dienstkonten sind auf dem geklonten Computer vorhanden:<br /><br />%2<br /><br />Damit der Klonvorgang erfolgreich ist, müssen alle verwalteten Dienstkonten entfernt werden. Dazu können Sie das PowerShell-Cmdlet "Remove-ADComputerServiceAccount" verwenden.|  
|Hinweise und Lösungen|Erwartet bei der Verwendung von eigenständigen MSAs (nicht bei Gruppen-MSA). Befolgen Sie *nicht* den Ereignisratschlag, das Konto zu entfernen – dieser ist falsch. Verwenden Sie Uninstall-ADServiceAccount- [https://technet.microsoft.com/library/hh852310](https://technet.microsoft.com/library/hh852310).<br /><br />Eigenständige MSAs, die zuerst in Windows Server 2008 R2 eingeführt wurden, wurden in Windows Server 2012 durch Gruppen-MSAs (gMSA) ersetzt. GMSAs bieten Unterstützung für das Klonen.|  

|||  
|-|-|  
|Ereignis-ID|2225|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Informationen|  
|Meldung|Die zwischengespeicherten geheimen Schlüssel des folgenden Sicherheitsprinzipals wurden erfolgreich vom lokalen Domänencontroller entfernt:<br /><br />%1<br /><br />Nach dem Klonen eines schreibgeschützten Domänencontrollers werden geheime Schlüssel, die zuvor auf dem als Klonquelle verwendeten schreibgeschützten Domänencontroller zwischengespeichert wurden, vom geklonten Domänencontroller entfernt.|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|2226|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Entfernen von zwischengespeicherten geheimen Schlüsseln des folgenden Sicherheitsprinzipals vom lokalen Domänencontroller:<br /><br />%1<br /><br />Fehler: %2 (%3)<br /><br />Nach dem Klonen eines schreibgeschützten Domänencontrollers müssen geheime Schlüssel, die zuvor auf dem als Klonquelle verwendeten schreibgeschützten Domänencontroller zwischengespeichert wurden, aus dem Klon entfernt werden. Geschieht dies nicht, wird das Risiko eines Angriffs zum Abrufen dieser Anmeldeinformationen von einem gestohlenen oder kompromittierten Klon erhöht. Falls der Sicherheitsprinzipal ein Konto mit umfangreichen Rechten ist und dagegen geschützt werden sollte, verwenden Sie den rootDSE-Vorgang "rODCPurgeAccount", um die geheimen Schlüssel manuell auf dem lokalen Domänencontroller zu löschen.|  
|Hinweise und Lösungen|Untersuchen Sie die System- und Verzeichnisdienst-Ereignisprotokolle auf weitere Informationen.|  

|||  
|-|-|  
|Ereignis-ID|2227|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|Bei dem Versuch, zwischengespeicherte geheime Schlüssel vom lokalen Domänencontroller zu entfernen, wurde eine Ausnahme ausgegeben.<br /><br />Weitere Daten:<br /><br />Ausnahmewert: %1<br /><br />Fehlerwert: %2<br /><br />DSID: %3<br /><br />Nach dem Klonen eines schreibgeschützten Domänencontrollers müssen geheime Schlüssel, die zuvor auf dem als Klonquelle verwendeten schreibgeschützten Domänencontroller zwischengespeichert wurden, aus dem Klon entfernt werden. Geschieht dies nicht, wird das Risiko eines Angriffs zum Abrufen dieser Anmeldeinformationen von einem gestohlenen oder kompromittierten Klon erhöht. Falls einer dieser Sicherheitsprinzipale ein Konto mit umfangreichen Rechten ist und dagegen geschützt werden sollte, verwenden Sie den rootDSE-Vorgang "rODCPurgeAccount", um die geheimen Schlüssel manuell auf dem lokalen Domänencontroller zu löschen.|  
|Hinweise und Lösungen|Untersuchen Sie die System- und Verzeichnisdienst-Ereignisprotokolle auf weitere Informationen.|  

|||  
|-|-|  
|Ereignis-ID|2228|  
|Source|Microsoft-Windows-ActiveDirectory_DomainService|  
|Nach Schweregrad|Fehler|  
|Meldung|Die Generierungs-ID des virtuellen Computers in der Active Directory-Datenbank dieses Domänencontrollers unterscheidet sich vom aktuellen Wert dieses virtuellen Computers. Eine Konfigurationsdatei zum Klonen des virtuellen Domänencontrollers (DCCloneConfig.xml) konnte jedoch nicht gefunden werden, sodass der Domänencontroller nicht geklont wurde. Falls ein Klonvorgang für den Domänencontroller ausgeführt werden sollte, stellen Sie sicher, dass eine DCCloneConfig.xml-Datei in einem der unterstützten Speicherorte bereitgestellt ist. Darüber hinaus steht die IP-Adresse dieses Domänencontrollers in Konflikt mit der IP-Adresse eines anderen Domänencontrollers. Um sicherzustellen, dass der Betrieb nicht unterbrochen wird, wurde der Domänencontroller so konfiguriert, dass er im DSRM gestartet wird.<br /><br />Weitere Daten:<br /><br />Doppelte IP-Adresse: %1|  
|Hinweise und Lösungen|Dieser Schutzmechanismus beendet doppelte Domänencontroller, wenn möglich (bei der Verwendung von DHCP beispielsweise nicht). Fügen Sie eine gültige DcCloneConfig.xml-Datei hinzu, entfernen Sie das DSRM-Kennzeichen, und führen Sie das Klonen dann erneut durch.|  

|||  
|-|-|  
|Ereignis-ID|29218|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Klonen des virtuellen Domänencontrollers. Der Klonvorgang konnte nicht abgeschlossen werden, und der geklonte Domänencontroller wurde im DSRM (Directory Services Restore Mode) neu gestartet.<br /><br />Weitere Informationen zu Fehlern, die mit dem Klonversuch für den virtuellen Domänencontroller im Zusammenhang stehen, finden Sie in den zuvor protokollierten Ereignissen und in "%systemroot%\debug\dcpromo.log". Hier finden Sie auch Angaben dazu, ob dieses Klonimage wiederverwendet werden kann.<br /><br />Falls mindestens ein Protokolleintrag darauf hinweist, dass der Klonvorgang nicht wiederholt werden kann, muss das Image auf sichere Art zerstört werden. Andernfalls können Sie die Fehler beheben, das DSRM-Startkennzeichen löschen und normal neu starten. Beim Neustart wird der Klonvorgang wiederholt.|  
|Hinweise und Lösungen|Überprüfen Sie die System- und Verzeichnisdienstprotokolle sowie die Datei dcpromo.log auf weitere Details für das Fehlschlagen des Klonens.|  

|||  
|-|-|  
|Ereignis-ID|29219|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Informationen|  
|Meldung|Der virtuelle Domänencontroller wurde erfolgreich geklont.|  
|Hinweise und Lösungen|Dies ist ein Erfolgsereignis und nur ein Problem, wenn es unerwartet ist.|  

|||  
|-|-|  
|Ereignis-ID|29248|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Für das Klonen des Domänencontrollers konnte die Winlogon-Benachrichtigung nicht abgerufen werden. Folgender Fehlercode wurde zurückgegeben: %1 (%2).<br /><br />Weitere Informationen zu diesem Fehler finden Sie in "%systemroot%\debug\dcpromo.log". Suchen Sie dort nach Fehlern, die mit dem Klonversuch für den virtuellen Domänencontroller zu tun haben.|  
|Hinweise und Lösungen|Wenden Sie sich an den Microsoft-Produktsupport.|  

|||  
|-|-|  
|Ereignis-ID|29249|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler bei dem Versuch, beim Klonen des virtuellen Domänencontrollers die Konfigurationsdatei für den virtuellen Domänencontroller zu analysieren.<br /><br />Folgender HRESULT-Code wurde zurückgegeben: %1.<br /><br />Die Konfigurationsdatei ist:%2<br /><br />Beheben Sie die Fehler in der Konfigurationsdatei, und wiederholen Sie den Klonvorgang.<br /><br />Weitere Informationen zu diesem Fehler finden Sie in "%systemroot%\debug\dcpromo.log".|  
|Hinweise und Lösungen|Untersuchen Sie die Datei dclconeconfig.xml mithilfe eines XML-Editors auf Syntaxfehler und die DCCloneConfigSchema.xsd-Schemadatei.|  

|||  
|-|-|  
|Ereignis-ID|29250|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Klonen des virtuellen Domänencontrollers. Auf dem geklonten virtuellen Domänencontroller sind momentan Anwendungen oder Dienste aktiviert, die in der für das Klonen von virtuellen Domänencontrollern verwendeten Liste zulässiger Anwendungen nicht aufgeführt sind.<br /><br />Die folgenden Einträge fehlen:<br /><br />%2<br /><br />%1 (falls vorhanden) wurde als definierte Aufnahmeliste verwendet.<br /><br />Der Klonvorgang kann nicht abgeschlossen werden, wenn nicht klonbare Anwendungen installiert sind.<br /><br />Führen Sie das Active Directory-Powershell-Cmdlet "Get-ADDCCloningExcludedApplicationList" aus, um zu prüfen, welche Anwendungen auf dem geklonten Computer installiert, aber nicht in der Liste zugelassener Anwendungen enthalten sind. Fügen Sie diese Anwendungen der Liste zulässiger Anwendungen hinzu, wenn sie mit dem Klonen eines virtuellen Domänencontrollers kompatibel sind. Deinstallieren Sie alle Anwendungen, die nicht mit dem Klonen des virtuellen Domänencontrollers kompatibel sind, und wiederholen Sie dann den Klonvorgang.<br /><br />Der Klonvorgang für virtuelle Domänencontroller sucht nach der Datei mit der Liste zugelassener Anwendungen, "CustomDCCloneAllowList.xml", basierend auf der folgenden Reihenfolge: Die zuerst gefundene Datei wird verwendet, und alle anderen werden ignoriert:<br /><br />1. Der Name des Registrierungswerts lautet: HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters\AllowListFolder<br /><br />2. Dasselbe Verzeichnis, in dem sich der Ordner des DSA-Arbeitsverzeichnisses befindet<br /><br />3. %windir%\NTDS<br /><br />4. Lese-/Schreibwechselmedien in der Reihenfolge der Laufwerksbuchstaben am Laufwerkstamm|  
|Hinweise und Lösungen|Befolgen Sie die Anweisungen in der Meldung.|  

|                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Ereignis-ID       |                                                                                                                                                                                                                                                                                                         29251                                                                                                                                                                                                                                                                                                          |
|        Source        |                                                                                                                                                                                                                                                                                   Microsoft-Windows-DirectoryServices-DSROLE-Server                                                                                                                                                                                                                                                                                    |
|       Nach Schweregrad       |                                                                                                                                                                                                                                                                                                         Fehler                                                                                                                                                                                                                                                                                                          |
|       Meldung        | Die IP-Adresse des geklonten Rechners konnte nicht zurückgesetzt werden.<br /><br />Folgender Fehlercode wurde zurückgegeben: %1 (%2).<br /><br />Ursache dieses Fehlers könnte eine fehlerhafte Konfiguration in den Netzwerkkonfigurationsabschnitten in der Konfigurationsdatei des virtuellen Domänencontrollers sein.<br /><br />Weitere Informationen zu Fehlern, die beim Klonen eines virtuellen Domänencontrollers hinsichtlich des Zurücksetzens von IP-Adressen auftreten können, finden Sie in "%systemroot%\debug\dcpromo.log".<br /><br />Details zum Zurücksetzen von Computer-IP-Adressen auf dem geklonten Computer finden Sie unter https://go.microsoft.com/fwlink/?LinkId=208030 |
| Hinweise und Lösungen |                                                                                                                                                                                                                                                  Vergewissern Sie sich, dass die in der dccloneconfig.xml- Datei festgelegten IP-Informationen gültig sind und den ursprünglichen Quellcomputer nicht duplizieren.                                                                                                                                                                                                                                                   |

|                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Ereignis-ID       |                                                                                                                                                                                                                                                                                   29253                                                                                                                                                                                                                                                                                   |
|        Source        |                                                                                                                                                                                                                                                             Microsoft-Windows-DirectoryServices-DSROLE-Server                                                                                                                                                                                                                                                             |
|       Nach Schweregrad       |                                                                                                                                                                                                                                                                                   Fehler                                                                                                                                                                                                                                                                                   |
|       Meldung        | Fehler beim Klonen des virtuellen Domänencontrollers. Der Klondomänencontroller konnte den als primären Domänencontroller (PDC) fungierenden Betriebsmaster nicht in der Ursprungsdomäne des geklonten Computers finden.<br /><br />Folgender Fehlercode wurde zurückgegeben: %1 (%2).<br /><br />Vergewissern Sie sich, dass der primäre Domänencontroller in der Ursprungsdomäne des geklonten Computers einem aktiven Domänencontroller zugeordnet, online und betriebsbereit ist. Vergewissern Sie sich, dass der geklonte Computer über die erforderlichen Ports und Protokolle eine LDAP/RPC-Verbindung mit dem primären Domänencontroller hat. |
| Hinweise und Lösungen |                                                                                                                                      Vergewissern Sie sich, dass die IP-Adresse des geklonten Domänencontrollers und die DNS-Informationen festgelegt sind. Verwenden Sie Dcdiag. exe/Test: loercheck, um zu überprüfen, ob der PDCE Online ist, verwenden Sie Nltest. exe/Server: *<PDCE>* /DCLIST: *<domain>* zum gültigen RPC, rufen Sie eine Netzwerk Erfassung vom PDCE ab, während das Klonen fehlschlägt, und analysieren Sie den Datenverkehr.                                                                                                                                       |

|                      |                                                                                                                                                                                                                                                                                                                                                                    |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Ereignis-ID       |                                                                                                                                                                               29254                                                                                                                                                                                |
|        Source        |                                                                                                                                                         Microsoft-Windows-DirectoryServices-DSROLE-Server                                                                                                                                                          |
|       Nach Schweregrad       |                                                                                                                                                                               Fehler                                                                                                                                                                                |
|       Meldung        | Es konnte keine Bindung mit dem primären Domänencontroller %1 hergestellt werden.<br /><br />Folgender Fehlercode wurde zurückgegeben: %2 (%3).<br /><br />Vergewissern Sie sich, dass der primäre Domänencontroller %1 online und betriebsbereit ist. Vergewissern Sie sich, dass der geklonte Computer über die erforderlichen Ports und Protokolle eine LDAP/RPC-Verbindung mit dem primären Domänencontroller hat. |
| Hinweise und Lösungen |                                   Vergewissern Sie sich, dass die IP-Adresse des geklonten Domänencontrollers und die DNS-Informationen festgelegt sind. Verwenden Sie Dcdiag. exe/Test: loercheck, um zu überprüfen, ob der PDCE Online ist, verwenden Sie Nltest. exe/Server: *<PDCE>* /DCLIST: *<domain>* zum gültigen RPC, rufen Sie eine Netzwerk Erfassung vom PDCE ab, während das Klonen fehlschlägt, und analysieren Sie den Datenverkehr.                                   |

|||  
|-|-|  
|Ereignis-ID|29255|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Klonen des virtuellen Domänencontrollers.<br /><br />Bei dem Versuch, Objekte auf dem primären Domänencontroller %1 zu erstellen, die für das zu klonende Image erforderlich sind, wurde der Fehler %2 (%3) zurückgegeben.<br /><br />Überprüfen Sie, ob der geklonte Domänencontroller über die Berechtigung verfügt, sich selbst zu klonen. Suchen Sie auf dem primären Domänencontroller %1 im Ereignisprotokoll für den Verzeichnisdienst nach zugehörigen Ereignissen.|  
|Hinweise und Lösungen|Suchen Sie unter MS TechNet, in der MS Knowledge Base und in MS-Blogs nach dem bestimmten Fehler, um seine typische Bedeutung zu bestimmen und ihn dann auf der Basis dieser Ergebnisse zu behandeln.|  

|||  
|-|-|  
|Ereignis-ID|29256|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Festlegen des Kennzeichens für Starten im Verzeichnisdienste-Wiederherstellungsmodus. Fehlercode: %1.<br /><br />Weitere Informationen zu Fehlern finden Sie in der Datei %systemroot%\debug\dcpromo.log.|  
|Hinweise und Lösungen|Untersuchen Sie das Verzeichnisdienstprotokoll und dcpromo.log auf Details. Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise die Verwendung von Berechtigungen blockieren.|  

|||  
|-|-|  
|Ereignis-ID|29257|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Der virtuelle Domänencontroller wurde geklont. Der Computer konnte wegen eines Fehlers nicht neu gestartet werden: Fehlercode: %1.<br /><br />Starten Sie den Computer neu, damit der Klonvorgang abgeschlossen wird.|  
|Hinweise und Lösungen|Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise die Verwendung von Berechtigungen blockieren.|  

|||  
|-|-|  
|Ereignis-ID|29264|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Fehler beim Löschen des Kennzeichens für Starten im Verzeichnisdienste-Wiederherstellungsmodus. Fehlercode: %1.<br /><br />Weitere Informationen zu Fehlern finden Sie in der Datei %systemroot%\debug\dcpromo.log.|  
|Hinweise und Lösungen|Untersuchen Sie das Verzeichnisdienstprotokoll und dcpromo.log auf Details. Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise die Verwendung von Berechtigungen blockieren.|  

|||  
|-|-|  
|Ereignis-ID|29265|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Informationen|  
|Meldung|Der virtuelle Domänencontroller wurde erfolgreich geklont. Die für das Klonen des virtuellen Domänencontrollers verwendete Konfigurationsdatei "%1" wurde in "%2" umbenannt.|  
|Hinweise und Lösungen|Nicht zutreffend, die ist ein Erfolgsereignis.|  

|||  
|-|-|  
|Ereignis-ID|29266|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Der virtuelle Domänencontroller wurde erfolgreich geklont. Die für das Klonen des virtuellen Domänencontrollers verwendete Konfigurationsdatei "%1" konnte wegen eines Fehlers aber nicht umbenannt werden. Fehlercode: %2 (%3).|  
|Hinweise und Lösungen|Benennen Sie die Datei dccloneconfig.xml manuell um.|  

|||  
|-|-|  
|Ereignis-ID|29267|  
|Source|Microsoft-Windows-DirectoryServices-DSROLE-Server|  
|Nach Schweregrad|Fehler|  
|Meldung|Beim Klonen des virtuellen Domänencontrollers wurde die Liste der für das Klonen virtueller Domänencontroller zugelassenen Anwendungen nicht überprüft.<br /><br />Folgender Fehlercode wurde zurückgegeben: %1 (%2).<br /><br />Dieser Fehler wird möglicherweise durch einen Syntaxfehler in der Datei mit der Klonzulassungsliste verursacht. (Zurzeit wird diese Datei überprüft: %3) Weitere Informationen zu diesem Fehler finden Sie in "%systemroot%\debug\dcpromo.log".|  
|Hinweise und Lösungen|Befolgen Sie die Anweisungen im Ereignis.|  

##### <a name="error-messages"></a>Fehlermeldungen  
Es gibt keine direkten interaktiven Fehler für ein fehlgeschlagenes Klonen von virtuellen Domänencontrollern. Alle Kloninformationen werden in den System- und Verzeichnisdienstprotokollen sowie den Protokollen zum Heraufstufen von Domänencontrollern in dcpromo.log protokolliert. Wenn der Server jedoch im DS-Wiederherstellungsmodus gestartet wird, sollten Sie sofort untersuchen, wenn das Heraufstufen oder Klonen fehlgeschlagen ist.  

Die Datei dcpromo.log ist der erste Ort, den Sie bei Klonfehlern überprüfen sollten. Je nach aufgelistetem Fehler ist es möglicherweise erforderlich, für eine weitere Diagnose die Verzeichnisdienst- und Systemprotokolle zu überprüfen.  

#### <a name="known-issues-and-support-scenarios"></a>Bekannte Probleme und Supportszenarien  
Es folgt eine Liste gängiger Probleme beim Windows Server 2012-Entwicklungsprozess. All diese Probleme sind entwurfsbedingt, und es gibt entweder eine gültige Problemumgehung oder eine geeignetere Methode, um diese komplett zu vermeiden. Einige werden möglicherweise in späteren Versionen von Windows Server 2012 behoben.  

|||  
|-|-|  
|**Problem:**|**Klonen schlägt fehl, DSRM**|  
|**On**|Klonen wird im Verzeichnisdienste-Wiederherstellungsmodus gestartet|  
|**Lösung und Hinweise**|Überprüfen Sie alle Schritte, die Sie aus den Abschnitten „Bereitstellen eines virtualisierten Domänencontrollers“ und [Allgemeine Methode für die Problembehandlung beim Klonen von Domänencontrollern](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_GeneralMethodology) befolgt haben.<br /><br />Beschrieben in KB 2742844.|  

|||  
|-|-|  
|**Problem:**|**Zusätzliche IP-Leases bei Verwendung von DHCP zum Klonen**|  
|**On**|Nach dem erfolgreichen Klonen eines Domänencontrollers und der Verwendung von DHCP übernimmt der erste Start des Klons eine DHCP-Lease. Wenn der Server dann umbenannt und als Domänencontroller neu gestartet ist, übernimmt er eine zweite DHCP-Lease. Die erste IP-Adresse ist nicht freigegeben, und Sie enden mit einer „Phantom“-Lease.|  
|**Lösung und Hinweise**|Löschen Sie die ungenutzte Adresslease in DHCP, oder lassen Sie sie normal ablaufen. Beschrieben in KB 2742836.|  

|||  
|-|-|  
|**Problem:**|**Nach einer sehr langen Verzögerung schlägt das Klonen in DSRM fehl**|  
|**On**|Das Klonen scheint bei „Das Domänencontrollerklonen ist zu X% abgeschlossen“ für 8 bis 15 Minuten zu stoppen. Danach schlägt das Klonen fehl und wird im DSRM gestartet.|  
|**Lösung und Hinweise**|Der geklonte Computer kann keine dynamische IP-Adresse von DHCP oder SLAAC abrufen, verwendet eine doppelte IP-Adresse oder kann den PDC nicht finden. Mehrere vom Klonvorgang durchgeführte erneute Versuche führen zu der Verzögerung. Beheben Sie das Netzwerkproblem, um das Klonen zuzulassen.<br /><br />Beschrieben in KB 2742844.|  

|||  
|-|-|  
|**Problem:**|**Beim Klonen werden nicht alle Dienst Prinzipal Namen neu erstellt.**|  
|**On**|Wenn ein Satz von *dreiteiligen* Dienstprinzipalnamen sowohl einen NetBIOS-Namen mit einem Port als auch einen ansonsten identischen NetBIOS-Namen ohne einen Port enthalten, wird der Eintrag ohne Port nicht mit dem neuen Computernamen erneut erstellt. Zum Beispiel:<br /><br />customspn/DC1:200/app1 INVALID USE OF SYMBOLS *wird mit dem neuen Computernamen neu erstellt*<br /><br />customspn/DC1/app1 INVALID USE OF SYMBOLS *wird nicht mit dem neuen Computernahmen neu erstellt*<br /><br />Vollqualifizierte Namen und SPNs ohne drei Teile werden neu erstellt, unabhängig von Ports. Die folgenden werden beispielsweise erfolgreich auf dem Klon neu erstellt:<br /><br />customspn/DC1:202 INVALID USE OF SYMBOLS *wird neu erstellt*<br /><br />customspn/DC1 INVALID USE OF SYMBOLS *wird neu erstellt*<br /><br />customspn/DC1.corp.contoso.com:202 INVALID USE OF SYMBOLS *wird neu erstellt*<br /><br />customspn/DC1.corp.contoso.com INVALID USE OF SYMBOLS *wird neu erstellt*|  
|**Lösung und Hinweise**|Dies ist eine Einschränkung des Benennungsvorgangs für Domänencontroller in Windows, nicht nur beim Klonen. Dreiteilige SPNS werden in keinem Szenario von der Benennungslogik verarbeitet. Die meisten in Windows enthaltenen Dienste sind davon nicht betroffen, da sie alle fehlenden SPNs nach Bedarf neu erstellen. Für andere Anwendungen ist möglicherweise eine manuelle Eingabe des SPN erforderlich, um das Problem zu beheben.<br /><br />Beschrieben in KB 2742874.|  

|||  
|-|-|  
|**Problem:**|**Klonen schlägt fehl, startet DSRM, allgemeine Netzwerkfehler**|  
|**On**|Das Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet Es sind allgemeine Netzwerkfehler vorhanden.|  
|Lösung und Hinweise|Stellen Stellen Sie sicher, dass dem neuen Klon keine doppelte statische MAC-Adresse vom Quelldomänencontroller zugewiesen wurde. Sie können sehen, ob ein virtueller Computer statische MAC-Adressen verwendet, indem Sie den folgenden Befehl auf dem Hypervisorhost für den Quell- und den geklonten virtuellen Computer ausführen:<br /><br />Get-VM-VMName *Test-VM* &#124; Get-vmnetworkadapter &#124; FL *<br /><br />Ändern Sie die MAC-Adresse in eine eindeutige statische Adresse, oder stellen Sie auf die Verwendung von dynamischen MAC-Adressen um.<br /><br />Beschrieben in KB 2742844.|  

|                          |                                                                                                                                                                                                                                                                                                                                                                 |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **Problem:**         |                                                                                                                                               **Beim Klonen tritt ein Fehler auf, der DSRM als Duplikat des Quell Domänen Controllers startet.**                                                                                                                                                |
|       **On**       |                                     Ein neuer Klon wird ohne Klonen gestartet. Die Datei dccloneconfig.xml wird nicht umbenannt, und der Server startet im Domänendienst-Wiederstellungsmodus. Das Verzeichnisdienst-Ereignisprotokoll zeigt Fehler 2164 an.<br /><br />*<COMPUTERNAME>* konnte den dsrolesvc-Dienst nicht starten, um den lokalen virtuellen Domänen Controller zu klonen.                                      |
| **Lösung und Hinweise** | Untersuchen Sie die Diensteinstellungen für den DS-Rollenserverdienst (DsRoleSvc), und stellen Sie sicher, dass der Starttyp auf Manuell festgelegt ist. Vergewissern Sie sich, dass kein Drittanbieterprogramm das Starten dieses Diensts verhindert.<br /><br />Weitere Informationen dazu, wie Sie diesen sekundären Domänencontroller freigeben und gleichzeitig sicherstellen, dass Updates ausgehend repliziert werden, finden Sie im Microsoft KB-Artikel 2742970. |

|||  
|-|-|  
|**Problem:**|**Das Klonen schlägt fehl, startet in DSRM, Fehler 8610**|  
|**On**|Der Klon wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet. In der Datei Dcpromo .log wird Fehler 8610 angezeigt (das heißt ERROR_DS_ROLE_NOT_VERIFIED 8610 oder 0x21A2)|  
|**Lösung und Hinweise**|Dies passiert, wenn der PDC sichtbar sein kann, aber keine ausreichende Replikation durchgeführt hat, um die Übernahme der Rolle selbst zuzulassen. Beispielsweise, wenn das Klonen gestartet wird und ein anderer Administrator die Rolle PDCE FSMO zu einem neuen Domänencontroller verschiebt.<br /><br />Beschrieben in KB 2742916.|  

|||  
|-|-|  
|**Problem:**|**Klonen schlägt fehl, startet DSRM, allgemeine Netzwerkfehler**|  
|**On**|Der Klon wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet. Es sind allgemeine Netzwerkfehler vorhanden.|  
|**Lösung und Hinweise**|Stellen Stellen Sie sicher, dass dem neuen Klon keine doppelte statische MAC-Adresse vom Quelldomänencontroller zugewiesen wurde. Sie können sehen, ob ein virtueller Computer statische MAC-Adressen verwendet, indem Sie den folgenden Befehl auf dem Hyper-V-Host für den Quell- und den geklonten virtuellen Computer ausführen:<br /><br />Get-VM-VMName *Test-VM* &#124; Get-vmnetworkadapter &#124; FL *<br /><br />Ändern Sie die MAC-Adresse in eine eindeutige statische Adresse, oder stellen Sie auf die Verwendung von dynamischen MAC-Adressen um.<br /><br />Beschrieben in KB 2742844.|  

|||  
|-|-|  
|**Problem:**|**Fehler beim Klonen, starten im DSRM**|  
|**On**|Der Klon wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet.|  
|**Lösung und Hinweise**|Stellen Sie sicher, dass die Datei dccloneconfig.xml die Schemadefinition enthält (siehe sampledccloneconfig.xml, Zeile 2):<br /><br />**< d3c: dccloneconfig xmlns:d3c = "URI:Microsoft. com: Schemas: dccloneconfig" >**<br /><br />Beschrieben in KB 2742844.|  

|||  
|-|-|  
|Problem|**Bei der Protokollierung bei DSRM sind keine Anmelde Server verfügbar.**|  
|**On**|Das Klonen wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet Sie versuchen sich anzumelden und erhalten den Fehler:<br /><br />**Zurzeit stehen keine Anmelde Server zur Verfügung, um die Anmelde Anforderung zu bedienen.**|  
|**Lösung und Hinweise**|Stellen Stellen Sie sicher, dass Sie sich mit dem DSRM-Administratorkonto und nicht dem Domänenkonto anmelden. Verwenden Sie den linken Pfeil, und geben den folgenden Benutzer ein:<br /><br />**.\administrator**<br /><br />Beschrieben in KB 2742908.|  

|||  
|-|-|  
|**Problem:**|**Klon Quelle schlägt fehl bei DSRM, Fehler**|  
|**On**|Während des Klonens wird Fehler 8437 „Fehler beim Erstellen von Domänencontrollerobjekten auf PDC (0x20f5)“ angezeigt|  
|**Lösung und Hinweise**|Ein doppelter Computername wurde in DCCloneConfig.xml als Quelldomänencontroller oder ein vorhandener Domänencontroller festgelegt. Der Computername muss außerdem im NetBIOS-Computernamenformat sein (höchstens 15 Zeichen, kein FQDN).<br /><br />Korrigieren Sie die Datei dccloneconfig.xml, indem Sie einen eindeutigen, gültigen Namen festlegen.<br /><br />Beschrieben in KB 2742959.|  

|||  
|-|-|  
|**Problem:**|**New-addccloneconfigfile-Fehler "der Index lag außerhalb des gültigen Bereichs"**|  
|**On**|Bei der Ausführung des Cmdlets new-addccloneconfigfile erhalten Sie die Fehlermeldung:<br /><br />Index lag außerhalb des zulässigen Bereichs. Er muss nicht negativ und kleiner als die Auflistung sein.|  
|**Lösung und Hinweise**|Sie müssen das Cmdlet in einer Windows PowerShell-Konsole mit Administratorrechten ausführen. Der Fehler wird durch eine fehlende Mitgliedschaft in der Gruppe der lokalen Administratoren auf dem Computer verursacht.<br /><br />Beschrieben in KB 2742927.|  

|||  
|-|-|  
|**Problem:**|**Fehler beim Klonen, doppelter DC**|  
|**On**|Klon wird ohne Klonen gestartet und dupliziert vorhandenen Domänencontroller|  
|**Lösung und Hinweise**|Der Computer wurde kopiert und gestartet, enthält aber keine DcCloneConfig.xml-Datei an einem der unterstützten Speicherorte und hat keine doppelte IP-Adresse mit dem Quelldomänencontroller. Der Domänencontroller muss ordnungsgemäß entfernt werden, um einen Datenverlust zu vermeiden.<br /><br />Beschrieben in KB 2742970.|  

|||  
|-|-|  
|**Problem:**|**New-addccloneconfigfile schlägt fehl, wenn der Server nicht funktionstüchtig ist, wenn überprüft wird, ob der Quell Domänen Controller Mitglied der Gruppe klonbare Domänen Controller ist, wenn kein GC verfügbar ist.**|  
|**On**|Beim Ausführen von New-ADDCCloneConfigFile zum Erstellen einer dccloneconfig.xml-Datei erhalten Sie die folgende Fehlermeldung:<br /><br />Code: der Server ist nicht betriebsbereit.|  
|**Lösung und Hinweise**|Überprüfen Sie die Konnektivität mit einem globalen Katalogserver von dem Server, auf dem Sie New-ADDCCloneConfigFile ausführen, und vergewissern Sie sich, dass die Mitgliedschaft des Quelldomänencontrollers in der Gruppe „Klonbare Domänencontroller“ an diesen globalen Katalogserver repliziert wurde.<br /><br />Führen Sie den folgenden Befehl als Mittel aus, um den Locatorcache des Domänencontrollers in Fällen zu leeren, in denen ein globaler Katalogserver oder ein Domänencontroller kürzlich offline geschaltet wurde:<br /><br />Code-nltest/dsgetdc:/GC/Force|  

### <a name="advanced-troubleshooting"></a>Erweiterte Fehlerbehandlung  
In diesem Modul erfahren Sie mehr über die erweiterte Fehlerbehandlung, indem *funktionierende* Protokolle als Beispiele verwendet und Erläuterungen zu den Ereignissen bereitgestellt werden. Wenn Sie verstehen, wie ein erfolgreicher Vorgang auf einem virtualisierten Quelldomänencontroller aussieht, werden Fehler in Ihrer Umgebung offensichtlich. Diese Protokolle werden nach ihrer Quelle dargestellt, aufsteigend in der Reihenfolge *erwarteter* Ereignisse (auch wenn es sich um Warnungen und Fehler handelt) in jedem Protokoll, die mit einem geklonten Domänencontroller zusammenhängen.  

#### <a name="cloning-a-domain-controller"></a>Klonen eines Domänencontrollers  
In diesem Beispiel verwendet der geklonte Domänencontroller DHCP, um eine IP-Adresse abzurufen, repliziert SYSVOL über FRS oder DFSR (sehen Sie sich bei Bedarf das entsprechende Protokoll an), ist ein globaler Katalogserver und verwendet eine leere dccloneconfig.xml-Datei.  

##### <a name="directory-services-event-log"></a>Verzeichnisdienst-Ereignisprotokoll  
Das Verzeichnisdienst-Ereignisprotokoll enthält den größten Teil der ereignisbasierten Betriebsinformationen beim Klonen. Der Hypervisor ändert die VM-Generations-ID. Der NTDS-Dienst bemerkt dies, macht den RID-Pool ungültig und ändert die Aufrufkennung. Die neue VM-Generations-ID wird festgelegt, und der Server repliziert Active Directory-Daten eingehend. Der DFSR-Dienst wird angehalten, und seine Datenbank, die SYSVOL hostet, wird gelöscht, wodurch eine nicht autoritative eingehende Synchronisierung erzwungen wird. Der hohe USN-Grenzwert wird angepasst.  


|              |                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** |          **Quelle**           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  **Nachricht**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|   **2160**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                         Von der lokalen Instanz der Active Directory-Domänendienste wurde eine Klonkonfigurationsdatei für virtuelle Domänencontroller gefunden.<br /><br />Fundstelle der Klonkonfigurationsdatei:<br /><br />*<path>* \dccloneconfig.XML<br /><br />Das Vorliegen einer Klonkonfigurationsdatei lässt darauf schließen, dass der lokale virtuelle Domänencontroller ein Klon eines anderen virtuellen Domänencontrollers ist. Es wird begonnen, die Active Directory -Domänendienste zu klonen.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|   **2191**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                             Fehler beim Festlegen des unten stehenden Registrierungswerts zum Deaktivieren von DNS-Aktualisierungen durch die Active Directory-Domänendienste.<br /><br />Registrierungsschlüssel:<br /><br />SYSTEM\CurrentControlSet\Services\Netlogon\Parameters<br /><br />Registrierungswert:<br /><br />UseDynamicDns<br /><br />Registrierungswertdaten:<br /><br />0<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. Nach dem Klonen werden DNS-Aktualisierungen vom Klonprozess wieder aktiviert.                                                                                                                                                                                                                                                                                                                                                                                              |
|   **2191**   | ActiveDirectory_DomainService | Fehler beim Festlegen des unten stehenden Registrierungswerts zum Deaktivieren von DNS-Aktualisierungen durch die Active Directory-Domänendienste.<br /><br />Registrierungsschlüssel:<br /><br />SYSTEM\CurrentControlSet\Services\Dnscache\Parameters<br /><br />Registrierungswert:<br /><br />RegistrationEnabled<br /><br />Registrierungswertdaten:<br /><br />0<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. Nach dem Klonen werden DNS-Aktualisierungen vom Klonprozess wieder aktiviert.<br /><br />"Information 2/7/2012 3:12:49 pm Microsoft-Windows-ActiveDirectory_DomainService 2191 Internal Configuration" Active Directory Domain Services legen Sie den folgenden Registrierungs Wert fest, um DNS-Updates zu deaktivieren.<br /><br />Registrierungsschlüssel:<br /><br />SYSTEM\CurrentControlSet\Services\Tcpip\Parameters<br /><br />Registrierungswert:<br /><br />DisableDynamicUpdate<br /><br />Registrierungswertdaten:<br /><br />1<br /><br />Während des Klonens sind die Computernamen des lokalen Computers und des Quellcomputers möglicherweise kurzzeitig identisch. Für diese Zeitspanne wird die Registrierung von DNS A- und AAAA-Datensätzen deaktiviert, sodass Clients keine Anforderungen an den lokalen Computer senden können. Nach dem Klonen werden DNS-Aktualisierungen vom Klonprozess wieder aktiviert. |
|   **2172**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Das msDS-GenerationId-Attribut des Domänencontrollers wurde gelesen.<br /><br />Wert des msDS-GenerationId-Attributs:<br /><br />*<Number>*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|   **2170**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                           Es wurde keine Änderung der Generations-ID erkannt.<br /><br />Zwischengespeicherte Generations-ID in DS (alter Wert):<br /><br />*<Number>*<br /><br />Aktuelle Generations-ID des virtuellen Computers (neuer Wert):<br /><br />*<Number>*<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Von den Active Directory-Domänendiensten wird eine neue Aufruf-ID zur Wiederherstellung des Domänencontrollers erstellt. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde.                                                                                                                                                                                                                                                                                                                           |
|   **1109**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                           Das invocationID-Attribut für diesen Domänencontroller wurde geändert. Die höchste Aktualisierungssequenznummer zum Zeitpunkt der Erstellung der Sicherung lautet wie folgt:<br /><br />InvocationID-Attribut (alter Wert):<br /><br />*<GUID>*<br /><br />InvocationID-Attribut (neuer Wert):<br /><br />*<GUID>*<br /><br />Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Die Aufruf-ID (invocationID-Attribut) wird in den folgenden Situationen geändert: nach Wiederherstellung des Verzeichnisservers von einem Sicherungsmedium, nach Konfiguration des Verzeichnisservers als Host einer beschreibbaren Anwendungsverzeichnispartition, bei fortgesetzter Ausführung des Verzeichnisservers, nachdem eine Momentaufnahme des virtuellen Computers angewendet wurde, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde.                                                                                                                                                                                                                            |
|   **1000**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          Das Starten der Microsoft-Active Directory-Domänendienste wurde abgeschlossen.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|   **1394**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Alle Probleme, die Aktualisierungen der Active Directory-Domänendienste-Datenbank verhinderten, wurden behoben. Neue Aktualisierungen der Active Directory-Domänendienste-Datenbank sind erfolgreich. Der Netzwerkanmeldedienst wird neu gestartet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|   **2163**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  Der DsRoleSvc-Dienst zum Klonen des lokalen virtuellen Domänencontrollers wurde gestartet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|   **326**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                NTDS (536) NTDSA: Das Datenbankmodul hat eine Datenbank angefügt (1, C:\Windows\NTDS\ntds.dit). (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.016, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000.<br /><br />Gespeicherter Cache: 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|   **103**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  NTDS (536) NTDSA: Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.032, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|   **102**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             NTDS (536) NTDSA: Das Datenbankmodul (6.02.8225.0000) startet eine neue Instanz (0).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **105**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               NTDS (536) NTDSA: Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.016, [2] 0.000, [3] 0.015, [4] 0.078, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.046, [10] 0.000, [11] 0.000.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|   **1004**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          Die Active Directory-Domänendienste wurden heruntergefahren.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|   **102**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             NTDS (536) NTDSA: Das Datenbankmodul (6.02.8225.0000) startet eine neue Instanz (0).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **326**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                NTDS (536) NTDSA: Das Datenbankmodul hat eine Datenbank angefügt (1, C:\Windows\NTDS\ntds.dit). (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.015, [3] 0.016, [4] 0.000, [5] 0.031, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000.<br /><br />Gespeicherter Cache: 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|   **105**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               NTDS (536) NTDSA: Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit=1 Sekunde)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.031, [2] 0.000, [3] 0.000, [4] 0.391, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.000.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|   **1109**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                           Das invocationID-Attribut für diesen Domänencontroller wurde geändert. Die höchste Aktualisierungssequenznummer zum Zeitpunkt der Erstellung der Sicherung lautet wie folgt:<br /><br />InvocationID-Attribut (alter Wert):<br /><br />*<GUID>*<br /><br />InvocationID-Attribut (neuer Wert):<br /><br />*<GUID>*<br /><br />Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Die Aufruf-ID (invocationID-Attribut) wird in den folgenden Situationen geändert: nach Wiederherstellung des Verzeichnisservers von einem Sicherungsmedium, nach Konfiguration des Verzeichnisservers als Host einer beschreibbaren Anwendungsverzeichnispartition, bei fortgesetzter Ausführung des Verzeichnisservers, nachdem eine Momentaufnahme des virtuellen Computers angewendet wurde, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde.                                                                                                                                                                                                                            |
|   **1168**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Interner Fehler: Ein Fehler bei den Active Directory-Domänendiensten ist aufgetreten.<br /><br />Weitere Daten<br /><br />Fehlerwert (dezimal):<br /><br />2<br /><br />Fehlerwert (hexadezimal):<br /><br />2<br /><br />Interne ID:<br /><br />7011658                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|   **1110**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                           Das Heraufstufen dieses Servers zum globalen Katalog wird um das folgende Intervall verzögert.<br /><br />Intervall (Minuten):<br /><br />5<br /><br />Diese Verzögerung ist notwendig, damit die erforderlichen Partitionen vorbereitet werden können, bevor der globale Katalog angekündigt wird. Sie können in der Registrierung die Anzahl an Sekunden angeben, die der Verzeichnissystem-Agent vor dem Heraufstufen des Domänencontrollers zum globalen Katalog warten soll, Weitere Informationen zum Registrierungswert Global Catalog Delay Advertisement finden Sie im Resource Kit Distributed Systems Guide.                                                                                                                                                                                                                                                                                                                                                                                                                            |
|   **103**    |           NTDS ISAM           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  NTDS (536) NTDSA: Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.047, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.016, [10] 0.000, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|   **1004**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          Die Active Directory-Domänendienste wurden heruntergefahren.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|   **1539**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  Die Active Directory-Domänendienste konnten den softwarebasierten Datenträgerschreibungscache auf der folgenden Festplatte nicht deaktivieren.<br /><br />Festplatte:<br /><br />c:<br /><br />Möglicherweise gehen Daten bei einem Systemfehler verloren.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|   **2179**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  Für das msDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers wurde der folgende Parameter festgelegt:<br /><br />Generations-ID-Attribut:<br /><br />*<Number>*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|   **2173**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      Fehler beim Lesen des msDS-GenerationId-Attributs des Computerobjekts des Domänencontrollers. Mögliche Ursachen sind, dass eine Datenbanktransaktion nicht korrekt ausgeführt wurde oder dass die Generations-ID in der lokalen Datenbank nicht vorhanden ist. Zu bedenken ist auch, dass beim ersten Neustart nach einem DCPromo-Vorgang noch kein msDS-GenerationId-Attribut vorhanden ist.<br /><br />Weitere Daten<br /><br />Fehlercode:<br /><br />6                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|   **1000**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Das Starten der Microsoft-Active Directory-Domänendienste wurde abgeschlossen. Version 6.2.8225.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|   **1394**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Alle Probleme, die Aktualisierungen der Active Directory-Domänendienste-Datenbank verhinderten, wurden behoben. Neue Aktualisierungen der Active Directory-Domänendienste-Datenbank sind erfolgreich. Der Netzwerkanmeldedienst wird neu gestartet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|   **1128**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      1128 Konsistenzprüfung "Eine Replikationsverbindung wurde vom folgenden Quellverzeichnisdienst zum lokalen Verzeichnisdienst erstellt.<br /><br />Quellverzeichnisdienst:<br /><br />CN = NTDS-Einstellungen, *<Domain Controller DN>*<br /><br />Lokaler Verzeichnisdienst:<br /><br />CN = NTDS-Einstellungen, *<Domain Controller DN>*<br /><br />Weitere Daten<br /><br />Begründung: Code:<br /><br />0x2<br /><br />Interne Kennung für Erstellungspunkt:<br /><br />f0a025d                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|   **1999**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                           Der Quellverzeichnisdienst hat die Aktualisierungssequenznummer optimiert, die vom Zielverzeichnisdienst dargestellt wird. Der Quell- und der Zielverzeichnisdienst haben einen gemeinsamen Replikationspartner. Der Zielverzeichnisdienst ist auf dem gleichen Stand wie der gemeinsame Replikationspartner, und der Quellverzeichnisdienst wurde mit Hilfe einer Sicherung dieses Partners installiert.<br /><br />Kennung des Zielverzeichnisdiensts:<br /><br />*<GUID> (<FQDN>)*<br /><br />Kennung des gemeinsamen Verzeichnisdiensts:<br /><br />*<GUID>*<br /><br />Gemeinsame Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Als Folge dessen wurde der Aktualitätsvektor des Zielverzeichnisdienstes mit den folgenden Einstellungen konfiguriert.<br /><br />Vorherige Objekt-Aktualisierungssequenznummer:<br /><br />0<br /><br />Vorherige Eigenschafts-Aktualisierungssequenznummer:<br /><br />0<br /><br />Datenbank-GUID:<br /><br />*<GUID>*<br /><br />Objekt-Aktualisierungssequenznummer:<br /><br />*<Number>*<br /><br />Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<Number>*                                                                                                                                                                                                                                           |

##### <a name="system-event-log"></a>Systemereignisprotokoll  
Die nächsten Hinweise zu Klonvorgängen befinden sich im Systemereignisprotokoll. Wenn der Hypervisor dem Gastcomputer mitteilt, dass er geklont oder aus einer Momentaufnahme wiederhergestellt wurde, macht der Domänencontroller sofort seinen RID-Pool ungültig, um ein späteres Duplizieren von Sicherheitsprinzipalen zu vermeiden. Wenn das Klonen fortgesetzt wird, kommt es zu verschiedenen erwarteten Vorgängen und Meldungen, hauptsächlich rund um das Starten und Anhalten von Diensten und die dadurch verursachten Fehler. Nach Abschluss des Klonvorgangs notiert das Systemereignisprotokoll einen Erfolg des gesamten Klonvorgangs.  

||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**16654**|Verzeichnisdienste-SAM|Ein Pool aus Kontobezeichnern (RIDs) wurde ungültig gemacht. Dies kann in den folgenden zu erwartenden Fällen auftreten:<br /><br />1. Ein Domänencontroller wurde aus einer Datensicherung wiederhergestellt.<br /><br />2. Ein Domänencontroller auf einem virtuellen Computer wurde aus einer Momentaufnahme wiederhergestellt.<br /><br />3. Ein Administrator hat den Pool manuell ungültig gemacht.|  
|**7036**|Dienststeuerungs-Manager|Der Dienst der Active Directory-Verzeichnisdienste wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Dienst für das Kerberos-Schlüsselverteilungscenter wird jetzt ausgeführt.|  
|**3096**|Netlogon|Der primäre Domänencontroller für diese Domäne konnte nicht gefunden werden.|  
|**7036**|Dienststeuerungs-Manager|Der Dienst für den Sicherheitskonten-Manager wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Serverdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Die Active Directory-Webdienste werden jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der DFS-Replikationsdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Dateireplikationsdienst wird jetzt ausgeführt.|  
|**14533**|Microsoft-Windows-DfsSvc|DFS hat alle Namespaces erstellt.|  
|**14531**|Microsoft-Windows-DfsSvc|DFS-Server wurde vollständig initialisiert.|  
|**7036**|Dienststeuerungs-Manager|Der DFS-Namespacedienst wird jetzt ausgeführt.|  
|**7023**|Dienststeuerungs-Manager|Der standortübergreifende Messagingdienst wurde mit folgendem Fehler beendet:<br /><br />Der angegebene Server kann den angeforderten Vorgang nicht ausführen.|  
|**7036**|Dienststeuerungs-Manager|Der standortübergreifende Messagingdienst wurde beendet.|  
|**5806**|Netlogon|Dynamische Aktualisierungen wurden auf diesem Domänencontroller manuell deaktiviert.<br /><br />BENUTZERAKTION<br /><br />Konfigurieren Sie diesen Domänencontroller zur Verwendung dynamischer Aktualisierungen neu, oder fügen Sie die DNS-DNS-Datensätze aus der Datei '%SystemRoot%\System32\Config\Netlogon.dns' manuell zur DNS-Datenbank hinzu.|  
|**16651**|Verzeichnisdienste-SAM|Die Anforderung eines neuen Kontenidentifizierungspool ist fehlgeschlagen. Der Vorgang wird solange wiederholt, bis er erfolgreich ausgeführt wird. Der Fehler ist:<br /><br />Der angeforderte FSMO-Vorgang konnte nicht ausgeführt werden. Der aktuelle FSMO-Inhaber war nicht erreichbar.|  
|**7036**|Dienststeuerungs-Manager|Der DNS-Serverdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der DS-Rollenserverdienst wird jetzt ausgeführt.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Dateireplikationsdienst wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Dienst für das Kerberos-Schlüsselverteilungscenter wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der DNS-Serverdienst wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Dienst der Active Directory-Verzeichnisdienste wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wird jetzt ausgeführt.|  
|**7040**|Dienststeuerungs-Manager|Der Starttyp der Active Directory-Domänendienste wurde von automatischem Start zu deaktiviert geändert.|  
|**7036**|Dienststeuerungs-Manager|Der Netlogon-Dienst wurde beendet.|  
|**7036**|Dienststeuerungs-Manager|Der Dateireplikationsdienst wird jetzt ausgeführt.|  
|**29219**|DirectoryServices-DSROLE-Server|Der virtuelle Domänencontroller wurde erfolgreich geklont.|  
|**29223**|DirectoryServices-DSROLE-Server|Dieser Server ist jetzt ein Domänencontroller.|  
|**29265**|DirectoryServices-DSROLE-Server|Der virtuelle Domänencontroller wurde erfolgreich geklont. Die für das Klonen des virtuellen Domänencontrollers verwendete Konfigurationsdatei C:\Windows\NTDS\DCCloneConfig.xml wurde in C:\Windows\NTDS\DCCloneConfig.20120207-151533.xml umbenannt.|  
|**1074**|User32|Der Prozess C:\Windows\system32\lsass.exe (DC2) hat den Neustart des Computers DC2 für Benutzer NT AUTHORITY\SYSTEM aus dem folgenden Grund initiiert: Betriebssystem: Neukonfigurierung (geplant)<br /><br />Begründung: Code: 0x80020004<br /><br />Herunterfahrtyp: Neustart<br /><br />Kommentar: „|  

##### <a name="dcpromolog"></a>DCPROMO.LOG  
Dcpromo.log enthält den tatsächlichen Heraufstufungsteil des Klonvorgangs, der im Verzeichnisdienst-Ereignisprotokoll nicht beschrieben ist. Das das Protokoll keine Erläuterung zur Bedeutung der Ereignisprotokolleinträge bietet, enthält dieser Abschnitt des Moduls zusätzliche Anmerkungen.  

Der Heraufstufungsprozess bedeutet, dass der Klonvorgang beginnt, der Domänencontroller von seiner aktuellen Konfiguration bereinigt und über die vorhandene AD-Datenbank erneut heraufgestuft wird (ähnlich einer IFM-Heraufstufung). Dann repliziert der Domänencontroller eingehende Änderungsdeltas von AD und SYSVOL, und das Klonen ist abgeschlossen.  

> [!NOTE]  
> Das Protokoll wurde in diesem Modul aus Gründen der besseren Lesbarkeit geändert, indem die Datumsspalte entfernt wurde.  

> [!NOTE]  
> Ein weitere Erläuterung zu dcpromo.log finden Sie unter „Grundlegendes über und Problembehandlung für die vereinfachte AD DS-Verwaltung in Windows Server 2012“.  
>   
> [https://go.microsoft.com/fwlink/p/?LinkId=237244](https://go.microsoft.com/fwlink/p/?LinkId=237244)  

-   Starten der klonbasierten Heraufstufung  

-   Setzen Sie das Kennzeichen für den Verzeichnisdienst-Wiederherstellungsmodus, damit der Server nicht wieder normal neu gestartet wird wie der ursprüngliche Klon und Benennungs- oder Verzeichnisdienstkollisionen verursacht.  

-   Aktualisieren Sie das Verzeichnisdienst-Ereignisprotokoll.  

```  
15:14:01 [INFO] vDC Cloneing: Setting Boot into DSRM flag succeeded.  
15:14:01 [WARNING] Cannot get user Token for Format Message: 1725l  
15:14:01 [INFO] vDC Cloning: Created vDCCloningUpdate event.  
15:14:01 [INFO] vDC Cloning: Created vDCCloningComplete event.  
```  

-   Beenden Sie den NetLogon-Dienst, damit der Domänencontroller nicht ankündigt.  

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

-   Untersuchen Sie die Datei dccloneconfig.xml auf administratorspezifische Anpassungen.  

-   In diesem Beispielfall ist die Datei leer, sodass alle Einstellungen automatisch generiert werden und eine automatische IP-Adressierung vom Netzwerk erforderlich ist.  

```  
15:14:02 [INFO] vDC Cloning: Clone config file C:\Windows\NTDS\DCCloneConfig.xml is considered to be a blank file (containing 0 bytes)  
15:14:02 [INFO] vDC Cloning: Parsing clone config file C:\Windows\NTDS\DCCloneConfig.xml returned HRESULT 0x0  
```  

-   Vergewissern Sie sich, dass keine Dienste oder Programme installiert sind, die nicht Teil von DefaultDCCloneAllowList.xml oder CustomDCCloneAllowList.xml sind.  

```  
15:14:02 [INFO] vDC Cloning: Checking allowed list:  
15:14:03 [INFO] vDC Cloning: Completed checking allowed list:  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  

-   Aktivieren Sie DHCP auf den Netzwerkadaptern, da die IP-Informationen nicht vom Administrator angegeben wurden.  

```  
15:14:03 [INFO] vDC Cloning: Enable DHCP:  
15:14:03 [INFO] WMI Instance: Win32_NetworkAdapterConfiguration.Index=12  
15:14:03 [INFO] Method: EnableDHCP  
15:14:03 [INFO] HRESULT code: 0x0 (0)  
15:14:03 [INFO] Return Value: 0x0 (0)  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  

-   Suchen Sie nach dem PDC-Emulator.  

-   Legen Sie den Standort des Klons fest (wird in diesem Fall automatisch generiert).  

-   Legen Sie den Namen des Klons fest (wird in diesem Fall automatisch generiert).  

```  
15:14:03 [INFO] vDC Cloning: Found PDC. Name: DC1.root.fabrikam.com  
15:14:04 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:04 [INFO] vDC Cloning: Winlogon UI Notification #1: Domain Controller cloning is at 5% completion...  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #2: Domain Controller cloning is at 10% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Site of the cloned DC: Default-First-Site-Name  
```  

-   Erstellen Sie das neue Kloncomputerobjekt.  

-   Benennen Sie den Klon gemäß dem neuen Namen um.  

```  
15:14:05 [INFO] vDC Cloning: Clone DC objects are created on PDC.  
15:14:05 [INFO] Name of the cloned DC: DC2-CL0001  
15:14:05 [INFO] DsRolepSetRegStringValue on System\CurrentControlSet\Services\NTDS\Parameters\CloneMachineName to DC2-CL0001 returned 0  
15:14:05 [INFO] vDC Cloning: Save CloneMachineName in registry: 0x0 (0)  
```  

-   Stellen Sie die Einstellungen für die Heraufstufung bereit, basierend auf der früheren dccloneconfig.xml oder automatischen Generierungsregeln.  

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

-   Starten Sie die Heraufstufung.  

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

-   Stoppen Sie, und konfigurieren Sie alle AD DS-relevanten Dienste (NTDS, NTFRS/DFSR, KDC, DNS).  

> [!NOTE]  
> Dass der DNS-Dienst zum Herunterfahren lange braucht, ist in diesem Szenario erwartet, da er AD-integrierte Zonen verwendet, die auch vor dem Stoppen des NTDS-Diensts nicht mehr verfügbar waren. Weitere Informationen dazu finden Sie in den später in diesem Abschnitt des Moduls beschriebenen DNS-Ereignissen.  

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

-   Erzwingen Sie die NT5DS (NTP)-Zeitsynchronisierung mit einem anderen Domänencontroller (normalerweise dem PDCE).  

```  
15:15:02 [INFO] Forcing time sync  
```  

-   Kontaktieren Sie einen Domänencontroller, auf dem das Konto des Quelldomänencontrollers des Klons vorhanden ist.  

-   Löschen Sie alle vorhandenen Kerberos-Tickets.  

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

-   Stoppen Sie den NetLogon-Dienst, und legen Sie seinen Starttyp fest.  

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

-   Konfigurieren Sie die automatische Ausführung für die DFSR/NTFRS-Dienste.  

-   Löschen Sie ihre vorhandenen Datenbankdateien, um eine nicht autoritative Synchronisierung von SYSVOL beim nächsten Start des Dienstes zu erzwingen.  

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

-   Starten Sie den Heraufstufungsprozess mit der vorhandenen NTDS-Datenbankdatei.  

-   Kontaktieren Sie den RID-Master.  

> [!NOTE]  
> Der AD DS-Dienst ist hier nicht tatsächlich installiert, dies ist eine Vorversionsinstrumentation im Protokoll.  

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

-   Ändern Sie die vorhandene Aufruf-ID, die in der Datenbank des Quellcomputers vorhanden war.  

-   Erstellen Sie ein neues NTDS-Einstellungsobjekt für diesen Klon.  

-   Replizieren Sie das AD-Objektdelta vom Partnerdomänencontroller.  

> [!NOTE]  
> Auch wenn alle Objekte als repliziert aufgelistet sind, handelt es sich nur um Metadaten, die für die Zusammenfassung der Aktualisierungen erforderlich sind. Alle unveränderten Objekte in der geklonten NTDS-Datenbank sind bereits vorhanden und müssen nicht erneut repliziert werden, wie bei der Verwendung der IFM-basierten Heraufstufung.  

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

-   Schließen Sie den kritischen AD DS-Teil der Heraufstufung ab.  

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

-   Schließen Sie die eingehende Replikation von SYSVOL ab.  

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

-   Aktivieren Sie die Client-DNS-Registrierung.  

```  
15:15:18 [INFO] vDC Cloning: Set DisableDynamicUpdate reg value to 0 to enable dynamic update records registration.  
15:15:18 [INFO] vDC Cloning: Set UseDynamicDns reg value to 1 to enable dynamic update records registration.  
15:15:18 [INFO] vDC Cloning: Set RegistrationEnabled reg value to 1 to enable dynamic update records registration.  
```  

-   Führen Sie die SYSPREP-Module aus, die vom DefaultDCCloneAllowList.xml <SysprepInformation>-Element angegeben werden.  

```  
15:15:18 [INFO] vDC Cloning: Running sysprep providers.  
15:15:32 [INFO] vDC Cloning: Completed running sysprep providers.  
```  

-   Die Heraufstufung des Klonvorgangs ist abgeschlossen.  

-   Entfernen Sie das DSRM-Startkennzeichen, damit der Server beim nächsten Mal normal gestartet wird.  

-   Benennen Sie die Datei dccloneconfig.xml um, damit Sie nicht beim nächsten Start erneut gelesen wird.  

-   Starten Sie den Computer neu.  

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

##### <a name="active-directory-web-services-event-log"></a>Ereignisprotokoll der Active Directory-Webdienste  
Während des Klonens ist die NTDS.DIT-Datenbank oft für längere Zeit offline geschaltet. Der ADWS-Dienst protokolliert dafür mindestens ein Ereignis. Wenn das Klonen abgeschlossen ist, wird der ADWS-Dienst neu gestartet und bemerkt, dass noch kein gültiges Computerzertifikat vorhanden ist (je nachdem, ob In Ihrer Umgebung eine Microsoft PKI mit automatischer Registrierung vorhanden ist, kann dies sein oder nicht), und startet dann die Instanz für den neuen Domänencontroller.  

||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**1202**|Ereignisse der ADWS-Instanz|Auf diesem Computer wird nun die angegebene Verzeichnisinstanz gehostet, doch konnte diese von Active Directory-Webdiensten nicht bedient werden. Von Active Directory-Webdiensten wird in regelmäßigen Abständen erneut versucht, den Vorgang auszuführen.<br /><br />Verzeichnisinstanz: NTDS<br /><br />LDAP-Port der Verzeichnisinstanz: 389<br /><br />SSL-Port der Verzeichnisinstanz: 636|  
|**1000**|Ereignisse der ADWS-Instanz|Die Active Directory-Webdienste werden gestartet.|  
|**1008**|Ereignisse der ADWS-Instanz|Die Sicherheitsberechtigungen von Active Directory-Webdiensten wurden erfolgreich reduziert.|  
|**1100**|Ereignisse der ADWS-Instanz|Die Werte im Abschnitt <appsettings> der Konfigurationsdatei der Active Directory-Webdienste wurden fehlerfrei geladen.|  
|**1400**|Ereignisse der ADWS-Instanz|ADWS-Zertifikatereignisse"Von den Active Directory-Webdiensten konnte kein Serverzertifikat mit dem angegebenen Zertifikatnamen gefunden werden. Für Zertifikate ist die Verwendung von SSL/TLS-Verbindungen erforderlich. Wenn Sie SSL/TLS-Verbindungen verwenden möchten, stellen Sie sicher, dass auf dem Computer ein gültiges Serverauthentifizierungszertifikat von einer vertrauenswürdigen Zertifizierungsstelle installiert ist.<br /><br />Zertifikats Name: *<Server FQDN>*|  
|**1100**|Ereignisse der ADWS-Instanz|Die Werte im Abschnitt <appsettings> der Konfigurationsdatei der Active Directory-Webdienste wurden fehlerfrei geladen.|  
|**1200**|Ereignisse der ADWS-Instanz|Die angegebene Verzeichnisinstanz wird nun von Active Directory-Webdiensten bedient.<br /><br />Verzeichnisinstanz: NTDS<br /><br />LDAP-Port der Verzeichnisinstanz: 389<br /><br />SSL-Port der Verzeichnisinstanz: 636|  

##### <a name="dns-server-event-log"></a>Ereignisprotokoll des DNS-Servers  
Beim DNS-Dienst treten während des Klonvorgangs kurze erwartete Ausfälle auf, da der DNS-Dienst weiter ausgeführt wird, während die AD DS-Datenbank offline geschaltet ist. Dazu kommt es, wenn Sie den in Active Directory integrierten DNS verwenden, nicht, wenn Sie den standardmäßigen primären oder sekundären DNS verwenden. Diese Fehler werden mehrmals protokolliert. Nach Abschluss des Klonvorgangs ist DNS wieder ganz normal online.  

||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**4013**|DNS-Server-Service|Der DNS-Server wartet darauf, dass von den Active Directory-Domänendiensten angezeigt wird, dass die Erstsynchronisierung des Verzeichnisses durchgeführt wurde. Der DNS-Serverdienst kann erst nach der Erstsynchronisierung gestartet werden, da wichtige DNS-Daten möglicherweise noch nicht auf diesen Domänencontroller repliziert wurden. Sofern die im Ereignisprotokoll der Active Directory-Domänendienste protokollierten Ereignisse deutlich machen, dass Probleme bei der DNS-Namensauflösung vorliegen, sollte ggf. die IP-Adresse eines weiteren DNS-Servers für diese Domäne der DNS-Serverliste in den Internetprotokolleigenschaften dieses Computers hinzugefügt werden. Dieses Ereignis wird alle zwei Minuten protokolliert, bis von den Active Directory-Domänendiensten angezeigt wird, dass die Erstsynchronisierung durchgeführt wurde.|  
|**4015**|DNS-Server-Service|Der DNS-Server hat einen kritischen Active Directory-Fehler ermittelt. Stellen Sie sicher, dass Active Directory ordnungsgemäß funktioniert. Die erweiterten Fehlerdebuginformationen (die eventuell leer sind) lauten """. Die Ereignisdaten enthalten den Fehlercode.|  
|**4000**|DNS-Server-Service|Der DNS-Server konnte Active Directory nicht öffnen.  Dieser DNS-Server ist für das Abrufen und Verwenden von Informationen aus dem Verzeichnis für diese Zone konfiguriert und kann die Zone ohne die Informationen nicht laden.  Stellen Sie sicher, dass Active Directory ordnungsgemäß funktioniert, und laden Sie die Zone neu. Die Ereignisdaten enthalten den Fehlercode.|  
|**4013**|DNS-Server-Service|Der DNS-Server wartet darauf, dass von den Active Directory-Domänendiensten angezeigt wird, dass die Erstsynchronisierung des Verzeichnisses durchgeführt wurde. Der DNS-Serverdienst kann erst nach der Erstsynchronisierung gestartet werden, da wichtige DNS-Daten möglicherweise noch nicht auf diesen Domänencontroller repliziert wurden. Sofern die im Ereignisprotokoll der Active Directory-Domänendienste protokollierten Ereignisse deutlich machen, dass Probleme bei der DNS-Namensauflösung vorliegen, sollte ggf. die IP-Adresse eines weiteren DNS-Servers für diese Domäne der DNS-Serverliste in den Internetprotokolleigenschaften dieses Computers hinzugefügt werden. Dieses Ereignis wird alle zwei Minuten protokolliert, bis von den Active Directory-Domänendiensten angezeigt wird, dass die Erstsynchronisierung durchgeführt wurde.|  
|**2**|DNS-Server-Service|Der DNS-Server wurde gestartet.|  
|**4**|DNS-Server-Service|Der DNS-Server hat das Laden von Zonen im Hintergrund abgeschlossen. Alle Zonen sind nun für DNS-Aktualisierungen und Zonenübertragungen verfügbar, sofern ihre jeweilige Konfiguration dies zulässt.|  

##### <a name="file-replication-service-event-log"></a>Ereignisprotokoll des Dateireplikationsdiensts  
Der Dateireplikationsdienst synchronisiert während des Klonvorgangs nicht autoritativ von einem Partner. Der Klonvorgang erreicht dies durch Löschen der NTFRS-Datenbankdateien und unveränderten Inhalten von SYSVOL zur Verwendung als zuvor per Seeding hinzugefügte Daten. Die zwei Synchronisierungsversuche sind erwartet.  


|              |            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** | **Quelle** |                                                                                                                                                                                                                                                                                                                                                                                                                  **Nachricht**                                                                                                                                                                                                                                                                                                                                                                                                                  |
|  **13562**   |   NtFrs    |                                                                                                                                                                                                                                                                            Es folgt eine Zusammenfassung aller Warnungen und Fehler, die beim Abfragen des Domänencontrollers DC2.root.fabrikam.com der Konfigurationsinformationen des FRS-Replikatsatzes vom Dateireplikationsdienst ermittelt wurden.<br /><br />Es konnte keine Bindung mit dem Domänencontroller hergestellt werden. Der Vorgang wird beim nächsten Abrufzyklus wiederholt.                                                                                                                                                                                                                                                                            |
|  **13502**   |   NtFrs    |                                                                                                                                                                                                                                                                                                                                                                                                   Der Dateireplikationsdienst wird angehalten.                                                                                                                                                                                                                                                                                                                                                                                                   |
|  **13565**   |   NtFrs    |                                                                         Der Dateireplikationsdienst initialisiert den Systemdatenträger mit Daten eines anderen Domänencontrollers. Computer DC2 kann nicht zum Domänencontroller benannt werden, bis dieser Prozess beendet ist. Das Systemvolumen wird dann als SYSVOL geteilt.<br /><br />Um die SYSVOL-Freigabe zu überprüfen, geben Sie an der Eingabeaufforderung Folgendes ein:<br /><br />Netzwerkfreigabe<br /><br />Wenn der Dateireplikationsdienst den Initialisierungsprozess beendet, wird die SYSVOL-Freigabe angezeigt.<br /><br />Die Initialisierung des Systemdatenträgers kann einige Zeit in Anspruch nehmen. Der Zeitaufwand ist von der Datenmenge im Systemdatenträger, der Verfügbarkeit anderer Domänencontroller, und dem Replikationsintervall zwischen anderen Domänencontrollern abhängig.                                                                         |
|  **13501**   |   NtFrs    |                                                                                                                                                                                                                                                                                                                                                                                                   Der Dateireplikationsdienst wird gestartet.                                                                                                                                                                                                                                                                                                                                                                                                    |
|  **13502**   |   NtFrs    |                                                                                                                                                                                                                                                                                                                                                                                                   Der Dateireplikationsdienst wird angehalten.                                                                                                                                                                                                                                                                                                                                                                                                   |
|  **13503**   |   NtFrs    |                                                                                                                                                                                                                                                                                                                                                                                                   Der Dateireplikationsdienst wurde angehalten.                                                                                                                                                                                                                                                                                                                                                                                                   |
|  **13565**   |   NtFrs    |                                                                         Der Dateireplikationsdienst initialisiert den Systemdatenträger mit Daten eines anderen Domänencontrollers. Computer DC2 kann nicht zum Domänencontroller benannt werden, bis dieser Prozess beendet ist. Das Systemvolumen wird dann als SYSVOL geteilt.<br /><br />Um die SYSVOL-Freigabe zu überprüfen, geben Sie an der Eingabeaufforderung Folgendes ein:<br /><br />Netzwerkfreigabe<br /><br />Wenn der Dateireplikationsdienst den Initialisierungsprozess beendet, wird die SYSVOL-Freigabe angezeigt.<br /><br />Die Initialisierung des Systemdatenträgers kann einige Zeit in Anspruch nehmen. Der Zeitaufwand ist von der Datenmenge im Systemdatenträger, der Verfügbarkeit anderer Domänencontroller, und dem Replikationsintervall zwischen anderen Domänencontrollern abhängig.                                                                         |
|  **13501**   |   NtFrs    |                                                                                                                                                                                                                                                                                                                                                                                                   Der Dateireplikationsdienst wird gestartet.                                                                                                                                                                                                                                                                                                                                                                                                   |
|  **13553**   |   NtFrs    |                                                                                                                                                                          Der Dateireplikationsdienst hat diesen Computer dem folgenden Replikatsatz hinzugefügt:<br /><br />"DOMAIN SYSTEM VOLUME (SYSVOL SHARE)"<br /><br />Informationen zu diesem Ereignis sind unten angezeigt:<br /><br />Der DNS-Name des Computers ist *<Domain Controller FQDN>* .<br /><br />Mitgliedsname des Replikat Satzes ist *<Domain Controller>*<br /><br />Stammpfad des Replikat Satzes ist *<path>*<br /><br />Der replikatstagingverzeichnispfad ist *<path>*<br /><br />Der Pfad des Replikat Arbeitsverzeichnisses ist *<path>*                                                                                                                                                                           |
|  **13520**   |   NtFrs    |                Der Datei Replikations Dienst hat die bereits vorhandenen Dateien in <path>auf *<path>* verschoben \NtFrs_PreExisting___See_EventLog.<br /><br />Der Datei Replikations Dienst kann die Dateien in *<path>-* \NtFrs_PreExisting___See_EventLog jederzeit löschen. Dateien können vor dem Löschen gespeichert werden, indem Sie aus *<path>* kopiert werden \NtFrs_PreExisting___See_EventLog. Das Kopieren der Dateien nach c:\windows\sysvol\domain kann zu Namenskonflikten führen, wenn die Dateien auf einem anderen replizierenden Computer bereits vorhanden sind.<br /><br />In einigen Fällen kopiert der Datei Replikations Dienst eine Datei von *<path>-* \NtFrs_PreExisting___See_EventLog in *<path>* , anstatt die Datei von einem anderen replizierenden Partner zu replizieren.<br /><br />Der Speicherplatz kann jederzeit wieder hergestellt werden, indem die Dateien in *<path>-* \NtFrs_PreExisting___See_EventLog.) gelöscht werden.                 |
|  **13508**   |   NtFrs    | der Datei Replikations Dienst hat Probleme beim Aktivieren der Replikation von *\\ @ no__t-2 @ no__t-3* zu *<Domain Controller>* für *<path>* . verwenden Sie dazu das<br /><br />DNS-Name *\\ @ no__t-2 @ no__t-3*. Es wird ein neuer Versuch gestartet.<br /><br />Mögliche Ursachen für diese Warnung sind:<br /><br />[1] der DNS *-Name \\ @ no__t-2 @ no__t-3* kann von diesem Computer nicht ordnungsgemäß aufgelöst werden.<br /><br />[2] der FRS wird nicht auf *\\ @ no__t-2 @ no__t-3*ausgeführt.<br /><br />[3] Die Topologieinformationen im Active Directory dieses Replikats wurden noch nicht auf allen Domänencontrollern repliziert.<br /><br />Diese Ereignisprotokollmeldung wird einmal pro Verbindung angezeigt. Nachdem der Fehler behoben wurde, wird eine andere Ereignisprotokollmeldung angezeigt, die bestätigt, dass die Verbindung hergestellt wurde. |
|  **13509**   |   NtFrs    |                                                                                                                                                                                                                                                                                                                                            Der Datei Replikations Dienst hat die Replikation von *\\ @ no__t-2 @ no__t-3* nach wiederholten Wiederholungen in *<Domain Controller>* für *<Path>* aktiviert.                                                                                                                                                                                                                                                                                                                                             |
|  **13516**   |   NtFrs    |                                                                                                                                                                                                                                               Der Datei Replikations Dienst verhindert nicht mehr, dass der Computer *<Domain Controller>* zu einem Domänen Controller wird. Der Systemdatenträger wurde erfolgreich initialisiert. Der Netzwerkanmeldedienst wurde benachrichtigt, dass der Systemdatenträger jetzt als SYSVOL freigegeben werden kann.<br /><br />Geben Sie "net share" ein, um die SYSVOL-Freigabe zu überprüfen."                                                                                                                                                                                                                                               |

##### <a name="dfs-replication-event-log"></a>Ereignisprotokoll der DFS-Replikation  
Die DFSR-Dienste synchronisieren während des Klonvorgangs nicht autoritativ von einem Partner. Der Klonvorgang erreicht dies durch Löschen der DFSR-Datenbankdateien und unveränderten Inhalten von SYSVOL zur Verwendung als zuvor per Seeding hinzugefügte Daten. Die zwei Synchronisierungsversuche sind erwartet.  


|              |            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** | **Quelle** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           **Nachricht**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   **1004**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst wurde gestartet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **1314**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  Der DFS-Replikationsdienst hat die Debugprotokolldateien erfolgreich konfiguriert.<br /><br />Zusätzliche Informationen:<br /><br />Pfad der Debugprotokolldatei: C:\Windows\debug                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|   **6102**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst hat den WMI-Anbieter erfolgreich registriert.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **1206**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Der DFS-Replikationsdienst hat die Verbindung zum Domänencontroller DC2.corp.contoso.com zum Zugriff auf Konfigurationsinformationen erfolgreich hergestellt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|   **1210**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    Der DFS-Replikationsdienst hat erfolgreich einen RPC-Listener für eingehende Replikationsanforderungen eingerichtet.<br /><br />Zusätzliche Informationen:<br /><br />Port: 0"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|   **4614**   |    DFSR    | Der DFS-Replikationsdienst hat SYSVOL im lokalen Pfad C:\Windows\SYSVOL\domain initialisiert und wartet darauf, die erste Replikation auszuführen. Der replizierte Ordner bleibt im ersten Synchronisierungsstatus, bis er mit seinem Partner repliziert wurde. Wenn der Server zu einem Domänencontroller heraufgestuft wurde, führt der Domänencontroller keine Ankündigung durch und dient als Domänencontroller, bis dieses Problem behoben wurde. Dies kann darauf zurückzuführen sein, dass der angegebene Partner sich selbst in einem ersten Synchronisierungsstatus befindet. Eine weitere mögliche Ursache ist, dass auf diesem Server oder beim Synchronisierungspartner Zugriffsverletzungen aufgetreten sind. Wenn dieses Ereignis bei der Migration von SYSVOL aus dem Dateireplikationsdienst (FRS) zur DFS-Replikation aufgetreten ist, werden die Änderungen nicht nach außen repliziert, bis dieses Problem behoben wurde. Dies kann dazu führen, dass der SYSVOL-Ordner auf diesem Server nicht mehr mit anderen Domänencontrollern synchron ist.<br /><br />Zusätzliche Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners: *<GUID>*<br /><br />Replikationsgruppenname: Domain System Volume<br /><br />Replikations Gruppen-ID: *<GUID>*<br /><br />Mitglieds-ID: *<GUID>*<br /><br />Schreibgeschützt: 0 |
|   **4604**   |    DFSR    |                                                                                                                                                                                                                                                                      Der DFS-Replikationsdienst hat den SYSVOL-replizierten Ordner im lokalen PfadC:\Windows\SYSVOL\domain erfolgreich initialisiert. Dieses Mitglied hat die erste Synchronisierung von SYSVOL mit Partner  dc1.corp.contoso.com abgeschlossen.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie dann "net share" ein, um das Vorhandensein der SYSVOL-Freigabe zu prüfen.<br /><br />Zusätzliche Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners: *<GUID>*<br /><br />Replikationsgruppenname: Domain System Volume<br /><br />Replikations Gruppen-ID: *<GUID>*<br /><br />Mitglieds-ID: *<GUID>*<br /><br />Synchronisierungs Partner: *<domain controller FQDN>*                                                                                                                                                                                                                                                                       |

## <a name="BKMK_TshootVDCSafeRestore"></a>Problembehandlung bei der sicheren Wiederherstellung virtualisierter Domänen Controller  

### <a name="tools-for-troubleshooting"></a>Tools zur Problembehandlung  

#### <a name="logging-options"></a>Protokollierungsoptionen  
Die integrierten Protokolle sind das wichtigste Tool für die Problembehandlung bei der sicheren Momentaufnahmenwiederherstellung von Domänencontrollern. Alle Protokolle sind standardmäßig für maximale Ausführlichkeit aktiviert und konfiguriert.  

|||  
|-|-|  
|**Vorgang**|**Angezeigt**|  
|**Momentaufnahme Erstellung**|-Ereignisviewer\anwendungs-und dienstprotokolle\microsoft\windows\hyper-v-Worker|  
|**Momentaufnahme Wiederherstellung**|-Ereignisviewer\anwendungs-und dienstprotokolle\verzeichnisdienst<br />-Ereignisviewer\windows-Protokolle\System<br />-Ereignisviewer\windows-Protokolle\Anwendung<br />-Ereignisviewer\anwendungs-und dienstprotokolle\datei Replikations Dienst<br />-Ereignisviewer\anwendungs-und dienstprotokolle\dfs-Replikation<br />-Ereignisviewer\anwendungs-und dienstprotokolle\dns<br />-Ereignisviewer\anwendungs-und dienstprotokolle\microsoft\windows\hyper-v-Worker|  

#### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>Tools und Befehle für die Problembehandlung bei der Domänencontroller-Konfiguration  
Die folgenden Tools dienen als Ausgangspunkt bei der Behandlung von Problemen, die nicht durch Protokolle erklärt werden können:  

-   Dcdiag.exe  

-   Repadmin.exe  

-   Netzwerkmonitor 3.4  

#### <a name="BKMK_TshhotSafeRestore"></a>Allgemeine Methodik zur Problembehandlung der sicheren Wiederherstellung von Domänen  

1.  Ist die sichere Momentaufnahmenwiederherstellung erwartet, hat aber Probleme?  

    1.  Untersuchen Sie das Verzeichnisdienst-Ereignisprotokoll.  

        1.  Treten bei der Momentaufnahmenwiederherstellung Fehler auf?  

        2.  Treten bei der AD-Replikation Fehler auf?  

    2.  Untersuchen Sie das Systemereignisprotokoll.  

        1.  Gibt es Kommunikationsfehler?  

        2.  Gibt es AD-Fehler?  

2.  Ist die sichere Momentaufnahmenwiederherstellung unerwartet?  

    1.  Untersuchen Sie Überwachungsprotokolle des Hypervisors, um herauszufinden, von wem und wodurch ein Rollback verursacht wurde.  

    2.  Kontaktieren Sie alle Administratoren des Hypervisors, und befragen Sie sie, wer ein Rollback des virtuellen Computers ohne Benachrichtigung durchgeführt hat.  

3.  Implementiert der Server einen USN-Rollbackschutz und wird nicht sicher wiederhergestellt?  

    1.  Untersuchen Sie die Verzeichnisdienst-Ereignisprotokolle auf einen nicht unterstützten Hypervisor oder nicht unterstützte Integrationsdienste.  

    2.  Untersuchen Sie das Betriebssystem und überprüfen Sie die Ausführung von Windows Server 2012.  

### <a name="BKMK_TshootSpecificSafeRestore"></a>Problembehandlung bei bestimmten Problemen  

#### <a name="events"></a>Ereignisse  
Alle Ereignisse bei der sicheren Momentaufnahmenwiederherstellung eines virtualisierten Domänencontroller werden in das Verzeichnisdienst-Ereignisprotokoll des wiederhergestellten virtuellen Domänencontrollercomputers geschrieben. Das Anwendungs-, Dateireplikationsdienst- und DFS-Replikationsereignisprotokoll enthält möglicherweise auch nützliche Problembehandlungsinformationen für fehlgeschlagene Wiederherstellungsvorgänge.  

Im Folgenden sind die für die sichere Wiederherstellung in Windows Server 2012 spezifischen Ereignisse im Verzeichnisdienst-Ereignisprotokoll aufgeführt.  


|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                              **2170**                                                                                                                                                                                                                                                                                                                                                              |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                          Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                           |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                              Warnung                                                                                                                                                                                                                                                                                                                                                               |
|       **Nachricht**        | Es wurde keine Änderung der Generations-ID erkannt.<br /><br />Zwischengespeicherte Generations-ID (DS, alter Wert):%1<br /><br />Aktuelle Generations-ID des virtuellen Computers (neuer Wert):%2<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. *<COMPUTERNAME>* erstellt eine neue Aufruf-ID, um den Domänen Controller wiederherzustellen. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                            Dies ist ein Erfolgsereignis, wenn die Momentaufnahme erwartet war. Falls nicht, untersuchen Sie das Hyper-V-Worker-Ereignisprotokoll, oder wenden Sie sich an den Hypervisoradministrator.                                                                                                                                                                                                                                                                                             |

|||  
|-|-|  
|**Ereignis-ID**|**2174**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Der Domänencontroller ist weder ein Klon noch eine wiederhergestellte Momentaufnahme eines virtuellen Domänencontrollers.|  
|**Hinweise und Lösung**|Erwartetes Ereignis beim Starten von physischen Domänencontrollern oder virtualisierten Domänencontrollern, die nicht von einer Momentaufnahme wiederhergestellt wurden|  

|||  
|-|-|  
|**Ereignis-ID**|**2181**|  
|**Quelle**|Microsoft-Windows-ActiveDirectory_DomainService|  
|**Zunehmen**|Informationen|  
|**Nachricht**|Die Transaktion wurde aufgrund der Wiederherstellung des virtuellen Computers in einen früheren Zustand abgebrochen.  Dies erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration.|  
|**Hinweise und Lösung**|Beim Wiederherstellen einer Momentaufnahme erwartet. Transaktionen verfolgen die Änderung der VM-Generations-ID.|  

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                                                **2185**                                                                                                                                                                                                                                                                                                                                                                                 |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                                             Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                                             |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                                              Informationen                                                                                                                                                                                                                                                                                                                                                                              |
|       **Nachricht**        |                                                                                      *<COMPUTERNAME>* hat den FRS-oder DFSR-Dienst zum Replizieren des Ordners "SYSVOL" beendet.<br /><br />Dienstname:%1<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisieren. Zu diesem Zweck wird der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. Beim Neustart des Diensts wird das Ereignis 2187 protokolliert.                                                                                       |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                                                           Beim Wiederherstellen einer Momentaufnahme erwartet. Alle SYSVOL-Daten auf diesem Domänencontroller werden mit der Kopie eines Partnerdomänencontrollers ersetzt.                                                                                                                                                                                                                                                                                                                           |
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                                                  2186                                                                                                                                                                                                                                                                                                                                                                                   |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                                             Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                                             |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                                                  Fehler                                                                                                                                                                                                                                                                                                                                                                                  |
|       **Nachricht**        | *<COMPUTERNAME>* konnte den FRS-oder DFSR-Dienst zum Replizieren des Ordners "SYSVOL" nicht abbrechen.<br /><br />Dienstname:%1<br /><br />Fehlercode: %2<br /><br />Fehlermeldung: %3<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisieren. Zu diesem Zweck wird der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und dann mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. *<COMPUTERNAME>* konnte den aktuell ausgefallenen Dienst nicht beenden, und die nicht autoritative Wiederherstellung kann nicht ausgeführt werden. Führen Sie manuell eine nicht autoritative Wiederherstellung aus. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                                                                                  Untersuchen Sie die System-, FRS- und DFSR-Ereignisprotokolle auf weitere Informationen.                                                                                                                                                                                                                                                                                                                                                   |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                           **2187**                                                                                                                                                                                                                                                           |
|        **Quelle**        |                                                                                                                                                                                                                                       Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                        |
|       **Zunehmen**       |                                                                                                                                                                                                                                                        Informationen                                                                                                                                                                                                                                                         |
|       **Nachricht**        | *<COMPUTERNAME>* hat den FRS-oder DFSR-Dienst gestartet, mit dem der SYSVOL-Ordner repliziert wird.<br /><br />Dienstname:%1<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* ist erforderlich, um eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat zu initialisieren. Zu diesem Zweck wurde der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. |
| **Hinweise und Lösung** |                                                                                                                                                                                                     Beim Wiederherstellen einer Momentaufnahme erwartet. Alle SYSVOL-Daten auf diesem Domänencontroller werden mit der Kopie eines Partnerdomänencontrollers ersetzt.                                                                                                                                                                                                      |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                                                                 **2188**                                                                                                                                                                                                                                                                                                                                                                                                  |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                                                              Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                                                              |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                                                                   Fehler                                                                                                                                                                                                                                                                                                                                                                                                   |
|       **Nachricht**        | *<COMPUTERNAME>* konnte den FRS-oder DFSR-Dienst nicht starten, der zum Replizieren des SYSVOL-Ordners verwendet wird.<br /><br />Dienstname:%1<br /><br />Fehlercode: %2<br /><br />Fehlermeldung: %3<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisieren. Zu diesem Zweck wird der FRS oder der DFS-Replikationsdienst zum Replizieren von SYSVOL beendet und mit geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. *<COMPUTERNAME>* konnte den FRS-oder DFSR-Dienst zum Replizieren des Ordners "SYSVOL" nicht starten und kann die nicht autoritative Wiederherstellung nicht durchführen. Führen Sie manuell eine nicht autoritative Wiederherstellung aus, und starten Sie den Dienst neu. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                                                                                                   Untersuchen Sie die System-, FRS- und DFSR-Ereignisprotokolle auf weitere Informationen.                                                                                                                                                                                                                                                                                                                                                                    |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                         **2189**                                                                                                                                                                                                                                                                                                          |
|        **Quelle**        |                                                                                                                                                                                                                                                                                      Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                      |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                       Informationen                                                                                                                                                                                                                                                                                                       |
|       **Nachricht**        | *<COMPUTERNAME>* legen Sie die folgenden Registrierungs Werte zum Initialisieren des SYSVOL-Replikats während einer nicht autorisierenden Wiederherstellung fest:<br /><br />Registrierungswert:%1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisieren. Zu diesem Zweck wird der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                    Beim Wiederherstellen einer Momentaufnahme erwartet. Alle SYSVOL-Daten auf diesem Domänencontroller werden mit der Kopie eines Partnerdomänencontrollers ersetzt.                                                                                                                                                                                                                                                    |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                                                                                              **2190**                                                                                                                                                                                                                                                                                                                                                                                                                              |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                                                                                          Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                                                                                           |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                                                                                               Fehler                                                                                                                                                                                                                                                                                                                                                                                                                                |
|       **Nachricht**        | *<COMPUTERNAME>* konnte die folgenden Registrierungs Werte nicht festlegen, um das SYSVOL-Replikat während einer nicht autorisierenden Wiederherstellung zu initialisieren:<br /><br />Registrierungswert:%1<br /><br />Registrierungswert: %2<br /><br />Registrierungswertdaten: %3<br /><br />Fehlercode: %4<br /><br />Fehlermeldungen: %5<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der die Domänencontrollerrolle hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisieren. Zu diesem Zweck wird der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. Fehler beim Festlegen der oben aufgeführten Registrierungs Werte durch *<COMPUTERNAME>* . die nicht autoritative Wiederherstellung kann nicht durchgeführt werden. Führen Sie manuell eine nicht autoritative Wiederherstellung aus. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                                                                                                       Untersuchen Sie die Anwendungs- und Systemereignisprotokolle. Überprüfen Sie Drittanbieteranwendungen, die möglicherweise Registrierungsaktualisierungen blockieren.                                                                                                                                                                                                                                                                                                                                                                       |

|                          |                                                                                                                                                                                                                                                                    |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                              **2200**                                                                                                                              |
|        **Quelle**        |                                                                                                          Microsoft-Windows-ActiveDirectory_DomainService                                                                                                           |
|       **Zunehmen**       |                                                                                                                           Informationen                                                                                                                            |
|       **Nachricht**        | Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* initialisiert die Replikation, um den Domänen Controller aktuell zu machen. Nach Abschluss der Replikation wird das Ereignis 2201 protokolliert. |
| **Hinweise und Lösung** |                                                                                         Beim Wiederherstellen einer Momentaufnahme erwartet. Kennzeichnet den Beginn einer eingehenden Replikation.                                                                                         |

|                          |                                                                                                                                                                                                         |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                **2201**                                                                                                 |
|        **Quelle**        |                                                                             Microsoft-Windows-ActiveDirectory_DomainService                                                                             |
|       **Zunehmen**       |                                                                                              Informationen                                                                                              |
|       **Nachricht**        | Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* hat die Replikation beendet, um den Domänen Controller aktuell zu machen. |
| **Hinweise und Lösung** |                                                              Beim Wiederherstellen einer Momentaufnahme erwartet. Kennzeichnet das Ende einer eingehenden Replikation.                                                               |

|                          |                                                                                                                                                                                                                                                                             |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                  **2202**                                                                                                                                   |
|        **Quelle**        |                                                                                                               Microsoft-Windows-ActiveDirectory_DomainService                                                                                                               |
|       **Zunehmen**       |                                                                                                                                    Fehler                                                                                                                                    |
|       **Nachricht**        | Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* konnte die Replikation nicht durchführen, um den Domänen Controller auf den neuesten Stand zu bringen. Er wird nach der nächsten periodischen Replikation aktualisiert. |
| **Hinweise und Lösung** |                                                                        Untersuchen Sie das Verzeichnisdienst- und das Systemereignisprotokoll. Verwenden Sie repadmin.exe, um eine Replikation zu erzwingen, und notieren Sie alle Fehler.                                                                         |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                                                                                                                                                                   **2204**                                                                                                                                                                                                                                                                                                                                                                                                                    |
|        **Quelle**        |                                                                                                                                                                                                                                                                                                                                                                                                Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                                                                                                                                                                |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                                                                                                                                                                 Informationen                                                                                                                                                                                                                                                                                                                                                                                                                 |
|       **Nachricht**        | *<COMPUTERNAME>* hat eine Änderung der Generations-ID der virtuellen Maschine erkannt. Die Änderung bedeutet, dass der virtuelle Domänencontroller in einem früheren Zustand wiederhergestellt wurde. *<COMPUTERNAME>* führt die folgenden Vorgänge aus, um den wiederhergestellten Domänen Controller vor möglichen Daten Abweichungen zu schützen und die Erstellung von Sicherheits Prinzipalen mit doppelten SIDs zu schützen:<br /><br />Es wird eine neue Aufruf-ID erstellt.<br /><br />Der aktuelle RID-Pool wird ungültig gemacht.<br /><br />Bei der nächsten eingehenden Replikation erfolgt eine Überprüfung hinsichtlich des Besitzers der FSMO-Rollen. Wenn der Domänencontroller Besitzer einer FSMO-Rolle ist, ist diese Rolle bis zum Abschluss der Replikation nicht verfügbar.<br /><br />Der SYSVOL-Replikationsdienst wird wiederhergestellt.<br /><br />Die Replikation wird gestartet, um den wiederhergestellten Domänencontroller auf den aktuellen Stand zu bringen.<br /><br />Es wird ein neuer RID-Pool angefordert. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                                                                                                                    Beim Wiederherstellen einer Momentaufnahme erwartet. Das erklärt die verschiedenen Vorgänge zum Zurücksetzen, die als Teil des sicheren Wiederherstellungsvorgangs vorkommen.                                                                                                                                                                                                                                                                                                                                                    |

|                          |                                                                                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                          **2205**                                                                           |
|        **Quelle**        |                                                       Microsoft-Windows-ActiveDirectory_DomainService                                                       |
|       **Zunehmen**       |                                                                        Informationen                                                                        |
|       **Nachricht**        |                        *@no__t -1* den aktuellen RID-Pool ungültig, nachdem der virtuelle Domänen Controller in den vorherigen Zustand zurückversetzt wurde.                        |
| **Hinweise und Lösung** | Beim Wiederherstellen einer Momentaufnahme erwartet. Der lokale RID-Pool muss zerstört werden, da der Domänencontroller eine Zeitreise gemacht hat und der Pool möglicherweise bereits ausgestellt wurde. |

|                          |                                                                                                                                                                                                         |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                **2206**                                                                                                 |
|        **Quelle**        |                                                                             Microsoft-Windows-ActiveDirectory_DomainService                                                                             |
|       **Zunehmen**       |                                                                                                  Fehler                                                                                                  |
|       **Nachricht**        | *<COMPUTERNAME>* konnte den aktuellen RID-Pool nicht für ungültig erklären, nachdem der virtuelle Domänen Controller in den vorherigen Zustand zurückversetzt wurde.<br /><br />Weitere Daten:<br /><br />Fehlercode: %1<br /><br />Fehlerwert: %2 |
| **Hinweise und Lösung** |                     Untersuchen Sie das Verzeichnisdienst- und das Systemereignisprotokoll. Vergewissern Sie sich über Dcdiag.exe /test:ridmanager, dass der RID-Master online ist und von diesem Server erreicht werden kann.                      |

|                          |                                                                                                                                                                                         |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                        **2207**                                                                                         |
|        **Quelle**        |                                                                     Microsoft-Windows-ActiveDirectory_DomainService                                                                     |
|       **Zunehmen**       |                                                                                          Fehler                                                                                          |
|       **Nachricht**        | *<COMPUTERNAME>* konnte nicht wieder hergestellt werden, nachdem der virtuelle Domänen Controller in den vorherigen Zustand zurückversetzt wurde. Es war ein Neustart im Verzeichnisdienst-Wiederherstellungsmodus (DSRM) erforderlich. Weitere Informationen finden Sie in den vorhergehenden Ereignissen. |
| **Hinweise und Lösung** |                                                                  Untersuchen Sie das Verzeichnisdienst- und das Systemereignisprotokoll.                                                                  |

|                          |                                                                                                                                                                                                                                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                            **2208**                                                                                                                                                             |
|        **Quelle**        |                                                                                                                                         Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                         |
|       **Zunehmen**       |                                                                                                                                                          Informationen                                                                                                                                                          |
|       **Nachricht**        |                                                                                                            *<COMPUTERNAME>* löschte DFSR-Datenbanken zum Initialisieren des SYSVOL-Replikats während einer nicht autorisierenden Wiederherstellung.                                                                                                             |
| **Hinweise und Lösung** | Beim Wiederherstellen einer Momentaufnahme erwartet. Damit wird garantiert, dass DFSR SYSVOL nicht autoritativ von einem Partnerdomänencontroller synchronisiert. Beachten Sie, dass alle anderen von DFSR replizierten Ordner auf demselben Volume wie SYSVOL ebenfalls nicht autoritativ synchronisiert werden (es wird nicht empfohlen, dass Domänencontroller benutzerdefinierte DFSR-Sätze auf demselben Volume wie SYSVOL hosten). |

|                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       **Ereignis-ID**       |                                                                                                                                                                                                                                                                         **2209**                                                                                                                                                                                                                                                                         |
|        **Quelle**        |                                                                                                                                                                                                                                                     Microsoft-Windows-ActiveDirectory_DomainService                                                                                                                                                                                                                                                      |
|       **Zunehmen**       |                                                                                                                                                                                                                                                                          Fehler                                                                                                                                                                                                                                                                           |
|       **Nachricht**        | Fehler beim Löschen von DFSR-Datenbanken durch *<COMPUTERNAME>* .<br /><br />Weitere Daten:<br /><br />Fehlercode: %1<br /><br />Fehlerwert: %2<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. *<COMPUTERNAME>* muss eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisieren. Für DFSR wird dies ausgeführt, indem der DFSR-Dienst beendet wird, die DFSR-Datenbanken gelöscht werden und der Dienst neu gestartet wird. Beim Neustart wird von DSFR so vorgegangen, dass die Datenbanken wiederhergestellt werden und die Erstsynchronisierung gestartet wird. |
| **Hinweise und Lösung** |                                                                                                                                                                                                                                                               Untersuchen Sie das DFSR-Ereignisprotokoll.                                                                                                                                                                                                                                                                |

#### <a name="error-messages"></a>Fehlermeldungen  
Es gibt keine direkten interaktiven Fehler für eine fehlgeschlagene sichere Momentaufnahmenwiederherstellung eines virtualisierten Domänencontrollers. Alle Kloninformationen werden im den Verzeichnisdienst-Ereignisprotokollen protokolliert. Natürlich manifestieren sich alle kritischen Replikations- oder Serverankündigungsfehler als Symptome an anderer Stelle.  

#### <a name="known-issues-and-support-scenarios"></a>Bekannte Probleme und Supportszenarien  
Die [allgemeine Methode für die Problembehandlung der sicheren Wiederherstellung von Domänen Controllern](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootSpecificSafeRestore) ist in der Regel für die Behandlung der meisten  

|||  
|-|-|  
|**Problem:**|**Auf dem kürzlich sicheren wiederhergestellten Domänen Controller können keine neuen Sicherheits Prinzipale erstellt werden.**|  
|**On**|Nach der Wiederherstellung einer Momentaufnahme schlagen Versuche, einen neuen Sicherheitsprinzipal (Benutzer, Computer, Gruppe) auf diesem Computer zu erstellen, mit dem folgenden Fehler fehl:<br /><br />Fehler 0x2010<br /><br />Der Verzeichnisdienst kann keinen relativen Bezeichner zuweisen.|  
|**Lösung und Hinweise**|Dieses Problem wird durch die veraltete Kenntnis der FSMO-Rolle des RID-Masters auf dem wiederhergestellten Computer verursacht. Wenn die Rolle nach der Erstellung und späteren Wiederherstellung einer Momentaufnahme an diesen oder einen anderen Domänencontroller verschoben wurde, hat der wiederhergestellte Domänencontroller keine Kenntnis des RID-Masters, bis die Erstreplikation abgeschlossen ist.<br /><br />Lassen Sie zum Beheben dieses Problems zu, dass die AD-Replikation an den wiederhergestellten Domänencontroller eingehend abgeschlossen wird. Falls das Problem bestehen bleibt, vergewissern Sie sich, dass alle Domänencontroller die korrekte Kenntnis darüber haben, auf dem Domänencontroller der RID-Master gehostet ist.|  

|||  
|-|-|  
|**Problem:**|**Wiederhergestellte Domänen Controller geben SYSVOL nicht frei, Ankündigung**|  
|**On**|Nach der Wiederherstellung einer Momentaufnahme kündigt mindestens ein Domänencontroller nicht an, SYSVOL ist nicht freigegeben, und er verfügt nicht über aktuelle SYSVOL-Inhalte.|  
|**Lösung und Hinweise**|Auf den Upstreampartnern des Domänencontrollers ist kein funktionierendes SYSVOL-Replikat vorhanden, das ordnungsgemäß mit DFSR oder FRS repliziert. Dieses Problem steht nicht im Zusammenhang mit der sicheren Wiederherstellung, manifestiert sich aber wahrscheinlich als ein solches, da dem Kunden nicht bewusst war, dass das andere Replikationsproblem nicht wiederhergestellte Domänencontroller betrifft.|  

### <a name="advanced-troubleshooting"></a>Erweiterte Fehlerbehandlung  
In diesem Modul erfahren Sie mehr über die erweiterte Fehlerbehandlung, indem *funktionierende* Protokolle als Beispiele verwendet und Erläuterungen zu den Ereignissen bereitgestellt werden. Wenn Sie verstehen, wie ein erfolgreicher Vorgang auf einem virtualisierten Quelldomänencontroller aussieht, werden Fehler in Ihrer Umgebung offensichtlich. Diese Protokolle werden nach ihrer Quelle dargestellt, aufsteigend in der Reihenfolge *erwarteter* Ereignisse in jedem Protokoll, die mit einem geklonten Domänencontroller zusammenhängen.  

#### <a name="restoring-a-domain-controller-that-replicates-sysvol-using-dfsr"></a>Wiederherstellen eines Domänencontrollers, der SYSVOL über DFSR repliziert  

##### <a name="directory-services-event-log"></a>Verzeichnisdienst-Ereignisprotokoll  
Das Verzeichnisdienst-Ereignisprotokoll enthält den größten Teil der Betriebsinformationen für die sichere Wiederherstellung. Der Hypervisor ändert die VM-Generations-ID. Der NTDS-Dienst bemerkt dies, macht den RID-Pool ungültig und ändert die Aufrufkennung. Die neue VM-Generations-ID wird festgelegt, und der Server repliziert AD-Daten eingehend. Der DFSR-Dienst wird angehalten, und seine Datenbank, die SYSVOL hostet, wird gelöscht, wodurch eine nicht autoritative eingehende Synchronisierung erzwungen wird. Der hohe USN-Grenzwert wird angepasst.  


|              |                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** |          **Quelle**           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           **Nachricht**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   **2170**   | ActiveDirectory_DomainService |                                                                                                                                                                   Es wurde keine Änderung der Generations-ID erkannt.<br /><br />Zwischengespeicherte Generations-ID in DS (alter Wert):<br /><br />*<number>*<br /><br />Aktuelle Generations-ID des virtuellen Computers (neuer Wert):<br /><br />*<number>*<br /><br />Die Änderung der Generations-ID erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Von den Active Directory-Domänendiensten wird eine neue Aufruf-ID zur Wiederherstellung des Domänencontrollers erstellt. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde.                                                                                                                                                                   |
|   **2181**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                           Die Transaktion wurde aufgrund der Wiederherstellung des virtuellen Computers in einen früheren Zustand abgebrochen.  Dies erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   **2204**   | ActiveDirectory_DomainService |                                                                                                                          Von den Active Directory-Domänendiensten wurde eine Änderung der Generations-ID der virtuellen Maschine erkannt. Die Änderung bedeutet, dass der virtuelle Domänencontroller in einem früheren Zustand wiederhergestellt wurde. Folgende Vorgänge werden von den Active Directory-Domänendiensten ausgeführt, um den wiederhergestellten Domänencontroller vor möglichen Datenabweichungen zu schützen sowie zu verhindern, dass Sicherheitsprinzipale mit doppelten SIDs erstellt werden:<br /><br />Es wird eine neue Aufruf-ID erstellt.<br /><br />Der aktuelle RID-Pool wird ungültig gemacht.<br /><br />Bei der nächsten eingehenden Replikation erfolgt eine Überprüfung hinsichtlich des Besitzers der FSMO-Rollen. Wenn der Domänencontroller Besitzer einer FSMO-Rolle ist, ist diese Rolle bis zum Abschluss der Replikation nicht verfügbar.<br /><br />Der SYSVOL-Replikationsdienst wird wiederhergestellt.<br /><br />Die Replikation wird gestartet, um den wiederhergestellten Domänencontroller auf den aktuellen Stand zu bringen.<br /><br />Es wird ein neuer RID-Pool angefordert."                                                                                                                          |
|   **2181**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                           Die Transaktion wurde aufgrund der Wiederherstellung des virtuellen Computers in einen früheren Zustand abgebrochen.  Dies erfolgt nach der Anwendung einer Momentaufnahme des virtuellen Computers, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   **1109**   | ActiveDirectory_DomainService |                                                                   Das invocationID-Attribut für diesen Domänencontroller wurde geändert. Die höchste Aktualisierungssequenznummer zum Zeitpunkt der Erstellung der Sicherung lautet wie folgt:<br /><br />InvocationID-Attribut (alter Wert):<br /><br />*<GUID>*<br /><br />InvocationID-Attribut (neuer Wert):<br /><br />*<GUID>*<br /><br />Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Die Aufruf-ID (invocationID-Attribut) wird in den folgenden Situationen geändert: nach Wiederherstellung des Verzeichnisservers von einem Sicherungsmedium, nach Konfiguration des Verzeichnisservers als Host einer beschreibbaren Anwendungsverzeichnispartition, bei fortgesetzter Ausführung des Verzeichnisservers, nachdem eine Momentaufnahme des virtuellen Computers angewendet wurde, nach einem Importvorgang für den virtuellen Computer oder nach einer Livemigration. Virtualisierte Domänencontroller dürfen nicht mit einer Momentaufnahme des virtuellen Computers wiederhergestellt werden. Das unterstützte Verfahren zum Wiederherstellen oder Zurücksetzen des Inhalts einer Datenbank der Active Directory-Domänendienste ist das Wiederherstellen einer Systemstatussicherung, die mit einer für die Active Directory-Domänendienste geeigneten Sicherungsanwendung erstellt wurde.                                                                    |
|   **2179**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          Für das msDS-GenerationId-Attribut des Computerobjekts des Domänencontrollers wurde der folgende Parameter festgelegt:<br /><br />Generations-ID-Attribut:<br /><br />*<number>*                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   **2200**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                       Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. Von den Active Directory-Domänendiensten wird die Replikation initialisiert, um den Domänencontroller auf den neuesten Stand zu bringen. Nach Abschluss der Replikation wird das Ereignis 2201 protokolliert.                                                                                                                                                                                                                                                                                                                                                                                                                        |
|   **2201**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                                                                                                                                                                                     Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. Die Replikation, mit der der Domänencontroller auf den neuesten Stand gebracht wurde, wurde abgeschlossen.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|   **2185**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                           Der Dateireplikationsdienst (FRS) oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" wurde beendet.<br /><br />Dienstname:<br /><br />DFSR<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. Daher muss von den Active Directory-Domänendiensten eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Zu diesem Zweck wird der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. Beim Neustart des Diensts wird das Ereignis 2187 protokolliert."                                                                                                                                                                                                                                           |
|   **2208**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                                Die DFSR-Datenbanken wurden von den Active Directory-Domänendiensten gelöscht, um im Verlauf einer nicht autoritativen Wiederherstellung das SYSVOL-Replikat zu initialisieren.<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. Daher muss von den Active Directory-Domänendiensten eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Für DFSR wird dies ausgeführt, indem der DFSR-Dienst beendet wird, die DFSR-Datenbanken gelöscht werden und der Dienst neu gestartet wird. Beim Neustarten von DFSR werden die Datenbanken neu erstellt und die erste Synchronisierung gestartet. "                                                                                                                                                                                                                                                                                 |
|   **2187**   | ActiveDirectory_DomainService |                                                                                                                                                                                                                                                                          Der Dateireplikationsdienst (FRS) oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" wurde gestartet.<br /><br />Dienstname:<br /><br />DFSR<br /><br />Von Active Directory wurde erkannt, dass der virtuelle Computer, der den Domänencontroller hostet, in einen früheren Zustand zurückversetzt wurde. Daher muss von den Active Directory-Domänendiensten eine nicht autoritative Wiederherstellung für das lokale SYSVOL-Replikat initialisiert werden. Zu diesem Zweck wurde der FRS oder der DFS-Replikationsdienst zum Replizieren des Ordners "SYSVOL" beendet und mit den geeigneten Registrierungsschlüsseln und -werten zum Auslösen der Wiederherstellung neu gestartet. "                                                                                                                                                                                                                                                                           |
|   **1587**   | ActiveDirectory_DomainService | Dieser Verzeichnisdienst wurde wiederhergestellt, oder er wurde als Host für eine Anwendungsverzeichnispartition konfiguriert. Darum hat sich seine Replikationsidentität geändert. Ein Partner hat Replikationsänderungen angefordert und dabei die alte Identität verwendet. Die Anfangssequenznummer wurde angepasst.<br /><br />Der Zielverzeichnisdienst, der der folgenden Objekt-GUID entspricht, hat Änderungen angefordert, die bei einer Aktualisierungssequenznummer beginnen sollen, die vor der Aktualisierungssequenznummer liegen, bei der der lokale Verzeichnisdienst vom Sicherungsmedium wiederhergestellt wurde.<br /><br />Objekt-GUID:<br /><br />*<GUID> (<FQDN of partner domain controller>)*<br /><br />Aktualisierungssequenznummer zur Zeit der Wiederherstellung:<br /><br />*<number>*<br /><br />Als Folge dessen wurde der Aktualitätsvektor des Zielverzeichnisdienstes mit den folgenden Einstellungen konfiguriert.<br /><br />Vorherige Datenbank-GUID:<br /><br />*<GUID>*<br /><br />Vorherige Objekt-Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Vorherige Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Neue Datenbank-GUID:<br /><br />*<GUID>*<br /><br />Neue Objekt-Aktualisierungssequenznummer:<br /><br />*<number>*<br /><br />Neue Eigenschafts-Aktualisierungssequenznummer:<br /><br />*<number>* |

##### <a name="system-event-log"></a>Systemereignisprotokoll  
Im Systemereignisprotokoll ist die Computerzeit vermerkt, zu der ein offline geschalteter virtueller Computer wieder online geschaltet und mit der Hostzeit synchronisiert wird. Der RID-Pool wird ungültig gemacht, und der DFSR- oder FRS-Dienst wird neu gestartet.  


|              |                         |                                                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** |       **Quelle**        |                                                                                                                                                                                                       **Nachricht**                                                                                                                                                                                                       |
|    **1**     |     Kernel-General      |                                                                                                                                   Die Systemzeit hat sich auf *? <now>* geändert. aus *< Momentaufnahme Zeit/Datum >* .<br /><br />Änderungsgrund: Eine Anwendung oder Systemkomponente hat die Zeit geändert.                                                                                                                                   |
|  **16654**   | Verzeichnisdienste-SAM  | Ein Pool aus Kontobezeichnern (RIDs) wurde ungültig gemacht. Dies kann in den folgenden zu erwartenden Fällen auftreten:<br /><br />1. Ein Domänencontroller wurde aus einer Datensicherung wiederhergestellt.<br /><br />2. Ein Domänencontroller auf einem virtuellen Computer wurde aus einer Momentaufnahme wiederhergestellt.<br /><br />3. Ein Administrator hat den Pool manuell ungültig gemacht.<br /><br />Weitere Informationen finden Sie unter <https://go.microsoft.com/fwlink/?LinkId=226247>. |
|   **7036**   | Dienststeuerungs-Manager |                                                                                                                                                                                 Der DFS-Replikationsdienst wurde beendet.                                                                                                                                                                                  |
|   **7036**   | Dienststeuerungs-Manager |                                                                                                                                                                                 Der DFS-Replikationsdienst wird jetzt ausgeführt.                                                                                                                                                                                  |

##### <a name="application-event-log"></a>Anwendungsereignisprotokoll  
Im Anwendungsereignisprotokoll wird das Starten und Beenden der DFSR-Datenbank notiert.  


|              |            |                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** | **Quelle** |                                                                                                                                                                                           **Nachricht**                                                                                                                                                                                            |
|   **103**    |   ESENT    |        Dfsrs (1360) \\ @ no__t-1. \ C: \System Volume information\dfsr\database @ no__t-2_ @ no__t-3 @ no__t-4\dfsr.DB: Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.141, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.016, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.         |
|   **102**    |   ESENT    |                                                                                                                    Dfsrs (532) \\ @ no__t-1. \ C: \System Volume information\dfsr\database @ no__t-2_ @ no__t-3 @ no__t-4\dfsr.DB: Das Datenbankmodul (6.02.8189.0000) startet eine neue Instanz (0).                                                                                                                    |
|   **105**    |   ESENT    |                                      Dfsrs (532) \\ @ no__t-1. \ C: \System Volume information\dfsr\database @ no__t-2_ @ no__t-3 @ no__t-4\dfsr.DB: Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.000.                                      |
|              |            | Dfsrs (532) \\ @ no__t-1. \ C: \System Volume information\dfsr\database @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5\dfsr.DB: Das Datenbankmodul hat eine neue Datenbank erstellt (1, \\ @ no__t-1. \ C: \System Volume information\dfsr\database @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5\dfsr.DB). (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.016, [4] 0.062, [5] 0.000, [6] 0.016, [7] 0.000, [8] 0.000, [9] 0.015, [10] 0.000, [11] 0.000. |

##### <a name="dfs-replication-event-log"></a>Ereignisprotokoll der DFS-Replikation  
Der DFSR-Dienst wird beendet, und die Datenbank, die SYSVOL enthält, wird gelöscht, wodurch eine eingehende nicht autoritative Synchronisierung erzwungen wird.  


|              |            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** | **Quelle** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           **Nachricht**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|   **1006**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst wird beendet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **1008**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst wurde beendet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **1002**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst wird gestartet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **1004**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst wurde gestartet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|   **1314**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  Der DFS-Replikationsdienst hat die Debugprotokolldateien erfolgreich konfiguriert.<br /><br />Zusätzliche Informationen:<br /><br />Pfad der Debugprotokolldatei: C:\Windows\debug                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|   **6102**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Der DFS-Replikationsdienst hat den WMI-Anbieter erfolgreich registriert.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|   **1206**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Der DFS-Replikation Dienst hat erfolgreich eine Verbindung mit dem Domänen Controller *<domain controller FQDN>* hergestellt, um auf Konfigurationsinformationen zuzugreifen                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|   **1210**   |    DFSR    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    Der DFS-Replikationsdienst hat erfolgreich einen RPC-Listener für eingehende Replikationsanforderungen eingerichtet.<br /><br />Zusätzliche Informationen:<br /><br />Port: 0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|   **4614**   |    DFSR    | Der DFS-Replikationsdienst hat SYSVOL im lokalen Pfad C:\Windows\SYSVOL\domain initialisiert und wartet darauf, die erste Replikation auszuführen. Der replizierte Ordner bleibt im ersten Synchronisierungsstatus, bis er mit seinem Partner repliziert wurde. Wenn der Server zu einem Domänencontroller heraufgestuft wurde, führt der Domänencontroller keine Ankündigung durch und dient als Domänencontroller, bis dieses Problem behoben wurde. Dies kann darauf zurückzuführen sein, dass der angegebene Partner sich selbst in einem ersten Synchronisierungsstatus befindet. Eine weitere mögliche Ursache ist, dass auf diesem Server oder beim Synchronisierungspartner Zugriffsverletzungen aufgetreten sind. Wenn dieses Ereignis bei der Migration von SYSVOL aus dem Dateireplikationsdienst (FRS) zur DFS-Replikation aufgetreten ist, werden die Änderungen nicht nach außen repliziert, bis dieses Problem behoben wurde. Dies kann dazu führen, dass der SYSVOL-Ordner auf diesem Server nicht mehr mit anderen Domänencontrollern synchron ist.<br /><br />Zusätzliche Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners: *<GUID>*<br /><br />Replikationsgruppenname: Domain System Volume<br /><br />Replikations Gruppen-ID: *<GUID>*<br /><br />Mitglieds-ID: *<GUID>*<br /><br />Schreibgeschützt: 0 |
|   **4604**   |    DFSR    |                                                                                                                                                                                                                                                                   Der DFS-Replikationsdienst hat den SYSVOL-replizierten Ordner im lokalen PfadC:\Windows\SYSVOL\domain erfolgreich initialisiert. Dieses Mitglied hat die erste Synchronisierung von SYSVOL mit Partner  dc1.corp.contoso.com abgeschlossen.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie dann "net share" ein, um das Vorhandensein der SYSVOL-Freigabe zu prüfen.<br /><br />Zusätzliche Informationen:<br /><br />Name des replizierten Ordners: SYSVOL-Freigabe<br /><br />ID des replizierten Ordners: *<GUID>*<br /><br />Replikationsgruppenname: Domain System Volume<br /><br />Replikations Gruppen-ID: *<GUID>*<br /><br />Mitglieds-ID: *<GUID>*<br /><br />Synchronisierungs Partner: *<partner domain controller FQDN>*                                                                                                                                                                                                                                                                    |

#### <a name="restoring-a-domain-controller-that-replicates-sysvol-using-frs"></a>Wiederherstellen eines Domänencontrollers, der SYSVOL über FRS repliziert  
In diesem Fall wird das Dateireplikations-Ereignisprotokoll anstelle des DFSR-Ereignisprotokolls verwendet. In das Anwendungsereignisprotokoll werden auch verschiedene FRS-relevante Ereignisse geschrieben. Davon abgesehen sind die Meldungen des Verzeichnisdienst- und Systemereignisprotokolls im Allgemeinen dieselben und werden in derselben zuvor beschriebenen Reihenfolge ausgegeben.  

##### <a name="file-replication-service-event-log"></a>Ereignisprotokoll des Dateireplikationsdiensts  
Der FRS-Dienst wird mit einem D2 BURFLAGS-Wert beendet und neu gestartet, um SYSVOL nicht autoritativ zu synchronisieren.  


|              |            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ereignis-ID** | **Quelle** |                                                                                                                                                                                                                                                                                                                                                                                           **Nachricht**                                                                                                                                                                                                                                                                                                                                                                                            |
|  **13502**   |   NTFRS    |                                                                                                                                                                                                                                                                                                                                                                            Der Dateireplikationsdienst wird angehalten.                                                                                                                                                                                                                                                                                                                                                                             |
|  **13503**   |   NTFRS    |                                                                                                                                                                                                                                                                                                                                                                            Der Dateireplikationsdienst wurde angehalten.                                                                                                                                                                                                                                                                                                                                                                             |
|  **13501**   |   NTFRS    |                                                                                                                                                                                                                                                                                                                                                                             Der Dateireplikationsdienst wird gestartet.                                                                                                                                                                                                                                                                                                                                                                             |
|  **13512**   |   NTFRS    |                                                                                                                                                                                                                                                            Der Dateireplikationsdienst hat einen aktivierten Datenträgerschreibungs-Cache in dem Laufwerk mit dem Verzeichnis c:\windows\ntfrs\jet auf dem Computer DC4 ermittelt. Der Dateireplikationsdienst kann eventuell nicht wiederhergestellt werden, wenn die Stromzufuhr des Laufwerks unterbrochen wird und wichtige Updates verloren gehen.                                                                                                                                                                                                                                                            |
|  **13565**   |   NTFRS    |                                                  Der Dateireplikationsdienst initialisiert den Systemdatenträger mit Daten eines anderen Domänencontrollers. Computer DC4 kann nicht zum Domänencontroller benannt werden, bis dieser Prozess beendet ist. Das Systemvolumen wird dann als SYSVOL geteilt.<br /><br />Um die SYSVOL-Freigabe zu überprüfen, geben Sie an der Eingabeaufforderung Folgendes ein:<br /><br />Netzwerkfreigabe<br /><br />Wenn der Dateireplikationsdienst den Initialisierungsprozess beendet, wird die SYSVOL-Freigabe angezeigt.<br /><br />Die Initialisierung des Systemdatenträgers kann einige Zeit in Anspruch nehmen. Der Zeitaufwand ist von der Datenmenge im Systemdatenträger, der Verfügbarkeit anderer Domänencontroller, und dem Replikationsintervall zwischen anderen Domänencontrollern abhängig."                                                  |
|  **13520**   |   NTFRS    | Der Datei Replikations Dienst hat die bereits vorhandenen Dateien in *<path>* auf *<path>* verschoben \NtFrs_PreExisting___See_EventLog.<br /><br />Der Datei Replikations Dienst kann die Dateien in *<path>-* \NtFrs_PreExisting___See_EventLog jederzeit löschen. Dateien können vor dem Löschen gespeichert werden, indem Sie aus *<path>* kopiert werden \NtFrs_PreExisting___See_EventLog. Das Kopieren der Dateien in *<path>* kann zu Namenskonflikten führen, wenn die Dateien auf einem anderen replizierenden Partner bereits vorhanden sind.<br /><br />In einigen Fällen kopiert der Datei Replikations Dienst eine Datei von *<path>-* \NtFrs_PreExisting___See_EventLog in *<path>* , anstatt die Datei von einem anderen replizierenden Partner zu replizieren.<br /><br />Der Speicherplatz kann jederzeit wieder hergestellt werden, indem die Dateien in *<path>-* \NtFrs_PreExisting___See_EventLog. gelöscht werden. |
|  **13553**   |   NTFRS    |                                                                                                                                            Der Dateireplikationsdienst hat diesen Computer dem folgenden Replikatsatz hinzugefügt:<br /><br />"DOMAIN SYSTEM VOLUME (SYSVOL SHARE)"<br /><br />Informationen zu diesem Ereignis sind unten angezeigt:<br /><br />Der DNS-Name des Computers ist " *<domain controller FQDN>* ".<br /><br />Mitgliedsname des Replikat Satzes ist " *<domain controller name>* "<br /><br />Stammpfad des Replikat Satzes ist " *<path>* "<br /><br />Der Pfad des Replikat Stagingverzeichnisses ist " *<path>* "<br /><br />Der Pfad des Replikat Arbeitsverzeichnisses ist " *<path>* ".                                                                                                                                             |
|  **13554**   |   NTFRS    |                                                                                                                                                                                                                     Der Dateireplikationsdienst hat dem Replikatsatz die folgenden Verbindungen hinzugefügt:<br /><br />"DOMAIN SYSTEM VOLUME (SYSVOL SHARE)"<br /><br />Eingehender von " *<partner domain controller FQDN>* "<br /><br />Ausgehend von " *<partner domain controller FQDN>* "<br /><br />Weitere Informationen werden in den folgenden Ereignisprotokollmeldungen angezeigt.                                                                                                                                                                                                                     |
|  **13516**   |   NTFRS    |                                                                                                                                                                                                                                  Der Dateireplikationsdienst verhindert nicht mehr die Heraufstufung des Computers DC4 zum Domänencontroller. Der Systemdatenträger wurde erfolgreich initialisiert. Der Netzwerkanmeldedienst wurde benachrichtigt, dass der Systemdatenträger jetzt als SYSVOL freigegeben werden kann.<br /><br />Geben Sie "net share" ein, um die SYSVOL-Freigabe zu überprüfen.                                                                                                                                                                                                                                  |

##### <a name="application-event-log"></a>Anwendungsereignisprotokoll  
Die FRS-Datenbank wird beendet und startet und wird aufgrund des D2 BURFLAGS-Vorgangs analysiert.  

||||  
|-|-|-|  
|**Ereignis-ID**|**Quelle**|**Nachricht**|  
|**327**|ESENT|ntfrs (1424) Das Datenbankmodul hat eine Datenbank getrennt (1, c:\windows\ntfrs\jet\ntfrs.jdb). (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.015, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.516, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.063, [12] 0.000.<br /><br />Wiederhergestellter Cache: 0|  
|**103**|ESENT|ntfrs (1424) Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, [10] 0.000, [11] 0.016, [12] 0.000, [13] 0.000, [14] 0.047, [15] 0.000.|  
|**102**|ESENT|ntfrs (3000) Das Datenbankmodul (6.02.8189.0000) startet eine neue Instanz (0).|  
|**105**|ESENT|ntfrs (3000) Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.062, [10] 0.000, [11] 0.141.|  
|**103**|ESENT|ntfrs (3000) Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000, [13] 0.015, [14] 0.000, [15] 0.000.|  
|**102**|ESENT|ntfrs (3000) Das Datenbankmodul (6.02.8189.0000) startet eine neue Instanz (0).|  
|**105**|ESENT|ntfrs (3000) Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.078, [10] 0.000, [11] 0.109.|  
|**325**|ESENT|ntfrs (3000) Das Datenbankmodul hat eine neue Datenbank erstellt (1, c:\windows\ntfrs\jet\ntfrs.jdb). (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.016, [4] 0.016, [5] 0.000, [6] 0.015, [7] 0.000, [8] 0.000, [9] 0.078, [10] 0.016, [11] 0.000.|  
|**103**|ESENT|ntfrs (3000) Das Datenbankmodul hat die Instanz (0) beendet.<br /><br />Dirty Shutdown: 0<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.078, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.125, [10] 0.016, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000.|  
|**102**|ESENT|ntfrs (3000) Das Datenbankmodul (6.02.8189.0000) startet eine neue Instanz (0).|  
|**105**|ESENT|ntfrs (3000) Das Datenbankmodul hat eine neue Instanz (0) gestartet. (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.016, [2] 0.000, [3] 0.000, [4] 0.094, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.032, [10] 0.000, [11] 0.000.|  
|**326**|ESENT|ntfrs (3000) Das Datenbankmodul hat eine Datenbank angehängt (1, c:\windows\ntfrs\jet\ntfrs.jdb). (Zeit=0 Sekunden)<br /><br />Interne Zeitsteuerungsabfolge: [1] 0.000, [2] 0.015, [3] 0.000, [4] 0.000, [5] 0.016, [6] 0.015, [7] 0.000, [8] 0.000, [9] 0.000, [10] 0.000, [11] 0.000, [12] 0.000.<br /><br />Gespeicherter Cache: 1|  



