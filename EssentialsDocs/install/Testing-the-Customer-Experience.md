---
title: Testen der Benutzerfreundlichkeit
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 938b64d96111a3ed128ec184acde56f20cb1abda
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819783"
---
# <a name="testing-the-customer-experience"></a>Testen der Benutzerfreundlichkeit

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie die Benutzerfreundlichkeit und Ihre Partneranpassungen überprüfen möchten, gehen Sie die Erstkonfiguration eines Zielcomputers durch. Sie sollten die Erstkonfiguration zumindest einmal manuell abschließen, um die Benutzerfreundlichkeit genau zu testen. Wenn Sie das Dashboard mit einem Cobranding versehen haben, müssen Sie die Erstkonfiguration abschließen, um das Branding zu überprüfen. Wenn Sie die Remote Webzugriff-Website mit einem Cobranding versehen haben, müssen Sie auf http://< Servername\> zugreifen, um das Branding zu überprüfen (< Servername\> ist der Name des Servers). Mit dem Abschnitt "InitialConfiguration" der Datei "cfg.ini" können Sie das Testen der Benutzerfreundlichkeit automatisieren. Weitere Informationen zum Erstellen dieses Abschnitts in der Datei "cfg.ini" finden Sie unter [Erstellen der Datei "cfg.ini"](Create-the-Cfg.ini-File.md).  
  
> [!IMPORTANT]
>  Sie müssen den Befehl "Sysprep.exe" ausführen, um das Abbild für die Bereitstellung vorzubereiten, bevor Sie die Erstkonfiguration testen. Weitere Informationen zum Ausführen von "Sysprep.exe" finden Sie unter [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md).  
  
> [!IMPORTANT]
>  Eine Netzwerkverbindung ist erforderlich, um die Erstkonfiguration zu testen. DHCP ist auf dem Server nicht konfiguriert oder installiert, sodass Netzwerktests ohne Störung möglich sind.  
  
 Überprüfen Sie die Supportinformationen des Partners, indem Sie im Dashboard neben der Schaltfläche "Hilfe" auf den Pfeil nach unten klicken.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md)