---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: "Unterstützung für die Verwendung von Hyper-V-Replikat für virtualisierte Domänencontroller"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0444198196ed08a22aba92a0f59cc6e7a2518a2e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>Unterstützung für die Verwendung von Hyper-V-Replikat für virtualisierte Domänencontroller

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird erläutert, die Unterstützung der Verwendung von Hyper-V-Replikat auf einen virtuellen Computer (VM) replizieren, der als Domänencontroller (DC) ausgeführt wird. Hyper-V-Replikat ist eine neue Funktion von Hyper-V, beginnend mit Windows Server2012, der einen integrierten Replikationsmechanismus auf VM-Ebene bereitstellt.  
  
Hyper-V-Replikat repliziert ausgewählte VMs asynchron von einem primären Hyper-V-Host zu einem Replikat-Hyper-V-Host über LAN- oder WAN-Verbindungen. Nachdem die erste Replikation abgeschlossen ist, werden nachfolgende Änderungen in einem vom Administrator definierten Intervall repliziert.  
  
Failover kann geplant oder ungeplant sein. Ein geplantes Failover von einem Administrator auf dem primären virtuellen Computer initiiert wird, und alle nicht replizierten Änderungen auf das Replikat-VM, um Datenverluste zu verhindern, dass kopiert werden. Ein ungeplantes Failover wird auf dem virtuellen Replikatcomputer in Reaktion auf einen unerwarteten Ausfall des primären virtuellen Computers initiiert. Datenverluste sind möglich, da es besteht keine Möglichkeit, Änderungen auf dem primären virtuellen Computer zu übertragen, die möglicherweise noch nicht repliziert worden sind.  
  
