---
title: Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
ms.author: benarm
author: BenjaminArmstrong
ms.date: 10/03/2016
ms.openlocfilehash: 891ad97d8ae5ef01c6dbfd0d59f7be6316c6e687
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746745"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows

>Gilt für: Windows Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Hyper-V unterstützt sowohl emulierten als auch Hyper-v-spezifische Geräte für virtuelle Linux-und FreeBSD-Maschinen. Bei der Ausführung mit emulierten Geräten muss keine zusätzliche Software installiert werden. Emulierten Geräte bieten jedoch keine hohe Leistung und können nicht die umfassende Verwaltungsinfrastruktur für virtuelle Computer nutzen, die die Hyper-V-Technologie bietet. Um alle von Hyper-v bereitgestellten Vorteile vollständig nutzen zu können, ist es am besten, Hyper-v-spezifische Geräte für Linux und FreeBSD zu verwenden. Die Sammlung der Treiber, die zum Ausführen von Hyper-V-spezifischen Geräten erforderlich sind, wird als Linux-Integration Services (LIS) oder FreeBSD Integration Services (bis) bezeichnet.

LIS wurde zum Linux-Kernel hinzugefügt und wird für neue Releases aktualisiert. Linux-Distributionen, die auf älteren Kernel basieren, haben jedoch möglicherweise nicht die neuesten Verbesserungen oder Korrekturen. Microsoft stellt einen Download bereit, der installierbare LIS-Treiber für einige Linux-Installationen auf der Grundlage dieser älteren Kernel enthält. Da Verteilungs Anbieter Versionen von Linux-Integration Services enthalten, empfiehlt es sich, ggf. die neueste herunterladbare Version von Lis für Ihre Installation zu installieren.

Bei anderen Linux-Distributionen werden die Änderungen regelmäßig in den Kernel und die Anwendungen des Betriebssystems integriert, sodass keine separaten Downloads oder Installationen erforderlich sind.

Für ältere FreeBSD-Releases (vor 10,0) stellt Microsoft Ports bereit, die installierbare-bis-Treiber und entsprechende Daemons für FreeBSD Virtual Machines enthalten. Für Neuere FreeBSD-Releases ist bis in das FreeBSD-Betriebssystem integriert, und es ist kein separater Download oder eine separate Installation erforderlich, mit Ausnahme eines herunterladbare KVP-Ports, der für FreeBSD 10,0 benötigt wird.

> [!TIP]
> - Laden Sie [Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) aus dem Evaluation Center herunter.

Ziel dieses Inhalts sind die Bereitstellung von Informationen, die Ihnen helfen, Ihre Linux-oder FreeBSD-Bereitstellung auf Hyper-V zu vereinfachen. Zu den Details gehören:

* Linux-Distributionen oder FreeBSD-Releases, die den Download und die Installation von Lis-oder bis-Treibern erfordern.

* Linux-Distributionen oder FreeBSD-Releases, die integrierte LIS-oder bis-Treiber enthalten.

* Featureverteilungszuordnungen, die auf die Features in großen Linux-Distributionen oder FreeBSD-Releases hinweisen.

* Bekannte Probleme und Problem Umgehungen für jede Distribution oder Version.

* Funktionsbeschreibung für jede LIS-oder bis-Funktion.

**Möchten Sie einen Vorschlag zu Features und Funktionen erstellen?** Gibt es etwas, das wir besser machen können? Auf der [Windows Server User Voice](https://windowsserver.uservoice.com/forums/295062-linux-support) -Website können Sie neue Features und Funktionen für Linux-und FreeBSD-Virtual Machines auf Hyper-V vorschlagen und sehen, was andere Personen sagen.

## <a name="in-this-section"></a>In diesem Abschnitt

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
