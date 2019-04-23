---
ms.assetid: 7dd905ea-4235-4519-8400-31b4fa0ed1bf
title: Ermöglichen, dass Clients den nächstgelegenen Domänencontroller finden
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7550bdcea4e7b06d31463744bfdc3319c012c62c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880361"
---
# <a name="enabling-clients-to-locate-the-next-closest-domain-controller"></a>Ermöglichen, dass Clients den nächstgelegenen Domänencontroller finden

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie einen Domänencontroller, die WindowsServer 2008 oder höher ausgeführt wird haben, können Sie machen es möglich, dass Clientcomputer mit Windows Vista oder höher oder WindowsServer 2008 oder neuer Suche nach Domänencontrollern effizienter durch Aktivieren der **versuchen Sie es weiter Am nächstgelegenen Standort** gruppenrichtlinieneinstellung. Diese Einstellung verbessert die Domänencontroller-Locator (Domänencontrollerlocator) dazu beiträgt, die den Netzwerkdatenverkehr, insbesondere in großen Unternehmen zu optimieren, die vielen Zweigstellen und Websites verfügen.

Diese neue Einstellung kann beeinflussen, wie Sie Standortverknüpfungskosten konfigurieren, da es die Reihenfolge auswirkt, in der Domänencontroller gespeichert sind. Für Unternehmen, die viele nabenstandorten und Filialen haben, können Sie deutlich Active Directory-Datenverkehrs im Netzwerk reduzieren, indem Sie sicherstellen, dass Clients Failover zum nächsten Hubstandort ausgeführt wird, wenn einen Domänencontroller am nächstgelegenen Hubstandort gefunden werden kann.

Als allgemeine bewährte Methode sollten Sie Ihre Standorttopologie vereinfachen und die standortverknüpfung Kosten so weit wie möglich, wenn Sie aktivieren die **versuchen Sie es am nächstgelegenen Standort** festlegen. In Unternehmen mit vielen nabenstandorten kann dadurch alle Pläne vereinfachen, die Sie vornehmen, für die Behandlung von Situationen, in denen Clients an einem Standort, müssen für ein Failover zu einem Domänencontroller an einem anderen Standort.

In der Standardeinstellung die **versuchen Sie es am nächstgelegenen Standort** -Einstellung nicht aktiviert. Wenn die Einstellung nicht aktiviert ist, verwendet Domänencontrollerlocator des folgenden Algorithmus, um das Auffinden eines Domänencontrollers:

- Versuchen Sie, ein Domänencontroller am selben Standort gefunden.
- Wenn sich am selben Standort kein Domänencontroller verfügbar ist, versuchen Sie es auf einen beliebigen Domänencontroller in der Domäne zu finden.

> [!NOTE]
> Dies ist der gleiche Algorithmus, den Domänencontrollerlocator in früheren Versionen von Active Directory verwendet. Weitere Informationen finden Sie im Artikel [wie DNS-Unterstützung für die Funktionsweise von Active Directory](https://go.microsoft.com/fwlink/?LinkId=108587).

Wenn Sie aktivieren die **versuchen Sie es am nächstgelegenen Standort** Einstellung Domänencontrollerlocator anhand des folgenden Algorithmus zum Auffinden eines Domänencontrollers:

- Versuchen Sie, ein Domänencontroller am selben Standort gefunden.
- Wenn sich am selben Standort kein Domänencontroller verfügbar ist, versuchen Sie, einen Domänencontroller in der am nächstgelegenen Standort suchen. Ein Standort ist genauer, wenn sie eine niedrigere-standortverknüpfung Kosten als einen anderen Standort mit einem höheren Kosten Standort-Link verfügt.
- Wenn es sich bei dem nächstliegenden Standort kein Domänencontroller verfügbar ist, versucht, einen beliebigen Domänencontroller in der Domäne zu finden.

Die **versuchen Sie es am nächstgelegenen Standort** Einstellung, die in Koordination mit automatischen standortabdeckung funktioniert. Wenn der nächstliegenden Standort kein Domänencontroller ist, versucht Domänencontrollerlocator beispielsweise der Domänencontroller gesucht, der automatische standortabdeckung für diesen Standort ausführt.

In der Standardeinstellung berücksichtigt Domänencontrollerlocator nicht einem beliebigen Standort, der einem schreibgeschützten Domänencontroller (RODC) enthält, wenn es feststellt, dass die am nächstgelegenen Standort. Darüber hinaus, wenn der Client eine Antwort von einem Domänencontroller, die eine Version älter als Windows Server 2008 ausgeführt wird erhält, entspricht das Verhalten der Domänencontrollerlocator Wenn wird nicht aktiviert ist.

Nehmen wir beispielsweise an, dass eine Topologie vier Standorte mit den Werten des Standort-Link in der folgenden Abbildung verfügt. In diesem Beispiel sind alle Domänencontroller beschreibbare Domänencontroller, auf denen WindowsServer 2008 oder höher ausgeführt wird.

![Clients nach Domänencontroller suchen](media/Enabling-Clients-to-Locate-the-Next-Closest-Domain-Controller/beff4087-fb2a-463b-96ac-d440a9e29b75.gif)

Wenn die **versuchen Sie es am nächstgelegenen Standort** gruppenrichtlinieneinstellung wird in diesem Beispiel aktiviert, wenn ein Clientcomputer in greift versucht wird, um einen Domänencontroller zu suchen, zuerst wird versucht, einen Domänencontroller in seiner eigenen greift finden. Wenn kein in greift verfügbar ist, versucht, einen Domänencontroller passenden zu finden.

Wenn die Einstellung nicht aktiviert ist, versucht der Client, einen Domänencontroller in passenden Site_C oder Site_D gesucht werden soll, wenn keine Domänencontroller in greift verfügbar ist.

> [!NOTE]
> Die **versuchen Sie es am nächstgelegenen Standort** Einstellung, die in Koordination mit automatischen standortabdeckung funktioniert. Wenn der nächstliegenden Standort kein Domänencontroller ist, versucht Domänencontrollerlocator beispielsweise der Domänencontroller gesucht, der automatische standortabdeckung für diesen Standort ausführt.

Anwenden der **versuchen Sie es am nächstgelegenen Standort** festlegen, können Sie ein Gruppenrichtlinienobjekt (GPO) erstellen und verknüpfen Sie ihn in das entsprechende Objekt für Ihre Organisation, oder Ändern der Standarddomänenrichtlinie so, dass sie alle Clients auswirken, auf denen Windows ausgeführt. Vista oder höher und WindowsServer 2008 oder neuer in der Domäne. Weitere Informationen zum Festlegen der **versuchen Sie es am nächstgelegenen Standort** finden Sie unter [ermöglichen Clients das Auffinden eines Domänencontrollers in der am nächstgelegenen Standort](https://technet.microsoft.com/library/cc772592.aspx).
