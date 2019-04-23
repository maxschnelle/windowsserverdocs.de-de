---
title: Planen der Hyper-V-Sicherheit in Windows Server
description: Stellt eine Listen von sicherheitsüberlegungen für Hyper-V-Hosts und virtuelle Computer
ms.prod: windows-server-threshold
ms.service: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 115db481-b57e-41c3-8354-504f4bc6113a
manager: dongill
author: larsiwer
ms.author: kathyDav
ms.date: 08/03/2018
ms.openlocfilehash: 462124e1907ef03aa7746dd050be3e8c84c7abda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877411"
---
# <a name="plan-for-hyper-v-security-in-windows-server"></a>Planen der Hyper-V-Sicherheit in Windows Server

>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

Sichern Sie Betriebssystem des Hyper-V-Hosts, virtuelle Computer, Konfigurationsdateien und Daten des virtuellen Computers. Verwenden Sie die folgende Liste der empfohlenen Methoden als Prüfliste können Sie Ihre Hyper-V-Umgebung zu sichern.

## <a name="secure-the-hyper-v-host"></a>Schützen von Hyper-V-Hosts
- **Behalten Sie den Host, die sichern Betriebssystem.**
    - Minimieren Sie die Angriffsfläche, indem Sie mithilfe der mindestens Windows Server-Installationsoption, die Sie für das Verwaltungsbetriebssystem benötigen. Weitere Informationen finden Sie unter den [Installationsoptionen Abschnitt](/windows-server/windows-server#installation-options) der technischen Windows Server-Inhaltsbibliothek. Es wird nicht empfohlen, dass Sie produktionsworkloads auf Hyper-V unter Windows 10 ausführen.
    - Halten Sie die Hyper-V-Host-Betriebssystem, Firmware und Gerätetreibern mit der neuesten Sicherheitsupdates auf dem neuesten Stand. Überprüfen Sie die Empfehlungen Ihres Anbieters Firmware- und Treiberversionen zu aktualisieren.
    - Hyper-V-Host als Arbeitsstation verwenden Sie keine oder unnötigen Software zu installieren.
    - Verwalten Sie Hyper-V-Host, Remote. Wenn Sie den Hyper-V-Host lokal verwalten müssen, verwenden Sie Credential Guard. Weitere Informationen finden Sie unter [Schützen abgeleiteter Domänenanmeldeinformationen mit Credential Guard](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard).
    - Aktivieren Sie die anwendungssteuerungscode-Integritätsrichtlinien. Verwenden der virtualisierungsbasierten Sicherheit geschützt Code Integrity-Dienste. Weitere Informationen finden Sie unter [Device Guard-Bereitstellungshandbuch](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide).
- **Verwenden Sie ein sicheres Netzwerk.**
    - Verwenden Sie ein separates Netzwerk mit einem dedizierten Netzwerkadapter für den physischen Hyper-V-Computer.
    - Verwenden Sie ein privates oder sicheren Netzwerk Konfigurationen für den virtuellen Computer und virtuellen Festplattendateien an.
    - Verwenden Sie ein privates/dedizierte Netzwerk für Ihre live Migration-Traffic. Erwägen Sie die Aktivierung von IPSec in diesem Netzwerk, Verschlüsselung und des virtuellen Computers Daten, die über das Netzwerk während der Migration zu schützen. Weitere Informationen finden Sie unter [Einrichten von Hosts für die Livemigration ohne Failoverclustering](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md).
- **Secure Storage Migration-Traffic.** 

    Verwenden Sie SMB 3.0 für End-to-End-Verschlüsselung von SMB-Daten und Datenschutz, Manipulationen oder Lauschangriffen in nicht vertrauenswürdigen Netzwerken an. Verwenden Sie ein privates Netzwerk Zugriff auf den Inhalt des SMB-Freigabe um Man-in-the-Middle-Angriffe zu verhindern. Weitere Informationen finden Sie unter [SMB Sicherheitsverbesserungen](https://technet.microsoft.com/library/dn551363.aspx). 
- **Konfigurieren von Hosts als Teil eines geschützten Fabrics.** 

    Weitere Informationen finden Sie unter [überwachten Fabric](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md).
- **Schützen Sie Geräte an.** 

    Sichern Sie die Speichergeräte, in dem Sie Ressourcendateien für die virtuellen Computer beibehalten.
    
- **Sichern Sie die Festplatte an.** 

    Verwenden Sie BitLocker Drive Encryption, um Ressourcen zu schützen.
    
- **Erhöhen Sie das Hyper-V-Host-Betriebssystem.** 

    Verwenden Sie die Baseline-Einstellung sicherheitsempfehlungen beschrieben, die der [Windows Server-Sicherheitsbaseline](https://docs.microsoft.com/windows/device-security/windows-security-baselines).
    
- **Weisen Sie die erforderlichen Berechtigungen.**
    - Hinzufügen von Benutzern, die zum Verwalten des Hyper-V-Hosts den Hyper-V-Gruppe "Administratoren" werden müssen.
    - Gewähren Sie Administratoren für virtuelle Computer keinen, dass die Berechtigungen auf dem Hyper-V-Betriebssystem zu hosten.

- **Konfigurieren von Antivirus-Ausschlüsse und Optionen für die Hyper-V.**  

    Windows Defender schon [automatischen Ausschlüsse](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/configure-server-exclusions-windows-defender-antivirus) konfiguriert. Weitere Informationen zu Ausnahmen, finden Sie unter [antivirus-Ausschlüsse für Hyper-V-Hosts sollten](https://support.microsoft.com/kb/3105657). 

- **Binden Sie keine unbekannten VHDs.** Dies kann den Host in der Datei Systemangriffe auf Anwendungsebene verfügbar machen.

- **Aktivieren Sie nicht in Ihrer produktionsumgebung schachteln, es sei denn, dies erforderlich ist.**

    Wenn Sie die Schachtelung aktivieren, keine nicht unterstützte Hypervisoren auf einem virtuellen Computer ausgeführt.  

Sicherer Umgebungen:

- **Verwenden Sie Hardware mit einem Trusted Platform Module (TPM) 2.0-Chip, um ein geschütztes Fabric einrichten.** 

    Weitere Informationen finden Sie unter [Systemanforderungen für Hyper-V unter Windows Server 2016](../system-requirements-for-hyper-v-on-windows.md).

## <a name="secure-virtual-machines"></a>Sichern von virtuellen Computern
- **Erstellen Sie Generation 2 virtuellen Computern für unterstützte Gastbetriebssysteme.** 

    Weitere Informationen finden Sie unter [Sicherheitseinstellungen für die Generation 2](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md).
    
- **Aktivieren des sicheren Starts.** 

    Weitere Informationen finden Sie unter [Sicherheitseinstellungen für die Generation 2](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md).
    
- **Lassen Sie das Gast-Betriebssystem zu sichern.**

    - Installieren Sie die neuesten Sicherheitsupdates, bevor Sie auf einem virtuellen Computer in einer produktionsumgebung aktivieren.
    - Installieren Sie die Integrationsdienste für unterstützte Gastbetriebssysteme, die benötigt werden, und bewahren Sie sie auf dem neuesten Stand. Integration von Dienstupdates für Gäste, die unterstützte Windows-Versionen ausgeführt werden über Windows Update verfügbar.
    - Härten des Betriebssystems, der ausgeführt wird, auf jedem virtuellen Computer basierend auf der Rolle, die es ausführt. Verwenden Sie die Baseline-Einstellung sicherheitsempfehlungen, die im Abschnitt der [Windows-Sicherheitsbaseline](https://docs.microsoft.com/windows/device-security/windows-security-baselines).
    
- **Verwenden Sie ein sicheres Netzwerk.** 

    Stellen Sie sicher, virtuelle Netzwerkadapter verbinden, mit dem richtigen virtuellen Switch, und die geeignete sicherheitseinstellung und Beschränkungen angewendet haben.
    
- **Store von virtuellen Festplatten und die momentaufnahmedateien an einem sicheren Ort.**

- **Schützen Sie Geräte an.** 

    Konfigurieren Sie nur die erforderlichen Geräte für einen virtuellen Computer. Aktivieren Sie diskrete gerätezuordnung in Ihrer produktionsumgebung nicht nur bei für ein bestimmtes Szenario Bedarf. Wenn Sie es aktivieren, stellen Sie sicher, dass nur Geräte aus der vertrauenswürdigen Anbieter verfügbar machen. 
    
- **Konfigurieren von antivirus, Firewall und Angriffserkennungssoftware** auf virtuellen Computern nach Bedarf basierend auf der VM-Rolle.

- **Aktivieren Sie basierte virtualisierungssicherheit für Gäste, auf denen Windows 10 oder WindowsServer 2016 oder höher ausgeführt.** 

    Weitere Informationen finden Sie unter den [Device Guard-Bereitstellungshandbuch](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide).
    
- **Aktivieren Sie diskrete Gerätezuordnung nur bei Bedarf für eine bestimmte Arbeitslast**. 

    Aufgrund der Art der Übergabe durch ein physisches Gerät arbeiten Sie mit der Hersteller des Geräts zu verstehen, wenn es in einer sicheren Umgebung verwendet werden soll.

Sicherer Umgebungen:

- **Bereitstellen Sie virtueller Computer mit Schutz aktiviert, und klicken Sie auf ein geschütztes Fabric bereitstellen.** 

    Weitere Informationen finden Sie unter [Sicherheitseinstellungen für die Generation 2](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md) und [überwachten Fabric](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md).
