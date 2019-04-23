---
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
title: Einführung in die Virtualisierung der Active Directory-Domänendienste (Active Directory Domain Services, ADDS) (Ebene100)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b818ba5a58db38bdb3c0f630a8d9d2daa1494403
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878091"
---
# <a name="introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100"></a>Einführung in die Virtualisierung der Active Directory-Domänendienste (Active Directory Domain Services, ADDS) (Ebene100)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

An der Virtualisierung von AD DS (Active Directory Domain Services)-Umgebungen wird schon seit einigen Jahren gearbeitet. Ab Windows Server 2012 bietet AD DS mehr Unterstützung für das Virtualisieren von Domänencontrollern, indem virtualisierungssichere Funktionen eingeführt.

## <a name="safe-virtualization-of-domain-controllers"></a>Sichere Virtualisierung von Domänencontrollern

Virtuelle Umgebungen bedeuten individuelle Herausforderungen für verteilte Arbeitslasten, die von einem logischen taktbasierten Replikationsschema abhängen. Die AD DS-Replikation verwendet beispielsweise einen monoton steigenden Wert (als %%amp;quot;USN%%amp;quot; oder %%amp;quot;Updatesequenznummer%%amp;quot;), der Transaktionen auf jedem Domänencontroller zugewiesen ist. Jeder Domänencontroller-Datenbank-Instanz erhält auch eine Identität, einen InvocationID genannt. Die Aufrufkennung eines Domänencontrollers dient in Verbindung mit der USN als eindeutiger Bezeichner, der jeder Schreibtransaktion auf jedem Domänencontroller zugeordnet ist, und innerhalb der Gesamtstruktur eindeutig sein muss.

Die AD DS-Replikation verwendet Aufrufkennungen und USNs auf jedem Domänencontroller, um zu bestimmen, welche Änderungen auf anderen Domänencontrollern repliziert werden müssen. Wenn ein Domänencontroller ein außerhalb seines Wirkungsbereichs die Rollback wird und eine USN für eine vollkommen andere Transaktion wiederverwendet wird, wird die Replikation nicht zusammengeführt, da andere Domänencontroller davon ausgehen werden, dass sie die Updates bereits empfangen haben der wiederverwendeten USN im Kontext der Aufrufkennung zugeordnet ist.

Die folgende Abbildung veranschaulicht z. B. die Abfolge von Ereignissen in Windows Server 2008 R2 und älteren Betriebssystemen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In dieser Abbildung wird das USN-Rollback auf VDC2, wenn ein Replikationspartner feststellt, dass VDC2 einen aktualitäts-USN-Wert gesendet hat, der zuvor vom Replikationspartner, aufgetreten ist, gibt an, dass die Datenbank von VDC2 des Rollback hat nicht ordnungsgemäß.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

Ein virtuellen Computer (VM) erleichtert hypervisoradministratoren einer Domäne des Controllers USNs (die logische Uhr), ein Rollback z. B. eine Momentaufnahme außerhalb seines Wirkungsbereichs der angewendet. Weitere Informationen zur USN und zum USN-Rollback, einschließlich weiterer Abbildungen zur Veranschaulichung unerkannter Instanzen eines USN-Rollbacks, finden Sie unter [USN and USN Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback).

Ab Windows Server 2012, AD DS virtuelle Domänencontroller gehostet, die auf Hypervisor-Plattformen, die Bezeichner mit VM-Generations-ID ermitteln und bereitstellen, erforderlichen Sicherheitsmaßnahmen auf die AD DS-Umgebung zu schützen, wenn der virtuelle Computer ein Rollback ausgeführt wird in der Zeit von der Anwendung von einer VM-Momentaufnahme. Der VM-Generations-ID-Entwurf verwendet einen unabhängigen Mechanismus des Hypervisoranbieters, um diesen Bezeichner im Adressbereich des virtuellen Gastcomputers bereitzustellen, damit die sichere Virtualisierung ständig von jedem Hypervisor verfügbar ist, der VM-Generations-ID unterstützt. Dieser Bezeichner kann von Diensten und Anwendungen verwendet werden, die innerhalb des virtuellen Computers ausgeführt werden, um zu ermitteln, ob für einen virtuellen Computer ein Rollback durchgeführt wurde.

### <a name="BKMK_HowSafeguardsWork"></a>Wie funktionieren diese Virtualisierungs-Sicherheitsmaßnahmen?
Während der Installation des Domänencontrollers speichert AD DS den Bezeichner VM-Generations-ID anfänglich als Teil des MsDS-GenerationID-Attributs auf die Domänencontroller Computerobjekt in der Datenbank (häufig als Verzeichnisinformationsstruktur oder DIT bezeichnet). Die VM-Generations-ID wird von einem Windows-Treiber innerhalb des virtuellen Computers unabhängig nachverfolgt.

Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der VM-Generations-ID aus dem Treiber des virtuellen Computers mit einem Wert in der DIT verglichen.

Unterscheiden sich die beiden Werte, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, um das erneute Verwenden der USN zu verhindern. Sind die Werte identisch, wird die Transaktion normal ausgeführt.

AD DS vergleicht auch bei jedem Neustart des Domänencontrollers den aktuellen Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der DIT. Unterscheiden sich die Werte, wird die Aufrufkennung zurückgesetzt, der RID-Pool verworfen und die DIT mit dem neuen Wert aktualisiert. Außerdem wird der Ordner %%amp;quot;SYSVOL%%amp;quot; nicht autorisierend synchronisiert, um die sichere Wiederherstellung abzuschließen. Dadurch können Schutzvorrichtungen die Anwendung von Momentaufnahmes auf heruntergefahrenen virtuellen Computern erweitern. Diese in Windows Server 2012 eingeführten Schutzvorrichtungen ermöglichen AD DS-Administratoren zum Nutzen der individuellen Vorteile der Bereitstellung und Verwaltung von Domänencontrollern in einer virtualisierten Umgebung.

Die folgende Abbildung zeigt, wie virtualisierungsschutzvorrichtungen angewendet werden, wenn dasselbe USN-Rollback auf einem virtualisierten Domänencontroller erkannt wird, die Windows Server 2012 auf einem Hypervisor ausgeführt wird, die VM-Generations-ID unterstützt.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

In diesem Fall werden Virtualisierungsschutzvorrichtungen ausgelöst, wenn der Hypervisor eine Änderung am Wert der VM-Generations-ID erkennt. Dabei wird auch die Aufrufkennung des virtualisierten Domänencontrollers (im vorhergehenden Beispiel von A zu B) zurückgesetzt und der auf dem virtuellen Computer gespeicherte Wert der VM-Generations-ID so aktualisiert, dass er mit dem neuen vom Hypervisor gespeicherten Wert (G2) übereinstimmt. Mit den Schutzvorrichtungen wird sichergestellt, dass die Replikation für beide Domänencontroller zusammengeführt wird.

