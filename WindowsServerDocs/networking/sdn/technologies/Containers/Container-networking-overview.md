---
title: Übersicht über Container-Networking
description: Dieses Thema bietet eine Übersicht über den Netzwerkstapel für Windows-Container und enthält Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von Netzwerken für Container.
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: pashort
author: jmesser81
ms.date: 09/04/2018
ms.openlocfilehash: 72b1ac739d9012ac7b90e97abe22e5f321ddba63
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886141"
---
# <a name="container-networking-overview"></a>Übersicht über Container-Networking

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wir geben Ihnen einen Überblick über den Netzwerkstapel für Windows-Container, und schließen wir Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von Netzwerken für Container, in diesem Thema.

Windows Server-Container sind eine schlankes Betriebssystem Virtualization-Methode, die Trennung von Anwendungen oder Dienste von anderen Diensten, die auf demselben containerhost ausgeführt. Windows-Containern funktionieren ähnlich wie virtuelle Computer. Wenn aktiviert, verfügt jeder Container eine separate Ansicht von dem Betriebssystem, Prozesse, Dateisystem, Registrierung und IP-Adressen, die Sie eine Verbindung mit virtuellen Netzwerken herstellen können. 

Ein Windows-Container teilt sich einen Kernel mit dem containerhost und allen Containern, die auf dem Host ausgeführt. Aufgrund des gemeinsam genutzten Kernelspeichers benötigen diese Container die gleiche Kernelversion und -konfiguration. Container bieten Anwendungsisolation mittels einer isolationstechnologie für Prozesse und Namespaces.

>[!IMPORTANT]
>Windows-Container bieten keine sicherheitsbegrenzung schädlicher und sollte nicht verwendet werden, um nicht vertrauenswürdigem Code zu isolieren. 

Mit Windows-Containern können Sie einen Hyper-V-Host bereitstellen, in dem Sie eine oder mehrere virtuelle Computer auf den VM-Hosts erstellen. In den VM-Hosts Container erstellt, und der Zugriff über einen virtuellen Switch auf dem virtuellen Computer ausgeführt wird. Sie können wieder verwendbare Images, die in einem Repository gespeichert verwenden, das Betriebssystem und Dienste in Containern bereitstellen. Jeder Container verfügt über einen virtuellen Netzwerkadapter das mit einem virtuellen Switch verbunden wird, die Weiterleitung von eingehendem und ausgehendem Datenverkehr. Sie können den containerendpunkte ein Netzwerk des lokalen Hosts (z. B. NAT), physischen oder virtuellen Overlay-Netzwerk im SDN-Stapel erstellt anfügen.

Zur Erzwingung der Trennung zwischen Containern auf demselben Host, erstellen Sie ein netzwerkdepot für die einzelnen Windows Server und Hyper-V-Container. Windows Server-Container verwenden eine Host-vNIC für die Verbindung mit dem virtuellen Switch. Hyper-V-Container verwenden eine synthetische VM-NIC (nicht für die Utility-VM verfügbar gemacht) für die Verbindung mit dem virtuellen Switch. 

## <a name="related-topics"></a>Verwandte Themen 

- [Windows-Containernetzwerk](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture): Informationen Sie zum Erstellen und Verwalten von containernetzwerke für nicht-Overlay/SDN-Bereitstellungen.

- [Verbinden von containerendpunkten mit einem virtuellen mandantennetzwerk](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md): Informationen Sie zum Erstellen und Verwalten von containernetzwerke für Overlay virtuelle Netzwerke mit SDN. 