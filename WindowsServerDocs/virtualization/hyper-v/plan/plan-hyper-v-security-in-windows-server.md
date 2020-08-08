---
title: Planen der Hyper-V-Sicherheit in Windows Server
description: Enthält eine Liste mit Sicherheitsüberlegungen für Hyper-v-Hosts und virtuelle Computer.
ms.topic: article
ms.assetid: 115db481-b57e-41c3-8354-504f4bc6113a
manager: dongill
author: larsiwer
ms.author: kathydav
ms.date: 08/03/2018
ms.openlocfilehash: b9cb34a7d7c790bb7eee939f9247609e7cee6e3e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947976"
---
# <a name="plan-for-hyper-v-security-in-windows-server"></a>Planen der Hyper-V-Sicherheit in Windows Server

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Sichern Sie das Hyper-V-Host Betriebssystem, die virtuellen Computer, die Konfigurationsdateien und die Daten des virtuellen Computers. Verwenden Sie die folgende Liste der empfohlenen Vorgehensweisen als Checkliste, die Sie beim Schutz Ihrer Hyper-V-Umgebung unterstützt.

## <a name="secure-the-hyper-v-host"></a>Sichern des Hyper-V-Hosts
- **Halten Sie das Host Betriebssystem als sicher.**
    - Minimieren Sie die Angriffsfläche mithilfe der mindestens erforderlichen Windows Server-Installationsoption, die Sie für das Verwaltungs Betriebssystem benötigen. Weitere Informationen finden Sie im [Abschnitt Installationsoptionen](/windows-server/windows-server#installation-options) der technischen Inhalts Bibliothek für Windows Server. Es wird nicht empfohlen, produktionsworkloads auf Hyper-V unter Windows 10 auszuführen.
    - Halten Sie das Betriebssystem, die Firmware und die Gerätetreiber für das Hyper-V-Host mit den neuesten Sicherheitsupdates auf dem neuesten Stand. Überprüfen Sie die Empfehlungen Ihres Herstellers, um Firmware und Treiber zu aktualisieren.
    - Verwenden Sie den Hyper-V-Host nicht als Arbeitsstation, oder installieren Sie keine unnötige Software.
    - Verwalten Sie den Hyper-V-Host Remote. Wenn Sie den Hyper-V-Host lokal verwalten müssen, verwenden Sie Credential Guard. Weitere Informationen finden Sie unter [Schützen abgeleiteter Domänenanmeldeinformationen mit Credential Guard](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard).
    - Aktivieren von Code Integritäts Richtlinien Verwenden Sie virtualisierungsbasierte, Sicherheits geschützte Code Integritäts Dienste. Weitere Informationen finden Sie im [Device Guard-Bereitstellungs Handbuch](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide).
- **Verwenden Sie ein sicheres Netzwerk.**
    - Verwenden Sie ein separates Netzwerk mit einem dedizierten Netzwerkadapter für den physischen Hyper-V-Computer.
    - Verwenden Sie ein privates oder sicheres Netzwerk für den Zugriff auf VM-Konfigurationen und virtuelle Festplatten Dateien.
    - Verwenden Sie ein privates/dediziertes Netzwerk für den Live Migrations Datenverkehr. Aktivieren Sie IPSec in diesem Netzwerk, um die Verschlüsselung zu verwenden und die Daten Ihrer VM während der Migration zu schützen. Weitere Informationen finden Sie unter [Einrichten von Hosts für die Live Migration ohne Failoverclustering](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md).
- **Sicherer Speicher Migrations Datenverkehr.**

    Verwenden Sie SMB 3,0 für die End-to-End-Verschlüsselung von SMB-Daten und Datenschutz Manipulationen bzw. das Löschen von nicht vertrauenswürdigen Netzwerken. Verwenden Sie ein privates Netzwerk für den Zugriff auf den SMB-Freigabe Inhalt, um man-in-the-Middle-Angriffe zu verhindern. Weitere Informationen finden Sie unter [SMB-Sicherheitsverbesserungen](https://technet.microsoft.com/library/dn551363.aspx).
- **Konfigurieren Sie Hosts als Teil eines geschützten Fabrics.**

    Weitere Informationen finden Sie unter geschütztes [Fabric](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md).
- **Sichere Geräte.**

    Sichern Sie die Speichergeräte, auf denen die Ressourcen Dateien des virtuellen Computers aufbewahrt werden.

- **Sichern Sie die Festplatte.**

    Verwenden Sie BitLocker-Laufwerkverschlüsselung, um Ressourcen zu schützen.

- **Sichern Sie das Hyper-V-Host Betriebssystem.**

    Verwenden Sie die in der [Windows Server-Sicherheitsbasis Linie](https://docs.microsoft.com/windows/device-security/windows-security-baselines)beschriebenen grundlegenden Sicherheitseinstellungen.

- **Erteilen Sie entsprechende Berechtigungen.**
    - Fügen Sie Benutzer hinzu, die den Hyper-v-Host für die Hyper-v-Administratoren Gruppe verwalten müssen.
    - Erteilen Sie keine Berechtigungen für Administratoren für virtuelle Computer auf dem Hyper-V-Host Betriebssystem.

- **Konfigurieren Sie antivirenausschlüsse und Optionen für Hyper-V.**

    Für Windows Defender sind bereits [Automatische Ausschlüsse](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/configure-server-exclusions-windows-defender-antivirus) konfiguriert. Weitere Informationen zu Ausschlüssen finden Sie unter [Empfohlene antivirenausschlüsse für Hyper-V-Hosts](https://support.microsoft.com/kb/3105657).

- **Fügen Sie keine unbekannten VHDs ein.** Dadurch kann der Host Angriffe auf Dateisystem Ebene verfügbar machen.

- **Aktivieren Sie die Schachtelung in Ihrer Produktionsumgebung nur, wenn dies erforderlich ist.**

    Wenn Sie die Schachtelung aktivieren, führen Sie keine nicht unterstützten Hypervisoren auf einem virtuellen Computer aus.

Für sicherere Umgebungen:

- **Verwenden Sie Hardware mit einem Trusted Platform Module-Chip (TPM) 2,0, um ein geschütztes Fabric einzurichten.**

    Weitere Informationen finden Sie unter [System Anforderungen für Hyper-V auf Windows Server 2016](../system-requirements-for-hyper-v-on-windows.md).

## <a name="secure-virtual-machines"></a>Sichern von virtuellen Computern
- **Erstellen Sie virtuelle Computer der Generation 2 für unterstützte Gast Betriebssysteme.**

    Weitere Informationen finden Sie unter [Sicherheitseinstellungen der Generation 2](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md).

- **Aktivieren Sie den sicheren Start.**

    Weitere Informationen finden Sie unter [Sicherheitseinstellungen der Generation 2](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md).

- **Halten Sie das Gast Betriebssystem sicher.**

    - Installieren Sie die neuesten Sicherheitsupdates, bevor Sie einen virtuellen Computer in einer Produktionsumgebung einschalten.
    - Installieren Sie Integration Services für die unterstützten Gast Betriebssysteme, die diese benötigen, und halten Sie Sie auf dem neuesten Stand. Integration Services-Updates für Gäste, die unterstützte Windows-Versionen ausführen, sind über Windows Update verfügbar.
    - Härtung des Betriebssystems, das auf den einzelnen virtuellen Computern ausgeführt wird, basierend auf der Rolle, die es ausführt. Verwenden Sie die grundlegenden Sicherheits Einstellungs Empfehlungen, die in der [Windows-Sicherheitsbaseline](https://docs.microsoft.com/windows/device-security/windows-security-baselines)beschrieben werden.

- **Verwenden Sie ein sicheres Netzwerk.**

    Stellen Sie sicher, dass virtuelle Netzwerkadapter eine Verbindung mit dem richtigen virtuellen Switch herstellen und die entsprechenden Sicherheitseinstellungen und Einschränkungen angewendet werden.

- **Speichern von virtuellen Festplatten und Momentaufnahme Dateien an einem sicheren Ort.**

- **Sichere Geräte.**

    Konfigurieren Sie nur erforderliche Geräte für eine virtuelle Maschine. Aktivieren Sie keine diskrete Geräte Zuweisung in Ihrer Produktionsumgebung, es sei denn, Sie benötigen Sie für ein bestimmtes Szenario. Wenn Sie diese Option aktivieren, stellen Sie sicher, dass Sie nur Geräte von vertrauenswürdigen Anbietern verfügbar machen.

- **Konfigurieren Sie die Software für Antivirus-, Firewall-und Eindring** Versuche auf virtuellen Computern entsprechend der Rolle des virtuellen Computers entsprechend.

- **Aktivieren Sie die virtualisierungsbasierte Sicherheit für Gäste, auf denen Windows 10 oder Windows Server 2016 oder höher ausgeführt wird.**

    Weitere Informationen finden Sie im [Device Guard-Bereitstellungs Handbuch](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide).

- **Aktivieren Sie nur diskrete Geräte Zuweisungen, wenn dies für eine bestimmte Arbeitsauslastung erforderlich ist**.

    Aufgrund der Art der Übergabe eines physischen Geräts sollten Sie mit dem Gerätehersteller zusammenarbeiten, um zu verstehen, ob er in einer sicheren Umgebung verwendet werden sollte.

Für sicherere Umgebungen:

- **Stellen Sie virtuelle Computer mit aktiviertem Schutz bereit, und stellen Sie Sie in einem geschützten Fabric bereit.**

    Weitere Informationen finden Sie unter [Sicherheitseinstellungen der Generation 2](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md) und geschütztes [Fabric](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md).
