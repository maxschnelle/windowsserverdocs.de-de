---
title: Installieren oder Entfernen von Sprachpaketen
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9999b78b1b0a4b1823162158b95d175f9c159091
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87837929"
---
# <a name="install-or-remove-language-packs"></a>Installieren oder Entfernen von Sprachpaketen

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Abbild erstellen, wie in den [Sprachpaketen und der Bereitstellung](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824829(v=win.10)) beschrieben, bevor Sie das Windows Server Essentials-Sprachpaket hinzufügen.

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

 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)