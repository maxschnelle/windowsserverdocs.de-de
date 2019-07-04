---
title: Neuerungen in Windows Server, Version 1903
description: In diesem Thema werden einige der neuen Features in Windows Server, Version 1903, beschrieben, die ein Release im halbjährlichen Kanal darstellt.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.openlocfilehash: 0ec6a7ec624818b92fb306089f3dea3c786c0827
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280317"
---
# <a name="whats-new-in-windows-server-version-1903"></a>Neuerungen in Windows Server, Version 1903

>Gilt für: Windows Server (Halbjährlicher Kanal)

In diesem Thema werden einige der neuen Features in Windows Server, Version 1903, beschrieben, die ein Release im halbjährlichen Kanal darstellt. Zu diesen Features zählen Verbesserungen für das Ausführen und Verwalten von Containern, Tools für das Arbeiten in Server Core-Installationen und die Möglichkeit, Speicherplatz von Linux-Geräten zu migrieren.

Um herauszufinden, was demgegenüber neu im aktuellsten LTSC-Release (Long-Term Servicing Channel) von Windows Server ist, lesen Sie [Neuerungen in Windows Server 2019](../get-started-19/whats-new-19.md). Lesen Sie außerdem [Neues in Windows 10, Version 1903 – Infos für IT-Experten](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903).

Die Systemanforderungen für dieses Release sind die gleichen wie für Windows Server 2019 – weitere Informationen finden Sie unter [Systemanforderungen](../get-started-19/sys-reqs-19.md). Informationen über entfernte Features finden Sie unter [Features, die entfernt wurden bzw. deren Entfernung aus künftigen Windows Server, Version 1903, geplant ist](../get-started-19/removed-features-1903.md)

> [!NOTE]
> Windows-Container müssen die gleiche Windows-Version wie der Hostserver oder eine *frühere* Version verwenden. Beispielsweise kann ein Hostserver, der die veröffentlichte Version von Windows Server ausführt, Version 1903 (Build 18342), Windows Server-Container mit der gleichen oder einer früheren Version und Buildnummer ausführen (selbst wenn der Container eine Insider Preview-Version von Windows ausführt). Weitere Informationen finden Sie unter [Versionskompatibilität von Windows-Containern](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility).

## <a name="enhanced-support-for-non-microsoft-container-services"></a>Verbesserte Unterstützung für nicht von Microsoft stammende Containerdienste

Wir haben die Plattformfunktionen auf die Unterstützung von Azure-Containerdiensten und nicht von Microsoft stammende Containerdienste erweitert.

