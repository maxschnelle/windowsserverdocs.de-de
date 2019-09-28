---
title: Sichere Virtualisierung Active Directory Domain Services (AD DS)
description: Rollback und sichere Virtualisierung von Active Directory
ms.topic: article
ms.prod: windows-server
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: 67e35a47467b1f5f66bfd073c6f9db06094ea3f9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391028"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Sichere Virtualisierung Active Directory Domain Services (AD DS)

>Gilt für: Windows Server

Ab Windows Server 2012 bietet AD DS mehr Unterstützung für die Virtualisierung von Domänen Controllern, indem virtualisierungssichere Funktionen eingeführt werden. In diesem Artikel wird die Rolle von-Anwendungen und invocationids bei der Domänen Controller Replikation erläutert. Außerdem werden mögliche mögliche Probleme erläutert.

## <a name="update-sequence-number-and-invocationid"></a>Update Sequenznummer und invocationID

Virtuelle Umgebungen bedeuten individuelle Herausforderungen für verteilte Arbeitslasten, die von einem logischen taktbasierten Replikationsschema abhängen. Die AD DS-Replikation verwendet beispielsweise einen monoton steigenden Wert (als %%amp;quot;USN%%amp;quot; oder %%amp;quot;Updatesequenznummer%%amp;quot;), der Transaktionen auf jedem Domänencontroller zugewiesen ist. Jeder Domänen Controller-Daten Bank Instanz wird auch eine Identität zugewiesen, die als invocationID bezeichnet wird. Die Aufrufkennung eines Domänencontrollers dient in Verbindung mit der USN als eindeutiger Bezeichner, der jeder Schreibtransaktion auf jedem Domänencontroller zugeordnet ist, und innerhalb der Gesamtstruktur eindeutig sein muss.

Die AD DS-Replikation verwendet Aufrufkennungen und USNs auf jedem Domänencontroller, um zu bestimmen, welche Änderungen auf anderen Domänencontrollern repliziert werden müssen. Wenn für einen Domänen Controller ein Rollback außerhalb der Informationen des Domänen Controllers ausgeführt wird und für eine vollkommen andere Transaktion eine Anwendungs-Anwendungs Laufzeit verwendet wird, wird die Replikation nicht konvergiert, da andere Domänen Controller davon ausgehen, dass Sie die Updates bereits erhalten haben. wird der wiederverwendeten Benutzer-ID im Kontext dieser invocationID zugeordnet.

Die folgende Abbildung veranschaulicht z. B. die Abfolge von Ereignissen in Windows Server 2008 R2 und älteren Betriebssystemen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In dieser Abbildung erfolgt die Erkennung eines Rollbacks für die Wiedergabe auf VDC2, wenn ein Replikations Partner erkennt, dass VDC2 einen Aktualitäts-UPN-Wert gesendet hat, der zuvor vom Replikations Partner erkannt wurde. Dies deutet darauf hin, dass für dies-Datenbank ein Rollback durchgeführt wurde. nicht ordnungsgemäß.

