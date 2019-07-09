---
title: Unterstützte Konfigurationen für Remotedesktopdienste
description: Enthält Informationen zu Konfigurationen für RDS in Windows Server 2016.
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66453083"
---
# <a name="supported-configurations-for-remote-desktop-services-in-windows-server-2016"></a>Unterstützte Konfigurationen für Remotedesktopdienste in Windows Server 2016

> Gilt für: Windows Server 2016

Wenn es um unterstützte Konfigurationen für Remotedesktopdienste geht, ist die Interoperabilität von Versionen das größte Problem. Die meisten Umgebungen enthalten mehrere Versionen von Windows Server, so können Sie z. B. möglicherweise über eine bestehende Windows Server 2012 R2 RDS-Bereitstellung verfügen, möchten aber auf Windows Server 2016 aktualisieren, um die Vorteile der neuen Features zu nutzen (z. B. die Unterstützung von OpenGL\OpenCL, der diskreten Gerätezuweisung oder von direkten Speicherplätzen). Es stellt sich dann die Frage, welche RDS-Komponenten mit verschiedenen Versionen arbeiten können und welche identisch sein müssen?

Unter diesem Aspekt finden Sie hier grundlegende Richtlinien für unterstützte Konfigurationen von Remotedesktopdiensten in Windows Server 2016.

> [!NOTE]
> Stellen Sie sicher, dass Sie die [Systemanforderungen für Windows Server 2016](../../get-started/system-requirements.md) gelesen haben.

## <a name="best-practices"></a>Empfohlene Methoden
- Verwenden Sie Windows Server 2016 für Ihre Remotedesktopinfrastruktur – Web Access, Gateway, Verbindungsbroker und Lizenzserver. Windows Server 2016 ist für diese Komponenten abwärtskompatibel. So kann sich ein 2012 R2 RD-Sitzungshost mit einem 2016 RD-Verbindungsbroker verbinden, aber der umgekehrte Fall ist nicht zulässig.

- Für RD-Sitzungshosts – alle Sitzungshosts in einer Sammlung müssen auf derselben Ebene liegen, aber Sie können mehrere Sammlungen verwenden. Sie verfügen über eine Sammlung mit Windows Server 2012 R2-Sitzungshosts und eine mit Windows Server 2016-Sitzungshosts.

- Wenn Sie für Ihren RD-Sitzungshost ein Upgrade auf Windows Server 2016 durchführen, führen Sie auch ein Upgrade des Lizenzservers durch. Denken Sie daran, dass ein Lizenzserver für 2016 nur CALs von allen früheren Versionen von Windows Server bis hinunter zu Windows Server 2003 verarbeiten kann.

