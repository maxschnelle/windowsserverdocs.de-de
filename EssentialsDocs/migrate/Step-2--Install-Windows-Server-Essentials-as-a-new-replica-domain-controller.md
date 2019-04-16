---
title: "Schritt2: Installieren Sie Windows Server Essentials als neues Replikat-Domänencontroller"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>Schritt2: Installieren Sie Windows Server Essentials als neues Replikat-Domänencontroller

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

In diesem Abschnittwird beschrieben, wie Windows Server Essentials und Windows Server2012 R2 Standard (mit aktivierter Windows Server Essentials Experience-Rolle) als Domänencontroller installiert werden.  
  
 Für Umgebungen mit bis zu 25 Benutzer und 50 Geräte können Sie die Schrittein dieser Anleitung zum Migrieren von früheren Versionen von Windows SBS zu Windows Server Essentials befolgen. Für Umgebungen mit bis zu 100 Benutzern und 200 Geräten können Sie die gleiche Anweisungen zum Migrieren auf die Standard- und Datacenter-Editionen von Windows Server2012 R2 mit installierter Windows Server Essentials Experience-Rolle ausführen. In dieser Dokumentation werden beide Szenarien behandelt.  
  
> [!IMPORTANT]
>  Wenn Sie mit Windows Server Essentials migrieren, wird die folgende Fehlermeldung hinzugefügt in das Ereignisprotokoll jeden Tag während der Karenzzeit von 21Tagen bis Sie den Quellserver aus dem Netzwerk entfernen. Nach der Toleranzperiode von 21 Tagen wird der Quellserver heruntergefahren. <br> **Die Überprüfung der FSMO-Rolle wurde eine Bedingung in Ihrer Umgebung, die nicht mit der Lizenzierungsrichtlinie konform ist festgestellt. Der Verwaltungsserver muss der primäre Domänencontroller und der Domänennamenmaster Active Directory enthalten. Fahren Sie die Active Directory-Rollen jetzt an den Verwaltungsserver. Dieser Server wird werden automatisch heruntergefahren, wenn das Problem nicht innerhalb von 21Tagen ab dem Zeitpunkt korrigiert ist diese Bedingung wurde zuerst erkannt**.   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>Installieren von Windows Server Essentials oder Windows Server2012 R2 Standard auf dem Zielserver  
  
1.  Installieren von Windows Server Essentials oder Windows Server2012 R2 Standard mit aktivierter mithilfe der Anweisungen in Windows Server Essentials Experience-Rolle [installieren und Konfigurieren von Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  
  
    > [!NOTE]
    >  Wenn die konfigurieren Windows Server Essentials-Konfigurationsassistent gestartet wird, brechen Sie es.  
  
2.  Übertragen Sie die FSMO-Rollen vom Quellserver.  
  
    > [!NOTE]
    >  Wenn Windows Server Essentials der einzige Domänencontroller in der Domäne ist, wird die FSMO-Rolle automatisch verschoben, mit dem Server mit Windows Server Essentials, wenn Sie den Quellserver tiefer stufen.  
  
3.  Öffnen Sie Server-Manager, und führen Sie den Assistenten zum Hinzufügen von Rollen und Features.  
  
4.  Wenn nicht installiert ist, fügen Sie Windows Server Essentials Experience-Rolle hinzu.  
  
5.  Nach der Installation von Windows Server Essentials Experience-Rolle wird das Konfigurieren von Windows Server Essentials-Aufgabe im Infobereich angezeigt. Klicken Sie auf die Aufgabe, um das Konfigurieren von Windows Server Essentials-Assistenten zu starten.  
  
6.  Führen Sie die Anweisungen zum Abschließen der Konfiguration von Windows Server Essentials. Bevor Sie den Assistenten ausführen, führen Sie folgende Schritteaus:  
  
    -   Ändern Sie ggf. den Namen des Servers, da Sie den Namen nicht ändern können, nachdem Sie die konfigurieren Sie Windows Server Essentials-Assistenten abgeschlossen haben.  
  
    -   Stellen Sie sicher, dass die Zeit und die Einstellungen richtig sind.  
  
7.  Überprüfen Sie die Installation wie folgt aus:  
  
    1.  Öffnen Sie das Dashboard.  
  
    2.  Klicken Sie auf **Benutzer** Registerkarte, und stellen Sie sicher, dass die Benutzerkonten in Active Directory aufgeführt sind.  
  
### <a name="transfer-the-operations-master-roles"></a>Übertragen der Betriebsmasterrollen  
 Die (auch als flexible einfache Mastervorgänge oder FSMO bezeichnet) Betriebsmasterrollen müssen innerhalb von 21Tagen nach der Installation von Windows Server Essentials auf dem Zielserver vom Quellserver auf den Zielserver übertragen werden.  
  
##### <a name="to-transfer-the-operations-master-roles"></a>Übertragen der Betriebsmasterrollen  
  
1.  Öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator. Weitere Informationen finden Sie unter [, öffnen Sie ein Eingabeaufforderungsfenster als Administrator](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx).  
  
2.  Geben Sie an der Eingabeaufforderung **NETDOM QUERY FSMO**, und drücken Sie dann die EINGABETASTE.  
  
3.  Geben Sie an der Eingabeaufforderung **Ntdsutil**, und drücken Sie dann die EINGABETASTE.  
  
4.  Bei der **Ntdsutil** Befehlszeile verwenden, geben Sie die folgenden Befehle:  
  
    1.  Typ **aktivieren Instance NTDS**, und drücken Sie dann die EINGABETASTE.  
  
    2.  Typ **Rollen**, und drücken Sie dann die EINGABETASTE.  
  
    3.  Typ **Verbindungen**, und drücken Sie dann die EINGABETASTE.  
  
    4.  Typ **mit Server verbinden***< ServerName\ >* (wobei *< ServerName\ >* ist der Name des Zielservers), und drücken Sie dann die EINGABETASTE.  
  
    5.  Geben Sie an der Eingabeaufforderung **q**, und drücken Sie dann die EINGABETASTE.  
  
        1.  Typ **transfer PDC**, drücken Sie die EINGABETASTE, und klicken Sie dann auf **Ja** in der **Bestätigung** Dialogfeld.  
  
        2.  Typ **Transfer Infrastructure Master**, drücken Sie die EINGABETASTE, und klicken Sie dann auf **Ja** in der **Bestätigung** Dialogfeld.  
  
        3.  Typ **transfer naming Master**, drücken Sie die EINGABETASTE, und klicken Sie dann auf **Ja** in der **Bestätigung** Dialogfeld.  
  
        4.  Typ **Transfer RID-Master**, drücken Sie die EINGABETASTE, und klicken Sie dann auf **Ja** in der **Bestätigung** Dialogfeld.  
  
        5.  Typ **Transfer Schemamaster**, drücken Sie die EINGABETASTE, und klicken Sie dann auf **Ja** in der **Bestätigung** Dialogfeld.  
  
    6.  Typ **q**, und drücken Sie dann die EINGABETASTE, bis Sie zur Eingabeaufforderung zurückkehren.  
  
> [!NOTE]
>  Auf einem beliebigen Server im Netzwerk stellen Sie sicher, dass die Betriebsmasterrollen auf den Zielserver übertragen wurden. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator (Weitere Informationen finden Sie unter [, öffnen Sie ein Eingabeaufforderungsfenster als Administrator](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)). Typ **Netdom Query Fsmo**, und drücken Sie dann die EINGABETASTE.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben Windows Server Essentials als einen neuen Replikatdomänencontroller installiert. Lesen Sie jetzt [Schritt3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).  
  
Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

