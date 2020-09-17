---
title: Konfigurieren Sie einen virtuellen Computer mit einem SCSI-Controller, um das Plug-in und den Hot-trennen Sie-Speicher zu integrieren.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
ms.date: 8/16/2016
ms.openlocfilehash: 9f0cdb47206c89c4da66786e8dfd118e6a05be81
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746975"
---
# <a name="configure-a-virtual-machine-with-a-scsi-controller-to-be-able-to-hot-plug-and-hot-unplug-storage"></a>Konfigurieren Sie einen virtuellen Computer mit einem SCSI-Controller, um das Plug-in und den Hot-trennen Sie-Speicher zu integrieren.

>Gilt für: Windows Server 2016



*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein virtueller Computer wurde gefunden, der nicht mit einem SCSI-Controller konfiguriert ist.*

## <a name="impact"></a>Auswirkung

*Sie sind nicht in der Lage, den trennen Sie-in-Plug-in-Speicher für die folgenden virtuellen Computer zu schließen:*

\<list of virtual machine names>

Durch die Fähigkeit, ein Hot-Plug-in oder Hot-trennen Sie-Speicher zu ermöglichen, ist es einfacher, die Speicheranforderungen eines virtuellen Computers ohne Ausfallzeiten zu verwalten Virtuelle Computer ohne SCSI-Controller müssen heruntergefahren werden, bevor Sie Speicher hinzufügen oder entfernen können.

## <a name="resolution"></a>Lösung

*Wenn Sie keine Hot-Plug-oder Hot-trennen Sie-Speicher für diesen virtuellen Computer benötigen, ist keine Aktion erforderlich. Fahren Sie andernfalls den virtuellen Computer herunter, und fügen Sie der Konfiguration einen SCSI-Controller hinzu.*

Um einen SCSI-Controller für das Hot-Plug-in und den Hot-trennen Sie-Speicher zu verwenden, muss auf dem Gast Betriebssystem die aktuelle Version von Integration Services ausgeführt werden.



