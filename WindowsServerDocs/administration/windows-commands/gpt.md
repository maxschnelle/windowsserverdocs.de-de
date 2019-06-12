---
title: gpt
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cba9839f98dfd5a72289838273a057dd0e09a7e5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438183"
---
# <a name="gpt"></a>gpt

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Grundlegende Datenträger GUID-Partitionstabelle (Gpt) weist die GPT-Attribute auf die Partition mit dem Fokus.  GPT-Partitionsattribute bieten zusätzliche Informationen zur Verwendung der Partition an. Einige Attribute sind spezifisch für den Partitionstyp GUID.

> [!CAUTION]
> Ändern der GPT-Attribute möglicherweise die Basisdaten Volumes Laufwerkbuchstaben zugewiesen werden soll, oder, um zu verhindern, dass das Dateisystem Einbindung fehlschlägt. Sie sollten die Gpt-Attribute nicht ändern, es sei denn, Sie sind ein Originalgerätehersteller (OEM) oder IT-Experte, der bereits über Erfahrung mit Gpt-Datenträger ist.
> ## <a name="syntax"></a>Syntax
> ```
> gpt attributes=<n>
> ```
> ## <a name="parameters"></a>Parameter
> 
> |   Parameter    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
> |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | attributes=<n> | Gibt den Wert für das Attribut, das Sie auf die Partition mit dem Fokus anwenden möchten. Das Feld der Gpt-Attribut ist ein 64-Bit-Feld, das zwei Unterfeldern. Das höhere Feld wird nur im Rahmen der Partitions-ID, interpretiert, während das untere Feld für alle Partitions-IDs ist. Zulässige Werte sind:<br /><br />-   **0 x 0000000000000001**. Gibt an, dass die Partition durch den Computer erforderlich ist, ordnungsgemäß funktioniert.<br />-   **0x8000000000000000**. Gibt an, dass die Partition nicht erhält einen Laufwerkbuchstaben standardmäßig, wenn der Datenträger verschoben wird, auf einen anderen Computer oder der Datenträger von einem Computer zum ersten Mal angezeigt wird.<br />-   **0x4000000000000000**. Blendet eine Partition des Volumes an. Die Partition wird von der bereitstellungs-Manager, also nicht erkannt werden.<br />-   **0x2000000000000000**. Gibt an, dass die Partition eine Schattenkopie von einer anderen Partition.<br />-   **0x1000000000000000**. Gibt an, dass die Partition schreibgeschützt ist. Dieses Attribut verhindert, dass das Volume geschrieben wird.<br /><b />Weitere Informationen zu diesen Attributen finden Sie im Attributabschnitt "am [Create_PARTITION_PARAMETERS Struktur](https://go.microsoft.com/fwlink/?LinkId=203812) (<https://go.microsoft.com/fwlink/?LinkId=203812>). |
> 
> ## <a name="remarks"></a>Hinweise
> - Die EFI-Systempartition enthält nur die Binärdateien, die zum Starten des Betriebssystems. Dies erleichtert es OEM-Binärdateien oder Binärdateien spezifisch für ein Betriebssystem in anderen Partitionen platziert werden.
> - Eine einfache GPT-Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Partition** Befehl aus, wählen Sie eine einfache Gpt-Partition und verschiebt den Fokus auf sie.
>   ## <a name="BKMK_examples"></a>Beispiele für
>   Wenn Sie einen Gpt-Datenträger auf einem neuen Computer verschieben und möchte verhindern, dass dieser Computer automatisch ein Laufwerkbuchstabe zugewiesen, auf die Partition mit Fokus, Typ:
>   ```
>   gpt attributes=0x8000000000000000
>   ```

