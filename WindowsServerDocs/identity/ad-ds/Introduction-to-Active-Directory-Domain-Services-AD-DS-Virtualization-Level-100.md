---
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
title: "Einführung in die Active Directory Domain Services (AD DS) Virtualization (Level 100)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3c7fdc2e20bc4a27f2555af54f396a15f664d6c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100"></a>Einführung in die Active Directory Domain Services (AD DS) Virtualization (Level 100)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Virtualisierung von Active Directory-Domänendienste (AD DS)-Umgebungen wurde für eine Anzahl von Jahren laufende. Ab Windows Server 2012, bietet AD DS mehr Unterstützung für das Virtualisieren von Domänencontrollern, indem virtualisierungssichere Funktionen eingeführt und die schnelle Bereitstellung von virtuellen Domänencontrollern durch Klonen ermöglicht wurde. Diese neuen Virtualisierungsfeatures größer öffentlicher und privater Clouds unterstützen, hybridumgebungen Teile von AD DS lokal vorhanden sind und in der Cloud und AD DS-Infrastrukturen, die vollständig befinden sich auf lokale.

**In diesem Dokument**

-   [Sichere Virtualisierung von Domänencontrollern](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#safe_virt_dc)

-   [Klonen virtualisierter Domänencontroller](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#virtualized_dc_cloning)

-   [Schritte zum Bereitstellen eines geklonten virtualisierten Domänencontrollers](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)

-   [Problembehandlung](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#troubleshooting)

## <a name="safe_virt_dc"></a>Sichere Virtualisierung von Domänencontrollern
Virtuelle Umgebungen bedeuten individuelle Herausforderungen für verteilte Arbeitslasten, die eine logische Uhr Replikationsschema abhängen. AD DS-Replikation verwendet beispielsweise einen monoton steigenden Wert (bekannt als eine USN oder Update Sequence Number) für Transaktionen auf jedem Domänencontroller zugewiesen. Jeder Domänencontroller-Datenbankinstanz erhält auch eine andere Identität als ein InvocationID bezeichnet. Die Aufrufkennung eines Domänencontrollers und seine USN dienen zusammen, wie eine eindeutige Kennung, die Verbindung mit jeder Schreibtransaktion auf jedem Domänencontroller ausgeführt und muss innerhalb der Gesamtstruktur eindeutig sein.

AD DS-Replikation verwendet Aufrufkennungen und USNs auf jedem Domänencontroller, um zu bestimmen, welche Änderungen auf andere Domänencontroller repliziert werden müssen. Wenn ein Domänencontroller ein außerhalb seines Wirkungsbereichs der Rollback wird und eine USN für eine vollkommen andere Transaktion wiederverwendet wird, wird die Replikation nicht zusammengeführt, da andere Domänencontroller davon ausgehen können, dass sie bereits im Kontext der Aufrufkennung der wiederverwendet USN zugeordneten Aktualisierungen erhalten haben.

Die folgende Abbildung zeigt z. B. die Abfolge der Ereignisse, die durchgeführt wird in Windows Server 2008 R2 und älteren Betriebssystemen, wenn ein USN-Rollback auf VDC2, dem Zieldomänencontroller erkannt wird, die auf einem virtuellen Computer ausgeführt wird. In der folgenden Abbildung wird das USN-Rollback auf vdc2 erkannt, wenn ein Replikationspartner feststellt, dass VDC2 einen aktualitäts-USN-Wert gesendet hat, der zuvor vom Replikationspartner gesehen wurde das angibt, dass die Datenbank von VDC2 des rechtzeitig unzulässiges Rollback ausgeführt wurde.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

Ein virtuellen Computer (VM) ganz einfach hypervisoradministratoren einer Domäne des Controllers USNs (die logische Uhr), Rollback z. B. Anwenden eines Snapshots außerhalb seines Wirkungsbereichs der. Weitere Informationen zu USN und USN Rollback, einschließlich weiterer Abbildungen zur Veranschaulichung unerkannter Instanzen eines USN-Rollbacks, finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback).

Ab Windows Server 2012, AD DS virtuelle Domänencontroller gehostet, auf hypervisorplattformen, die Bezeichner mit dem Namen VM-Generations-ID ermitteln und Bereitstellen der erforderlichen Sicherheitsmaßnahmen die AD DS-Umgebung zu schützen, wenn die virtuelle Maschine durch die Anwendung einer VM-Momentaufnahme zeitlich zurückgesetzt wird. VM-Generations-ID verwendet einen unabhängigen Mechanismus des Hypervisor-Hersteller dieser Bezeichner im Adressbereich des virtuellen Gastcomputer verfügbar machen, damit die sichere Virtualisierung ständig von jedem Hypervisor verfügbar ist, der die VM-Generations-ID unterstützt. Dieser Bezeichner kann verwendet werden, von Diensten und Anwendungen, die innerhalb des virtuellen Computers ausgeführt werden, zu ermitteln, ob eine virtuelle Maschine zeitlich zurückgesetzt wurde.

### <a name="BKMK_HowSafeguardsWork"></a>Wie funktionieren diese Virtualisierungs-Sicherheitsmaßnahmen implementiert?
Während der Installation des Domänencontrollers speichert AD DS den Bezeichner VM-Generations-ID zunächst als Teil des MsDS-GenerationID-Attributs auf dem Domänencontroller-Computerobjekt in seiner Datenbank (häufig als Verzeichnisstruktur oder DIT bezeichnet). Die VM-Generations-ID wird von einem Windows-Treiber innerhalb des virtuellen Computers unabhängig nachverfolgt.

Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der die VM-Generations-ID aus dem Treiber des virtuellen Computers mit einem Wert in der DIT verglichen.

Wenn die beiden Werte unterschiedlich sind, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, und vermeiden somit erneute verwenden der USN. Wenn die Werte identisch sind, wird die Transaktion normal ausgeführt.

AD DS vergleicht auch den aktuellen Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der DIT jedes Mal der Domänencontroller neu gestartet wird und, falls abweichend, es wird die Aufrufkennung zurückgesetzt, der RID-Pool und die DIT mit dem neuen Wert aktualisiert. Ebenfalls nicht autoritativ wird den SYSVOL-Ordner synchronisiert, um die sichere Wiederherstellung abzuschließen. Dadurch können Schutzvorrichtungen die Anwendung von Momentaufnahmen auf virtuellen Computern erweitern. Diese Schutzvorrichtungen, die in Windows Server 2012 eingeführte ermöglichen AD DS-Administratoren der individuellen Vorteile der Bereitstellung und Verwaltung von Domänencontrollern in einer virtualisierten Umgebung profitieren.

Die folgende Abbildung zeigt, wie virtualisierungsschutzvorrichtungen angewendet werden, wenn dasselbe USN-Rollback auf einem virtualisierten Domänencontroller erkannt wird, die Windows Server 2012 auf einem Hypervisor ausgeführt wird, der die VM-Generations-ID unterstützt.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

In diesem Fall, wenn der Hypervisor eine Änderung auf VM-Generations-ID-Wert erkennt, virtualisierungsschutzvorrichtungen ausgelöst, einschließlich das Zurücksetzen die aufrufkennung des virtualisierten Domänencontrollers (von A zu B im vorherigen Beispiel) und Aktualisieren des VM-Generations-ID-Werts auf dem virtuellen Computer entsprechend den neuen vom Hypervisor gespeicherten Wert (G2) gespeichert. Den Schutzvorrichtungen wird sichergestellt, dass die Replikation für beide Domänencontroller zusammengeführt.

Mit Windows Server 2012 AD DS Schutzvorrichtungen auf virtuellen Domänencontrollern auf VM-Generations-ID-fähigen Hypervisoren gehostet und stellt sicher, dass die versehentliche Anwendung von Momentaufnahmen oder ähnliche Hypervisor-fähigen Mechanismen, die könnte der Rollback Zustand eines virtuellen Computers nicht unterbrechen die AD DS-Umgebung (durch Verhindern von Replikationsproblemen wie z. B. einer USN-Blase oder veralteten Objekten). Wiederherstellen eines Domänencontrollers durch Anwenden der Momentaufnahme eines virtuellen Computers wird jedoch als alternativmechanismus zum Sichern von einem Domänencontroller nicht empfohlen. Es wird empfohlen, dass Sie Windows Server-Sicherung oder andere VSS Writer weiterhin-basierte sicherungslösungen zu verwenden.

> [!CAUTION]
> Wenn ein Domänencontroller in einer produktionsumgebung versehentlich auf einen Momentaufnahme zurückgesetzt wird, wird empfohlen, dass Sie wenden Sie sich an die Anbieter für die Anwendungen und Dienste auf diesem virtuellen Computer, um Anweisungen zum Überprüfen des Status dieser Programme nach der Momentaufnahme wiederherstellen.

Weitere Informationen finden Sie unter [Architektur virtualisierter Domänencontroller die sichere Wiederherstellung](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).

## <a name="virtualized_dc_cloning"></a>Klonen virtualisierter Domänencontroller
Ab Windows Server 2012, können Administratoren einfach und sicher replikatsdomänencontroller bereitstellen ein vorhandenen virtuellen Domänencontrollers kopieren. In einer virtuellen Umgebung müssen Administratoren nicht mehr wiederholt Bereitstellen eines Images für Server mit Hilfe von sysprep.exe vorbereitet, den Server zu einem Domänencontroller heraufstufen, und schließen Sie zusätzliche konfigurationsanforderungen für die Bereitstellung von jedem Replikat-Domänencontroller.

> [!NOTE]
> Administratoren müssen vorhandene Prozessen zum Bereitstellen von des ersten Domänencontrollers in einer Domäne, z. B. die Verwendung einer sysprep.exe, den Server zu einem Domänencontroller heraufstufen und schließen Sie alle zusätzlichen konfigurationsanforderungen Vorbereiten einer Server virtuellen Festplatte (VHD) folgen. Verwenden Sie die aktuelle serversicherung in einem notfallwiederherstellungs-Szenario den ersten Domänencontroller in einer Domäne wiederherstellen.

### <a name="scenarios-that-benefit-from-virtual-domain-controller-cloning"></a>Szenarien, die vom Klonen virtueller Domänencontroller profitieren

-   Schnelle Bereitstellung zusätzlicher Domänencontroller in einer neuen Domäne

-   Schnelle Wiederherstellung der Geschäftskontinuität während der Wiederherstellung durch Wiederherstellen von AD DS-Kapazität mittels schneller Bereitstellung von Domänencontrollern durch Klonen

-   Optimieren Sie privater cloudbereitstellungen mittels eine flexible Bereitstellung von Domänencontrollern auf eine höhere zu erfüllen

-   Schnelle Bereitstellung von testumgebungen, die das Bereitstellen und Testen der neuen Features und Funktionen vor dem Produktionsrollout

-   Schnelles erfüllen höherer kapazitätsanforderungen in Zweigstellen durch Klonen vorhandener Domänencontroller in Filialen

Wenn Sie eine große Anzahl von Domänencontrollern schnell bereitstellen, weiterhin Ihren vorhandenen Verfahren zum Überprüfen der Integritäts jedes Domänencontrollers nach Abschluss der Installation. Bereitstellen Sie Domänencontroller in Batches angemessener Größe bereit, damit Sie deren Integrität nach jeder abgeschlossenen Installation eines Abschluss überprüfen können. Die empfohlene Batchgröße ist 10. Weitere Informationen finden Sie unter [Schritte zum Bereitstellen eines geklonten virtualisierten Domänencontrollers](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc).

### <a name="clear-separation-of-responsibilities"></a>Klare verantwortungsteilung
Die Autorisierung zum Klonen virtualisierter Domänencontroller wird von der AD DS-Administrator gesteuert. Damit hypervisoradministratoren zusätzliche Domänencontroller durch Kopieren virtueller Domänencontroller bereitstellen muss der AD DS-Administrator auswählen und einen Domänencontroller zu autorisieren, und führen Sie die vorbereitenden Schritte aus, damit es als Quelle für das Klonen.

Mit der Bereitstellung virtueller Computer in der Regel unter den Geltungsbereich des Administrators Hypervisor, können hypervisoradministratoren Replikat virtuellen domänencontrollercomputern bereitstellen, indem virtualisierte Domänencontroller, die für das Klonen von der AD DS-Administrator vorbereitet und autorisiert werden kopiert.

> [!WARNING]
> Alle Personen dürfen die Hypervisors, der einen virtuellen Domänencontroller hostet Hoch vertrauenswürdig und in der Umgebung überwacht.

### <a name="how-does-virtual-domain-controller-cloning-work"></a>Wie funktioniert das Klonen eines virtuellen Domänencontrollers?
Der klonprozess beinhaltet das Erstellen einer Kopie der virtuellen Festplatte einer vorhandenen virtuellen Domänencontrollers (oder für komplexere Konfigurationen, die VM-Domänencontroller), für das Klonen in AD DS, und erstellen eine Konfigurationsdatei zum Klonen autorisieren. Dies reduziert die Anzahl der Schritte und die benötigte Zeit Bereitstellen eines virtuellen Replikatsdomänencontrollers Beseitigung ansonsten wiederholt auszuführende Bereitstellungsaufgaben.

Der geklonte Domänencontroller verwendet die folgenden Kriterien ermitteln, ob es sich um eine Kopie eines anderen Domänencontrollers ist:

1.  Der Wert der VM-Generations-ID angegeben, von der virtuellen Maschine unterscheidet sich der Wert der in der DIT gespeicherten VM-Generations-ID zur Verfügung.

    > [!NOTE]
    > Die Hypervisor-Plattform muss die VM-Generations-ID unterstützen (Windows Server 2012 Hyper-V unterstützt VM-Generations-ID).

2.  Vorhandensein einer Datei %% amp;quot;dccloneconfig.XML%%amp;quot; in einem der folgenden Speicherorte:

    -   Das Verzeichnis, in dem die DIT befindet

    -   %windir%\ntds

    -   Im Stammverzeichnis eines Wechselmedienlaufwerks

Die Kriterien erfüllt, wird es durch den Prozess zum Bereitstellen von sich selbst als einen Replikatdomänencontroller klonen.

Der geklonte Domänencontroller verwendet den Sicherheitskontext des Quell-Domänencontroller (der Domänencontroller, dessen Kopie er darstellt), wenden Sie sich an den Windows Server 2012 primären Domänencontroller (PDC) Emulator Inhaber der Betriebsmasterfunktion (auch als flexible einfache Mastervorgänge oder FSMO-Funktion). Der PDC-Emulator muss Windows Server 2012 ausgeführt werden, aber es muss nicht auf einem Hypervisor ausgeführt werden.

> [!NOTE]
> Wenn Sie eine schemaerweiterung mit Attributen, die auf den Quelldomänencontroller verweisen und das Attribut auf einem der kopierten Objekte (Computerobjekt, NTDS-Einstellungsobjekt) zum Erstellen des Klons ist, dieses Attribut nicht kopiert oder aktualisiert, um den geklonten Domänencontroller verweisen.

Nachdem Sie sichergestellt, dass der anfordernde Domänencontroller für das Klonen autorisiert ist, der PDC-Emulator eine neue Computeridentität neues Konto, SID, Namen und Kennwort, die Computer als einen Replikatdomänencontroller identifiziert erstellen und senden diese Informationen an den Klon zurück. Der geklonte Domänencontroller bereitet dann die AD DS-Datenbankdateien, sondern als Replikat dienen soll, und er bereinigt auch den Zustand des Computers.

Weitere Informationen finden Sie unter [virtualisierte Domänencontroller, die Architektur für das Klonen](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch).

### <a name="cloning-components"></a>Das Klonen Komponenten
Die klonkomponenten umfassen neue Cmdlets im Active Directory-Modul für Windows PowerShell und dazugehörige XML-Dateien:

-   **New-ADDCCloneConfigFile** "dieses Cmdlet erstellt, und platziert dccloneconfig.XML-Datei am richtigen Speicherort um sicherzustellen, dass sie zum Auslösen des Klonens verfügbar. Es führt auch voraussetzungsprüfungen um erfolgreiches Klonen sicherzustellen. Es ist in Active Directory-Modul für Windows PowerShell enthalten. Kann lokal auf einem virtualisierten Domänencontroller, der zum Klonen vorbereitet wird ausgeführt, oder Sie können dafür Remote mit der offline-Option. Sie können die Einstellungen für den geklonten Domänencontroller, z. B. Name, Website und IP-Adresse angeben.

    Die voraussetzungsprüfungen, die ausgeführt werden:

    > [!NOTE]
    > Werden keine voraussetzungsprüfungen durchgeführt, wenn die "offline-Option wird verwendet. Weitere Informationen finden Sie unter [Running New-ADDCCloneConfigFile im Offlinemodus](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode).

    -   Der vorbereitete DC ist für das Klonen autorisiert (ist ein Mitglied der **Klonbare Domänencontroller** Gruppe)

    -   Der PDC-Emulator ausgeführt wird, Windows Server 2012.

    -   Programme oder Dienste aufgeführt, Ausführen von **Get-ADDCCloningExcludedApplicationList** in CustomDCCloneAllowList.xml (am Ende der Liste mit klonkomponenten ausführlicher erläutert) enthalten sind.

-   **DCCloneConfig.xml** "erfolgreich Klonen ein virtualisierten Domänencontrollers, diese Datei muss vorhanden sein, in dem Verzeichnis, in dem die DIT befindet, *%windir%\NTDS*, oder im Stammverzeichnis eines Wechselmedienlaufwerks. Außer als ein Auslöser verwendet wird, um zu erkennen und Initiieren eines Klonvorgangs, bietet es auch die Möglichkeit, Konfigurationseinstellungen für den geklonten Domänencontroller festgelegt.

    Das Schema und eine Beispieldatei für die Datei DCCloneConfig.xml befinden sich auf alle Windows Server 2012-Computer an:

    -   %windir%\system32\DCCloneConfigSchema.xsd

    -   %windir%\system32\SampleDCCloneConfig.Xml

    Es wird empfohlen, dass Sie das Cmdlet "New-ADDCCloneConfigFile" verwenden, um die Datei DCCloneConfig.xml zu erstellen. Sie könnten zwar auch auch die Schemadatei mit einem XML-fähigen Editor zum Erstellen dieser Datei, erhöht die Manuelles Editieren der Datei die Wahrscheinlichkeit von Fehlern. Wenn Sie die Datei bearbeiten, müssen sie mithilfe von XML-fähigen Editor, z. B. Visual Studio ausgeführt werden [XML Notepad](https://www.microsoft.com/download/details.aspx?displaylang=en&id=7973), oder Drittanbieter-Anwendungen (verwenden Sie nicht Editor).

-   **Get-ADDCCloningExcludedApplicationList** "dieses Cmdlet wird ausgeführt, auf dem Quelldomänencontroller vor dem Beginn des klonprozesses, um festzustellen, welche Dienste oder installierte Programme nicht auf der unterstützten Standardliste %% amp;quot;defaultdccloneallowlist.XML%%amp;quot; sind oder einen benutzerdefinierten Aufnahmeliste Liste mit dem Namen %% amp;quot;customdccloneallowlist.XML%%amp;quot und somit nicht Auswirkungen des Klonens ausgewertet.

    Dieses Cmdlet durchsucht den Quelldomänencontroller für Dienste im Dienste-Manager, und der installierten Programme aufgeführt, unter **HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall** , die nicht in der Standardliste (%% amp;quot;defaultdccloneallowlist.XML%%amp;quot;) angegeben oder, sofern angegeben ist, die benutzerdefinierten Aufnahmeliste (%% amp;quot;customdccloneallowlist.XML%%amp;quot). Die Liste der Anwendungen und Dienste, die durch Ausführen des Cmdlets zurückgegeben wird, ist der Unterschied zwischen was bereits bereitgestellt wurde in DefaultDCCloneAllowList.xml oder die Datei CustomDCCloneAllowList.xml und die Liste, die zur Laufzeit erstellt wurde, basierend auf was auf dem Quelldomänencontroller installiert ist. Die Dienste und Programme Ausgabe von Get-ADDCCloningExcludedApplicationList kann zur Datei CustomDCCloneAllowList.xml hinzugefügt werden, wenn Sie feststellen, dass die Dienste oder Programme sicher geklont werden können. Um festzustellen, ob ein Dienst oder ein installiertes Programm sicher geklont werden kann, Werten Sie die folgenden Bedingungen:

    -   Ist der Dienst oder das installierte Programm durch die Computeridentität, z. B. Name, SID, Kennwort und So weiter beeinträchtigt?

    -   Wird den Dienst oder installiert Anwendung Store alle Zustände lokal auf dem Computer, der die Funktionen auf dem Klon beeinflussen könnten?

    Sie müssen gemeinsam mit dem Softwareanbieter der Anwendung bestimmen, ob der Dienst oder das Programm sicher geklont werden kann.

    > [!NOTE]
    > Überprüfen Sie vor der Bereitstellung zusätzlicher Dienste oder Programme in der Datei %% amp;quot;customdccloneallowlist.XML%%amp;quot; ob Sie die erforderliche Lizenz zum Kopieren der Software auf diesem virtuellen Computer verfügen.

    Wenn die Anwendungen nicht klonbar, entfernen sie aus dem Quelldomänencontroller vor dem Erstellen der Klon-Medium. Wenn eine Anwendung in der Cmdlet-Ausgabe angezeigt, aber nicht in der Datei %% amp;quot;customdccloneallowlist.XML%%amp;quot; enthalten ist, schlägt das Klonen fehl. Für das Klonen erfolgreich ist, sollte die Cmdlet-Ausgabe keine Dienste oder Programme aufgelistet. Anders ausgedrückt, sollte eine Anwendung in der Datei %% amp;quot;customdccloneallowlist.XML%%amp;quot; enthalten oder vom Quelldomänencontroller entfernt.

    Die folgende Tabelle erläutert die Optionen für die Ausführung von Get-ADDCCloningExcludedApplicationList.

    |||
    |-|-|
    |Argument|Erläuterung|
    |*<no argument specified>*|Zeigt eine Liste der Dienste oder Programme auf der Konsole, die für das Klonen nicht berücksichtigt wurden. Wenn bereits eine CustomDCCloneAllowList.XML in einem der zulässigen Speicherorte vorhanden ist, wird die Datei zeigt die verbleibenden Dienste und Programme (u. u. keine, wenn die Listen übereinstimmen) verwendet.|
    |– GenerateXml|Erstellt die Datei %% amp;quot;customdccloneallowlist.XML%%amp;quot; mit den Diensten und Programmen auf der Konsole aufgeführt.|
    |-Force|Überschreibt eine vorhandene %% amp;quot;customdccloneallowlist.XML%%amp;quot;-Datei.|
    |-Pfad|Der Ordnerpfad CustomDCCloneAllowList.XML erstellen.|

-   **DefaultDCCloneAllowList.xml** "Diese Datei ist standardmäßig auf alle Windows Server 2012 Domain Controller In die *%windir%\system32*. Es listet die Dienste und Programme, die standardmäßig sicher geklont werden können. Sie müssen den Speicherort oder den Inhalt dieser Datei nicht ändern oder das Klonen fehl.

-   **CustomDCCloneAllowList.xml** "besitzen Sie Dienste oder installierte Programme, die auf dem Quell-Domänencontroller befinden, die in der Datei %% amp;quot;defaultdccloneallowlist.XML%%amp;quot; aufgeführten sind, diese Dienste und Programme in enthalten sein müssen diese Datei. Nach der Dienste oder installierte Programme, die nicht aufgeführt sind die in der Datei %% amp;quot;defaultdccloneallowlist.XML%%amp;quot; führen Sie die **Get-ADDCCloningExcludedApplicationList** Cmdlet. Verwenden Sie die **"GenerateXml** Argument, um die XML-Datei zu generieren.

    Der Klonvorgang überprüft die folgenden Speicherorten in der Reihenfolge nach dieser Datei und die erste XML-Datei gefunden, unabhängig von den anderen Inhalt des Ordners verwendet:

    1.  Die folgenden Registrierungsschlüssel:

        ```
        HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters
        AllowListFolder (REG_SZ)
        ```

    2.  DSA-Arbeitsverzeichnis

    3.  %systemroot%\NTDS

    4.  Lese-/Schreib-Wechselmedien Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stammverzeichnis des Laufwerks

### <a name="deployment-scenarios"></a>Szenarien für die Bereitstellung
Die folgenden Bereitstellungsszenarios werden für das Klonen des virtuellen Domänencontrollers unterstützt:

-   Bereitstellen eines geklonten Domänencontrollers durch Erstellen einer Kopie der Datei von einem Quelldomänencontroller virtuelle Festplatte (Vhd).

-   Bereitstellen eines geklonten Domänencontrollers durch Kopieren des virtuellen Computers des Quelldomänencontrollers mithilfe der Export-/Importsemantik vom Hypervisor.

> [!NOTE]
> Die Schritte im Abschnitt [Schritte zum Bereitstellen eines geklonten virtualisierten Domänencontrollers](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc) veranschaulichen das Kopieren eines virtuellen Computers mithilfe der Export-/Importfeatures von Windows Server 2012 Hyper-V.

## <a name="steps_deploy_vdc"></a>Schritte zum Bereitstellen eines geklonten virtualisierten Domänencontrollers

-   [Erforderliche Komponenten](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#prerequisites)

-   [Schritt 1: Erteilen Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk4_grant_source)

-   [Schritt 2: Ausführen von Get-ADDCCloningExcludedApplicationList-cmdlet](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet)

-   [Schritt 3: Ausführen von New-ADDCCloneConfigFile](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk5_create_insert_dccloneconfig)

-   [Schritt 4: Exportieren Sie und importieren Sie der virtuellen Maschine von der Quell-Domänencontroller](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk7_export_import_vm_sourcedc)

### <a name="prerequisites"></a>Erforderliche Komponenten

-   Um die Schritte in den folgenden Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein, oder die entsprechenden Berechtigungen zugewiesen haben sie.

-   Windows PowerShell-Befehle in diesem Handbuch verwendeten müssen über ein Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt werden. Zu diesem Zweck mit der rechten Maustaste die **Windows PowerShell** Symbol, und klicken Sie dann auf **als Administrator ausführen**.

-   Ein Windows Server 2012-Server mit der Hyper-V-Serverrolle installiert (**HyperV1**).

-   Einen zweiten Windows Server 2012-Server mit der Hyper-V-Serverrolle installiert (**HyperV2**).

    > [!NOTE]
    > -   Wenn Sie einen anderen Hypervisor verwenden, wenden Sie den Anbieter, um sicherzustellen, dass der Hypervisor VM-Generations-ID unterstützt. Wenn der Hypervisor die VM-Generations-ID nicht unterstützt, und Sie haben eine dccloneconfig.XML-Datei angegeben, wird die neue virtuelle Maschine in Directory Services-Wiederherstellungsmodus (DSRM) gestartet.
    > -   Dieses Handbuch empfiehlt und enthält zwei verschiedene Hyper-V-Hosts, welche wird verhindert, einen einzigen Fehlerpunkt dass mit Anweisungen, um die Verfügbarkeit des AD DS-Diensts zu erhöhen. Allerdings benötigen Sie keine zwei Hyper-V-Hosts zum Klonen virtueller Domänencontroller ausführen.
    > -   Sie müssen ein Mitglied der Gruppe "Administratoren" auf jedem Hyper-V-Server (**HyperV1** und **HyperV2**).
    > -   Um erfolgreich zu importieren und Exportieren von einer VHD-Datei, die mithilfe von Hyper-V, sollten die virtuellen Netzwerkswitches auf beiden Hyper-V-Hosts den gleichen Namen haben. Beispielsweise haben ein virtueller Netzwerkswitch auf **HyperV1** VNet mit dem Namen, und es muss ein virtueller Netzwerkswitch auf **HyperV2** mit dem Namen VNet.
    > -   Wenn die zwei Hyper-V-Hosts (**HyperV1** und **HyperV2**) verschiedene Prozessoren haben, fahren Sie den virtuellen Computer (**VirtualDC1**), die Sie verwenden möchten, exportieren, mit der rechten Maustaste des virtuellen Computers aus, und klicken Sie auf **Einstellungen**, klicken Sie auf **Prozessor**, und wählen Sie unter **Prozessorkompatibilität** wählen **Migrieren zu einem physischen Computer mit einer anderen Prozessorversion** , und klicken Sie auf **OK**.

-   Einer bereitgestellten Windows Server 2012-Domänencontroller (virtualisiert oder physisch), der die PDC-Emulatorrolle hostet (**DC1**). Führen Sie den folgenden Windows PowerShell-Befehl, um zu überprüfen, ob die PDC-Emulatorrolle auf einem Windows Server 2012-Domänencontroller gehostet wird:

    ```
    Get-ADComputer (Get-ADDomainController "Discover "Service "PrimaryDC").name "Property operatingsystemversion | fl
    ```

    Der OperatingSystemVersion-Wert sollte als Version 6.2 zurückgegeben werden. Bei Bedarf können Sie die PDC-Emulatorrolle auf einen Domänencontroller übertragen, die Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [Using Ntdsutil.exe to transfer oder FSMO-Funktionen auf einem Domänencontroller](https://support.microsoft.com/kb/255504).

-   Eine bereitgestellte virtualisierte Domänencontroller einer Windows Server 2012-Gast (**VirtualDC1**), die sich in derselben Domäne wie der Windows Server 2012-Domänencontroller, der die PDC-Emulatorrolle hostet (**DC1**). Dadurch werden die für das Klonen verwendeten Quelldomänencontroller. Der virtuelle gastdomänencontroller wird auf einem Windows Server 2012 Hyper-V-Server gehostet werden (**HyperV1**).

    > [!NOTE]
    > -   Für das Klonen erfolgreich ist, der Quelldomänencontroller, mit dem Erstellen des Klons, von einem Domänencontroller nicht möglich, die seit der Erstellung der Quelle VHD Media herabgestuft wurde.
    > -   Beenden Sie den Quelldomänencontroller vor dem Kopieren des virtuellen Computers oder der virtuellen Festplatte.
    > -   Sie sollten nicht Klonen eine virtuellen Festplatte oder Wiederherstellen einen Momentaufnahme, die älter als die Tombstone-Lebensdauer (oder die Gültigkeitsdauer gelöschten Objekts, wenn die Active Directory-Papierkorb aktiviert ist). Wenn Sie eine virtuelle Festplatte eines vorhandenen Domänencontrollers kopieren, müssen Sie die VHD-Datei ist nicht älter-Wert der Tombstone-Lebensdauer (standardmäßig 60 Tage). Kopieren Sie keine virtuelle Festplatte eines aktiven Domänencontrollers Klon-Medium zu erstellen.

    Werfen Sie alle virtuellen Diskettenlaufwerks (VFD) der Quelle vorhanden sind. Dies kann zu freigabeproblemen führen, bei dem Versuch, den neuen virtuellen Computer importieren.

    Nur Windows Server 2012-Domänencontroller auf einem VM-Generations-ID-Hypervisor gehostet können als Quelle für das Klonen verwendet werden. Die Windows Server 2012 verwendeten Quelldomänencontroller für das Klonen sollte in einem fehlerfreien Zustand. Bestimmen Sie den Status der Quelldomänencontroller ausgeführt [Dcdiag](https://technet.microsoft.com/library/cc731968(WS.10).aspx). Um ein besseres Verständnis der von Dcdiag zurückgegebenen Ausgabe zu erhalten, finden Sie unter [tatsächlich Funktionsweise von DCDIAG... tun? ](http://blogs.technet.com/b/askds/archive/2011/03/22/what-does-dcdiag-actually-do.aspx).

    Wenn der Quelldomänencontroller ein DNS-Server ist, werden der geklonte Domänencontroller auch einen DNS-Server. Sie sollten einem DNS-Server die Hosts nur Active Directory-integrierte Zonen auswählen.

    DNS-Clienteinstellungen werden nicht geklont, sondern stattdessen in die Datei DCCloneConfig.xml-Datei angegeben sind. Wenn sie nicht angegeben sind, wird der geklonte Domänencontroller standardmäßig auf sich selbst als bevorzugter DNS-Server zeigen. Der geklonte Domänencontroller haben keine DNS-Delegierung. Der Administrator der übergeordneten DNS-Zone sollte die DNS-Delegierung für den geklonten Domänencontroller nach Bedarf aktualisiert werden.

    > [!WARNING]
    > Virtualisierungs-Sicherheitsmaßnahmen werden nicht auf Active Directory Lightweight Directory Services (AD LDS) erweitert. Aus diesem Grund sollten Sie nicht versuchen, einen AD DS-Domänencontroller zu klonen, auf dem AD LDS-Instanz gehostet wird, durch Hinzufügen von AD LDS-Instanz zu CustomDCCloneAllowList.xml. Da AD LDS nicht VM-Generations-ID-fähig ist, kann Klonen eines Domänencontrollers mit AD LDS USN-Rollback-zu-abweichungen auf die AD LDS-Konfigurationssatz führen.

    Die folgenden Serverrollen werden nicht für das Klonen unterstützt:

    -   Dynamic Host Configuration-Protokoll (DHCP)

    -   Active Directory-Zertifikatdienste (AD CS)

    -   Active Directory Lightweight Directory Services (AD LDS)

### <a name="bkmk4_grant_source"></a>Schritt 1: Erteilen Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden
In diesem Verfahren Sie erteilen dem Quelldomänencontroller die Berechtigung, geklont zu werden mithilfe von **Active Directory-Verwaltungscenter** der Quelldomänencontroller Hinzufügen der **Klonbare Domänencontroller** Gruppe.

##### <a name="to-grant-the-source-virtualized-domain-controller-the-permission-to-be-cloned"></a>So gewähren Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden

1.  Auf einem beliebigen Domänencontroller in derselben Domäne wie der zum Klonen vorbereitete Domänencontroller (**VirtualDC1**) öffnen **Active Directory Administrative Center** (ADAC), suchen Sie das virtualisierte Domänencontrollerobjekt (Domänencontroller befinden sich in der Regel unter der **Domänencontroller** Container in ADAC), mit der rechten Maustaste es, wählen Sie **zur Gruppe hinzufügen** und wählen Sie unter **Geben Sie die zu verwendenden Objektnamen ein** Typ **Klonbare Domänencontroller** , und klicken Sie dann auf **OK**.

    In diesem Schritt durchgeführte Aktualisierung der Gruppenmitgliedschaft muss zu der PDC-Emulator repliziert werden, bevor der Klonvorgang ausgeführt werden kann. Wenn die **Klonbare Domänencontroller** Gruppe gefunden wird, zu der PDC-Emulatorrolle möglicherweise nicht auf einem Domänencontroller mit Windows Server 2012 gehostet werden.

    > [!NOTE]
    > Öffnen Sie zum Öffnen von ADAC auf einem Windows Server 2012-Domänencontroller, die Windows PowerShell, und geben **dsac.exe**.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Das folgende Windows PowerShell-Cmdlet führt dieselbe Funktion wie das vorhergehende Verfahren:


    Add-ADGroupMember "Identity "CN=Cloneable Domain Controllers,CN=Users, DC=Fabrikam,DC=Com" "Member "CN=VirtualDC1,OU=Domain Controllers,DC=Fabrikam,DC=com"


### <a name="bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet"></a>Schritt 2: Ausführen von Get-ADDCCloningExcludedApplicationList-cmdlet
In diesem Verfahren führen Sie die `Get-ADDCCloningExcludedApplicationList` Cmdlet auf dem virtualisierten Quelldomänencontroller zu identifizieren, Programme oder Dienste, die nicht für das Klonen ausgewertet werden. Sie müssen das Cmdlet "Get-ADDCCloningExcludedApplicationList", bevor Sie das Cmdlet "New-ADDCCloneConfigFile" ausgeführt werden, da das Cmdlet "New-ADDCCloneConfigFile" eine ausgeschlossene Anwendung ermittelt, es keine DCCloneConfig.xml-Datei erstellt wird.

##### <a name="to-identify-applications-or-services-that-run-on-a-source-domain-controller-which-have-not-been-evaluated-for-cloning"></a>Identifizieren von Anwendungen oder Dienste, die auf einem Quelldomänencontroller ausgeführt, die nicht für das Klonen ausgewertet wurden

1.  Auf dem Quelldomänencontroller (**VirtualDC1**), klicken Sie auf **Server-Manager**, klicken Sie auf **Tools**, klicken Sie auf **Active Directory-Modul für Windows PowerShell** und geben Sie dann den folgenden Befehl:


    Get-ADDCCloningExcludedApplicationList


2.  Überprüfen Sie die Liste mit zurückgegebenen Diensten und installierten Programme, mit dem Softwarehersteller, um festzustellen, ob diese sicher geklont werden können. Wenn Anwendungen oder Dienste in der Liste sicher geklont werden können, müssen Sie sie aus dem Quelldomänencontroller entfernen, oder das Klonen fehl.

3.  Für den Satz von Diensten und installierten Programme, um sicher geklont werden, führen Sie den Befehl erneut mit dem **"GenerateXML** Switch bereitstellen, diese Dienste und Programme in der **CustomDCCloneAllowList.xml** Datei.


    Get-ADDCCloningExcludedApplicationList - GenerateXml


### <a name="bkmk5_create_insert_dccloneconfig"></a>Schritt 3: Ausführen von New-ADDCCloneConfigFile
New-ADDCCloneConfigFile auf dem Quelldomänencontroller ausgeführt, und geben Sie optional Konfigurationseinstellungen für den geklonten Domänencontroller, z. B. den Namen, IP-Adresse und DNS-Auflösung.

Geben Sie z. B. zum Erstellen eines geklonten Domänencontrollers mit dem Namen VirtualDC2 mit einer statischen IPv4-Adresse:


    New-ADDCCloneConfigFile "Static -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.255.0" -CloneComputerName "VirtualDC2" -IPv4DefaultGateway "10.0.0.3" -SiteName "REDMOND"

> [!NOTE]
> Der geklonte Domänencontroller wird am selben Standort wie der Quelldomänencontroller befinden, es sei denn, ein anderen Standort in der Datei DCCloneConfig.xml-Datei angegeben wird. Es wird empfohlen, dass Sie einen geeigneten Standort in der Datei DCCloneConfig.xml-Datei für den geklonten Domänencontroller anhand seiner IP-Adresse angeben.

Der Computername ist optional. Wenn Sie nicht angeben, wird basierend auf folgendem Algorithmus ein eindeutiger Name generiert werden:

-   Das Präfix ist die ersten 8 Zeichen des Namens des Quellcomputers Domain Controller. Beispielsweise wird der quellcomputername des Sourcecomputer% auf Präfixzeichenfolge %% SourceCo gekürzt.

-   Ein eindeutiges Namenssuffix im Format "" CL*nnnn*"wird an die Präfixzeichenfolge angehängt, in denen * nnnn * der nächste verfügbare Wert zwischen 0001-9999, die vom PDC ermittelt wird derzeit nicht verwendet wird. Z. B. wenn 0047 die nächste verfügbare Zahl im zulässigen Bereich ist, wird im vorangehenden Beispiel der Computer Name sourceco% mit, der abgeleitete Name für den geklonten Computer verwenden als SourceCo-CL0047 festgelegt.

> [!NOTE]
> Ein globaler Katalogserver (GC) ist erforderlich für das Cmdlet "New-ADDCCloneConfigFile" ordnungsgemäß funktioniert. Der Quelldomänencontroller Mitgliedschaft in der **Klonbare Domänencontroller** Gruppe muss auf dem globalen Katalogserver wiedergegeben werden. Der globale Katalogserver muss nicht auf dem Domänencontroller als PDC-Emulator sein, aber vorzugsweise sollten Sie sich am selben Standort sein. Wenn kein globaler Katalogserver nicht verfügbar ist, schlägt der Befehl fehl mit Fehler "der Server ist nicht betriebsbereit." Weitere Informationen finden Sie unter [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).

Zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone1 mit statischen IPv4-Einstellungen, und geben Sie bevorzugte und alternative WINS-Server aus, geben Sie Folgendes ein:


    New-ADDCCloneConfigFile "CloneComputerName "Clone1" "Static -IPv4Address "10.0.0.5" "IPv4DNSResolver "10.0.0.1" "IPv4SubnetMask "255.255.0.0" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


> [!NOTE]
> Wenn Sie WINS-Server angeben, müssen Sie angeben, beide **"PreferredWINSServer** und **" AlternateWINSServer**. Wenn Sie nur eines dieser Argumente angeben, schlägt fehl mit Fehler Code 0 x 80041005 beim angezeigt, in die Datei dcpromo.log klonen.

Geben Sie zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone2 mit dynamischen IPv4-Einstellungen:


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" 


> [!NOTE]
> In diesem Fall, wird ein DHCP-Server in der Umgebung, dass der Klon erreichen kann und die IP-Adresse und andere relevante Netzwerkeinstellungen zu erhalten.

Zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone2 mit dynamischen IPv4-Einstellungen, und geben Sie bevorzugte und alternative WINS-Server aus, geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" -SiteName "REDMOND" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


Um einen geklonten Domänencontroller mit dynamischen IPv6-Einstellungen zu erstellen, geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


Um einen geklonten Domänencontroller mit statischen IPv6-Einstellungen zu erstellen, geben Sie Folgendes ein:


    New-ADDCCloneConfigFile "Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


> [!NOTE]
> Wenn Sie IPv6-Einstellungen angeben, ist der einzige Unterschied zwischen den Einstellungen für statischen und dynamischen die Einbindung von **-statische** wechseln. Die Aufnahme der **-statische** Switch ist es notwendig, geben Sie mindestens eine **IPv6DNSResolver**. Die statische IPv6-Adresse wird erwartet, über die automatische Konfiguration zustandsloser Adressen (SLAAC) mit Router zugewiesenen Präfixen konfiguriert werden. Bei dynamischem IPv6 sind die DNS-Auflösungen sind optional, aber es wird erwartet, dass der Klon einen IPv6-fähigen DHCP-Server im Subnetz zum Abrufen von IPv6-Adresse und DNS-Konfigurationsinformationen erreichen kann.

#### <a name="BKMK_OfflineMode"></a>Ausführen von New-ADDCCloneConfigFile im Offlinemodus
Wenn Sie mehrere Kopien der Quelldomänencontroller-Medien, die zum Klonen vorbereitet wurden (d. h. der Quelldomänencontroller für das Klonen autorisiert ist, das Cmdlet "Get-ADDCCloningExcludedApplicationList" wurde ausgeführt usw.) und für jede Kopie des Mediums verschiedene Einstellungen angeben möchten, können Sie New-ADDCCloneConfigFile im Offlinemodus ausführen. Dies kann effizienter als das individuelle vorbereiten jedes virtuellen Computers, z. B. durch Importieren aller Kopien sein.

In diesem Fall können Domänen-Admins den Offlinedatenträger bereitstellen und Remoteserver-Verwaltungstools (RSAT) zum Ausführen des Cmdlets New-ADDCCloneConfigFile mit dem - offline-Argument verwenden, um die XML-Dateien, die werksähnliche Automatisierung mithilfe der neue Windows PowerShell-Optionen, die in Windows Server 2012 enthalten ermöglicht hinzufügen. Weitere Informationen dazu, wie Sie die Offlinedatenträgers zum Ausführen der Cmdlets New-ADDCCloneConfigFile im Offlinemodus finden Sie unter [Adding XML to the Offline System Disk](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_Offline).

Sie sollten zunächst das Cmdlet lokal ausführen, auf den Quellmedien, um sicherzustellen, dass die voraussetzungsprüfungen erfolgreich durchgeführt. Die voraussetzungsprüfungen werden nicht im Offlinemodus ausgeführt, da das Cmdlet von einem Computer ausgeführt werden kann, die nicht aus der gleichen Domäne oder von einem Computer einer Domäne angehört. Nachdem Sie das Cmdlet lokal ausführen, wird eine DCCloneConfig.xml-Datei erstellt. Sie können die Datei DCCloneConfig.xml löschen, die lokal erstellt wird, wenn Sie anschließend den Offlinemodus verwenden möchten.

Zum Erstellen eines geklonten Domänencontrollers mit dem Namen CloneDC1 im Offlinemodus am Standort REDMOND"mit statischen IPv4-Adresse, Typ:


    New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS


Zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone2 im Offlinemodus mit statischen IPv4- und IPv6-Einstellungen geben:


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS


Zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit statischen IPv4 und IPv6-Einstellungen, und geben Sie mehrere DNS-Server für die DNS-auflösungseinstellungen, geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS 


Zum Erstellen eines geklonten Domänencontrollers mit dem Namen Clone1 im Offlinemodus mit dynamischen IPv4- und IPv6-Einstellungen geben:


    New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS


Geben Sie zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit dynamischen IPv4 und IPv6-Einstellungen:


    New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS


### <a name="bkmk7_export_import_vm_sourcedc"></a>Schritt 4: Exportieren Sie und importieren Sie der virtuellen Maschine von der Quell-Domänencontroller
Exportieren Sie in diesem Verfahren der virtuellen Maschine von dem virtualisierten Quelldomänencontroller und importieren Sie dann den virtuellen Computer. Diese Aktion wird in der Domäne einen geklonter virtualisierte Domänencontroller erstellt.

Sie müssen ein Mitglied der Gruppe "Administratoren" auf jedem Hyper-V-Host sein. Wenn Sie für jeden Server unterschiedliche Anmeldeinformationen verwenden, führen Sie die Windows PowerShell-Cmdlets zum Exportieren und importieren die virtuelle Maschine in verschiedenen Windows PowerShell-Sitzungen.

Wenn auf dem Quelldomänencontroller Momentaufnahmen vorhanden sind, sollten gelöscht werden, bevor der Quelldomänencontroller exportiert wird, da der virtuelle Computer nicht importiert wird, wenn eine Momentaufnahme prozessoreinstellungen verfügt, die mit dem hyper-V-Zielhost nicht kompatibel sind. Wenn die prozessoreinstellungen zwischen den Quell- und Ziel-hyper-V-Hosts kompatibel sind, können Sie exportieren und kopieren die Quelle ohne vorheriges Löschen von Momentaufnahmen. Nach dem importieren müssen jedoch die Momentaufnahmen gelöscht werden vom geklonten virtuellen Computer vor dem Beginn.

##### <a name="to-copy-a-virtual-domain-controller-by-exporting-and-then-importing-the-virtualized-source-domain-controller"></a>Um einen virtuellen Domänencontroller durch Exportieren und importieren dann den virtualisierten Quelldomänencontroller kopieren

1.  Auf **HyperV1**, Herunterfahren der Quelldomänencontroller (**VirtualDC1**).

    ![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    Stop-VM-Namen VirtualDC1 - ComputerName HyperV1


2.  Auf **HyperV1**, löschen Sie Momentaufnahmen und exportieren Sie dann den Quelldomänencontroller (VirtualDC1) in das Verzeichnis c:\CloneDCs.

> [!NOTE]
> Sie sollten alle zugeordneten Momentaufnahmen löschen, da jedes Mal, wenn eine Momentaufnahme erstellt wird, eine neue AVHD-Datei, die erstellt wird als differenzierender Datenträger fungiert. Dies löst eine Kettenreaktion aus. Wenn Sie Momentaufnahmen erstellt haben, und legen Sie die Datei DCCLoneConfig.xml in der virtuellen Festplatte, können Sie am Ende Erstellen eines Klons von einer älteren DIT-Version oder die Konfigurationsdatei in die falsche VHD-Datei einfügen. Löschen der Momentaufnahme werden alle diese AVHDs in die virtuelle Festplatte.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***


    Get-VMSnapshot VirtualDC1 | Remove-VMSnapshot -IncludeAllChildSnapshots
    Export-VM -Name VirtualDC1 -ComputerName HyperV1 -Path c:\CloneDCs\VirtualDC1


3.  Kopieren Sie den Ordner **virtualdc1** in das Verzeichnis c:\Import **HyperV2**.

4.  Auf **HyperV2**mit **Hyper-V-Manager**, Importieren des virtuellen Computers (mit der **virtuellen Computer importieren** Assistenten **Hyper-V-Manager**) aus dem Ordner **c:\Import\virtualdc1** und löschen Sie alle verknüpften **Snapshots**.

Verwenden der **virtuellen Computer kopieren (neue eindeutige ID erstellen)** beim Importieren des virtuellen Computers die option.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Machines"
    $vm = Import-VM -Path $path.fullname -Copy -GenerateNewId
    Rename-VM $vm VirtualDC2


Zum Erstellen mehrerer geklonter Domänencontroller vom selben Quelldomänencontroller:

  -   UI: in der **virtuellen Computer importieren** -Assistenten geben Sie neue Speicherorte für **Ordner für Virtual Machine Configuration**, **momentaufnahmespeicher**, **Ordner für Smart Paging**, und ein anderes **Speicherort** für die virtuellen Festplatten für den virtuellen Computer.

  -   WindowsPowerShell: Geben Sie neue Speicherorte für die virtuelle Maschine mithilfe der folgenden Parameter für die `Import-VM` Cmdlet:

        $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Computer" Import-VM-Pfad $path.fullname-Kopie - GenerateNewId - ComputerName HyperV2 - VhdDestinationPath "Path" - SnapshotFilePath "Path" - SmartPagingFilePath "Path" - VirtualMachinePath "Pfad"


> [!NOTE]
> Erstellen mehrerer geklonter Domänencontroller gleichzeitig die empfohlene Batchgröße ist 10. Die maximale Anzahl wird eingeschränkt, indem Sie die maximale Anzahl von ausgehenden replikationsverbindungen, d. h. 16 für verteilte Datei-Replikation (DFSR) und 10 für Windows-Verwaltungsinstrumentation (File Replication Service, FRS). Sie sollten nicht mehr als die empfohlene Anzahl von geklonten Domänencontrollern gleichzeitig bereitstellen, wenn Sie die Nummer für Ihre Umgebung gründlich getestet haben.

5.  Auf **HyperV1**, starten Sie den Quelldomänencontroller (**(VirtualDC1**) wieder online zu schalten.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    Start-VM -Name VirtualDC1 -ComputerName HyperV1


6.  Auf **HyperV2**, starten Sie den virtuellen Computer (**VirtualDC2**) online als geklonten Domänencontroller in der Domäne zugänglich.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***


    Start-VM -Name VirtualDC2 -ComputerName HyperV2

> [!NOTE]
> Für das Klonen erfolgreich ist, muss der PDC-Emulator ausgeführt werden. Wenn er heruntergefahren wurde, stellen Sie sicher, dass er wieder hochgefahren und die erstsynchronisierung ausgeführt, d. h. fähig ist die PDC-Emulatorrolle enthält. Weitere Informationen finden Sie unter Microsoft [KB-Artikel 305476](https://support.microsoft.com/kb/305476).

Nach Abschluss des Klonvorgangs, vergewissern Sie sich, der Namen des geklonten Computers um sicherzustellen, dass der Klonvorgang erfolgreich war. Stellen Sie sicher, dass der virtuelle Computer nicht in Directory Services-Wiederherstellungsmodus (DSRM) gestartet wurde. Wenn Sie versuchen, anmelden und eine Fehlermeldung, dass keine Anmeldeserver verfügbar sind, versuchen Sie sich im Verzeichnisdienst-Wiederherstellungsmodus. Wenn der Domänencontroller nicht erfolgreich geklont wurde und im Verzeichnisdienst-Wiederherstellungsmodus gestartet wird, überprüfen Sie die Protokolle in der Ereignisanzeige und Dcpromo-Protokolle im Ordner "%systemroot%/debug".

Der geklonte Domänencontroller wird Mitglied der **Klonbare Domänencontroller** gruppieren, weil sie die Mitgliedschaft vom Quelldomänencontroller kopiert. Als bewährte Methode sollten Sie lassen den **Klonbare Domänencontroller** Gruppe leer, bis Sie zum Ausführen von Klonvorgängen bereit sind, und Sie Mitglieder entfernen sollten, nachdem das Klonen abgeschlossen wurden.

Wenn der Quelldomänencontroller ein Sicherungsmedium speichert, wird der geklonte Domänencontroller auch das Sicherungsmedium gespeichert. Sie können ausführen `wbadmin get versions` auf dem Sicherungsmedium auf dem geklonten Domänencontroller anzuzeigen. Ein Mitglied der Gruppe Domänen-Admins, sollte das Sicherungsmedium auf dem geklonten Domänencontroller zu verhindern, dass versehentlich wiederhergestellt löschen. Weitere Informationen zur Vorgehensweise beim Löschen einer systemstatussicherung mithilfe von wbadmin.exe finden Sie unter [Wbadmin delete Systemstatebackup](https://technet.microsoft.com/library/cc742081(v=WS.10).aspx).

## <a name="troubleshooting"></a>Problembehandlung
Wenn der geklonte Domänencontroller (**VirtualDC2**) in Directory Services-Wiederherstellungsmodus (DSRM) gestartet, es gibt keine zurück zum normalen Modus auf den nächsten Neustart. Um zu einem Domänencontroller anzumelden, der im Verzeichnisdienst-Wiederherstellungsmodus gestartet wird, verwenden Sie **. \Administrator** , und geben Sie das DSRM-Kennwort.

Korrigieren Sie die Ursache des Fehlers beim Klonen, und stellen Sie sicher, dass die Datei dcpromo.log nicht darauf hinweist, dass der Klonvorgang nicht wiederholt werden kann nicht. Wenn der Klonvorgang nicht wiederholt werden kann, verwerfen Sie das Medium sicher. Wenn der Klonvorgang wiederholt werden kann, müssen Sie den DS-Wiederherstellungsmodus löschen, um wiederholen Sie den Klonvorgang erneut auszuführen.

1.  Öffnen von Windows Server 2012 mit einem Befehl mit erhöhten Rechten, (rechts klicken Sie auf Windows Server 2012, und wählen Sie als Administrator ausführen), und geben Sie dann **Msconfig**.

2.  Auf der **Start** Registerkarte **Startoptionen**Kontrollkästchen **Abgesicherter Start** (mit der Option bereits ausgewählt **Active Directory-Reparatur aktiviert**).

3.  Klicken Sie auf **OK** und neu starten, wenn Sie aufgefordert werden.

Weitere Informationen zur Problembehandlung bei virtualisierte Domänencontroller, finden Sie unter [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).


