---
title: Vorbereiten der Umgebung für die Windows Admin Center
description: Vorbereiten der Umgebung für Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 598eeae64925d24ec6d97b59da9cae1e2d10585d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864971"
---
# <a name="prepare-your-environment-for-windows-admin-center"></a>Vorbereiten der Umgebung für die Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Es gibt einige Serverversionen, die zusätzliche Vorbereitung benötigen, bevor sie mit Windows Admin Center verwalten können:

- [Windows Server 2012 und 2012 R2](#prepare-windows-server-2012-and-2012-r2)
- [Windows Server 2008 R2](#prepare-windows-server-2008-r2)
- [Microsoft Hyper-V Server 2016](#prepare-microsoft-hyper-v-server-2016)
- [Microsoft Hyper-V Server 2012 R2](#prepare-microsoft-hyper-v-server-2012-r2)

## <a name="prepare-windows-server-2012-and-2012-r2"></a>Vorbereiten von Windows Server 2012 und 2012 R2

### <a name="install-wmf-version-51-or-higher"></a>Installieren von WMF Version 5.1 oder höher

Windows Admin Center erfordert PowerShell-Features, die nicht standardmäßig in Windows Server 2012 und 2012 R2 enthalten sind. Zum Verwalten von Windows Server 2012 oder 2012 R2 mit Windows Admin Center müssen Sie WMF Version 5.1 oder höher auf diesen Servern installieren.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist.

Wenn dies nicht der Fall ist, können Sie [herunterladen und WMF 5.1 installieren](https://docs.microsoft.com/powershell/wmf/5.1/install-configure).

## <a name="prepare-windows-server-2008-r2"></a>Vorbereiten von Windows Server 2008 R2

### <a name="install-wmf-version-51-or-higher"></a>Installieren von WMF Version 5.1 oder höher

Windows Admin Center erfordert PowerShell-Features, die in Windows Server 2008 R2 standardmäßig nicht enthalten sind. Zum Verwalten von Windows Server 2008 R2 mit Windows Admin Center müssen Sie WMF Version 5.1 oder höher auf diesen Servern installieren. 

Sicherstellen, dass [.NET Framework 4.5.2 oder höher](https://docs.microsoft.com/dotnet/framework/install/on-windows-7) bereits auf Ihrem Computer installiert ist.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist.

Wenn dies nicht der Fall ist, können Sie [herunterladen und WMF 5.1 installieren](https://docs.microsoft.com/powershell/wmf/5.1/install-configure).

Führen Sie `Enable-PSRemoting –force` in einer PowerShell-Konsole, um remote Powershell-Verbindung zu aktivieren. 

### <a name="enable-remote-desktop"></a>Aktivieren von Remotedesktop

Um Remotedesktop in Windows Admin Center zu verwenden, müssen Sie Remotedesktop auf Ihrem Windows Server 2008 R2-Server zu aktivieren.

**Server-Manager**wechseln Sie zu **Remotedesktop konfigurieren**. Bei aktivierter Remotedesktop "Verbindungen von Computern unter einer Version von Remotedesktop zulassen".

## <a name="prepare-microsoft-hyper-v-server-2016"></a>Vorbereiten von Microsoft Hyper-V Server 2016

Zum Verwalten von Microsoft Hyper-V Server 2016 mit Windows Admin Center sind einige Serverrollen, die Sie benötigen aktivieren, bevor Sie dies tun können.

### <a name="to-manage-microsoft-hyper-v-server-2016-with-windows-admin-center"></a>Zum Verwalten von Microsoft Hyper-V Server 2016 mit Windows Admin Center:

1. Aktivieren Sie Remoteverwaltung.
2. Aktivieren Sie die Datei-Serverrolle.
3. Aktivieren Sie Hyper-V-Modul für PowerShell.

### <a name="step-1-enable-remote-management"></a>**Schritt 1:** Remoteverwaltung aktivieren

So aktivieren Sie die Remoteverwaltung in Hyper-V Server:

1. Melden Sie sich Hyper-V Server.
2. Geben Sie an des- **Server-Konfiguration** (SCONFIG), **4** zum Konfigurieren von remote-Verwaltung.
3. Geben Sie **1** ein, um die Remoteverwaltung aktivieren.
4. Geben Sie **4**, um zum Hauptmenü zurück.

### <a name="step-2-enable-file-server-role"></a>**Schritt 2:** Aktivieren Sie die Datei-Serverrolle

So aktivieren die Dateiserverrolle für einfache Datei Dateifreigabe und remote Management:

1. Klicken Sie im Menü **Extras** auf **Rollen und Funktionen** .
2. **Rollen und Features**, suchen Sie nach **Datei und Speicherdienste**, und überprüfen **-Datei und iSCSI-Services** und **Dateiserver**:

![](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-3-enable-hyper-v-module-for-powershell"></a>**Schritt 3:** Aktivieren Sie Hyper-V-Modul für PowerShell

So aktivieren Hyper-V-Modul für PowerShell-Features:

1. Klicken Sie im Menü **Extras** auf **Rollen und Funktionen** .
2. Finden Sie in **-Rollen und-Features**die **Remoteserver-Verwaltungstools**, und überprüfen Sie **Rollenverwaltungstools** und **Hyper-V-Modul für PowerShell**:

![](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2016 ist jetzt für die Verwaltung mit Windows Admin Center bereit.

## <a name="prepare-microsoft-hyper-v-server-2012-r2"></a>Vorbereiten von Microsoft Hyper-V Server 2012 R2

Zum Verwalten von Microsoft Hyper-V Server 2012 R2 mit Windows Admin Center sind einige Serverrollen, die Sie benötigen aktivieren, bevor Sie dies tun können.  Darüber hinaus müssen Sie WMF Version 5.1 oder höher zu installieren.

### <a name="to-manage-microsoft-hyper-v-server-2012-r2-with-windows-admin-center"></a>Zum Verwalten von Microsoft Hyper-V Server 2012 R2 mit Windows Admin Center:

1. Installieren von Windows Management Framework (WMF) Version 5.1 oder höher
2. Remoteverwaltung aktivieren
3. Aktivieren Sie die Datei-Serverrolle
4. Aktivieren Sie Hyper-V-Modul für PowerShell

### <a name="step-1-install-windows-management-framework-51"></a>**Schritt 1:** Installieren Sie Windows Management Framework 5.1

Windows Admin Center erfordert PowerShell-Features, die nicht in Microsoft Hyper-V Server 2012 R2 standardmäßig enthalten sind. Zum Verwalten von Microsoft Hyper-V Server 2012 R2 mit Windows Admin Center müssen Sie WMF Version 5.1 oder höher zu installieren.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist. 

Bei Bedarf können Sie [WMF 5.1 herunterladen](https://docs.microsoft.com/powershell/wmf/5.1/install-configure).

### <a name="step-2-enable-remote-management"></a>**Schritt 2:** Remoteverwaltung aktivieren 

So aktivieren Sie Hyper-V Server remote Management:

1. Melden Sie sich Hyper-V Server.
2. Geben Sie an des- **Server-Konfiguration** (SCONFIG), **4** zum Konfigurieren von remote-Verwaltung.
3. Geben Sie **1** ein, um die Remoteverwaltung aktivieren.
4. Geben Sie **4**, um zum Hauptmenü zurück.

### <a name="step-3-enable-file-server-role"></a>Schritt 3: Aktivieren Sie die Datei-Serverrolle

So aktivieren die Dateiserverrolle für einfache Datei Dateifreigabe und remote Management:

1. Klicken Sie im Menü **Extras** auf **Rollen und Funktionen** .
2. **Datei und Speicherdienste** suchen Sie im **Rollen und Features**, und überprüfen Sie **Datei und iSCSI-Services** und **Dateiserver**:

![](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-4-enable-hyper-v-module-for-powershell"></a>Schritt 4: Aktivieren Sie Hyper-V-Modul für PowerShell ##

So aktivieren Hyper-V-Modul für PowerShell-Features:

1. Klicken Sie im Menü **Extras** auf **Rollen und Funktionen** .
2. Finden Sie in **-Rollen und-Features**die **Remoteserver-Verwaltungstools**, und überprüfen Sie **Rollenverwaltungstools** und **Hyper-V-Modul für PowerShell**:

![](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2012 R2 ist jetzt für die Verwaltung mit Windows Admin Center bereit.

> [!Tip]
> Sind Sie bereit zum Installieren von Windows Admin Center? [Jetzt herunterladen](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center#download-now)