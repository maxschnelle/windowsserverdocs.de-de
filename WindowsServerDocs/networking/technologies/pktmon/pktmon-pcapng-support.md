---
title: Pktmon-Unterstützung für wireshark (pcapng)
description: Verwenden Sie dieses Thema, um die vom Paket Monitor generierten pcapng-Protokolle mit Wireshark zu analysieren.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: c65604f6e3f4e87b806513063800ee62d52d1feb
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632507"
---
# <a name="pktmon-support-for-wireshark-pcapng"></a>Pktmon-Unterstützung für wireshark (pcapng)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows 10, Azure Stack HCI, Azure Stack Hub, Azure

Der Paket Monitor (pktmon) kann Protokolle in das pcapng-Format konvertieren. Diese Protokolle können mithilfe von Wireshark (oder einem beliebigen pcapng Analyzer) analysiert werden. einige wichtige Informationen können jedoch in den pcapng-Dateien fehlen. In diesem Thema wird die erwartete Ausgabe erläutert und erläutert, wie Sie Sie nutzen können.

## <a name="pktmon-pcapng-syntax"></a>Pktmon-pcapng-Syntax

Verwenden Sie die folgenden Befehle, um die pktmon-Erfassung in das pcapng-Format zu konvertieren.

```powershell
C:\Test> pktmon pcapng help
pktmon pcapng log.etl [-o log.pcapng]
    Convert log file to pcapng format.
    Dropped packets are not included by default.

-o, --out
    Name of the formatted pcapng file.

-d, --drop-only
    Convert dropped packets only.

-c, --component-id
    Filter packets by a specific component ID.

Example: pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

## <a name="output-filtering"></a>Ausgabe Filterung

Alle Informationen zu den Paket Lösch Berichten und der Paketfluss über den Netzwerk Stapel gehen in der Ausgabe des pcapng verloren. Daher sollte der Protokoll Inhalt für eine solche Konvertierung sorgfältig vorgefiltert werden. Zum Beispiel:

- Das pcapng-Format unterscheidet nicht zwischen einem fließenden Paket und einem gelöschten Paket. Wenn Sie alle Pakete in der Erfassung von gelöschten Paketen trennen möchten, generieren Sie zwei pcapng-Dateien. eine, die alle Pakete (" **pktmon pcapng Log. ETL-out Log-Capture. ETL** ") enthält, und eine weitere, die nur gelöschte Pakete enthält (" **pktmon pcapng Log. ETL--Drop-only-out Log-Drop. ETL** "). Auf diese Weise können Sie die gelöschten Pakete in einem separaten Protokoll analysieren.
- Das pcapng-Format unterscheidet nicht zwischen verschiedenen Netzwerkkomponenten, bei denen ein Paket aufgezeichnet wurde. Geben Sie für solche mehrschichtigen Szenarien die gewünschte Komponenten-ID in der pcapng-Ausgabe " **pktmon pcapng Log. ETL--Component-ID 5** " an. Wiederholen Sie diesen Befehl für jeden Satz von Komponenten-IDs, an denen Sie interessiert sind.
