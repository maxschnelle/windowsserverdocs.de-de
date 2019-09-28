---
title: Kompatible Hardware mit Windows Server Virtualization-basiertem Schutz der Code Integrität
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5a9a4b91cc3528ce59f8ef3e4952b6162ca5c74e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403690"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>Kompatible Hardware mit Windows Server Virtualization-basiertem Schutz der Code Integrität

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In Windows Server 2016 wurde ein neuer virtualisierungbasierter Code Schutz eingeführt, um physische und virtuelle Computer vor Angriffen zu schützen, die den Systemcode ändern. Um diese hohe Schutz Ebene zu erreichen, arbeitet Microsoft zusammen mit den Computer Hardwareherstellern (Original Equipment Manufacturers, OEMs) zusammen, um schädliche Schreibvorgänge in den System Ausführungs Code zu verhindern. Dieser Schutz kann auf jedes System angewendet werden und wird als einer der Bausteine für die Implementierung der Hyper-V-Host Integrität für abgeschirmte virtuelle Computer (VMS) verwendet. 

Wie bei jedem hardwarebasierten Schutz sind einige Systeme aufgrund von Problemen wie der falschen Markierung von Speicherseiten als ausführbare Dateien oder dem tatsächlichen Versuch, Code zur Laufzeit zu ändern, möglicherweise nicht kompatibel. Dies kann zu unerwarteten Fehlern, z. b. Datenverlust oder einem blauen, führen. Bildschirm Fehler (auch als "Fehler beim Abbrechen" bezeichnet). 

Um kompatibel zu sein und die neue Sicherheitsfunktion vollständig zu unterstützen, müssen OEMs die in UEFI 2,6 definierte Speicher Adress Tabelle implementieren, die in Jan. 2016 veröffentlicht wurde. Die Übernahme des neuen UEFI-Standards nimmt Zeit in Anspruch. um Kunden zu verhindern, dass Probleme auftreten, möchten wir in der Zwischenzeit Informationen über Systeme und Konfigurationen bereitstellen, mit denen wir diese featuremenge getestet haben, sowie über Systeme, die nicht kompatibel sind. 

## <a name="non-compatible-systems"></a>Nicht kompatible Systeme

Die folgenden Konfigurationen sind bekanntermaßen nicht kompatibel mit dem virtualisierungsbasierten Schutz der Code Integrität und können nicht als Host für abgeschirmte VMS verwendet werden:

- Dell PowerEdge-Server, auf denen PERC H330 RAID-Controller ausgeführt werden. Weitere Informationen finden Sie im folgenden Artikel des Dell-Supports [H330 – Aktivieren von "Host-Überwachungs-Hyper-V-Unterstützung" oder "Device Guard" bei Win 2016 OS verursacht Betriebssystem Start Fehler](http://www.dell.com/Support/Article/us/en/19/QNA44045).  


## <a name="compatible-systems"></a>Kompatible Systeme

Dabei handelt es sich um die Systeme, die wir und unsere Partner in unserer Umgebung getestet haben. Vergewissern Sie sich, dass das System in Ihrer Umgebung erwartungsgemäß funktioniert: 

- Virtual Machines – Sie können den virtualisierungsbasierten Schutz der Code Integrität auf virtuellen Computern aktivieren, die auf einem Hyper-V-Host ab Windows Server 2016 ausgeführt werden.



