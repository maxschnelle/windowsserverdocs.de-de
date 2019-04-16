---
ms.assetid: 341614c6-72c2-444f-8b92-d2663aab7070
title: "Architektur virtualisierter Domänencontroller"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac8b190df065547d82aa431761eb5c00c94a2ad6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-architecture"></a>Architektur virtualisierter Domänencontroller

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema behandelt die Architektur des Klonen virtualisierter Domänencontroller und die sichere Wiederherstellung. Es zeigt die Prozesse, die klonen und Klon-und Wiederherstellungsprozessen sowie eine ausführliche Erklärung der einzelnen Schritte im Prozess.  
  
-   [Architektur für das Klonen von virtualisierten Domänencontrollern](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)  
  
-   [Architektur virtualisierter Domänencontroller die sichere Wiederherstellung](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)  
  
## <a name="BKMK_CloneArch"></a>Architektur für das Klonen von virtualisierten Domänencontrollern  
  
### <a name="overview"></a>(Übersicht)  
Klonen virtualisierter Domänencontroller basiert auf der Hypervisor-Plattform bereitgestellten Bezeichner mit dem Namen **VM-Generations-ID** zum Erstellen eines virtuellen Computers zu erkennen. AD DS speichert den Wert der diese ID in der Datenbank (NTDS. DIT) während der heraufstufung des Domänencontrollers. Wenn Sie den virtuellen Computer gestartet wird, wird der aktuelle Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der Datenbank verglichen. Wenn die beiden Werte unterschiedlich sind, wird der Domänencontroller wird die Aufrufkennung zurückgesetzt und der RID-Pool, damit keine erneute verwenden der USN oder das potenzielle erstellen doppelte Sicherheitsprinzipale. Der Domänencontroller anschließend sucht nach der Datei DCCloneConfig.xml an den Speicherorten genannten in Schritt 3 in [Cloning Detailed Processing](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneProcessDetails). Wenn eine DCCloneConfig.xml-Datei gefunden wird, muss er als Klon bereitgestellt wird und zum Bereitstellen von sich selbst als einen zusätzlichen Domänencontroller wieder heraufstufen mit der vorhandenen NTDS Klonvorgang ausgelöst. DIT und SYSVOL-Inhalt kopiert Quellmedien.  
  
In einer gemischten Umgebung, in dem alle Hypervisoren VM-Generations-ID unterstützt, andere dagegen nicht ist es möglich, dass ein Klon-Medium versehentlich auf einem Hypervisor bereitgestellt werden, die VM-Generations-ID nicht unterstützt. Das Vorhandensein der Datei DCCloneConfig.xml gibt die Absicht, einen Domänencontroller zu klonen. Aus diesem Grund Wenn eine DCCloneConfig.xml-Datei beim Starten jedoch ein VM-Generations-ID gefunden wird ist nicht vom Host angegeben, der Klon-DC in Directory Services-Wiederherstellungsmodus (DSRM), die Auswirkung auf die restliche Umgebung zu verhindern, dass gestartet wird. Das Klon-Medium kann anschließend in einem Hypervisor, der die VM-Generations-ID unterstützt verschoben werden, und klicken Sie dann das Klonen dort wiederholt werden.  
  
