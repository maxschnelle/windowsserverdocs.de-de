---
title: Tiefer stufen und Entfernen des Quell Servers aus dem neuen Windows Server Essentials network1
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: d9f18b29-8e03-439e-bdf0-1dac5e4f70c5
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 3e0902f99be96e3197b90b4892f78849a5c84125
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622879"
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>Tiefer stufen und Entfernen des Quell Servers aus dem neuen Windows Server Essentials network1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Nachdem Sie die Installation von Windows Server Essentials abgeschlossen haben und die Aufgaben im Migrations-Assistenten abgeschlossen haben, müssen Sie die folgenden Aufgaben ausführen:


1.  [Deinstallieren Sie Exchange Server 2003](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003).

2.  [Trennen der Verbindung der Drucker, die direkt mit dem Quellserver verbunden sind](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).

3.  [Den Quellserver tiefer stufen](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).

4.  [Verschieben Sie die DHCP-Server Rolle vom Quell Server auf den Router](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole).

5.  [Entfernen und Wiederverwenden des Quellserver](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).


###  <a name="uninstall-exchange-server-2003"></a><a name="BKMK_UninstallExchangeServer2003"></a> Deinstallieren von Exchange Server 2003

> [!IMPORTANT]
>  Wenn Sie nach dem Verschieben von Postfächern auf den Zielserver, und vor der Deinstallation von Exchange Server 2003 vom Quellserver Benutzerkonten hinzufügen, werden die Postfächer auf dem Quellserver hinzugefügt. Dies ist beabsichtigt. Sie müssen die Postfächer auf den Zielserver für alle Benutzerkonten, die während dieser Zeit hinzugefügt werden, verschieben. Wiederholen Sie die Anweisungen unter Verschieben von Exchange Server-Postfächern und Einstellungen für die Windows Server Essentials-Migration, bevor Sie Exchange Server 2003 deinstallieren.

 Sie müssen Exchange Server 2003 vom Quellserver deinstallieren, bevor Sie ihn tieferstufen. Dies entfernt alle Verweise in Active Directory-Domänendienste (AD DS) zu Exchange Server auf dem Quellserver. Sie müssen Ihre Windows Small Business Server 2003 Medien haben, um Exchange Server 2003 zu entfernen.

##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>So deinstallieren Sie Exchange Server 2003 vom Quellserver

1. Melden Sie sich am zweiten Server als Administrator an.

2. Klicken Sie auf **Start**, klicken Sie auf **Systemsteuerung**, und klicken Sie dann auf **Programme hinzufügen oder entfernen**.

3. Wählen Sie in der Liste der Programme, **Windows Small Business Server 2003** und klicken Sie dann auf **Ändern/deinstallieren**.

4. Klicken Sie im Setup-Assistenten auf **Weiter**, bis die Seite **Auswahl der Komponenten** angezeigt wird.

5. Erweitern Sie auf der Seite Auswahl der Komponenten **Exchange Server** und wählen Sie dann **Entfernen**.

   > [!NOTE]
   >
   >  Exchange-Server überprüft, um sicherzustellen, dass keine Postfächer oder Öffentlichen Ordner auf dem Server vorhanden sind. Wenn irgendwelche Daten verbleiben, wird eine Fehlermeldung angezeigt, wenn Sie auf **Entfernen** klicken. Um dieses Problem zu vermeiden, stellen Sie sicher, dass Sie alle Verfahren im Thema [Verschieben von SBS 2003-Einstellungen und Daten auf den Ziel Server](./move-windows-sbs-2003-to-the-destination-server-for-migration.md)abgeschlossen haben.


6. Klicken Sie auf **Weiter**.

7. Wenn Sie aufgefordert werden, legen Sie Windows Small Business Server 2003-CD # ein und befolgen Sie die Anweisungen auf dem Bildschirm.

###  <a name="disconnect-printers-that-are-directly-connected-to-the-source-server"></a><a name="BKMK_PhysicallyDisconnect"></a> Drucker trennen, die direkt mit dem Quell Server verbunden sind
 Bevor Sie den Quellserver tiefer stufen, trennen Sie physisch alle Drucker, die direkt mit dem Quellserver verbunden sind und über den Quellserver freigegeben werden. Stellen Sie sicher, dass keine Active Directory-Objekte für den Drucker, die direkt mit dem Quellserver verbunden waren, verbleiben. Die Drucker können dann direkt mit dem Ziel Server verbunden und von Windows Server Essentials gemeinsam genutzt werden.

###  <a name="demote-the-source-server"></a><a name="BKMK_DemoteTheSourceServer"></a> Herabstufen des Quell Servers
 Bevor Sie auf dem Quellserver von der Rolle des AD DS-Domänencontroller auf die Rolle des Mitgliedsservers einer Domäne herabstufen, stellen Sie sicher, dass Gruppenrichtlinieneinstellungen auf allen Clientcomputern angewendet werden, wie im folgenden Verfahren beschrieben.

> [!IMPORTANT]
>  Quellserver und Zielserver müssen mit dem Netzwerk verbunden sein, während die Änderungen an den Gruppenrichtlinien auf den Clientcomputern aktualisiert werden.

##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>Aktualisierung der Gruppenrichtlinie auf einem Clientcomputer erzwingen

1.  Melden Sie sich als Administrator beim Clientcomputer an.

2.  Öffnen Sie ein Eingabeaufforderungsfenster als ein Administrator.

3.  Geben Sie an der Eingabeaufforderung **gpupdate /force**, und drücken Sie dann die EINGABETASTE.

