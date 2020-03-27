---
title: Hinzufügen von Informationen zum zuständigen Partner im Rahmen des Microsoft Online Services-Partnervertrags
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ec8387c59ebf42eb4287807e5959a50cea4215c4
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310246"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Hinzufügen von Informationen zum zuständigen Partner im Rahmen des Microsoft Online Services-Partnervertrags

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Wenn Sie ein Microsoft Online Services-Partner Vertragspartner für Office 365 sind, müssen Sie zum sicherstellen, dass Sie ordnungsgemäß kompensiert werden, wenn eine Abonnement Anforderung über das Office 365-Integrationsmodul aus Windows Server Essentials stammt, eine Registrierungsschlüssel, der die Identifikations-ID (Partner-of-Record Identification, por ID) enthält. Die folgenden Informationen werden gelesen und über die Anmelde-URLs für Office 365 an den Dienstanbieter übermittelt.  
  
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
  
6.  Geben Sie **Partner** als Namen der Zeichenfolge ein, und drücken Sie dann die EINGABETASTE.  
  
7.  Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **Partner**, und klicken Sie dann auf **Ändern**.  
  
8.  Geben Sie im Feld **Wert** die POR ID ein, und klicken Sie anschließend auf **OK**.  
  
## <a name="see-also"></a>Weitere Informationen  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

