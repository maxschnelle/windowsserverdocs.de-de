---
title: Übersicht über die Bereitstellung des Funkzugriffs
description: Dieses Thema ist Teil des Windows Server 2016-Netzwerk Handbuchs "Bereitstellen von Kenn Wort basiertem 802.1 x authentifizierten drahtlosen Zugriff".
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 29ae0f54-f045-465a-a08e-5867979345f2
author: shortpatti
ms.author: pashort
ms.openlocfilehash: 93fb80c550771e4e7d8bc400d647b520b0c67fdf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356085"
---
# <a name="wireless-access-deployment-overview"></a>Übersicht über die Bereitstellung des Funkzugriffs

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In der folgenden Abbildung sind die Komponenten dargestellt, die für die Bereitstellung des drahtlos Zugriffs mit 802.1 x-Authentifizierung mit dem Wert von "Peer-no__t-0ms @ no__t-1chap V2" erforderlich sind.  

![Übersicht der 802.1 x-Bereitstellungs Infrastruktur](../../../media/8021X-Deploy-Overview/8021X-Deploy-Overview.jpg)

## <a name="wireless-access-deployment-components"></a>Bereitstellungs Komponenten für den drahtlos Zugriff
Für diese drahtlos Zugriffs Bereitstellung ist die folgende Infrastruktur erforderlich:

### <a name="8021x-capable-wireless-access-points"></a>802.1 x @ no__t-0fähige drahtlos Zugriffspunkte
Nachdem die erforderlichen Netzwerkinfrastruktur Dienste, die Ihr Drahtlos Netzwerk unterstützen, vorhanden sind, können Sie den Entwurfsprozess für den Speicherort der drahtlos Zugriffspunkte starten. Der Entwurfsprozess für drahtlos Bereitstellungen umfasst die folgenden Schritte:

- Identifizieren Sie die Bereiche der Abdeckung für drahtlose Benutzer. Wenn Sie die Bereiche der Abdeckung identifizieren, achten Sie darauf, dass Sie einen drahtlosen Dienst außerhalb des Aufbaus bereitstellen möchten. wenn dies der Fall ist, legen Sie fest, wo sich diese externen Bereiche befinden.

- Bestimmen Sie, wie viele drahtlos Zugriffspunkte bereitgestellt werden, um eine angemessene Abdeckung sicherzustellen

- Bestimmen Sie, wo drahtlose APS platziert werden sollen.

- Wählen Sie die Kanal Frequenzen für drahtlos Zugriffspunkte aus.

### <a name="active-directory-domain-services"></a>Active Directory Domain Services
Die folgenden Elemente AD DS sind für die Bereitstellung des drahtlos Zugriffs erforderlich.

#### <a name="users-and-computers"></a>Benutzer und Computer

Verwenden Sie den Active Directory Benutzer und Computer Snap @ no__t-0in zum Erstellen und Verwalten von Benutzerkonten sowie zum Erstellen einer drahtlos Sicherheitsgruppe, die die einzelnen Domänen Mitglieder enthält, denen Sie drahtlos Zugriff gewähren möchten.

#### <a name="wireless-network-ieee-80211-policies"></a>Drahtlos Netzwerk \(ieee 802.11 @ no__t-1-Richtlinien

