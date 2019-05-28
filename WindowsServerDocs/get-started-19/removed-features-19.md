---
title: Funktionen, die entfernt oder sollen in Windows Server-2019
description: Informationen Sie zu den Features und Funktionen entfernt oder entfernen, die ab Windows Server-2019.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: jasongerend
ms.author: jgerend
manager: jasgro
ms.date: 05/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 820dfed8a0a58d3ccc64023325c373b761461ba8
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2019
ms.locfileid: "65976524"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>Funktionen, die entfernt oder ersetzt, die ab Windows Server-2019

>Gilt für: Windows Server 2019

Jede Version von Windows Server fügt die neuen Features und Funktionen; wir auch gelegentlich entfernen, Features und Funktionen, in der Regel, da wir eine bessere Option hinzugefügt haben. Hier sind die Details zu Features und Funktionen, die wir in Windows Server-2019 entfernt.

> [!TIP]
> - Sie können den frühen Zugriff auf Windows Server-Builds abrufen, indem Sie am [Windows-Insider-Programm](https://insider.windows.com) teilnehmen. Dies ist eine hervorragende Möglichkeit zum Testen der geänderten Features.
> - Haben Sie Fragen zu anderen Versionen? Lesen Sie die Informationen für [Neuigkeiten in Windows Server](../get-started/whats-new-in-windows-server.md).

**Die Liste kann geändert und enthalten möglicherweise nicht alle betroffenen Features oder Funktionen.** 

## <a name="features-we-removed-in-this-release"></a>In dieser Version entfernte Features

Wir haben die folgenden Features und Funktionen aus dem installierten Produkt-Image in Windows Server-2019 entfernen. Anwendungen oder Code, der von diesen Features abhängt, funktioniert in dieser Version nicht, se sei denn, Sie verwenden eine alternative Methode.

|Feature    |Stattdessen können Sie...|
|-----------|--------------------
|Business-Überprüfung, auch Verwaltung verteilter Scanvorgänge (DSM) genannt|Dieser sichere Überprüfung und Verwaltungsfunktionen für die Überprüfung entfernen wir sind – es sind keine Geräte, die dieses Feature zu unterstützen.|
|Drucken von Komponenten – jetzt optionale Komponente für Server Core-Installationen|In früheren Versionen von Windows Server, der die Drucken Komponenten waren *deaktiviert* standardmäßig in der Server Core-Installationsoption. Wir, die in Windows Server 2016, sodass sie in der Standardeinstellung geändert. In Windows Server-2019 sind diese Komponenten drucken erneut für Server Core standardmäßig deaktiviert. Wenn Sie die print-Komponenten aktivieren möchten, erreichen Sie dies durch Ausführen der **Install-WindowsFeature-Druckserver** Cmdlet.|
|[Remotedesktopverbindung-Broker und Remotedesktop-Virtualisierungshost](../remote/remote-desktop-services/desktop-hosting-service.md) in einer Server Core-Installation|Die meisten Remotedesktopverbindungsbereitstellungen erfüllen diese Rollen am selben Standort mit den Remotedesktop-Sitzungshost (RDSH), für den Server mit Desktopdarstellung erforderlich sind. Um mit RDSH konsistent zu bleiben, ändern wir die Rollen, die Server mit Desktopdarstellung erfordern. Diese RDS-Rollen sind nicht mehr verfügbar ist, für die Verwendung in einer [Server Core-Installation](../administration/server-core/what-is-server-core.md). Bei Bedarf [diese Rollen als Teil Ihrer per Remotedesktop-Infrastruktur bereitstellen](../remote/remote-desktop-services/rds-deploy-infrastructure.md), können Sie [auf Windows Server mit Desktopdarstellung installieren](../get-started/getting-started-with-server-with-desktop-experience.md). <br/><br/>Diese Rollen sind auch in die Desktop Experience-Installationsoption von Windows Server 2019 enthalten. |

## <a name="features-were-no-longer-developing"></a>Features, die nicht mehr entwickelt werden

Wir entwickeln diese Funktionen nicht mehr aktiv und kann von einem zukünftigen Update entfernen. Einige Features wurden mit anderen Features oder Funktionen ersetzt, während andere aus verschiedenen Quellen jetzt verfügbar sind. 

Wenn Sie Feedback zu der vorgeschlagenen Austausch diese Features haben, können Sie die [app Feedback-Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)verwenden. 

| Feature   | Stattdessen können Sie... |
|-----------|---------------------|
| Wichtige Speicherlaufwerk in Hyper-V|Wir arbeiten jedoch nicht mehr auf die Schlüssel Speicherlaufwerk-Funktion in Hyper-V. Wenn Sie VMs der Generation 1 verwenden, sehen Sie sich [Generation 1 VM Virtualisierungssicherheit](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v) Informationen zu Optionen, die in Zukunft. Wenn Sie neue virtuelle Computer verwenden virtuelle Maschinen der Generation 2 mit TPM-Geräten für eine sicherere Lösung erstellen. |
| Vertrauenswürdige Platform Module (TPM)-Verwaltungskonsole|Die Informationen, die zuvor in der TPM-Verwaltungskonsole zur Verfügung steht jetzt auf die [ **gerätesicherheit** ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) auf der Seite die [Windows Defender Security Center](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center). |
| Host Guardian Service Active Directory-nachweismodus|Wir nicht mehr Host Guardian Service, Active Directory-nachweismodus entwickeln: Wir haben stattdessen eine neue nachweismodus, hinzugefügt [hosten den schlüsselnachweis](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md), ist wesentlich einfacher und ebenso als kompatibel ist, als Active Directory-Basis einen Nachweis an.  Dieser neue Modus stellt die entsprechenden Funktionalität mit einer Setupfunktionalität, einfachere Verwaltung und weniger infrastrukturabhängigkeiten als den Nachweis der Active Directory bereit. Host-schlüsselnachweis hat bestehen keine zusätzlichen hardwareanforderungen, über welche Active Directory-Nachweis erforderlich, damit alle vorhandenen Systeme mit den neuen Modus kompatibel bleiben. Finden Sie unter [Bereitstellen von überwachten Hosts](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md) für Weitere Informationen zu den Nachweis-Optionen. |
| OneSync-Dienst|Der Dienst OneSync synchronisiert die Daten für die E-Mail, Kalender und Benutzer-apps. Wir haben die Outlook-app eine Synchronisierungs-Engine hinzugefügt, die die gleiche Synchronisierung bereitstellt. |
| Remote Differential Compression-API-Unterstützung|Remote Differential Compression-API-Unterstützung aktiviert die Synchronisierung von Daten mit einer Remotequelle mit komprimierungstechnologien, die die über das Netzwerk übertragene Datenmenge minimiert. Diese Unterstützung ist nicht aktuell von Microsoft-Produkten verwendet werden. |
| WFP-Erweiterung für einfachen Filter-Switches|Die WFP-Erweiterung für die einfache Filter Switches ermöglicht Entwicklern das Erstellen von [einfaches Netzwerk paketfilterung-Erweiterungen für den virtuellen Hyper-V-Switch](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering). Sie können die gleiche Funktionalität erreichen, durch das Erstellen einer vollständigen filternden-Erweiterungs. Daher müssen wir diese Erweiterung in der Zukunft entfernt. |