- Wir haben CRI-containerd mit dem Hostcomputedienst (Host Compute Service, HCS) integriert, um Pods von Windows-Containern und Linux-Containern unter Windows (LCOW) auf Azure zu unterstützen.
- Wir haben mit der Kubernetes-Community zusammengearbeitet, um Windows-Containerunterstützung zu ermöglichen. Mit der Veröffentlichung von Kubernetes v1.14 wurde die Knotenunterstützung für Windows Server offiziell von Beta zu stabil heraufgestuft. Weitere Informationen finden Sie unter [Windows containers now supported in Kubernetes](https://cloudblogs.microsoft.com/opensource/2019/03/25/windows-server-containers-now-supported-kubernetes/) (Windows-Container werden jetzt in Kubernetes unterstützt).
- Tigera Calico für Windows ist jetzt allgemein als Teil des Tigera Essentials-Abonnements erhältlich und bietet sowohl Netzwerke ohne Overlay als auch interoperable Netzwerkrichtlinien für gemischte Linux/Windows-Umgebungen.
- Wir haben Verbesserungen der Skalierbarkeit vorgenommen, was die Unterstützung für Overlaynetzwerke für Windows-Container verbessert, einschließlich der Integration mit Kubernetes durch das neueste Release von Flannel und Kubernetes v1.14. Weitere Informationen finden Sie unter [Einführung in die Windows-Unterstützung in Kubernetes](https://kubernetes.io/docs/setup/windows/).

## <a name="directx-hardware-acceleration-in-containers"></a>DirectX-Hardwarebeschleunigung in Containern

Wir aktivieren Unterstützung für Hardwarebeschleunigung von DirectX-APIs in Windows-Containern, um Szenarien wie Machine Learning (ML) unter Einbeziehung von lokaler GPU-Hardware (Graphical Processing Unit) zu unterstützen. Weitere Informationen finden Sie unter [Bringing GPU acceleration to Windows containers](https://techcommunity.microsoft.com/t5/Containers/Bringing-GPU-acceleration-to-Windows-containers/ba-p/393939) (Einbeziehung von GPU-Beschleunigung in Windows-Containern).

## <a name="updated-container-identity-and-group-managed-service-account-documentation"></a>Aktualisierte Dokumentation zu Containeridentität und gruppenverwalteten Dienstkonten

Wir haben der Dokumentation zu [Gruppenverwalteten Dienstkonten](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts) weitere Beispiele und Kompatibilitätsinformationen hinzugefügt und das [CredentialSpec-PowerShell-Modul](https://www.powershellgallery.com/packages/CredentialSpec) vom PowerShell-Katalog aus zugänglich gemacht. Weitere Informationen finden Sie im Blogbeitrag [What's new for container identity](https://techcommunity.microsoft.com/t5/Containers/What-s-new-for-container-identity/ba-p/389151) (Neues zur Containeridentität).

## <a name="add-task-scheduler-and-hyper-v-manager-to-server-core-installations"></a>Hinzufügen von Aufgabenplanung und Hyper-V-Manager zu Server Core-Installationen

Wie Ihnen vielleicht bekannt ist, empfehlen wir die Verwendung der Server Core-Installationsoption beim Einsatz von Windows Server im halbjährlichen Kanal in Produktionsumgebungen. Standardmäßig sind in Server Core jedoch eine Reihe nützlicher Verwaltungstools fortgelassen. Viele der häufig verwendeten Tools lassen sich durch Installieren des App-Kompatibilitätsfeatures hinzufügen, aber einige Tools fehlten immer noch.

Auf der Grundlage von Kundenfeedback haben wir uns daher entschieden, dem App-Kompatibilitätsfeature in dieser Version zwei weitere Tools hinzuzufügen: Aufgabenplanung (taskschd.msc) und Hyper-V-Manager (virtmgmt.msc).

Weitere Informationen finden Sie unter [Server Core-App-Kompatibilitätsfeature](../get-started-19/install-fod-19.md).

## <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>Der Speichermigrationsdienst kann jetzt lokale Konten, Cluster und Linux-Server migrieren

Mit dem Speichermigrationsdienst können Server einfacher zu einer neueren Version von Windows Server migriert werden. Er bietet ein grafisches Tool, das Daten auf Servern inventarisiert und anschließend die Daten und die Konfiguration auf neuere Server überträgt – ganz ohne Apps oder die Notwendigkeit für Benutzer, irgendetwas zu ändern.

Wenn Sie diese Version von Windows Server zum Orchestrieren von Migrationen verwenden möchten, haben wir für Sie die folgenden Funktionen hinzugefügt:

- Migrieren lokaler Benutzer und Gruppen zum neuen Server
- Migrieren von Speicher von Failoverclustern
- Migrieren von Speicher von einem Linux-Server, der Samba verwendet
- Vereinfachte Synchronisierung von migrierten Freigaben zu Azure mithilfe von Azure-Dateisynchronisierung
- Migrieren zu neuen Netzwerken wie etwa Azure

Weitere Informationen über den Speichermigrationsdienst finden Sie unter [Speichermigrationsdienst – Übersicht](../storage/storage-migration-service/overview.md).

## <a name="system-insights-disk-anomaly-detection"></a>System Insights-Datenträger-Anomalieerkennung

[System Insights](../manage/system-insights/overview.md) ist ein Feature zur vorausschauenden Analyse, das lokal Systemdaten von Windows Server analysiert und Einsichten in die Funktionsweise des Servers bietet. Es bietet standardmäßig eine Reihe integrierter Funktionen, wir haben aber die Möglichkeit zum Installieren weiterer Funktionen im Windows Admin Center hinzugefügt, und den Anfang macht die Erkennung von Datenträgeranomalien.

Die Erkennung von Datenträgeranomalien ist eine neue Funktion, die den Fall hervorhebt, dass Datenträger sich *anders* als gewöhnlich verhalten. Zwar ist anders nicht zwangsläufig schlecht, aber die Darstellung der anomalen Momente kann bei der Behandlung von Problemen auf Ihren Systemen eine große Hilfe sein.

Diese Funktion ist auch für Server verfügbar, die Windows Server 2019 ausführen.

## <a name="windows-admin-center-enhancements"></a>Verbesserungen am Windows Admin Center

Eine neue Version von Windows Admin Center wurde veröffentlicht, die Windows Server um neue Funktionen bereichert. Informationen zu den neuesten Features finden Sie unter [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md).

## <a name="security-baseline-for-windows-10-and-windows-server"></a>Sicherheitsgrundlinie für Windows 10 und Windows Server

Die Entwurfsversion der [Grundlinieneinstellungen der Sicherheitskonfiguration](https://blogs.technet.microsoft.com/secguide/2019/04/24/security-baseline-draft-for-windows-10-v1903-and-windows-server-v1903/) für Windows 10, Version 1903, und für Windows Server, Version 1903, ist verfügbar.

## <a name="setupdiag"></a>SetupDiag
[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag), Version 1.4.1, ist verfügbar.

SetupDiag ist ein Befehlszeilentool, mit dem Sie feststellen können, warum ein Windows-Update fehlgeschlagen ist. SetupDiag durchsucht dazu die Windows Setup-Protokolldateien. Beim Durchsuchen von Protokolldateien verwendet SetupDiag eine Reihe von Regeln für den Abgleich mit bekannten Problemen. In der aktuellen Version von SetupDiag enthält die Datei „rules.xml” 53 Regeln, die bei der Ausführung von SetupDiag extrahiert werden. Die Datei „rules.xml“ wird aktualisiert, sobald neue Versionen von SetupDiag verfügbar sind.

## <a name="update-rollback-improvements"></a>Verbesserungen beim Rollback von Updates

Server können jetzt nach Startfehlern automatisch wiederhergestellt werden, indem Updates entfernt werden, wenn der Startfehler erstmals nach der Installation vor Kurzem erfolgter Treiber- oder Qualitätsupdates aufgetreten ist. Wenn ein Gerät nach der vor Kurzem erfolgten Installation von Qualitäts- oder Treiberupdates nicht mehr ordnungsgemäß starten kann, deinstalliert Windows die Updates nun automatisch, um dem Gerät so schnell wie möglich wieder den normalen Betrieb zu ermöglichen.

Für diese Funktion muss der Server die Server Core-Installationsoption mit einer Partition für die [Windows-Wiederherstellungsumgebung](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) verwenden.

## <a name="microsoft-defender-advanced-threat-protection-atp-improvements"></a>Verbesserungen an Microsoft Defender Advanced Threat Protection (ATP)

Windows Server beinhaltet Microsoft Defender Advanced Thread Protection (weitere Informationen finden Sie unter [Windows Defender Antivirus auf Windows Server](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-on-windows-server-2016)). In dieser Version sind die folgenden Verbesserungen enthalten:

- [Verringerung der Angriffsoberfläche](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction): IT-Administratoren können Geräte mit erweitertem Webschutz konfigurieren, der ihnen das Definieren von Zulassungs- und Ablehnungslisten für bestimmte URLs und IP-Adressen ermöglicht.
- [Sicherheit der nächsten Generation](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10): Steuerelemente wurden auf den Schutz vor Ransomware, Missbrauch von Anmeldeinformationen und Angriffen, die über Wechselmedien übertragen werden, ausgeweitet.
    - Funktionen zur Durchsetzung von Integrität: Aktivieren von Remote-Laufzeitnachweis.
    - Manipulationsresistente Funktionen: Verwendet auf Virtualisierung basierende Sicherheit, um kritische ATP-Sicherheitsfunktionen gegenüber dem Betriebssystem und Angreifern zu isolieren.
- Microsoft Defender ATP-Schutztechnologien der nächsten Generation:
    - **Erweitertes Machine Learning**: Mit erweitertem Machine Learning und KI-Modellen verbessert, die einen Schutz vor Angriffen auch auf dem Scheitelpunkt und unter Nutzung innovativer Techniken zum Exploit von Sicherheitsrisiken, Tools und Malware ermöglichen.
    - **Notfallschutz vor Ausbrüchen**: Bietet Notfallschutz vor Ausbrüchen, der Geräte automatisch mit neuer Intelligenz aktualisiert, wenn ein neuer Ausbruch erkannt wurde.
    - **ISO 27001-zertifizierte Compliance**: Stellt sicher, dass der Clouddienst auf Bedrohungen, Sicherheitsrisiken und Auswirkungen hin analysiert wurde und das Risikomanagement und Sicherheitskontrollen aktiv sind.
    - **Geolocation-Unterstützung**: Unterstützung von Geolocation und Hoheit von Beispieldaten sowie konfigurierbare Aufbewahrungsrichtlinien.