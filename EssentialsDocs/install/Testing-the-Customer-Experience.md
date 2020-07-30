---
title: Testen der Benutzerfreundlichkeit
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f639f01a96f55bcf7b9f8c0e19f02862f4e06a88
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181086"
---
# <a name="testing-the-customer-experience"></a>Testen der Benutzerfreundlichkeit

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie die Benutzerfreundlichkeit und Ihre Partneranpassungen überprüfen möchten, gehen Sie die Erstkonfiguration eines Zielcomputers durch. Sie sollten die Erstkonfiguration zumindest einmal manuell abschließen, um die Benutzerfreundlichkeit genau zu testen. Wenn Sie das Dashboard mit einem Cobranding versehen haben, müssen Sie die Erstkonfiguration abschließen, um das Branding zu überprüfen. Wenn Sie die Remote Webzugriff Website mit einem Namen versehen haben, müssen Sie auf http://<Servername zugreifen, \> um das Branding zu überprüfen (<Server \> Name ist der Name des Servers). Mit dem Abschnitt "InitialConfiguration" der Datei "cfg.ini" können Sie das Testen der Benutzerfreundlichkeit automatisieren. Weitere Informationen zum Erstellen dieses Abschnitts in der Datei "cfg.ini" finden Sie unter [Erstellen der Datei "cfg.ini"](Create-the-Cfg.ini-File.md).

> [!IMPORTANT]
>  Sie müssen den Befehl "Sysprep.exe" ausführen, um das Abbild für die Bereitstellung vorzubereiten, bevor Sie die Erstkonfiguration testen. Weitere Informationen zum Ausführen von "Sysprep.exe" finden Sie unter [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md).

> [!IMPORTANT]
>  Eine Netzwerkverbindung ist erforderlich, um die Erstkonfiguration zu testen. DHCP ist auf dem Server nicht konfiguriert oder installiert, sodass Netzwerktests ohne Störung möglich sind.

 Überprüfen Sie die Supportinformationen des Partners, indem Sie im Dashboard neben der Schaltfläche "Hilfe" auf den Pfeil nach unten klicken.

## <a name="see-also"></a>Weitere Informationen
 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)