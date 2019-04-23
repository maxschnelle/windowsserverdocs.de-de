---
title: Ersetzen der Endpunkt-URLs des O365-Integrationsmoduls (Abonnement/Testabonnement) zur Unterstützung des Microsoft Online Services-Wiederverkäufervertrags
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b690cedd2f692cc6d11af6e05dd0cd4b4ea5a1d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833101"
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Ersetzen der Endpunkt-URLs des O365-Integrationsmoduls (Abonnement/Testabonnement) zur Unterstützung des Microsoft Online Services-Wiederverkäufervertrags

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>   
 Wenn Sie ein Microsoft Online Service Reseller Agreement ANMELDETRANSAKTIONEN-Partner, um sicherzustellen, dass Kunden über Ihr Portal verarbeitet werden können, müssen Sie ersetzen die Endpunkt-URLs, die von der Windows Server Essentials Office 365-Integrationsmodul verwendet.  
  
 Vom Integrationsmodul werden die folgenden vier Endpunkt-URLs verwendet:  
  
1.  Endpunkt für ein Office 365 Enterprise-Abonnement.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ  
  
    -   Schlüsselname = MOSRASTDBUY  
  
    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Zum Beispiel: Wert = http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Endpunkt für ein Office 365 Enterprise-Testabonnement.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ  
  
    -   Schlüsselname = MOSRASTDTRY  
  
    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Zum Beispiel: Wert = http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Ein Office 365 Small Business Premium-Abonnement erwerben-Endpunkt.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ  
  
    -   Schlüsselname = MOSRALITEBUY  
  
    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Zum Beispiel: Wert = http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Ein Office 365 Small Business Premium-Abonnement Testversion Endpunkt.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ  
  
    -   Schlüsselname = MOSRALITETRY  
  
    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Zum Beispiel: Wert = http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>So fügen Sie der Registrierung einen Schlüssel für die Endpunkt-URL hinzu  
  
1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit** ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Fensterbereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** und **MSO**.  
  
3.  Wenn **MSO** nicht vorhanden ist, klicken Sie mit der rechten Maustaste auf **Windows Server**, zeigen Sie auf **Neu**, klicken Sie auf „Schlüssel“, und geben Sie dann **MSO** als Namen des Schlüssels ein.  
  
4.  Klicken Sie mit der rechten Maustaste auf "MSO", und klicken Sie dann auf **Zeichenfolgenwert**. Geben Sie einen der folgenden Zeichenfolgennamen für Endpunkte als Namen der Zeichenfolge ein:  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  Klicken Sie im rechten Fensterbereich mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie anschließend auf **Ändern**.  
  
6.  Geben Sie im Feld **Wert** die neue Endpunkt-URL ein, und klicken Sie anschließend auf **OK**.  
  
7.  Wiederholen Sie die Schritte 4 bis 6 für jeden in Schritt 4 aufgeführten Zeichenfolgennamen.  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md) [erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

