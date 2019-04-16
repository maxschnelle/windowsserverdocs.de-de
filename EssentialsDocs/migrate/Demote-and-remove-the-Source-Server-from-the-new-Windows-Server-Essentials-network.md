---
title: Tieferstufen Sie und entfernen Sie des Quellservers aus der neuen Windows Server Essentials-network1
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9f18b29-8e03-439e-bdf0-1dac5e4f70c5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1545189732194ad5c0aba401f834b0102799e016
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>Tieferstufen Sie und entfernen Sie des Quellservers aus der neuen Windows Server Essentials-network1

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Nach Abschluss der Installation von Windows Server Essentials, und Sie die Aufgaben im Migrations-Assistenten ausführen, müssen Sie die folgenden Aufgaben ausführen:  
  

1.  [Deinstallieren von Exchange Server2003](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003).  
  
2.  [Trennen Sie die Verbindung, die direkt auf dem Quellserver verbunden sind](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).  
  
3.  [Den Quellserver tiefer stufen](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den Router](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole).  
  
5.  [Entfernen und wiederverwenden des Quellservers](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

1.  [Deinstallieren von Exchange Server2003](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003).  
  
2.  [Trennen Sie die Verbindung, die direkt auf dem Quellserver verbunden sind](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).  
  
3.  [Den Quellserver tiefer stufen](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den Router](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole).  
  
5.  [Entfernen und wiederverwenden des Quellservers](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

  
###  <a name="BKMK_UninstallExchangeServer2003"></a>Deinstallieren von Exchange Server2003  
  
> [!IMPORTANT]
>  Wenn Sie nach dem Verschieben von Postfächern auf den Zielserver und vor der Deinstallation von Exchange Server2003 vom Quellserver Benutzerkonten hinzufügen, werden die Postfächer auf dem Quellserver hinzugefügt. Dies ist beabsichtigt. Sie müssen die Postfächer auf den Zielserver für alle Benutzerkonten verschieben, die während dieser Zeit hinzugefügt werden. Wiederholen Sie die Anweisungen im Exchange Server Postfächer verschieben und Einstellungen für Windows Server Essentials-Migration, vor der Deinstallation von Exchange Server2003.  
  
 Sie müssen Exchange Server2003 vom Quellserver deinstallieren, bevor Sie ihn Tieferstufen. Dies entfernt alle Verweise in Active Directory-Domänendienste (AD DS) zu Exchange Server auf dem Quellserver. Sie benötigen Windows Small Business Server2003 Medien auf Exchange Server2003 entfernen.  
  
##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>So deinstallieren Sie Exchange Server2003 vom Quellserver  
  
1.  Melden Sie sich auf dem Quellserver als administrator  
  
2.  Klicken Sie auf **starten**, klicken Sie auf **Systemsteuerung**, und klicken Sie dann auf **Software**.  
  
3.  Wählen Sie in der Liste der Programme, **Windows Small Business Server2003**, und klicken Sie dann auf **ändern/Deinstallieren**.  
  
4.  Klicken Sie im Setup-Assistenten auf **Weiter** bis die **Auswahl der Komponenten** Seite wird angezeigt.  
  
5.  Erweitern Sie auf der Seite Auswahl der Komponenten **Exchange Server**, und wählen Sie dann **entfernen**.  
  
    > [!NOTE]

    >  Exchange-Server überprüft, um sicherzustellen, dass keine Postfächer oder öffentlichen Ordner auf dem Server vorhanden sind. Wenn irgendwelche Daten verbleiben, wird eine Fehlermeldung angezeigt, wenn Sie auf **entfernen**. Um dieses Problem zu vermeiden, stellen Sie sicher, dass Sie alle Verfahren im Thema abgeschlossen haben [Verschieben von SBS 2003-Einstellungen und Daten auf den Zielserver](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  

    >  Exchange-Server überprüft, um sicherzustellen, dass keine Postfächer oder öffentlichen Ordner auf dem Server vorhanden sind. Wenn irgendwelche Daten verbleiben, wird eine Fehlermeldung angezeigt, wenn Sie auf **entfernen**. Um dieses Problem zu vermeiden, stellen Sie sicher, dass Sie alle Verfahren im Thema abgeschlossen haben [Verschieben von SBS 2003-Einstellungen und Daten auf den Zielserver](../migrate/Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  

  
6.  Klicken Sie auf **Weiter**.  
  
7.  Wenn Sie aufgefordert werden, legen Sie Windows Small Business Server2003-CD 3, und folgen Sie den Anweisungen auf dem Bildschirm.  
  
###  <a name="BKMK_PhysicallyDisconnect"></a>Trennen Sie die Verbindung, die direkt auf dem Quellserver verbunden sind  
 Bevor Sie den Quellserver tiefer stufen, trennen Sie physisch alle Drucker, die direkt auf dem Quellserver verbunden sind und über den Quellserver freigegeben werden. Stellen Sie sicher, dass keine Active Directory-Objekte für den Drucker bleiben, die direkt auf dem Quellserver verbunden waren. Die Drucker können dann direkt auf den Zielserver verbunden und in Windows Server Essentials freigegeben werden.  
  
###  <a name="BKMK_DemoteTheSourceServer"></a>Den Quellserver tiefer stufen  
 Bevor Sie den Quellserver aus der Rolle des AD DS-Domänencontroller auf die Rolle des Mitgliedsservers einer Domäne herabstufen, stellen Sie sicher, dass Gruppenrichtlinieneinstellungen auf allen Clientcomputern angewendet werden, wie im folgenden Verfahren beschrieben.  
  
> [!IMPORTANT]
>  Der Quellserver und Zielserver müssen mit dem Netzwerk verbunden werden, während Änderungen an den Gruppenrichtlinien auf den Clientcomputern aktualisiert werden.  
  
##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>Um eine Aktualisierung der Gruppenrichtlinie auf einem Clientcomputer erzwingen  
  
1.  Melden Sie sich an den Clientcomputer als Administrator an.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster als Administrator.  
  
3.  Geben Sie an der Eingabeaufforderung **Gpupdate/force**, und drücken Sie dann die EINGABETASTE.  
  
4.  Der Prozess kann es nötig sein, melden Sie sich ab und melden Sie sich wieder beendet. Klicken Sie auf **Ja** zu bestätigen.  
  
##### <a name="to-demote-the-source-server"></a>Um den Quellserver tiefer stufen  
  
1.  Klicken Sie auf dem Quellserver auf **starten**, klicken Sie auf **ausführen**, Typ **Dcpromo**, und klicken Sie dann auf **OK**.  
  
2.  Klicken Sie auf **Weiter** zweimal.  
  
    > [!NOTE]
    >  Wählen Sie nicht **dieser Server ist der letzte Domänencontroller in der Domäne**.  
  
3.  Geben Sie ein Kennwort für das neue Administratorkonto auf dem Server, und klicken Sie dann auf **Weiter**.  
  
4.  In der **Zusammenfassung** im Dialogfeld werden Sie darüber informiert, dass AD DS vom Computer entfernt wird und dass der Server Mitglied der Domäne werden soll. Klicken Sie auf **Weiter**.  
  
5.  Klicken Sie auf **Fertig stellen**. Der Quellserver wird neu gestartet.  
  
6.  Nach dem Neustart der Quellserver werden fügen Sie den Quellserver als Mitglied einer Arbeitsgruppe hinzu, bevor Sie ihn vom Netzwerk trennen.  
  
 Nachdem Sie den Quellserver als Mitglied einer Arbeitsgruppe hinzufügen und ihn vom Netzwerk trennen, müssen Sie es aus AD DS auf dem Zielserver entfernen.  
  
##### <a name="to-remove-the-source-server-from-active-directory"></a>So entfernen den Quellserver aus Active Directory  
  
1.  Öffnen Sie auf dem Zielserver **Active Directory-Benutzer und -Computer**.  
  
2.  In der **Active Directory-Benutzer und -Computer** Navigationsbereich, erweitern Sie den Domänennamen und erweitern Sie dann **Computer**.  
  
3.  Mit der rechten Maustaste, der den Namen des Quellservers ggf. weiterhin in der Liste der Server, klicken Sie auf **löschen**, und klicken Sie dann auf **Ja**.  
  
4.  Stellen Sie sicher, dass der Quellserver nicht aufgeführt ist, und schließen Sie dann **Active Directory-Benutzer und -Computer**.  
  
###  <a name="BKMK_MoveTheDHCPRole"></a>Verschieben Sie die DHCP-Serverrolle vom Quellserver auf den router  
  
> [!NOTE]

>  Wenn Sie diese Aufgabe bereits vor Beginn des Migrationsprozesses durchgeführt, fahren Sie mit Abschnitt [entfernen und wiederverwenden des Quellservers](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

>  Wenn Sie diese Aufgabe bereits vor Beginn des Migrationsprozesses durchgeführt, fahren Sie mit Abschnitt [entfernen und wiederverwenden des Quellservers](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

  
 Wenn der Quellserver die DHCP-Serverrolle ausgeführt wird, führen Sie die folgenden Schritte aus, um die DHCP-Serverrolle auf den Router verschieben.  
  
##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Um die DHCP-Serverrolle vom Quellserver auf den Router zu verschieben.  
  
1.  Deaktivieren Sie den DHCP-Dienst auf dem Quellserver wie folgt aus:  
  
    1.  Klicken Sie auf dem Quellserver auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Dienste**.  
  
    2.  In der Liste der derzeit ausgeführten Dienste mit der rechten Maustaste die **Windows Server**, und klicken Sie dann auf **Eigenschaften**.  
  
    3.  Für **Starttyp**Option **deaktiviert**.  
  
    4.  Beenden Sie den Dienst.  
  
2.  Die DHCP-Serverrolle auf dem Router aktivieren  
  
    1.  Führen Sie die Anweisungen in der Routerdokumentation, um die DHCP-Serverrolle auf dem Router aktivieren.  
  
    2.  Folgen Sie den Anweisungen in der Routerdokumentation so konfigurieren Sie den DHCP-Bereich auf dem Router für den DHCP-Bereich auf dem Quellserver identisch sein, um sicherzustellen, dass vom Quellserver ausgestellte IP-Adressen unverändert bleiben.  
  
    > [!IMPORTANT]
    >  Wenn Sie keine statische IP-Adresse oder DHCP-Reservierungen auf dem Router, für den Zielserver eingerichtet haben, und der DHCP-Bereich identisch mit dem Quellserver ist, ist es möglich, dass der Router eine neue IP-Adresse für den Zielserver ausstellt. In diesem Fall die portweiterleitungsregeln des Routers zum Weiterleiten der neuen IP-Adresse des Zielservers zurückgesetzt.  
  
###  <a name="BKMK_RemoveTheSourceServer"></a>Entfernen und wiederverwenden des Quellservers  
 Deaktivieren Sie den Quellserver und dem Netzwerk trennen. Es wird empfohlen, dass Sie nicht neu zu, den Quellserver für mindestens eine Woche formatieren, um sicherzustellen, dass alle erforderlichen Daten zum Zielserver migriert. Nachdem Sie überprüft haben, dass alle Daten migriert wurden, können Sie diesen Server im Netzwerk als sekundärer Server für andere Aufgaben neu installieren bei Bedarf.  
  
> [!NOTE]
>  Nach dem Herabstufen und des Quellservers entfernen, starten Sie den Zielserver neu.  
  
 Nachdem Sie den Quellserver tiefer stufen, ist es nicht in einem fehlerfreien Zustand. Wenn Sie den Quellserver wiederverwenden möchten, ist die einfachste Möglichkeit zum Formatieren Sie es ein Server-Betriebssystem installieren und dann für die Verwendung als zusätzlichen Server einrichten.