In Windows Server 2012 AD DS Schutzvorrichtungen auf virtuellen Domänencontrollern, die auf VM-Generations-ID-fähigen Hypervisoren gehostet werden soll, und stellt sicher, dass die versehentliche Anwendung von Momentaufnahmen oder ähnlicher Hypervisor-fähigen Mechanismen, die ein Rollback einer virtuellen könnten Status des Computers ist die AD DS-Umgebung nicht unterbrochen werden (durch Verhindern von Replikationsproblemen wie z. B. einer USN-Blase oder veralteten Objekten). Das Wiederherstellen eines Domänencontrollers mittels Anwendung eines Momentaufnahmes eines virtuellen Computers wird jedoch nicht als Alternativmechanismus zum Sichern eines Domänencontrollers empfohlen. Es wird empfohlen, weiterhin die Windows Server-Sicherung oder andere VSS Writer-basierte Sicherungslösungen zu verwenden.

> [!CAUTION]
> Wenn ein Domänencontroller in einer produktionsumgebung versehentlich mit einer Momentaufnahme wiederhergestellt wird, wird empfohlen, dass Sie die Hersteller für Anwendungen und Dienste, die auf diesem virtuellen Computer, um Anweisungen zum Überprüfen des Status dieser Programme nach gehostet werden. Wenden Sie sich an Wiederherstellung einer Momentaufnahme.

Weitere Informationen finden Sie unter [Virtualized domain controller safe restore architecture](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).

## <a name="virtualized_dc_cloning"></a>Klonen von virtualisierten Domänencontrollern
Ab Windows Server 2012, können Administratoren einfach und sicher replikatsdomänencontroller bereitstellen durch Kopieren eines vorhandenen virtuellen Domänencontrollers. In einer virtuellen Umgebung müssen Administratoren nicht mehr jedesmal ein mit %%amp;quot;sysprep.exe%%amp;quot; vorbereitetes Serverabbild bereitstellen, den Server zu einem Domänencontroller heraufstufen und zusätzliche Konfigurationsanforderungen erfüllen, um einen Replikatsdomänencontroller bereitzustellen.

> [!NOTE]
> Administratoren müssen vorhandenen Prozessen folgen, um den ersten Domänencontroller in einer Domäne bereitzustellen, z. B. Vorbereiten einer virtuellen Serverfestplatte mithilfe von %%amp;quot;sysprep.exe%%amp;quot;, Heraufstufen des Servers zu einem Domänencontroller und Erfüllen zusätzlicher Konfigurationsanforderungen. In einem Notfallwiederherstellungs-Szenario verwenden Sie die aktuelle Serversicherung zum Wiederherstellen des ersten Domänencontrollers in einer Domäne.

### <a name="scenarios-that-benefit-from-virtual-domain-controller-cloning"></a>Szenarien, die vom Klonen virtueller Domänencontroller profitieren

-   Schnelle Bereitstellung zusätzlicher Domänencontroller in einer neuen Domäne

-   Schnelle Wiederherstellung der Geschäftskontinuität bei einer Notfallwiederherstellung durch Wiederherstellung der AD DS-Kapazität mittels schneller Bereitstellung von Domänencontrollern durch Klonen

-   Optimieren privater Cloudbereitstellungen mittels flexibler Bereitstellung von Domänencontrollern, um höhere Skalierungsanforderungen zu erfüllen

-   Schnelle Bereitstellung von Testumgebungen, um das Bereitstellen und Testen neuer Features und Funktionen vor dem Produktionsrollout zu ermöglichen

-   Schnelles Erfüllen höherer Kapazitätsanforderungen in Zweigstellen durch Klonen vorhandener Domänencontroller in Zweigstellen

Folgen Sie beim schnellen Bereitstellen einer großen Anzahl von Domänencontrollern weiterhin Ihren vorhandenen Verfahren zum Überprüfen der Integrität jedes Domänencontrollers nach Abschluss der Installation. Stellen Sie Domänencontroller in Batches angemessener Größe bereit, damit Sie deren Integrität nach jeder abgeschlossenen Installation eines Batches überprüfen können. Die empfohlene Batchgröße ist 10. Weitere Informationen finden Sie unter [Steps for deploying a clone virtualized domain controller](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc).

### <a name="clear-separation-of-responsibilities"></a>Klare Verantwortungsteilung
Die Autorisierung zum Klonen virtualisierter Domänencontroller wird vom AD DS-Administrator gesteuert. Damit Hypervisoradministratoren zusätzliche Domänencontroller durch Kopieren virtueller Domänencontroller bereitstellen können, muss der AD DS-Administrator einen Domänencontroller auswählen, autorisieren und anschließend vorbereitende Schritte für die Aktivierung des Controllers als Quelle zum Klonen ausführen.

Da der virtuelle Computer in der Regel im Geltungsbereich des Hypervisoradministrators bereitgestellt wird, können Hypervisoradministratoren virtuelle Replikatsdomänencontroller bereitstellen, indem virtualisierte Domänencontroller kopiert werden, die zum Klonen durch den AD DS-Administrator autorisiert und vorbereitet sind.

> [!WARNING]
> Jeder, der als Administrator des Hypervisors zugelassen ist, der einen virtuellen Domänencontroller hostet, muss in der Umgebung sehr vertrauenswürdig sein und überwacht werden.

### <a name="how-does-virtual-domain-controller-cloning-work"></a>Wie funktioniert das Klonen eines virtuellen Domänencontrollers?
Der klonprozess beinhaltet eine Kopie eines vorhandenen virtuellen Domänencontrollers des VHD (oder für komplexere Konfigurationen, der den virtuellen Domänencontrollercomputer), für das Klonen in AD DS, und erstellen eine Konfigurationsdatei zum Klonen autorisieren. Dadurch werden die Anzahl der Schritte und die benötigte Zeit für das Bereitstellen eines virtuellen Replikatsdomänencontrollers reduziert, indem ansonsten wiederholt auszuführende Bereitstellungsaufgaben eliminiert werden.

Der geklonte Domänencontroller stellt anhand folgender Kriterien fest, dass er eine Kopie eines anderen Domänencontrollers ist:

1.  Der vom virtuellen Computer bereitgestellte Wert der VM-Generations-ID unterscheidet sich vom Wert der in der DIT gespeicherten VM-Generations-ID.

    > [!NOTE]
    > Die hypervisorplattform muss die VM-Generations-ID unterstützen (Windows Server 2012 Hyper-V unterstützt VM-Generations-ID).

2.  Die Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; muss an einem der folgenden Speicherorte vorhanden sein:

    -   Das Verzeichnis, in dem sich die DIT befindet

    -   %windir%\NTDS

    -   Der Stamm eines Wechselmedienlaufwerks

Sobald die Kriterien erfüllt sind, durchläuft der Domänencontroller den Klonprozess, um sich selbst als Replikatsdomänencontroller bereitzustellen.

Der geklonte Domänencontroller verwendet den Sicherheitskontext des Quelldomänencontrollers (der Domänencontroller, dessen Kopie er darstellt), die Windows Server 2012 primären Domänencontroller (PDC) Emulator Inhaber der Betriebsmasterfunktion (auch bekannt als kontaktieren flexible einfache Mastervorgänge oder FSMO-Funktion). Der PDC-Emulator muss Windows Server 2012 ausgeführt werden, aber es muss nicht auf einem Hypervisor ausgeführt werden.

