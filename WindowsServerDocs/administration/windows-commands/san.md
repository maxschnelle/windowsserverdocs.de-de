---
title: san
description: Referenz Artikel für den San-Befehl, der die Storage Area Network-Richtlinie (San) für das Betriebssystem anzeigt oder festlegt.
ms.topic: reference
ms.assetid: d57c2df1-eb82-4b81-b8cd-e30564c6a929
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8881855e77f8df579cb054954d26296edf4c971f
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388369"
---
# <a name="san"></a>san

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Storage Area Network-Richtlinie (San) für das Betriebssystem an oder legt diese fest. Bei Verwendung ohne Parameter wird die aktuelle SAN-Richtlinie angezeigt.

## <a name="syntax"></a>Syntax

```
san [policy={onlineAll | offlineAll | offlineShared}] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Policy = {onlineall|offlineall|offlineshared}] | Legt die San-Richtlinie für das aktuell gestartete Betriebssystem fest. Die San-Richtlinie legt fest, ob ein neu ermittelter Datenträger online geschaltet wird oder offline bleibt und ob er Lese-/Schreibzugriff oder schreibgeschützt ist. Wenn ein Datenträger offline ist, kann das Datenträger Layout gelesen werden, es werden jedoch keine Volumegeräte über Plug & Play angezeigt. Dies bedeutet, dass auf dem Datenträger kein Dateisystem bereitgestellt werden kann. Wenn ein Datenträger online ist, werden ein oder mehrere Volumegeräte für den Datenträger installiert. Im folgenden finden Sie eine Erläuterung zu den einzelnen Parametern:<ul><li>**onlineall**. Gibt an, dass alle neu ermittelten Datenträger online geschaltet werden und Lese-/Schreibzugriff erfolgen. **Wichtig:** Das Angeben von **onlineall** auf einem Server, der Datenträger freigibt, kann zu Daten Beschädigungen führen. Daher sollten Sie diese Richtlinie nicht festlegen, wenn Datenträger von Servern gemeinsam genutzt werden, es sei denn, der Server ist Teil eines Clusters.</li><li>**Offline**. Gibt an, dass alle neu ermittelten Datenträger mit Ausnahme des Start Datenträgers standardmäßig offline und schreibgeschützt sind.</li><li>**offlinesed**. Gibt an, dass alle neu ermittelten Datenträger, die sich nicht in einem freigegebenen Bus (z. b. SCSI und iSCSI) befinden, online geschaltet werden und Lese-/Schreibzugriff erhalten Datenträger, die offline bleiben, werden standardmäßig schreibgeschützt.</li></ul>Weitere Informationen finden Sie unter [VDS_san_POLICY-Enumeration](https://docs.microsoft.com/windows/win32/api/vds/ne-vds-vds_san_policy?redirectedfrom=MSDN). |
| Noerr | Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle Richtlinie anzuzeigen:

```
san
```

Geben Sie Folgendes ein, um alle neu ermittelten Datenträger außer dem Start Datenträger standardmäßig offline und schreibgeschützt zu machen:

```
san policy=offlineAll
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
