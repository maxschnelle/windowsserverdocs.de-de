---
title: san
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d57c2df1-eb82-4b81-b8cd-e30564c6a929
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e020bc3327ccce5e80f4428078c87d1083c4a7df
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932819"
---
# <a name="san"></a>san

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Storage Area Network-Richtlinie (San) für das Betriebssystem an oder legt diese fest.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.

## <a name="syntax"></a>Syntax
```
san [policy={onlineAll | offlineAll | offlineShared}] [noerr]
```
#### <a name="parameters"></a>Parameter

|                          Parameter                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|--------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Policy = {onlineall &#124; offlineall &#124; offlineshared}] | Legt die San-Richtlinie für das aktuell gestartete Betriebssystem fest. Die San-Richtlinie legt fest, ob ein neu ermittelter Datenträger online geschaltet wird oder offline bleibt und ob er Lese-/Schreibzugriff oder schreibgeschützt ist. Wenn ein Datenträger offline ist, kann das Datenträger Layout gelesen werden, es werden jedoch keine Volumegeräte über Plug & Play angezeigt. Dies bedeutet, dass auf dem Datenträger kein Dateisystem bereitgestellt werden kann. Wenn ein Datenträger online ist, werden ein oder mehrere Volumegeräte für den Datenträger installiert. Im folgenden finden Sie eine Erläuterung zu den einzelnen Parametern:<p>-   **onlineall**. Gibt an, dass alle neu ermittelten Datenträger online geschaltet werden und Lese-/Schreibzugriff erfolgen. **Wichtig:**     Das Angeben von **onlineall** auf einem Server, der Datenträger freigibt, kann zu Daten Beschädigungen führen. Daher sollten Sie diese Richtlinie nicht festlegen, wenn Datenträger von Servern gemeinsam genutzt werden, es sei denn, der Server ist Teil eines Clusters.<br />-   **Offline**. Gibt an, dass alle neu ermittelten Datenträger mit Ausnahme des Start Datenträgers standardmäßig nur in der Standardeinstellung offline geschaltet werden.<br />-   **offlinesed**. Gibt an, dass alle neu ermittelten Datenträger, die sich nicht in einem freigegebenen Bus (z. b. SCSI und iSCSI) befinden, online geschaltet werden und Lese-/Schreibzugriff erhalten Datenträger, die offline bleiben, werden standardmäßig schreibgeschützt.<p>Weitere Informationen finden Sie unter [VDS_san_POLICY-Enumeration](https://go.microsoft.com/fwlink/?LinkId=203815) ( <https://go.microsoft.com/fwlink/?LinkId=203815> ). |
|                            Noerr                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

## <a name="remarks"></a>Hinweise
- Wenn der Befehl keine Parameter erhält, wird die aktuelle SAN-Richtlinie angezeigt.
  ## <a name="examples"></a>Beispiele
  Geben Sie Folgendes ein, um die aktuelle Richtlinie anzuzeigen:
  ```
  san
  ```
  Geben Sie Folgendes ein, um alle neu ermittelten Datenträger außer dem Start Datenträger standardmäßig offline und schreibgeschützt zu machen:
  ```
  san policy=offlineAll
  ```
  ## <a name="additional-references"></a>Weitere Verweise
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
