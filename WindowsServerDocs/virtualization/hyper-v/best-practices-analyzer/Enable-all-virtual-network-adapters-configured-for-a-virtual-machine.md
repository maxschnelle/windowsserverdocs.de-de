---
title: Alle für einen virtuellen Computer konfigurierten virtuellen Netzwerkadapter aktivieren
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
ms.date: 8/16/2016
ms.openlocfilehash: 81e0bbb8fce32b8343a13dea953498efb627d496
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746285"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>Alle für einen virtuellen Computer konfigurierten virtuellen Netzwerkadapter aktivieren

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein oder mehrere Netzwerkadapter sind möglicherweise auf einem virtuellen Computer deaktiviert.*

## <a name="impact"></a>Auswirkung

*Die folgenden virtuellen Computer verfügen möglicherweise nicht über eine Netzwerk Konnektivität:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Verwenden Sie Geräte-Manager im Gast Betriebssystem, um alle virtuellen Netzwerkadapter zu aktivieren. Wenn der Adapter nicht erforderlich ist, verwenden Sie den Hyper-V-Manager, um ihn vom virtuellen Computer zu entfernen.*



