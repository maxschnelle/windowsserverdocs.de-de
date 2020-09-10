---
title: 'Schritt 6: Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 86244c66-2c5e-488d-adb8-112e1ca3e2e1
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 6c4410cb94f79be291984a92a2b788e3ae984a4f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625425"
---
# <a name="step-6-demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network"></a>Schritt 6: Tieferstufen und Entfernen des Quellservers aus dem neuen Windows Server Essentials-Netzwerk

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

Nachdem Sie die Installation von Windows Server Essentials abgeschlossen und die Migration abgeschlossen haben, müssen Sie die folgenden Aufgaben ausführen:

1.  [Entfernen von Active Directory-Zertifikatdiensten](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_ADCS)

2.  [Trennen Sie die Verbindung der Drucker, die direkt mit dem Quellserver verbunden sind.](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)

3.  [Den Quellserver tiefer stufen](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)

4.  [Entfernen und Wiederverwenden des Quellserver .](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)

##  <a name="remove-active-directory-certificate-services"></a><a name="BKMK_ADCS"></a> Entfernen von Active Directory-Zertifikat Diensten
 Das Verfahren unterscheidet sich geringfügig, wenn Sie mehrere Rollendienste für Active Directory-Zertifikatdienste (AD CS) auf einem einzelnen Server installiert haben. Sie können das folgende Verfahren zum Deinstallieren eines AD CS-Rollendiensts und Beibehalten anderer AD CS-Rollendienste verwenden.

 Um diese Schritte abzuschließen, müssen Sie sich mit den gleichen Berechtigungen wie der Benutzer anmelden, der die Zertifizierungsstelle (CA) installiert hat. Wenn Sie eine Unternehmenszertifizierungsstelle deinstallieren, ist die Mitgliedschaft in der Gruppe "Organisations-Admins" oder einer gleichwertigen Gruppe die Mindestvoraussetzung, um diese Schritte ausführen zu können.

#### <a name="to-remove-ad-cs"></a>So entfernen Sie AD CS

1.  Melden Sie sich als Domänenadministrator beim Quellserver an.

2.  Klicken Sie auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Server-Manager**.

3.  Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Weiter**.

4.  Klicken Sie in der **Rollenübersicht** auf **Rollen entfernen**.

5.  Klicken Sie im Assistenten zum Entfernen von Rollen auf **Weiter**.

6.  Deaktivieren Sie das Kontrollkästchen **Active Directory-Zertifikatdienste**, und klicken Sie dann auf **Weiter**.

7.  Überprüfen Sie die Informationen auf der Seite **Entfernungsauswahl bestätigen**, und klicken Sie dann auf **Entfernen**.

    > [!NOTE]
    >  Wenn Internetinformationsdienste (Internet Information Services, IIS) ausgeführt wird, werden Sie aufgefordert, den Dienst zu beenden, bevor Sie fortfahren. Klicken Sie auf **OK**.

    > [!NOTE]
    >  Zunächst müssen Sie u. U. **Zertifizierungsstellen-Webregistrierung** entfernen, falls installiert.

8.  Starten Sie den Server nach Abschluss des Assistenten zum Entfernen von Rollen neu, und schließen Sie die Deinstallation ab.

    > [!IMPORTANT]
    >  Starten Sie den Server neu, auch wenn Sie nicht dazu aufgefordert werden.

##  <a name="disconnect-printers-that-are-directly-connected-to-the-source-server"></a><a name="BKMK_PhysicallyDisconnect"></a> Drucker trennen, die direkt mit dem Quell Server verbunden sind
 Bevor Sie den Quellserver tiefer stufen, trennen Sie physisch alle Drucker, die direkt mit dem Quellserver verbunden sind und über den Quellserver freigegeben werden. Stellen Sie sicher, dass keine Active Directory-Objekte für den Drucker, die direkt mit dem Quellserver verbunden waren, verbleiben. Die Drucker können dann direkt mit dem Ziel Server verbunden und von Windows Server Essentials gemeinsam genutzt werden.

