---
title: Erstellen eines einfachen benutzerdefinierten Abbilds
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: c4b1d0bde98ee162d099976f4ac4db49c9deb773
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623829"
---
# <a name="create-a-simple-customized-image"></a>Erstellen eines einfachen benutzerdefinierten Abbilds

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können ein einfaches benutzerdefiniertes Abbild mit dem folgenden Verfahren erstellen:

#### <a name="to-create-the-image"></a>So erstellen Sie das Abbild

1.  Drücken Sie nach der Serverinstallation auf der ersten Seite der Erstkonfiguration UMSCHALT+F10, um das Befehlsfenster zu öffnen.

2.  Erstellen Sie unter dem Stammverzeichnis des Systemlaufwerks eine Datei "SkipIC.txt".

3.  Starten Sie den Server neu.

4.  Starten Sie den Server mithilfe eines USB-Speichersticks oder einer DVD, der bzw. die die Datei "unattend.xml" enthält. Weitere Informationen zum Erstellen eines startfähigen USB-Speichersticks finden Sie unter [Erstellen eines startfähigen USB-Speichersticks](Create-a-Bootable-USB-Flash-Drive.md).

5.  Fügen Sie auf dem Dashboard ein Logo als Branding hinzu. Weitere Informationen zum Hinzufügen von Branding finden Sie unter [Hinzufügen von Branding zum Dashboard, zu Remotewebzugriff und zum Launchpad](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md).

6.  Erstellen Sie die Datei "OOBE.xml", um benutzerdefinierte Informationen wie den Firmennamen, ein Logo und den Endbenutzer-Lizenzvertrag anzuzeigen. Weitere Informationen zur Datei „OOBE.xml“ finden Sie unter [Create the Oobe.xml File Including Logo and EULA](Create-the-Oobe.xml-File-Including-Logo-and-EULA.md).

7.  Ändern Sie den standardmäßigen Servernamen, sofern Sie ihn nicht in der Datei "unattend.xml" definieren.

8.  Standardmäßig besteht der Servername aus einer zufälligen Zeichenfolge. Ändern Sie den Servernamen in eine andere Zeichenfolge (beispielsweise "ContosoServer"), und teilen Sie anschließend Ihren Kunden den neuen Servernamen mit.

9. Bereiten Sie das Abbild vor, wie unter [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) beschrieben.

## <a name="see-also"></a>Weitere Informationen
 Informationen zu den ersten Schritten [mit dem Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)