---
title: Entfernte oder veraltete künftigen Windows Server 2019 Features
description: Informationen Sie zu den Features und Funktionen entfernte oder veraltete entfernen, beginnend mit Windows Server 2019.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: jasgro
ms.date: 03/29/2019
ms.localizationpriority: medium
ms.openlocfilehash: 470857616a9b36d238de031b4ccf80a68eff1e61
ms.sourcegitcommit: 971f6538e8d89af84ef50fc8aab2188bdf6f47cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2019
ms.locfileid: "9279131"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>Entfernte oder veraltete Windows Server 2019 Features

>Gilt für: Windows Server2019

Jede Version von Windows Server fügt die neuen Features und Funktionen; wir auch gelegentlich entfernen, Features und Funktionen, in der Regel, da wir eine bessere Option hinzugefügt haben. Hier sind Details zu den Features und Funktionen, die wir in Windows Server 2019 entfernt.   

> [!TIP]
> - Sie können den frühen Zugriff auf Windows Server-Builds abrufen, indem Sie am [Windows-Insider-Programm](https://insider.windows.com) teilnehmen. Dies ist eine hervorragende Möglichkeit zum Testen der geänderten Features.
> - Haben Sie Fragen zu anderen Versionen? Sehen Sie sich die Informationen für [Windows Server, Version 1803](../get-started/windows-server-1803-removed-features.md), [Windows Server, Version 1709](../get-started/removed-features-1709.md)und [Windows Server 2016](../get-started/deprecated-features.md).

**Die Liste ist Änderungen vorbehalten. Zudem enthält sie möglicherweise nicht alle veralteten Features oder Funktionen.** 

## <a name="features-we-removed-in-this-release"></a>In dieser Version entfernte Features

Wir haben die folgenden Features und Funktionen aus dem installierten Produktbild in Windows Server 2019 entfernen. Anwendungen oder Code, der von diesen Features abhängt, funktioniert in dieser Version nicht, se sei denn, Sie verwenden eine alternative Methode.   

|Funktion    |Stattdessen können Sie...|
|-----------|--------------------
|Business-Überprüfung, auch Verwaltung verteilter Scanvorgänge (DSM) genannt|Wir diese scanverwaltungsfunktionen und Scanner-Management-Funktionen entfernen – es gibt keine Geräte, die dieses Feature unterstützen.|
|Drucken Sie Komponenten - jetzt optionale Komponente für Server Core-Installationen|In früheren Versionen von Windows Server wurden die Drucken-Komponenten in der Server Core-Installationsoption standardmäßig *deaktiviert* . Wir geändert, die in Windows Server 2016 standardmäßig aktivieren. In Windows Server 2019 sind diese drucken Komponenten wieder für Server Core standardmäßig deaktiviert. Wenn Sie die Drucken-Komponenten aktivieren möchten, können Sie dies tun, durch Ausführen des **Druck-Installation-WindowsFeature-Server** -Cmdlet.|
|[Remotedesktopverbindung-Broker und Remotedesktop-Virtualisierungshost](../remote/remote-desktop-services/desktop-hosting-service.md) in einer Server Core-Installation|Die meisten Remotedesktopverbindungsbereitstellungen erfüllen diese Rollen am selben Standort mit den Remotedesktop-Sitzungshost (RDSH), für den Server mit Desktopdarstellung erforderlich sind. Um mit RDSH konsistent zu bleiben, ändern wir die Rollen, die Server mit Desktopdarstellung erfordern. Diese RDS-Rollen sind nicht mehr für die Verwendung in einer [Server Core-Installation](../administration/server-core/what-is-server-core.md)verfügbar. Wenn Sie [diese Funktionen als Teil der Remotedesktop-Infrastruktur](../remote/remote-desktop-services/rds-deploy-infrastructure.md)bereitstellen müssen, können Sie [diese auf Windows Server mit Desktopdarstellung installieren](../get-started/getting-started-with-server-with-desktop-experience.md). <br/><br/>Diese Rollen sind auch in die Desktop Experience-Installationsoption von Windows Server 2019 enthalten. |



## <a name="features-were-no-longer-developing"></a>Features, die nicht mehr entwickelt werden

Wir diese Features sind nicht mehr aktiv entwickeln und sie von zukünftigen Aktualisierungen entfernen. Einige Features wurden mit anderen Features oder Funktionen ersetzt, während andere aus verschiedenen Quellen jetzt verfügbar sind. 

Wenn Sie Feedback zu der vorgeschlagenen Austausch diese Features haben, können Sie die [app Feedback-Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)verwenden. 

|Funktion    |Stattdessen können Sie...|
|-----------|---------------------|
|Wichtige Speicherlaufwerk in Hyper-V|Wir arbeiten nicht mehr auf das Feature Schlüssel Speicherlaufwerk in Hyper-V. Wenn Sie die virtuellen Computer der 1. Generation verwenden, sehen Sie sich [Der Generation 1 VM-Virtualisierungssicherheit](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v) Informationen zu den Optionen, die Zukunft. Wenn Sie erstellen, verwenden neue virtuelle Computer der Generation 2 virtuelle Computer mit TPM-Geräte für eine sicherere Lösung. |
|Trusted Platform Module (TPM)-Verwaltungskonsole|Die Informationen, die zuvor verfügbar in der TPM-Verwaltungskonsole ist jetzt auf der Seite " [**Device Security**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) " in der [Windows Defender Security Center](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)verfügbar.|
|Host Guardian Service Active Directory Attestation Modus|Wir entwickeln nicht mehr Host Guardian Service Active Directory Attestation-Modus – wir haben einen neuen Attestation-Modus, [Host den schlüsselnachweis nutzen](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md), die sehr viel einfacher und gleichermaßen als kompatibel, wie Active Directory Attestation basierte stattdessen hinzugefügt.  Dieser neue Modus bietet gleichwertige Funktion mit einem-Setupprogramm, einfachere Verwaltung und weniger infrastrukturabhängigkeiten als der Active Directory-Nachweis. Host-schlüsselnachweis hat keine zusätzlichen hardwareanforderungen für über was ActiveDirectory-Nachweis erforderlich, damit alle vorhandene Systemen mit den neuen Modus kompatibel bleibt. Weitere Informationen zu den integritätsnachweis-Optionen finden Sie in der [Bereitstellen geschützten Hosts](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md) .|
|OneSync-Dienst|Der Dienst OneSync synchronisiert die Daten für die apps Mail, Kalender und Kontakte. Wir haben ein Synchronisierungsmodul Outlook app hinzugefügt, die die gleiche Synchronisierung bereitstellt.|
|Remote Differential Compression API-Unterstützung|Remote Differential Compression API-Unterstützung aktiviert das Synchronisieren von Daten mit einer Remotequelle mithilfe von Komprimierung-Technologien, die die Menge an Daten, die über das Netzwerk gesendet minimiert. Diese Unterstützung wird derzeit nicht von beliebigen Microsoft-Produkts verwendet.|
|Windows-Dateischutz einfache Filter Switch-Erweiterung|Die Windows-Dateischutz einfache Filter Switch-Erweiterung ermöglicht Entwicklern das [einfache Netzwerk Paket Filterplattform Erweiterungen für Hyper-V virtual switch](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering)erstellen kann. Sie können die gleiche Funktionalität durch Erstellen einer vollständigen Filterplattform-Erweiterungs erzielen. Daher werden wir diese Erweiterung in Zukunft entfernen.|

