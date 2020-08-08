---
title: Alle für einen virtuellen Computer konfigurierten virtuellen Netzwerkadapter aktivieren
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7958bf5ced635c344ded45f8fde54bd7779ccbe9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960573"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>Alle für einen virtuellen Computer konfigurierten virtuellen Netzwerkadapter aktivieren

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein oder mehrere Netzwerkadapter sind möglicherweise auf einem virtuellen Computer deaktiviert.*

## <a name="impact"></a>Auswirkung

*Die folgenden virtuellen Computer verfügen möglicherweise nicht über eine Netzwerk Konnektivität:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Verwenden Sie Geräte-Manager im Gast Betriebssystem, um alle virtuellen Netzwerkadapter zu aktivieren. Wenn der Adapter nicht erforderlich ist, verwenden Sie den Hyper-V-Manager, um ihn vom virtuellen Computer zu entfernen.*



