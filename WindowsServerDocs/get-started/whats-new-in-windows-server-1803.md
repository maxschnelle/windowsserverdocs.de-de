---
title: Neuerungen in Windows Server, Version 1803
description: Welche neuen Features sind für Compute, Identitäten, Verwaltung, Automatisierung, Netzwerk, Sicherheit und Speicher verfügbar?
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.date: 05/07/2018
ms.openlocfilehash: 73d0d62aac3771c4150a133950085170f7f51cb5
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961142"
---
# <a name="whats-new-in-windows-server-version-1803"></a>Neuerungen in Windows Server, Version 1803

>Gilt für: Windows Server (Halbjährlicher Kanal)

<img src=../media/landing-icons/new.png style='float:left; padding:.5em;' alt=Icon showing a newspaper>&nbsp;Weitere Informationen zu den neuesten Features in Windows finden Sie unter [Neuerungen in Windows Server](whats-new-in-windows-server.md). In diesem Abschnitt wird beschrieben, was in Windows Server, Version 1803, neu ist und was sich geändert hat. Die hier aufgeführten Neuerungen und Änderungen haben bei der Arbeit in dieser Version vermutlich die größte Auswirkung. Informationen finden Sie unter [Update für Windows Server (Halbjährlicher Kanal)](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/).

## <a name="windows-admin-center"></a>Windows Admin Center

