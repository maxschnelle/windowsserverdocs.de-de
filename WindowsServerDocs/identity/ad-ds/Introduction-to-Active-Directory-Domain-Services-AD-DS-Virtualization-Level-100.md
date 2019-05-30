---
title: Sichere Virtualisierung von Active Directory Domain Services (AD DS)
description: Ein USN-Rollback und sichere Virtualisierung von Active Directory
ms.topic: article
ms.prod: windows-server-threshold
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: aa84e09e8a958193fee82c7b9c03cd1dca910c55
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2019
ms.locfileid: "63684180"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Sichere Virtualisierung von Active Directory Domain Services (AD DS)

>Gilt für: Windows Server

Ab Windows Server 2012 bietet AD DS mehr Unterstützung für das Virtualisieren von Domänencontrollern, indem virtualisierungssichere Funktionen eingeführt. Dieser Artikel erläutert die Rolle des USNs und InvocationIDs in der Domänencontroller-Replikation, und es wird erläutert, welche Probleme, die auftreten können.

## <a name="update-sequence-number-and-invocationid"></a>Aktualisierungssequenznummer und InvocationID

Virtuelle Umgebungen bedeuten individuelle Herausforderungen für verteilte Arbeitslasten, die von einem logischen taktbasierten Replikationsschema abhängen. Die AD DS-Replikation verwendet beispielsweise einen monoton steigenden Wert (als %%amp;quot;USN%%amp;quot; oder %%amp;quot;Updatesequenznummer%%amp;quot;), der Transaktionen auf jedem Domänencontroller zugewiesen ist. Jeder Domänencontroller-Datenbank-Instanz erhält auch eine Identität, einen InvocationID genannt. Die Aufrufkennung eines Domänencontrollers dient in Verbindung mit der USN als eindeutiger Bezeichner, der jeder Schreibtransaktion auf jedem Domänencontroller zugeordnet ist, und innerhalb der Gesamtstruktur eindeutig sein muss.

Die AD DS-Replikation verwendet Aufrufkennungen und USNs auf jedem Domänencontroller, um zu bestimmen, welche Änderungen auf anderen Domänencontrollern repliziert werden müssen. Wenn ein Domänencontroller ein außerhalb seines Wirkungsbereichs die Rollback wird und eine USN für eine vollkommen andere Transaktion wiederverwendet wird, wird die Replikation nicht zusammengeführt, da andere Domänencontroller davon ausgehen werden, dass sie die Updates bereits empfangen haben der wiederverwendeten USN im Kontext der Aufrufkennung zugeordnet ist.

Die folgende Abbildung veranschaulicht z. B. die Abfolge von Ereignissen in Windows Server 2008 R2 und älteren Betriebssystemen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In dieser Abbildung wird das USN-Rollback auf VDC2, wenn ein Replikationspartner feststellt, dass VDC2 einen aktualitäts-USN-Wert gesendet hat, der zuvor vom Replikationspartner, aufgetreten ist, gibt an, dass die Datenbank von VDC2 des Rollback hat nicht ordnungsgemäß.

