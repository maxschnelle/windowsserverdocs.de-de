---
title: Entfernte oder zur Entfernung vorgesehene Features in Windows Server 2019
description: Erfahren Sie mehr über die entfernten oder zur Entfernung vorgesehenen Features ab Windows Server 2019.
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
ms.date: 08/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0f6b6ac42c096c6c80404c2d650905e73da8a97a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868650"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>Entfernte oder zur Ersetzung vorgesehene Features in Windows Server 2019

>Gilt für: Windows Server 2019

In jeder Version von Windows Server kommen neue Features und Funktionen hinzu; gelegentlich entfernen wir auch Features und Funktionen, normalerweise, weil wir eine bessere Option hinzugefügt haben. Hier sind Details zu den Features und Funktionen, die wir in Windows Server 2019 entfernt haben.

> [!TIP]
> - Sie können frühzeitig Zugriff auf Windows Server-Builds erhalten, indem Sie am [Windows Insider-Programm](https://insider.windows.com) teilnehmen – das ist eine hervorragende Möglichkeit, Änderungen an Features zu testen.
> - Haben Sie Fragen zu anderen Releases? Weitere Informationen: [Features, die entfernt wurden bzw. deren Ersetzung in Windows Server geplant ist](removed-features.md).

**Änderungen an der Liste sind vorbehalten. Zudem enthält sie möglicherweise nicht alle betroffenen Features oder Funktionen.** 

## <a name="features-we-removed-in-this-release"></a>In dieser Version entfernte Features

Wir haben die folgenden Features und Funktionen aus dem installierten Produktimage von Windows Server 2019 entfernt. Anwendungen oder Code, die von diesen Features abhängen, funktionieren in dieser Version nicht, es sei denn, Sie verwenden eine alternative Methode.

| Feature   | Alternativ verwendbar |
| --------- | -------------------- |
| Business Scanning, auch als Verwaltung verteilter Scanvorgänge (Distributed Scan Management, DSM) bezeichnet|Wir entfernen diese Funktion zur Verwaltung sicherer Scanvorgänge und Scanner – sie wird von keinem Gerät unterstützt. |
| Druckkomponenten: jetzt eine optionale Komponente für Server Core-Installationen|In früheren Versionen von Windows Server waren die Druckkomponenten standardmäßig in der Server Core-Installationsoption *deaktiviert*. Wir haben das in Windows Server 2016 geändert, sie sind jetzt standardmäßig aktiviert. In Windows Server 2019 sind diese Druckkomponenten für Server Core standardmäßig wieder deaktiviert. Wenn Sie die Druckkomponenten aktivieren müssen, können Sie dazu das Cmdlet **Install-WindowsFeature Print-Server** ausführen. |
| [Remotedesktop-Verbindungsbroker und Remotedesktop-Virtualisierungshost](../remote/remote-desktop-services/desktop-hosting-service.md) in einer Server Core-Installation|In den meisten Bereitstellungen von Remotedesktopdiensten sind diese Rollen zusammen mit dem Remotedesktop-Sitzungshost (RDSH), für den Server mit Desktopdarstellung erforderlich ist, auf einem System untergebracht; um Konsistenz mit RDSH zu erreichen, ändern wir diese Rollen so, dass ebenfalls Server mit Desktopdarstellung erforderlich ist. Diese RDS-Rollen stehen in einer [Server Core-Installation](../administration/server-core/what-is-server-core.md) nicht mehr zur Verwendung zur Verfügung. Wenn Sie [diese Rollen als Teil Ihrer Remotedesktop-Infrastruktur bereitstellen](../remote/remote-desktop-services/rds-deploy-infrastructure.md) müssen, können Sie sie auf einem [Windows Server mit Desktopdarstellung installieren](../get-started/getting-started-with-server-with-desktop-experience.md). <br/><br/>Diese Rollen sind darüber hinaus in der Installationsoption mit Desktopdarstellung von Windows Server 2019 enthalten. |

## <a name="features-were-no-longer-developing"></a>Features, die wir nicht mehr weiterentwickeln

Wir entwickeln diese Features nicht mehr aktiv weiter und werden sie möglicherweise aus zukünftigen Updates entfernen. Einige Features wurden durch andere Features oder Funktionen ersetzt, während andere jetzt aus anderen Quellen stammen. 

Wenn Sie Feedback zur vorgeschlagenen Ersetzung eines dieser Features haben, können Sie die [Feedback-Hub-App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) verwenden. 

| Feature     | Alternativ verwendbar |
| ----------- | --------------------- |
| Schlüsselspeicher-Laufwerk in Hyper-V|Wir arbeiten nicht mehr am Schlüsselspeicher-Laufwerkfeature in Hyper-V. Wenn Sie VMs der ersten Generation verwenden, lesen Sie [Generation 1 VM Virtualization Security](../virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v.md) (Virtualisierungssicherheit bei VMs der ersten Generation), um Informationen zu den zukünftigen Optionen zu erhalten. Wenn Sie neue VMs erstellen, verwenden Sie virtuelle Computer der zweiten Generation mit TPM-Geräten, die eine sicherere Lösung darstellen. |
| TPM-Verwaltungskonsole (Trusted Platform Module)|Die bisher in der TPM-Verwaltungskonsole verfügbaren Informationen stehen jetzt auf der Seite [**Gerätesicherheit**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) im [Windows Defender Security Center](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center) zur Verfügung. |
| Active Directory-Nachweismodus des Host-Überwachungsdiensts|Wir entwickeln den Active Directory-Nachweismodus des Host-Überwachungsdiensts nicht mehr weiter – stattdessen haben wir einen neuen Nachweismodus eingeführt, [Hostschlüsselnachweis](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md), der viel einfacher und genauso kompatibel wie der Active Directory-basierte Nachweis ist.  Dieser neue Modus bietet die gleiche Funktionalität mit einer Setupoberfläche, einfacherer Verwaltung und weniger Infrastrukturabhängigkeiten als der Active Directory-Nachweis. Für den Hostschlüsselnachweis bestehen keine zusätzlichen Hardwareanforderungen über das hinaus, was für den Active Directory-Nachweis erforderlich war, daher bleiben alle vorhandenen Systeme mit dem neuen Modus kompatibel. Weitere Informationen über bestehende Nachweisoptionen finden Sie unter [Bereitstellen geschützter Hosts](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md). |
| OneSync-Dienst | Der OneSync-Dienst synchronisiert Daten für die E-Mail-, Kalender- und Kontakte-Apps. Wir haben der Outlook-App ein Synchronisierungsmodul hinzugefügt, das die gleiche Synchronisierung leistet. |
| Remotedifferenzialkomprimierungs-API-Unterstützung | Die Unterstützung für die Remotedifferenzialkomprimierungs-API ermöglicht das Synchronisieren von Daten mit einer Remotequelle mithilfe von Komprimierungstechnologien, die die Menge der über das Netzwerk gesendeten Daten minimiert. |
| Schlanke WFP-Filterswitcherweiterung | Die schlanke WFP-Filterswitcherweiterung ermöglicht Entwicklern das Erstellen von [einfachen Netzwerkpaketfilter-Erweiterungen für den virtuellen Hyper-V-Switch](https://docs.microsoft.com/windows-hardware/drivers/network/using-virtual-switch-filtering). Sie können die gleiche Funktionalität erreichen, indem Sie eine vollständige Filtererweiterung erstellen. Daher werden wir diese Erweiterung in Zukunft entfernen. |
