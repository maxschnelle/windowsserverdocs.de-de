---
title: Erstellen des mehrsprachigen Mediums zur Clientwiederherstellung
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 2fdbc016-d464-43cb-bd75-8a63e61588a2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4057e0d6805c7633bf07960d06d97b2eab15f28a
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838089"
---
# <a name="build-multi-language-client-restore-media"></a>Erstellen des mehrsprachigen Mediums zur Clientwiederherstellung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Abbild erstellen, wie unter Exemplarische Vorgehensweise: Erstellen von [Windows-Images](/previous-versions/windows/it-pro/windows-8.1-and-8/jj126995(v=win.10)) in mehreren Sprachen beschrieben, bevor Sie "install. wim" das Windows Server Essentials sprach Pack hinzufügen

 Beim Erstellen der mehrsprachigen Serverinstallations-DVD werden für "Install.wim" für Server die Sprachpakete installiert. Als Bestandteil des Sprachpakets werden die lokalisierten Ressourcen für den Wiederherstellungs-Assistenten installiert.

### <a name="to-build-a-multi-language-client-restore-media"></a>So erstellen Sie ein mehrsprachiges Medium zur Clientwiederherstellung

1.  Stellen Sie "Install.wim" unter "C:\mount" bereit. Der Ordner "C:\mount\Programme\Windows Server\bin\ClientRestore" wird als Stamm für das Medium der Clientwiederherstellung verwendet: [RestoreMediaRoot] im unteren Beispiel:

    ```
    dism /mount-wim /wimfile:install.wim /index:1 /mountdir:c:\mount
    ```

2.  Stellen Sie die WIM-Datei für die Clientwiederherstellung unter "[RestoreMediaRoot]\Sources\Boot.wim" bereit (für "boot_x86.wim" müssen dieselben Schritte ausgeführt werden). Die Befehlszeile lautet wie folgt:

    ```
    dism /mount-wim /wimfile:boot.wim /index:1 /mountdir:c:\mountRestore
    ```

3.  Fügen Sie dem Wiederherstellungsmedium das Paket "WinPE-Setup.cab" hinzu, indem Sie Folgendes ausführen:

    ```
    dism /image:c:\mountRestore /add-package /packagepath:WinPE-Setup.cab
    ```

4.  Bearbeiten Sie "c:\mountRestore\windows\system32\winpeshl.ini" in Editor, und fügen Sie die folgenden Inhalte hinzu:

    ```
    [LaunchApp]
    AppPath = %SYSTEMDRIVE%\sources\SelectLanguage.exe
    ```

5.  Fügen Sie dem Wiederherstellungsmedium Sprachpakete hinzu. Sprachpakete können durch Ausführen des folgenden Befehls hinzugefügt werden:

    ```
    dism /image:c:\mountRestore /add-package /packagepath:[language pack path]
    ```

     Es sind die folgenden Sprachpakete hinzuzufügen:

    1.  WinPE-Sprachpaket ("lp.cab")

    2.  WinPE-Setup-Sprachpaket ("WinPE-Setup_[lang].cab", beispielsweise "WinPE-Setup_en-us.cab")

    3.  Für asiatische Schriftarten wie zh-cn, zh-tw, zh-hk, ko-kr und ja-jp muss ein zusätzliches Schriftartenpaket installiert werden ("winpe-fontsupport-[Sprache].cab", z. B. "winpe-fontsupport-zh-cn.cab").

6.  Erstellen Sie eine neue Datei "Lang.ini". Führen Sie dazu Folgendes aus:

    ```
    dism /image:c:\mountRestore /Gen-LangINI /distribution:mount
    ```

7.  Führen Sie ein Commit des Abbilds aus, und heben Sie die Bereitstellung des Abbilds auf. Führen Sie dazu Folgendes aus:

    ```
    dism /unmount-wim /mountdir:c:\mountRestore /commit
    ```

8.  Wiederholen Sie für "[RestoreMediaroot]\Sources\Boot_x86.wim" die Schritte 2 bis 7.

9. Führen Sie ein Commit des Abbilds aus, und heben Sie die Bereitstellung des Abbilds auf. Führen Sie dazu Folgendes aus:

    ```
    dism /unmount-wim /mountdir:c:\mount /commit
    ```

## <a name="see-also"></a>Weitere Informationen

 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)