---
title: Übersicht über die Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Networking Guide "Deploy Password-Based 802.1 X Authenticated Wireless Access"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 29ae0f54-f045-465a-a08e-5867979345f2
author: shortpatti
ms.author: pashort
ms.openlocfilehash: 6658c4750ba2f71b24acd4f7da02029da63179bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818921"
---
# <a name="wireless-access-deployment-overview"></a>Übersicht über die Bereitstellung des Funkzugriffs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgende Abbildung zeigt die Komponenten, die erforderlich sind, zum Bereitstellen von 802.1 X-Drahtloszugriff mit PEAP\-MS\-CHAP-v2.  

![Übersicht über die Bereitstellung-Infrastruktur mit 802.1X-Authentifizierung](../../../media/8021X-Deploy-Overview/8021X-Deploy-Overview.jpg)

## <a name="wireless-access-deployment-components"></a>Bereitstellungskomponenten für drahtlosen Zugriff
Die folgende Infrastruktur ist für diese Bereitstellung des funkzugriffs erforderlich:

### <a name="8021x-capable-wireless-access-points"></a>802.1 X\-kann drahtlose Zugriffspunkte
Nachdem die erforderlichen Netzwerk-Infrastrukturdienste, die Unterstützung von Ihrem drahtlosen lokalen Netzwerks vorhanden sind, können Sie den Entwurfsprozess für den Speicherort der drahtlosen Zugriffspunkte beginnen. Der Entwurfsprozess der drahtlose AP-Bereitstellung umfasst die folgenden Schritte aus:

- Identifizieren Sie die Bereiche der Abdeckung für Mobiltelefone. Bestimmen Sie identifizieren die Bereiche der Abdeckung, um festzustellen, ob der Dienst für drahtlose außerhalb des Gebäudes bieten möchten Sie sicher sein, und wenn Ja, genau, in dem die externen Bereiche.

- Bestimmen, wie viele Drahtloszugriffspunkten, um sicherzustellen, dass ausreichende Abdeckung bereitstellen.

- Bestimmen des Installationsorts für die drahtlosen Zugriffspunkte zu platzieren.

- Wählen Sie die Häufigkeit der Kanal für drahtlose APs.

### <a name="active-directory-domain-services"></a>Active Directory Domain Services
Die folgenden Elemente von AD DS sind für die Bereitstellung des funkzugriffs erforderlich.

#### <a name="users-and-computers"></a>Benutzer und-Computer

Verwenden Sie Active Directory-Benutzer und Computer ausrichten\-in zum Erstellen und Verwalten von Benutzerkonten, und klicken Sie auf eine drahtlose Sicherheitsgruppe zu erstellen, der jedes Mitglied der Domäne enthält, an den drahtlosen Zugriff zu gewähren.

#### <a name="wireless-network-ieee-80211-policies"></a>Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien

Sie können sich auf dem Drahtlosnetzwerk \(IEEE 802.11\) richtlinienerweiterung der Gruppenrichtlinien-Verwaltungskonsole zum Konfigurieren von Richtlinien, die an drahtlose Computer angewendet werden, wenn sie versuchen, auf das Netzwerk zugreifen.

Im Gruppenrichtlinienverwaltungs-Editor, wenn Sie nach rechts\-klicken Sie auf **Drahtlosnetzwerk \(IEEE 802.11\) Richtlinien**, Sie haben die folgenden zwei Optionen für den Typ der Richtlinie für Drahtlosnetzwerke, die Sie erstellen.

- **Erstellen Sie eine neue Richtlinie für Drahtlosnetzwerke für Windows Vista und spätere Versionen**

- **Erstellen einer neuen Windows XP-Richtlinie**

>[!TIP]
>Wenn Sie eine neue Richtlinie für Drahtlosnetzwerke zu konfigurieren, müssen Sie die Möglichkeit, den Namen und eine Beschreibung der Richtlinie zu ändern. Wenn Sie den Namen der Richtlinie ändern, wird die Änderung übernommen, der **Details** Bereich des Gruppenrichtlinienverwaltungs-Editor und in der Titelleiste des Dialogfelds Drahtlosnetzwerk-Richtlinie. Unabhängig davon, wie Sie Ihre Richtlinien umbenennen, die neue XP-Drahtlosnetzwerkrichtlinie stets aufgelistet in Gruppenrichtlinienverwaltungs-Editor mit der **Typ** anzeigen **XP**. Andere Richtlinien sind aufgeführt, mit der **Typ** mit **Vista und neuere Versionen**.  

Das Wireless Network Policy für Windows Vista und neuere Versionen können Sie konfigurieren, zu priorisieren und verwalten mehrere WLAN-Profilen. Ein drahtloses Profil ist eine Auflistung von Konnektivitäts- und Sicherheitseinstellungen, die für die Verbindung mit einem bestimmten drahtlosen Netzwerk verwendet werden. Wenn Gruppenrichtlinien auf Ihren drahtlosen Client-Computern aktualisiert wird, werden die Profile, die Sie in der Drahtlosnetzwerkrichtlinie erstellen automatisch an der Konfiguration auf Ihren drahtlosen Client-Computern hinzugefügt, der Drahtlosnetzwerkrichtlinie gilt.

