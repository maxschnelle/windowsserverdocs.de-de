---
title: Sichere Virtualisierung von Active Directory Domain Services (AD DS)
description: USN-Rollback und sichere Virtualisierung von Active Directory
ms.topic: article
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 03/22/2019
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: fbacb87d99bf5b396e119028e15e8a4aa0c9ef53
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88940980"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Sichere Virtualisierung von Active Directory Domain Services (AD DS)

>Gilt für: Windows Server

Ab Windows Server 2012 bietet AD DS durch die Einführung von virtualisierungssicheren Funktionen mehr Unterstützung für das Virtualisieren von Domänencontrollern. In diesem Artikel werden die Rollen von Updatesequenznummern (USNs) und Aufruf-IDs in der Domänencontrollerreplikation sowie mögliche Probleme erläutert.

## <a name="update-sequence-number-and-invocationid"></a>Updatesequenznummer und Aufruf-ID

Virtuelle Umgebungen bedeuten individuelle Herausforderungen für verteilte Arbeitslasten, die von einem logischen taktbasierten Replikationsschema abhängen. Die AD DS-Replikation verwendet beispielsweise einen monoton steigenden Wert (als %%amp;quot;USN%%amp;quot; oder %%amp;quot;Updatesequenznummer%%amp;quot;), der Transaktionen auf jedem Domänencontroller zugewiesen ist. Jeder Datenbankinstanz eines Domänencontrollers wird auch eine Identität zugewiesen, die als Aufruf-ID bezeichnet wird. Die Aufrufkennung eines Domänencontrollers dient in Verbindung mit der USN als eindeutiger Bezeichner, der jeder Schreibtransaktion auf jedem Domänencontroller zugeordnet ist, und innerhalb der Gesamtstruktur eindeutig sein muss.

Die AD DS-Replikation verwendet Aufrufkennungen und USNs auf jedem Domänencontroller, um zu bestimmen, welche Änderungen auf anderen Domänencontrollern repliziert werden müssen. Wenn für einen Domänencontroller ein Rollback außerhalb seines Wirkungsbereichs ausgeführt wird und eine USN für eine vollkommen andere Transaktion wiederverwendet wird, wird die Replikation nicht zusammengeführt, da andere Domänencontroller davon ausgehen, dass sie die der wiederverwendeten USN zugeordneten Aktualisierungen im Kontext der Aufruf-ID bereits erhalten haben.

Die folgende Abbildung veranschaulicht z. B. die Abfolge von Ereignissen in Windows Server 2008 R2 und älteren Betriebssystemen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In der folgenden Abbildung wird das USN-Rollback auf VDC2 erkannt, wenn ein Replikationspartner feststellt, dass VDC2 einen USN-Wert zur Aktualität gesendet hat, der zuvor vom Replikationspartner gesehen wurde. Dies weist darauf hin, dass ein nicht ordnungsgemäßes Rollback für die VDC2-Datenbank durchgeführt wurde.

