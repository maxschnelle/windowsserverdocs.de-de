---
title: Installieren oder Entfernen von Sprachpaketen
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860091"
---
# <a name="install-or-remove-language-packs"></a>Installieren oder Entfernen von Sprachpaketen

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Abbild erstellen, wie beschrieben in der [Sprachpakete und Bereitstellung](https://technet.microsoft.com/library/hh824829) , bevor Sie das Windows Server Essentials-Sprachpaket hinzufügen.  
  
 Sprachpakete sind nur für das Erstellen mehrsprachiger Abbilder verfügbar. Die Informationen in diesem Abschnitt sind speziell das Installieren und Entfernen von Sprachpaketen auf Windows Server Essentials.  
  
> [!NOTE]
>  Wenn Sie die Erstkonfiguration über einen Clientcomputer ausgeführt haben, der ostasiatische Sprachen nicht unterstützt, beispielsweise ja-jp, und wenn Englisch im mehrsprachigen Abbild auf dem Server nicht enthalten ist, werden auf der Webseite der Erstkonfiguration Quadrate angezeigt. Damit auf der Webseite der Erstkonfiguration Englisch voreingestellt ist, muss das von Ihnen erstellte mehrsprachige Abbild Englisch enthalten.  
  
## <a name="adding-language-packs-to-an-image"></a>Hinzufügen von Sprachpaketen zu einem Abbild  
 Sprachpakete sind auf der DVD zur OEM-Anpassung enthalten. Es wird empfohlen, die Sprachpakete auf Ihren Referenzcomputer zu kopieren, bevor sie dem Abbild hinzugefügt werden.  
  
 Verwenden Sie den folgenden Befehl, um Sprachpakete zu installieren:  
  
 **DISM.exe / online/Add-Package-Package:\\< Vollständiger Pfad zum CAB-Datei\>\lp.cab**  
  
 Mit dem folgenden Befehl wird ein Sprachpaket für Deutsch hinzugefügt:  
  
 **dism.exe /online /Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  Sie müssen auch Sprachpakete für Windows Server Essentials, um das Betriebssystem vollständig zu lokalisieren anwenden.  
  
## <a name="removing-language-packs-from-an-image"></a>Entfernen von Sprachpaketen aus einem Abbild  
 Verwenden Sie den folgenden Befehl, um ein Sprachpaket zu entfernen, das nicht länger Bestandteil eines Abbilds sein soll.  
  
 **DISM.exe / online/Remove-Package-Package:\\< Vollständiger Pfad zum CAB-Datei\>\lp.cab**  
  
 Mit dem folgenden Befehl wird ein Sprachpaket für Deutsch entfernt:  
  
 **dism.exe /online /Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

