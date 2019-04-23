---
title: Hinzufügen von Informationen zum zuständigen Partner im Rahmen des Microsoft Online Services-Partnervertrags
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 39ce43228cd7392bcc86de4a410c52676ce15047
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833041"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Hinzufügen von Informationen zum zuständigen Partner im Rahmen des Microsoft Online Services-Partnervertrags

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Wenn Sie ein Microsoft Online Service Partner Agreement (Rahmen)-Partner für Office 365 sind, um sicherzustellen, dass Sie ordnungsgemäß kompensiert werden, eine Anforderung von Windows Server Essentials über das Office 365-Integrationsmodul ausbezahlt wird, wenn müssen Sie zum Erstellen einer der Registrierungsschlüssel, die Ihre Partner-of-Record-ID (POR ID) enthält. Die folgenden Informationen werden gelesen und über die Anmelde-URLs für Office 365 an den Dienstanbieter übermittelt.  
  
-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO  
  
-   Typ = Zeichenfolge  
  
-   Schlüsselname = Partner  
  
-   Wert = xxxxx, wobei xxxxx die POR ID ist  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>So fügen Sie der Registrierung den Schlüssel für die POR ID hinzu  
  
1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit** ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, **SOFTWARE**, dann **Microsoft** und schließlich **Windows Server**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
4.  Geben Sie **MSO** als Schlüsselnamen ein.  
  
5.  Klicken Sie mit der rechten Maustaste auf den gerade erstellten Schlüssel, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Geben Sie **Partner** als Namen der Zeichenfolge ein, und drücken Sie dann die  EINGABETASTE.  
  
7.  Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **Partner**, und klicken Sie dann auf **Ändern**.  
  
8.  Geben Sie im Feld **Wert** die POR ID ein, und klicken Sie anschließend auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

