---
title: Übersicht über Container-Networking
description: Dieses Thema enthält eine Übersicht über den Netzwerk Stapel für Windows-Container und enthält Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von Container Netzwerken.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: anpaul
author: AnirbanPaul
ms.date: 09/04/2018
ms.openlocfilehash: 8e2f10c7577f6f271c3766cff9a4fb1cc9d41140
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854313"
---
# <a name="container-networking-overview"></a>Übersicht über Container-Networking

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erhalten Sie einen Überblick über den Netzwerk Stapel für Windows-Container. Außerdem finden Sie hier Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von Container Netzwerken.

Windows Server-Container sind eine vereinfachte Virtualisierungsmethode für das Betriebssystem, die Anwendungen oder Dienste von anderen Diensten trennt, die auf demselben Container Host ausgeführt werden. Windows-Container funktionieren ähnlich wie virtuelle Computer. Wenn diese Option aktiviert ist, verfügt jeder Container über eine separate Ansicht des Betriebssystems, der Prozesse, des Dateisystems, der Registrierung und der IP-Adressen, die Sie mit den virtuellen Netzwerken verbinden können. 

Ein Windows-Container nutzt einen Kernel mit dem Container Host und allen Containern, die auf dem Host ausgeführt werden. Aufgrund des gemeinsam genutzten Kernelspeichers benötigen diese Container die gleiche Kernelversion und -konfiguration. Container bieten Anwendungs Isolation durch Prozess-und Namespace Isolations Technologie.

>[!IMPORTANT]
>Windows-Container bieten keine feindliche Sicherheitsgrenze und sollten nicht zum Isolieren von nicht vertrauenswürdigem Code verwendet werden. 

Mit Windows-Containern können Sie einen Hyper-V-Host bereitstellen, auf dem Sie eine oder mehrere virtuelle Maschinen auf den VM-Hosts erstellen. Innerhalb der VM-Hosts werden Container erstellt, und der Netzwerk Zugriff erfolgt über einen virtuellen Switch, der auf dem virtuellen Computer ausgeführt wird. Sie können wiederverwendbare Images verwenden, die in einem Repository gespeichert sind, um das Betriebssystem und die Dienste in Containern bereitzustellen. Jeder Container verfügt über einen virtuellen Netzwerkadapter, der eine Verbindung mit einem virtuellen Switch herstellt und eingehenden und ausgehenden Datenverkehr weiterleitet. Sie können Container Endpunkte einem lokalen Host Netzwerk (z. b. NAT), dem physischen Netzwerk oder dem virtuellen über Lagerungs Netzwerk anfügen, das über den Sdn-Stapel erstellt wurde.

Zum Erzwingen der Isolation zwischen Containern auf demselben Host erstellen Sie für jeden Windows Server-und Hyper-V-Container ein Netzwerk Depot. Windows Server-Container verwenden eine Host-vNIC für die Verbindung mit dem virtuellen Switch. Hyper-V-Container verwenden eine synthetische VM-NIC (nicht für die Utility-VM verfügbar gemacht) für die Verbindung mit dem virtuellen Switch. 

## <a name="related-topics"></a>Verwandte Themen 

- [Windows-Container Netzwerk](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture): erfahren Sie, wie Sie Container Netzwerke für nicht-Overlay-/Sdn-bereit Stellungen erstellen und verwalten.

- [Verbinden von Container Endpunkten mit einem virtuellen Mandanten Netzwerk](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md): erfahren Sie mehr über das Erstellen und Verwalten von Container Netzwerken für virtuelle über Lagerungs Netzwerke mit Sdn. 