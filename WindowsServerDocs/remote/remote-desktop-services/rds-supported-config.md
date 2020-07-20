---
title: Unterstützte Konfigurationen für Remotedesktopdienste
description: Enthält Informationen zu Konfigurationen für RDS in Windows Server 2016 und Windows Server 2019.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 07/14/2020
ms.topic: article
ms.assetid: c925c7eb-6880-411f-8e59-bd0f57cc5fc3
author: lizap
manager: dongill
ms.openlocfilehash: 406112eae884b1e34d54eb18700c3ad28c3f52c6
ms.sourcegitcommit: f81aa22739d818382d314561dece59a9341dfb6f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2020
ms.locfileid: "86390077"
---
# <a name="supported-configurations-for-remote-desktop-services"></a>Unterstützte Konfigurationen für Remotedesktopdienste

> Gilt für: Windows Server 2016, Windows Server 2019

Wenn es um unterstützte Konfigurationen für Remotedesktopdienste geht, ist die Interoperabilität von Versionen das größte Problem. Die meisten Umgebungen enthalten mehrere Versionen von Windows Server, so können Sie z. B. möglicherweise über eine bestehende Windows Server 2012 R2 RDS-Bereitstellung verfügen, möchten aber auf Windows Server 2016 aktualisieren, um die Vorteile der neuen Features zu nutzen (z. B. die Unterstützung von OpenGL\OpenCL, der diskreten Gerätezuweisung oder von direkten Speicherplätzen). Es stellt sich dann die Frage, welche RDS-Komponenten mit verschiedenen Versionen arbeiten können und welche identisch sein müssen?

Unter diesem Aspekt finden Sie hier grundlegende Richtlinien für unterstützte Konfigurationen von Remotedesktopdiensten in Windows Server.

> [!NOTE]
> Überprüfen Sie die [Systemanforderungen für Windows Server 2016](../../get-started/system-requirements.md) und die [Systemanforderungen für Windows Server 2019](../../get-started-19/sys-reqs-19.md).

## <a name="best-practices"></a>Empfohlene Methoden

- Verwenden Sie Windows Server 2019 für Ihre Remotedesktopinfrastruktur (Web Access, Gateway, Verbindungsbroker und Lizenzserver). Windows Server 2019 ist abwärtskompatibel mit diesen Komponenten. Dies bedeutet, dass ein Windows Server 2016- oder Windows Server 2012 R2 RD-Sitzungshost eine Verbindung mit einem 2019 RD-Verbindungsbroker herstellen kann, aber nicht umgekehrt.

- Für RD-Sitzungshosts – alle Sitzungshosts in einer Sammlung müssen auf derselben Ebene liegen, aber Sie können mehrere Sammlungen verwenden. Sie verfügen über eine Sammlung mit Windows Server 2016-Sitzungshosts und eine mit Windows Server 2019-Sitzungshosts.

- Wenn Sie für Ihren RD-Sitzungshost ein Upgrade auf Windows Server 2019 durchführen, führen Sie auch ein Upgrade des Lizenzservers durch. Denken Sie daran, dass ein Lizenzserver für 2019 nur CALs von allen früheren Versionen von Windows Server bis hinunter zu Windows Server 2003 verarbeiten kann.