![Die Abfolge der Ereignisse, wenn ein USN-Rollback erkannt wird](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

Ein virtuellen Computer (VM) erleichtert hypervisoradministratoren einer Domäne des Controllers USNs (die logische Uhr), ein Rollback z. B. eine Momentaufnahme außerhalb seines Wirkungsbereichs der angewendet. Weitere Informationen zur USN und zum USN-Rollback, einschließlich weiterer Abbildungen zur Veranschaulichung unerkannter Instanzen eines USN-Rollbacks, finden Sie unter [USN and USN Rollback](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback).

Ab Windows Server 2012, AD DS virtuelle Domänencontroller gehostet, die auf Hypervisor-Plattformen, die Bezeichner mit VM-Generations-ID ermitteln und bereitstellen, erforderlichen Sicherheitsmaßnahmen auf die AD DS-Umgebung zu schützen, wenn der virtuelle Computer ein Rollback ausgeführt wird in der Zeit von der Anwendung von einer VM-Momentaufnahme. Der VM-Generations-ID-Entwurf verwendet einen unabhängigen Mechanismus des Hypervisoranbieters, um diesen Bezeichner im Adressbereich des virtuellen Gastcomputers bereitzustellen, damit die sichere Virtualisierung ständig von jedem Hypervisor verfügbar ist, der VM-Generations-ID unterstützt. Dieser Bezeichner kann von Diensten und Anwendungen verwendet werden, die innerhalb des virtuellen Computers ausgeführt werden, um zu ermitteln, ob für einen virtuellen Computer ein Rollback durchgeführt wurde.

## <a name="effects-of-usn-rollback"></a>Auswirkungen des USN-rollback

Bei USN-Rollbacks werden Änderungen an Objekten und Attributen nicht eingehende repliziert von Ziel-Domänencontrollern, die zuvor die USN gesehen haben.

Da diese Zieldomänencontroller, dass sie auf dem neuesten Stand sind angenommen, werden keine Replikationsfehler gemeldet, im Verzeichnisdienst-Ereignisprotokollen oder mithilfe der überwachungs-und Diagnosetools.

Ein USN-Rollback kann die Replikation aller Objekte oder Attribute in einer beliebigen Partition auswirken. Die meisten Nebeneffekt ist, dass die Benutzerkonten und Computerkonten, die auf dem Rollback-Domänencontroller erstellt werden auf mindestens einem Replikationspartner nicht vorhanden sind. Oder der Aktualisierung von Kennwörtern, die auf dem Rollback-Domänencontroller stammen, sind nicht auf den Replikationspartner.

Ein USN-Rollback kann einen beliebigen Objekttyp in jeder Active Directory-Partition Replikation verhindern. Die folgenden: Objekttypen aus

* Die Active Directory-Replikationstopologie und den Zeitplan
* Das Vorhandensein von Domänencontrollern in der Gesamtstruktur und die Rollen, die diesen Domänencontroller enthalten
* Das Vorhandensein von Domänen- und Partitionen in der Gesamtstruktur
* Das Vorhandensein von Sicherheitsgruppen und ihren aktuellen Gruppenmitgliedschaften
* DNS-Einträgen Registrierung in Active Directory-integrierte DNS-Zonen

Die Größe der USN Lücke kann Hunderte, Tausende oder sogar Zehntausende von Änderungen für Benutzer, Computer, Vertrauensstellungen, Kennwörter und Sicherheitsgruppen darstellen. Die USN-Lücke wird definiert, durch den Unterschied zwischen der höchsten USN Anzahl, die vorhanden waren, wenn die Sicherung des wiederhergestellten Systemstatus erstellt wurde und die ändert sich der Anzahl der stammen, die auf dem Rollback-Domänencontroller erstellt wurden, bevor sie offline geschaltet wurde.

## <a name="detecting-a-usn-rollback"></a>Erkennen von einem USN-rollback

Da es sich bei ein USN-Rollback nur schwer zu erkennen ist, protokolliert ein Domänencontroller Ereignis 2095, wenn einem Quelldomänencontroller zahlreiche USN zuvor bestätigt an einem Zieldomänencontroller ohne eine entsprechende Änderung der aufrufkennung. sendet

Um zu verhindern, dass ist eindeutig, die Updates in Active Directory erstellt werden, auf dem falsch wiederhergestellten Domänencontroller stammen der Netlogon-Dienst wurde angehalten. Wenn der Anmeldedienst angehalten wird, können Benutzer- und Computerkonten nicht das Kennwort auf einem Domänencontroller ändern, die keine ausgehenden Änderungen replizieren werden. Active Directory-Verwaltungstools werden auf ähnliche Weise einen fehlerfreien Domänencontroller bevorzugt, wenn sie Updates für Objekte in Active Directory.

Auf einem Domänencontroller werden die ereignismeldungen, die wie folgt aussehen aufgezeichnet, wenn die folgenden Bedingungen erfüllt sind:

* Einem Quelldomänencontroller sendet eine zuvor bestätigte USN-Reihe an einem Zieldomänencontroller.
* Es gibt keine entsprechende Änderung in die Aufruf-ID.

Diese Ereignisse können in das Verzeichnisdienst-Ereignisprotokoll erfasst werden. Sie können jedoch überschrieben werden, bevor sie von einem Administrator festgestellt werden.

Wenn Sie vermuten, dass ein USN-Rollback ist aufgetreten, aber ein entsprechendes Ereignis im Ereignisprotokoll überprüfen Sie Protokolle für die Beschleunigung dynamischer Websites ist nicht schreibbar Eintrag in der Registrierung nicht angezeigt. Dieser Eintrag enthält gerichtlicher Beweis, dass ein USN-Rollback aufgetreten ist.

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Löschen oder ändern manuell die Beschleunigung dynamischer Websites ist nicht schreibbar registrierungseintragswert setzt sich die Rollback-Domänencontroller in einer dauerhaft nicht unterstützten Zustand. Aus diesem Grund werden diese Änderungen nicht unterstützt. Insbesondere entfernt das Ändern des Werts der Quarantäne-Verhalten hinzugefügt, indem der USN-Rollback-Erkennungscode aus. Die Active Directory-Partitionen, auf dem Rollback-Domänencontroller werden dauerhaft inkonsistent mit Replikationspartnern direkte und transitive, in der gleichen Active Directory-Gesamtstruktur.

Weitere Informationen zu dieser Registrierung Schlüssel und Auflösung Schritten finden Sie im Supportartikel [Active Directory-Replikation Fehler 8456 oder 8457: "Der Quelle | Zielserver lehnt replikationsanforderungen derzeit"](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination).

## <a name="virtualization-based-safeguards"></a>Grundlage Virtualisierungs-Sicherheitsmaßnahmen

Während der Installation des Domänencontrollers speichert AD DS den Bezeichner VM-Generations-ID anfänglich als Teil des MsDS-GenerationID-Attributs auf die Domänencontroller Computerobjekt in der Datenbank (häufig als Verzeichnisinformationsstruktur oder DIT bezeichnet). Die VM-Generations-ID wird von einem Windows-Treiber innerhalb des virtuellen Computers unabhängig nachverfolgt.

Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der VM-Generations-ID aus dem Treiber des virtuellen Computers mit einem Wert in der DIT verglichen.

Unterscheiden sich die beiden Werte, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, um das erneute Verwenden der USN zu verhindern. Sind die Werte identisch, wird die Transaktion normal ausgeführt.

AD DS vergleicht auch bei jedem Neustart des Domänencontrollers den aktuellen Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der DIT. Unterscheiden sich die Werte, wird die Aufrufkennung zurückgesetzt, der RID-Pool verworfen und die DIT mit dem neuen Wert aktualisiert. Außerdem wird der Ordner %%amp;quot;SYSVOL%%amp;quot; nicht autorisierend synchronisiert, um die sichere Wiederherstellung abzuschließen. Dadurch können Schutzvorrichtungen die Anwendung von Momentaufnahmes auf heruntergefahrenen virtuellen Computern erweitern. Diese in Windows Server 2012 eingeführten Schutzvorrichtungen ermöglichen AD DS-Administratoren zum Nutzen der individuellen Vorteile der Bereitstellung und Verwaltung von Domänencontrollern in einer virtualisierten Umgebung.

Die folgende Abbildung zeigt, wie virtualisierungsschutzvorrichtungen angewendet werden, wenn dasselbe USN-Rollback auf einem virtualisierten Domänencontroller erkannt wird, die Windows Server 2012 auf einem Hypervisor ausgeführt wird, die VM-Generations-ID unterstützt.

![Sicherheitsmaßnahmen angewendet, wenn dasselbe USN-Rollback erkannt wird](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

In diesem Fall werden Virtualisierungsschutzvorrichtungen ausgelöst, wenn der Hypervisor eine Änderung am Wert der VM-Generations-ID erkennt. Dabei wird auch die Aufrufkennung des virtualisierten Domänencontrollers (im vorhergehenden Beispiel von A zu B) zurückgesetzt und der auf dem virtuellen Computer gespeicherte Wert der VM-Generations-ID so aktualisiert, dass er mit dem neuen vom Hypervisor gespeicherten Wert (G2) übereinstimmt. Mit den Schutzvorrichtungen wird sichergestellt, dass die Replikation für beide Domänencontroller zusammengeführt wird.

In Windows Server 2012 AD DS Schutzvorrichtungen auf virtuellen Domänencontrollern, die auf VM-Generations-ID-fähigen Hypervisoren gehostet werden soll, und stellt sicher, dass die versehentliche Anwendung von Momentaufnahmen oder ähnlicher Hypervisor-fähigen Mechanismen, die ein Rollback einer virtuellen könnten Status des Computers ist die AD DS-Umgebung nicht unterbrochen werden (durch Verhindern von Replikationsproblemen wie z. B. einer USN-Blase oder veralteten Objekten).

Wiederherstellen eines Domänencontrollers durch Anwenden einer Momentaufnahme des virtuellen Computers sollte nicht als alternativmechanismus zum Sichern auf eines Domänencontrollers. Es wird empfohlen, weiterhin die Windows Server-Sicherung oder andere VSS Writer-basierte Sicherungslösungen zu verwenden.

> [!CAUTION]
> Wenn ein Domänencontroller in einer produktionsumgebung versehentlich mit einer Momentaufnahme wiederhergestellt wird, wird empfohlen, dass Sie die Hersteller für Anwendungen und Dienste, die auf diesem virtuellen Computer, um Anweisungen zum Überprüfen des Status dieser Programme nach gehostet werden. Wenden Sie sich an Wiederherstellung einer Momentaufnahme.

Weitere Informationen finden Sie unter [Virtualized domain controller safe restore architecture](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).

## <a name="recovering-from-a-usn-rollback"></a>Wiederherstellung nach einem USN-rollback

Es gibt zwei Ansätze zur Wiederherstellung nach eines USN-Rollbacks:

* Entfernen Sie den Domänencontroller aus der Domäne
* Wiederherstellen Sie Systemstatus einer fehlerfreien Sicherung.

### <a name="remove-the-domain-controller-from-the-domain"></a>Entfernen Sie den Domänencontroller aus der Domäne

1. Entfernen von Active Directory vom Domänencontroller werden von einem eigenständigen Server erzwingen.
2. Fahren Sie den tiefer gestuften Server herunter.
3. Bereinigen Sie die Metadaten des herabgestuften Domänencontrollers auf einem fehlerfreien Domänencontroller aus.
4. Wenn der Fehler bei der Wiederherstellung den Betrieb von Domänencontrollern Hosts Rollen zu bewahren, übertragen Sie diese Rollen zu einem fehlerfreien Domänencontroller.
5. Starten Sie den tiefer gestuften Server neu.
6. Falls erforderlich sind, installieren Sie Active Directory erneut auf dem eigenständigen Server.
7. Wenn der Domänencontroller bereits ein globaler Katalog eingesetzt wurde, konfigurieren Sie den Domänencontroller als globalen Katalog.
8. Wenn der Domänencontroller zuvor Betriebsmasterfunktionen gehostet, übertragen Sie die Vorgänge, mit dem Domänencontroller Betriebsmasterrollen zu sichern.

### <a name="restore-the-system-state-of-a-good-backup"></a>Wiederherstellen Sie Systemstatus einer fehlerfreien Sicherung.

Bewerten Sie, ob gültige systemstatussicherungen für diesen Domänencontroller vorhanden sind. Wenn eine gültige systemstatussicherung erstellt wurde, bevor der Rollback-Domänencontroller wurde nicht ordnungsgemäß wiederhergestellt, und die Sicherung enthält Änderungen, die auf dem Domänencontroller vorgenommen wurden, stellen Sie den Systemstatus aus der letzten Sicherung wieder her.

Sie können die Momentaufnahme auch als Quelle für eine Sicherung verwenden. Oder Sie können festlegen, dass die Datenbank selbst Geben Sie eine neue Aufruf-ID, die mit dem Verfahren im Abschnitt [Wiederherstellen eines virtualisierten Domänencontrollers, wenn Daten einen entsprechenden systemstatussicherung nicht verfügbar ist.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available)

## <a name="next-steps"></a>Nächste Schritte

* Weitere Informationen zur Problembehandlung bei virtuellen Domänencontrollern finden Sie unter [Problembehandlung für virtualisierte Domänencontroller](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).
* [Ausführliche Informationen zu Windows-Zeitdienst (W32Time)](../../networking/windows-time-service/windows-time-service-top.md)