4.  Dafür müssen Sie sich möglicherweise ab-und wieder anmelden, um den Vorgang abzuschließen. Klicken Sie zum Bestätigen auf **Ja**.

##### <a name="to-demote-the-source-server"></a>So stufen Sie den Quellserver tiefer

1. Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Ausführen**, geben Sie **dcpromo** ein und klicken Sie dann auf **OK**.

2. Klicken Sie zweimal auf **Weiter**.

   > [!NOTE]
   >  Wählen Sie **Dieser Server ist der letzte Domänencontroller in der Domäne** nicht aus.

3. Geben Sie ein Kennwort für das neue Administratorkonto auf dem Server ein und klicken Sie dann auf **Weiter**.

4. Im Dialogfeld **Zusammenfassung** werden Sie darüber informiert, dass AD DS vom Computer entfernt wird und der Server ein Mitglied der Domäne werden soll. Klicken Sie auf **Weiter**.

5. Klicken Sie auf **Fertig stellen**. Der Quellserver wird neu gestartet.

6. Nach dem Neustart des Quellservers fügen Sie den Quellserver als Mitglied einer Arbeitsgruppe hinzu, bevor Sie die Verbindung zum Netzwerk trennen.

   Nachdem Sie den Quellserver als Mitglied einer Arbeitsgruppe hinzufügen und ihn vom Netzwerk trennen, müssen Sie es aus dem AD DS auf dem Zielserver entfernen.

##### <a name="to-remove-the-source-server-from-active-directory"></a>So entfernen den Quellserver aus Active Directory

1.  Öffnen Sie auf dem Zielserver **Active Directory-Benutzer und-Computer**.

2.  Erweitern Sie im **Active Directory-Benutzer und-Computer**-Navigationsbereich den Domänennamen und erweitern Sie dann **Computer**.

3.  Klicken Sie mit der rechten Maustaste auf der Namen des Quellservers, wenn er noch in der Liste der Server vorhanden ist, klicken Sie auf **Löschen** und klicken Sie dann auf **Ja**.

4.  Überprüfen Sie, ob der Quellserver nicht aufgeführt wird und schließen Sie dann**Active Directory-Benutzer und-Computer**.

###  <a name="move-the-dhcp-server-role-from-the-source-server-to-the-router"></a><a name="BKMK_MoveTheDHCPRole"></a> Verschieben der DHCP-Server Rolle vom Quell Server auf den Router

> [!NOTE]
>
>  Wenn Sie diese Aufgabe bereits vor Beginn des Migrationsprozesses durchgeführt haben, fahren Sie mit Abschnitt [Entfernen und Wiederverwenden des Quellservers](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer) fort.


 Wenn Ihr Quellserver in der DHCP-Rolle ausgeführt wird, führen Sie die folgenden Schritte aus, um die DHCP-Rolle auf den Router zu verschieben.

##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Verschieben der DHCP-Serverrolle vom Quellserver auf den Router.

1.  Deaktivieren Sie wie folgt den DHCP-Dienst auf dem Quellserver:

    1.  Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Verwaltungstools** und klicken Sie dann auf **Dienste**.

    2.  Klicken Sie mit der rechten Maustaste in der Liste der derzeit ausgeführten Dienste auf **Windows Server** und klicken Sie dann auf **Eigenschaften**.

    3.  Wählen Sie für **Starttyp** die Option **deaktiviert**.

    4.  Beenden Sie den Dienst.

2.  Aktivieren Sie die DHCP-Serverrolle auf Ihrem Router

    1.  Befolgen Sie die Anweisungen in Ihrer Router-Dokumentation, um die DHCP-Serverrolle auf dem Router zu aktivieren.

    2.  Befolgen Sie, um sicherzustellen, dass die vom Quellserver ausgestellten IP-Adressen unverändert bleiben, die Anweisungen in der Routerdokumentation, um den DHCP-Bereich auf den Router so zu konfigurieren, dass er mit dem DHCP-Bereich auf dem Quellserver identisch ist.

    > [!IMPORTANT]
    >  Wenn Sie keine statische IP oder DHCP-Reservierungen auf dem Router für den Zielserver eingerichtet haben, und der DHCP-Bereich nicht identisch mit dem Quellserver ist, ist es möglich, dass der Router eine neue IP-Adresse für den Zielserver ausstellt. Setzen Sie in diesem Fall die Portweiterleitungsregeln des Routers zum Weiterleiten auf die neue IP-Adresse des Zielservers zurück.

###  <a name="remove-and-repurpose-the-source-server"></a><a name="BKMK_RemoveTheSourceServer"></a> Entfernen und Wiederherstellen des Quell Servers
 Deaktivieren Sie den Quellserver, und trennen Sie ihn vom Netzwerk. Es wird empfohlen, den Quellserver für mindestens eine Woche nicht neu zu formatieren, um sicherzustellen, dass alle erforderlichen Daten auf den Zielserver migriert wurden. Nachdem Sie sichergestellt haben, dass alle Daten migriert wurden, können Sie, falls erforderlich, diesen Server im Netzwerk als sekundären Server für andere Aufgaben neu installieren.

> [!NOTE]
>  Starten Sie nach dem Herabstufen und Entfernen des Quellservers den Zielserver neu.

 Nachdem Sie den Quellserver tiefergestuft wurde, befindet er nicht in einem fehlerfreien Zustand. Wenn Sie den Quellserver wiederverwenden möchten, ist die einfachste Möglichkeit, ihn neu zu formatieren, indem Sie ein Server-Betriebssystem installieren und es anschließend für die Verwendung als zusätzlichen Server einrichten.