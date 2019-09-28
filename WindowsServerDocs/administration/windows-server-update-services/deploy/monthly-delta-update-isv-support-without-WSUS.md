---
title: Monatliche Delta Update-ISV-Unterstützung ohne WSUS
description: 'Windows Server Update Service (WSUS)-Thema: wie unabhängige Software Hersteller (ISV) temporär ein monatliches Delta Update anstelle der WSUS Express-Update Bereitstellung verwenden können, um die Paketgröße zu verringern.'
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: 4607827d73c34f50f721a2774fa498eb95f9dbb8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361728"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>Monatliche Delta Update-ISV-Unterstützung ohne WSUS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

Downloads für Windows 10-Updates können sehr umfangreich sein, da jedes Paket alle zuvor veröffentlichten Korrekturen enthält, um die Konsistenz und Einfachheit sicherzustellen.  

Seit Version 7 konnte Windows die Größe der Windows Update Downloads mit einer Funktion namens " [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)" reduzieren, und auch wenn consumergeräte diese standardmäßig unterstützen, erfordern Windows 10 Enterprise-Geräte Windows Server Update Services (WSUS). Vorteil von Express. Wenn Sie über WSUS verfügen, finden Sie weitere Informationen [unter Unterstützung für die Express-Update Bereitstellung](express-update-delivery-ISV-support.md). Wir empfehlen die Verwendung, um die Express-Update Übermittlung zu aktivieren. 

Wenn WSUS derzeit nicht installiert ist, Sie jedoch kleinere Update Paketgrößen benötigen, können Sie ein monatliches Delta Update verwenden. Durch das Delta Update werden die Paketgrößen erheblich reduziert, aber nicht so viel wie bei der WSUS Express-Update Bereitstellung. Es wird empfohlen, dass Sie nach Möglichkeit ein WSUS Express-Update bereitstellen, um die größte Verringerung der Paketgrößen zu erzielen. Im folgenden Diagramm werden Delta-, kumulative und Express-Downloadgrößen für Windows 10, Version 1607, verglichen:

![Vergleich der Download Größe](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>Was ist eine monatliche Delta Aktualisierung?

Es gibt zwei Varianten des monatlichen Sicherheitsupdates: Delta und kumulativ.

Das monatliche Delta Update ist neu, und eine vorläufige Lösung für ISVs, die keine WSUS zur Verringerung der Größe der Update Pakete zur Verfügung haben.

>[!IMPORTANT]
>**Delta Update ist für die Wartung von Windows 10, Version 1607 (Anniversary Update), Version 1703 (Creators Update) und Version 1709 (Fall Creators Update) verfügbar.** Für Releases nach Version 1709 müssen Sie eine Bereitstellungs Infrastruktur implementieren, die die [Express-Update Bereitstellung](express-update-delivery-ISV-support.md) unterstützt, um weiterhin inkrementelle Updates nutzen zu können.

Bei Verwendung des monatlichen Delta Updates enthalten Pakete nur die Updates eines Monats. Monatlicher kumulativer Wert enthält alle Updates bis zu diesem Update Release, was zu einer umfangreichen Datei führt, die jeden Monat vergrößert. Sowohl Delta-als auch monatliche Updates werden am zweiten Dienstag eines jeden Monats, auch bekannt als "Update Dienstag", veröffentlicht. In der folgenden Tabelle werden Delta-und kumulative Updates verglichen:

|                    | Monatliches **Delta** Update                                                                                                                                                                                                       | Monatliches **Kumulatives** Update                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Bereich**          | Einzelnes Update mit **nur neuen Korrekturen für diesen Monat**                                                                                                                                                                           | Einzelnes Update mit allen neuen Korrekturen für diesen Monat und alle vorangegangenen Monate                                                                                                                                                   |
| **Application**    | Kann nur angewendet werden, wenn die Aktualisierung des vorherigen Monats angewendet wurde (kumulativ oder Delta).                                                                                                                                           | Kann jederzeit angewendet werden                                                                                                                                                                                                |
| **Liefer**       | Wird **nur in Windows Update Katalog veröffentlicht,** wo Sie für die Verwendung mit anderen Tools oder Prozessen heruntergeladen werden kann. Nicht für PCs angeboten, die mit Windows Update verbunden sind                                                         | Veröffentlicht in Windows Update (wo alle Consumer-PCs installiert werden), WSUS und der Windows Update-Katalog                                                                                                                |

Delta und kumulativ verfügen über die gleiche KB-Nummer, mit derselben Klassifizierung und der Freigabe gleichzeitig. Updates können entweder durch den Update Titel im Katalog oder durch den Namen der MSU unterschieden werden:

- 2017-02 *\***Delta**Update\** für Windows 10, Version 1607 für x64-Systeme (KB1234567)
- 2017-02 *\***Kumulatives**Update\** für Windows 10, Version 1607 für x86-basierte Systeme (KB1234567)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>Verwendungszwecke des monatlichen Delta Updates

Wenn die Größe des Updates für das Client Gerät von Bedeutung ist, empfehlen wir die Verwendung eines Delta Updates auf den Geräten, auf denen das Update im vorherigen Monat vorhanden ist, und das kumulative Update auf den Geräten, die ausfallen. Auf diese Weise benötigen alle Geräte nur ein einzelnes Update, um Sie auf den neuesten Stand zu bringen. Dies erfordert eine geringfügige Anpassung des gesamten Update Verwaltungsprozesses, da Sie unterschiedliche Updates auf der Grundlage der aktuellen Geräte in der Organisation bereitstellen müssen:

![Vergleich der Download Größe](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>Verhindern der Bereitstellung von Delta-und kumulativen Updates im selben Monat

Da Delta Update und Kumulatives Update gleichzeitig verfügbar sind, ist es wichtig zu verstehen, was geschieht, wenn Sie beide Updates im selben Monat bereitstellen.

Wenn Sie die gleiche Version des Deltas und des kumulativen Updates genehmigen und bereitstellen, generieren Sie nicht nur zusätzlichen Netzwerk Datenverkehr, da beide auf den PC heruntergeladen werden, Sie können den Computer nach dem Neustart jedoch möglicherweise nicht mit Windows neu starten.

Wenn Delta-und kumulative Updates versehentlich installiert sind und der Computer nicht mehr gestartet wird, können Sie mit den folgenden Schritten wiederherstellen:

1. Starten in WinRE-Eingabeaufforderung
2. Auflisten der Pakete im Zustand "Ausstehend":

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **Beispiel**:` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. Öffnen Sie die Textdatei, in der Sie **Get-Packages**weitergeleitet haben. Wenn Sie ausstehende Patches für die Installation sehen, führen Sie für jeden Paketnamen " **Remove-Package** " aus:
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **Beispiel**:`x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >Entfernen Sie ausstehende Patches deinstallieren nicht.

>[!IMPORTANT]
>**Delta Update ist für die Wartung von Windows 10, Version 1607 (Anniversary Update), Version 1703 (Creators Update) und Version 1709 (Fall Creators Update) verfügbar.** Für Releases nach Version 1709 müssen Sie eine Bereitstellungs Infrastruktur implementieren, die die [Express-Update Bereitstellung](express-update-delivery-ISV-support.md) unterstützt, um weiterhin inkrementelle Updates nutzen zu können.
