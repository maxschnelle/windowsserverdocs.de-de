---
ms.assetid: 341614c6-72c2-444f-8b92-d2663aab7070
title: Architektur virtualisierter Domänencontroller
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: fa8645198374d91911f8ec7dc15f04bea4865e38
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824443"
---
# <a name="virtualized-domain-controller-architecture"></a>Architektur virtualisierter Domänencontroller

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel behandelt die Architektur für das Klonen und die sichere Wiederherstellung virtualisierter Domänencontroller. Sie finden Flussdiagramme zu den Klon- und Wiederherstellungsprozessen sowie eine detaillierte Erklärung der einzelnen Prozessschritte.  
  
-   [Klonen von virtualisierten Domänen Controllern](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)  
  
-   [Architektur der sicheren Wiederherstellung virtualisierter Domänen Controller](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)  
  
## <a name="virtualized-domain-controller-cloning-architecture"></a><a name="BKMK_CloneArch"></a>Klonen von virtualisierten Domänen Controllern  
  
### <a name="overview"></a>Übersicht  
Das Klonen virtualisierter Domänencontroller benötigt einen von der Hypervisor-Plattform bereitgestellten Bezeichner mit dem Namen **VM-Generations-ID**, mit dem die Erstellung virtueller Computer erkannt wird. AD DS speichert diesen Bezeichner bei der Heraufstufung des Domänencontrollers in der Datenbank (NTDS.DIT). Beim Hochfahren des virtuellen Computers wird der aktuelle Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der Datenbank verglichen. Unterscheiden sich die beiden Werte, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, um das erneute Verwenden der USN oder mögliche doppelt vergebene Sicherheitsprinzipale zu verhindern. Anschließend sucht der Domänencontroller nach der Datei DCCloneConfig.xml an den in Schritt 3 unter [Details zum Klonprozess](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneProcessDetails) beschriebenen Orten. Wenn die Datei DCCloneConfig.xml gefunden wird, geht der DC davon aus, dass er als Klon bereitgestellt wird und initialisiert das Klonen, um sich selbst durch erneute Heraufstufung als zusätzlicher Domänencontroller bereitzustellen. Dabei werden die vom Quellmedium kopierten Inhalte von NTDS.DIT und SYSVOL verwendet.  
  
In gemischten Umgebungen, in denen nicht alle Hypervisoren die VM-Generations-ID unterstützen, kann es passieren, dass ein Klon-Medium versehentlich auf einem Hypervisor bereitgestellt wird, der die VM-Generations-ID nicht unterstützt. Das Vorhandensein der Datei DCCloneConfig.xml gibt die Absicht an, einen DC klonen zu wollen. Wenn also die Datei DCCloneConfig.xml beim Hochfahren gefunden wird, aber keine VM-Generations-ID vom Host angegeben wurde, wird der Klon-DC in den Verzeichnisdienstwiederherstellungs (DSRM)-Modus gestartet, um Auswirkungen auf die restliche Umgebung zu verhindern. Das Klon-Medium kann anschließend auf einen Hypervisor verschoben werden, der die VM-Generations-ID unterstützt, und das Klonen dort wiederholt werden.  
  
