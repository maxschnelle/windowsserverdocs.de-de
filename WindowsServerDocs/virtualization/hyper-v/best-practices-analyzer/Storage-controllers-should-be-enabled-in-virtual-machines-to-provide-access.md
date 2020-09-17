---
title: Speichercontroller müssen in virtuellen Computern aktiviert werden, um Zugriff auf den angeschlossenen Speicher bereitzustellen.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 532548a1-8ffe-4b5b-902e-ed2f0819012b
ms.date: 8/16/2016
ms.openlocfilehash: 5eb1767fd51253ed26c0a169be1043b633dbcbcd
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746195"
---
# <a name="storage-controllers-should-be-enabled-in-virtual-machines-to-provide-access-to-attached-storage"></a>Speichercontroller müssen in virtuellen Computern aktiviert werden, um Zugriff auf den angeschlossenen Speicher bereitzustellen.

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

*Ein oder mehrere Speichercontroller sind möglicherweise auf einem virtuellen Computer deaktiviert.*

## <a name="impact"></a>Auswirkung

*Virtuelle Computer können keinen mit einem deaktivierten Speichercontroller verbundenen Speicher verwenden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Verwenden Sie Geräte-Manager im Gast Betriebssystem, um alle Speichercontroller zu aktivieren. Wenn der Speichercontroller nicht erforderlich ist, verwenden Sie den Hyper-V-Manager, um ihn vom virtuellen Computer zu entfernen.*

Anweisungen zur Verwendung von Geräte-Manager finden Sie in der Hilfe zum Gast Betriebssystem. Anweisungen zum Entfernen des Speicher Controllers finden Sie im folgenden Verfahren.

#### <a name="to-remove-a-scsi-storage-controller-from-the-virtual-machine"></a>So entfernen Sie einen SCSI-Speichercontroller von der virtuellen Maschine

1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.

2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten.

3.  Wenn die virtuelle Maschine ausgeführt wird, fahren Sie den virtuellen Computer herunter. Klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **herunter**fahren.

4.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.

5.  Klicken Sie im linken Bereich des Dialog Felds **Einstellungen** unter **Hardware**auf SCSI- **Controller**.

6.  Klicken Sie im rechten Bereich auf **Entfernen**.



