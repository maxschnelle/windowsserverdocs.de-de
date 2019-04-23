---
title: Monatliche Delta aktualisieren, ohne WSUS ISV-Unterstützung
description: Windows Server Update Service (WSUS)-Thema – wie Hersteller ISVS (Independent Software) können vorübergehend monatliche Delta-Update statt WSUS Express Update Übermittlung Sie Größe des Pakets reduzieren
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: c89d5eb754685fb8000ac2025af391057e77654c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848611"
---
#<a name="monthly-delta-update-isv-support-without-wsus"></a>Monatliche Delta aktualisieren, ohne WSUS ISV-Unterstützung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

Windows 10-Update-Downloads können groß sein, da jedes Paket auf alle zuvor veröffentlichten Updates, um sicherzustellen, dass Konsistenz und Einfachheit enthält.  

Version 7, Windows seit verringern, die Größe des Windows Update-Downloads durch eine Funktion namens [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2), und obwohl Geräte für Verbraucher standardmäßig unterstützt, wird Windows 10 Enterprise-Geräte erfordern Windows Server Update Services (WSUS) Express nutzen. Wenn Sie WSUS zur Verfügung haben, finden Sie unter [aktualisierungsunterstützung für Übermittlung ISVS Express](express-update-delivery-ISV-support.md). Es wird empfohlen, verwenden, um die Übermittlung von Express-Update zu aktivieren. 

Wenn Sie derzeit keine WSUS installiert, aber Sie Paketgrößen kleinere, in der Zwischenzeit aktualisieren müssen, können Sie die monatlichen Delta-Update. Delta-Update wird Paketgrößen im Wesentlichen, aber nicht so viel wie WSUS Express Update Übermittlung verringert. Es wird empfohlen, dass Sie die WSUS-Express-Update, wann immer möglich, dass die größte Verringerung des Paketgrößen bereitstellen. Es folgt ein Diagramm, das Delta, kumulativ und Express-Download-Größen für Windows 10, Version 1607 vergleichen:

![Größenvergleich herunterladen](../../media/express-update-delivery-isv-support/delta-1.png)

##<a name="what-is-monthly-delta-update"></a>Was ist monatlich Delta-Update?

Es gibt zwei Varianten der monatlichen Sicherheitsupdates: Delta und dem kumulativen.

Monatliche Delta-Update ist neu, und ein vorläufige Lösung für die unabhängige Softwarehersteller, die keine WSUS verfügbar, um zu reduzieren, die Größe des Pakets zu aktualisieren.

>[!IMPORTANT]
>**Delta-Update ist verfügbar für die Wartung von Windows 10, Version 1607 (Anniversary Update), Version 1703 (Creators Update) und Version 1709 (Fall Creators Update).** Für Versionen nach Version 1709, Sie benötigen eine Bereitstellungsinfrastruktur zu implementieren, unterstützt [Express Update Delivery](express-update-delivery-ISV-support.md) um den Vorgang fortzusetzen, inkrementelle Updates zu nutzen.

Mit monatlicher Delta-Update, nur enthalten einen Monat Pakete. Monatlichen kumulativen enthält alle Updates bis zu diesem Update-Version, was zu einer großen Datei, die jeden Monat wächst. Sowohl Delta und monatliche Updates werden jeweils am zweiten Dienstag eines jeden Monats, auch bekannt als "Update Tuesday." veröffentlicht. Die folgende Tabelle vergleicht das Delta und kumulativen Updates:

|                    | Monatliche **Delta** aktualisieren                                                                                                                                                                                                       | Monatliche **kumulativen** aktualisieren                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Bereich**          | Einzelnes Update mit **nur neuen Fixes für diesen Monat**                                                                                                                                                                           | Einzelnes Update alle neuen Fixes für diesen Monat und alle vorherigen Monaten                                                                                                                                                   |
| **Application**    | Kann nur angewendet werden, war das Update des Vormonats angewendet (kumulativen oder Delta)                                                                                                                                           | Kann jederzeit angewendet werden                                                                                                                                                                                                |
| **Übermittlung**       | **Nur für Windows Update-Katalog veröffentlicht** , in dem für die Verwendung mit anderen Tools oder Prozessen heruntergeladen werden kann. Auf PCs, die mit Windows Update verbunden sind, nicht angeboten.                                                         | In Windows Update (, in dem alle Consumer PCs installiert werden), WSUS und dem Windows Update-Katalog veröffentlicht                                                                                                                |

Delta und dem kumulativen haben die gleichen KB-Nummer, mit der gleichen Klassifizierung, und gleichzeitig freizugeben. Updates können entweder mit dem Titel des Updates im Katalog oder durch die MSU-Datei den Namen unterschieden werden:

- 2017-02 *\***Delta-Update**\** für Windows 10 Version 1607 für X64-basierte Systeme (KB1234567)
- 2017-02 *\***Kumulatives Update**\** für Windows 10 Version 1607 X86-basierten Systemen (KB1234567)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>Verwendung des monatlichen Delta-Update

Wenn das Update an den Client relevant ist, wird empfohlen, mithilfe von Delta-Update auf den Geräten, die des vorhergehenden Monats aktualisieren, und auf den Geräten zu aktualisieren, die im Rückstand sind kumulativ. Auf diese Weise alle Geräte erfordern nur ein einzelnes Update aus, um sie auf dem neuesten Stand zu bringen. Dies erfordert eine geringfügige Anpassung in der gesamten Update Management-Vorgang, wie Sie zum Bereitstellen von anderen Updates, die basierend auf die Geräte in der Organisation wie auf dem neuesten Stand sind ist:

![Größenvergleich herunterladen](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>Verhindern der Bereitstellung von Delta- und kumulativen Updates im selben Monat

Da die Delta-Update und das kumulative Update zur gleichen Zeit verfügbar sind, es ist wichtig zu verstehen, was geschieht, wenn Sie beide Updates im selben Monat bereitstellen.

Wenn Sie genehmigt und die gleiche Version des Deltas und die kumulativen Updates bereitstellen, nicht nur generieren Sie zusätzlichen Netzwerkdatenverkehr da beide werden in den PC heruntergeladen, aber Sie möglicherweise nicht in der Lage, Ihre Computer auf Windows nach dem Neustart neu zu starten.

Wenn sowohl Delta und kumulativen Updates versehentlich installiert sind, und Ihrem Computer nicht mehr gestartet werden wird, können Sie mit den folgenden Schritten wiederherstellen:

1. Starten Sie in WinRE-Eingabeaufforderung
2. Listen Sie die Pakete im Status "Ausstehend" auf:

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **Beispiel**: ` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. Öffnen Sie die Textdatei, in dem Sie über die Pipeline **Get-Packages**. Wenn Sie Installation steht an Patches angezeigt wird, führen Sie **Remove-Package** für jedes Paketname:
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **Beispiel**: `x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >Entfernen Sie nicht ausstehende Patches deinstallieren.

>[!IMPORTANT]
>**Delta-Update ist verfügbar für die Wartung von Windows 10, Version 1607 (Anniversary Update), Version 1703 (Creators Update) und Version 1709 (Fall Creators Update).** Für Versionen nach Version 1709, Sie benötigen eine Bereitstellungsinfrastruktur zu implementieren, unterstützt [Express Update Delivery](express-update-delivery-ISV-support.md) um den Vorgang fortzusetzen, inkrementelle Updates zu nutzen.