Wenn das Klon-Medium auf einem Hypervisor bereitgestellt wird, der die VM-Generations-ID unterstützt, und keine DCCloneConfig.xml-Datei vorhanden ist, löst der DC Schutzmaßnahmen gegen USN-Wiederverwendung und doppelte SIDs aus, wenn er eine Änderung der VM-Generations-ID zwischen seiner eigenen DIT und der neuen DIT aus der VM erkennt. Der Klonvorgang wird jedoch nicht gestartet, sodass der sekundäre Domänencontroller weiterhin unter derselben Identität wie der Quell-DC laufen kann. Der sekundäre DC sollte schnellstmöglich aus dem Netzwerk entfernt werden, um Inkonsistenzen in der Umgebung zu vermeiden. Weitere Informationen dazu, wie Sie diesen sekundären Domänencontroller freigeben und gleichzeitig sicherstellen, dass Updates ausgehend repliziert werden, finden Sie im Microsoft KB-Artikel [2742970](https://support.microsoft.com/kb/2742970).  
  
### <a name="cloning-detailed-processing"></a><a name="BKMK_CloneProcessDetails"></a>Ausführliche Verarbeitung Klonen  
Das folgende Diagramm zeigt die Architektur für den ursprünglichen Klonprozess und für Wiederholungen des Klonprozesses. Diese Prozesse werden im Verlauf dieses Artikels genauer beschrieben.  
  
**Ursprünglicher Klon Vorgang**  
  
![Virtualisierte DC-Architektur](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_InitialCloningProcess.png)  
  
**Klon Vorgang wird wiederholt.**  
  
![Virtualisierte DC-Architektur](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_CloningRetryProcess.png)  
  
In den folgenden Schritten wird der Prozess genauer beschrieben:  
  
1.  Ein existierender virtueller Domänencontroller wird in einem Hypervisor hochgefahren, der die VM-Generations-ID unterstützt.  
  
    1.  Diese VM hat nach der Heraufstufung keine existierende VM-Generations-ID im entsprechenden AD DS-Computerobjekt.  
  
    2.  Selbst wenn die ID null ist, bedeutet die nächste Computererstellung dennoch einen Klonvorgang, da die neue VM-Generations-ID nicht übereinstimmt.  
  
    3.  Die VM-Generations-ID wird nach dem nächsten Neustart des DC gesetzt und wird nicht repliziert.  
  
2.  Anschließend liest der virtuelle Computer die vom VMGenerationCounter-Treiber bereitgestellte VM-Generations-ID aus. Die beiden VM-Generations-IDs werden verglichen.  
  
    1.  Wenn die IDs übereinstimmen, handelt es sich nicht um einen neuen virtuellen Computer, und es wird kein Klonvorgang ausgelöst. Wenn eine DCCloneConfig.xml-Datei existiert, benennt der Domänencontroller die Datei mit einem Zeitstempel um, um das Klonen zu verhindern. Der Startvorgang des Servers wird normal fortgesetzt. Jeder Neustart eines virtuellen Domänencontrollers unter Windows Server 2012 erfolgt auf diese Weise.  
  
    2.  Wenn die beiden IDs nicht übereinstimmen, handelt es sich um einen neuen virtuellen Computer, der eine NTDS.DIT-Datei aus einem vorherigen Domänencontroller enthält (oder es handelt sich um eine wiederhergestellte Momentaufnahme). Wenn eine DCCloneConfig.xml-Datei existiert, fährt der Domänencontroller mit dem Klonprozess fort. Andernfalls wird der Wiederherstellungsprozess der Momentaufnahme fortgesetzt. Weitere Informationen finden Sie unter [Sichere Wiederherstellungsarchitektur für virtualisierte Domänencontroller](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).  
  
    3.  Wenn der Hypervisor keine VM-Generations-ID zum Vergleich bereitstellt, aber eine DCCloneConfig.xml-Datei existiert, benennt der Gast die Datei um und startet im DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen. Wenn keine dccloneconfig.xml-Datei existiert, fährt der Gast normal hoch (mit einem möglichen doppelt vorhandenen Domänencontroller im Netzwerk). Weitere Informationen zum Freigeben dieses doppelt vorhandenen Domänencontrollers finden Sie im Microsoft KB-Artikel [2742970](https://support.microsoft.com/kb/2742970).  
  
3.  Der NTDS-Dienst prüft den Wert des VDCisCloning-DWORDs in der Registrierung (unter HKEY_Local_Machine\System\CurrentControlSet\Services\Ntds\Parameters).  
  
    1.  Wenn dieser Wert nicht existiert, handelt es sich um den ersten Versuch, diesen virtuellen Computer zu klonen. Der Gast implementiert die Sicherheitsmaßnahmen gegen doppelte VDC-Objekte, indem er den lokalen RID-Pool ungültig macht und eine neue Replikations-Aufrufkennung für den Domänencontroller einrichtet  
  
    2.  Wenn diese bereits auf den Wert 0x1 gesetzt ist, handelt es sich um einen Wiederholungsversuch, und der vorherige Klonversuch ist fehlgeschlagen. Die Sicherheitsmaßnahmen gegen doppelte VDC-Objekte werden nicht implementiert, da diese bereits zuvor ausgeführt wurden und der Gast ansonsten unnötigerweise mehrfach verändern würde.  
  
4.  Der IsClone DWORD-Registrierungswert wird nicht geschrieben (unter Hkey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters)  
  
5.  Der NTDS-Dienst ändert die Gast-Boot-Kennzeichnung, um zukünftige Neustarts im DS-Reparaturmodus auszuführen.  
  
6.  Der NTDS-Dienst versucht, die Datei DcCloneConfig.xml an den drei möglichen Orten zu lesen (DSA-Arbeitsverzeichnis, %windir%\NTDS oder les-/schreibbare Wechselmedien in der Reihenfolge der Laufwerkbuchstaben im Stammverzeichnis des Laufwerks).  
  
    1.  Wenn die Datei an keinem der gültigen Orte existiert, prüft der Gast die IP-Adresse auf Duplikate. Wenn die IP-Adresse nicht dupliziert ist, wird der Server normal hochgefahren. Wenn eine duplizierte IP-Adresse existiert, startet der Computer im DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen.  
  
    2.  Wenn die Datei an einem der gültigen Orte existiert, prüft der NTDS-Dienst die enthaltenen Einstellungen. Wenn die Datei leer ist (oder einzelne Einstellungen leer sind), konfiguriert NTDS automatische Werte für diese Einstellungen.  
  
    3.  Wenn die Datei DcCloneConfig.xml existiert, aber ungültige Einträge enthält oder nicht lesbar ist, schlägt der Klonvorgang fehl und der Gast startet in den Verzeichnisdienstwiederherstellungsmodus (DSRM).  
  
7.  Der Gast deaktiviert die automatische DNS-Registrierung, um eine versehentliche Übernahme von Quell-Computername und IP-Adressen zu verhindern.  
  
8.  Der Gast beendet den Anmeldedienst, um Ankündigungen oder Antworten auf AD DS-Anfragen von Clients aus dem Netzwerk zu verhindern.  
  
9. NTDS prüft, ob keine Dienste oder Programme installiert sind, die nicht in DefaultDCCloneAllowList.xml oder CustomDCCloneAllowList.xml enthalten sind  
  
    1.  Falls Dienste oder Programme installiert sind, die nicht in der Standard-Ausschlussliste oder der benutzerdefinierten Ausschlussliste enthalten sind, schlägt der Klonvorgang fehl und der Gast startet in den DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen.  
  
    2.  Falls keine Inkompatibilitäten vorliegen, wird der Klonvorgang fortgesetzt.  
  
10. Wenn automatische IP-Adressierung aufgrund leerer DCCloneConfig.xml-Netzwerkeinstellungen verwendet wird, aktiviert der Gast DHCP auf den Netzwerkkarten, um eine IP-Adresslease, Netzwerkrouting und Namensauflösungsinformationen zu erhalten.  
  
11. Der Gast sucht und kontaktiert den Domänencontroller, der die PDC-Emulator-FSMO-Rolle ausführt. Dazu werden DNS und das DCLocator-Protokoll verwendet. Der Gast stellt eine RPC-Verbindung her und ruft die Methode IDL_DRSAddCloneDC auf, um das Domänencontroller-Computerobjekt zu klonen.  
  
    1.  Wenn das Quell-Computerobjekt des Gasts die erweiterte Domänenkopf-Berechtigung "Zulassen, dass sich ein DC selbst klont" enthält, wird der Klonvorgang fortgesetzt.  
  
    2.  Wenn das Quell-Computerobjekt des Gasts diese erweiterte Berechtigung nicht enthält, schlägt der Klonvorgang fehl und der Gast startet in den DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen.  
  
12. Der Name des AD DS-Computerobjekts wird auf den in DCCloneConfig.xml angegebenen Namen gesetzt, falls vorhanden, oder andernfalls automatisch auf dem PDCE generiert. NTDS erstellt das korrekte NTDS-Einstellungsobjekt für den entsprechenden logischen Active Directory-Ort.  
  
    1.  Wenn es sich um einen PDC-Klonvorgang handelt, benennt der Gast den lokalen Computer um und startet neu. Nach dem Neustart wird Schritt 1-10 erneut durchlaufen und anschließend Schritt 13 fort geleitet.  
  
    2.  Falls es sich um einen Replikat-DC-Klonvorgang handelt, findet zu diesem Zeitpunkt kein Neustart statt.  
  
13. Der Fast stellt die Heraufstufungseinstellungen für den DS-Rollenserverdienst bereit, der die Heraufstufung beginnt.  
  
14. Der DS-Rollenserverdienst beendet alle AD DS-bezogenen Dienst (NTDS, NTFRS/DFSR, KDC, DNS).  
  
15. Der Gast erzwingt eine NT5DS (Windows NTP)-Zeitsynchronisierung mit einem anderen Domänencontroller (in einer normalen Windows-Zeitdiensthierarchie wird dazu der PDCE verwendet). Der Gast kontaktiert den PDCE. Alle existierenden Kerberos-Tickets werden gelöscht.  
  
16. Der Gast konfiguriert die DFSR- oder NTFRS-Dienste für die automatische Ausführung. Der Gast löscht alle vorhandenen DFSR-und NTFRS-Datenbankdateien (Standard: c:\windows\ntfrs und c:\System Volume information\dfsr\\ *< database_GUID >* ), um beim nächsten Start des Diensts eine nicht autoritative Synchronisierung von SYSVOL zu erzwingen. Der Gast löscht die Dateiinhalte von SYSVOL nicht, um Synchronisierung mit Startwerten zu versehen, wenn die Synchronisierung später gestartet wird.  
  
17. Der Gast wird umbenannt. Der DS-Rollenserverdienst auf dem Gast beginnt mit der AD DS-Konfiguration (Heraufstufung) und verwendet dabei die NTDS.DIT-Datenbankdatei als Quelle, anstelle der in c:\windows\system32 enthaltenen Datenbankvorlage, wie bei einer normalen Heraufstufung.  
  
18. Der Gast kontaktiert den Inhaber der RID-Master-FSMO-Rolle, um eine neue RID-Pool-Zuweisung zu erhalten.  
  
19. Der Heraufstufungsprozess erstellt eine neue Aufrufkennung und generiert das NTDS-Einstellungsobjekt für den geklonten Domänencontroller neu (dies ist unabhängig vom Klonvorgang Teil der Domänen-Heraufstufung, wenn eine existierende NTDS.DIT-Datenbank verwendet wird).  
  
20. NTDS wird in Objekten repliziert, die fehlen, neuer sind oder eine höhere Versionsnummer haben, von einem Partner-Domänencontroller. NTDS.DIT enthält bereits Objekte vom Zeitpunkt, zu dem der Quell-Domänencontroller offline genommen wurde. Diese Objekte werden nach Möglichkeit verwendet, um den eingehenden Replikations-Datenverkehr zu minimieren. Die globalen Katalogpartionen werden gefüllt.  
  
21. Der DFSR- oder FRS-Dienst startet. Da keine Datenbank vorhanden ist, wird SYSVOL nicht autoritativ von einem Replikationspartner in eingehender Richtung repliziert. Dieser Prozess verwendet bereits existierende Daten im SYSVOL-Ordner, um den Replikations-Datenverkehr zu minimieren.  
  
22. Der Gast aktiviert die DNS-Clientregistrierung erneut, da der Computer nun eindeutig benannt und mit dem Netzwerk verbunden ist.  
  
23. Der Gast führt die im <SysprepInformation>-Element in der Datei in DefaultDCCloneAllowList.xml angegebenen SYSPREP-Module aus, um Verweise auf den vorherigen Computernamen und alte SIDs zu entfernen.  
  
24. Klonvorgang und Heraufstufung sind abgeschlossen.  
  
    1.  Der Gast entfernt das DSRM-Startkennzeichen, sodass der nächste Neustart normal ausgeführt wird.  
  
    2.  Der Gast benennt die Datei DCCloneConfig.xml mit angefügtem Zeitstempel um, sodass diese beim nächsten Neustart nicht erneut gelesen wird.  
  
    3.  Der Gast entfernt den VdcIsCloning DWORD-Registrierungswert unter HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters.  
  
    4.  Der Gast setzt den "VdcCloningDone" DWORD-Registrierungswert unter HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters auf 0x1. Windows verwendet diesen Wert nicht, stellt ihn jedoch als Markierung für externe Programme bereit.  
  
25. Der Gast aktualisiert das msDS-GenerationID-Attribut seines eigenen geklonten Domänencontroller-Objekts auf den aktuellen Wert der Gast-VM-Generations-ID.  
  
26. Der Gast wird neu gestartet. Er ist nun ein normaler Domänencontroller mit Ankündigungen.  
  
## <a name="virtualized-domain-controller-safe-restore-architecture"></a><a name="BKMK_SafeRestoreArch"></a>Architektur der sicheren Wiederherstellung virtualisierter Domänen Controller  
  
### <a name="overview"></a>Übersicht  
AD DS benötigt einen von der Hypervisor-Plattform bereitgestellten Bezeichner mit dem Namen **VM-Generations-ID** , um die Wiederherstellung einer Momentaufnahme eines virtuellen Computers zu erkennen. AD DS speichert diesen Bezeichner bei der Heraufstufung des Domänencontrollers in der Datenbank (NTDS.DIT). Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der VM-Generations-ID des virtuellen Computers mit einem Wert in der Datenbank verglichen. Unterscheiden sich die beiden Werte, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, um das erneute Verwenden der USN oder mögliche doppelt vergebene Sicherheitsprinzipale zu verhindern. Die sichere Wiederherstellung kann in zwei Szenarien erfolgen:  
  
-   Beim Start eines virtuellen Domänencontrollers, nachdem eine Momentaufnahme im heruntergefahrenen Zustand wiederhergestellt wurde  
  
-   Beim Wiederherstellen einer Momentaufnahme auf einem laufenden virtuellen Domänencontroller  
  
    Wenn sich der virtuelle Domänencontroller im Unterbrechungsstatus befindet und nicht heruntergefahren wurde, müssen Sie den AD DS-Dienst neu starten, um eine neue RID Pool-Anfrage auszulösen. Sie können den AD DS-Dienst über das Dienste-Snap-In oder mithilfe von Windows PowerShell (Restart-Service NTDS -force) neu starten.  
  
In den folgenden Abschnitten wird die sichere Wiederherstellung für die einzelnen Szenarien detailliert beschrieben.  
  
### <a name="safe-restore-detailed-processing"></a>Sichere Wiederherstellung: Detaillierter Prozess  
Das folgende Flussdiagramm beschreibt die sichere Wiederherstellung beim Start eines virtuellen Domänencontrollers, nachdem eine Momentaufnahme im heruntergefahrenen Zustand wiederhergestellt wurde.  
  
![Virtualisierte DC-Architektur](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringNormalBoot.png)  
  
1.  Wenn der virtuelle Computer nach der Wiederherstellung einer Momentaufnahme hochfährt, erhält er vom Hypervisor-Host eine neue VM-Generations-ID aufgrund der Wiederherstellung.  
  
2.  Die neue VM-Generations-ID des virtuellen Computers wird mit der VM-Generations-ID in der Datenbank verglichen. Da die beiden IDs nicht übereinstimmen, werden Virtualisierungs-Sicherheitsmaßnahmen implementiert (siehe Schritt 3 im vorigen Abschnitt). Nach Abschluss der Wiederherstellung wird die VM-Generierungs-ID des AD DS-Computerobjekts aktualisiert, um mit der neuen, vom Hypervisor-Host bereitgestellten ID übereinzustimmen.  
  
3.  Der Gast implementiert die folgenden Virtualisierungs-Sicherheitsmaßnahmen:  
  
    1.  Der lokale RID-Pool wird ungültig gemacht.  
  
    2.  Für die Domänencontroller-Datenbank wird eine neue Aufrufkennung gesetzt.  
  
> [!NOTE]  
> Dieser Teil der sicheren Wiederherstellung überlappt sich mit dem Klonvorgang. Obwohl es sich um eine sichere Wiederherstellung eines virtuellen Domänencontrollers nach dem Neustart nach einer Momentaufnahmen-Wiederherstellung handelt, werden dieselben Schritte auch beim Klonvorgang ausgeführt.  
  
Das folgende Diagramm zeigt, wie die Virtualisierungs-Sicherheitsmaßnahmen Abweichungen durch USN-Rollback verhindern, wenn eine Momentaufnahme auf einem laufenden Domänencontroller wiederhergestellt wird.  
  
![Virtualisierte DC-Architektur](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringSnapShotRestore.png)  
  
> [!NOTE]  
> Die vorige Illustration wurde vereinfacht, um die Konzepte zu erläutern.  
  
1.  Zum Zeitpunkt T1 erstellt der Hypervisor-Administrator eine Momentaufnahme des virtuellen DC1. DC1 hat zu diesem Zeitpunkt einen USN-Wert (**highestCommittedUsn** in der Praxis) von 100, einen InvocationId (im vorigen Diagramm als ID dargestellt)-Wert von A (in der Praxis wäre dies die GUID). Beim savedVMGID-Wert handelt es sich um die VM-Generations-ID in der DIT-Datei des DC (für das Computerobjekt des DC in einem Attribut mit dem Namen **msDS-GenerationId**gespeichert). VMGID ist der aktuelle Wert der VM-Generations-ID aus dem Treiber des virtuellen Computers. Dieser Wert wird vom Hypervisor bereitgestellt.  
  
2.  Zu einem späteren Zeitpunkt T2 werden 100 Benutzer zu diesem DC hinzugefügt (betrachten Sie Benutzer als ein Beispiel für Änderungen, die zwischen T1 und T1 auf diesem DC durchgeführt wurden. Diese Änderungen können in der Praxis eine Mischung aus Benutzererstellungen, Gruppenerstellungen, Kennwortänderungen, Attributänderungen usw. sein). In diesem Beispiel verbraucht jede Änderung eine eindeutige USN (obwohl eine Benutzererstellung in der Praxis mehr als eine USN verbrauchen kann). Vor der Übernahme dieser Änderungen prüft DC1, ob der Wert der VM-Generations-ID in dessen Datenbank (savedVMGID) mit dem aktuellen, aus dem Treiber verfügbaren Wert (VMGID), übereinstimmt. Die beiden Werte sind gleich, da noch kein Rollback erfolgt ist. Daher werden die Änderungen übernommen, und USN auf 200 gesetzt, um anzugeben, dass die nächste Änderung USN 201 verwenden kann. InvocationId, savedVMGID und VMGID ändern sich nicht. Diese Änderungen werden beim nächsten Replikationszyklus auf DC2 repliziert. DC2 aktualisiert den hohen Grenzwert (und **Updatess Vector**), der hier einfach als DC1 (A) @USN = 200 dargestellt wird. DC2 kennt also alle Änderungen aus DC1 im Kontext der Aufrufkennungen A bis USN 200.  
  
3.  Zum Zeitpunkt T3 wird die zum Zeitpunkt T1 erstellte Momentaufnahme auf DC1 angewendet. Für DC1 wurde ein Rollback ausgeführt. Die USN wird daher auf 100 zurückgesetzt, um anzugeben, dass USNs ab 101 für die folgenden Änderungen verwendet werden können. Zu diesem Zeitpunkt wäre der Wert von VMGID jedoch unterschiedlich auf Hypervisoren, die die VM-Generations-ID unterstützen.  
  
4.  Wenn auf DC1 in der Folge irgendwelche Änderungen durchgeführt werden, wird der Wert der VM-Generations-ID in der Datenbank (savedVMGID) mit dem Wert aus dem Treiber des virtuellen Computers (VMGID) verglichen. In diesem Fall stimmen die IDs nicht überein. DC1 interpretiert dies als Anzeigen für einen Rollback und löst Virtualisierungs-Sicherheitsmaßnahmen aus. Dabei wird die eigene Aufrufkennung (ID = B) zurückgesetzt und der RID-Pool gelöscht (im vorigen Diagramm nicht gezeigt). Anschließend wird der neue Wert von vmgid in der Datenbank gespeichert, und diese Updates werden im Kontext der neuen invocationID B für diese Updates ("US-101-250") ausgeführt. Beim nächsten Replikations Zyklen weiß DC2 nichts von DC1 im Kontext von invocationID b, sodass alles von DC1 angefordert wird, das invocationID b zugeordnet ist. Folglich werden die Updates, die auf DC1 nach der Anwendung der Momentaufnahme ausgeführt werden, sicher zusammengeführt. Außerdem werden die zum Zeitpunkt T2 auf DC1 durchgeführten Änderungen (die auf DC1 nach der Wiederherstellung der Momentaufnahme verloren gegangen waren) bei der nächsten Replikation wieder auf DC1 repliziert, da diese Änderungen zuvor auf DC2 repliziert worden waren (angezeigt durch die gepunktete Linie zurück zu DC1).  
  
Nachdem der Gast die Virtualisierungs-Sicherheitsmaßnahmen implementiert hat, repliziert NTDS die Active Directory-Objektdifferenzen in eingehender Richtung nicht autoritativ von einem Domänencontroller. Der Aktualitätsvektor des Zielverzeichnisdienstes wird entsprechend aktualisiert. Anschließend synchronisiert der Gast SYSVOL:  
  
-   Falls FRS verwendet wird, beendet der Gast den NTFRS-Dienst und setzt den D2 BURFLAGS-Registrierungswert. Anschließend wird der NTFRS-Dienst gestartet, repliziert nicht autoritativ in eingehender Richtung und verwendet dabei existierende und unveränderte SYSVOL-Daten, soweit möglich.  
  
-   Bei Verwendung von DFSR beendet der Gast den DFSR-Dienst und löscht die DFSR-Datenbankdateien (Standard Speicherort:%SystemRoot%\System Volume information\dfsr\\ *<database GUID>* ). Anschließend wird der DSFR-Dienst gestartet, repliziert nicht autoritativ in eingehender Richtung und verwendet dabei existierende und unveränderte SYSVOL-Daten, soweit möglich.  
  
> [!NOTE]  
> -   Falls der Hypervisor keine VM-Generations-ID zum Vergleich bereitstellt, unterstützt dieser die Virtualisierungs-Schutzmaßnahmen nicht und der Gast funktioniert wie ein virtualisierter Domänencontroller unter Windows Server 2008 oder einer früheren Version. Der Gast implementiert den USN Rollback-Quarantäneschutz, falls versucht wird, mit USNs zu replizieren, die unterhalb der zuletzt vom Partner-DC gesehenen USN liegen. Weitere Informationen zum USN-Rollback-Quarantäneschutz finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx).  
  