##### <a name="allowing-connections-to-multiple-wireless-networks"></a>Zulassen von Verbindungen mit mehreren drahtlosen Netzwerken

Wenn Sie drahtlose Clients, die verschiedene physische Standorte in Ihrer Organisation verschoben werden verfügen, empfiehlt z. B. zwischen hauptniederlassung und eine Filiale, Computer keine Verbindung mit mehr als einem drahtlosen Netzwerk. In diesem Fall können Sie ein Drahtlosprofil konfigurieren, die die spezifischen Konnektivität und Sicherheit der Einstellungen für jedes Netzwerk enthält.

Nehmen wir beispielsweise an, die Ihr Unternehmen verfügt über ein drahtloses Netzwerk für die wichtigsten Unternehmenszentrale mit einem Service Set Identifier \(SSID\) WlanCorp.

Die Zweigstelle verfügt auch über ein drahtloses Netzwerk, das Sie auch eine Verbindung herstellen möchten. Die Zweigstelle hat die SSID als WlanBranch konfiguriert.

In diesem Szenario können Sie konfigurieren, ein Profil für jedes Netzwerk, und Computer oder andere Geräte, die in beiden der Unternehmenszentrale verwendet werden, und Filiale kann auf die drahtlosen Netzwerke verbinden, wenn sie physisch im Bereich der Bereich des Netzwerks sind.

##### <a name="mixed-mode-wireless-networks"></a>Gemischte\-Modus drahtlosen Netzwerken

Alternativ können Sie davon ausgehen Sie, dass Ihr Netzwerk sind eine Mischung von wireless-Computer und Geräte, die verschiedene Sicherheitsstandards zu unterstützen. Vielleicht haben einige ältere Computer Drahtlosadapter, mit denen nur WPA können\-Enterprise, während neuere Geräte, die eine stärkere WPA2 verwenden können\-Enterprise-Standard.

Sie können zwei verschiedene Profile erstellen, die die gleiche SSID und die nahezu identische Einstellungen für Konnektivität und Sicherheit zu verwenden.

Sie können die Drahtlosauthentifizierung WPA2 festlegen, in einem Profil\-Enterprise mit AES und dem anderen Profil können Sie angeben, dass WPA\-Enterprise und TKIP.

Dies wird auch bezeichnet als eine gemischte\-im Modus für Bereitstellungen, und sie können Sie Computer unterschiedliche Typen und wireless-Funktionen auf das gleiche drahtlose Netzwerk freigeben.

### <a name="network-policy-server-nps"></a>Netzwerkrichtlinienserver \(NPS\)
NPS ermöglicht Ihnen das Erstellen und Durchsetzen von Netzwerkzugriffsrichtlinien für die Anforderung von Verbindungsauthentifizierung und Autorisierung.

Wenn Sie NPS als RADIUS-Server verwenden, konfigurieren Sie Netzwerkzugriffsserver, z. B. drahtlose Zugriffspunkte als RADIUS-Clients in NPS. Außerdem konfigurieren Sie die Netzwerkrichtlinien, die NPS verwendet, um auf Clients zu authentifizieren und autorisieren die eigenen verbindungsanforderungen an.  

### <a name="wireless-client-computers"></a>Drahtlose Clientcomputer
In diesem Handbuch sind drahtlose Clientcomputer, Computer und andere Geräte verfügen, die über Adapter für IEEE 802.11-Drahtlosnetzwerke und Windows-Client oder Windows Server-Betriebssysteme ausgeführt werden.

#### <a name="server-computers-as-wireless-clients"></a>Server-Computer als drahtlose clients

Standardmäßig ist die Funktionalität für drahtlose 802.11 auf Computern deaktiviert, die Windows Server ausgeführt werden.

Um drahtlose Verbindungen auf Computern mit Serverbetriebssystemen zu aktivieren, müssen Sie installieren und aktivieren Sie die w-LAN \(WLAN\) mithilfe von Windows PowerShell oder das Hinzufügen von Rollen und Features-Assistenten in Server-Service-Funktion -Manager.

Bei der Installation der **WLAN-Dienst** Features des neuen Diensts **WLAN-Autokonfigurationsdienst** ist installiert **Services**. Wenn die Installation abgeschlossen ist, müssen Sie den Server neu starten.

Nach dem Neustart des Servers, können Sie WLAN-Autokonfigurationsdienst zugreifen, wenn Sie auf **starten**, **Windows-Verwaltung**, und **Services**.

Nach der Installation und Server neu zu starten, der Dienst befindet sich im Status "beendet" als Starttyp des WLAN-Autokonfigurationsdienst **automatische**. Um den Dienst zu starten, doppelklicken Sie auf **WLAN-Autokonfigurationsdienst**. Auf der **allgemeine** auf **starten**, und klicken Sie dann auf **OK**.

Der WLAN-Autokonfigurationsdienst listet Drahtlosadapter und verwaltet werden, sowohl für drahtlose Verbindungen als auch für das WLAN-Profilen, die Einstellungen enthalten, die für die Serverkonfiguration für die Verbindung mit einem drahtlosen Netzwerk erforderlich sind.

Einen Überblick über die Bereitstellung des funkzugriffs, finden Sie unter [drahtlosen Zugriff Bereitstellungsprozess](c-wireless-access-deploy-process.md).