##  <a name="demote-the-source-server"></a><a name="BKMK_DemoteTheSourceServer"></a> Herabstufen des Quell Servers
 Bevor Sie auf dem Quellserver von der Rolle des AD DS-Domänencontroller auf die Rolle des Mitgliedsservers einer Domäne herabstufen, stellen Sie sicher, dass Gruppenrichtlinieneinstellungen auf allen Clientcomputern angewendet werden, wie im folgenden Verfahren beschrieben.

> [!IMPORTANT]
>  Quellserver und Zielserver müssen mit dem Netzwerk verbunden sein, während die Änderungen an den Gruppenrichtlinien auf den Clientcomputern aktualisiert werden.

#### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>Aktualisierung der Gruppenrichtlinie auf einem Clientcomputer erzwingen

1. Melden Sie sich als Administrator beim Clientcomputer an.

2. Öffnen Sie ein Eingabeaufforderungsfenster als ein Administrator.

3. Geben Sie an der Eingabeaufforderung **gpupdate /force**, und drücken Sie dann die EINGABETASTE.

4. Dafür müssen Sie sich möglicherweise ab-und wieder anmelden, um den Vorgang abzuschließen. Klicken Sie zum Bestätigen auf **Ja**.

   Wenn Sie von Windows Server Essentials oder den vorherigen Versionen migrieren, finden Sie unter [Entfernen von Active Directory Domain Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh472163(v=ws.11))Informationen zum Herabstufen des Servers. Nachdem Sie den Quellserver als Mitglied einer Arbeitsgruppe hinzufügen und ihn vom Netzwerk trennen, müssen Sie es aus dem AD DS auf dem Zielserver entfernen.

   Wenn Sie von Windows Server Essentials migrieren, verwenden Sie Server-Manager, um die Active Directory Domain Services-Rolle zu entfernen, und verwenden Sie dabei das folgende Verfahren zum Herabstufen des Domänen Controllers auf dem Quell Server:

#### <a name="to-remove-the-source-server-from-active-directory"></a>So entfernen den Quellserver aus Active Directory

1.  Öffnen Sie auf dem Zielserver **Active Directory-Benutzer und-Computer**.

2.  Erweitern Sie im **Active Directory-Benutzer und-Computer**-Navigationsbereich den Domänennamen und erweitern Sie dann **Computer**.

3.  Wenn der Quellserver noch in der Liste der Server vorhanden ist, klicken Sie mit der rechten Maustaste auf dessen Namen und klicken auf **Löschen** und dann auf **Ja**.

4.  Überprüfen Sie, ob der Quellserver nicht aufgeführt wird und schließen Sie dann**Active Directory-Benutzer und-Computer**.

##  <a name="remove-and-repurpose-the-source-server"></a><a name="BKMK_RemoveTheSourceServer"></a> Entfernen und Wiederherstellen des Quell Servers
 Deaktivieren Sie den Quellserver, und trennen Sie ihn vom Netzwerk. Es wird empfohlen, den Quellserver für mindestens eine Woche nicht neu zu formatieren, um sicherzustellen, dass alle erforderlichen Daten auf den Zielserver migriert wurden. Nachdem Sie sichergestellt haben, dass alle Daten migriert wurden, können Sie, falls erforderlich, diesen Server im Netzwerk als sekundären Server für andere Aufgaben neu installieren.

> [!NOTE]
>  Starten Sie nach dem Herabstufen und Entfernen des Quellservers den Zielserver neu.

 Nachdem Sie den Quellserver tiefergestuft wurde, befindet er nicht in einem fehlerfreien Zustand. Wenn Sie den Quellserver wiederverwenden möchten, ist die einfachste Möglichkeit, ihn neu zu formatieren, indem Sie ein Server-Betriebssystem installieren und es anschließend für die Verwendung als zusätzlichen Server einrichten.

## <a name="next-steps"></a>Nächste Schritte
 Sie haben den Quell Server tiefer gestuft und aus dem neuen Windows Server Essentials-Netzwerk entfernt. Gehen Sie jetzt zu [Schritt 7: Ausführen von Aufgaben nach der Migration für die Migration zu Windows Server Essentials](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md).


Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).