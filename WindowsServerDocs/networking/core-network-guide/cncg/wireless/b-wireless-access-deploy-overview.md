---
title: Übersicht über die Bereitstellung von drahtlosen Zugriff
description: In diesem Thema ist Teil des Windows Server 2016 Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 29ae0f54-f045-465a-a08e-5867979345f2
author: shortpatti
ms.author: pashort
ms.openlocfilehash: 11d87254d8819606a06acedd407bb2e09a45cb60
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment-overview"></a>Übersicht über die Bereitstellung von drahtlosen Zugriff

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die folgende Abbildung zeigt, dass die Komponenten, die erforderlich sind, zum Bereitstellen von 802.1 X drahtlosen Zugriff mit PEAP\-MS\-CHAP v2 authentifiziert.  

![802. 1 x-Infrastruktur Übersicht über die Bereitstellung](../../../media/8021X-Deploy-Overview/8021X-Deploy-Overview.jpg)

## <a name="wireless-access-deployment-components"></a>Bereitstellungskomponenten für drahtlosen Zugriff
Die folgende Infrastruktur ist für die Bereitstellung von 802.1X-Drahtloszugriff erforderlich:

### <a name="8021x-capable-wireless-access-points"></a>802.1X\-fähigen Drahtloszugriffspunkten
Nach der erforderlichen Infrastruktur Netzwerkdiensten wireless LAN vorhanden sind, können Sie den Entwurfsprozess für den Speicherort der drahtlosen Zugriffspunkte beginnen. Der drahtlose Zugriffspunkt Design Bereitstellungsprozess umfasst die folgenden Schritte:

- Identifizieren Sie die Bereiche der Abdeckung für Mobiltelefone. Während identifizieren die Bereiche der Abdeckung, müssen Sie herausfinden, ob Sie Drahtlosdienst außerhalb des Gebäudes bereitstellen möchten, und wenn dies der Fall ist, bestimmen Sie speziell, wo sich diese externen Bereiche befinden.

- Bestimmen, wie viele drahtlose Zugriffspunkte bereitgestellt, um angemessenen erfassungsrahmen sicherzustellen.

- Bestimmen des Installationsorts für die drahtlosen Zugriffspunkte platziert.

- Wählen Sie die Kanalfrequenzen für drahtlose Zugriffspunkte.

### <a name="active-directory-domain-services"></a>Active Directory-Domänendienste
Die folgenden Elemente der AD DS sind für die Bereitstellung von 802.1X-Drahtloszugriff erforderlich.

#### <a name="users-and-computers"></a>Benutzer und-Computer

Verwenden Sie die Active Directory-Benutzer und -Computer-Snap-in erstellen und Verwalten von Benutzerkonten und eine drahtlosen Sicherheitsgruppe zu erstellen, die jedes Mitglied der Domäne enthält, der Sie drahtlosen Zugriff gewähren möchten.

#### <a name="wireless-network-ieee-80211-policies"></a>Drahtloses Netzwerk \ (IEEE 802.11\) Richtlinien

Sie können das Drahtlosnetzwerk \ (IEEE 802.11\) Erweiterung der Gruppenrichtlinien-Verwaltungskonsole zum Konfigurieren von Richtlinien, die auf drahtlose Computer angewendet werden, wenn sie versuchen, auf das Netzwerk zugreifen.

Im Gruppenrichtlinienverwaltungs-Editor, wenn Sie mit der rechten Maustaste auf **Drahtlosnetzwerk \ (IEEE 802.11\) Richtlinien**, Sie haben die folgenden beiden Optionen für den Typ der Richtlinie für drahtlose Netzwerke, die Sie erstellen.

- **Erstellen einer neuen Drahtlosnetzwerkrichtlinie für windowsvista und späteren Versionen**

- **Erstellen einer neuen Windows XP-Richtlinie**

>[!TIP]
>Wenn Sie eine neue Drahtlosnetzwerkrichtlinie zu konfigurieren, müssen Sie die Möglichkeit, den Namen und die Beschreibung der Richtlinie ändern. Wenn Sie den Namen der Richtlinie ändern, wird die Änderung der **Details** Bereich des Gruppenrichtlinienverwaltungs-Editor und in der Titelleiste des Dialogfelds Drahtlosnetzwerk-Richtlinie. Unabhängig davon, wie Sie Ihre Richtlinien umbenennen, der neue XP-Drahtlosnetzwerkrichtlinie immer erscheint im Gruppenrichtlinienverwaltungs-Editor mit der **Typ** anzeigen **XP**. Sind andere Richtlinien aufgeführt, mit der **Typ** mit **Vista und neuere Versionen**.  

Das drahtlose Netzwerk-Richtlinie für Windows Vista und neuere Versionen können Sie konfigurieren, priorisieren und verwalten mehrere WLAN-Profilen. Ein Drahtlosprofil ist eine Sammlung der Konnektivität und Sicherheitseinstellungen, die für die Verbindung mit einem bestimmten Drahtlosnetzwerk verwendet werden. Bei der Aktualisierung der Gruppenrichtlinie auf Ihren drahtlosen Client-Computern werden die Profile, die Sie der Drahtlosnetzwerkrichtlinie erstellen der Konfiguration auf Ihren drahtlosen Client-Computern automatisch hinzugefügt, die der Drahtlosnetzwerkrichtlinie gilt.