„Projekt Honolulu“ ist nun **Windows Admin Center**.
<br>&nbsp;
> [!video https://www.youtube.com/embed/WCWxAp27ERk?autoplay=false]

[Windows Admin Center](../manage/windows-admin-center/overview.md) konsolidiert alle Aspekte der lokalen und Remoteserver-Verwaltung. Windows Admin Center ist eine lokal bereitgestellte, browserbasierte Verwaltungsbenutzeroberfläche, die keine Internetverbindung erfordert und Ihnen vollständige Kontrolle über alle Aspekte der Windows Server-Bereitstellung gibt.

## <a name="windows-server-release-strategy"></a>Windows Server-Versionsstrategie

Windows Server, Version 1709, wurde im September 2017 als die erste Version des halbjährlichen Kanals veröffentlicht. Der halbjährliche Kanal hat eine schnellere Versionskadenz und berücksichtigt Feedback von Personen, die eine schnelle Innovation alle paar Monate wünschen. Dies ergänzt Long Term Servicing Channel, dessen Versionsfrequenz alle 2 bis 3 Jahre ist.

Basierend auf Feedback und Telemetrie, haben diese Kanäle demonstriert, dass sie auch der folgenden allgemeinen Strategie entsprechen:
- Der halbjährliche Kanal eignet sich ideal für moderne Anwendungen und Innovationsszenarien, beispielsweise Container und Micro-Dienste.
- Long-Term Servicing Channel ist die bevorzugte Version für Infrastruktur-Szenarien wie softwaredefiniertes Rechenzentrum und hyperkonvergente Infrastruktur (HCI).

Die spezifischen Szenarien für den halbjährlichen Kanal und Long-Term Servicing Channel lauten wie folgt:

|   | Long Term Servicing Channel |  Halbjährlicher Kanal |
| ------------- | ------------- | ------------ |
| Empfohlene Szenarien     | Dateiserver für allgemeine Zwecke, Erst- und Drittanbieter-Arbeitslasten, herkömmliche Apps, Infrastrukturrollen, softwaredefiniertes Rechenzentrum und hyperkonvergente Infrastruktur  | Anwendungen in Containern, Container-Hosts und Anwendungsszenarien, die von schneller Innovation profitieren |
| Neue Versionen  | Alle 2–3 Jahre  | Alle 6 Monate |
| Support  | 5 Jahre Mainstreamsupport und 5 Jahre erweiterten Support  | 18 Monate |
| Editionen  | Alle verfügbaren Editionen von Windows Server  | Standard Edition und Datacenter Edition |
| Für wen nutzbar  | Alle Kunden über alle Kanäle | Nur Software Assurance- und Cloud-Kunden |
| Installationsoptions  | Server Core und Server mit Desktopdarstellung  | Server Core für Containerhost, Containerimage und Nano Server-Containerimage |

## <a name="application-platform-and-containers"></a>Anwendungsplattform und Container

- Optimization (Optimierung)
    - Das Server Core-Containerimage wird von Windows Server, Version 1709, um 30% reduziert.
    - Die Anwendungskompatibilität wurde auch zur Unterstützung der herkömmlichen Anwendungscontainer verbessert.
    - Die Start- und Laufzeitleistung von Containern wurden dank verschiedener Fixes und Optimierungen verbessert.
- Containernetzwerke: Localhost und HTTP-Proxy-Unterstützung wurde hinzugefügt, und Container-Skalierbarkeit und -Startzeit wurden verbessert.
- Tools: Unterstützung für Curl.exe, Tar.exe und SSH wurde verbessert, um PowerShell als Ergänzung für das Erstellen und Debuggen von Szenarien zu verwenden.

### <a name="server-core-container-image"></a>Server Core-Containerimage

Ein kleinerer Server Core-Container mit besserer Anwendungskompatibilität ist jetzt verfügbar. Ausführliche Informationen finden Sie [hier](https://techcommunity.microsoft.com/t5/virtualization/bg-p/Virtualization).

- Nicht verwendete optionale Features und Rollen wurden entfernt. Weitere Informationen finden Sie unter [In Server Core-Containern nicht vorhandene Rollen, Rollendienste und Features](../administration/server-core/server-core-container-removed-roles.md).
    - Verringerte Downloadgröße auf 1,58 GB, 30% Reduzierung seit Windows Server, Version 1709.
    - Größe auf dem Datenträger wurde auf 3,61 GB reduziert, 20% Reduzierung seit Windows Server, Version 1709.
- Nano Server-Containerimage liegt unter 100MB

### <a name="windows-subsystem-for-linux-wsl"></a>Windows-Subsystem für Linux (WSL)

WSL ermöglicht Serveradministratoren, vorhandene Tools und Linux-Skripts auf Windows Server zu verwenden. Zahlreiche Verbesserungen, die im [Blog „Befehlszeile”](https://devblogs.microsoft.com/commandline/tag/wsl/) präsentiert werden, sind nun Teil von Windows Server, einschließlich Hintergrundaufgaben, DriveFS, WSLPath und vieles mehr.

### <a name="kubernetes"></a>Kubernetes

Kubernetes (häufig K8s genannt) ist ein Open-Source-System für die Automatisierung der Bereitstellung, Skalierung und Verwaltung von containerisierten Anwendungen, die unter dem Engagement der [Cloud Native Computing Foundation](https://www.cncf.io) entwickelt wurden.

In Windows Server, Version 1709, konnten Benutzer Kubernetes auf Windows-Netzwerken nutzen, einschließlich:
- Freigegebene Pod-Depots: Infrastruktur- und Worker-Pods teilen sich jetzt ein Netzwerkdepot (vergleichbar mit einem Linux-Namespace).
- Optimierung der Endpunkte: Dank der Depotfreigabe müssen Containerdienste (mindestens) nur halb so viele Endpunkte wie zuvor nachverfolgen.
- Optimierung des Datenpfads: Verbesserungen der virtuellen Filterplattform und des Host Networking Service ermöglichen einen Kernel-basierten Lastenausgleich.

Mit der Veröffentlichung von Windows Server, Version 1803, werden weitere Features in kommenden Kubernetes-Versionen zur Verfügung stehen:
- [Speicher-Plug-Ins](https://github.com/Microsoft/K8s-Storage-Plugins) für Windows-Container, von Kubernetes koordiniert.
- Netzwerke auf Cloud-Niveau mit Initiativen wie unsere Partnerschaft mit Unterstützung von [Tigera auf Projekt Calico](https://cloudblogs.microsoft.com/windowsserver/2017/12/07/securing-modernized-apps-and-simplified-networking-on-windows-with-calico/).
- Windows-Plattform-Unterstützung für Hyper-V isolierte Pods mit mehreren Containern pro Pod.

### <a name="application-compatibility-and-feature-parity-issues-fixed"></a>Anwendungskompatibilitäts- und Funktionsparitätsprobleme wurden behoben.

- Microsoft Message Queuing (MSMQ) wird jetzt in einem Server Core-Container installiert.
- Ein Problem, das ASP.NET-Leistungsindikatoren aufhob, wurde behoben.
- Ein Problem, in dem Dienste in Containern keine Benachrichtigung zum Herunterfahren erhielten, wurde behoben.
    - Insbesondere wurde die Benachrichtigung für Server Core- und Nano Server Container-basierte Images wurde in ein CTRL_SHUTDOWN_EVENT geändert. Darüber hinaus erweitert es die Benachrichtigung in Server Core Container-basierten Images auf alle Prozesse, die im Container ausgeführt werden, einschließlich des Sendens von Servicebenachrichtigungen zum Herunterfahren für im Container ausgeführte Dienste.
- Eine Inkompatibilität von Docker Pull & Docker Last mit der Richtlinieneinstellung, die bestimmt, ob der BitLocker-Schutz für Festplattenlaufwerke erforderlich ist, um darauf schreiben zu können (FDVDenyWriteAccess), wurde korrigiert.

## <a name="storage"></a>Speicher

Mit dieser Version ist es möglich, zu verhindern, dass der Dienst Ressourcen-Manager für Dateiserver ein Änderungsjournal (auch bekannt als USN) auf allen Volumes beim Start des Dienstes erstellt. Dies kann Speicherplatz auf jedem Volume sparen, deaktiviert allerdings in Echtzeit die Dateiklassifizierung. Weitere Informationen finden Sie unter [Ressourcen-Manager für Dateiserver – Übersicht](../storage/fsrm/fsrm-overview.md).

## <a name="features-added-to-server-core"></a>Features, die Server Core hinzugefügt wurden

Server Core wurde die Transport-Server-Rolle in der Windows-Bereitstellungsdienste (WDS)-Rolle hinzugefügt.

Transport-Server enthält nur die Kernnetzwerkteile von WDS. Mit Transport-Server können Sie Multicast-Namespaces erstellen, die Daten (einschließlich Betriebssystemabbilder) von einem eigenständigen Server übertragen. Sie können es auch verwenden, wenn Sie einen PXE-Server wünschen, der Clients den PXE-Start ermöglicht, und um Ihre eigene benutzerdefinierte Setup-Anwendung herunterzuladen. Wenn Sie eine der folgenden Szenarien verwenden möchten, sollten Sie diese Option verwenden.

Den folgenden Windows PowerShell-Befehl können Sie verwenden, um den Transport-Server-Dienst auf Server Core zu aktivieren:

```
Install-WindowsFeature -Name WDS
```

## <a name="additional-references"></a>Weitere Verweise

[Dateiinformationen für die Windows Server-Version](./windows-server-release-info.md)<br>
[Neues in Windows 10, Version 1803 – Infos für IT-Experten](/windows/whats-new/whats-new-windows-10-version-1803)
