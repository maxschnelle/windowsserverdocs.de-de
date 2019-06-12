---
title: Unterstützte Konfigurationen für Remote Desktop Services
description: Enthält Informationen zu unterstützten Konfigurationen für Remotedesktopdienste in Windows Server 2016.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 12/20/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c925c7eb-6880-411f-8e59-bd0f57cc5fc3
author: lizap
manager: dongill
ms.openlocfilehash: 8571c2220f804a27e4e1a6b744e8e15e38bd53a3
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453083"
---
# <a name="supported-configurations-for-remote-desktop-services-in-windows-server-2016"></a>Unterstützte Konfigurationen für Remotedesktopdienste in Windows Server 2016

> Gilt für: Windows Server 2016

Wenn es um die unterstützten Konfigurationen für Remote Desktop Services-Umgebungen geht, ist meist das größte Problem Version Interoperabilität. Die meisten Umgebungen sind mehrere Versionen von Windows Server – Sie können z. B. haben eine vorhandene Windows Server 2012 R2 RDS-Bereitstellung aber auf Windows Server 2016 nutzen die neuen Features (z. B. Unterstützung für OpenGL\OpenCL, diskrete Werte aktualisieren möchten Gerätezuordnung, oder "direkte Speicherplätze"). Die Frage, welche RDS-Komponenten mit verschiedenen Versionen arbeiten können und welche identisch sein müssen?

Beachten Sie, sind hier grundlegende Richtlinien für die unterstützten Konfigurationen von Remotedesktopdiensten in Windows Server 2016.

> [!NOTE]
> Überprüfen Sie die [Systemanforderungen für Windows Server 2016](../../get-started/system-requirements.md).

## <a name="best-practices"></a>Empfohlene Methoden
- Verwenden Sie Windows Server 2016 für die Remotedesktop-Infrastruktur – die Web Access-Gateway, Connection Broker und Lizenzserver. Windows Server 2016 ist abwärtskompatibel für diese Komponenten – also ein 2012 R2-RD-Sitzungshost kann mit einem 2016-Remotedesktop-Verbindungsbroker verbinden, aber das Gegenteil nicht trifft.

- Für RD-Sitzungshosts: alle Session Hosts in einer Auflistung auf der gleichen Ebene sein müssen, jedoch können Sie mehrere Sammlungen verfügen. Sie können eine Sammlung mit Windows Server 2012 R2-Sitzungshosts und eine mit Windows Server 2016-Sitzungshosts verwenden.

- Wenn Sie Ihre RD Session Host auf Windows Server 2016 aktualisieren, auch aktualisieren Sie den Lizenzserver. Denken Sie daran, dass ein Lizenz für 2016-Server CALs in allen früheren Versionen von Windows Server, auf Windows Server 2003 verarbeiten kann.