- Befolgen Sie die unter [Aktualisieren Ihrer Umgebung für Remotedesktopdienste](upgrade-to-rds.md#flow-for-deployment-upgrades) empfohlene Reihenfolge für das Upgrade.

- Wenn Sie eine hochverfügbare Umgebung erstellen, müssen sich alle Ihre Verbindungsbroker auf derselben Betriebssystemebene befinden.

## <a name="rd-connection-brokers"></a>RD-Verbindungsbroker

Windows Server 2016 hebt die Beschränkung für die Anzahl der Verbindungsbroker auf, die Sie in einer Bereitstellung verwenden können, wenn Sie Remotedesktop-Sitzungshosts (RDSH) und Remotedesktop-Virtualisierungshosts (RDVH) verwenden, die auch Windows Server 2016 ausführen. Die folgende Tabelle zeigt, welche Versionen von RDS-Komponenten mit den Versionen 2016 und 2012 R2 des Verbindungsbrokers in einer hochverfügbaren Bereitstellung mit drei oder mehr Verbindungsbrokern arbeiten.

|Drei oder mehr RD-Verbindungsbroker bei Hochverfügbarkeit|RDSH oder RDVH 2019|RDSH oder RDVH 2016|RDSH oder RDVH 2012 R2|
|---|---|---|---|
 |Windows Server 2019-Verbindungsbroker|Unterstützt|Unterstützt|Unterstützt|
 |Windows Server 2016-Verbindungsbroker|NICHT ZUTREFFEND|Unterstützt|Unterstützt|
 |Windows Server 2012 R2-Verbindungsbroker|NICHT ZUTREFFEND|NICHT ZUTREFFEND|Nicht unterstützt|

## <a name="support-for-graphics-processing-unit-gpu-acceleration"></a>Unterstützung für GPU-Beschleunigung (Graphics Processing Unit)

Remotedesktopdienste unterstützen Systeme, die mit GPUs ausgestattet sind. Anwendungen, die eine GPU erfordern, können über die Remoteverbindung verwendet werden. Darüber hinaus können Sie das GPU-beschleunigte Rendering und die Codierung aktivieren, um die Leistung und Skalierbarkeit der App zu verbessern.

Remotedesktopdienste-Sitzungshosts und Betriebssysteme von Einzelsitzungsclients können die Vorteile von physischen oder virtuellen GPUs nutzen, die auf vielfältige Weise für das Betriebssystem bereitgestellt werden, z. B. [für Azure-GPU optimierte VM-Größen](/en-us/azure/virtual-machines/windows/sizes-gpu), für den physischen RDSH-Server verfügbare GPUs und GPUs, die für VMs über unterstützte Hypervisoren bereitgestellt werden.

Hilfe zum Ermitteln Ihrer Anforderungen finden Sie unter [Welche Grafikvirtualisierungstechnologie ist für Sie geeignet?](rds-graphics-virtualization.md). Spezielle Informationen zu DDA finden Sie unter [Planen der Bereitstellung der diskreten Gerätezuweisung](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).

GPU-Anbieter können über ein separates Lizenzierungsschema für RDSH-Szenarien verfügen oder die GPU-Verwendung auf dem Serverbetriebssystem einschränken. Klären Sie die Anforderungen mit Ihrem bevorzugten Anbieter ab.

Bei GPUs, die von einem nicht von Microsoft stammenden Hypervisor oder einer nicht von Microsoft stammenden Cloudplattform bereitgestellt werden, müssen Treiber von WHQL digital signiert und vom GPU-Anbieter bereitgestellt werden.

### <a name="remote-desktop-session-host-support-for-gpus"></a>Remotedesktop-Sitzungshostunterstützung für GPUs

In der folgenden Tabelle sind die Szenarien aufgeführt, die von verschiedenen Versionen von RDSH-Hosts unterstützt werden.

|Feature|Windows Server 2008 R2|Windows Server 2012 R2|Windows Server 2016|Windows Server 2019|
|---|---|---|---|---|
|Verwendung der Hardware-GPU für alle RDP-Sitzungen|Nein|Ja|Ja|Ja|
|H.264/AVC-Hardwarecodierung (wenn von der GPU unterstützt)|Nein|Nein|Ja|Ja|
|Lastenausgleich zwischen mehreren, dem Betriebssystem präsentierten GPUs|Nein|Nein|Nein|Ja|
|H.264/AVC-Codierungsoptimierungen zum Minimieren der Bandbreitennutzung|Nein|Nein|Nein|Ja|
|H.264/AVC-Unterstützung für 4K-Auflösung|Nein|Nein|Nein|Ja|

### <a name="vdi-support-for-gpus"></a>VDI-Unterstützung für GPUs

Die folgende Tabelle enthält eine Übersicht der Unterstützung für GPU-Szenarien im Clientbetriebssystem.

|Feature|Windows 7 SP1|Windows 8.1|Windows 10|
|---|---|---|---|
|Verwendung der Hardware-GPU für alle RDP-Sitzungen|Nein|Ja|Ja|
|H.264/AVC-Hardwarecodierung (wenn von der GPU unterstützt)|Nein|Nein|Windows 10 1703 und höher|
|Lastenausgleich zwischen mehreren, dem Betriebssystem präsentierten GPUs|Nein|Nein|Windows 10 1803 und höher|
|H.264/AVC-Codierungsoptimierungen zum Minimieren der Bandbreitennutzung|Nein|Nein|Windows 10 1803 und höher|
|H.264/AVC-Unterstützung für 4K-Auflösung|Nein|Nein|Windows 10 1803 und höher|

### <a name="remotefx-3d-video-adapter-vgpu-support"></a>Unterstützung für RemoteFX 3D-Grafikkarte (vGPU)

> [!NOTE]
> Aufgrund von Sicherheitsbedenken ist RemoteFX vGPU auf allen Windows-Versionen ab dem Sicherheitsupdate vom 14. Juli 2020 standardmäßig deaktiviert. Weitere Informationen dazu finden Sie in [KB 4570006](https://support.microsoft.com/help/4570006).

Remotedesktopdienste unterstützen RemoteFX vGPUs, wenn der virtuelle Computer als Hyper-V-Gast unter Windows Server 2012 R2 oder Windows Server 2016 ausgeführt wird. Die folgenden Gastbetriebssysteme bieten RemoteFX vGPU-Unterstützung:

- Windows 7 SP1
- Windows 8.1
- Windows 10 1703 oder höher
- Windows Server 2016, nur in einer Einzelsitzungsbereitstellung

### <a name="discrete-device-assignment-support"></a>Unterstützung der diskreten Gerätezuweisung

Remotedesktopdienste unterstützen physische GPUs, die mit diskreter Gerätezuweisung von Windows Server 2016- oder Windows Server 2019-Hyper-V-Hosts präsentiert werden. Weitere Informationen finden Sie unter [Planen der Bereitstellung der diskreten Gerätezuweisung](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).


## <a name="vdi-deployment--supported-guest-oses"></a>VDI-Bereitstellung: Unterstützte Gastbetriebssysteme

RD-Virtualisierungshostserver von Windows Server 2016 und Windows Server 2019 RD unterstützen die folgenden Gastbetriebssysteme:

- Windows 10 Enterprise
- Windows 8.1 Enterprise
- Windows 7 SP1 Enterprise

> [!NOTE]
> - Remotedesktopdienste unterstützen keine heterogenen Sitzungssammlungen. Die Betriebssysteme aller virtuellen Computer in einer Sammlung müssen dieselbe Version aufweisen.
> - Sie können getrennte homogene Sammlungen mit verschiedenen Gastbetriebssystemversionen auf demselben Host verwenden.
> - Der zum Ausführen von VMS verwendete Hyper-V-Host muss dieselbe Version aufweisen, wie der zum Erstellen der ursprünglichen VM-Vorlagen verwendete Hyper-V-Host.

## <a name="single-sign-on"></a>Einmaliges Anmelden

Windows Server 2016 und Windows Server 2019 RDS unterstützen zwei wichtige SSO-Funktionen:

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
