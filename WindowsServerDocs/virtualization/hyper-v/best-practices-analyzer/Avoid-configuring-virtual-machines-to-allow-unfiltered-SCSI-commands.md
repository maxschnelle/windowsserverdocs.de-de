---
title: Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 33c211073c74da334abb8b483fa36974216a1185
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948583"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>Vermeiden Sie die Konfiguration virtueller Computer, um ungefilterte SCSI-Befehle zuzulassen

>Gilt für: Windows Server 2016



*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Operationen (Operations)|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein virtueller Computer ist so konfiguriert, dass er ungefilterte SCSI-Befehle zulässt.*

## <a name="impact"></a>Auswirkung

*Das umgehen der SCSI-Befehls Filterung stellt ein Sicherheitsrisiko dar. Diese Konfiguration sollte nur aktiviert werden, wenn Sie für die Kompatibilität mit Speicheranwendungen erforderlich ist, die im Gast Betriebssystem ausgeführt werden. Die folgenden virtuellen Computer sind so konfiguriert, dass Sie ungefilterte SCSI-Befehle zulassen:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Wenden Sie sich an Ihren Speicher Anbieter, um zu ermitteln, ob diese Konfiguration erforderlich ist. Wenn das Verwaltungs Betriebssystem oder andere Gast Betriebssysteme kompromittiert sind oder ungewöhnliche Verhalten aufweisen, konfigurieren Sie den virtuellen Computer neu, damit die Befehle blockiert werden.*



