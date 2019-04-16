---
title: WLAN-Bereitstellungsprozess
description: In diesem Thema ist Teil des Windows Server 2016 Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2555f238-926e-4b20-9bfb-9774831062da
author: shortpatti
ms.author: pashort
ms.openlocfilehash: fcdbe796e4d530604dfec448e817eab877d34c4f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment-process"></a>WLAN-Bereitstellungsprozess

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die, mit der drahtlosen Zugriff bereitstellen, wird in diesen Phasen:

## <a name="stage-1--ap-deployment"></a>Phase 1 – AP-Bereitstellung

Planen Sie, Bereitstellen Sie und konfigurieren Sie Ihre Zugriffspunkte für drahtlosen Client-Konnektivität und für die Verwendung mit NPS. Je nach Ihrer Vorlieben und der Netzwerk-Abhängigkeiten können Sie entweder registrierungseintragswert-Einstellungen für Ihre drahtlosen Zugriffspunkte vor der Installation werden in Ihrem Netzwerk konfigurieren, oder Sie können sie Remote nach der Installation konfigurieren.

## <a name="stage-2--ad-ds-group-configuration"></a>Schritt 2 – Konfiguration von AD DS-Gruppe

In AD DS müssen Sie einen oder mehrere Computer mit drahtlosem Sicherheitsgruppen erstellen.

Identifizieren Sie anschließend die Benutzer, die drahtlosen Zugriff auf das Netzwerk zulässig sind.

Fügen Sie schließlich die Benutzer zu den entsprechenden Benutzern Sicherheitsgruppen, die Sie erstellt haben.

>[!NOTE]
>Standardmäßig die **Netzwerkzugriffsberechtigungen** in DFÜ-Eigenschaften des Benutzerkontos konfiguriert ist mit der Einstellung **steuern den Zugriff über die NPS-Netzwerkrichtlinien**. Es sei denn, Sie spezifischen Gründe zum Ändern dieser Einstellung verfügen, empfiehlt es sich, dass Sie die standardmäßigen übernehmen. Dadurch können Sie die Steuerung des Netzwerkzugriffs durch die Netzwerkrichtlinien, die Sie in NPS konfigurieren.

## <a name="stage-3--group-policy-configuration"></a>Phase 3 – der Konfiguration von Gruppenrichtlinien

Konfigurieren Sie das WLAN-Netzwerk \ (IEEE 802.11\) Erweiterung der Gruppenrichtlinie mithilfe der Gruppenrichtlinienverwaltungs-Editor Microsoft Management Console \(MMC\).

Um Domäne\-Computern mit den Einstellungen in den Richtlinien für drahtlose Netzwerke konfigurieren, müssen Sie eine Gruppenrichtlinie anwenden. Wenn ein Computer zunächst mit der Domäne hinzugefügt wird, wird automatisch eine Gruppenrichtlinie angewendet. Wenn Änderungen an der Gruppenrichtlinie vorgenommen werden, werden die neuen Einstellungen automatisch angewendet:

- Durch eine Gruppenrichtlinie registrierungseintragswert vorgegebenen Intervallen

- Wenn ein Domänenbenutzer abmeldet und wieder zurück an das Netzwerk

- Durch die Clientcomputer neu zu starten und Anmelden bei der Domäne

Sie können auch erzwingen, der Gruppenrichtlinie zu aktualisieren, während Sie auf einem Computer angemeldet, durch Ausführen des Befehls **Gpupdate** an der Eingabeaufforderung.

## <a name="stage-4--nps-server-configuration"></a>Schritt 4 – NPS-Serverkonfiguration

Verwenden Sie ein Konfigurations-Assistent auf dem Netzwerkrichtlinienserver, drahtlose Zugriffspunkte als RADIUS-Clients hinzufügen und die Netzwerkrichtlinien erstellen, die NPS verwendet, bei der Verarbeitung von verbindungsanforderungen.

Wenn der Assistent zum Erstellen Sie der Netzwerkrichtlinien, geben Sie PEAP als EAP-Typ und die Benutzer-Sicherheitsgruppe, die in der zweiten Phase erstellt wurde.

## <a name="stage-5--deploy-wireless-clients"></a>Schritt 5: Bereitstellen von WLAN-clients

Verwenden Sie Clientcomputer eine Verbindung mit dem Netzwerk herstellen.

Für Computer, die mit dem drahtgebundenen Netzwerk anmelden können, werden die erforderlichen funkkonfigurationseinstellungen automatisch angewendet, wenn Gruppenrichtlinien aktualisiert wird.

Wenn Sie die Einstellung in Drahtlosnetzwerk aktiviert haben \ (IEEE 802.11\) Richtlinien automatisch eine Verbindung herstellen, wenn der Computer innerhalb des Übertragungsbereichs des Funknetzwerks, Ihre drahtlosen Domäne\ verbundenen Computer wird dann wird automatisch versucht, eine Verbindung mit dem WLAN.

Um eine Verbindung mit dem Drahtlosnetzwerk herzustellen, müssen Benutzer nur ihren Namen und das Kennwort Anmeldeinformationen des Domänenbenutzers nach Aufforderung durch Windows angeben.

Bei der Planung die Bereitstellung des funkzugriffs finden Sie unter [drahtlosen Zugriff Bereitstellungsplanung](d-wireless-access-planning.md).