- Befolgen Sie die unter [Aktualisieren Ihrer Umgebung für Remotedesktopdienste](upgrade-to-rds.md#flow-for-deployment-upgrades) empfohlene Reihenfolge für das Upgrade. 

- Wenn Sie eine hochverfügbare Umgebung erstellen, müssen sich alle Ihre Verbindungsbroker auf derselben Betriebssystemebene befinden.

## <a name="rd-connection-brokers"></a>RD-Verbindungsbroker

Windows Server 2016 hebt die Beschränkung für die Anzahl der Verbindungsbroker auf, die Sie in einer Bereitstellung verwenden können, wenn Sie Remotedesktop-Sitzungshosts (RDSH) und Remotedesktop-Virtualisierungshosts (RDVH) verwenden, die auch Windows Server 2016 ausführen. Die folgende Tabelle zeigt, welche Versionen von RDS-Komponenten mit den Versionen 2016 und 2012 R2 des Verbindungsbrokers in einer hochverfügbaren Bereitstellung mit drei oder mehr Verbindungsbrokern arbeiten.

| Drei oder mehr RD-Verbindungsbroker bei Hochverfügbarkeit              | RDSH 2016 | RDVH 2016 | RDSH 2012 R2  | RDVH 2012 R2  |
|------------------------------------------|-----------|-----------|---------------|---------------|
| Windows Server 2016-Verbindungsbroker    | Unterstützt | Unterstützt | Unterstützt     | Unterstützt     |
| Windows Server 2012 R2-Verbindungsbroker | N/V       | N/V       | Unterstützt     | Unterstützt     |

## <a name="support-for-gpu-acceleration-with-hyper-v"></a>Unterstützung für GPU-Beschleunigung mit Hyper-V
Die folgende Tabelle zeigt die Unterstützung für die GPU-Beschleunigung auf virtuellen Computern. Hilfe zum Ermitteln Ihrer Anforderungen finden Sie unter [Welche Grafikvirtualisierungstechnologie ist für Sie geeignet?](rds-graphics-virtualization.md). Spezielle Informationen zu DDA finden Sie unter [Planen der Bereitstellung der diskreten Gerätezuweisung](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).

|VM-Gastbetriebssystem  |Windows Server 2012 R2 oder Windows Server 2016<br> Hyper-V RemoteFX vGPU (virtueller Computer der ersten Generation) |  Windows Server 2016 Hyper-V RemoteFX vGPU (virtueller Computer der zweiten Generation) |  Windows Server 2016 Hyper-V – Diskrete Gerätezuweisung (virtueller Computer der zweiten Generation) |
|-----------------------------|------------------------------------------------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| Windows 7 SP1               | Ja                                                        | Nein                                                     | Nein                                                                  |
| Windows 8.1                 | Ja                                                        | Nein                                                     | Nein                                                                  |
| Windows 10 1511 Update      | Ja                                                        | Ja                                                    | Ja                                                                 |
| Windows Server 2012 R2      | Ja                                                        | Nein                                                     | Ja (KB 3133690 erforderlich)                                           |
| Windows Server 2016         | Ja                                                        | Ja                                                    | Ja                                                                 |
| Windows Server 2012 R2 RDSH | Nein                                                         | Nein                                                     | Ja (KB 3133690 erforderlich)                                           |
| Windows Server 2016 RDSH    | Nein                                                         | Nein                                                     | Ja                                                                 |
## <a name="vdi-deployment--supported-guest-oss"></a>VDI-Bereitstellung: Unterstützte Gastbetriebssysteme 
RD-Virtualisierungshostserver von Windows Server 2016 unterstützen die folgenden Gastbetriebssysteme:

- Windows 10 Enterprise
- Windows 8.1 Enterprise 
- Windows 8 Enterprise 
- Windows 7 SP1 Enterprise 

Die folgende Tabelle zeigt die unterstützten Kombinationen von RD-Virtualisierungshost-Betriebssystemen und Gastbetriebssystemen:

| RDVH-Betriebssystemversion        | Gastbetriebssystemversion           |
| ------------- |-------------|
| Windows Server 2016      | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012 R2   | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012      | Windows 7 SP1, Windows 8, Windows 8.1 |

> [!NOTE]  
> - Remotedesktopdienste von Windows Server 2016 unterstützen keine heterogenen Sammlungen. Alle virtuellen Computer in einer Sammlung müssen dieselbe Betriebssystemversion aufweisen. 
> - Sie können getrennte homogene Sammlungen mit verschiedenen Gastbetriebssystemversionen auf demselben Host verwenden. 
> - VM-Vorlagen müssen auf einem Windows Server 2016 Hyper-V-Host erstellt werden, um als Gastbetriebssystem auf einem Windows Server 2016 Hyper-V-Host verwendet werden zu können.

## <a name="single-sign-on-sso"></a>Einmaliges Anmelden (Single Sign-On, SSO)
Windows Server 2016 RDS unterstützt zwei wichtige SSO-Funktionen:

 - In-App (Remotedesktopanwendung für Windows, iOS, Android und Mac)
 - Web-SSO
 
Mithilfe der Remotedesktopanwendung können Sie Anmeldeinformationen entweder als Teil der Verbindungsinformationen ([Mac](clients/remote-desktop-mac.md)) oder als Teil der verwalteten Konten ([iOS](clients/remote-desktop-ios.md#manage-your-user-accounts), [Android](clients/remote-desktop-android.md#manage-your-user-accounts), Windows) sicher über die für die einzelnen Betriebssysteme eindeutigen Mechanismen speichern.

Um eine Verbindung zu Desktops und RemoteApps mit SSO über den Remotedesktopverbindungsclient des Posteingangs unter Windows herzustellen, müssen Sie über Internet Explorer eine Verbindung mit der RD-Webseite herstellen. Die folgenden Konfigurationsoptionen sind auf der Serverseite erforderlich. Für Web-SSO werden keine anderen Konfigurationen unterstützt:

 - Auf die formularbasierte Authentifizierung (Standard) festgelegtes RD-Web
 - Auf die Kennwortauthentifizierung (Standard) festgelegtes RD-Gateway
 - In den RD-Gateway-Eigenschaften auf „RD-Gateway-Anmeldeinformationen für Remotecomputer verwenden“ (Standard) festgelegte RDS-Bereitstellung

> [!NOTE]
> Aufgrund der erforderlichen Konfigurationsoptionen wird Web-SSO für Smartcards nicht unterstützt. Benutzer, die sich über Smartcards anmelden, werden möglicherweise mehrfach aufgefordert, sich anzumelden.

Weitere Informationen zum Erstellen der VDI-Bereitstellung von Remotedesktopdiensten finden Sie unter [Unterstützte Windows 10-Sicherheitskonfigurationen für Remotedesktopdienste-VDI](rds-vdi-supported-config.md).

## <a name="using-remote-desktop-services-with-application-proxy-services"></a>Verwenden von Remotedesktopdiensten mit Anwendungsproxydiensten

Sie können Remotedesktopdienste, mit Ausnahme des Webclients, mit dem [Azure AD-Anwendungsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-remote-desktop) verwenden. Remotedesktopdienste unterstützen nicht die Verwendung von [Webanwendungsproxys](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server), die in Windows Server 2016 und früheren Versionen enthalten sind.
