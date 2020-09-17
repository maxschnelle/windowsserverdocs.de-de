---
title: Anzeige Adapter sollten auf virtuellen Computern aktiviert werden, um Videofunktionen bereitzustellen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
ms.date: 8/16/2016
ms.openlocfilehash: 0c51100a55ab6780c83dc95404e92275a1898da6
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744025"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>Anzeige Adapter sollten auf virtuellen Computern aktiviert werden, um Videofunktionen bereitzustellen.

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

*Das Video Gerät für den Microsoft Virtual Machine Bus ist möglicherweise auf einem virtuellen Computer deaktiviert.*

Das Videogerät für den Microsoft Virtual Machine Bus ist ein virtueller Grafikadapter, der für die Verwendung mit virtuellen Hyper-V-Computern optimiert ist. Wenn ein virtueller Computer nicht für die Verwendung des Microsoft Virtual Machine Bus-Videogeräts konfiguriert ist, wird eine Legacy Grafikkarte verwendet. Das Videogerät des Microsoft Virtual Machine Bus-Videos ist besser als eine ältere Grafikkarte.

## <a name="impact"></a>Auswirkung

*Die Video Leistung für die folgenden virtuellen Computer wird beeinträchtigt:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Verwenden Sie Geräte-Manager im Gast Betriebssystem, um das Video Gerät für den Microsoft Virtual Machine Bus zu aktivieren.*

Die Schritte, die für die Geräte-Manager Verwendung von erforderlich sind, sind je nach Betriebssystem unterschiedlich. Anweisungen hierzu finden Sie in der Hilfe zum Gast Betriebssystem.