> [!NOTE]
> Wenn Sie eine Schemaerweiterung mit Attributen haben, die auf den Quelldomänencontroller verweisen, und das Attribut sich auf einem der kopierten Objekte (Computerobjekt, NTDS-Einstellungsobjekt) befindet, um den Klon zu erstellen, wird dieses Attribut nicht kopiert oder so aktualisiert, dass es auf den geklonten Domänencontroller verweist.

Nach dem Überprüfen, ob der anfordernde Domänencontroller für das Klonen autorisiert ist, erstellt der PDC-Emulator eine neue Computeridentität mit neuem Konto sowie SID, Namen und Kennwort, die den Computer als Replikatsdomänencontroller identifizieren, und sendet diese Informationen an den Klon zurück. Der geklonte Domänencontroller bereitet dann die AD DS-Datenbankdateien vor, die als Replikat dienen sollen, und bereinigt auch den Status des Computers.

Weitere Informationen finden Sie unter [Sichere Klonarchitektur für virtualisierte Domänencontroller](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch).

### <a name="cloning-components"></a>Klonkomponenten
Die Klonkomponenten umfassen neue Cmdlets im Active Directory-Modul für Windows PowerShell und dazugehörige XML-Dateien:

-   **New-ADDCCloneConfigFile** "mit diesem Cmdlet erstellt und platziert dccloneconfig.XML-Datei am richtigen Speicherort, um sicherzustellen, dass er für das Auslösen des Klonens verfügbar. Zudem werden Voraussetzungsprüfungen durchgeführt, um ein erfolgreiches Klonen sicherzustellen. Das Cmdlet ist im Active Directory-Modul für Windows PowerShell enthalten. Sie können es lokal auf einem virtualisierten Domänencontroller ausführen, der zum Klonen vorbereitet ist, oder Sie können es mithilfe der Option %%amp;quot;-offline%%amp;quot; remote ausführen. Sie können Einstellungen für die den geklonten Domänencontroller festlegen, z. B. Name, Website und IP-Adresse.

    Folgende Voraussetzungsprüfungen werden durchgeführt:

    > [!NOTE]
    > Werden keine voraussetzungsprüfungen durchgeführt, wenn die "offline-Option verwendet wird. Weitere Informationen finden Sie unter [Ausführen von %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; im Offlinemodus](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode).

    -   Der vorbereitete DC ist für das Klonen autorisiert (er ist Mitglied der Gruppe **Klonbare Domänencontroller**)

    -   Der PDC-Emulator ausgeführt wird, Windows Server 2012.

    -   Alle Programme oder Dienste, die nach dem Ausführen von **Get-ADDCCloningExcludedApplicationList** aufgelistet wurden, sind in der Liste %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot; enthalten (und werden am Ende dieser Liste mit Klonkomponenten ausführlicher erklärt).

