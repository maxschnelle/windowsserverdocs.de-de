---
title: 'Schritt6: Tieferstufen Sie und entfernen Sie des Quellservers aus dem neuen Windows Server Essentials-Netzwerk'
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86244c66-2c5e-488d-adb8-112e1ca3e2e1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 24a1f2da2333c7e6854e9efd9d996391d0fcb3b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="step-6-demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network"></a>Schritt6: Tieferstufen Sie und entfernen Sie des Quellservers aus dem neuen Windows Server Essentials-Netzwerk

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Nach Abschluss der Installation von Windows Server Essentials und die Migration durchführen, müssen Sie die folgenden Aufgaben ausführen:  
  
1.  [Entfernen der Active Directory-Zertifikatsdienste](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_ADCS)  
  
2.  [Trennen Sie die Verbindung, die direkt auf dem Quellserver verbunden sind](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)  
  
3.  [Den Quellserver tiefer stufen](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)  
  
4.  [Entfernen und wiederverwenden des Quellservers](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)  
  
##  <a name="BKMK_ADCS"></a>Entfernen der Active Directory-Zertifikatsdienste  
 Das Verfahren ist geringfügig, wenn Sie mehrere Rollendienste für Active Directory-Zertifikatdienste (AD CS) auf einem einzelnen Server installiert haben. Sie können das folgende Verfahren zum Deinstallieren eines AD CS-Rollendiensts und beibehalten anderer AD CS-Rollendienste verwenden.  
  
 Um dieses Verfahren abzuschließen, müssen Sie sich mit den gleichen Berechtigungen wie der Benutzer anmelden, die die Zertifizierungsstelle (CA) installiert. Wenn Sie eine Unternehmenszertifizierungsstelle deinstallieren möchten, ist Mitglied der Gruppe Organisations-Admins oder die Entsprechung mindestens erforderlich, um dieses Verfahren ausführen.  
  
#### <a name="to-remove-ad-cs"></a>So entfernen Sie AD CS  
  
1.  Melden Sie sich an den Quellserver als Domänenadministrator an.  
  
2.  Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Server-Manager**.  
  
3.  Klicken Sie auf **Weiter** in der **User Account Control** Dialogfeld.  
  
4.  In der **Rollenübersicht** auf **Entfernen von Rollen**.  
  
5.  Klicken Sie im Assistenten zum Entfernen von Rollen auf **Weiter**.  
  
6.  Deaktivieren der **Active Directory Certificate Services**, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Entfernungsauswahl bestätigen** Seite, überprüfen Sie die Informationen, und klicken Sie dann auf **entfernen**.  
  
    > [!NOTE]
    >  Wenn Internetinformationsdienste (Internet Information Services, IIS) ausgeführt wird, werden Sie aufgefordert, zum Beenden des Diensts, bevor Sie fortfahren. Klicken Sie auf **OK**.  
  
    > [!NOTE]
    >  Zunächst müssen Sie entfernen **Zertifizierungsstellen-Webregistrierung**, wenn es installiert ist.  
  
8.  Nach Abschluss des Assistenten zum Entfernen von Rollen, starten Sie den Server, um die Deinstallation abzuschließen.  
  
    > [!IMPORTANT]
    >  Starten Sie den Server neu, auch wenn Sie nicht dazu aufgefordert werden.  
  
##  <a name="BKMK_PhysicallyDisconnect"></a>Trennen Sie die Verbindung, die direkt auf dem Quellserver verbunden sind  
 Bevor Sie den Quellserver tiefer stufen, trennen Sie physisch alle Drucker, die direkt auf dem Quellserver verbunden sind und über den Quellserver freigegeben werden. Stellen Sie sicher, dass keine Active Directory-Objekte für den Drucker bleiben, die direkt auf dem Quellserver verbunden waren. Die Drucker können dann direkt auf den Zielserver verbunden und in Windows Server Essentials freigegeben werden.  
  
