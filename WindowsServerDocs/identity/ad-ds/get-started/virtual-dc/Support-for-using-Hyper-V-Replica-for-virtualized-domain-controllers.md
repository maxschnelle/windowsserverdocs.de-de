---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: Unterstützung für Hyper-V-Replikate als virtualisierte Domänencontroller
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0203c6de55a4e691d7c484351a3280c49891f317
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866281"
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>Unterstützung für Hyper-V-Replikate als virtualisierte Domänencontroller

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird die Unterstützung für die Verwendung eines Hyper-V-Replikats für die Replikation eines virtuellen Computers (VM) dargestellt, auf dem ein Domänencontroller ausgeführt wird. Das Hyper-V-Replikat ist eine neue Funktion von Hyper-V, die mit Windows Server 2012 eingeführt wurde und einen integrierten Replikationsmechanismus auf VM-Ebene bereitstellt.  
  
Das Hyper-V Replikat repliziert ausgewählte VMs asynchron von einem primären Hyper-V-Host zu einem Replikat-Hyper-V-Host über LAN- oder WAN-Verbindungen. Wenn die erste Replikation abgeschlossen ist, werden nachfolgende Änderungen in einem vom Administrator angegebenen Intervall repliziert.  
  
Das Failover kann geplant oder ungeplant erfolgen. Ein geplantes Failover wird von einem Administrator auf dem primären virtuellen Computer initiiert, und alle nicht replizierten Änderungen werden an den virtuellen Replikatcomputer kopiert, um Datenverluste zu verhindern. Ein ungeplantes Failover wird auf dem virtuellen Replikatcomputer in Reaktion auf einen unerwarteten Ausfall des primären virtuellen Computerts initiiert. Datenverluste sind möglich, da es keine Gelegenheit gibt, Änderungen auf dem primären virtuellen Computer zu übertragen, die möglicherweise noch nicht repliziert wurden.  
  
