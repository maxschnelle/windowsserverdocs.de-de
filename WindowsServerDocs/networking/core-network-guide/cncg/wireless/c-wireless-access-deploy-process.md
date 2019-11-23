---
title: Prozess der Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Netzwerk Handbuchs "Bereitstellen von Kenn Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff".
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2555f238-926e-4b20-9bfb-9774831062da
author: shortpatti
ms.author: pashort
ms.openlocfilehash: 10c69e1aa6157c7f088f190c0283b33b630bc25f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406256"
---
# <a name="wireless-access-deployment-process"></a>Prozess der Bereitstellung des Funkzugriffs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der Prozess, mit dem Sie den drahtlosen Zugriff bereitstellen, erfolgt in den folgenden Phasen:

## <a name="stage-1--ap-deployment"></a>Phase 1 – AP-Bereitstellung

Planen, bereitstellen und Konfigurieren von APS für drahtlose Client Konnektivität und für die Verwendung mit NPS. Abhängig von Ihrer Präferenz und den Netzwerk Abhängigkeiten können Sie vor der Installation im Netzwerk entweder\-vorab Einstellungen für Ihre drahtlos Zugriffspunkte konfigurieren, oder Sie können Sie nach der Installation Remote konfigurieren.

## <a name="stage-2--adds-group-configuration"></a>Phase 2 – AD DS Gruppenkonfiguration

In AD DS müssen Sie mindestens eine Sicherheitsgruppe für drahtlose Benutzer erstellen.

Identifizieren Sie als nächstes die Benutzer, denen der drahtlose Zugriff auf das Netzwerk gestattet ist.

Fügen Sie abschließend die Benutzer zu den entsprechenden Sicherheitsgruppen hinzu, die Sie erstellt haben.

>[!NOTE]
>Standardmäßig wird die Einstellung für die **Netzwerk Zugriffsberechtigung** in Benutzerkonto-DFÜ-Eigenschaften mit der Einstellung **Zugriffs Steuerung über NPS-Netzwerk Richtlinie**konfiguriert. Es wird empfohlen, die Standardeinstellung beizubehalten, es sei denn, Sie haben bestimmte Gründe, diese Einstellung zu ändern. Dies ermöglicht es Ihnen, den Netzwerk Zugriff über die Netzwerk Richtlinien zu steuern, die Sie in NPS konfigurieren.

## <a name="stage-3--group-policy-configuration"></a>Phase 3 – Gruppenrichtlinie Konfiguration

Konfigurieren Sie mithilfe der Gruppenrichtlinienverwaltungs-Editor Microsoft Management Console \(MMC-\)das Drahtlos Netzwerk \(IEEE 802,11\) Richtlinien Erweiterung von Gruppenrichtlinie.

Zum Konfigurieren von Domänen\-Mitglieds Computern mithilfe der Einstellungen in den Drahtlos Netzwerk Richtlinien müssen Sie Gruppenrichtlinie anwenden. Wenn ein Computer erstmalig der Domäne hinzugefügt wird, wird Gruppenrichtlinie automatisch angewendet. Wenn Änderungen an Gruppenrichtlinie vorgenommen werden, werden die neuen Einstellungen automatisch angewendet:

- Durch Gruppenrichtlinie in vor\-festgelegten Intervallen

- Wenn ein Domänen Benutzer sich ab-und wieder am Netzwerk anmeldet

- Durch Neustarten des Client Computers und Anmelden bei der Domäne

Sie können auch erzwingen, dass Gruppenrichtlinie aktualisiert wird, während Sie an einem Computer angemeldet sind, indem Sie den Befehl **gpupdate** an der Eingabeaufforderung ausführen.

## <a name="stage-4--nps-configuration"></a>Phase 4 – NPS-Konfiguration

Verwenden Sie einen Konfigurations-Assistenten in NPS, um drahtlos Zugriffspunkte als RADIUS-Clients hinzuzufügen und um die Netzwerk Richtlinien zu erstellen, die NPS beim Verarbeiten von Verbindungsanforderungen verwendet.

Wenn Sie den Assistenten verwenden, um die Netzwerk Richtlinien zu erstellen, geben Sie PEAP als EAP-Typ und die Sicherheitsgruppe "drahtlose Benutzer" an, die in der zweiten Phase erstellt wurde.

## <a name="stage-5--deploy-wireless-clients"></a>Phase 5 – Bereitstellen von drahtlosen Clients

Verwenden Sie Client Computer, um eine Verbindung mit dem Netzwerk herzustellen.

Für Domänen Mitglieds Computer, die sich am kabelgebundenen LAN anmelden können, werden die erforderlichen drahtlos Konfigurationseinstellungen automatisch angewendet, wenn Gruppenrichtlinie aktualisiert wird.

Wenn Sie die Einstellung in Drahtlos Netzwerk \(IEEE 802,11\) Richtlinien aktivieren, um automatisch eine Verbindung herzustellen\-, wenn sich der Computer im Broadcast Bereich des drahtlos Netzwerks befindet, wird automatisch versucht, eine Verbindung mit dem drahtlosen LAN herzustellen.

Zum Herstellen einer Verbindung mit dem Drahtlos Netzwerk müssen Benutzer nur Ihre Domänen Benutzernamen-und Kenn Wort Anmelde Informationen angeben, wenn Sie von Windows aufgefordert werden.

Informationen zum Planen Ihrer drahtlos Zugriffs Bereitstellung finden Sie unter [Planen der Bereitstellung von drahtlos Zugriff](d-wireless-access-planning.md).
