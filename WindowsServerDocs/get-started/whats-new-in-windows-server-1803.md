---
title: Neues in Windows Server, Version 1803
description: Welche neuen Features sind für Compute, Identitäten, Verwaltung, Automatisierung, Netzwerk, Sicherheit und Speicher verfügbar?
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.date: 05/07/2018
ms.openlocfilehash: c4f80b668b91e65b6c8bc528e14f52a1d117a3c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823091"
---
# <a name="whats-new-in-windows-server-version-1803"></a>Neues in IPAM unter Windows Server, Version 1803.

>Gilt für: Windows Server (Semi-Annual Channel)

<img src="../media/landing-icons/new.png" style='float:left; padding:.5em;' alt="Icon showing a newspaper">&nbsp;In diesem Abschnitt wird beschrieben, was in Windows Server, Version 1803, neu ist und was sich geändert hat. Die hier aufgeführten Neuerungen und Änderungen haben bei der Arbeit in dieser Version vermutlich die größte Auswirkung. Informationen finden Sie unter [Windows Server Semi-Annual Channel Update](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/).

## <a name="windows-admin-center"></a>Windows Admin Center

Projekt Honolulu ist nun **Windows Admin Center**.
<br>&nbsp;
> [!video https://www.youtube.com/embed/WCWxAp27ERk?autoplay=false]

[Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview) konsolidiert alle Aspekte der lokalen und Remoteserver-Verwaltung. Windows Admin Center ist eine lokal bereitgestellte, browserbasierte Management-Benutzeroberfläche, die keine Verbindung mit dem Internet erfordert und Ihnen vollständige Kontrolle über alle Aspekte der Windows Server-Bereitstellung gibt.

## <a name="windows-server-release-strategy"></a>Windows Server-Versionsstrategie

Windows Server, Version 1709 wurde im September 2017 als die erste Version des Semi-Annual Channel veröffentlicht. Semi-Annual Channel hat eine schnellere Versionskadenz und Feedback von Personen, die eine schnelle Innovation alle paar Monate wünschen. Dies ergänzt Long Term Servicing Channel, dessen Versionsfrequenz alle 2 bis 3 Jahre ist.

Basierend auf Feedback und Telemetrie, haben diese Kanäle demonstriert, dass sie auch der folgenden allgemeinen Strategie entsprechen:
- Semi-Annual Channel eignet sich ideal für moderne Anwendungen und Innovationsszenarien, beispielsweise Container und Micro-Dienste.
- Long-Term Servicing Channel ist die bevorzugte Version für Infrastruktur-Hauptszenarien wie Software-Defined Datacenter und hyperkonvergente Infrastruktur (HCI). 

Die spezifischen Szenarien für Semi-Annual Channel und Long-Term Servicing Channel lauten wie folgt:

|   | Long Term Servicing Channel |  Semi-Annual Channel |
| ------------- | ------------- | ------------ |
| Empfohlene Szenarien     | Dateiserver für allgemeine Zwecke, Erst- und Drittanbieter-Arbeitslasten, herkömmliche Apps, Infrastruktur-Rollen, Software-Defined Datacenter und hyperkonvergente Infrastruktur  | Containerisierte Anwendungen, Container-Hosts und Anwendungsszenarien profitieren von schneller Innovation |
| Neu erschienen  | Alle 2 – 3 Jahre  | Alle sechs Monate |
| Support  | 5 Jahre Mainstreamsupport und 5 Jahre erweiterten Support  | 18 Monate |
| Editionen  | Alle verfügbaren Editionen von Windows Server  | Standard Edition und Datacenter Edition |
| Wer kann es verwenden  | Alle Kunden über alle Kanäle | Software Assurance und Cloud nur für Kunden |
| Installationsoptions  | Server Core und Server mit Desktop-Version  | Server Core für Containerhost, Containerimage und Nano Server-Containerimage |

## <a name="application-platform-and-containers"></a>Anwendungsplattform und Container

- Optimization (Optimierung)
    - Das Server Core-Containerimage wird von Windows Server, Version 1709, um 30 % reduziert. 
    - Anwendungskompatibilität wurde auch zur Unterstützung der traditionellen Anwendungscontainer verbessert.
    - Container Start- und Laufzeitleistung wurden dank verschiedener Fixes und Optimierungen verbessert.
- Containernetzwerk-Funktionen: "Localhost" und HTTP-Proxy-Unterstützung hinzugefügt wurde, und Container Skalierbarkeit und die Startzeit wird verbessert.
- Tools: Unterstützung für Curl.exe Tar.exe und SSH wurde verbessert, um PowerShell zum Erstellen und Debuggen von Szenarien zu ergänzen.

### <a name="server-core-container-image"></a>Server Core-Containerimage

Ein kleinerer Server Core-Container mit besserer Anwendungskompatibilität ist jetzt verfügbar. Ausführliche Informationen finden Sie [hier](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/).

- Nicht verwendete optionale Features und Rollen wurden entfernt. Weitere Informationen finden Sie unter [Nicht in Server Core-Containern vorhandene Rollen, Rollendienste und Features](../administration/server-core/server-core-container-removed-roles.md).
    - Verringerte Downloadgröße auf 1,58 GB, 30 % Reduzierung seit Windows Server, Version 1709.
    - Größe auf dem Datenträger wurde auf 3,61 GB reduziert, 20 % Reduzierung seit Windows Server, Version 1709.
- Nano Server-Containerimage liegt unter 100MB

### <a name="windows-subsystem-for-linux-wsl"></a>Windows-Subsystem für Linux (WSL)

WSL ermöglicht Serveradministratoren, vorhandene Tools und Linux-Skripts auf Windows Server zu verwenden. Zahlreichen Verbesserungen, die im [Blog „Befehlszeile”](https://blogs.msdn.microsoft.com/commandline/tag/wsl/) präsentiert sind, sind nun Teil des Windows-Servers, einschließlich Hintergrundaufgaben, DriveFS, WSLPath und vieles mehr.

### <a name="kubernetes"></a>Kubernetes 

Kubernetes (häufig K8s genannt) ist ein Open-Source-System für die Automatisierung der Bereitstellung, Skalierung und Verwaltung von containerisierten Anwendungen, die unter dem Engagement der [Cloud Native Computing Foundation](https://www.cncf.io)entwickelt wurden. 

In Windows Server, Version 1709, konnten Benutzer Kubernetes auf Windows-Netzwerken nutzen, einschließlich:
- Freigegebene Pod Depots: Infrastruktur- und Workerrollen Pods verfügen nun über ein netzwerkdepot (analog zu einem Linux-Namespace).
- Endpunktoptimierung: Dank der Depot freigeben zu können müssen containerdienste mindestens die Hälfte so viele Endpunkte nachverfolgen.
- Datenpfad-Optimierung: Verbesserungen an der virtuellen Filterplattform und der Dienst für die Host-Netzwerke ermöglichen die Kernel-basierte Lastenausgleich.

Mit der Version von Windows Server, Version 1803 sind weitere Features in kommenden Kubernetes-Versionen verfügbar: 
- [Speicher-Plug-Ins](https://github.com/Microsoft/K8s-Storage-Plugins) für Windows-Container, von Kubernetes koordiniert.
- Netzwerke auf Cloud-Niveau mit Initiativen wie unsere Partnerschaft mit [Tigera auf Projekt Calico](https://cloudblogs.microsoft.com/windowsserver/2017/12/07/securing-modernized-apps-and-simplified-networking-on-windows-with-calico/).
- Windows-Plattform-Unterstützung für Hyper-V isolierte Depots mit mehreren Containern pro Depot.

### <a name="application-compatibility-and-feature-parity-issues-fixed"></a>Anwendungskompatibilitäts- und Funktionsparitätsprobleme wurden behoben

- Microsoft Message Queuing (MSMQ) wird jetzt in einem Server Core-Container installiert.
- Ein Problem, das ASP.NET-Leistungsindikatoren aufhob, wurde korrigiert.
- Ein Problem, in dem Dienste in Containern keine Benachrichtigung zum Herunterfahren erhielten, wurde korrigiert.
    - Die Benachrichtigung für Server Core und Nano Server Container-basierte Images wurde in ein CTRL_SHUTDOWN_EVENT geändert. Darüber hinaus erweitert es die Benachrichtigung in Server Core Container-basierte Images auf alle Prozesse, die im Container ausgeführt werden, einschließlich Servicebenachrichtigungen für das Herunterfahren für im Container ausgeführte Dienste.
- Eine Inkompatibilität von Docker Pull & Docker Last mit der Richtlinieneinstellung, die bestimmt, ob der BitLocker-Schutz für feste Datenlaufwerke erforderlich ist, um darauf schreiben zu können (FDVDenyWriteAccess), wurde korrigiert. 

## <a name="storage"></a>Speicher

Mit dieser Version ist es möglich, zu verhindern, dass der Ressourcen-Manager-Dienst ein Änderungsjournal (auch bekannt als USN) auf allen Volumes beim Start des Dienstes erstellt. Dies kann Speicherplatz auf jedem Datenträger sparen, deaktiviert allerdings in Echtzeit die Dateiklassifizierung. Weitere Informationen finden Sie unter [Übersicht über den Ressourcen-Manager für Dateiserver](https://docs.microsoft.com/windows-server/storage/fsrm/fsrm-overview).

## <a name="features-added-to-server-core"></a>Features, die Server Core hinzugefügt wurden

Server Core wurde die Transport-Server-Rolle in der Windows-Bereitstellungsdienste (WDS)-Rolle hinzugefügt.

Transport-Server enthält nur die Kernnetzwerkteile von WDS. Mit Transport-Server können Sie Multicast-Namespaces erstellen, die Daten (einschließlich Betriebssystemabbilder) von einem eigenständigen Server übertragen. Sie können es auch verwenden, wenn Sie einen PXE-Server wünschen, der Clients den PXE-Start ermöglicht und um Ihre eigene benutzerdefinierte Setup-Anwendung herunterzuladen. Wenn Sie eine der folgenden Szenarien verwenden möchten, sollten Sie diese Option verwenden.

Den folgenden Windows PowerShell-Befehl können Sie verwenden, um den Transport-Server-Dienst auf Server Core zu aktivieren:

```
Install-WindowsFeature -Name WDS
```

## <a name="see-also"></a>Siehe auch

[Informationen zu Windows Server-Version](https://docs.microsoft.com/windows-server/get-started/windows-server-release-info)<br>
[Was ist neu in Windows 10, Version 1803 IT Pro-Inhalt](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1803)