- Führen Sie die Upgrade-Reihenfolge empfohlen [ein Upgrade Ihrer Umgebung Remote Desktop Services](upgrade-to-rds.md#flow-for-deployment-upgrades). 

- Wenn Sie eine hoch verfügbare Umgebung erstellen, müssen alle Ihren Verbindungsbroker der Ebene des gleichen sein.

## <a name="rd-connection-brokers"></a>Remotedesktop-Verbindungsbroker

Windows Server 2016 entfernt die Einschränkung für die Anzahl der Verbindungsbroker, die Sie in einer Bereitstellung, bei Verwendung von Remote Desktop Session Hosts (RDSH) und Remote Desktop Virtualization-Hosts (RDVH), die auch Windows Server 2016 ausgeführt. Die folgende Tabelle zeigt die Versionen von RDS-Komponenten arbeiten mit 2016 und 2012 R2-Versionen der Verbindungsbroker in einer hoch verfügbaren Bereitstellung mit drei oder mehr Verbindungsbroker.

| 3 + Verbindungsbroker im hohe Verfügbarkeit              | RDSH 2016 | RDVH 2016 | RDSH 2012 R2  | RDVH 2012 R2  |
|------------------------------------------|-----------|-----------|---------------|---------------|
| Windows Server 2016-Verbindungsbroker    | Unterstützt | Unterstützt | Unterstützt     | Unterstützt     |
| Windows Server 2012 R2-Verbindungsbroker | Nicht zutreffend       | Nicht zutreffend       | Unterstützt     | Unterstützt     |

## <a name="support-for-gpu-acceleration-with-hyper-v"></a>Unterstützung für GPU-Beschleunigung mit Hyper-V
In der folgende Tabelle erläutert die Unterstützung für GPU-Beschleunigung auf virtuellen Computern. Finden Sie unter [der Grafik-Virtualisierungstechnologie für Sie geeignet ist?](rds-graphics-virtualization.md) für Hilfe bei der Frage, was Sie benötigen. Spezielle Informationen DDA, sehen Sie sich [Planen für die Bereitstellung von diskrete Gerätezuordnung](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).

|VM-Gast-BS  |Windows Server 2012 R2 oder Windows Server 2016<br> Hyper-V-RemoteFX vGPU (Gen 1-Computer) |  Windows Server 2016 Hyper-V RemoteFX vGPU (Gen 2-VM) |  Diskrete Gerätezuordnung für Windows Server 2016 Hyper-V (Gen 2-VM) |
|-----------------------------|------------------------------------------------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| Windows 7 SP1               | Ja                                                        | Nein                                                     | Nein                                                                  |
| Windows 8.1                 | Ja                                                        | Nein                                                     | Nein                                                                  |
| Windows 10 1511 Update      | Ja                                                        | Ja                                                    | Ja                                                                 |
| Windows Server 2012 R2      | Ja                                                        | Nein                                                     | Ja (KB 3133690 erforderlich)                                           |
| Windows Server 2016         | Ja                                                        | Ja                                                    | Ja                                                                 |
| Windows Server 2012 R2 RDSH | Nein                                                         | Nein                                                     | Ja (KB 3133690 erforderlich)                                           |
| Windows Server 2016 RDSH    | Nein                                                         | Nein                                                     | Ja                                                                 |
## <a name="vdi-deployment--supported-guest-oss"></a>VDI-Bereitstellung – Gastbetriebssysteme OSs 
Remotedesktop-Virtualisierungshosts von Windows Server 2016 unterstützt die folgenden Betriebssysteme:

- Windows 10 Enterprise
- Windows 8.1 Enterprise 
- Windows 8 Enterprise 
- Windows 7 SP1 Enterprise 

Die folgende Tabelle zeigt die unterstützten Betriebssysteme für Remotedesktop-Virtualisierungshosts und Gast-Betriebssystem-Kombinationen:

| RDVH OS Version        | Version des Gastbetriebssystems           |
| ------------- |-------------|
| Windows Server 2016      | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012 R2   | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012      | Windows 7 SP1, Windows 8, Windows 8.1 |

> [!NOTE]  
> - Windows Server 2016 Remote Desktop Services unterstützt keine heterogene Sammlungen. Alle virtuellen Computer in einer Auflistung muss dieselbe Version des Betriebssystems. 
> - Sie können separate homogene Sammlungen mit anderen Gast-BS-Versionen auf demselben Host verwenden. 
> - VM-Vorlagen müssen auf einem Windows Server 2016 Hyper-V-Host verwendet werden, als Gastbetriebssystem auf einem Windows Server 2016 Hyper-V-Host erstellt werden.

## <a name="single-sign-on-sso"></a>Einmaliges Anmelden (SSO)
Windows Server 2016 RDS unterstützt die zwei wichtigsten SSO-Funktionen:

 - In-app (Remote Desktop-Anwendung auf Windows, iOS, Android und Mac)
 - Web-SSO
 
Verwenden die Remote Desktop-Anwendung, Sie können Speichern von Anmeldeinformationen als Teil der Verbindungsinformationen ([Mac](clients/remote-desktop-mac.md)) oder als Teil der verwalteten Konten ([iOS](clients/remote-desktop-ios.md#manage-your-user-accounts), [Android](clients/remote-desktop-android.md#manage-your-user-accounts), Windows) sicher über die Mechanismen, die für jedes Betriebssystem eindeutig.

Um über den Posteingang Remote Desktop Connection-Client auf Windows-Desktops und RemoteApps mit SSO zu verbinden, müssen Sie zu der RD-Webseite über Internet Explorer verbinden. Die folgenden Konfigurationsoptionen sind auf dem Server erforderlich. Keine anderen Konfigurationen werden für Web-SSO unterstützt:

 - RD-Web festgelegt Forms-basierte Authentifizierung (Standard)
 - RD-Gateway festgelegt werden, um das Kennwort-Authentifizierung (Standard)
 - Legen Sie die RDS-Bereitstellung auf "Verwendung RD-Gateway-Anmeldeinformationen für Remotecomputer" (Standard), in den Eigenschaften des RD-Gateway

> [!NOTE]
> Aufgrund der erforderlichen Konfiguration-Optionen wird die Web-SSO mit Smartcards nicht unterstützt. Benutzer, für die Anmeldung über Smartcards mehrere aufforderungen zum Anmelden auftreten kann.

Finden Sie weitere Informationen zum Erstellen von VDI-Bereitstellung der Remotedesktopdienste [unterstützt Windows 10-Sicherheitskonfigurationen für Remote Desktop Services VDI](rds-vdi-supported-config.md).

## <a name="using-remote-desktop-services-with-application-proxy-services"></a>Verwenden Remote Desktop Services mit anwendungsproxydienste

Sie können mit Remote Desktop Services, mit Ausnahme der Webclient verwenden [Azure AD-Anwendungsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-remote-desktop). Remote Desktop Services unterstützt die Verwendung nicht [Web Application Proxy](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server), die in Windows Server 2016 und früheren Versionen enthalten ist.