![Die Ereignisabfolge bei Erkennung eines USN-Rollbacks](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

Mithilfe einer VM (virtueller Computer) können Hypervisoradministratoren ganz einfach ein Rollback für die USNs eines Domänencontrollers (die logische Uhr) durchführen, indem sie beispielsweise eine Momentaufnahme außerhalb des Wirkungsbereichs des Domänencontrollers anwenden. Weitere Informationen zur USN und zum USN-Rollback, einschließlich weiterer Abbildungen zur Veranschaulichung unerkannter Instanzen eines USN-Rollbacks, finden Sie unter [USN and USN Rollback](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553(v=ws.10)#usn_and_usn_rollback).

Ab Windows Server 2012 können virtuelle AD DS-Domänencontroller, die auf Hypervisorplattformen gehostet werden, die den Bezeichner „VM-Generations-ID“ zur Verfügung stellen, erforderliche Sicherheitsmaßnahmen erkennen und anwenden, um die AD DS-Umgebung zu schützen, wenn für die VM ein Rollback mittels Anwendung einer VM-Momentaufnahme durchgeführt wird. Der VM-Generations-ID-Entwurf verwendet einen unabhängigen Mechanismus des Hypervisoranbieters, um diesen Bezeichner im Adressbereich des virtuellen Gastcomputers bereitzustellen, damit die sichere Virtualisierung ständig von jedem Hypervisor verfügbar ist, der VM-Generations-ID unterstützt. Dieser Bezeichner kann von Diensten und Anwendungen verwendet werden, die innerhalb des virtuellen Computers ausgeführt werden, um zu ermitteln, ob für einen virtuellen Computer ein Rollback durchgeführt wurde.

## <a name="effects-of-usn-rollback"></a>Auswirkungen von USN-Rollbacks

Wenn USN-Rollbacks auftreten, werden Änderungen an Objekten und Attributen nicht von Zieldomänencontrollern eingehend repliziert, die die USN zuvor gesehen haben.

Da diese Zieldomänencontroller annehmen, dass sie auf dem neuesten Stand sind, werden keine Replikationsfehler in der AD DS-Ereignisprotokollen oder von Überwachungs- und Diagnosetools gemeldet.

Das USN-Rollback kann sich auf die Replikation von Objekten oder Attributen in beliebigen Partitionen auswirken. Der am häufigsten beobachtete Nebeneffekt ist, dass Benutzer- und Computerkonten, die auf dem Rollbackdomänencontroller erstellt werden, auf einem oder mehreren Replikationspartnern nicht vorhanden sind. Alternativ können Kennwortupdates, die vom Rollbackdomänencontroller stammen, auf Replikationspartnern nicht vorhanden sein.

Ein USN-Rollback kann die Replikation von beliebigen Objekttypen in beliebigen Active Directory-Partitionen verhindern. Zu diesen Objekttypen gehören die folgenden:

* Die Active Directory-Replikationstopologie und -Planung
* Das Vorhandensein von Domänencontrollern in der Gesamtstruktur und die Rollen, die diese Domänencontroller enthalten
* Das Vorhandensein von Domänen- und Anwendungspartitionen in der Gesamtstruktur
* Das Vorhandensein von Sicherheitsgruppen und ihren aktuellen Gruppenmitgliedschaften
* Registrierung des DNS-Eintrags in in Active Directory integrierten DNS-Zonen

Die Menge der fehlenden USNs kann Hunderten, Tausenden oder sogar Zehntausenden Änderungen an Benutzern, Computern, Vertrauensstellungen, Kennwörtern und Sicherheitsgruppen entsprechen. Die Menge der fehlenden USNs wird durch den Unterschied zwischen der höchsten USN, die zum Zeitpunkt der Erstellung der wiederhergestellten Systemstatussicherung vorhanden war, und der Anzahl der Quelländerungen definiert, die auf dem zurückgesetzten Domänencontroller erstellt wurden, bevor dieser offline geschaltet wurde.

## <a name="detecting-a-usn-rollback"></a>Erkennen eines USN-Rollbacks

Da es schwierig ist, ein USN-Rollback zu erkennen, protokolliert ein Domänencontroller das Ereignis 2095, wenn ein Quelldomänencontroller eine zuvor anerkannte USN-Zahl ohne eine entsprechende Änderung an der Aufrufs-ID an einen Zieldomänencontroller sendet.

Der Anmeldedienst wird angehalten, um die Erstellung eindeutiger Quellupdates für Active Directory auf dem nicht ordnungsgemäß wiederhergestellten Domänencontroller zu verhindern. Wenn der Anmeldedienst angehalten wurde, können Benutzer- und Computerkonten das Kennwort eines Domänencontrollers nicht ändern, der solche Änderungen nicht ausgehend repliziert. Ebenso bevorzugen Active Directory-Verwaltungstools einen fehlerfreien Domänencontroller, wenn sie Updates an Objekten in Active Directory vornehmen.

Wenn die folgenden Bedingungen auf einem Domänencontroller vorliegen, werden Ereignismeldungen ähnlich den folgenden aufgezeichnet:

* Ein Quelldomänencontroller sendet eine zuvor anerkannte USN-Zahl an einen Zieldomänencontroller.
* Es liegt keine entsprechende Änderung in der Aufruf-ID vor.

Diese Ereignisse können im Directory Service-Ereignisprotokoll erfasst werden. Sie können jedoch überschrieben werden, bevor ein Administrator sie sieht.

Wenn Sie vermuten, dass ein USN-Rollback aufgetreten ist, aber kein entsprechendes Ereignis in den Ereignisprotokollen finden können, prüfen Sie die Registrierung auf den Eintrag „DSA Not Writable“ (in den Verzeichnissystem-Agent kann nicht geschrieben werden). Dieser Eintrag bietet forensische Beweise für das Auftreten eines USN-Rollbacks.

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Durch Löschen oder manuelles Ändern des Registrierungseintragswerts „DSA Not Writable“ wird der Rollbackdomänencontroller permanent in einen nicht unterstützten Status versetzt. Daher werden solche Änderungen nicht unterstützt. Durch das Ändern des Werts wird das Quarantäneverhalten entfernt, das durch den USN-Rollbackerkennungscode hinzugefügt wird. Die Active Directory-Partitionen auf dem Rollbackdomänencontroller werden dauerhaft inkonsistent mit direkten und transitiven Replikationspartnern in derselben Active Directory-Gesamtstruktur sein.

Weitere Informationen zu diesem Registrierungsschlüssel und den Lösungsschritten finden Sie im Supportartikel [Active Directory-Replikationsfehler 8456 oder 8457: „Der Quell-/Zielserver nimmt zurzeit keine Replikationsanforderungen entgegen“](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination).

## <a name="virtualization-based-safeguards"></a>Virtualisierungsbasierte Sicherheitsmaßnahmen

Während der Installation des Domänencontrollers speichert AD DS den Bezeichner „VM-Generations-ID“ als Teil des Attributs „msDS-GenerationID“ im Computerobjekt des Domänencontrollers in dessen Datenbank (oft als Verzeichnisinformationsstruktur oder DIT (Directory Information Tree) bezeichnet). Die VM-Generations-ID wird von einem Windows-Treiber innerhalb des virtuellen Computers unabhängig nachverfolgt.

Wenn ein Administrator den virtuellen Computer aus einem früheren Momentaufnahme wiederherstellt, wird der aktuelle Wert der VM-Generations-ID aus dem Treiber des virtuellen Computers mit einem Wert in der DIT verglichen.

Unterscheiden sich die beiden Werte, wird die Aufrufkennung zurückgesetzt und der RID-Pool verworfen, um das erneute Verwenden der USN zu verhindern. Sind die Werte identisch, wird die Transaktion normal ausgeführt.

AD DS vergleicht auch bei jedem Neustart des Domänencontrollers den aktuellen Wert der VM-Generations-ID des virtuellen Computers mit dem Wert in der DIT. Unterscheiden sich die Werte, wird die Aufrufkennung zurückgesetzt, der RID-Pool verworfen und die DIT mit dem neuen Wert aktualisiert. Außerdem wird der Ordner %%amp;quot;SYSVOL%%amp;quot; nicht autorisierend synchronisiert, um die sichere Wiederherstellung abzuschließen. Dadurch können Schutzvorrichtungen die Anwendung von Momentaufnahmen auf heruntergefahrenen virtuellen Computern erweitern. Diese in Windows Server 2012 eingeführten Sicherheitsmaßnahmen ermöglichen AD DS-Administratoren die Nutzung der einzigartigen Vorteile der Bereitstellung und Verwaltung von Domänencontrollern in einer virtualisierten Umgebung.

In der folgenden Abbildung wird veranschaulicht, wie Virtualisierungsschutzvorrichtungen angewendet werden, wenn dasselbe USN-Rollback auf einem virtualisierten Domänencontroller erkannt wird, der Windows Server 2012 auf einem Hypervisor ausführt, der die VM-Generations-ID unterstützt.

![Bei Erkennung desselben USN-Rollbacks angewendete Sicherheitsmaßnahmen](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

In diesem Fall werden Virtualisierungsschutzvorrichtungen ausgelöst, wenn der Hypervisor eine Änderung am Wert der VM-Generations-ID erkennt. Dabei wird auch die Aufrufkennung des virtualisierten Domänencontrollers (im vorhergehenden Beispiel von A zu B) zurückgesetzt und der auf dem virtuellen Computer gespeicherte Wert der VM-Generations-ID so aktualisiert, dass er mit dem neuen vom Hypervisor gespeicherten Wert (G2) übereinstimmt. Mit den Schutzvorrichtungen wird sichergestellt, dass die Replikation für beide Domänencontroller zusammengeführt wird.

In Windows Server 2012 verwendet AD DS Sicherheitsmaßnahmen auf virtuellen Domänencontrollern, die auf VM-Generations-ID-fähigen Hypervisoren gehostet werden, und stellt sicher, dass die versehentliche Anwendung von Momentaufnahmen oder ähnlicher Hypervisor-fähigen Mechanismen, die ein Rollback für den Status einer VM durchführen könnten, die AD DS-Umgebung nicht beeinträchtigt (durch Verhindern von Replikationsproblemen wie z. B. einer USN Bubble oder veralteten Objekten).

Das Wiederherstellen eines Domänencontrollers mittels Anwendung einer VM-Momentaufnahme wird jedoch nicht als Alternativmechanismus zum Sichern eines Domänencontrollers empfohlen. Es wird empfohlen, weiterhin die Windows Server-Sicherung oder andere VSS Writer-basierte Sicherungslösungen zu verwenden.

> [!CAUTION]
> Wenn ein Domänencontroller in einer Produktionsumgebung versehentlich auf eine Momentaufnahme zurückgesetzt wird, wird empfohlen, sich an die Anbieter der Anwendungen und der auf dieser VM gehosteten Dienste zu wenden, um Anweisungen zum Überprüfen der Status dieser Programme nach der Momentaufnahmenwiederherstellung zu erhalten.

Weitere Informationen finden Sie unter [Virtualized domain controller safe restore architecture](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).

## <a name="recovering-from-a-usn-rollback"></a>Wiederherstellung nach einem USN-Rollback

Es gibt zwei Ansätze für die Wiederherstellung nach einem USN-Rollback:

* Entfernen des Domänencontrollers aus der Domäne
* Wiederherstellen des Systemstatus einer fehlerfreien Sicherung

### <a name="remove-the-domain-controller-from-the-domain"></a>Entfernen des Domänencontrollers aus der Domäne

1. Entfernen Sie Active Directory aus dem Domänencontroller, um ihn als eigenständigen Server zu erzwingen.
2. Fahren Sie den herabgestuften Server herunter.
3. Bereinigen Sie die Metadaten des herabgestuften Domänencontrollers über einen fehlerfreien Domänencontroller.
4. Wenn der fehlerhaft wiederhergestellte Domänencontroller Betriebsmasterrollen hostet, übertragen Sie diese Rollen auf einen fehlerfreien Domänencontroller.
5. Starten Sie den herabgestuften Server neu.
6. Installieren Sie Active Directory bei Bedarf erneut auf dem eigenständigen Server.
7. Wenn der Domänencontroller zuvor ein globaler Katalog war, konfigurieren Sie den Domänencontroller erneut als globalen Katalog.
8. Wenn der Domänencontroller zuvor Betriebsmasterrollen gehostet hat, übertragen Sie die Betriebsmasterrollen zurück auf den Domänencontroller.

### <a name="restore-the-system-state-of-a-good-backup"></a>Wiederherstellen des Systemstatus einer fehlerfreien Sicherung

Werten Sie aus, ob gültige Systemstatussicherungen für diesen Domänencontroller vorhanden sind. Wenn eine gültige Systemstatussicherung erstellt wurde, bevor die fehlerhafte Wiederherstellung des Domänencontrollers ausgeführt wurde, für den ein Rollback durchgeführt wurde, und die Sicherung aktuelle Änderungen enthält, die auf dem Domänencontroller durchgeführt wurden, stellen Sie den Systemstatus aus der aktuellsten Sicherung wieder her.

Sie können die Momentaufnahme auch als Sicherungsquelle verwenden. Alternativ können Sie die Datenbank so einrichten, dass sie sich selbst eine neue Aufrufs-ID erteilt, indem Sie die Vorgehensweise aus dem Abschnitt [Wiederherstellen eines virtuellen Domänencontrollers, wenn keine entsprechende Sicherung der Systemstatusdaten verfügbar ist](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available) durchführen.

## <a name="next-steps"></a>Nächste Schritte

* Weitere Informationen zur Problembehandlung bei virtuellen Domänencontrollern finden Sie unter [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).
* [Ausführliche Informationen zum Windows-Zeitdienst (W32Time)](../../networking/windows-time-service/windows-time-service-top.md)
