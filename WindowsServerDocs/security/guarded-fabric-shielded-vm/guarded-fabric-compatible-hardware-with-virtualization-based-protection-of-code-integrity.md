---
title: Kompatible Hardware mit Windows Server-Virtualisierung mit dem Schutz der Codeintegrität
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: a52ff808af94159fe50c72bf0466768047ceea90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820371"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>Kompatible Hardware mit Windows Server-Virtualisierung mit dem Schutz der Codeintegrität

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Windows Server 2016 eingeführt, eine neue Schutzgruppe Virtualisierung basierende Code zum Schutz von physischen und virtuellen Computern vor Angriffen, die Systemcode zu ändern. Um diese hohe Schutzebene zu erreichen, arbeitet Microsoft zusammen mit den Herstellern der Computer-Hardware (Original Equipment Manufacturers, OEMs oder OEMs) zu verhindern, dass böswillige Schreibvorgänge in Systemcode-Ausführung. Dieser Schutz kann auf jedem System angewendet werden und wird als einer der Bausteine für die Implementierung der Integrität von Hyper-V-Hosts für abgeschirmte virtuelle Computer (VMs) verwendet. 

Wie bei keinen Schutz hardwarebasiert einige Systeme möglicherweise nicht kompatibel sind aufgrund von Problemen wie z. B. fehlerhafte Kennzeichnung der Seiten im Arbeitsspeicher als ausführbare Dateien oder indem Sie Code zur Laufzeit ändern, was möglicherweise zu unerwarteten Fehlern, einschließlich Daten verloren gehen oder ein blauer führt tatsächlich versuchen Bildschirm-Fehler (auch als einen Stop-Fehler). 

Um kompatibel sein, und das neuen Sicherheitsfeature vollständig unterstützen, müssen OEMs implementieren die Arbeitsspeicher-Adressentabelle definiert, die im UEFI-2.6, die im Januar 2016 veröffentlicht wurde. Die Übernahme der der neue standard UEFI nimmt Zeit in Anspruch; um zu verhindern, dass Kunden, die bei der Probleme auftreten, möchten wir in der Zwischenzeit bieten Informationen zu Systemen und Konfigurationen, die getesteten diese Featureliste mit als auch Systeme, die wir kennen, die nicht kompatibel. 

## <a name="non-compatible-systems"></a>Nicht-kompatible Systeme

Die folgenden Konfigurationen sind bekannte nicht kompatible mit Virtualisierung basierende Schutz der Codeintegrität und nicht als Host für abgeschirmte VMs verwendet werden:

- Dell PowerEdge-Servern, die mit PERC H330 RAID-Controller für Weitere Informationen finden Sie unter den folgenden Artikel von Dell Support [H330 – aktivieren Sie "Unterstützung für Host-Überwachungsdiensts-Hyper-V" oder "Device Guard" unter Windows 2016-Betriebssystem führt dazu, dass Fehler beim Startvorgang des Betriebssystems](http://www.dell.com/Support/Article/us/en/19/QNA44045).  


## <a name="compatible-systems"></a>Kompatiblen Systemen

Hierbei handelt es sich um die Systeme, die wir und unsere Partner in unserer Umgebung getestet haben. Stellen Sie sicher, dass Sie überprüfen, ob das System in Ihrer Umgebung funktioniert: 

- Virtuelle Computer – können Sie Virtualisierung basierende Schutz Codeintegrität auf virtuellen Computern aktivieren, die auf einem Hyper-V-Host ab Windows Server 2016 ausgeführt werden.



