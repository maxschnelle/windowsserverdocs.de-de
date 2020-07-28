---
title: 'Schritt 2: Installieren von Windows Server Essentials als neuen Replikatsdomänencontroller'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6efaaf1e7c9bdc6cf4224700feeae463a1bb8883
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180476"
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>Schritt 2: Installieren von Windows Server Essentials als neuen Replikatsdomänencontroller

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

In diesem Abschnitt wird beschrieben, wie Sie Windows Server Essentials und Windows Server 2012 R2 Standard (mit aktivierter Rolle "Windows Server Essentials-Rolle") als Domänen Controller installieren.

 Für Umgebungen mit bis zu 25 Benutzern und 50 Geräten können Sie die Schritte in dieser Anleitung befolgen, um von früheren Versionen von Windows SSB zu Windows Server Essentials zu migrieren. Für Umgebungen mit bis zu 100 Benutzern und 200 Geräten können Sie denselben Leitfaden befolgen, um zu den Standard-und Datacenter-Editionen von Windows Server 2012 R2 mit installierter Windows Server Essentials-Umgebung zu migrieren. In dieser Dokumentation werden beide Szenarien behandelt.

> [!IMPORTANT]
>  Wenn Sie zu Windows Server Essentials migrieren, wird die folgende Fehlermeldung täglich in der Karenzzeit von 21 Tagen zum Ereignisprotokoll hinzugefügt, bis Sie den Quell Server aus dem Netzwerk entfernen. Nach der Toleranzperiode von 21 Tagen wird der Quellserver heruntergefahren. <br> **Die FSMO-Rollen Überprüfung hat eine Bedingung in Ihrer Umgebung erkannt, die nicht mit der Lizenzierungs Richtlinie konform ist. Der Verwaltungs Server muss den primären Domänen Controller und die Domänen Namen-Master Active Directory Rollen enthalten. Verschieben Sie die Active Directory Rollen jetzt auf den Verwaltungs Server. Dieser Server wird automatisch heruntergefahren, wenn das Problem nicht innerhalb von 21 Tagen nach der ersten Erkennung dieses Zustands behoben wird**.

#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>Installieren von Windows Server Essentials oder Windows Server 2012 R2 Standard auf dem Ziel Server

1.  Installieren Sie Windows Server Essentials oder Windows Server 2012 R2 Standard mit aktivierter Rolle "Windows Server Essentials-Rolle", indem Sie die Anweisungen unter [Installieren und Konfigurieren von Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)befolgen.

    > [!NOTE]
    >  Wenn der Windows Server Essentials-Konfigurationsassistent gestartet wird, brechen Sie ihn ab.

2.  Übertragen Sie die FSMO-Rollen vom Quellserver.

    > [!NOTE]
    >  Wenn Windows Server Essentials der einzige Domänen Controller in der Domäne ist, wird die FSMO-Rolle automatisch auf den Server verschoben, auf dem Windows Server Essentials ausgeführt wird, wenn Sie den Quell Server herabstufen.

3.  Öffnen Sie Server-Manager, und führen Sie den Assistenten zum Hinzufügen von Rollen und Features aus.

4.  Sofern nicht installiert, fügen Sie die Rolle „Windows Server Essentials Experience“ hinzu.

5.  Nach der Installation der Rolle „Windows Server Essentials Experience“ wird die Aufgabe „Windows Server Essentials konfigurieren“ im Benachrichtigungsbereich angezeigt. Klicken Sie auf die Aufgabe, um den Assistenten zum Konfigurieren von Windows Server Essentials zu starten.

6.  Befolgen Sie die Anweisungen zum Abschließen der Konfiguration von Windows Server Essentials. Bevor Sie den Assistenten ausführen, führen Sie folgende Schritte aus:

    -   Ändern Sie ggf. den Namen des Servers, da Sie den Namen nach Abschluss des Konfiguratoinsassistenten von Windows Server Essentials nicht mehr ändern können.

    -   Stellen Sie sicher, dass die Zeit und die Einstellungen des Servers korrekt sind.

7.  Überprüfen Sie die Installation wie folgt:

    1.  Öffnen Sie das Dashboard.

    2.  Klicken Sie auf die Registerkarte **Benutzer**, und stellen Sie sicher, dass die Benutzerkonten in Active Directory aufgeführt sind.

### <a name="transfer-the-operations-master-roles"></a>Übertragen der Betriebsmasterrollen
 Die Betriebs Master Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet) müssen innerhalb von 21 Tagen nach der Installation von Windows Server Essentials auf dem Zielserver vom Quell Server auf den Zielserver übertragen werden.

##### <a name="to-transfer-the-operations-master-roles"></a>So übertragen Sie Betriebsmasterrollen

1.  Öffnen Sie auf dem Zielserver ein Eingabeaufforderungsfenster als Administrator. Informationen hierzu finden Sie unter [Öffnen eines Eingabeaufforderungsfensters als Administrator](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx).

2.  Geben Sie an der Eingabeaufforderung **NETDOM QUERY FSMO** ein, und drücken Sie dann die EINGABETASTE.

3.  Geben Sie an der Eingabeaufforderung **ntdsutil** ein, und drücken Sie dann die EINGABETASTE.

4.  An der Eingabeaufforderung **ntdsutil** geben Sie die folgenden Befehle ein:

    1.  Geben Sie **activate instance NTDS** ein, und drücken Sie dann die EINGABETASTE.

    2.  Geben Sie **roles** ein, und drücken Sie dann die EINGABETASTE.

    3.  Geben Sie **connections** ein, und drücken Sie dann die EINGABETASTE.

    4.  Geben Sie **Connect to Server<Server** *Name \> * ein (wobei *<Server \> * Name der Name des Zielservers ist), und drücken Sie dann die EINGABETASTE.

    5.  Geben Sie an der Eingabeaufforderung **q** ein, und drücken Sie dann die EINGABETASTE.

        1.  Geben Sie **transfer PDC** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.

        2.  Geben Sie **transfer infrastructure master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.

        3.  Geben Sie **transfer naming master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.

        4.  Geben Sie **transfer RID master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.

        5.  Geben Sie **transfer schema master** ein, drücken Sie die EINGABETASTE, und klicken Sie dann im Dialogfeld **Bestätigung der Funktionenübertragung** auf **Ja**.

    6.  Geben Sie **q** ein, und drücken Sie dann die EINGABETASTE, bis Sie zur Eingabeaufforderung zurückkehren.

> [!NOTE]
>  Auf einem beliebigen Server im Netzwerk können Sie sich vergewissern, dass die Betriebsmasterrollen auf den Zielserver übertragen wurden. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator (weitere Informationen finden Sie unter [Öffnen eines Eingabeaufforderungsfensters als Administrator](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)). Geben Sie **netdom query fsmo** ein, und drücken Sie dann die EINGABETASTE.

## <a name="next-steps"></a>Nächste Schritte
 Sie haben Windows Server Essentials als neuen Replikat Domänen Controller installiert. Gehen Sie jetzt zu [Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

