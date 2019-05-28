---
title: Was ist neu in Windows Server, Version 1903 sein
description: Dieses Thema beschreibt einige der neuen Features in Windows Server, Version 1903 sein, eine Halbjährlicher Kanal-Version ist.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.openlocfilehash: 2aa84df1ca162cb6e2dfa580b4b0744ff08cc95a
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983440"
---
# <a name="whats-new-in-windows-server-version-1903"></a>Was ist neu in Windows Server, Version 1903

>Gilt für: Windows Server (Semi-Annual Channel)

Dieses Thema beschreibt einige der neuen Features in Windows Server, Version 1903 sein, eine Halbjährlicher Kanal-Version ist. Zu diesen Funktionen gehören Verbesserungen für die Ausführung und Verwaltung von Containern, Tools für die Arbeit in Server Core-Installationen und die Möglichkeit zum Migrieren von Speicher von Linux-Geräten.

Stattdessen neuerungen in der neuesten Version der langfristigen Wartungskanal (LTSC) von Windows Server finden Sie unter finden Sie unter [Neuigkeiten in Windows Server-2019](../get-started-19/whats-new-19.md). Siehe auch [Neuigkeiten in Windows 10, Version 1903 IT Pro-Inhalt](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903).

Die Systemanforderungen für diese Version sind identisch mit dem Windows Server-2019 – finden Sie unter [Systemanforderungen](../get-started-19/sys-reqs-19.md) für Weitere Informationen. Was ist vor kurzem entfernt wurde, finden Sie unter [Funktionen entfernt oder geplant für den Austausch, die mit Windows Server, Version 1903 ab](../get-started-19/removed-features-1903.md)

> [!NOTE]
> Windows-Containern müssen die gleiche Version von Windows verwenden, als dem Hostserver oder *früheren* Version. Z. B. kann einem Hostserver, die unter der endgültigen Produktversion von Windows Server, Version 1903 (build 18342) Windows Server-Container mit dieselbe oder eine frühere Version ausführen und Buildnummer (selbst wenn der Container eine Insider Preview-Version von Windows verwendet). Weitere Informationen finden Sie unter [Windows Container-Versionskompatibilität](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility).

## <a name="enhanced-support-for-non-microsoft-container-services"></a>Verbesserte Unterstützung für nicht-Microsoft containerdienste

Wir erweiterte Funktionen zur Unterstützung von Azure Container Service und die containerdienste von nicht-Microsoft-Plattform.

