---
title: SAN
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d57c2df1-eb82-4b81-b8cd-e30564c6a929
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90b6cec9e44ae91b21932c1e4c46a33e0b5da5e4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441672"
---
# <a name="san"></a>SAN

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt an, oder legt die Richtlinie zur Storage Area Network (San) für das Betriebssystem.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.

## <a name="syntax"></a>Syntax
```
san [policy={onlineAll | offlineAll | offlineShared}] [noerr]
```
### <a name="parameters"></a>Parameter

|                          Parameter                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|--------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| policy={ onlineAll &#124; offlineAll &#124; offlineShared }] | Legt fest, die San-Richtlinie für das Betriebssystem zurzeit gestartet. Die San-Richtlinie bestimmt, ob ein neu ermittelte Datenträger online geschaltet wird, oder bleibt offline, und gibt an, ob wird Lese-/Schreibzugriff oder schreibgeschützt bleibt. Wenn ein Datenträger offline ist, das Datenträgerlayout gelesen werden kann, aber keine Volumegeräte werden über Plug & Play aufgeführt. Dies bedeutet, dass kein Dateisystem auf dem Datenträger bereitgestellt werden kann. Wenn ein Datenträger online ist, werden ein oder mehrere Volumegeräte für den Datenträger installiert. Im folgenden finden eine Erläuterung der einzelnen Parameter:<br /><br />-   **onlineAll**. Gibt an, dass alle neu ermittelt, dass die Datenträger online und wurden Lese-/Schreibzugriff eingerichtet werden sollen. **WICHTIG:**     Angeben von **OnlineAll** auf einem Server, die gemeinsam von Datenträgern kann zur Beschädigung von Daten führen. Aus diesem Grund sollten Sie diese Richtlinie nicht festgelegt, wenn der Datenträger von Servern gemeinsam genutzt werden, es sei denn, der Server Teil eines Clusters ist.<br />-   **offlineAll**. Gibt an, dass alle Datenträger mit der Ausnahme beim Startdatenträger offline kann neu ermittelte Andread nur in der Standardeinstellung.<br />-   **offlineShared**. Gibt an, dass alle neu ermittelt, dass die Datenträger, die nicht auf einem freigegebenen Bus (z. B. SCSI und iSCSI) befinden, online geschaltet werden, und Lese-und Schreibzugriff versehen. Datenträger, die offline bleiben werden standardmäßig schreibgeschützt.<br /><br />Weitere Informationen finden Sie unter [VDS_san_POLICY Enumeration](https://go.microsoft.com/fwlink/?LinkId=203815) (<https://go.microsoft.com/fwlink/?LinkId=203815>). |
|                            Diskpart                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Nur für Skripting verwendet. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

## <a name="remarks"></a>Hinweise
- Wenn der Befehl ohne Parameter angegeben ist, wird die aktuelle San-Richtlinie angezeigt.
  ## <a name="BKMK_Examples"></a>Beispiele für
  Wenn die aktuelle Richtlinie anzeigen möchten, geben Sie Folgendes ein:
  ```
  san
  ```
  Damit alle neu ermittelte Datenträger mit Ausnahme der startddatenträger, offline und standardmäßig schreibgeschützt, geben Sie Folgendes ein:
  ```
  san policy=offlineAll
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
