---
title: Kompatible Hardware mit Windows Server Virtualization-basiertem Schutz der Code Integrität
ms.prod: windows-server
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 32194d6f0634ab9cee90b321ea7a1f3e2769542d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856873"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>Kompatible Hardware mit Windows Server Virtualization-basiertem Schutz der Code Integrität

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In Windows Server 2016 wurde ein neuer virtualisierungbasierter Code Schutz eingeführt, um physische und virtuelle Computer vor Angriffen zu schützen, die den Systemcode ändern. Um diese hohe Schutz Ebene zu erreichen, arbeitet Microsoft zusammen mit den Computer Hardwareherstellern (Original Equipment Manufacturers, OEMs) zusammen, um schädliche Schreibvorgänge in den System Ausführungs Code zu verhindern. Dieser Schutz kann auf jedes System angewendet werden und wird als einer der Bausteine für die Implementierung der Hyper-V-Host Integrität für abgeschirmte virtuelle Computer (VMS) verwendet. 

Wie bei jedem hardwarebasierten Schutz sind einige Systeme aufgrund von Problemen wie der falschen Markierung von Speicherseiten als ausführbare Dateien oder durch das tatsächliche ändern von Code zur Laufzeit möglicherweise nicht kompatibel. Dies kann zu unerwarteten Fehlern, z. b. Datenverlust oder einem blauen Bildschirm Fehler (auch als "Fehler beim Abbrechen" bezeichnet) führen. 

Um kompatibel zu sein und die neue Sicherheitsfunktion vollständig zu unterstützen, müssen OEMs die in UEFI 2,6 definierte Speicher Adress Tabelle implementieren, die in Jan. 2016 veröffentlicht wurde. Die Übernahme des neuen UEFI-Standards nimmt Zeit in Anspruch. um Kunden zu verhindern, dass Probleme auftreten, möchten wir in der Zwischenzeit Informationen über Systeme und Konfigurationen bereitstellen, mit denen wir diese featuremenge getestet haben, sowie über Systeme, die nicht kompatibel sind. 

## <a name="non-compatible-systems"></a>Nicht kompatible Systeme

Die folgenden Konfigurationen sind bekanntermaßen nicht kompatibel mit dem virtualisierungsbasierten Schutz der Code Integrität und können nicht als Host für abgeschirmte VMS verwendet werden:

- Dell PowerEdge-Server, auf denen PERC H330 RAID-Controller ausgeführt werden. Weitere Informationen finden Sie im folgenden Artikel des Dell-Supports [H330 – Aktivieren von "Host-Überwachungs-Hyper-V-Unterstützung" oder "Device Guard" bei Win 2016 OS verursacht Betriebssystem Start Fehler](http://www.dell.com/Support/Article/us/en/19/QNA44045).  


## <a name="compatible-systems"></a>Kompatible Systeme

Dabei handelt es sich um die Systeme, die wir und unsere Partner in unserer Umgebung getestet haben. Vergewissern Sie sich, dass das System in Ihrer Umgebung erwartungsgemäß funktioniert: 

- Virtual Machines – Sie können den virtualisierungsbasierten Schutz der Code Integrität auf virtuellen Computern aktivieren, die auf einem Hyper-V-Host ab Windows Server 2016 ausgeführt werden.



