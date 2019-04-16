---
title: "Ersetzen Sie Office 365-Integration Modul kaufen Try-Endpunkt-URL zur Unterstützung von Microsoft Online Service Reseller Agreement"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Ersetzen Sie Office 365-Integration Modul kaufen Try-Endpunkt-URL zur Unterstützung von Microsoft Online Service Reseller Agreement

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_O365"></a>   
 Wenn Sie ein Microsoft Online Service Reseller Agreement ANMELDETRANSAKTIONEN-Partner, um sicherzustellen, dass kundenanmeldungen über Ihr Portal verarbeitet werden können, müssen Sie die von der Windows Server Essentials Office365-Integrationsmodul verwendete Endpunkt-URLs ersetzen.  
  
 Das Integrationsmodul werden die folgenden vier Endpunkt-URLs verwendet:  
  
1.  Ein Office365 Enterprise-Abonnement-Kauf-Endpunkt.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ-Wert  
  
    -   Schlüsselname = MOSRASTDBUY  
  
    -   Wert = *Xxxxx*, wobei Xxxxx die Abonnement-URL Enterprise ist. Wert, z.B. = http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Ein Office365 Enterprise-Abonnement Testversion Endpunkt.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ-Wert  
  
    -   Schlüsselname = MOSRASTDTRY  
  
    -   Wert = *Xxxxx*, wobei Xxxxx die Abonnement-URL Enterprise ist. Wert, z.B. = http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Ein Office365 Small Business Premium-Abonnement-Kauf-Endpunkt.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ-Wert  
  
    -   Schlüsselname = MOSRALITEBUY  
  
    -   Wert = *Xxxxx*, wobei Xxxxx die Abonnement-URL Enterprise ist. Wert, z.B. = http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Ein Office365 Small Business Premium-Abonnement Probeversion-Endpunkt.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Typ = REG-SZ-Wert  
  
    -   Schlüsselname = MOSRALITETRY  
  
    -   Wert = *Xxxxx*, wobei Xxxxx die Abonnement-URL Enterprise ist. Wert, z.B. = http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>Einen Endpunkt-URL-Schlüssel zur Registrierung hinzufügen  
  
1.  Klicken Sie auf dem Referenzcomputer auf **starten**, Typ **Regedit**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**, und erweitern Sie dann **MSO**.  
  
3.  Wenn "Mso" nicht vorhanden ist, mit der rechten Maustaste **Windows Server**, zeigen Sie auf **neu**, klicken Sie auf **Schlüssel**, und geben Sie dann **MSO** für den Namen des Schlüssels.  
  
4.  Maustaste auf "Mso", und klicken Sie dann auf **Zeichenfolgenwert**. Geben Sie einen der folgenden Endpunkt Zeichenfolgennamen für den Namen der Zeichenfolge:  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  Mit der rechten Maustaste im rechten Bereich der neuen Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
6.  Geben Sie Ihren neuen Endpunkt-URL in die **Wert** Textfeld ein, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die Schritte4 bis 6 für jeden in Schritt4 aufgeführten Zeichenfolgennamen.  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)[erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

