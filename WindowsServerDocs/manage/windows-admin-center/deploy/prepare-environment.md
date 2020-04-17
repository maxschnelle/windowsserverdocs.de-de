---
title: Vorbereiten der Umgebung für Windows Admin Center
description: Vorbereiten der Umgebung für Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 7a4dacd611741942e874e831fd9598aeda5e97b3
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269277"
---
# <a name="prepare-your-environment-for-windows-admin-center"></a>Vorbereiten der Umgebung für Windows Admin Center

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Es gibt einige Serverversionen, die zusätzliche Vorbereitung benötigen, bevor sie mit Windows Admin Center verwaltet werden können:

- [Windows Server 2012 und 2012 R2](#prepare-windows-server-2012-and-2012-r2)
- [Microsoft Hyper-V Server 2016](#prepare-microsoft-hyper-v-server-2016)
- [Microsoft Hyper-V Server 2012 R2](#prepare-microsoft-hyper-v-server-2012-r2)

Es gibt auch einige Szenarien, in denen die [Portkonfiguration auf dem Zielserver](#port-configuration-on-the-target-server) möglicherweise vor der Verwaltung mit Windows Admin Center geändert werden muss.

## <a name="prepare-windows-server-2012-and-2012-r2"></a>Vorbereiten von Windows Server 2012 und 2012 R2

### <a name="install-wmf-version-51-or-higher"></a>Installieren von WMF Version 5.1 oder höher

Windows Admin Center erfordert PowerShell-Features, die nicht standardmäßig in Windows Server 2012 und 2012 R2 enthalten sind. Zum Verwalten von Windows Server 2012 oder 2012 R2 mit Windows Admin Center musst du WMF Version 5.1 oder höher auf diesen Servern installieren.

Gebe `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder höher installiert ist.

Wenn dies nicht der Fall ist, kannst du [herunterladen und WMF 5.1 installieren](https://docs.microsoft.com/powershell/wmf/setup/install-configure).

## <a name="prepare-microsoft-hyper-v-server-2016"></a>Vorbereiten von Microsoft Hyper-V Server 2016

Zum Verwalten von Microsoft Hyper-V Server 2016 mit Windows Admin Center musst du zuvor einige erforderliche Serverrollen aktivieren.

### <a name="to-manage-microsoft-hyper-v-server-2016-with-windows-admin-center"></a>So verwaltest du Microsoft Hyper-V Server 2016 mit Windows Admin Center

1. Aktiviere die Remoteverwaltung.
2. Aktiviere die Dateiserverrolle.
3. Aktiviere das Hyper-V-Modul für PowerShell.

### <a name="step-1-enable-remote-management"></a>**Schritt 1:** Aktivieren der Remoteverwaltung

So aktivierst du die Remoteverwaltung in Hyper-V Server

1. Melde dich bei Hyper-V Server an.
2. Gebe beim Tool **Serverkonfiguration** (SCONFIG) den Wert **4** ein, um die Remoteverwaltung zu konfigurieren.
3. Gebe **1** ein, um die Remoteverwaltung zu aktivieren.
4. Gebe **4** ein, um zum Hauptmenü zurückzukehren.

### <a name="step-2-enable-file-server-role"></a>**Schritt 2:** Aktivieren der Dateiserverrolle

So aktivierst du die Dateiserverrolle für die grundlegende Dateifreigabe und Remoteverwaltung

1. Klicke in **Rollen und Funktionen** auf das Menü **Extras**.
2. Suche in **Rollen und Funktionen** nach **Datei- und Speicherdienste** und aktiviere **Datei- und iSCSI-Dienste** sowie **Dateiserver**:

![Screenshot „Rollen und Funktionen“ mit ausgewählter Rolle „Datei- und iSCSI-Dienste“](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-3-enable-hyper-v-module-for-powershell"></a>**Schritt 3:** Aktivieren des Hyper-V-Moduls für PowerShell

So aktivierst du das Hyper-V-Modul für PowerShell-Features

1. Klicke in **Rollen und Funktionen** auf das Menü **Extras**.
2. Suche in **Rollen und Funktionen** nach **Remoteserver-Verwaltungstools** und aktiviere **Rollenverwaltungstools** und **Hyper-V-Modul für PowerShell**:

![Screenshot „Rollen und Funktionen“ mit aktivierten Hyper-V-Rollen](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2016 ist jetzt für die Verwaltung mit Windows Admin Center bereit.

## <a name="prepare-microsoft-hyper-v-server-2012-r2"></a>Vorbereiten von Microsoft Hyper-V Server 2012 R2

Zum Verwalten von Microsoft Hyper-V Server 2012 R2 mit Windows Admin Center musst du zuvor einige Serverrollen aktivieren.  Darüber hinaus musst du WMF Version 5.1 oder höher installieren.

### <a name="to-manage-microsoft-hyper-v-server-2012-r2-with-windows-admin-center"></a>So verwaltest du Microsoft Hyper-V Server 2012 R2 mit Windows Admin Center

1. Installieren von Windows Management Framework (WMF) Version 5.1 oder höher
2. Aktivieren der Remoteverwaltung
3. Aktivieren der Dateiserverrolle
4. Aktivieren des Hyper-V-Moduls für PowerShell

### <a name="step-1-install-windows-management-framework-51"></a>Schritt 1: Installieren von Windows Management Framework 5.1

Windows Admin Center erfordert PowerShell-Features, die in Microsoft Hyper-V Server 2012 R2 nicht standardmäßig enthalten sind. Zum Verwalten von Microsoft Hyper-V Server 2012 R2 mit Windows Admin Center musst du WMF Version 5.1 oder höher installieren.

Gebe `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder höher installiert ist. 

Wenn es nicht installiert ist, kannst du [WMF 5.1](https://docs.microsoft.com/powershell/wmf/setup/install-configure) herunterladen.

### <a name="step-2-enable-remote-management"></a>Schritt 2: Aktivieren der Remoteverwaltung

So aktivierst du die Hyper-V Server-Remoteverwaltung

1. Melde dich bei Hyper-V Server an.
2. Gebe beim Tool **Serverkonfiguration** (SCONFIG) den Wert **4** ein, um die Remoteverwaltung zu konfigurieren.
3. Gebe **1** ein, um die Remoteverwaltung zu aktivieren.
4. Gebe **4** ein, um zum Hauptmenü zurückzukehren.

### <a name="step-3-enable-file-server-role"></a>Schritt 3: Aktivieren der Dateiserverrolle

So aktivierst du die Dateiserverrolle für die grundlegende Dateifreigabe und Remoteverwaltung

1. Klicke in **Rollen und Funktionen** auf das Menü **Extras**.
2. Suche in **Rollen und Funktionen** nach **Datei- und Speicherdienste** und aktiviere **Datei- und iSCSI-Dienste** sowie **Dateiserver**:

![Screenshot „Rollen und Funktionen“ mit ausgewählter Rolle „Datei- und iSCSI-Dienste“](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-4-enable-hyper-v-module-for-powershell"></a>Schritt 4: Aktivieren des Hyper-V-Moduls für PowerShell

So aktivierst du das Hyper-V-Modul für PowerShell-Features

1. Klicke in **Rollen und Funktionen** auf das Menü **Extras**.
2. Suche in **Rollen und Funktionen** nach **Remoteserver-Verwaltungstools** und aktiviere **Rollenverwaltungstools** und **Hyper-V-Modul für PowerShell**:

![Screenshot „Rollen und Funktionen“ mit aktivierten Hyper-V-Remoteserver-Verwaltungstools](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2012 R2 ist jetzt für die Verwaltung mit Windows Admin Center bereit.

## <a name="port-configuration-on-the-target-server"></a>Portkonfiguration auf dem Zielserver

Windows Admin Center verwendet das SMB-Dateifreigabeprotokoll für einige Dateikopieraufgaben, z. B. beim Importieren eines Zertifikats auf einem Remoteserver. Damit diese Dateikopiervorgänge erfolgreich sind, muss die Firewall auf dem Remoteserver eingehende Verbindungen an Port 445 zulassen.  Du kannst das Firewalltool in Windows Admin Center verwenden, um zu überprüfen, ob die Eingangsregel für „Dateiserver-Remoteverwaltung (SMB-In)“ so eingestellt ist, dass der Zugriff auf diesen Port zulässig ist.

> [!Tip]
> Bist du für die Installation von Windows Admin Center bereit? [Jetzt herunterladen](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center#download-now)