Wenn das Klon-Medium auf einem Hypervisor, der die VM-Generations-ID unterstützt bereitgestellt wird, aber eine DCCloneConfig.xml-Datei bereitgestellt wird, wird der Domänencontroller eine Änderung der VM-Generations-ID zwischen seiner eigenen DIT und der von dem neuen virtuellen Computer erkennt, wird es Sicherheitsmaßnahmen, um zu verhindern, dass USN-Wiederverwendung und doppelte SIDs ausgelöst. Allerdings wird das Klonen nicht gestartet, sodass der sekundäre Domänencontroller weiterhin unter derselben Identität wie der Quelldomänencontroller ausgeführt. Zu den frühesten Zeitpunkt zu Inkonsistenzen in der Umgebung zu vermeiden sollten diesen sekundären Domänencontroller aus dem Netzwerk entfernt werden. Weitere Informationen dazu, wie Sie diesen sekundären Domänencontroller freigeben und gleichzeitig sicherstellen, dass Updates ausgehend repliziert werden, finden Sie im Microsoft KB-Artikel [2742970](https://support.microsoft.com/kb/2742970).  
  
### <a name="BKMK_CloneProcessDetails"></a>Zum klonprozess  
Das folgende Diagramm zeigt die Architektur für den ursprünglichen klonprozess und für Wiederholungen des klonprozesses. Diese Prozesse werden weiter unten in diesem Thema ausführlich erläutert.  
  
**Ursprünglicher Klonprozess**  
  
![Architektur virtualisierter Domänencontroller](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_InitialCloningProcess.png)  
  
**Wiederholung des klonprozesses**  
  
![Architektur virtualisierter Domänencontroller](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_CloningRetryProcess.png)  
  
Die folgenden Schritte wird den Prozess genauer erläutert:  
  
1.  Ein vorhandenen virtuellen Domänencontrollers wird hochgefahren in einem Hypervisor, der VM-Generations-ID unterstützt.  
  
    1.  Diese VM hat keine vorhandenen Wertesatz der VM-Generations-ID-für die AD DS-Computerobjekt nach der heraufstufung.  
  
    2.  Auch wenn sie null ist, wird das nächste Computer erstellen weiterhin klonen, heißt dies wie eine neue VM-Generations-ID nicht übereinstimmt.  
  
    3.  Die VM-Generations-ID wird nach dem nächsten Neustart des DC festgelegt und wird nicht repliziert.  
  
2.  Anschließend liest der virtuelle Computer vom VMGenerationCounter-Treiber bereitgestellte VM-Generations-ID. Die beiden VM-Generations-IDs werden verglichen.  
  
    1.  Wenn die IDs übereinstimmen, dies ist nicht um eine neue virtuelle Maschine, und wird kein Klonvorgang ausgelöst. Wenn eine DCCloneConfig.xml-Datei existiert, benennt der Domänencontroller die Datei mit einen Zeitstempel, um das Klonen zu verhindern. Der Server weiterhin normal starten. Dies ist die Funktionsweise von jedem Neustart des virtuellen Domänencontrollers in Windows Server 2012.  
  
    2.  Wenn die beiden IDs nicht übereinstimmen, ist dies eine neue virtuelle Maschine, die ein NTDS enthält. DIT aus einem vorherigen Domänencontroller (oder es ist eine wiederhergestellte Momentaufnahme). Wenn eine DCCloneConfig.xml-Datei vorhanden ist, fährt der Domänencontroller mit dem klonprozess fort. Wenn dies nicht der Fall ist, fährt mit der Wiederherstellungsprozess der Momentaufnahme. Finden Sie unter [Architektur virtualisierter Domänencontroller die sichere Wiederherstellung](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).  
  
    3.  Wenn der Hypervisor keine VM-Generations-ID zum Vergleich bietet, aber eine DCCloneConfig.xml-Datei vorhanden ist, wird der Gast benennt die Datei um und startet im DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen. Wenn keine dccloneconfig.xml-Datei vorhanden ist, fährt der Gast Normal (mit einem möglichen doppelt vorhandenen Domänencontrollern im Netzwerk). Weitere Informationen zum Freigeben dieses doppelt vorhandenen Domänencontrollers finden Sie im Microsoft KB-Artikel [2742970](https://support.microsoft.com/kb/2742970).  
  
3.  Der NTDS-Dienst prüft den Wert des VDCisCloning-DWORDs Name des Registrierungsschlüssels (unter HKEY_Local_Machine\System\CurrentControlSet\Services\Ntds\Parameters).  
  
    1.  Wenn es nicht vorhanden ist, ist dies eine erste Versuch zu für diese virtuelle Maschine klonen. Der Gast implementiert die VDC-Objekt Duplizierung Schutzvorrichtungen für den lokalen RID-Pool ungültig und eine neue Replikations-Aufrufkennung für den Domänencontroller festlegen  
  
    2.  Wenn sie bereits auf 0 x 1 festgelegt ist, ist dies ein Versuch, Klonen "Wiederholen" Vorherige klonversuch ist fehlgeschlagen. Die VDC-Objekt Sicherheitsmaßnahmen werden nicht übernommen, und sie mussten Sie zuvor bereits ausgeführt wurden und würden unnötigerweise ändern den Gast mehrere Male.  
  
4.  Der Name des Registrierungswerts IsClone DWORD ist (unter Hkey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters) geschrieben.  
  
5.  Der NTDS-Dienst ändert die Gast-Boot-Kennzeichnung für alle weiteren Neustarts im DS-Wiederherstellungsmodus gestartet.  
  
6.  Der NTDS-Dienst versucht, lesen Sie die Datei DcCloneConfig.xml an der drei möglichen Orten (DSA-Arbeitsverzeichnis, % windir%\NTDS oder Wechselmedien Lese-/Schreib-Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stammverzeichnis des Laufwerks).  
  
    1.  Wenn die Datei nicht in einen gültigen Speicherort vorhanden ist, prüft der Gast die IP-Adresse für die Duplizierung. Wenn die IP-Adresse nicht dupliziert ist, wird der Server normal hochgefahren. Wenn eine doppelte IP-Adresse vorhanden ist, startet den Computer im DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen.  
  
    2.  Wenn die Datei in einen gültigen Speicherort vorhanden ist, prüft der NTDS-Dienst die Einstellungen. Wenn die Datei leer ist (oder einzelne Einstellungen leer sind), konfiguriert NTDS automatische Werte für diese Einstellungen.  
  
    3.  Wenn die Datei DcCloneConfig.xml vorhanden ist, aber ungültige Einträge enthält oder nicht lesbar ist, wird der Klonvorgang fehl und der Gast in Directory Services-Wiederherstellungsmodus (DSRM) gestartet.  
  
7.  Der Gast deaktiviert alle automatische DNS-Registrierung um versehentliche Übernahme von Quell-Computername und IP-Adressen zu verhindern.  
  
8.  Der Gast beendet den Anmeldedienst, um Ankündigungen oder Antworten von Netzwerk AD DS-Anfragen von Clients zu verhindern.  
  
9. NTDS prüft, ob keine Dienste oder Programme installiert, die nicht Teil der DefaultDCCloneAllowList.xml oder customdccloneallowlist.XML enthalten sind  
  
    1.  Wenn Dienste oder Programme installiert, die nicht in der Standard-Ausschlussliste enthalten sind, Liste "zulassen" oder der benutzerdefinierten Ausschlussliste enthalten, startet der Klonvorgang fehl und der Gast im DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern zu schützen.  
  
    2.  Falls keine Inkompatibilitäten vorliegen, wird der Klonvorgang fortgesetzt.  
  
10. Wenn automatische IP-Adressierung aufgrund leerer DCCloneConfig.xml-Netzwerkeinstellungen verwendet wird, aktiviert der Gast DHCP auf den Netzwerkadaptern, um eine IP-Adresslease, Netzwerkrouting und Namensauflösungsinformationen zu erhalten.  
  
11. Der Gast sucht und kontaktiert den Domänencontroller, der die PDC-Emulator-FSMO-Rolle ausgeführt wird. Dieser verwendet DNS und das DCLocator-Protokoll. Dies stellt eine RPC-Verbindung und ruft die Methode IDL_DRSAddCloneDC auf, die Domänencontroller-Computerobjekt zu klonen.  
  
    1.  Wenn der Quell-Computerobjekt des Gasts die erweiterte domänenkopf-Berechtigung der enthält "' Domänencontroller die Erstellung eines Klons von sich selbst erlauben" Klonvorgang fortgesetzt.  
  
    2.  Wenn der Quell-Computerobjekt des Gasts nicht enthält, dass der Klonvorgang fehl und der Gast erweiterte Berechtigung im DSRM, um das Netzwerk vor doppelt vorhandenen Domänencontrollern schützen gestartet wird.  
  
12. Der AD DS-Objekt Computername wird festgelegt, mit dem Namen in der Datei DCCloneConfig.xml angegeben werden, sofern vorhanden, oder andernfalls automatisch auf dem PDCE generiert. NTDS erstellt das korrekte NTDS-Einstellungsobjekt für den entsprechenden logischen Active Directory-Standort.  
  
    1.  Ist dies ein primärer Domänencontroller klonen, der Gast benennt den lokalen Computer und neu gestartet wird. Nach dem Neustart er wird durch die Schritte 1 bis 10 erneut durchlaufen und anschließend Schritt 13.  
  
    2.  Ist dies ein Replikat-DC klonen, kein Neustart in dieser Phase ist.  
  
13. Der Gast stellt die heraufstufungseinstellungen für den DS-rollenserverdienst, der heraufstufung beginnt.  
  
14. Der DS-rollenserverdienst beendet alle AD DS-verwandten Dienste (NTDS, NTFRS/DFSR, KDC, DNS).  
  
15. Der Gast erzwingt NT5DS (Windows NTP)-zeitsynchronisierung mit einem anderen Domänencontroller (in einer Hierarchie mit standardmäßigen Windows-Zeitdienst bedeutet dies mithilfe den PDCE). Der Gast kontaktiert den PDCE. Alle vorhandenen Kerberos-Tickets werden gelöscht.  
  
16. Der Gast konfiguriert die DFSR- oder NTFRS-Dienste automatisch ausgeführt. Der Gast löscht alle vorhandene DFSR und NTFRS-Datenbankdateien (Standard: c:\windows\ntfrs und c:\system Volume Information\dfsr\\*< Database_GUID >*), um die nicht autoritative Synchronisierung von SYSVOL zu erzwingen, wenn der Dienst wieder gestartet wird. Der Gast löscht nicht die Dateiinhalte von SYSVOL mit Startwerten bei die Synchronisierung später gestartet wird.  
  
17. Der Gast wird umbenannt. Der DS-rollenserverdienst auf dem Gast beginnt mit AD DS-Konfiguration (heraufstufung), mit der vorhandenen NTDS. DIT-Datei als Quelle, anstelle von der Vorlagendatenbank in c:\windows\system32 wie eine heraufstufung normalerweise enthalten.  
  
18. Der Gast kontaktiert den Inhaber der RID-Master-FSMO um eine neue RID-Pool-Zuweisung zu erhalten.  
  
19. Der Heraufstufungsprozess erstellt eine neue Aufruf-ID und das NTDS-Einstellungsobjekt für den geklonten Domänencontroller neu (unabhängig vom Klonvorgang, dies ist Teil der heraufstufung bei Verwendung einer vorhandenen NTDS. DIT-Datenbank).  
  
20. NTDS wird in Objekten, die fehlen, neuer oder eine höhere Version von einem Partner-Domänencontroller repliziert. Der NTDS. DIT enthält bereits Objekte vom Zeitpunkt der Quelldomänencontroller offline ist, und diese werden nach Möglichkeit verwendet, um Replikations-Datenverkehr zu minimieren eingehende. Die globalen katalogpartionen werden gefüllt.  
  
21. Der DFSR- oder FRS-Dienst startet, und da keine Datenbank, SYSVOL nicht autoritativ ist von einem Replikationspartner eingehende synchronisiert. Dieser Prozess verwendet bereits vorhandene Daten im Ordner "SYSVOL", um den Replikations-Datenverkehr zu minimieren.  
  
22. Der Gast reaktiviert DNS-Clientregistrierung nun, dass der Computer eindeutig benannt und im Netzwerk ist.  
  
23. Der Gast führt die vom DefaultDCCloneAllowList.xml angegebenen SYSPREP-Module <SysprepInformation> Element, um alle Verweise auf den vorherigen Computernamen und die SID zu bereinigen.  
  
24. Die heraufstufung des Klonvorgangs ist abgeschlossen.  
  
    1.  Der Gast entfernt die DSRM-Startkennzeichen, damit beim nächste Neustart normal ausgeführt wird.  
  
    2.  Der Gast benennt die Datei DCCloneConfig.xml mit einem angefügten Datums-/ Uhrzeitangabe, damit es erneut nicht beim nächsten Neustart gelesen wird.  
  
    3.  Der Gast entfernt den VdcIsCloning DWORD Name des Registrierungswerts unter HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters.  
  
    4.  Der Gast setzt den "VdcCloningDone" DWORD Name des Registrierungswerts unter HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters auf 0 x 1. Windows wird dieser Wert nicht verwendet, stellt ihn jedoch als Markierung für Dritte.  
  
25. Der Gast aktualisiert das MsDS-GenerationID-Attribut für einen eigenen geklonten Domänencontroller-Objekts mit den aktuellen Gast-VM-Generations-ID übereinstimmen  
  
26. Der Gast wird neu gestartet. Es ist nun ein normaler Domänencontroller mit Ankündigungen.  
  
## <a name="BKMK_SafeRestoreArch"></a>Architektur virtualisierter Domänencontroller die sichere Wiederherstellung  
  
### <a name="overview"></a>(Übersicht)  
AD DS benötigt einen von der Hypervisor-Plattform bereitgestellten Bezeichner mit dem Namen **VM-Generations-ID** die Wiederherstellung einer Momentaufnahme eines virtuellen Computers zu erkennen. AD DS speichert den Wert der diese ID in der Datenbank (NTDS. DIT) während der heraufstufung des Domänencontrollers. Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der Datenbank verglichen. Wenn die beiden Werte unterschiedlich sind, wird der Domänencontroller wird die Aufrufkennung zurückgesetzt und der RID-Pool, damit keine erneute verwenden der USN oder das potenzielle erstellen doppelte Sicherheitsprinzipale. Es gibt zwei Szenarien, in denen die sichere Wiederherstellung auftreten kann:  
  
-   Wenn ein virtuellen Domänencontrollers gestartet wird, nachdem eine Momentaufnahme wiederhergestellt wurde, während er heruntergefahren wurde  
  
-   Wenn eine Momentaufnahme auf einem laufenden Domänencontroller wiederhergestellt wird  
  
    Ist der virtuelle Domänencontroller in der Momentaufnahme in einen angehaltenen Zustand nicht herunterfahren, müssen Sie die AD DS-Dienst, um eine neue RID-Pool-Anfrage auszulösen neu zu starten. Sie können den AD DS-Dienst neu starten, verwenden das Dienste-Snap-in oder mithilfe von Windows PowerShell (Restart-Service NTDS-force).  
  
In den folgenden Abschnitten werden die sichere Wiederherstellung für jedes Szenario ausführlich.  
  
### <a name="safe-restore-detailed-processing"></a>Sichere Wiederherstellung: detaillierter Prozess  
Das folgende Flussdiagramm zeigt, wie die sichere Wiederherstellung tritt auf, wenn Sie ein virtuellen Domänencontroller gestartet wird, nachdem eine Momentaufnahme wiederhergestellt wurde, während er heruntergefahren wurde.  
  
![Architektur virtualisierter Domänencontroller](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringNormalBoot.png)  
  
1.  Wenn die virtuelle Maschine von nach einer Momentaufnahmen-Wiederherstellung gestartet wird, müssen sie neue VM-Generations-ID, die vom Hypervisor-Host aufgrund der Wiederherstellung bereitgestellt.  
  
2.  Die neue VM-Generations-ID des virtuellen Computers wird mit der VM-Generations-ID in der Datenbank verglichen. Da die beiden IDs nicht übereinstimmen, setzt es Virtualisierungs-Sicherheitsmaßnahmen implementiert (siehe Schritt 3 im vorherigen Abschnitt). Nach der Wiederherstellung wird, wird die VM-Generierungs auf die AD DS-Computerobjekts aktualisiert, um der neuen ID vom Hypervisor-Host bereitstellen.  
  
3.  Der Gast setzt Virtualisierungs-Sicherheitsmaßnahmen:  
  
    1.  Den lokalen RID-Pool wird ungültig.  
  
    2.  Wenn eine neue Aufruf-ID für die Domänencontroller-Datenbank.  
  
> [!NOTE]  
> Dieser Teil der sicheren Wiederherstellung überlappt mit dem Klonvorgang. Obwohl dieser Vorgang sichere Wiederherstellung eines virtuellen Domänencontrollers, ist nachdem es gestartet wird, um nach der Wiederherstellung einer Momentaufnahme ab, werden dieselben Schritte auch während des Klonens.  
  
Das folgende Diagramm zeigt, wie verhindert Virtualisierungs-Sicherheitsmaßnahmen abweichungen durch USN-Rollback, wenn eine Momentaufnahme auf einem laufenden Domänencontroller wiederhergestellt wird.  
  
![Architektur virtualisierter Domänencontroller](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringSnapShotRestore.png)  
  
> [!NOTE]  
> Die vorige Illustration wurde vereinfacht, um die Konzepte zu erläutern.  
  
1.  Zum Zeitpunkt T1 erstellt der Hypervisor-Administrator eine Momentaufnahme des virtuellen DC1. DC1 zu diesem Zeitpunkt hat einen USN-Wert (**HighestCommittedUsn** in der Praxis) von 100 InvocationId (im vorigen Diagramm als ID dargestellt)-Wert von A (in der Praxis wäre dies die GUID). Beim SavedVMGID-Wert wird die VM-Generations-ID in der DIT-Datei des DC (für das Computerobjekt des DC in einem Attribut mit dem Namen gespeichert **MsDS-GenerationId**). VMGID ist der aktuelle Wert der die VM-Generations-ID aus dem Treiber des virtuellen Computers. Dieser Wert wird vom Hypervisor bereitgestellt.  
  
2.  Zu einem späteren Zeitpunkt T2 werden 100 Benutzer zu diesem DC hinzugefügt (betrachten Sie Benutzer als Beispiel für Updates, die auf diesem DC zwischen durchgeführt wurden Zeit T1 und T2; diese Updates können tatsächlich eine Mischung aus benutzererstellungen, gruppenerstellungen, Kennwort-Updates, attributänderungen usw. sein). In diesem Beispiel verbraucht jede Änderung eine eindeutige USN (Obwohl in der Praxis die benutzererstellung eines mehr als eine USN verbrauchen kann). Vor der Übernahme dieser Änderungen prüft DC1, wenn der Wert der VM-Generations-ID in der Datenbank (SavedVMGID) identisch mit den aktuellen Wert von der Treiber (VMGID) verfügbar ist. Sind identisch, da noch kein Rollback geschehen ist, damit die Updates ein Commit ausgeführt sind und USN auf 200, gibt an, dass die nächste Änderung USN 201 verwenden kann. Es ist keine Änderung InvocationId, SavedVMGID und VMGID. Diese Updates werden Sie auf DC2 am nächsten Replikationszyklus repliziert. DC2 aktualisiert seinen hohen Grenzwert (und **UptoDatenessVector**) dargestellt als DC1(A) hier @USN = 200. DC2 kennt also alle Änderungen aus DC1 im Kontext der Aufrufkennungen A bis USN 200.  
  
3.  Zum Zeitpunkt T3 wird zum Zeitpunkt T1 Momentaufnahme auf DC1 angewendet. DC1 wurde, Rollback ausgeführt, damit die USN bis 100 Rollback, der angibt, dass USNs ab 101 konnten mit ihrer Hilfe nachfolgende Updates zuordnen. Jedoch wäre in diesem Fall der Wert von VMGID unterschiedlich auf Hypervisoren, die VM-Generations-ID unterstützen.  
  
4.  Später, wenn DC1 ein Update ausgeführt wird, wird überprüft, ob der Wert der VM-Generations-ID, die sie in der Datenbank (SavedVMGID) hat den Wert aus dem Treiber des virtuellen Computers (VMGID) identisch ist. In diesem Fall ist es nicht identisch, so dass DC1 dies als anzeigen für einen Rollback leitet und Virtualisierungs-Sicherheitsmaßnahmen löst. Anders ausgedrückt, wird seine InvocationId zurückgesetzt (ID = B) und der RID-Pool (in der obigen Abbildung nicht dargestellt). Klicken Sie dann den neuen Wert von VMGID in seiner Datenbank speichert und führt einen Commit für die Updates (USN 101 - 250) im Rahmen der neuen InvocationId B. Bei der nächsten Replikationszyklus nicht bekannt ist, DC2 von DC1 im Kontext der Aufrufkennung B, damit alles von DC1 InvocationID B. zugeordnete angefordert Daher werden die Updates auf DC1 ausgeführt wird, nach der Anwendung des Snapshots sicher konvergiert werden. Darüber hinaus würde der Updates, die ausgeführt wurden, auf DC1 auf T2 (die auf DC1 nach der Wiederherstellung der Momentaufnahme verloren wurden) wieder auf DC1 bei der nächsten geplanten Replikation repliziert werden, da sie sich an DC2 repliziert worden waren (durch die gepunktete Linie zurück zu DC1 angezeigt).  
  
Nachdem der Gast die Virtualisierungs-Sicherheitsmaßnahmen implementiert hat, repliziert NTDS die Active Directory eingehender nicht autoritativ von einem Partner-Domänencontroller. Der Aktualitätsvektor des zielverzeichnisdienstes wird entsprechend aktualisiert. Anschließend synchronisiert der Gast SYSVOL:  
  
-   Falls FRS verwendet wird, wird der Gast den NTFRS-Dienst beendet und setzt D2 BURFLAGS-Registrierungswert. Anschließend wird den NTFRS-Dienst, der repliziert nicht autoritativ in eingehender existierende und unveränderte SYSVOL Daten nach Möglichkeit gestartet.  
  
-   Falls DSFR verwendet wird, beendet der Gast den DFSR-Dienst und löscht die DFSR-Datenbankdateien (Standardspeicherort: %systemroot%\system Volume Information\dfsr\\*<database GUID>*). Sie dann die DFSR-Dienst gestartet, der repliziert nicht autoritativ in eingehender existierende und unveränderte SYSVOL Daten nach Möglichkeit.  
  
> [!NOTE]  
> -   Wenn der Hypervisor keine VM-Generations-ID zum Vergleich bereitstellt, der Hypervisor unterstützt keine Virtualisierungs-Sicherheitsmaßnahmen und der Gast funktioniert wie eine virtualisierte Domänencontroller, die Windows Server 2008 R2 ausgeführt wird oder einer früheren Version. Der Gast implementiert die USN-Rollback-Quarantäneschutz, wenn versucht wird zum Starten der Replikation mit USNs ab, die nicht über die letzten höchste USN anzeigen, indem Sie das Partner-DC erweiterte haben. Weitere Informationen zum USN-Rollback-Quarantäneschutz finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx)  
  


