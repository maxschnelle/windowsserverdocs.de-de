---
title: Installieren oder Entfernen von Sprachpaketen
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 64e982f7932f8ba3ecf83ffe6443391522ad0f12
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267551"
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
  
 **dism.exe/Online/Add-Package/PackagePath: C: \\<vollständiger Pfad zum Verzeichnis der CAB-Datei \>\lp.cab**  
  
 Mit dem folgenden Befehl wird ein Sprachpaket für Deutsch hinzugefügt:  
  
 **dism.exe /online /Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  Sie müssen auch Sprachpakete für Windows Server Essentials anwenden, um das Betriebssystem vollständig zu lokalisieren.  
  
## <a name="removing-language-packs-from-an-image"></a>Entfernen von Sprachpaketen aus einem Abbild  
 Verwenden Sie den folgenden Befehl, um ein Sprachpaket zu entfernen, das nicht länger Bestandteil eines Abbilds sein soll.  
  
 **dism.exe/Online/Remove-Package/PackagePath: C: \\<vollständiger Pfad zum Verzeichnis der CAB-Datei \>\lp.cab**  
  
 Mit dem folgenden Befehl wird ein Sprachpaket für Deutsch entfernt:  
  
 **dism.exe /online /Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>Weitere Informationen  

 [Erstellen und Anpassen des Bilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

