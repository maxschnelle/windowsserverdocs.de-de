---
ms.assetid: 7dd905ea-4235-4519-8400-31b4fa0ed1bf
title: "Aktivieren von Clients den nächstgelegenen Domänencontroller finden"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 39b1b79bba944c10b0c74c4bb18f6dcf80f8230e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="enabling-clients-to-locate-the-next-closest-domain-controller"></a>Aktivieren von Clients den nächstgelegenen Domänencontroller finden

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Sie einen Domänencontroller, die Windows Server2008 oder Windows Server2008 R2 ausgeführt wird haben, können Sie den Eindruck für Clientcomputer unter Windows Vista, Windows7, Windows Server2008 oder Windows Server2008 R2 mit einem Domänencontroller effizienter durch Aktivieren der **versuchen nächstliegenden Standort** Einstellung der Gruppenrichtlinie. Diese Einstellung verbessert den Domänencontrollerlocator (Domänencontrollerlocator) dazu beiträgt, Netzwerkdatenverkehr, insbesondere in großen Unternehmen zu optimieren, die viele Filialen und Websites verfügen.  
  
Diese neue Einstellung kann auswirken wie Standortverknüpfungskosten konfigurieren, da sie den Auftrag wirkt sich in dem Domänencontroller gespeichert sind. Für Unternehmen, die viele Hub-Websites und Filialen haben, können Sie erheblich Active Directory-Verkehr im Netzwerk reduzieren, indem Sie sicherstellen, dass Clients Failover zum nächstgelegenen Hubstandort ausgeführt wird, wenn einen Domänencontroller am nächstgelegenen Hubstandort gefunden werden kann.  
  
Als allgemeine bewährte Methode sollten Sie die Standorttopologie vereinfachen und standortverknüpfung Kosten so weit wie möglich, durch das Aktivieren der **versuchen nächstliegenden Standort** Einstellung. In Unternehmen mit zahlreichen Hub-Websites kann diese Pläne vereinfachen, die Sie vornehmen, für die Behandlung von Situationen, in denen Clients an einem Standort ein Failover auf einen Domänencontroller an einem anderen Standort müssen.  
  
Standardmäßig die **versuchen nächstliegenden Standort** Einstellung nicht aktiviert. Wenn die Einstellung nicht aktiviert ist, wird Domänencontrollerlocator folgenden Algorithmus zum Suchen eines Domänencontrollers verwendet:  
  
-   Versuchen Sie, einen Domänencontroller am selben Standort zu finden.  
  
-   Wenn kein Domänencontroller am selben Standort verfügbar ist, versuchen Sie, einen beliebigen Domänencontroller in der Domäne zu finden.  
  
> [!NOTE]  
> Dies ist der gleiche Algorithmus, den Domänencontrollerlocator in früheren Versionen von Active Directory verwendet. Weitere Informationen finden Sie unter DNS für Active Directory funktioniert wie unterstützen ([https://go.microsoft.com/fwlink/?LinkId=108587](https://go.microsoft.com/fwlink/?LinkId=108587)).  
  
Durch das Aktivieren der **versuchen nächstliegenden Standort** festlegen, Domänencontrollerlocator verwendet die folgenden Algorithmus, um einen Domänencontroller zu finden:  
  
-   Versuchen Sie, einen Domänencontroller am selben Standort zu finden.  
  
-   Wenn kein Domänencontroller am selben Standort verfügbar ist, versuchen Sie, in dem nächstliegenden Standort einen Domänencontroller gefunden. Ein Standort ist näher hat eine niedrigere Standortverknüpfungsobjekte Kosten als einen anderen Standort mit einem höheren Standort Link Kosten.  
  
-   Wenn in dem nächstliegenden Standort kein Domänencontroller verfügbar ist, versuchen Sie, einen beliebigen Domänencontroller in der Domäne zu finden.  
  
In der Standardeinstellung berücksichtigt Domänencontrollerlocator keinem Standort, der einem schreibgeschützten Domänencontroller (RODC) enthält, wenn sie den nächstliegenden Standort bestimmt. Darüber hinaus, da nur Windows Server2008 und Windows Server2008 R2 domänencontrollerunterstützung weiter am nächsten gelegenen Standort Funktionen, bei der der Client eine Antwort von einem Domänencontroller abgerufen, die eine frühere Version von Windows Server ausgeführt wird, das Verhalten der Domänencontrollerlocator identisch ist ist bei und der Wert nicht aktiviert.  
  
Nehmen wir beispielsweise an, dass eine Standorttopologie vier Standorte mit den Werten des Site-Link in der folgenden Abbildungverfügt. In diesem Beispiel werden alle Domänencontroller beschreibbaren Domänencontroller, auf denen Windows Server2008 oder Windows Server2008 R2 ausgeführt.  
  
![Aktivieren von Clients Domänencontroller finden](media/Enabling-Clients-to-Locate-the-Next-Closest-Domain-Controller/beff4087-fb2a-463b-96ac-d440a9e29b75.gif)  
  
Wenn die **versuchen nächstliegenden Standort** Gruppenrichtlinien-Einstellung in diesem Beispiel aktiviert ist, wenn ein Clientcomputer, der ausgeführt, Windows Vista, Windows7, Windows Server2008 wird oder Windows Server2008 R2 in greift versucht, einen Domänencontroller zu finden, er zunächst versucht, einen Domänencontroller in seiner eigenen greift finden. Wenn in greift verfügbar ist, wird versucht, einen Domänencontroller passenden finden.  
  
Wenn die Einstellung nicht aktiviert ist, sucht der Client einen Domänencontroller in den passenden, Site_C oder Site_D ist kein Domänencontroller verfügbar in greift.  
  
> [!NOTE]  
> Die **versuchen nächstliegenden Standort** Einstellung zusammen mit der automatischen standortabdeckung funktioniert. Wenn der nächstliegenden Standort kein Domänencontroller ist, versucht Domänencontrollerlocator z.B. den Domänencontroller zu finden, der automatische standortabdeckung für diesen Standort ausführt.  
  
Zum Anwenden der **versuchen nächstliegenden Standort** festlegen, können Sie ein Gruppenrichtlinienobjekt (GPO) erstellen und verknüpfen Sie es in das entsprechende Objekt für Ihre Organisation, oder ändern Sie die Standarddomänenrichtlinie so, dass sie die Auswirkung auf alle Clients, auf denen Windows Vista, Windows7, Windows Server2008 oder Windows Server2008 R2 in der Domäne ausgeführt. Weitere Informationen zur Vorgehensweise beim Festlegen der **versuchen nächstliegenden Standort** festlegen, finden Sie unter [Clients aktivieren, um einen Domänencontroller zu finden, in dem nächstliegenden Standort](https://technet.microsoft.com/library/cc772592.aspx).  
  