Weitere Informationen zu Hyper-V-Replikat finden Sie unter [Übersicht über die Hyper-V-Replikat](https://technet.microsoft.com/library/jj134172.aspx) und [Bereitstellen des Hyper-V-Replikats](https://technet.microsoft.com/library/jj134207.aspx).  
  
> [!NOTE]  
> Hyper-V-Replikat kann nur unter Windows Server Hyper-V, nicht die Version von Hyper-V ausgeführt werden, die unter Windows8 ausgeführt wird.  
  
## <a name="windows-server-2012-domain-controllers-required"></a>Windows Server2012-Domänencontroller erforderlich  
Windows Server2012 Hyper-V wird auch VM-GenerationID (VMGenID) eingeführt. VMGenID sorgt für den Hypervisor Gastbetriebssystem kommunizieren, wenn bedeutende Änderungen aufgetreten sind. Der Hypervisor kann beispielsweise einem virtualisierten Domänencontroller kommunizieren, dass eine Wiederherstellung von Snapshots (Hyper-V-Technologie zur momentaufnahmenwiederherstellung, keine Sicherungswiederherstellung) aufgetreten ist. AD DS in Windows Server2012 ist sich bewusst VMGenID VM-Technologie und verwendet diese erkennen, wenn der die hypervisorvorgänge, beispielsweise eine momentaufnahmenwiederherstellung, ausgeführt werden besser schützen kann.  
  
> [!NOTE]  
> Um den Punkt zu unterstreichen, bietet nur AD DS in Windows Server2012-Domänencontrollern diese Sicherheitsmaßnahmen von VMGenID. Domänencontroller, auf denen alle frühere Versionen von Windows Server ausgeführt werden Probleme, z.B. ein USN-Rollback, die auftreten können, wenn ein virtualisiertes Domänencontrollers mithilfe einer nicht unterstützten Mechanismus wie die Wiederherstellung einer Momentaufnahme wiederhergestellt wird. Weitere Informationen zu diesen Sicherheitsmaßnahmen und deren Auslösung finden Sie unter [Architektur von virtualisierten Domänencontrollern](https://technet.microsoft.com/library/jj574118.aspx).  
  
Tritt ein Failover der Hyper-V-Replikat (geplant oder ungeplant), erkennt Windows Server2012 virtualisierte Domänencontroller eine VMGenID-Zurücksetzung, die zuvor erwähnten Sicherheitsfunktionen ausgelöst. Active Directory-Vorgänge fahren dann normal fort. Das Replikat wird VM anstelle der primären virtuellen Computer ausgeführt.  
  
> [!NOTE]  
> Angesichts der Tatsache, dass jetzt jetzt zwei Instanzen derselben domänencontrolleridentität sind, besteht die Möglichkeit für die erste Instanz und die replizierte Instanz ausgeführt. Während der Hyper-V-Replikat Kontrollmechanismen, um den primären sicherzustellen und Replikat virtuelle Computer nicht gleichzeitig ausführen, ist es möglich, gleichzeitig ausgeführt werden soll, im Ereignisprotokoll der Verknüpfung zwischen ihnen nach der Replikation des virtuellen Computers ein Fehler auftritt. Diese sehr unwahrscheinliche Situation verfügen virtualisierte Domänencontroller, auf denen Windows Server2012 ausgeführt Sicherheitsmaßnahmen helfen, Schutz von AD DS, virtualisierten, auf denen frühere Versionen von Windows Server ausgeführt nicht.  
  
Wenn Sie Hyper-V-Replikat verwenden, stellen Sie sicher, dass Sie bewährte Methoden für die Folgen [Ausführen von virtuellen Domänencontrollern in Hyper-V](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx). Dies wird erläutert, z.B. Empfehlungen für das Speichern von Active Directory-Dateien auf virtuellen SCSI-Laufwerke, die eine höhere Garantie der Beständigkeit der Daten.  
  
## <a name="supported-and-unsupported-scenarios"></a>Unterstützte und nicht unterstützte Szenarien  
Nur virtuelle Computer, auf denen Windows Server2012 ausgeführt werden für ungeplante und Testfailovers unterstützt. Auch für ein geplantes Failover wird Windows Server2012 des virtualisierten Domänencontrollers empfohlen, um Risiken zu verringern, wenn ein Administrator versehentlich sowohl den primären virtuellen Computer und den replizierten virtuellen Computer gleichzeitig startet.  
  
Virtuelle Computer, auf denen frühere Versionen von Windows Server ausgeführt werden für geplante Failover unterstützt, aber nicht unterstützt für ungeplante Failover aufgrund eines potenziellen USN-Rollback. Weitere Informationen zu USN-Rollbacks finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10)).  
  
> [!NOTE]  
> Es gibt keine Anforderungen bezüglich der Funktionsebene für die Domäne oder Gesamtstruktur. Es gibt nur betriebssystemanforderungen für die Domänencontroller, die als virtuelle Computer ausgeführt wird, die mithilfe des Hyper-V-Replikats repliziert werden. Die virtuellen Computer können in einer Gesamtstruktur bereitgestellt werden, die andere physische oder virtuelle Domänencontroller enthält, die frühere Versionen von Windows Server ausgeführt und können möglicherweise nicht auch repliziert werden mithilfe von Hyper-V-Replikat.  
  
Diese Aussage zur Unterstützung basiert auf Tests, die in einer einzelnen Domäne-Gesamtstruktur ausgeführt wurden, obwohl auch Gesamtstrukturkonfigurationen mit mehreren Domänen unterstützt werden. Für diese Tests sind die virtualisierten Domänencontroller DC1 und DC2 Active Directory-Replikationspartner am selben Standort, auf einem Server mit Hyper-V unter Windows Server2012 gehostet. Die VM-Gast, der DC2 ausgeführt wird, hat Hyper-V-Replikat aktiviert. Der Replikatserver wird in einem anderen, geografisch entfernten Rechenzentrum gehostet. Die um unten beschriebenen Testfall Prozesse zu erklären, wird der virtuelle Computer auf dem Replikatserver ausgeführt als DC2-Rec bezeichnet (auch in der Praxis denselben Namen wie der ursprüngliche virtuelle Computer werden beibehalten).  
  
