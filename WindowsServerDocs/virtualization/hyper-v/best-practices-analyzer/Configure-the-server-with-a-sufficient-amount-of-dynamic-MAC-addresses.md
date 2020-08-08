---
title: Konfigurieren Sie den Server mit einer ausreichenden Anzahl dynamischer MAC-Adressen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: a2804519-9790-4006-80b6-e990a8f505fe
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b0416bb38e78f62bddf8a7937eb821ee0988286d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968377"
---
# <a name="configure-the-server-with-a-sufficient-amount-of-dynamic-mac-addresses"></a>Konfigurieren Sie den Server mit einer ausreichenden Anzahl dynamischer MAC-Adressen.

>Gilt für: Windows Server 2016

*Dieses Thema dient der Behebung eines bestimmten Problems, das durch einen Best Practices Analyzer Scan identifiziert wird. Die Informationen in diesem Thema sollten nur auf Computer angewendet werden, auf denen die Hyper-V-Best Practices Analyzer für Sie ausgeführt wurde und die in diesem Thema behandelt werden. Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Die Anzahl der verfügbaren dynamischen MAC-Adressen ist niedrig.*

## <a name="impact"></a>Auswirkung

*Wenn keine dynamischen MAC-Adressen verfügbar sind, können virtuelle Computer, die für die Verwendung einer dynamischen MAC-Adresse konfiguriert sind, nicht gestartet werden.*

## <a name="resolution"></a>Lösung

*Verwenden Sie den Manager für virtuelle Switches, um den Bereich dynamischer Adressen anzuzeigen und zu erweitern.*



