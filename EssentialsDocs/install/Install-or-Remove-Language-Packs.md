---
title: Installieren oder Entfernen von Sprachpaketen
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4f7657f3ecb3450b5253d1cfe2813c12ecc2718e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311720"
---
# <a name="install-or-remove-language-packs"></a>Installieren oder Entfernen von Sprachpaketen

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Abbild erstellen, wie in den [Sprachpaketen und der Bereitstellung](https://technet.microsoft.com/library/hh824829) beschrieben, bevor Sie das Windows Server Essentials-Sprachpaket hinzufügen.  
  
 Sprachpakete sind nur für das Erstellen mehrsprachiger Abbilder verfügbar. Die Informationen in diesem Abschnitt beziehen sich speziell auf das Installieren oder Entfernen von Sprachpaketen in Windows Server Essentials.  
  
> [!NOTE]
>  Wenn Sie die Erstkonfiguration über einen Clientcomputer ausgeführt haben, der ostasiatische Sprachen nicht unterstützt, beispielsweise ja-jp, und wenn Englisch im mehrsprachigen Abbild auf dem Server nicht enthalten ist, werden auf der Webseite der Erstkonfiguration Quadrate angezeigt. Damit auf der Webseite der Erstkonfiguration Englisch voreingestellt ist, muss das von Ihnen erstellte mehrsprachige Abbild Englisch enthalten.  
  
## <a name="adding-language-packs-to-an-image"></a>Hinzufügen von Sprachpaketen zu einem Abbild  
 Sprachpakete sind auf der DVD zur OEM-Anpassung enthalten. Es wird empfohlen, die Sprachpakete auf Ihren Referenzcomputer zu kopieren, bevor sie dem Abbild hinzugefügt werden.  
  
 Verwenden Sie den folgenden Befehl, um Sprachpakete zu installieren:  
  
 **"dismus. exe/Online/Add-Package/PackagePath: C:\\< vollständiger Pfad zum CAB-Dateiverzeichnis\>\lp.cab**  
  
 Mit dem folgenden Befehl wird ein Sprachpaket für Deutsch hinzugefügt:  
  
 **"dismus. exe"/Online/Add-Package/PackagePath: C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-DE\lp.cab**  
  
> [!IMPORTANT]
>  Sie müssen auch Sprachpakete für Windows Server Essentials anwenden, um das Betriebssystem vollständig zu lokalisieren.  
  
## <a name="removing-language-packs-from-an-image"></a>Entfernen von Sprachpaketen aus einem Abbild  
 Verwenden Sie den folgenden Befehl, um ein Sprachpaket zu entfernen, das nicht länger Bestandteil eines Abbilds sein soll.  
  
 **"dismus. exe/Online/Remove-Package/PackagePath: C:\\< vollständiger Pfad zum CAB-Dateiverzeichnis\>\lp.cab**  
  
 Mit dem folgenden Befehl wird ein Sprachpaket für Deutsch entfernt:  
  
 **"dismus. exe"/Online/Remove-Package/PackagePath: C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-DE\lp.cab**  
  
## <a name="see-also"></a>Weitere Informationen  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