![Die Abfolge von Ereignissen, wenn ein Rollback für das Wiederverwendungs Zeitpunkt erkannt wird](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

Mit einem virtuellen Computer (VM) können Hypervisor-Administratoren problemlos ein Rollback für die USNs (die logische Uhr) eines Domänen Controllers durchführen, indem Sie beispielsweise eine Momentaufnahme außerhalb der Informationen des Domänen Controllers anwenden. Weitere Informationen zur USN und zum USN-Rollback, einschließlich weiterer Abbildungen zur Veranschaulichung unerkannter Instanzen eines USN-Rollbacks, finden Sie unter [USN and USN Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback).

Ab Windows Server 2012 können AD DS virtuellen Domänen Controllern, die auf Hypervisor-Plattformen gehostet werden, die einen Bezeichner mit dem Namen VM-Generations-ID verfügbar machen, die Sicherheitsmaßnahmen erkennen und anwenden, um die AD DS Umgebung zu schützen, wenn die virtuelle Maschine die Zeit, die die Anwendung einer VM-Momentaufnahme zurückgibt. Der VM-Generations-ID-Entwurf verwendet einen unabhängigen Mechanismus des Hypervisoranbieters, um diesen Bezeichner im Adressbereich des virtuellen Gastcomputers bereitzustellen, damit die sichere Virtualisierung ständig von jedem Hypervisor verfügbar ist, der VM-Generations-ID unterstützt. Dieser Bezeichner kann von Diensten und Anwendungen verwendet werden, die innerhalb des virtuellen Computers ausgeführt werden, um zu ermitteln, ob für einen virtuellen Computer ein Rollback durchgeführt wurde.

## <a name="effects-of-usn-rollback"></a>Auswirkungen des Rollbacks für die Wiederverwendung

Wenn ein Rollback durchgeführt wird, werden Änderungen an Objekten und Attributen nicht von Zieldomänen Controllern, auf denen die Anwendungs-n zuvor aufgetreten ist, in eingehender Richtung repliziert.

Da diese Zieldomänen Controller der Meinung sind, dass Sie auf dem neuesten Stand sind, werden keine Replikations Fehler in Verzeichnisdienst-Ereignisprotokollen oder von Überwachungs-und Diagnosetools gemeldet.

Der ein-und Zurücksetzung kann sich auf die Replikation eines beliebigen Objekts oder Attributs in einer beliebigen Partition auswirken. Der am häufigsten beobachtete Nebeneffekt besteht darin, dass Benutzerkonten und Computer Konten, die auf dem Rollback-Domänen Controller erstellt werden, auf einem oder mehreren Replikations Partnern nicht vorhanden sind. Oder die Kenn Wort Aktualisierungen, die auf dem Rollback-Domänen Controller stammen, sind nicht auf den Replikations Partnern vorhanden.

Ein Rollback für ein Rollback kann verhindern, dass jeder Objekttyp in einer beliebigen Active Directory Partition replizieren kann. Diese Objekttypen umfassen Folgendes:

* Die Active Directory Replikations Topologie und des Zeitplans
* Das vorhanden sein von Domänen Controllern in der Gesamtstruktur und den Rollen, die diese Domänen Controller enthalten
* Das vorhanden sein von Domänen-und Anwendungs Partitionen in der Gesamtstruktur
* Das vorhanden sein von Sicherheitsgruppen und ihrer aktuellen Gruppenmitgliedschaften
* DNS-Daten Satz Registrierung in Active Directory integrierten DNS-Zonen

Die Größe des einfüglochs kann Hunderte, Tausende oder sogar Zehntausende Änderungen an Benutzern, Computern, Vertrauens Stellungen, Kenn Wörtern und Sicherheitsgruppen darstellen. Das USN-Loch wird durch den Unterschied zwischen der höchsten USN-Zahl definiert, die bei der Wiederherstellung des wiederhergestellten Systemstatus vorhanden war, und der Anzahl der ursprünglichen Änderungen, die auf dem zurückgeführten Domänen Controller vor dem Offline Vorgang erstellt wurden.

## <a name="detecting-a-usn-rollback"></a>Erkennen eines Rollbacks für die Wiederverwendung

Da ein Rollback für ein Rollback schwer zu erkennen ist, protokolliert ein Domänen Controller das Ereignis 2095, wenn ein Quell Domänen Controller eine zuvor bestätigte US-Nummer ohne entsprechende Änderung in der Aufruf-ID an einen Zieldomänen Controller sendet.

Der Anmeldedienst wurde angehalten, um zu verhindern, dass eindeutige Ursprungs Updates Active Directory auf dem falsch wiederhergestellten Domänen Controller erstellt werden. Wenn der Anmeldedienst angehalten wird, können Benutzer-und Computer Konten das Kennwort auf einem Domänen Controller nicht ändern, der nicht in den ausgehender Richtung steht. replizieren Sie diese Änderungen. Ebenso bevorzugen Active Directory Verwaltungs Tools einen fehlerfreien Domänen Controller, wenn Sie Objekte in Active Directory aktualisieren.

Auf einem Domänen Controller werden Ereignismeldungen, die den folgenden ähneln, aufgezeichnet, wenn die folgenden Bedingungen zutreffen:

* Ein Quell Domänen Controller sendet eine zuvor bestätigte US-Nummer an einen Zieldomänen Controller.
* Es gibt keine entsprechende Änderung in der Aufruf-ID.

Diese Ereignisse können im Verzeichnisdienst-Ereignisprotokoll aufgezeichnet werden. Sie können jedoch überschrieben werden, bevor Sie von einem Administrator beobachtet werden.

Wenn Sie vermuten, dass ein Rollback für ein Rollback durchgeführt wurde, aber kein entsprechendes Ereignis in den Ereignisprotokollen angezeigt wird, überprüfen Sie, ob der Registrierungs Eintrag für DSA nicht schreibgeschützt ist. Dieser Eintrag enthält forensische Beweise, dass ein Rollback für ein Rollback durchgeführt wurde.

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Durch Löschen oder manuelles Ändern des Registrierungs Eintrags Werts DSA, der nicht geschrieben werden konnte, wird der Rollback-Domänen Controller in einen permanent nicht unterstützten Zustand Daher werden solche Änderungen nicht unterstützt. Insbesondere wird durch das Ändern des Werts das Quarantäne Verhalten entfernt, das durch den Erkennungs Code der Wiederverwendungs Erkennung hinzugefügt wurde. Die Active Directory Partitionen auf dem Rollback-Domänen Controller sind mit direkten und transitiven Replikations Partnern in derselben Active Directory Gesamtstruktur dauerhaft inkonsistent.

Weitere Informationen zu diesem Registrierungsschlüssel und den Lösungs Schritten finden Sie im Support-Artikel [active Directory-Replikations Fehler 8456 oder 8457: "Die Quelle | der Zielserver lehnt die Replikations Anforderungen zurzeit ab "](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination).

## <a name="virtualization-based-safeguards"></a>Virtualisierungsbasierte Schutzmaßnahmen

Während der Installation des Domänen Controllers speichert AD DS anfänglich den VM-generationid-Bezeichner als Teil des msDS-generationid-Attributs für das Computer Objekt des Domänen Controllers in seiner Datenbank (häufig als Verzeichnis Informationsstruktur oder dit bezeichnet). Die VM-Generations-ID wird von einem Windows-Treiber innerhalb des virtuellen Computers unabhängig nachverfolgt.

Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der VM-Generations-ID aus dem Treiber des virtuellen Computers mit einem Wert in der DIT verglichen.

Unterscheiden sich die beiden Werte, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, um das erneute Verwenden der USN zu verhindern. Sind die Werte identisch, wird die Transaktion normal ausgeführt.

AD DS vergleicht auch bei jedem Neustart des Domänencontrollers den aktuellen Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der DIT. Unterscheiden sich die Werte, wird die Aufrufkennung zurückgesetzt, der RID-Pool verworfen und die DIT mit dem neuen Wert aktualisiert. Außerdem wird der Ordner %%amp;quot;SYSVOL%%amp;quot; nicht autorisierend synchronisiert, um die sichere Wiederherstellung abzuschließen. Dadurch können Schutzvorrichtungen die Anwendung von Momentaufnahmes auf heruntergefahrenen virtuellen Computern erweitern. Diese Sicherheitsvorkehrungen in Windows Server 2012 ermöglichen AD DS Administratoren, von den einzigartigen Vorteilen der Bereitstellung und Verwaltung von Domänen Controllern in einer virtualisierten Umgebung zu profitieren.

In der folgenden Abbildung wird gezeigt, wie virtualisierungsschutzvorrichtungen angewendet werden, wenn auf einem virtualisierten Domänen Controller, auf dem Windows Server 2012 ausgeführt wird, auf einem Hypervisor, der die VM-Generations-ID unterstützt, dasselbe Anwendungs Rollback erkannt wird.

![Sicherheitsvorkehrungen, die angewendet werden, wenn dasselbe Wiederverwendungs-Rollback erkannt wird](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

In diesem Fall werden Virtualisierungsschutzvorrichtungen ausgelöst, wenn der Hypervisor eine Änderung am Wert der VM-Generations-ID erkennt. Dabei wird auch die Aufrufkennung des virtualisierten Domänencontrollers (im vorhergehenden Beispiel von A zu B) zurückgesetzt und der auf dem virtuellen Computer gespeicherte Wert der VM-Generations-ID so aktualisiert, dass er mit dem neuen vom Hypervisor gespeicherten Wert (G2) übereinstimmt. Mit den Schutzvorrichtungen wird sichergestellt, dass die Replikation für beide Domänencontroller zusammengeführt wird.

Mit Windows Server 2012 setzt AD DS Sicherheitsmaßnahmen auf virtuellen Domänen Controllern, die auf VM-generationid-fähigen Hypervisoren gehostet werden, und stellt sicher, dass die versehentliche Anwendung von Momentaufnahmen oder anderen Hypervisor-fähigen Mechanismen, die ein virtuelles der Zustand des Computers beeinträchtigt nicht die AD DS Umgebung (durch verhindern von Replikations Problemen wie z. b. einer USN-Blase oder veralteten Objekten).

Das Wiederherstellen eines Domänen Controllers durch Anwenden einer Momentaufnahme eines virtuellen Computers wird nicht als alternativer Mechanismus zum Sichern eines Domänen Controllers empfohlen. Es wird empfohlen, weiterhin die Windows Server-Sicherung oder andere VSS Writer-basierte Sicherungslösungen zu verwenden.

> [!CAUTION]
> Wenn ein Domänen Controller in einer Produktionsumgebung versehentlich auf eine Momentaufnahme zurückgesetzt wird, empfiehlt es sich, die Anbieter für die Anwendungen und die auf diesem virtuellen Computer gehosteten Dienste zu konsultieren, um eine Anleitung zum Überprüfen des Status dieser Programme zu erhalten. Momentaufnahme Wiederherstellung.

Weitere Informationen finden Sie unter [Virtualized domain controller safe restore architecture](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).

## <a name="recovering-from-a-usn-rollback"></a>Wiederherstellen nach einem Wiederherstellungs-Rollback

Es gibt zwei Ansätze für die Wiederherstellung nach einem Wiederherstellungs-Rollback:

* Entfernen des Domänen Controllers aus der Domäne
* Wiederherstellen des Systemstatus einer guten Sicherung

### <a name="remove-the-domain-controller-from-the-domain"></a>Entfernen des Domänen Controllers aus der Domäne

1. Entfernen Sie Active Directory vom Domänen Controller, um einen eigenständigen Server zu erzwingen.
2. Fahren Sie den herab gedemoerten Server herunter.
3. Bereinigen Sie auf einem fehlerfreien Domänen Controller die Metadaten des herab stufenden Domänen Controllers.
4. Wenn der falsch wiederhergestellte Domänen Controller Betriebs Master Rollen hostet, übertragen Sie diese Rollen auf einen fehlerfreien Domänen Controller.
5. Starten Sie den herab gedemoerten Server neu.
6. Falls erforderlich, installieren Sie Active Directory erneut auf dem eigenständigen Server.
7. Wenn der Domänen Controller zuvor ein globaler Katalog war, konfigurieren Sie den Domänen Controller als globalen Katalog.
8. Wenn der Domänen Controller zuvor Betriebs Master Rollen gehostet hat, übertragen Sie die Betriebs Master Rollen zurück auf den Domänen Controller.

### <a name="restore-the-system-state-of-a-good-backup"></a>Wiederherstellen des Systemstatus einer guten Sicherung

Prüfen Sie, ob für diesen Domänen Controller gültige Systemstatus Sicherungen vorhanden sind. Wenn eine gültige Systemstatus Sicherung erstellt wurde, bevor der Rollback-Domänen Controller ordnungsgemäß wieder hergestellt wurde, und die Sicherung Letzte Änderungen enthält, die auf dem Domänen Controller vorgenommen wurden, stellen Sie den Systemstatus aus der letzten Sicherung wieder her.

Sie können die Momentaufnahme auch als Quelle für eine Sicherung verwenden. Sie können auch festlegen, dass die Datenbank eine neue Aufruf-ID erhält. verwenden Sie dazu das Verfahren im Abschnitt [Wiederherstellen eines virtuellen Domänen Controllers, wenn keine geeignete Systemstatus Daten-Sicherung verfügbar ist](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available) .

## <a name="next-steps"></a>Nächste Schritte

* Weitere Informationen zur Problembehandlung bei virtuellen Domänencontrollern finden Sie unter [Problembehandlung für virtualisierte Domänencontroller](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).
* [Ausführliche Informationen zum Windows-Zeit Dienst (W32Time)](../../networking/windows-time-service/windows-time-service-top.md)
