---
title: SCSI-Controller nur konfigurieren, wenn dies vom Gast Betriebssystem unterstützt wird
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
ms.date: 8/16/2016
ms.openlocfilehash: cadf4c0d0ce8cdd50d66a61f428b3e547dd457dc
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746995"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>SCSI-Controller nur konfigurieren, wenn dies vom Gast Betriebssystem unterstützt wird

>Gilt für: Windows Server 2016



|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein virtueller Computer wird mit einem SCSI-Controller konfiguriert, der nicht verwendet werden kann, da das Gast Betriebssystem SCSI-Controller nicht unterstützt.*

## <a name="impact"></a>Auswirkung

*Virtuelle Computer können keinen mit dem SCSI-Controller verbundenen Speicher verwenden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung

*Fahren Sie den virtuellen Computer herunter, und entfernen Sie den SCSI-Controller mit dem Hyper-V-Manager aus dem virtuellen Computer. Starten Sie dann den virtuellen Computer neu.*



