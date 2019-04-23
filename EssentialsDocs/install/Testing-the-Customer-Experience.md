---
title: Testen der Benutzerfreundlichkeit
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 223b0e1be3a53e9a7d198dc005fc8725e421db58
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838691"
---
# <a name="testing-the-customer-experience"></a>Testen der Benutzerfreundlichkeit

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Wenn Sie die Benutzerfreundlichkeit und Ihre Partneranpassungen überprüfen möchten, gehen Sie die Erstkonfiguration eines Zielcomputers durch. Sie sollten die Erstkonfiguration zumindest einmal manuell abschließen, um die Benutzerfreundlichkeit genau zu testen. Wenn Sie das Dashboard mit einem Cobranding versehen haben, müssen Sie die Erstkonfiguration abschließen, um das Branding zu überprüfen. Wenn Sie die Website für Remotewebzugriff Cobranding, müssen Sie http://<servername zugreifen\> an das branding zu überprüfen (< Servername\> ist der Name des Servers). Mit dem Abschnitt "InitialConfiguration" der Datei "cfg.ini" können Sie das Testen der Benutzerfreundlichkeit automatisieren. Weitere Informationen zum Erstellen dieses Abschnitts in der Datei "cfg.ini" finden Sie unter [Erstellen der Datei "cfg.ini"](Create-the-Cfg.ini-File.md).  
  
> [!IMPORTANT]
>  Sie müssen den Befehl "Sysprep.exe" ausführen, um das Abbild für die Bereitstellung vorzubereiten, bevor Sie die Erstkonfiguration testen. Weitere Informationen zum Ausführen von "Sysprep.exe" finden Sie unter [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md).  
  
> [!IMPORTANT]
>  Eine Netzwerkverbindung ist erforderlich, um die Erstkonfiguration zu testen. DHCP ist auf dem Server nicht konfiguriert oder installiert, sodass Netzwerktests ohne Störung möglich sind.  
  
 Überprüfen Sie die Supportinformationen des Partners, indem Sie im Dashboard neben der Schaltfläche "Hilfe" auf den Pfeil nach unten klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)