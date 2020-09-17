---
title: Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
ms.date: 8/16/2016
ms.openlocfilehash: 95d7fa223371aa3dbc3b66efcfefed217eed5216
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747085"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen

>Gilt für: Windows Server 2016



*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein virtueller Computer ist so konfiguriert, dass er ungefilterte SCSI-Befehle zulässt.*

## <a name="impact"></a>Auswirkung

*Das umgehen der SCSI-Befehls Filterung stellt ein Sicherheitsrisiko dar. Diese Konfiguration sollte nur aktiviert werden, wenn Sie für die Kompatibilität mit Speicheranwendungen erforderlich ist, die im Gast Betriebssystem ausgeführt werden. Die folgenden virtuellen Computer sind so konfiguriert, dass Sie ungefilterte SCSI-Befehle zulassen:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Wenden Sie sich an Ihren Speicher Anbieter, um zu ermitteln, ob diese Konfiguration erforderlich ist. Wenn das Verwaltungs Betriebssystem oder andere Gast Betriebssysteme kompromittiert sind oder ungewöhnliche Verhalten aufweisen, konfigurieren Sie den virtuellen Computer neu, damit die Befehle blockiert werden.*