- Wir die CRI-Containerd mit Host Compute Service (HCS) zur Unterstützung von Pods von Windows und Linux-Container unter Windows (LCOW) in Azure integriert.
- Wir haben mit der Kubernetes-Community, um Unterstützung für Windows-Containern zu aktivieren. Mit der Version von Kubernetes v1.14 hat Unterstützung für Windows Server-Knoten offiziell von Beta auf stabilen. Weitere Informationen finden Sie unter [Windows-Containern in Kubernetes nun unterstützt](https://cloudblogs.microsoft.com/opensource/2019/03/25/windows-server-containers-now-supported-kubernetes/).
- Tigera Calico für Windows ist jetzt allgemein verfügbar ist, als Teil des Tigera Essentials-Abonnement und Angebote nicht-Overlay-Netzwerk und Netzwerkrichtlinien für interoperable gemischten Linux/Windows-Umgebungen.
- Wir übermittelt Verbesserungen der Skalierbarkeit, die Netzwerkunterstützung für Windows-Container, einschließlich Integration mit Kubernetes in der neusten Version der jene und Kubernetes v1.14 Overlay zu verbessern. Weitere Informationen finden Sie unter [Einführung in die Windows-Unterstützung in Kubernetes](https://kubernetes.io/docs/setup/windows/).

## <a name="directx-hardware-acceleration-in-containers"></a>DirectX-Hardwarebeschleunigung in Containern

Aktivieren wir Unterstützung für die Hardwarebeschleunigung von DirectX-APIs in Windows-Container Tp unterstützungsszenarien wie z. B. lokale grafische Verarbeitung (Unit, GPU) Hardware mithilfe von Machine Learning (ML) Rückschlüsse. Weitere Informationen finden Sie unter [bringen GPU-Beschleunigung mit Windows-Containern](https://techcommunity.microsoft.com/t5/Containers/Bringing-GPU-acceleration-to-Windows-containers/ba-p/393939).

## <a name="updated-container-identity-and-group-managed-service-account-documentation"></a>Aktualisierte Container Benutzeridentität und die Dokumentation zu Service-Konto verwaltet werden

Wir hinzugefügt, Weitere Beispiele und Kompatibilität von Informationen zu den [Gruppenverwaltete Dienstkonten: Übersicht](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts) -Dokumentation und die [Anmeldeinformationen Spezifikation PowerShell-Modul](https://www.powershellgallery.com/packages/CredentialSpec) im PowerShell-Katalog verfügbar. Weitere Informationen finden Sie in der [Neuigkeiten für Container Identität](https://techcommunity.microsoft.com/t5/Containers/What-s-new-for-container-identity/ba-p/389151) Blogbeitrag.

## <a name="add-task-scheduler-and-hyper-v-manager-to-server-core-installations"></a>Server Core-Installationen der Aufgabenplanung und Hyper-V-Manager hinzufügen

Wie Sie wissen vielleicht, wird empfohlen, mithilfe der Installationsoption Server Core, bei Verwendung von Windows Server, Halbjährlicher Kanal in der Produktion. Server Core standardmäßig lässt jedoch eine Reihe von Tools für hilfreiches Verwaltungstool aus. Sie können die viele der am häufigsten verwendeten Tools durch Installieren des App-Kompatibilität, es gibt aber immer noch einige fehlende Tools hinzufügen.

Daher wurde hinzugefügt basierend auf Kundenfeedback, zwei weitere Tools für das App-Kompatibilität-Feature in dieser Version: Aufgabenplanung (taskschd.msc) und Hyper-V-Manager (virtmgmt.msc).

Weitere Informationen finden Sie unter [Kompatibilitätsfeature für Server Core-app](../get-started-19/install-fod-19.md).

## <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>Storage-Migration-Dienst migriert jetzt lokale Konten, -Cluster und Linux-Servern

Storage-Migration-Dienst erleichtert es, für die Migration der Server auf eine neuere Version von Windows Server. Es bietet ein grafisches Tool, die inventarisiert, die Daten auf Servern und dann die Daten und die Konfiguration auf neueren Servern übertragen – alles ohne Anwendungen oder Benutzer Änderungen vornehmen müssen.

Wenn diese Version von Windows Server verwenden, um Migrationen zu orchestrieren, haben wir die folgenden Funktionen hinzugefügt:

- Migrieren Sie lokale Benutzer und Gruppen mit dem neuen server
- Migrieren des Speichers von Failoverclustern
- Migrieren des Speichers von einem Linux-Server, der Samba verwendet
- Synchronisieren Sie leichter migrierte Dateifreigaben in Azure mithilfe von Azure File Sync
- Migrieren Sie zu neuen wie z. B. Azure-Netzwerken

Weitere Informationen zu Storage Migration Service, finden Sie unter [Übersicht über die Speicherung Datenbankmigrationsdienst](../storage/storage-migration-service/overview.md).

## <a name="system-insights-disk-anomaly-detection"></a>System Insights Datenträger Erkennung von Anomalien

[System Insights](../manage/system-insights/overview.md) ist ein predictive Analytics-Feature, das lokal analysiert Daten von Windows Server System und bietet einen Einblick in die Funktionsweise des Servers. Es enthält eine Reihe von integrierten Funktionen, aber wir haben die Möglichkeit, installieren zusätzliche Funktionen, die über Windows Admin Center, hinzugefügt, der Erkennung von Anomalien ab.

Erkennung von Anomalien ist eine neue Funktion, die hebt hervor, wenn Datenträger gerätefähigkeiten *anders* als üblich. Zwar verschiedene nicht unbedingt kann eine schlechte Sache, sehen diese anomalen Momente hilfreich sein, beim Behandeln von Problemen auf Ihren Systemen.

Diese Funktion steht auch für Server mit Windows Server-2019.

## <a name="windows-admin-center-enhancements"></a>Verbesserungen von Windows Admin Center

Eine neue Version von Windows Admin Center ist, Hinzufügen von neuen Funktionen zu Windows Server. Weitere Informationen zu den neuesten Features finden Sie unter [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md).

## <a name="security-baseline-for-windows-10-and-windows-server"></a>Grundlegende Sicherheit für Windows 10 und Windows Server

Der Draft-Version von der [Baseline Konfigurationseinstellungen](https://blogs.technet.microsoft.com/secguide/2019/04/24/security-baseline-draft-for-windows-10-v1903-and-windows-server-v1903/) Version 1903 für Windows 10, Version 1903 sein und für Windows Server verfügbar ist.

## <a name="setupdiag"></a>SetupDiag
[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) Version 1.4.1 ist verfügbar.

SetupDiag ist ein Befehlszeilentool, mit denen können diagnostizieren, warum ein Windows-Update ist fehlgeschlagen. SetupDiag durchsucht dazu die Windows Setup-Protokolldateien. Beim Durchsuchen von Protokolldateien verwendet SetupDiag eine Reihe von Regeln für den Abgleich mit bekannten Problemen. In der aktuellen Version von SetupDiag 53 in der Datei rules.xml enthaltenen Regeln vorhanden sind, wird der extrahiert, wenn SetupDiag ausgeführt wird. Die Datei rules.xml wird aktualisiert, sobald neue Versionen von SetupDiag verfügbar sind.

## <a name="update-rollback-improvements"></a>Aktualisieren Sie die Rollback-Verbesserungen

Server können jetzt automatisch wiederhergestellt werden beim Start von Updates zu entfernen, wenn nach der Installation des neuesten Updates für Treiber oder Qualität der Startfehler eingeführt wurde. Wenn ein Gerät nach der kürzlich durchgeführten Installationen von Servicequalitätsanforderungen Treiberupdates starten kann, wird die Updates für das Gerät zu versetzen, Sichern und normal ausgeführt von Windows jetzt automatisch deinstalliert.

Diese Funktion muss der Server mit die Server Core-Installationsoption verwenden eine [Windows-Wiederherstellungsumgebung](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) Partition.

## <a name="microsoft-defender-advanced-threat-protection-atp-improvements"></a>Verbesserungen von Microsoft Defender Advanced Threat Protection (ATP)

Windows Server beinhaltet Microsoft Defender Advanced Thread Protection (Weitere Informationen finden Sie unter [Windows Defender Antivirus auf Windows Server](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-on-windows-server-2016)). Dieses Release enthält die folgenden Verbesserungen:

- [Oberflächenverringerung Angriffe](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction) – IT-Administratoren können konfigurieren, Geräte mit Schutz für die erweiterte Web, die ihnen ermöglicht, definieren Sie zulassen und verweigern Sie Listen aus, für bestimmte URLs und IP-Adressen.
- [Sicherheit der nächsten Generation](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10) – Steuerelemente zum Schutz vor Ransomware, Missbrauch von Anmeldeinformationen und Angriffe, die über Wechselmedien übertragen werden erweitert wurden.
    - Integrität erzwingen Funktionen – Enable remote-Runtime-Nachweis.
    - Tamper-korrekturhilfen Funktionen – verwendet virtualisierungsbasierte Sicherheit zum Isolieren von Kritischer ATP Sicherheitsfunktionen außerhalb des Betriebssystems und der Angreifer.
- Technologien für Microsoft Defender-ATP-Schutz der nächsten Generation:
    - **Erweiterter Machine Learning**: Verbesserte mit fortschrittliches maschinelles lernen und KI-Modelle, die sie zum Schutz vor Apex-Angreifern, die mithilfe der innovativen Sicherheitsrisiko Exploit-Verfahren, Tools und Malware zu aktivieren.
    - **Notfall-Schutz**: Bietet Schutz für Notfall das automatisch aktualisiert Geräte neue Erkenntnisse, wenn ein neuer Ausbruch erkannt wurde.
    - **ISO 27001 Certified Compliance**: Stellt sicher, dass für die Bedrohungen, Schwachstellen und wirkt sich auf der Cloud-Dienst analysiert hat und Risiko-Management und Security-Steuerelemente vorhanden sind.
    - **Unterstützung für GeoLocation**: Unterstützung für Geolocation und -Hoheit, der Beispieldaten sowie Richtlinien für die konfigurierbare Aufbewahrung.