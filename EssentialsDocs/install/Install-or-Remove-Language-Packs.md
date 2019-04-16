---
title: Installieren oder Entfernen von Language Packs
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a41b491bbe4b4a8ee7f9743dc85e5bdaffb08496
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-or-remove-language-packs"></a>Installieren oder Entfernen von Language Packs

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Image erstellen, wie beschrieben in die [Language Packs und Bereitstellung](https://technet.microsoft.com/library/hh824829) , bevor Sie das Windows Server Essentials-Sprachpaket hinzufügen.  
  
 Sprachpakete sind nur für das Erstellen mehrsprachiger Abbilder verfügbar. Die Informationen in diesem Abschnitt sind speziell das Installieren und Entfernen von Language Packs für Windows Server Essentials.  
  
> [!NOTE]
>  Wenn Sie beabsichtigen, die anfängliche Konfiguration (IC) von einem Clientcomputer ausführen, der ostasiatische Sprachen, z. B. ja-jp, nicht unterstützt, und wenn Englisch im mehrsprachigen Abbild auf dem Server nicht enthalten ist, wird die Webseite der Erstkonfiguration Quadrate angezeigt. Für die Webseite der Erstkonfiguration Englisch muss das mehrsprachige Image, das Sie erstellen Englisch enthalten.  
  
## <a name="adding-language-packs-to-an-image"></a>Hinzufügen von Sprachpaketen zu einem Bild  
 Language Packs sind auf der OEM-Anpassung DVD zur Verfügung. Es wird empfohlen, dass die Language Packs auf Ihren Referenzcomputer kopieren, bevor Sie das Image Sprachpakete hinzu.  
  
 Sie müssen den folgenden Befehl verwenden, um Sprachpakete zu installieren:  
  
 **DISM.exe / online/Add-Package /PackagePath:C: \\ < Vollständiger Pfad zur CAB-Datei Directory\ > \lp.cab**  
  
 Der folgende Befehl zeigt z. B. ein Sprachpaket hinzufügen:  
  
 **DISM.exe / online/Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  Sie müssen auch Sprachpakete für Windows Server Essentials, um das Betriebssystem vollständig zu lokalisieren anwenden.  
  
## <a name="removing-language-packs-from-an-image"></a>Entfernen von Language Packs aus einem Bild  
 Sie können den folgenden Befehl verwenden, ein Sprachpaket zu entfernen, die Sie nicht mehr in ein Bild aufnehmen möchten:  
  
 **DISM.exe / online/Remove-Package /PackagePath:C: \\ < Vollständiger Pfad zur CAB-Datei Directory\ > \lp.cab**  
  
 Der folgende Befehl zeigt z. B. ein Sprachpaket zu entfernen:  
  
 **DISM.exe / online/Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

