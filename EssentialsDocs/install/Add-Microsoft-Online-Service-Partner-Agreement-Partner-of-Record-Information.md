---
title: "Microsoft Online Service Partner Agreement Partner-of-Record Informationen hinzufügen"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Microsoft Online Service Partner Agreement Partner-of-Record Informationen hinzufügen

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>   
 Wenn Sie ein Microsoft Online Service Partner Agreement (Rahmen)-Partner für Office365 sind, um sicherzustellen, dass Sie korrekte Vergütung erhalten, wenn eine aus Windows Server Essentials über das Office365-Integrationsmodul abonnementanfrage dazu Sie einen Registrierungsschlüssel erstellen, der Ihre Partner-of-Record Identification (POR ID) enthält. Die folgende Informationen wird lesen und die Office365-Anmeldung URLs an den Dienstanbieter weitergegeben.  
  
-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO  
  
-   Typ = Zeichenfolge  
  
-   Schlüsselname = Partner  
  
-   Wert = Xxxxx, wobei Xxxxx die POR ID ist  
  
#### <a name="to-add-the-por-id-key-to-the-registry"></a>Die POR ID-Schlüssel zur Registrierung hinzufügen  
  
1.  Klicken Sie auf dem Referenzcomputer auf **starten**, Typ **Regedit**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, und erweitern Sie dann **Windows Server**.  
  
3.  Mit der rechten Maustaste **Windows Server**, zeigen Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
4.  Typ **MSO** für den Namen des Schlüssels.  
  
5.  Maustaste, die Sie gerade erstellt haben, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Typ **Partner** für den Namen der Zeichenfolge ein, und drücken Sie dann die EINGABETASTE.  
  
7.  Mit der rechten Maustaste die neue **Partner** im rechten Bereich eine Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
8.  Geben Sie Ihre POR-ID in die **Wert** Textfeld ein, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