##### <a name="allowing-connections-to-multiple-wireless-networks"></a>Zulassen von Verbindungen zu mehreren Drahtlosnetzwerken

Wenn Sie drahtlose Clients, die über physischen Standorte in Ihrer Organisation verschoben werden verfügen, empfiehlt z. B. zwischen zentrale und einer Filiale Computer keine Verbindung mit mehr als ein Drahtlosnetzwerk. In diesem Fall können Sie ein Drahtlosprofil konfigurieren, die die spezifischen Konnektivität und Sicherheit der Einstellungen für jedes Netzwerk enthält.

Nehmen wir beispielsweise an, die Ihr Unternehmen verfügt über ein drahtloses Netzwerk für die wichtigsten Unternehmenszentrale mit Service Set Identifier \(SSID\) WlanCorp.

Die Zweigstelle verfügt auch über ein drahtloses Netzwerk, das Sie auch eine Verbindung herstellen möchten. Der Filiale verfügt über die SSID, die als WlanBranch konfiguriert.

In diesem Szenario können Sie konfigurieren Sie ein Profil für jedes Netzwerk und Computern oder anderen Geräten, die sowohl der Unternehmenszentrale verwendet werden, und Filiale kann entweder von drahtlosen Netzwerken verbinden, wenn sie sich physisch in Reichweite der Reichweite des Netzwerks sind.

##### <a name="mixed-mode-wireless-networks"></a>Drahtlosnetzwerke Mixed\-Modus

Alternativ wird davon ausgegangen Sie, dass Ihr Netzwerk verfügt über eine Mischung aus wireless-Computer und Geräte, die unterschiedliche Sicherheitsstandards unterstützen. Einige ältere Computer verfügen vielleicht Drahtlosadapter, die nur WPA\-Unternehmen, verwenden können, während die neuere Geräte den sichereren WPA2\-Enterprise-Standard verwenden können.

Sie können zwei verschiedene Profile erstellen, die die gleiche SSID und nahezu identische Konnektivität und Sicherheit-Einstellungen verwenden.

In einem Profil können Sie die WLAN-Authentifizierung auf WPA2\-Enterprise mit AES festlegen, und Sie können WPA\ Enterprise mit TKIP angeben, in dem anderen Profil.

Dies wird auch als Bereitstellung Mixed\-Modus bezeichnet, und Computer unterschiedliche Typen und wireless-Funktionen im selben drahtlose Netzwerk gemeinsam nutzen können.

### <a name="network-policy-server-nps"></a>Network Policy Server \(NPS\)
NPS ermöglicht Ihnen das Erstellen und Durchsetzen von Netzwerkzugriffsrichtlinien für die Anforderung Verbindungsauthentifizierung und Autorisierung.

Wenn Sie NPS als RADIUS-Server verwenden, konfigurieren Sie Netzwerkzugriffsserver, z. B. drahtlose Zugriffspunkte als RADIUS-Clients in NPS. Außerdem konfigurieren Sie die Netzwerkrichtlinien, mit denen NPS auf Clients zu authentifizieren und ihre verbindungsanforderungen zu autorisieren.  

### <a name="wireless-client-computers"></a>Drahtlose Clientcomputer
In diesem Leitfaden sind drahtlose Clientcomputer, auf Computern und anderen Geräten, die mit drahtlosen IEEE 802.11-Netzwerkadaptern ausgestattet sind, und Windows-Client oder Windows Server-Betriebssysteme ausgeführt werden.

#### <a name="server-computers-as-wireless-clients"></a>Server-Computer als drahtlose clients

Standardmäßig ist die Funktionalität für drahtlose 802.11 auf Computern deaktiviert, die Windows Server ausgeführt werden.

Um drahtlose Konnektivität auf Computern mit Server-Betriebssysteme aktivieren, müssen Sie installieren und aktivieren Sie die \(WLAN\) Drahtlos-LAN-Dienst-Features mithilfe von Windows PowerShell oder das Hinzufügen von Rollen und Features Assistenten im Server-Manager.

Bei der Installation der **WLAN-Dienst** Features, die den neuen Dienst **WLAN-Autokonfigurationsdienst** installiert **Dienste**. Nach Abschluss der Installation müssen Sie den Server neu starten.

Nach dem Neustart des Servers können Sie WLAN-Autokonfigurationsdienst zugreifen, wenn Sie auf **starten**, **Windows-Verwaltungsprogramme**, und **Dienste**.

Nach der Installation und Server neu zu starten, den Dienst befindet sich im Status "beendet" mit dem Starttyp der WLAN-Autokonfigurationsdienst **automatische**. Um den Dienst zu starten, doppelklicken Sie auf **WLAN-Autokonfigurationsdienst**. Auf der **allgemeine** auf **starten**, und klicken Sie dann auf **OK**.

Der WLAN-Autokonfigurationsdienst listet Drahtlosadapter und verwaltet drahtlose Verbindungen und der WLAN-Profilen, die Einstellungen enthalten, die zum Konfigurieren des Servers für die Verbindung mit einem drahtlosen Netzwerk erforderlich sind.

Einen Überblick über die Bereitstellung des funkzugriffs finden Sie unter [Wireless Access-Bereitstellungsprozess](c-wireless-access-deploy-process.md).
