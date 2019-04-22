---
title: 'Schritt 2: Installieren von Windows Server Essentials als ein neuer replikatsdomänencontroller'
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 757012b7d1a57a001e3b55cdc0604b63852a3d3c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816461"
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>Schritt 2: Installieren von Windows Server Essentials als ein neuer replikatsdomänencontroller

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In diesem Abschnitt wird beschrieben, wie Windows Server Essentials und Windows Server 2012 R2 Standard (mit aktivierter Windows Server Essentials Experience-Rolle) als Domänencontroller installiert werden.  
  
 Für Umgebungen mit bis zu 25 Benutzern und 50 Geräten können Sie die Schritte in diesem Handbuch Migrieren von früheren Versionen von Windows SBS zu Windows Server Essentials ausführen. Für Umgebungen mit bis zu 100 Benutzern und 200 Geräten können Sie die gleiche Anweisungen zum Migrieren auf die Standard- und Datacenter-Editionen von Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle folgen. In dieser Dokumentation werden beide Szenarien behandelt.  
  
> [!IMPORTANT]
>  Bei der Migration zu Windows Server Essentials die folgende Fehlermeldung wurde in das Ereignisprotokoll jeden Tag während der Karenzzeit 21 Tagen, bis Sie den Quellserver aus dem Netzwerk entfernen. Nach der Toleranzperiode von 21 Tagen wird der Quellserver heruntergefahren. <br> **Überprüfung der FSMO-Rolle wurde eine Bedingung in Ihrer Umgebung, die nicht mit der Lizenzierungsrichtlinie konform ist festgestellt. Der Verwaltungsserver muss die Active Directory-Rollen des primären Domänencontrollers und des Domänennamenmasters aufweisen. Verschieben Sie diese Active Directory-Rollen jetzt zum Verwaltungsserver. Dieser Server wird automatisch heruntergefahren, wenn das Problem nicht in 21 Tage ab dem Zeitpunkt behoben ist, diese Bedingung wurde zuerst erkannt**.   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>Installieren von Windows Server Essentials oder Windows Server 2012 R2 Standard auf dem Zielserver  
  
1.  Installieren von Windows Server Essentials oder Windows Server 2012 R2 Standard mit aktivierter mithilfe der Anweisungen in Windows Server Essentials Experience-Rolle [installieren und Konfigurieren von Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  
  
    > [!NOTE]
    >  Wenn der Windows Server Essentials-Konfigurationsassistent gestartet wird, brechen Sie ihn ab.  
  
2.  Übertragen Sie die FSMO-Rollen vom Quellserver.  
  
    > [!NOTE]
    >  Wenn Windows Server Essentials der einzige Domänencontroller in der Domäne ist, wird die FSMO-Rolle automatisch verschoben, an den Server, Windows Server Essentials ausgeführt wird, wenn Sie den Quellserver tiefer stufen.  
  
3.  Öffnen Sie Server-Manager, und führen Sie den Assistenten zum Hinzufügen von Rollen und Features aus.  
  
4.  Sofern nicht installiert, fügen Sie die Rolle „Windows Server Essentials Experience“ hinzu.  
  
5.  Nach der Installation der Rolle „Windows Server Essentials Experience“ wird die Aufgabe „Windows Server Essentials konfigurieren“ im Benachrichtigungsbereich angezeigt. Klicken Sie auf die Aufgabe, um den Assistenten zum Konfigurieren von Windows Server Essentials zu starten.  
  
6.  Befolgen Sie die Anweisungen zum Abschließen der Konfiguration von Windows Server Essentials. Bevor Sie den Assistenten ausführen, führen Sie folgende Schritte aus:  
  
    -   Ändern Sie ggf. den Namen des Servers, da Sie den Namen nach Abschluss des Konfiguratoinsassistenten von Windows Server Essentials nicht mehr ändern können.  
  
    -   Stellen Sie sicher, dass die Zeit des Servers und die Einstellungen richtig sind.  
  
7.  Überprüfen Sie die Installation wie folgt:  
  
    1.  Öffnen Sie das Dashboard.  
  
    2.  Klicken Sie auf die Registerkarte **Benutzer** , und stellen Sie sicher, dass die Benutzerkonten in Active Directory aufgeführt sind.  
  
### <a name="transfer-the-operations-master-roles"></a>Übertragen der Betriebsmasterrollen  
 Die (auch als flexible einfache Mastervorgänge oder FSMO bezeichnet) Betriebsmasterrollen müssen innerhalb von 21 Tagen nach der Installation von Windows Server Essentials auf dem Zielserver vom Quellserver auf den Zielserver übertragen werden.  
  
##### <a name="to-transfer-the-operations-master-roles"></a>So übertragen Sie Betriebsmasterrollen  
  
1.  Öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator. Informationen hierzu finden Sie unter [Öffnen eines Eingabeaufforderungsfensters als Administrator](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx).  
  
2.  Geben Sie an der Eingabeaufforderung **NETDOM QUERY FSMO**ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Geben Sie an der Eingabeaufforderung **ntdsutil** ein, und drücken Sie dann die EINGABETASTE.  
  
4.  An der Eingabeaufforderung **ntdsutil** geben Sie die folgenden Befehle ein:  
  
    1.  Geben Sie **activate instance NTDS**ein, und drücken Sie dann die EINGABETASTE.  
  
    2.  Geben Sie **roles** ein, und drücken Sie dann die EINGABETASTE.  
  
    3.  Geben Sie **connections** ein, und drücken Sie dann die EINGABETASTE.  
  
    4.  Typ **eine Verbindung mit Server herstellen** *< ServerName\>*  (wobei *< ServerName\>*  ist der Name des Zielservers), und drücken Sie dann die EINGABETASTE.  
  
    5.  Geben Sie an der Eingabeaufforderung **q**ein, und drücken Sie dann die EINGABETASTE.  
  
        1.  Geben Sie **transfer PDC** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.  
  
        2.  Geben Sie **transfer infrastructure master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.  
  
        3.  Geben Sie **transfer naming master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.  
  
        4.  Geben Sie **transfer RID master**ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja** .  
  
        5.  Geben Sie **transfer schema master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.  
  
    6.  Geben Sie **q**ein, und drücken Sie dann die EINGABETASTE, bis Sie zur Eingabeaufforderung zurückkehren.  
  
> [!NOTE]
>  Auf einem beliebigen Server im Netzwerk können Sie sich vergewissern, dass die Betriebsmasterrollen auf den Zielserver übertragen wurden. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator (weitere Informationen finden Sie unter [Öffnen eines Eingabeaufforderungsfensters als Administrator](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)). Geben Sie **netdom query fsmo**ein, und drücken Sie dann die EINGABETASTE.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben Windows Server Essentials als einen neuen Replikatdomänencontroller installiert. Wechseln Sie nun zur [Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).  
  
Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