##  <a name="BKMK_DemoteTheSourceServer"></a>Den Quellserver tiefer stufen  
 Bevor Sie den Quellserver aus der Rolle des AD DS-Domänencontroller auf die Rolle des Mitgliedsservers einer Domäne herabstufen, stellen Sie sicher, dass Gruppenrichtlinieneinstellungen auf allen Clientcomputern angewendet werden, wie im folgenden Verfahren beschrieben.  
  
> [!IMPORTANT]
>  Der Quellserver und Zielserver müssen mit dem Netzwerk verbunden werden, während Änderungen an den Gruppenrichtlinien auf den Clientcomputern aktualisiert werden.  
  
#### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>Um eine Aktualisierung der Gruppenrichtlinie auf einem Clientcomputer erzwingen  
  
1.  Melden Sie sich an den Clientcomputer als Administrator.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster als Administrator.  
  
3.  Geben Sie an der Eingabeaufforderung **Gpupdate/force**, und drücken Sie dann die EINGABETASTE.  
  
4.  Der Prozess kann es nötig sein, melden Sie sich ab und melden Sie sich wieder beendet. Klicken Sie auf **Ja** zu bestätigen.  
  
 Zum Tieferstufen des Servers, wenn Sie von Windows Server Essentials oder Vorgängerversionen migrieren, finden Sie unter [Entfernen von Active Directory-Domänendienste](https://technet.microsoft.com/library/hh472163.aspx). Nachdem Sie den Quellserver als Mitglied einer Arbeitsgruppe hinzufügen und ihn vom Netzwerk trennen, müssen Sie es aus AD DS auf dem Zielserver entfernen.  
  
 Wenn Sie von Windows Server Essentials migrieren, verwenden Sie Server-Manager zum Entfernen der Active Directory-Domänendienste-Rolle dabei zum Tieferstufen des Domänencontrollers auf dem Quellserver mithilfe des folgenden Verfahrens:  
  
#### <a name="to-remove-the-source-server-from-active-directory"></a>So entfernen den Quellserver aus Active Directory  
  
1.  Öffnen Sie auf dem Zielserver **Active Directory-Benutzer und -Computer**.  
  
2.  In der **Active Directory-Benutzer und -Computer** Navigationsbereich, erweitern Sie den Domänennamen und erweitern Sie dann **Computer**.  
  
3.  Wenn der Quellserver noch in der Liste der Server vorhanden ist, Maustaste auf den Namen des Quellservers, und klicken Sie auf **löschen**, und klicken Sie dann auf **Ja**.  
  
4.  Stellen Sie sicher, dass der Quellserver nicht aufgeführt ist, und schließen Sie dann **Active Directory-Benutzer und -Computer**.  
  
##  <a name="BKMK_RemoveTheSourceServer"></a>Entfernen und wiederverwenden des Quellservers  
 Deaktivieren Sie den Quellserver und dem Netzwerk trennen. Es wird empfohlen, dass Sie nicht neu zu, den Quellserver für mindestens eine Woche formatieren, um sicherzustellen, dass alle erforderlichen Daten zum Zielserver migriert. Nachdem Sie überprüft haben, dass alle Daten migriert wurden, können Sie diesen Server im Netzwerk als sekundärer Server für andere Aufgaben neu installieren bei Bedarf.  
  
> [!NOTE]
>  Nach dem Herabstufen und des Quellservers entfernen, starten Sie den Zielserver neu.  
  
 Nachdem Sie den Quellserver tiefer stufen, ist es nicht in einem fehlerfreien Zustand. Wenn Sie den Quellserver wiederverwenden möchten, ist die einfachste Möglichkeit zum Formatieren Sie es ein Server-Betriebssystem installieren und dann für die Verwendung als zusätzlichen Server einrichten.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben die tiefer gestuft und den Quellserver aus dem neuen Windows Server Essentials-Netzwerk entfernt. Lesen Sie jetzt [Schritt7: Ausführen von Aufgaben nach der Migration für die Windows Server Essentials-Migration](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md).  
  

Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