Weitere Informationen zum Hyper-V-Replikat finden Sie unter [Übersicht über Hyper-V-Replikat](https://technet.microsoft.com/library/jj134172.aspx) und [Bereitstellen des Hyper-V-Replikats](https://technet.microsoft.com/library/jj134207.aspx).  
  
> [!NOTE]  
> Das Hyper-V-Replikat kann nur unter Windows Server Hyper-V ausgeführt werden, nicht unter der Version, die auf Windows 8 ausgeführt wird.  
  
## <a name="windows-server-2012-or-newer-domain-controllers-required"></a>Windows Server 2012 oder höher-Domänencontroller ist erforderlich

Windows Server 2012 Hyper-V, VM-Generations-ID (VMGenID) eingeführt. VMGenID sorgt dafür, dass der Hypervisor mit dem Gastbetriebssysteme kommunizieren kann, wenn bedeutende Änderungen aufgetreten sind. Der Hypervisor kann beispielsweise einem virtualisierten Domänencontroller mitteilen, dass eine Wiederherstellung von einer Momentaufnahme durchgeführt wurde (Hyper-V-Technologie zur Momentaufnahmenwiederherstellung, keine Sicherungswiederherstellung). AD DS in Windows Server 2012 und höher ist die VMGenID VM-Technologie kennen und wird verwendet, um zu erkennen, wann hypervisorvorgänge, beispielsweise eine momentaufnahmenwiederherstellung, erfolgen die sich besser schützen können.  
  
> [!NOTE]
> Nur AD DS für Windows Server 2012-Domänencontroller oder höher bieten diese Sicherheitsmaßnahmen von VMGenID. Domänencontroller mit allen früheren Versionen von Windows Server unterliegen Problemen wie einem USN-Rollback, die auftreten können, wenn ein virtualisiertes Domänencontrollers mithilfe eines nicht unterstützten Mechanismus wie z. B. die Wiederherstellung einer Momentaufnahme wiederhergestellt wird ab. Weitere Informationen zu diesen Sicherheitsmaßnahmen und deren Auslösung finden Sie unter [Architektur für virtualisierte Domänencontroller](https://technet.microsoft.com/library/jj574118.aspx).  
  
Tritt ein Hyper-V-Replikat-Failover (geplant oder ungeplant), erkennt der virtualisierte Domänencontroller eine VMGenID-Zurücksetzung, der zuvor erwähnten Sicherheitsfunktionen ausgelöst. Active Directory-Vorgänge werden dann normal fortgesetzt. Der virtuelle Replikatcomputer wird anstelle des primären virtuellen Computers ausgeführt.  
  
> [!NOTE]  
> Aufgrund der Tatsache, dass jetzt zwei Instanzen derselben Domänencontrolleridentität vorhanden sind, können potenziell sowohl die primäre als auch die replizierte Instanz ausgeführt werden. Zwar bietet das Hyper-V-Replikat Kontrollmechanismen, um sicherzustellen, dass der primäre virtuelle Computer und der virtuelle Replikatcomputer nicht gleichzeitig ausgeführt werden, eine gleichzeitige Ausführung ist aber möglich, wenn die Verknüpfung zwischen ihnen nach der Replikation des virtuellen Computers fehlschlägt. Für diese sehr unwahrscheinliche Situation verfügen virtualisierte Domänencontroller, auf denen Windows Server 2012 ausgeführt wird, im Gegensatz zu virtualisierten Domänencontrollern mit früheren Versionen von Windows Server über Sicherheitsmaßnahmen für den Schutz von AD DS.  
  
Wenn Sie Hyper-V-Replikat verwenden möchten, stellen Sie sicher, müssen Sie bewährte Methoden für die [Ausführen von virtuellen Domänencontrollern auf Hyper-V](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx). In diesem Thema werden z. B. Empfehlungen für das Speichern von Active Directory-Dateien auf virtuellen SCSI-Datenträgern erläutert, die eine höhere Garantie für die Beständigkeit der Daten bieten.  
  
## <a name="supported-and-unsupported-scenarios"></a>Unterstützte und nicht unterstützte Szenarien

Nur virtuelle Computer führen Windows Server 2012 oder höher sind für ein ungeplantes Failover und zum Testen von Failover unterstützt. Sogar für Geplantes Failover wird WindowsServer 2012 oder höher des virtualisierten Domänencontrollers empfohlen, um Risiken zu verringern, wenn ein Administrator versehentlich sowohl der primäre virtuelle Computer als auch den replizierten virtuellen Computer gleichzeitig startet.  
  
Virtuelle Computer mit früheren Versionen von Windows Server werden für geplante Failover unterstützt, für ungeplante Failover aufgrund eines potenziellen USN-Rollback dagegen nicht. Weitere Informationen zu USN-Rollbacks, finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10)).  
  
> [!NOTE]  
> Für die Domäne oder Gesamtstruktur gibt es keine Funktionsebenenanforderungen, sondern nur Betriebssystemanforderungen für die Domänencontroller, die als virtuelle Computer ausgeführt und mithilfe des Hyper-V-Replikats repliziert werden. Die virtuellen Computer können in einer Gesamtstruktur bereitgestellt werden, die andere physische oder virtuelle Domänencontroller enthält, auf denen frühere Versionen von Windows Server ausgeführt und die möglicherweise ebenfalls mithilfe des Hyper-V-Replikats repliziert werden.  
  
Diese Aussage zur Unterstützung basiert auf Tests, die in einer Gesamtstruktur mit einer einzelnen Domäne durchgeführt wurden, obwohl auch Gesamtstrukturkonfigurationen mit mehreren Domänen unterstützt werden. Für diese Tests sind die virtualisierten Domänencontroller DC1 und DC2 Active Directory-Replikationspartner am selben Standort, die auf einem Server mit Hyper-V unter Windows Server 2012 gehostet werden. Auf dem VM-Gast, auf dem DC2 ausgeführt wird, wurde das Hyper-V-Replikat aktiviert. Der Replikatserver wird in einem anderen, geografisch entfernten Rechenzentrum gehostet. Für eine einfachere Erklärung der unten aufgeführten Testfallprozesse wird der virtuelle Computer, der auf dem Replikatserver ausgeführt wird, als DC2-Rec bezeichnet (obwohl er in der Praxis denselben Namen beibehält wie der ursprüngliche virtuelle Computer).  
  
