---
title: 'Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: a0e07d1a-8409-429b-87d7-0f4a7e14d668
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 7495831c6f593b65261fda8f50d4ef9d1000d9b4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625486"
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>Schritt 3: Hinzufügen von Computern zum neuen Windows Server Essentials-Server

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

Der nächste Schritt des Migrations Vorgangs besteht darin, Client Computer mit dem neuen Server zu verbinden, auf dem Windows Server Essentials ausgeführt wird.

> [!NOTE]
>  Sie können diesen Schritt bei Computern überspringen, auf denen die Betriebssysteme Windows XP oder Windows Vista ausgeführt werden. Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von der Windows Server-Connector-Software nicht unterstützt.

 Bevor Sie einen Client Computer mit dem neuen Windows Server Essentials-Server verbinden können, müssen Sie ihn vom Quell Server trennen, indem Sie die Windows Server Connector-Software auf dem Client Computer deinstallieren.

### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>So deinstallieren Sie Windows Server-Connector auf einem Clientcomputer

1.  Öffnen Sie auf einem Clientcomputer die Systemsteuerung und dann **Programme und Funktionen**.

2.  Klicken Sie in der Liste der Programme mit der rechten Maustaste auf die Connector-Anwendung, die auf dem Computer ausgeführt wird.

    > [!NOTE]
    >  Die Connector-Anwendung kann **Windows Small Business Server 2011 Essentials Connector**oder **Windows Server Essentials Connector**sein, je nachdem, mit welcher Version von Windows Server Essentials der Client Computer verbunden war.

3.  Klicken Sie auf **Deinstallieren**.

### <a name="to-reconnect-a-client-computer-to-the-server"></a>So verbinden Sie einen Clientcomputer erneut mit dem Server

1.  Melden Sie sich an dem Computer an, den Sie mit dem Server verbinden möchten.

    > [!NOTE]
    >  Wenn auf diesem Computer mehrere Benutzerkonten vorhanden sind, melden Sie sich mit dem Benutzerkonto an, dessen Dokumente, Bilder und persönliche Einstellungen Sie nach dem Verbinden mit dem Server beibehalten möchten.

2.  Öffnen Sie einen Internetbrowser, z. B. Internet Explorer.

3.  Geben Sie in der Adressleiste **http://<Servername \> /Connect**ein, und drücken Sie dann die EINGABETASTE.

4.  Befolgen Sie die Anweisungen auf dem Bildschirm, um den Client Computer mit dem neuen Windows Server Essentials-Server zu verbinden.

## <a name="next-steps"></a>Nächste Schritte
 Sie haben die Client Computer mit dem neuen Server verbunden, auf dem Windows Server Essentials ausgeführt wird. Gehen Sie jetzt zu [Schritt 4: Verschieben von Einstellungen und Daten auf den Ziel Server für die Migration zu Windows Server Essentials](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).


Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

