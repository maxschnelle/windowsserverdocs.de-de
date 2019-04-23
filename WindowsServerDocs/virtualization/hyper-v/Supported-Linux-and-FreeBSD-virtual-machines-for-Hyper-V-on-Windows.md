---
title: Unterstützte Linux- und FreeBSD-Computer für Hyper-V unter Windows
description: Enthält die Linux-Integrationsdienste und Features, die unterschiedlichen Versionen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 9df495bdc67b06a675fec050fb4c2960337ce8ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832901"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Unterstützte Linux- und FreeBSD-Computer für Hyper-V unter Windows

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Hyper-V unterstützt emulierten und Hyper-V-spezifischer Geräte für Linux- und FreeBSD-Computer. Bei der Ausführung mit emulierte Geräte ist keine zusätzliche Software muss installiert sein. Jedoch emulierte Geräte bieten keine hohe Leistung und nicht die, die die Hyper-V-Technologie bietet umfangreiche VM-Verwaltungsinfrastruktur genutzt. Um die vollständigen alle Vorteile nutzen, die Hyper-V bietet, empfiehlt es sich, Hyper-V-spezifischer Geräte für Linux und FreeBSD zu verwenden. Die Auflistung der Treiber, die zum Ausführen von Hyper-V-spezifischer Geräte erforderlich sind, werden als Linux-Integrationsdienste (LIS) oder FreeBSD Integration Services (BIS) bezeichnet.

LIS zum Linux-Kernel hinzugefügt wurde und wird für neue Versionen aktualisiert. Aber basierte auf älteren Kernels von Linux-Distributionen ggf. nicht die neuesten Verbesserungen oder Updates. Microsoft bietet einen Download, die installierbaren LIS-Treiber für einige Linux-Installationen, die basierend auf diesen älteren Kernels enthält. Da Verteilung von Herstellern Linux Integration Services-Versionen enthalten, ist es am besten, installieren Sie die neueste herunterladbare Version von LIS, sofern zutreffend, für die Installation.

Für andere Linux-Distributionen LIS sind Änderungen regelmäßig in die Betriebssystem-Kernel und Anwendungen integriert, sodass kein separater Download oder Installation erforderlich ist.

Für ältere FreeBSD-Versionen (vor 10.0) bietet Microsoft-Ports, die installierbaren BIS Treiber und die entsprechenden Daemons für die virtuelle FreeBSD-Computer enthalten. Für neuere FreeBSD-Versionen BIS ist in der FreeBSD-Betriebssystem integriert, und keine separaten Download oder eine Installation ist erforderlich, außer ein Download der KVP-Ports, der für FreeBSD 10.0 erforderlich ist.

> [!TIP]
> - Herunterladen [WindowsServer 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016) aus dem Evaluation Center.
> - Herunterladen [Microsoft Hyper-V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016) aus dem Evaluation Center.

Das Ziel dieses Inhalts ist, um Informationen bereitzustellen, können für eine Bereitstellung Linux und FreeBSD in Hyper-V einfachere. Spezifische Details umfassen Folgendes:

* Linux-Distributionen oder FreeBSD-Versionen, die den Download und Installation von LIS oder BIS Treiber erfordern.

* Linux-Distributionen oder FreeBSD-Versionen, die integrierte LIS oder BIS Treiber enthalten.

* Featurezuordnungen Verteilung erstellen, die die Funktionen in gängige Linux-Distributionen oder FreeBSD-Versionen angeben.

* Bekannte Probleme und problemumgehungen für jede Verteilung oder Version.

* Funktionsbeschreibung für jede Funktion LIS oder BIS.

**Möchten Sie einen Vorschlag zu Features und Funktionen zu machen?** Gibt es etwas, das wir besser machen können? Sie können die [Windows Server User Voice](https://windowsserver.uservoice.com/forums/295062-linux-support) Standort neue Features und Funktionen für Linux- und FreeBSD-Maschinen auf Hyper-V vorschlagen und sehen, was andere Personen zu sagen haben.

## <a name="in-this-section"></a>Inhalt dieses Abschnitts

* [Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Virtuelle Debian-Computer unterstützt auf Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux-VMs auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte SUSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte Ubuntu-VMs auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von FreeBSD in Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
