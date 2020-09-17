---
title: Konfigurieren Sie den Server mit einer ausreichenden Anzahl dynamischer MAC-Adressen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: a2804519-9790-4006-80b6-e990a8f505fe
ms.date: 8/16/2016
ms.openlocfilehash: 0631954ccb89c41637e92d1170bed99d82a085b5
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744125"
---
# <a name="configure-the-server-with-a-sufficient-amount-of-dynamic-mac-addresses"></a>Konfigurieren Sie den Server mit einer ausreichenden Anzahl dynamischer MAC-Adressen.

>Gilt für: Windows Server 2016

*Dieses Thema dient der Behebung eines bestimmten Problems, das durch einen Best Practices Analyzer Scan identifiziert wird. Die Informationen in diesem Thema sollten nur auf Computer angewendet werden, auf denen die Hyper-V-Best Practices Analyzer für Sie ausgeführt wurde und die in diesem Thema behandelt werden. Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Die Anzahl der verfügbaren dynamischen MAC-Adressen ist niedrig.*

## <a name="impact"></a>Auswirkung

*Wenn keine dynamischen MAC-Adressen verfügbar sind, können virtuelle Computer, die für die Verwendung einer dynamischen MAC-Adresse konfiguriert sind, nicht gestartet werden.*

## <a name="resolution"></a>Lösung

*Verwenden Sie den Manager für virtuelle Switches, um den Bereich dynamischer Adressen anzuzeigen und zu erweitern.*