### <a name="windows-server-2012"></a>Windows Server 2012

In der folgenden Tabelle werden die Unterstützung für virtualisierte Domänencontroller mit Windows Server 2012 und Testfälle dargestellt.  
  
|||  
|-|-|  
|Geplantes Failover|Ungeplantes Failover|  
|Unterstützt|Unterstützt|  
|Testfall:<br /><br />-DC1 und DC2 wird Windows Server 2012 ausgeführt.<br /><br />-DC2 wird heruntergefahren, und ein Failover auf DC2-Rec wird durchgeführt. Das Failover kann geplant oder ungeplant sein.<br /><br />– Nachdem DC2-Rec gestartet wurde, er überprüft, ob der Wert für VMGenID, der in der Datenbank identisch mit dem Wert ist vom Treiber virtuellen Computers, von dem Hyper-V-Replikatserver gespeichert.<br /><br />-Daher löst DC2-Rec virtualisierungssicherheitsmaßnahmen; Das heißt, es setzt seine InvocationID, verwirft seinen RID-Pool und legt eine erstsynchronisierung aus, bevor er eine Betriebsmasterrolle wird davon ausgegangen wird. Weitere Information zur Anforderung für die anfängliche Synchronisierung finden Sie unter .<br /><br />-DC2-Rec wird anschließend speichert den neuen Wert für VMGenID in seiner Datenbank und führt einen Commit für alle nachfolgenden Updates im Zusammenhang mit der neuen InvocationID.<br /><br />– Als Ergebnis des das Zurücksetzen der InvocationID wird DC1 konvergieren zu allen AD Änderungen von DC2-Rec eingeführt werden, selbst wenn sie ein Rollback ausgeführt wurde, in-Time, d. h., alle AD-Updates auf DC2-Rec ausgeführt wird, nach dem Failover sicher konvergiert werden|Für ein geplantes Failover ist der Testfall gleich, mit den folgenden Ausnahmen:<br /><br />– Alle AD aktualisiert auf DC2 empfangen, aber noch nicht an einen Replikationspartner von AD repliziert, bevor das failoverereignis verloren geht.<br /><br />-AD-Updates auf DC2 empfangen wird, nachdem die Zeit des Wiederherstellungspunkts, die von AD an DC1 repliziert wurden von DC1 an DC2-Rec repliziert werden.|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 und frühere Versionen

In der folgenden Tabelle werden die Unterstützung für virtualisierte Domänencontroller mit Windows Server 2008 R2 und früheren Versionen dargestellt.  
  
|||  
|-|-|  
|Geplantes Failover|Ungeplantes Failover|  
|Unterstützt, aber nicht empfohlen, da Domänencontroller mit diesen Versionen von Windows Server keine Unterstützung für VMGenID bieten oder damit verbundene Virtualisierungssicherheitsmaßnahmen verwenden. Damit entsteht das Risiko von einem USN-Rollback. Weitere Informationen finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10)).|Nicht unterstützte **beachten:** Ein ungeplantes Failover würde unterstützt werden, wenn ein USN-Rollback kein Risiko ist, beispielsweise bei einem einzelnen Domänencontroller in der Gesamtstruktur (eine Konfiguration, die nicht empfehlenswert ist).|  
|Testfall:<br /><br />-DC1 und DC2 wird Windows Server 2008 R2 ausgeführt.<br /><br />-DC2 wird heruntergefahren, und ein geplantes Failover auf DC2-Rec ausgeführt wird. Alle Daten auf DC2 werden an DC2-Rec repliziert, bevor das Herunterfahren abgeschlossen ist.<br /><br />– Nachdem DC2-Rec gestartet wurde, wird es Replikation mit DC1 mit derselben InvocationID wie DC2 fortgesetzt.|Nicht zutreffend|  
