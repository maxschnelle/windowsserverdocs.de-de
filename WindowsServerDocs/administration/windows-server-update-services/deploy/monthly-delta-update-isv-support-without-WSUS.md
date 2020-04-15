---
title: ISV-Unterstützung für monatliche Delta-Updates ohne WSUS
description: 'WSUS-Thema (Windows Server Update Service): Temporäre Verwendung monatlicher Delta-Updates für unabhängige Softwarehersteller (ISV) anstelle der WSUS-Express-Updatebereitstellung zum Reduzieren der Paketgröße'
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: 3ccddd3bfd55ae340dc5273905bb475e7d2cb98a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828743"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>ISV-Unterstützung für monatliche Delta-Updates ohne WSUS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

Windows 10-Updatedownloads können groß sein, da jedes Paket alle zuvor veröffentlichten Korrekturen enthält, um Konsistenz und Einfachheit sicherzustellen.  

Seit Version 7 kann Windows mithilfe des [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)-Features die Größe von Windows Update-Downloads reduzieren. Obwohl Verbrauchergeräte dieses Feature standardmäßig unterstützen, erfordern Windows 10 Enterprise-Geräte Windows Server Update Services (WSUS), um Express nutzen zu können. Wenn Sie über WSUS verfügen, finden Sie weitere Informationen unter [ISV-Unterstützung für die Express-Updatebereitstellung](express-update-delivery-ISV-support.md). Wir empfehlen die Verwendung zum Aktivieren der Express-Updatebereitstellung. 

Wenn WSUS derzeit nicht installiert ist, Sie vorläufig jedoch kleinere Updatepaketgrößen benötigen, können Sie ein monatliches Delta-Update verwenden. Durch das Delta-Update werden die Paketgrößen zwar erheblich reduziert, jedoch nicht so sehr wie bei der WSUS-Express-Updatebereitstellung. Es wird empfohlen, nach Möglichkeit ein WSUS-Express-Update bereitzustellen, um die Paketgrößen maximal zu verringern. Im folgenden Diagramm werden Downloadgrößen für Delta-Updates, kumulative Updates und Express-Updates für Windows 10 Version 1607 verglichen:

![Vergleich der Downloadgröße](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>Was ist ein monatliches Delta-Update?

Es gibt zwei Varianten des monatlichen Sicherheitsupdates: Delta-Updates und kumulative Updates.

Das monatliche Delta-Update ist neu und eine vorläufige Lösung für unabhängige Softwarehersteller, die nicht über WSUS verfügen, um die Paketgrößen zu verringern.

>[!IMPORTANT]
>**Das Delta-Update ist für die Wartung von Windows 10 Version 1607 (Anniversary Update), Version 1703 (Creators Update) und Version 1709 (Fall Creators Update) verfügbar.** Für Releases nach Version 1709 müssen Sie eine Bereitstellungsinfrastruktur implementieren, die die [Express-Updatebereitstellung](express-update-delivery-ISV-support.md) unterstützt, um weiterhin inkrementelle Updates nutzen zu können.

Bei Verwendung des monatlichen Delta-Updates enthalten Pakete nur die Updates eines Monats. Ein monatliches kumulatives Update enthält alle Updates bis zu diesem Update, was zu einer umfangreichen Datei führt, die jeden Monat vergrößert wird. Sowohl Delta als auch monatliche Updates werden am zweiten Dienstag eines jeden Monats veröffentlicht (auch bekannt als „Update-Dienstag“ bekannt). In der folgenden Tabelle werden Delta-Updates und kumulative Updates verglichen:

|                    | Monatliches **Delta**-Update                                                                                                                                                                                                       | Monatliches **kumulatives** Update                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scope**          | einzelnes Update **nur mit neuen Fehlerbehebungen für diesen Monat**                                                                                                                                                                           | einzelnes Update mit allen neuen Fehlerbehebungen für diesen und die vorherigen Monate                                                                                                                                                   |
| **Application**    | kann nur angewendet werden, wenn das Update des vorherigen Monats angewendet wurde (kumulatives Update oder Delta-Update)                                                                                                                                           | kann jederzeit angewendet werden                                                                                                                                                                                                |
| **Bereitstellung**       | **wird nur im Windows Update-Katalog veröffentlicht, wo es zur Verwendung mit anderen Tools oder Prozessen heruntergeladen werden kann;** wird nicht für PCs angeboten, die mit Windows Update verbunden sind                                                         | wird in Windows Update (wo es von allen Verbrauchercomputern installiert wird), WSUS und dem Windows Update-Katalog veröffentlicht                                                                                                                |

Delta-Updates und kumulative Updates verfügen über die gleiche KB-Nummer, die gleiche Klassifizierung und werden zur gleichen Zeit veröffentlicht Updates können entweder durch den Updatetitel im Katalog oder durch den Namen der MSU unterschieden werden:

- 02/2017 *\***Delta-Update**\**  für Windows 10 Version 1607 für x64-basierte Systeme (KB1234567)
- 02/2017 *\***Kumulatives Update**\**  für Windows 10 Version 1607 für x86-basierte Systeme (KB1234567)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>Verwendung des monatlichen Delta-Updates

Wenn die Größe eines Updates für das Clientgerät von Bedeutung ist, werden für Geräte, auf denen das Update des Vormonats installiert wurde, Delta-Updates und für Geräte, auf denen diese Updates nicht installiert wurden, kumulative Updates empfohlen. Auf diese Weise benötigen alle Geräte nur ein einzelnes Update, um sie auf den neuesten Stand zu bringen. Dies erfordert eine geringfügige Anpassung des gesamten Updateverwaltungsprozesses, da Sie basierend auf der Aktualität der Geräte in der Organisation unterschiedliche Updates bereitstellen müssen:

![Vergleich der Downloadgröße](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>Verhindern der Bereitstellung von Delta-Updates und kumulativen Updates im selben Monat

Da das Delta-Update und das kumulative Update gleichzeitig verfügbar sind, ist es wichtig zu verstehen, was geschieht, wenn Sie beide Updates im selben Monat bereitstellen.

Wenn Sie die gleiche Version des Delta-Updates und des kumulativen Updates genehmigen und bereitstellen, generieren Sie nicht nur zusätzlichen Netzwerkdatenverkehr, da beide auf den PC heruntergeladen werden, sondern Sie können Ihren Computer nach dem Neustart möglicherweise nicht mit Windows neu starten.

Wenn versehentlich Delta-Updates und kumulative Updates installiert sind und der Computer nicht mehr gestartet wird, können Sie diesen mit den folgenden Schritten wiederherstellen:

1. Starten Sie den Computer über die WinRE-Eingabeaufforderung.
2. Listen Sie die Pakete mit dem Status „Ausstehend“ auf:

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **Beispiel**: ` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. Öffnen Sie die Textdatei, in die Sie **get-packages** weitergeleitet haben. Führen Sie **remove-package** für jeden Paketnamen aus, wenn für die Installation ausstehende Patches angezeigt werden:
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **Beispiel**: `x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >Entfernen Sie keine für die Deinstallation ausstehenden Patches.

>[!IMPORTANT]
>**Das Delta-Update ist für die Wartung von Windows 10 Version 1607 (Anniversary Update), Version 1703 (Creators Update) und Version 1709 (Fall Creators Update) verfügbar.** Für Releases nach Version 1709 müssen Sie eine Bereitstellungsinfrastruktur implementieren, die die [Express-Updatebereitstellung](express-update-delivery-ISV-support.md) unterstützt, um weiterhin inkrementelle Updates nutzen zu können.