-   **DCCloneConfig.xml** "um das erfolgreiche Klonen ein virtualisierten Domänencontrollers, muss diese Datei vorhanden ist, in dem Verzeichnis, das sich die DIT befindet, werden *%windir%\NTDS*, oder im Stammverzeichnis eines Wechselmedienlaufwerks. Sie wird als ein Auslöser zum Ermitteln und Initiieren eines Klonvorgangs verwendet und bietet auch eine Methode zum Festlegen der Konfigurationseinstellungen für den geklonten Domänencontroller.

    Das Schema und eine Beispieldatei für die Datei %% amp;quot;dccloneconfig.XML%%amp;quot; werden auf allen Windows Server 2012-Computern unter gespeichert:

    -   %windir%\system32\DCCloneConfigSchema.xsd

    -   %windir%\system32\SampleDCCloneConfig.xml

    Es wird empfohlen, das Cmdlet %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; zum Erstellen das Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; zu verwenden. Das Verwenden der Schemadatei mit einem XML-fähigen Editor zum Erstellen dieser Datei ist zwar möglich, das manuelle Bearbeiten der Datei erhöht jedoch die Fehlerwahrscheinlichkeit. Wenn Sie die Datei bearbeiten, müssen Sie dazu einen XML-fähigen Editor wie z. B. Visual Studio, [XML Notepad](https://www.microsoft.com/download/details.aspx?displaylang=en&id=7973)oder eine Anwendung eines Drittanbieters verwenden (verwenden Sie nicht Editor).

-   **Get-ADDCCloningExcludedApplicationList** "dieses Cmdlet wird ausgeführt auf dem Quelldomänencontroller vor dem Beginn des klonprozesses auf, um zu ermitteln, welche Dienste oder installierten Programme nicht auf der unterstützten Standardliste, %% Amp;quot;defaultdccloneallowlist.XML%%amp;quot; oder einer benutzerdefinierten Aufnahmeliste benannte %% amp;quot;customdccloneallowlist.XML%%amp;quot, und haben dadurch nicht für die Auswirkungen des Klonens ausgewertet wurden.

    Dieses Cmdlet durchsucht den Quelldomänencontroller nach Diensten im Dienststeuerungs-Manager und unter **HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall** aufgeführten installierten Programmen, die nicht in der Standardliste (%%amp;quot;DefaultDCCloneAllowList.xml%%amp;quot;) oder ggf. in der benutzerdefinierten Aufnahmeliste (%%amp;quot;CustomDCCloneAllowList.xml%%amp;quot;) enthalten sind. Die Liste der Anwendungen und Dienste, die durch das Ausführen des Cmdlets zurückgegeben wird, zeigt den Unterschied zwischen dem, was bereits in der Datei %%amp;quot;DefaultDCCloneAllowList.xml%%amp;quot; oder %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot; bereitgestellt wurde, und der Liste, die zur Laufzeit erstellt wurde, basierend auf den Installationen auf dem Quelldomänencontroller. Die Dienst- und Programmausgabe von %%amp;quot;Get-ADDCCloningExcludedApplicationList%%amp;quot; kann der Datei %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot; hinzugefügt werden, wenn Sie feststellen, dass die Dienste oder Programme sicher geklont werden können. Werten Sie die folgenden Bedingungen aus, um zu ermitteln. ob ein Dienst oder ein installiertes Programm sicher geklont werden kann:

    -   Hat die Computeridentität (z. B. Name, SID, Kennwort) Auswirkungen auf den Dienst oder das installierte Programm?

    -   Speichert der Dienst oder das installierte Programm auf dem Computer lokal einen Status, der u. U. Auswirkungen auf dessen Funktionalität auf dem Klon hat?

    Sie müssen gemeinsam mit dem Softwareanbieter der Anwendung bestimmen, ob der Dienst oder das Programm sicher geklont werden kann.

    > [!NOTE]
    > Überprüfen Sie vor dem Bereitstellen zusätzlicher Dienste oder Programme in der Datei %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot;, ob Sie über die erforderliche Lizenz zum Kopieren der Software auf diesem virtuellen Computer verfügen.

    Sind die Anwendungen nicht klonbar, entfernen Sie sie vom Quelldomänencontroller, bevor Sie das Klonmedium erstellen. Ist eine Anwendung in der Cmdlet-Ausgabe enthalten, in der Datei %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot; jedoch nicht, schlägt das Klonen fehl. Für ein erfolgreiches Klonen sollte die Cmdlet-Ausgabe keine Dienste oder Programme enthalten. Eine Anwendung sollte also entweder in der Liste %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot; enthalten sein oder vom Quelldomänencontroller entfernt werden.

    In der folgenden Tabelle werden die Optionen zum Ausführen von %%amp;quot;Get-ADDCCloningExcludedApplicationList%%amp;quot; erklärt.

    |||
    |-|-|
    |Argument|Erläuterung|
    |*<no argument specified>*|Zeigt eine Liste mit Diensten oder Programmen auf der Konsole an, die beim Klonen nicht berücksichtigt wurden. Wenn die Datei %%amp;quot;CustomDCCloneAllowList.XML%%amp;quot; bereits an einem der zulässigen Speicherorte vorhanden ist, verwendet sie diese Datei, um die verbleibenden Dienste und Programme anzuzeigen (u. U. keine, wenn die Listen übereinstimmen).|
    |-GenerateXml|Erstellt die Datei %%amp;quot;CustomDCCloneAllowList.XML%%amp;quot; mit den in der Konsole aufgeführten Diensten und Programmen.|
    |-Force|Überschreibt eine vorhandene %%amp;quot;CustomDCCloneAllowList.XML%%amp;quot;-Datei.|
    |-Path|Ordnerpfad zum Erstellen von %%amp;quot;CustomDCCloneAllowList.XML%%amp;quot;.|

-   **DefaultDCCloneAllowList.xml** "Diese Datei ist vorhanden, wird standardmäßig auf jedem Windows Server 2012-Domäne-Controller In der *%windir%\system32*. Darin sind die Dienste und Programme aufgeführt, die standardmäßig sicher geklont werden können. Ändern Sie nicht den Speicherort oder den Inhalt dieser Datei, andernfalls schlägt das Klonen fehl.

-   **CustomDCCloneAllowList.xml** "Wenn Sie Dienste oder installierte Programme, die sich auf Ihrem Quelldomänencontroller befinden, in der Datei %% amp;quot;defaultdccloneallowlist.XML%%amp;quot; aufgeführten, diese Dienste und Programme enthalten sein müssen in diesem die Datei. Führen Sie das Cmdlet **Get-ADDCCloningExcludedApplicationList** aus, um Dienste oder installierte Programme ausfindig zu machen, die nicht in der Datei %%amp;quot;DefaultDCCloneAllowList.xml%%amp;quot; aufgeführt sind. Verwenden Sie die **"GenerateXml** Argument für die XML-Datei zu generieren.

    Der Klonprozess überprüft der Reihe nach folgende Speicherorte auf diese Datei und verwendet unabhängig vom Inhalt des Ordners die erste gefundene XML-Datei:

    1.  Der folgende Registrierungsschlüssel:

        ```
        HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters
        AllowListFolder (REG_SZ)
        ```

    2.  DSA-Arbeitsverzeichnis

    3.  %systemroot%\NTDS

    4.  Lese-/Schreib-Wechselmedien in der Reihenfolge des Laufwerkbuchstabens, im Stamm des Laufwerks

### <a name="deployment-scenarios"></a>Bereitstellungsszenarien
Folgende Bereitstellungsszenarien werden für das Klonen eines virtuellen Domänencontrollers unterstützt:

-   Bereitstellen eines geklonten Domänencontrollers durch Erstellen einer Kopie der Datei von einem Quelldomänencontroller virtuelle Festplatte (Vhd).

-   Bereitstellen eines geklonten Domänencontrollers durch Kopieren des virtuellen Computers eines Quelldomänencontrollers mithilfe der vom Hypervisor bereitgestellten Export-/Importsemantik.

> [!NOTE]
> Die Schritte im Abschnitt [Schritte zum Bereitstellen eines geklonten virtualisierten Domänencontrollers](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc) veranschaulichen das Kopieren eines virtuellen Computers mithilfe der Export-/Importfeatures von Windows Server 2012 Hyper-V.

## <a name="steps_deploy_vdc"></a>Schritte zum Bereitstellen eines geklonten virtualisierten Domänencontrollers

-   [Erforderliche Komponenten](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#prerequisites)

-   [Schritt 1: Gewähren Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk4_grant_source)

-   [Schritt 2: Das Cmdlet Get-ADDCCloningExcludedApplicationList "ausführen"](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet)

-   [Schritt 3: New-ADDCCloneConfigFile ausführen](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk5_create_insert_dccloneconfig)

-   [Schritt 4: Exportieren Sie und importieren Sie des virtuellen Computers des Quelldomänencontrollers](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk7_export_import_vm_sourcedc)

### <a name="prerequisites"></a>Erforderliche Komponenten

-   Damit Sie die Schritte in den folgenden Verfahren ausführen können, müssen Sie ein Mitglied der Gruppe der Domänen-Admins sein oder über dieselben Berechtigungen verfügen, die dieser Gruppe zugewiesen sind.

-   Die Windows PowerShell-Befehle, die in diesem Handbuch verwendeten müssen eine Eingabeaufforderung mit erhöhten Rechten ausgeführt werden. Zu diesem Zweck mit der rechten Maustaste die **Windows PowerShell** Symbol, und klicken Sie dann auf **als Administrator ausführen**.

-   Ein Windows Server 2012-Server mit Hyper-V-Serverrolle installiert (**HyperV1**).

-   Einen zweiten Windows Server 2012-Server mit Hyper-V-Serverrolle installiert (**HyperV2**).

    > [!NOTE]
    > -   Wenn Sie einen anderen Hypervisor verwenden, wenden Sie sich an den Anbieter, um zu überprüfen, ob der Hypervisor die VM-Generations-ID unterstützt. Wenn der Hypervisor die VM-Generations-ID nicht unterstützt und Sie eine %%amp;quot;DCCloneConfig.xml%%amp;quot;-Datei bereitgestellt haben, wird der neue virtuelle Computer im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) gestartet.
    > -   Um die Verfügbarkeit des AD DS-Diensts zu erhöhen, werden in diesem Handbuch Anweisungen empfohlen und zur Verfügung gestellt, bei denen zwei verschiedene Hyper-V-Hosts verwendet werden; dadurch wird verhindert, dass nur ein einziger potenzieller Fehlerpunkt vorhanden ist. Sie benötigen jedoch keine zwei Hyper-V-Host, um einen virtuellen Domänencontroller zu klonen.
    > -   Sie müssen auf allen Hyper-V-Servern (**HyperV1** und **HyperV2**) Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; sein.
    > -   Um eine VHD-Datei mithilfe von Hyper-V erfolgreich zu importieren und exportieren, sollten die virtuellen Netzwerkswitches auf beiden Hyper-V-Hosts denselben Namen haben. Ist auf **HyperV1** beispielsweise ein virtueller Netzwerkswitch mit dem Namen %%amp;quot;VNet%%amp;quot; vorhanden, muss auch auf **HyperV2** ein virtueller Netzwerkswitch mit dem Namen %%amp;quot;VNet%%amp;quot; vorhanden sein.
    > -   Wenn die beiden Hyper-V-Hosts (**HyperV1** und **HyperV2**) verschiedene Prozessoren verwenden, fahren Sie den virtuellen Computer (**VirtualDC1**) herunter, den die exportieren möchten, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, klicken Sie auf **Einstellungen** und auf **Prozessor**, wählen Sie unter **Prozessorkompatibilität** die Option **Zu einem physischen Computer mit einer anderen Prozessorversion migrieren**, und klicken Sie auf **OK**.

-   Eine bereitgestellte Windows Server 2012-Domänencontroller (virtualisiert oder physisch), der die PDC-Emulatorrolle hostet (**DC1**). Um zu überprüfen, ob die PDC-Emulatorrolle auf einem Windows Server 2012-Domänencontroller gehostet wird, führen Sie den folgenden Windows PowerShell-Befehl ein:

    ```
    Get-ADComputer (Get-ADDomainController "Discover "Service "PrimaryDC").name "Property operatingsystemversion | fl
    ```

    Der OperatingSystemVersion-Wert sollte als Version 6.2 zurückgegeben werden. Bei Bedarf können Sie die PDC-Emulatorrolle auf einem Domänencontroller übertragen, die Windows Server 2012 ausgeführt wird. Weitere Informationen finden Sie unter [Using Ntdsutil.exe to transfer or seize FSMO roles to a domain controller](https://support.microsoft.com/kb/255504).

-   Eine bereitgestellte Windows Server 2012 virtualisierter-gastdomänencontroller (**VirtualDC1**), die sich in derselben Domäne wie der Windows Server 2012-Domänencontroller, den PDC-Emulatorrolle hostet (**DC1**). Hierbei handelt es sich um den zum Klonen verwendeten Quelldomänencontroller. Der virtuelle gastdomänencontroller wird auf einem Windows Server 2012 Hyper-V-Server gehostet werden (**HyperV1**).

    > [!NOTE]
    > -   Damit das Klonen erfolgreich ist, darf der zum Erstellen des Klons verwendete Quelldomänencontroller nicht von einem Domänencontroller stammen, der seit der Erstellung des VHD-Quellmediums herabgestuft wurde.
    > -   Fahren Sie den Quelldomänencontroller vor dem Kopieren des virtuellen Computers oder der virtuellen Festplatte herunter.
    > -   Sie sollten keine virtuelle Festplatte klonen bzw. einen Momentaufnahme wiederherstellen, die die Tombstone-Lebensdauer überschreiten (bzw. die Lebensdauer des gelöschten Objekts, wenn der Active Directory-Papierkorb aktiviert ist). Wenn Sie eine virtuelle Festplatte eines vorhandenen Domänencontrollers kopieren, stellen Sie sicher, dass die VHD-Datei die Tombstone-Lebensdauer nicht überschreitet (Standardwert: 60 Tage). Sie sollten nicht die virtuelle Festplatte eines aktiven Domänencontrollers kopieren, um Klonmedien zu erstellen.

    Werfen Sie alle virtuellen Diskettenlaufwerke aus, die u. U. auf dem Quelldomänencontroller vorhanden sind. Dies kann beim Versuch, den neuen virtuellen Computer zu importieren, zu Freigabeproblemen führen.

    Nur Windows Server 2012-Domänencontroller auf einem VM-Generations-ID-Hypervisor gehostet, können als Quelle zum Klonen verwendet werden. Die Windows Server 2012 verwendeten Quelldomänencontroller für das Klonen sollte in einem fehlerfreien Zustand. Zum Ermitteln des Status des Quelldomänencontrollers führen Sie [dcdiag](https://technet.microsoft.com/library/cc731968(WS.10).aspx)aus. Um ein besseres Verständnis der von Dcdiag zurückgegebenen Ausgabe zu erhalten, finden Sie unter [What does DCDIAG... tun? ](http://blogs.technet.com/b/askds/archive/2011/03/22/what-does-dcdiag-actually-do.aspx).

    Wenn es sich beim Quelldomänencontroller um einen DNS-Server handelt, ist auch der geklonte Domänencontroller ein DNS-Server. Sie sollten einen DNS-Server auswählen, der nur Active Directory-integrierte Zonen hostet.

    DNS-Clienteinstellungen werden nicht geklont, sondern in der Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; angegeben. Werden die Einstellungen nicht angegeben, verweist der geklonte Domänencontroller standardmäßig auf sich selbst als bevorzugten DNS-Server. Für den geklonten Domänencontroller ist keine DNS-Delegierung vorhanden. Der Administrator der übergeordneten DNS-Zone sollte die DNS-Delegierung für den geklonten Domänencontroller bei Bedarf aktualisieren.

    > [!WARNING]
    > Die Virtualisierungsschutzvorrichtungen sind nicht auf Active Directory Lightweight Directory Services (AD LDS) erweiterbar. Daher sollten Sie nicht versuchen, einen AD DS-Domänencontroller zu klonen, der eine AD LDS-Instanz hostet, indem Sie der Liste %%amp;quot;CustomDCCloneAllowList.xml%%amp;quot; diese AD LDS-Instanz hinzufügen. Das AD LDS nicht VM-Generations-ID-fähig ist, kann das Klonen eines Domänencontroller mit AD LDS zu Abweichungen in diesem AD LDS-Konfigurationssatz führen, die durch ein USN-Rollback verursacht werden.

    Folgende Serverrollen werden nicht für das Klonen unterstützt:

    -   Dynamic Host Configuration-Protokoll (DHCP)

    -   Active Directory-Zertifikatdienste (AD CS)

    -   Active Directory Lightweight Directory Services (ADLDS)

### <a name="bkmk4_grant_source"></a>Schritt 1: Erteilen der Berechtigung, geklont zu werden, für den virtualisierten Quelldomänencontroller
In diesem Verfahren erteilen Sie dem Quelldomänencontroller die Berechtigung, geklont zu werden, indem Sie mit dem **Active Directory-Verwaltungscenter** den Quelldomänencontroller der Gruppe **Klonbare Domänencontroller** hinzufügen.

##### <a name="to-grant-the-source-virtualized-domain-controller-the-permission-to-be-cloned"></a>So erteilen Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden

1.  Öffnen Sie auf einem beliebigen Domänencontroller in derselben Domäne wie der zum Klonen vorbereitete Domänencontroller (**VirtualDC1**), das **Active Directory-Verwaltungscenter** (ADAC), suchen Sie das virtualisierte Domänencontrollerobjekt (Domänencontroller befinden sich in der Regel im ADAC im Container **Domänencontroller** ), klicken Sie mit der rechten Maustaste darauf, wählen Sie die Option **Zur Gruppe hinzufügen** , geben Sie unter **Geben Sie die zu verwendenden Objektnamen ein****Cloneable Domain Controllers** ein, und klicken Sie dann auf **OK**.

    Die in diesem Schritt durchgeführte Aktualisierung der Gruppenmitgliedschaft muss auf dem PDC-Emulator repliziert werden, bevor der Klonvorgang ausgeführt werden kann. Wenn die **Klonbare Domänencontroller** Gruppe wurde nicht gefunden, der die PDC-Emulatorrolle möglicherweise nicht auf einem Domänencontroller mit Windows Server 2012 gehostet.

    > [!NOTE]
    > Öffnen Sie zum Öffnen von ADAC auf einem Windows Server 2012-Domänencontroller mit Windows PowerShell, und geben **dsac.exe**.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Das folgende Windows PowerShell-Cmdlet führt dieselbe Funktion aus wie das vorhergehende Verfahren:


    Add-ADGroupMember "Identity "CN=Cloneable Domain Controllers,CN=Users, DC=Fabrikam,DC=Com" "Member "CN=VirtualDC1,OU=Domain Controllers,DC=Fabrikam,DC=com"


### <a name="bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet"></a>Schritt 2: Ausführen des Cmdlets „Get-ADDCCloningExcludedApplicationList“
In diesem Verfahren führen Sie das Cmdlet `Get-ADDCCloningExcludedApplicationList` auf dem virtualisierten Quelldomänencontroller aus, um Programme oder Dienste zu identifizieren, die nicht im Hinblick auf das Klonen ausgewertet wurden. Sie müssen das Cmdlet %%amp;quot;Get-ADDCCloningExcludedApplicationList%%amp;quot; vor dem Cmdlet %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; ausführen, da das Cmdlet %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; keine %%amp;quot;DCCloneConfig.xml%%amp;quot;-Datei erstellt, wenn es eine ausgeschlossene Anwendung ermittelt.

##### <a name="to-identify-applications-or-services-that-run-on-a-source-domain-controller-which-have-not-been-evaluated-for-cloning"></a>So identifizieren Sie Anwendungen oder Dienste, die auf einem Quelldomänencontroller ausgeführt werden und nicht im Hinblick auf Klonen ausgewertet wurden

1.  Klicken Sie auf dem Quelldomänencontroller (**VirtualDC1**) auf **Server-Manager**, **Tools** und **Active Directory-Modul für Windows PowerShell**, und geben Sie dann den folgenden Befehl ein:


    Get-ADDCCloningExcludedApplicationList


2.  Prüfen Sie gemeinsam mit dem Softwareanbieter die Liste mit zurückgegebenen Diensten und installierten Programmen, um zu ermitteln, ob diese sicher geklont werden können. Wenn bestimmte Anwendungen oder Dienste in der Liste nicht sicher geklont werden können, müssen Sie vom Quelldomänencontroller entfernt werden, andernfalls schlägt das Klonen fehl.

3.  Für den Satz von Diensten und installierten Programme, die sicher geklont werden ermittelt wurde, führen Sie den Befehl erneut mit der **"GenerateXML** wechseln Sie zur Bereitstellung dieser Dienste und Programme in der **%% amp;quot;customdccloneallowlist.XML%%amp;quot;**  Datei.


    Get-ADDCCloningExcludedApplicationList -GenerateXml


### <a name="bkmk5_create_insert_dccloneconfig"></a>Schritt 3: New-ADDCCloneConfigFile ausführen
Führen Sie auf dem Quelldomänencontroller %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; aus, und geben Sie optional Konfigurationseinstellungen für den geklonten Domänencontroller an, z. B. Name, IP-Adresse und DNS-Auflösung.

Geben Sie z. B. Folgendes ein, um einen geklonten Domänencontroller mit dem Namen %%amp;quot;VirtualDC2%%amp;quot; mit einer statischen IPv4-Adresse zu erstellen:


    New-ADDCCloneConfigFile "Static -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.255.0" -CloneComputerName "VirtualDC2" -IPv4DefaultGateway "10.0.0.3" -SiteName "REDMOND"

> [!NOTE]
> Der geklonte Domänencontroller wird sich am selben Standort wie der Quelldomänencontroller befinden, außer in der Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; ist ein anderer Standort angegeben. Es wird empfohlen, in der Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; einen geeigneten Standort für den geklonten Domänencontroller basierend auf dessen IP-Adresse anzugeben.

Der Computername ist optional. Wenn Sie keinen angeben, wird basierend auf folgendem Algorithmus ein eindeutiger Name generiert:

-   Das Präfix besteht aus den ersten acht Zeichen des Computernamens des Quelldomänencontrollers. Beispielsweise wird der Quellcomputername %%amp;quot;SourceComputer%%amp;quot; zur Präfixzeichenfolge %%amp;quot;SourceCo%%amp;quot; verkürzt.

-   Ein eindeutiges Namenssuffix im Format "" CL*Nnnn*"wird an die Präfixzeichenfolge angehängt, in denen *Nnnn* ist der nächste Wert zwischen 0001-9999 darstellt, der vom PDC ermittelt wird derzeit nicht verwendet. Wenn die nächste verfügbare Zahl im zulässigen Bereich z. B. 0047 ist und wie im vorangehenden Beispiel das Computernamenpräfix %%amp;quot;SourceCo%%amp;quot; verwendet wird, wird der abgeleitete Name für den geklonten Computer als %%amp;quot;SourceCo-CL0047%%amp;quot; festgelegt.

> [!NOTE]
> Damit das Cmdlet %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; ordnungsgemäß funktioniert, ist ein globaler Katalogserver erforderlich. Der Quelldomänencontroller Mitgliedschaft in der **Klonbare Domänencontroller** Gruppe muss auf dem globalen Katalogserver wiedergegeben werden. Der globale Katalogserver muss nicht derselbe Domänencontroller wie der PDC-Emulator sein, sollte sich jedoch möglichst am selben Standort befinden. Wenn kein globaler Katalogserver nicht verfügbar ist, kann der Befehl mit dem Fehler "der Server ist nicht funktionstüchtig." Weitere Informationen finden Sie unter [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).

Geben Sie Folgendes ein, um einen geklonten Domänencontroller mit dem Namen %%amp;quot;Clone1%%amp;quot; und statischen IPv4-Einstellungen zu erstellen, und geben Sie bevorzugte und alternative WINS-Server an:


    New-ADDCCloneConfigFile "CloneComputerName "Clone1" "Static -IPv4Address "10.0.0.5" "IPv4DNSResolver "10.0.0.1" "IPv4SubnetMask "255.255.0.0" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


> [!NOTE]
> Wenn Sie die WINS-Server angeben, müssen Sie angeben, beide **"PreferredWINSServer** und **" AlternateWINSServer**. Wenn Sie nur eines dieser Argumente angeben, schlägt das Klonen mit dem Fehlercode %%amp;quot;0x80041005%%amp;quot;, der in der Protokolldatei %%amp;quot;dcpromo.log%%amp;quot; angezeigt wird.

Zum Erstellen eines geklonten Domänencontrollers mit dem Namen %%amp;quot;Clone2%%amp;quot; mit dynamischen IPv4-Einstellungen geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" 


> [!NOTE]
> In diesem Fall sollte sich in der Umgebung ein DHCP-Server befinden, den der Klon erreichen kann und die IP-Adresse sowie andere relevante Netzwerkeinstellungen davon abrufen kann.

Geben Sie Folgendes ein, um einen geklonten Domänencontroller mit dem Namen %%amp;quot;Clone2%%amp;quot; und dynamischen IPv4-Einstellungen zu erstellen, und geben Sie bevorzugte und alternative WINS-Server an:


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" -SiteName "REDMOND" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


Geben Sie Folgendes ein, um einen geklonten Domänencontroller mit dynamischen IPv6-Einstellungen zu erstellen:


    New-ADDCCloneConfigFile -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


Geben Sie Folgendes ein, um einen geklonten Domänencontroller mit statischen IPv6-Einstellungen zu erstellen:


    New-ADDCCloneConfigFile "Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


> [!NOTE]
> Wenn Sie IPv6-Einstellungen angeben, ist der einzige Unterschied zwischen den Einstellungen für statischen und dynamischen die Aufnahme der **-statische** wechseln. Die Einbeziehung der **-statische** Switch macht es erforderlich, geben Sie mindestens eine **IPv6DNSResolver**. Die statische IPv6-Adresse wird erwartet, automatische Konfiguration zustandsloser Adressen (SLAAC) mit vom Router zugewiesenen Präfixen konfiguriert wird. Bei dynamischem IPv6 sind die DNS-Auflösungen sind optional, aber es wird erwartet, dass der Klon einen IPv6-fähigen DHCP-Server, auf das Subnetz, das Abrufen von IPv6-Adresse und DNS-Konfigurationsinformationen erreichen kann.

#### <a name="BKMK_OfflineMode"></a>Ausführen von New-ADDCCloneConfigFile in offline-Modus
Wenn Sie über mehrere Kopien von zum Klonen vorbereiteten Quelldomänencontroller-Medien verfügen (d. h. der Quelldomänencontroller ist zum Klonen autorisiert, das Cmdlet %%amp;quot;Get-ADDCCloningExcludedApplicationList%%amp;quot; wurde ausgeführt usw.), und Sie möchten für jede Kopie des Mediums verschiedene Einstellungen festlegen, können Sie %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; im Offlinemodus ausführen. Dies ist möglicherweise effizienter als das individuelle Vorbereiten jedes einzelnen virtuellen Computers, z. B. durch Importieren aller Kopien.

In diesem Fall können Domänen-Admins den Offlinedatenträger bereitstellen und Remote Serveradministration Tools (RSAT) zum Ausführen des Cmdlets New-ADDCCloneConfigFile mit den - offline-Argument verwenden, um die XML-Dateien, was die werksähnliche Automatisierung mithilfe neuer hinzufügen Windows PowerShell-Optionen, die in Windows Server 2012 enthalten. Weitere Informationen zum Bereitstellen des Offlinedatenträgers zum Ausführen des Cmdlets %%amp;quot;New-ADDCCloneConfigFile%%amp;quot; im Offlinemodus finden Sie unter [Hinzufügen von XML zum Offlinesystemdatenträger](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_Offline).

Sie sollten das Cmdlet zunächst lokal auf den Quellmedien ausführen, um sicherzustellen, dass die Voraussetzungsprüfungen erfolgreich durchgeführt werden. Die Voraussetzungsprüfungen werden nicht im Offlinemodus durchgeführt, da das Cmdlet u. U. auf einem Computer ausgeführt wird, der sich nicht in derselben Domäne befindet, bzw. auf einem Computer, der einer Domäne angehört. Nach dem lokalen Ausführen des Cmdlets wird die Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; erstellt. Sie können die lokal erstellte Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; löschen, wenn Sie anschließend den Offlinemodus verwenden möchten.

Erstellen ein geklonten Domänencontrollers mit dem Namen CloneDC1 im Offlinemodus am Standort REDMOND"mit statischen IPv4-Adresse, Typ:


    New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS


Zum Erstellen eines geklonten Domänencontrollers mit dem Namen %%amp;quot;Clone2%%amp;quot; im Offlinemodus mit statischen IPv4- und IPv6-Einstellungen geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS


Zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit statischen IPv4- und dynamischen IPv6-Einstellungen und zum Angeben mehrerer DNS-Server für die DNS-Auflösungseinstellungen geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS 


Zum Erstellen eines geklonten Domänencontrollers mit dem Namen %%amp;quot;Clone1%%amp;quot; im Offlinemodus mit statischen IPv4- und IPv6-Einstellungen geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS


Zum Erstellen eines geklonten Domänencontrollers im Offlinemodus mit dynamischen IPv4- und IPv6-Einstellungen geben Sie Folgendes ein:


    New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS


### <a name="bkmk7_export_import_vm_sourcedc"></a>Schritt 4: Exportieren und anschließendes Importieren des virtuellen Computers des Quelldomänencontrollers
In diesem Verfahren exportieren Sie den virtuellen Computer des virtualisierten Quelldomänencontroller und importieren dann den virtuellen Computer. Durch diese Aktion wird in Ihrer Domäne ein geklonter virtualisierte Domänencontroller erstellt.

Sie müssen auf jedem Hyper-V-Host Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; sein. Wenn Sie für jeden Server unterschiedliche Anmeldeinformationen verwenden, führen Sie die Windows PowerShell-Cmdlets aus, um den virtuellen Computern in verschiedenen Windows PowerShell-Sitzungen zu exportieren und importieren.

Wenn auf dem Quelldomänencontroller Momentaufnahmen vorhanden sind, sollten diese vor dem Exportieren des Quelldomänencontrollers gelöscht werden, da der virtuelle Computer nicht importiert wird, wenn die Prozessoreinstellungen einer Momentaufnahme nicht mit dem Hyper-V-Zielhost kompatibel sind. Wenn die Prozessoreinstellungen zwischen den Hyper-V-Quell- und Zielhosts kompatibel sind, können Sie die Quelle ohne vorheriges Löschen von Momentaufnahmen exportieren und kopieren. Nach dem Importieren müssen die Momentaufnahmen jedoch vom geklonten virtuellen Computer gelöscht werden, bevor er gestartet wird.

##### <a name="to-copy-a-virtual-domain-controller-by-exporting-and-then-importing-the-virtualized-source-domain-controller"></a>So kopieren Sie einen virtuellen Domänencontroller durch Exportieren und anschließendes Importieren des virtualisierten Quelldomänencontrollers

1.  Fahren Sie auf **HyperV1** den Quelldomänencontroller (**VirtualDC1**) herunter.

    ![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    Stop-VM -Name VirtualDC1 -ComputerName HyperV1


2.  Löschen Sie auf **HyperV1** Momentaufnahmen, und exportieren Sie dann den Quelldomänencontroller (VirtualDC1) in das Verzeichnis %%amp;quot;c:\CloneDCs%%amp;quot;.

> [!NOTE]
> Löschen Sie alle zugeordneten Momentaufnahmen, da bei jeder Erstellung einer Momentaufnahme auch eine neue AVHD-Datei erstellt wird, die als differenzierender Datenträger fungiert. Dies löst eine Kettenreaktion aus. Wenn Sie Momentaufnahmen erstellt haben, und die Datei %%amp;quot;DCCLoneConfig.xml%%amp;quot; auf der virtuellen Festplatte einfügen, erstellen Sie möglicherweise einen Klon einer älteren DIT-Version oder fügen die Konfigurationsdatei in die falsche VHD-Datei ein. Durch Löschen der Momentaufnahme werden all diese AVHDs in der Basis-VHD zusammengeführt.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***


    Get-VMSnapshot VirtualDC1 | Remove-VMSnapshot -IncludeAllChildSnapshots
    Export-VM -Name VirtualDC1 -ComputerName HyperV1 -Path c:\CloneDCs\VirtualDC1


3.  Kopieren Sie den Ordner **virtualdc1** in das Verzeichnis %%amp;quot;c:\Import%%amp;quot; von **HyperV2**.

4.  Importieren Sie auf **HyperV2**mit dem **Hyper-V-Manager**den virtuellen Computer (verwenden Sie dazu den Assistenten zum **Importieren virtueller Computer** in **Hyper-V-Manager**) aus dem Ordner **c:\Import\virtualdc1** , und löschen Sie alle dazugehörigen **Momentaufnahmen**.

Verwenden Sie beim Importieren des virtuellen Computers die Option **Virtuellen Computer kopieren (neue eindeutige ID erstellen)** .

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Machines"
    $vm = Import-VM -Path $path.fullname -Copy -GenerateNewId
    Rename-VM $vm VirtualDC2


So erstellen Sie mehrere geklonte Domänencontroller vom selben Quelldomänencontroller:

  -   Benutzeroberfläche: Geben Sie im Assistenten zum **Importieren virtueller Computer** neue Speicherorte für den **Ordner für die Konfiguration des virtuellen Computers**, den **Momentaufnahmespeicher**und den **Ordner für Smart Paging**sowie einen anderen **Speicherort** für die virtuellen Festplatten für dem virtuellen Computer an.

  -   Windows PowerShell: Geben Sie neue Speicherorte für den virtuellen Computer mithilfe der folgenden Parameter für die `Import-VM` Cmdlet:

        $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Computer" Import-VM-Pfad $path.fullname - kopieren - GenerateNewId - ComputerName HyperV2 - VhdDestinationPath "Path" - SnapshotFilePath "Path" - SmartPagingFilePath "Path" - VirtualMachinePath "Path"


> [!NOTE]
> Die empfohlene Batchgröße beim gleichzeitigen Erstellen mehrerer geklonter Domänencontroller ist 10. Die maximale Anzahl wird durch die maximale Anzahl von ausgehenden Replikationsverbindungen begrenzt, d. h. 16 für die DFS-Replikation (DFSR) und 10 für den Dateireplikationsdienst (File Replication Service, FRS). Sie sollten nicht mehr als die empfohlene Anzahl von geklonten Domänencontrollern gleichzeitig bereitstellen, außer Sie haben diese Anzahl in Ihrer Umgebung ausgiebig getestet.

5.  Starten Sie auf **HyperV1**den Quelldomänencontroller (**(VirtualDC1**) neu, um ihn wieder online zu schalten.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    Start-VM -Name VirtualDC1 -ComputerName HyperV1


6.  Starten Sie auf **HyperV2**den virtuellen Computer (**VirtualDC2**), um ihn als geklonten Domänencontroller in der Domäne online zu schalten.

![Einführung in AD DS](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***


    Start-VM -Name VirtualDC2 -ComputerName HyperV2

> [!NOTE]
> Damit das Klonen erfolgreich ist, muss der PDC-Emulator ausgeführt werden. Wenn er heruntergefahren wurde, stellen Sie sicher, dass er wieder hochgefahren und die Erstsynchronisierung ausgeführt wurde, damit er seine Rolle als PDC-Emulatorrolle erkennt. Weitere Informationen finden Sie im Microsoft [KB-Artikel 305476](https://support.microsoft.com/kb/305476).

Überprüfen Sie nach dem Abschließen des Klonvorgangs anhand des Namens des geklonten Computers, ob das Klonen erfolgreich war. Stellen Sie sicher, dass der virtuelle Computer nicht im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) gestartet wurde. Wenn Sie bei der Anmeldung die Fehlermeldung erhalten, dass keine Anmeldeserver verfügbar sind, versuchen Sie sich im Verzeichnisdienst-Wiederherstellungsmodus anzumelden. Wenn der Domänencontroller nicht erfolgreich geklont wurde und im Verzeichnisdienst-Wiederherstellungsmodus gestartet wurde, überprüfen Sie die Protokolle in der Ereignisanzeige und die DCpromo-Protokolle im Ordner %%amp;quot;%systemroot%/debug%%amp;quot;.

Der geklonte Domänencontroller wird Mitglied der Gruppe **Klonbare Domänencontroller**, da diese Mitgliedschaft vom Quelldomänencontroller kopiert wird. Als bewährte Methode sollten Sie die Gruppe **Klonbare Domänencontroller** leer lassen, bis Sie zum Ausführen von Klonvorgängen bereit sind. Zudem sollten Sie Mitglieder nach dem Abschließen der Klonvorgänge entfernen.

Wenn der Quelldomänencontroller ein Sicherungsmedium speichert, wird dieses auch vom geklonten Domänencontroller gespeichert. Führen Sie `wbadmin get versions` aus, um das Sicherungsmedium auf dem geklonten Domänencontroller anzuzeigen. Ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; sollte das Sicherungsmedium vom geklonten Domänencontroller entfernen, damit es nicht versehentlich wiederhergestellt wird. Weitere Informationen zum Löschen einer Systemstatussicherung mithilfe von „wbadmin.exe“ finden Sie unter [Wbadmin delete systemstatebackup](https://technet.microsoft.com/library/cc742081(v=WS.10).aspx).

## <a name="troubleshooting"></a>Problembehandlung bei
Wenn der geklonte Domänencontroller (**VirtualDC2**) im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) gestartet wird, kehrt er beim nächsten Neustart nicht automatisch zum normalen Modus zurück. Zum Anmelden an einem Domänencontroller, der im Verzeichnisdienst-Wiederherstellungsmodus gestartet wird, verwenden Sie **.\Administrator** und geben das DSRM-Kennwort ein.

Beheben Sie die Ursache des Fehlers beim Klonen, und stellen Sie sicher, dass in der Protokolldatei %%amp;quot;dcpromo.log%%amp;quot; nicht angegeben ist, dass der Klonvorgang nicht wiederholt werden kann. Wenn der Klonvorgang nicht wiederholt werden kann, verwerfen Sie das Medium auf sichere Art und Weise. Wenn der Klonvorgang wiederholt werden kann, müssen Sie das DSRM-Startkennzeichen löschen, um den Klonvorgang erneut auszuführen.

1.  Öffnen von Windows Server 2012 mit einem Befehl mit erhöhten Rechten, (rechts klicken Sie auf Windows Server 2012, und wählen Sie als Administrator ausführen), und geben Sie dann **Msconfig**.

2.  Deaktivieren Sie auf der Registerkarte **Start** unter **Startoptionen**die Option **Abgesicherter Start** (diese Option ist bereits mit der **%%amp;quot;Active Directory-Reparatur%%amp;quot;** aktiviert).

3.  Klicken Sie auf **OK** , und starten Sie den Computer neu, wenn Sie dazu aufgefordert werden.

Weitere Informationen zur Problembehandlung bei virtuellen Domänencontrollern finden Sie unter [Problembehandlung für virtualisierte Domänencontroller](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).