### <a name="windows-server-2012"></a>Windows Server 2012  
In der folgende Tabelle werden die Unterstützung für virtualisierte Domänencontroller, auf denen Windows Server2012 und Testfälle ausgeführt.  
  
|||  
|-|-|  
|Geplantes Failover|Ungeplantes Failover|  
|Unterstützt|Unterstützt|  
|Testfall:<br /><br />-DC1 und DC2 wird Windows Server2012 ausgeführt.<br /><br />-DC2 wird heruntergefahren, und ein Failover auf DC2-Rec wird durchgeführt. Das Failover kann geplant oder ungeplant sein.<br /><br />: Nachdem DC2-Rec gestartet wird, überprüft er, ob der Wert für VMGenID, der in der Datenbank identisch mit dem Wert ist aus dem Treiber des virtuellen Computers vom Hyper-V-Replikatserver gespeichert.<br /><br />-Daher löst DC2-Rec virtualisierungssicherheitsmaßnahmen; Anders ausgedrückt, setzt seine InvocationID zurück, verwirft seinen RID-Pool und legt eine Anforderung für die erste Synchronisierung, bevor er eine Betriebsmasterrolle übernimmt. Weitere Informationen über erforderliche anfängliche Synchronisierung finden Sie unter.<br /><br />-DC2-Rec speichert den neuen Wert für VMGenID in seiner Datenbank und führt einen Commit für alle nachfolgenden Updates im Zusammenhang mit der neuen InvocationID.<br /><br />-Aufgrund der Zurücksetzen der InvocationID wird DC1 konvergieren an alle AD-Änderungen von DC2-Rec eingeführt werden, auch wenn es ein Rollback ausgeführt wurde, in-Time d.h. alle AD-Updates auf DC2-Rec durchgeführt, nach das Failover sicher konvergiert werden|Der Testfall ist identisch mit denen für einen geplanten Failover mit den folgenden Ausnahmen:<br /><br />-AD Updates auf DC2 empfangen, aber noch nicht auf einen Replikationspartner von Active Directory repliziert vor dem Failoverereignis verloren geht.<br /><br />-AD Updates auf DC2 empfangen werden, nachdem die Zeit des Wiederherstellungspunkts, die von AD an DC1 repliziert wurden von DC1 an DC2-Rec repliziert werden.|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server2008 R2 und früheren Versionen  
In der folgende Tabelle werden die Unterstützung für virtualisierte Domänencontroller, auf denen Windows Server2008 R2 und früheren Versionen ausgeführt.  
  
|||  
|-|-|  
|Geplantes Failover|Ungeplantes Failover|  
|Unterstützt jedoch nicht empfohlen, da Domänencontroller, auf denen diese Versionen von Windows Server ausgeführt VMGenID unterstützen oder nicht verbundene virtualisierungssicherheitsmaßnahmen verwenden. Damit entsteht Risiko einer USN-Rollback. Weitere Informationen finden Sie unter [USN und USN-Rollback](https://technet.microsoft.com/en-us/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10)).|Nicht unterstützte **Hinweis:** ungeplantes Failover würde unterstützt werden, in dem ein USN-Rollback kein Risiko ist, z.B. einem einzelnen Domänencontroller in der Gesamtstruktur (eine Konfiguration, die nicht empfohlen wird).|  
|Testfall:<br /><br />-DC1 und DC2 wird Windows Server2008 R2 ausgeführt.<br /><br />-DC2 wird heruntergefahren, und ein geplantes Failover auf DC2-Rec wird durchgeführt werden kann. Alle Daten auf DC2 werden an DC2-Rec repliziert, bevor das Herunterfahren abgeschlossen ist.<br /><br />: Nachdem DC2-Rec gestartet wird, wird es Replikation mit DC1 mit derselben InvocationID wie DC2 wieder fortgesetzt.|N/V|  
  


