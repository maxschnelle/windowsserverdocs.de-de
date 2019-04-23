---
title: Prozess der Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2555f238-926e-4b20-9bfb-9774831062da
author: shortpatti
ms.author: pashort
ms.openlocfilehash: 6a286cf10e066043ee6f514bbf468bfb2b13f162
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879841"
---
# <a name="wireless-access-deployment-process"></a>Prozess der Bereitstellung des Funkzugriffs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die, die Sie verwenden, um den drahtlosen Zugriff bereitstellen, wird in dieser Phasen:

## <a name="stage-1--ap-deployment"></a>Phase 1 – Bereitstellung von AP

Planen Sie, Bereitstellen Sie und konfigurieren Sie Ihre Zugriffspunkte für die drahtlosen Client-Konnektivität und für die Verwendung mit NPS. Abhängig von Ihrer Präferenz und Netzwerk-Abhängigkeiten, können Sie vorab\-konfigurieren Sie Einstellungen für Ihre drahtlosen Zugriffspunkte vor der Installation in Ihrem Netzwerk, oder Sie können sie per Remotezugriff konfigurieren, nach der Installation.

## <a name="stage-2--adds-group-configuration"></a>Phase 2: Konfiguration von AD DS-Gruppe

In AD DS müssen Sie einen oder mehrere drahtlose Benutzer Sicherheitsgruppen erstellen.

Identifizieren Sie als Nächstes die Benutzer, die drahtlosen Zugriff auf das Netzwerk zulässig sind.

Fügen Sie schließlich die Benutzer auf die entsprechende drahtlose Benutzer-Sicherheitsgruppen, die Sie erstellt haben.

>[!NOTE]
>In der Standardeinstellung die **Netzwerk Zugriffsberechtigung** in DFÜ-Eigenschaften des Benutzerkontos mit der Einstellung konfiguriert ist **steuern den Zugriff über die Netzwerkrichtlinie für NPS**. Wenn Sie besondere Gründe Ändern dieser Einstellung haben, empfiehlt es sich, dass Sie die standardmäßigen übernehmen. Dadurch können Sie Zugriff auf das Netzwerk durch die Netzwerkrichtlinien steuern, die Sie in NPS konfigurieren.

## <a name="stage-3--group-policy-configuration"></a>Phase 3: Konfiguration von Gruppenrichtlinien

Konfigurieren Sie das WLAN-Netzwerk \(IEEE 802.11\) richtlinienerweiterung der Gruppenrichtlinie mithilfe der Gruppenrichtlinienverwaltungs-Editor-Microsoft Management Console \(MMC\).

So konfigurieren Sie die Domäne\-Mitgliedscomputer, die mit den Einstellungen in den Richtlinien für Drahtlosnetzwerke, Sie müssen Gruppenrichtlinien anwenden. Wenn ein Computer zunächst mit der Domäne hinzugefügt wird, wird die Gruppenrichtlinie automatisch angewendet. Wenn Änderungen an der Gruppenrichtlinie vorgenommen werden, werden die neuen Einstellungen automatisch angewendet werden:

- Durch eine Gruppenrichtlinie auf vor\-bestimmt die Intervalle

- Wenn ein Domänenbenutzer abgemeldet und dann zurück an das Netzwerk

- Durch den Client neu, und mit der Domäne anmelden

Sie können auch erzwingen, Gruppenrichtlinien zu aktualisieren, während Sie auf einem Computer angemeldet, mithilfe des Befehls **Gpupdate** an der Eingabeaufforderung.

## <a name="stage-4--nps-configuration"></a>Schritt 4 – NPS-Konfiguration

Verwenden Sie einen Konfigurations-Assistenten auf dem Netzwerkrichtlinienserver, drahtlose Zugriffspunkte als RADIUS-Clients hinzufügen und die Netzwerkrichtlinien erstellen, die NPS verwendet, bei der Verarbeitung von Anforderungen von Verbindungen.

Bei Verwendung des Assistenten, um den Netzwerkrichtlinien zu erstellen, geben Sie PEAP, als EAP-Typ und die Sicherheitsgruppe der drahtlose Benutzer, die in der zweiten Phase erstellt wurde.

## <a name="stage-5--deploy-wireless-clients"></a>Phase 5: Bereitstellen von WLAN-clients

Verwenden Sie Clientcomputer eine Verbindung mit dem Netzwerk herstellen.

Mitgliedscomputer der Domäne, die an das verdrahtete LAN anmelden können, werden die erforderlichen funkkonfigurationseinstellungen automatisch angewendet, wenn Gruppenrichtlinien aktualisiert wird.

Wenn Sie die Einstellung im Drahtlosnetzwerk aktiviert haben \(IEEE 802.11\) Richtlinien automatisch eine Verbindung herstellen, wenn der Computer befindet broadcast-Bereich von dem Drahtlosnetzwerk verbinden, Ihre drahtlose, Domäne\-verknüpften Computer werden dann versucht automatisch, für die Verbindung mit dem drahtlosen LAN.

Um mit dem drahtlosen Netzwerk zu verbinden, müssen Benutzer nur ihre Namen und das Kennwort domänenbenutzeranmeldeinformationen Aufforderung durch Windows bereitstellen.

Informationen zur Planung Ihrer Bereitstellung des funkzugriffs finden Sie unter [drahtlosen Zugriff Bereitstellungsplanung](d-wireless-access-planning.md).