Sie können das Drahtlos Netzwerk \(ieee 802.11 @ no__t-1 Policies-Erweiterung von Gruppenrichtlinie Management verwenden, um Richtlinien zu konfigurieren, die auf drahtlos Computer angewendet werden, wenn Sie versuchen, auf das Netzwerk zuzugreifen.

Wenn Sie in Gruppenrichtlinienverwaltungs-Editor mit der rechten Maustaste @ no__t-0klicken Sie auf **Drahtlos Netzwerk \(ieee 802.11 @ no__t-3-Richtlinien**, stehen Ihnen die folgenden beiden Optionen für den Typ der von Ihnen erstellten drahtlosen Richtlinie zur Anwendung.

- **Neue Richtlinie für Drahtlos Netzwerke für Windows Vista und spätere Releases erstellen**

- **Neue Windows XP-Richtlinie erstellen**

>[!TIP]
>Beim Konfigurieren einer neuen Drahtlos Netzwerk Richtlinie haben Sie die Möglichkeit, den Namen und die Beschreibung der Richtlinie zu ändern. Wenn Sie den Namen der Richtlinie ändern, wird die Änderung im **Detail** Bereich von Gruppenrichtlinienverwaltungs-Editor und auf der Titelleiste des Dialog Felds Drahtlos Netzwerk Richtlinie widergespiegelt. Unabhängig davon, wie Sie Ihre Richtlinien umbenennen, wird die neue drahtlose XP-Richtlinie immer in Gruppenrichtlinienverwaltungs-Editor mit dem **Typ** " **XP**" aufgeführt. Weitere Richtlinien sind mit dem **Typ** , der **Vista und spätere Releases**anzeigt, aufgeführt.  

Die Richtlinie für Drahtlos Netzwerke für Windows Vista und spätere Versionen ermöglicht Ihnen das konfigurieren, priorisieren und Verwalten mehrerer drahtloser Profile. Ein drahtlos Profil ist eine Sammlung von Verbindungs-und Sicherheitseinstellungen, die verwendet werden, um eine Verbindung mit einem bestimmten Drahtlos Netzwerk herzustellen. Wenn Gruppenrichtlinie auf Ihren drahtlosen Client Computern aktualisiert wird, werden die in der Drahtlos Netzwerk Richtlinie erstellten Profile automatisch der Konfiguration auf Ihren drahtlosen Client Computern hinzugefügt, für die die Richtlinie für Drahtlos Netzwerke gilt.

##### <a name="allowing-connections-to-multiple-wireless-networks"></a>Zulassen von Verbindungen mit mehreren Drahtlos Netzwerken

Wenn Sie über drahtlose Clients verfügen, die an physische Standorte in Ihrer Organisation verschoben werden (z. b. zwischen einem Hauptsitz und einer Zweigniederlassung), sollten Sie möchten, dass Computer eine Verbindung mit mehr als einem Drahtlos Netzwerk herstellen. In dieser Situation können Sie ein drahtlos Profil konfigurieren, das die spezifischen Konnektivitätseinstellungen und Sicherheitseinstellungen für jedes Netzwerk enthält.

Nehmen Sie beispielsweise an, dass Ihr Unternehmen über ein drahtloses Netzwerk für die Hauptniederlassung des Unternehmens verfügt und über einen Service Set Identifier \(ssid @ no__t-1 wlancorp verfügt.

Ihre Zweigstelle verfügt auch über ein Drahtlos Netzwerk, mit dem Sie auch eine Verbindung herstellen möchten. Die SSID ist in der Zweigstelle als wlanbranch konfiguriert.

In diesem Szenario können Sie ein Profil für jedes Netzwerk konfigurieren, und Computer oder andere Geräte, die sowohl in der Firmenniederlassung als auch in der Filiale verwendet werden, können eine Verbindung mit einem der Drahtlos Netzwerke herstellen, wenn Sie sich physisch im Bereich der Abdeckung eines Netzwerks befinden.

##### <a name="mixed-mode-wireless-networks"></a>Gemischte @ no__t-0mode-Drahtlos Netzwerke

Angenommen, Ihr Netzwerk verfügt über eine Mischung aus drahtlosen Computern und Geräten, die verschiedene Sicherheitsstandards unterstützen. Möglicherweise haben einige ältere Computer drahtlose Adapter, die nur WPA @ no__t-0enter Prise verwenden können, während neuere Geräte den stärkeren WPA2 @ no__t-1enter Prise Standard verwenden können.

Sie können zwei verschiedene Profile erstellen, die die gleiche SSID und nahezu identische Konnektivitätseinstellungen und Sicherheitseinstellungen verwenden.

In einem Profil können Sie die drahtlose Authentifizierung auf WPA2 @ no__t-0enter Prise mit AES festlegen. im anderen Profil können Sie WPA @ no__t-1enter Prise mit TKIP angeben.

Dies wird häufig als gemischte @ no__t-0mode-Bereitstellung bezeichnet und ermöglicht Computern mit unterschiedlichen Typen und drahtlosen Funktionen das Freigeben desselben drahtlos Netzwerks.

### <a name="network-policy-server-nps"></a>Netzwerk Richtlinien Server-\(nps @ no__t-1
Mithilfe von NPS können Sie Netzwerk Zugriffsrichtlinien für die Authentifizierung und Autorisierung von Verbindungsanforderungen erstellen und erzwingen.

Wenn Sie NPS als RADIUS-Server verwenden, konfigurieren Sie Netzwerk Zugriffs Server, z. b. drahtlos Zugriffspunkte, als RADIUS-Clients in NPS. Außerdem konfigurieren Sie die Netzwerk Richtlinien, die NPS verwendet, um Zugriffs Clients zu authentifizieren und deren Verbindungsanforderungen zu autorisieren.  

### <a name="wireless-client-computers"></a>Drahtlose Client Computer
Im Rahmen dieses Handbuchs sind drahtlose Client Computer Computer und andere Geräte, die mit IEEE 802,11-drahtlos Netzwerkadaptern ausgestattet sind und auf denen Windows-Client-oder Windows Server-Betriebssysteme ausgeführt werden.

#### <a name="server-computers-as-wireless-clients"></a>Server Computer als drahtlose Clients

Standardmäßig ist die Funktionalität für 802,11 Wireless auf Computern, auf denen Windows Server ausgeführt wird, deaktiviert.

Um die drahtlose Konnektivität auf Computern zu ermöglichen, auf denen Server Betriebssysteme ausgeführt werden, müssen Sie das Wireless LAN \(wlan @ no__t-1-Dienst Feature mithilfe von Windows PowerShell oder dem Assistenten zum Hinzufügen von Rollen und Features in Server-Manager installieren und aktivieren.

Wenn Sie das Feature des **Drahtlos-LAN-Diensts** installieren, wird die neue automatische Dienst- **WLAN-Konfiguration** in den- **Diensten**installiert. Wenn die Installation beendet ist, müssen Sie den Server neu starten.

Nachdem der Server neu gestartet wurde, können Sie auf die automatische WLAN-Konfiguration zugreifen, wenn Sie auf **Start**, **Windows-Verwaltungs Tools**und **Dienste**klicken.

Nach der Installation und dem Neustart des Servers befindet sich der Dienst für die automatische WLAN-Konfiguration in einem beendeten Zustand mit dem Starttyp " **automatisch**". Um den Dienst zu starten, doppelklicken Sie auf **WLAN AutoConfig**. Klicken Sie auf der Registerkarte **Allgemein** auf **Start**, und klicken Sie dann auf **OK**.

Der Dienst für die automatische WLAN-Konfiguration listet drahtlose Adapter auf und verwaltet sowohl drahtlos Verbindungen als auch drahtlos Profile, die Einstellungen enthalten, die zum Konfigurieren des Servers für die Verbindung mit einem Drahtlos Netzwerk erforderlich sind.

Einen Überblick über die Bereitstellung des drahtlos Zugriffs finden Sie unter [Bereitstellungs Prozess für drahtlos Zugriff](c-wireless-access-deploy-process.md).
