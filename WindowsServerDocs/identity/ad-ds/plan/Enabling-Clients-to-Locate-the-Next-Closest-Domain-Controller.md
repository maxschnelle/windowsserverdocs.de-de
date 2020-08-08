---
ms.assetid: 7dd905ea-4235-4519-8400-31b4fa0ed1bf
title: Ermöglichen, dass Clients den nächstgelegenen Domänencontroller finden
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: 54b830df42a99712c28bb49be7e89ee84a43b088
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941199"
---
# <a name="enabling-clients-to-locate-the-next-closest-domain-controller"></a>Ermöglichen, dass Clients den nächstgelegenen Domänencontroller finden

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie über einen Domänen Controller verfügen, auf dem Windows Server 2008 oder höher ausgeführt wird, können Sie auf Client Computern, auf denen Windows Vista oder höher oder Windows Server 2008 oder höher ausgeführt wird, das Auffinden von Domänen Controllern ermöglichen, indem Sie die Einstellung **nächsten Standort Gruppenrichtlinie testen** aktivieren. Diese Einstellung verbessert den Domänencontrollerlocator (Domänencontrollerlocator), indem der Netzwerkverkehr optimiert wird, insbesondere in großen Unternehmen, die über viele Zweigstellen und Standorte verfügen.

Diese neue Einstellung kann sich auf die Konfiguration der Standort Verknüpfungs Kosten auswirken, da Sie sich auf die Reihenfolge auswirkt, in der sich Domänen Controller befinden. Für Unternehmen, die über viele Hub-Standorte und Zweigstellen verfügen, können Sie Active Directory Datenverkehr im Netzwerk erheblich reduzieren, indem Sie sicherstellen, dass Clients ein Failover zum nächstgelegenen Hub-Standort durchführen, wenn Sie keinen Domänen Controller am nächstgelegenen Hub-Standort finden.

Als allgemeine bewährte Vorgehensweise sollten Sie die Standort Topologie und die Standort Verknüpfungs Kosten so weit wie möglich vereinfachen, wenn Sie die Einstellung **nächste Site testen** aktivieren. In Unternehmen mit vielen Hub-Standorten können dadurch alle Pläne vereinfacht werden, die Sie für die Behandlung von Situationen treffen, in denen Clients an einem Standort ein Failover zu einem Domänen Controller an einem anderen Standort ausführen müssen.

Standardmäßig ist die Einstellung **nächstgelegene Site testen** nicht aktiviert. Wenn die Einstellung nicht aktiviert ist, verwendet der Domänen Controller-Locator den folgenden Algorithmus, um einen Domänen Controller zu finden:

- Versuchen Sie, einen Domänen Controller am selben Standort zu finden.
- Wenn kein Domänen Controller am selben Standort verfügbar ist, versuchen Sie, einen beliebigen Domänen Controller in der Domäne zu finden.

> [!NOTE]
> Dabei handelt es sich um denselben Algorithmus, den der DC-Locator in früheren Versionen von Active Directory verwendet hat. Weitere Informationen finden Sie im Artikel über die [Funktionsweise der DNS-Unterstützung für Active Directory](/previous-versions/windows/it-pro/windows-server-2003/cc759550(v=ws.10)).

Wenn Sie die Einstellung für den nächst **gelegenen Standort testen** aktivieren, verwendet der Domänen Controller-Locator den folgenden Algorithmus, um einen Domänen Controller zu finden:

- Versuchen Sie, einen Domänen Controller am selben Standort zu finden.
- Wenn kein Domänen Controller am selben Standort verfügbar ist, versuchen Sie, am nächstgelegenen Standort einen Domänen Controller zu finden. Ein Standort ist genauer, wenn er über einen niedrigeren Standort Verknüpfungs Aufwand als ein anderer Standort mit höheren Standort Verknüpfungs Kosten verfügt.
- Wenn am nächstgelegenen Standort kein Domänen Controller verfügbar ist, versuchen Sie, einen beliebigen Domänen Controller in der Domäne zu finden.

Die Einstellung am **nächsten gelegenen Standort testen** funktioniert mit der automatischen Standort Abdeckung. Wenn beispielsweise der nächstgelegene Standort keinen Domänen Controller aufweist, versucht der Domänencontrollerlocator, den Domänen Controller zu finden, der die automatische Standort Abdeckung für diesen Standort ausführt.

Standardmäßig berücksichtigt der Domänen Controller-Locator keine Standorte, die einen schreibgeschützten Domänen Controller (Read-Only Domain Controller, RODC) enthalten, wenn er den nächstgelegenen Standort festlegt. Wenn der Client eine Antwort von einem Domänen Controller erhält, auf dem eine frühere Version als Windows Server 2008 ausgeführt wird, ist das Verhalten des Domänen Controller-Locators außerdem identisch mit dem Zeitpunkt, an dem die Einstellung nicht aktiviert ist.

Nehmen wir beispielsweise an, dass eine Standort Topologie über vier Standorte mit den Standort Verknüpfungs Werten in der folgenden Abbildung verfügt. In diesem Beispiel sind alle Domänen Controller beschreibbare Domänen Controller, auf denen Windows Server 2008 oder höher ausgeführt wird.

![Clients können Domänen Controller suchen](media/Enabling-Clients-to-Locate-the-Next-Closest-Domain-Controller/beff4087-fb2a-463b-96ac-d440a9e29b75.gif)

Wenn in diesem Beispiel die Einstellung am **nächsten gelegenen Standort** Gruppenrichtlinie aktiviert ist und ein Client Computer in Site_B versucht, einen Domänen Controller zu finden, versucht er zunächst, einen Domänen Controller in seinem eigenen Site_B zu finden. Wenn in Site_B keine verfügbar ist, wird versucht, in Site_A einen Domänen Controller zu finden.

Wenn die Einstellung nicht aktiviert ist, versucht der Client, einen Domänen Controller in Site_A, Site_C oder Site_D zu finden, wenn in Site_B kein Domänen Controller verfügbar ist.

> [!NOTE]
> Die Einstellung am **nächsten gelegenen Standort testen** funktioniert mit der automatischen Standort Abdeckung. Wenn beispielsweise der nächstgelegene Standort keinen Domänen Controller aufweist, versucht der Domänencontrollerlocator, den Domänen Controller zu finden, der die automatische Standort Abdeckung für diesen Standort ausführt.

Sie können ein Gruppenrichtlinie Objekt (GPO) erstellen und mit dem entsprechenden Objekt für Ihre Organisation verknüpfen **, indem Sie die Standard** Domänen Richtlinie so ändern, dass Sie sich auf alle Clients auswirkt, auf denen Windows Vista oder höher bzw. Windows Server 2008 oder höher in der Domäne ausgeführt wird. Weitere Informationen zum Festlegen der nächst **gelegenen Site** -Einstellung finden Sie unter Aktivieren von [Clients zum Auffinden eines Domänen Controllers am nächstgelegenen Standort](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc772592(v=ws.10)).
