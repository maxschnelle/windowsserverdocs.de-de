---
title: Branch Office Überlegungen
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: d93c37227af1eb62368fbcd4ec5d6a48374b45ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877061"
---
# <a name="branch-office-considerations"></a>Überlegungen zu Filialen

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal) 

Dieser Artikel beschreibt bewährte Methoden für die Ausführung von geschützten virtuellen Maschinen in Zweigstellen und anderen remote-Szenarien, in dem Hyper-V-Hosts Zeiträume mit eingeschränkter Konnektivität zum Host-Überwachungsdienst haben können.

## <a name="fallback-configuration"></a>Fallbackkonfiguration

Ab Windows Server-Version 1709, können Sie konfigurieren einen zusätzlichen Satz von URLs für Host-Überwachungsdienst auf Hyper-V-Hosts für die Verwendung, wenn Ihre primären Host-Überwachungsdienst reagiert.
Dadurch können Sie einen lokalen Host-Überwachungsdienst-Cluster ausführen, der verwendet wird als primärer Server für eine bessere Leistung mit der Möglichkeit, die auf Ihrem unternehmensdatencenter-Host-Überwachungsdienst zurückzugreifen, wenn der lokale Server nicht verfügbar sind.

Um die fallback-Option verwenden zu können, müssen Sie zwei HGS-Server einrichten. Sie können Windows Server-2019 ausgeführt, oder Windows Server 2016 und entweder Mitglied der gleichen oder einem anderen Cluster. Wenn sie die verschiedenen Clustern sind, möchten Sie einrichten, dass betriebliche Verfahren, um sicherzustellen, dass die Richtlinien Nachweis zwischen den beiden Servern synchronisiert sind. Beide müssen in der Lage, ordnungsgemäß autorisiert den Hyper-V-Host ausführen abgeschirmter VMs und das Schlüsselmaterial benötigt, um die geschützten virtuellen Computer zu starten. Sie können auswählen, ist ein Paar von freigegebenen Verschlüsselung und Signaturzertifikate zwischen den beiden Clustern, oder verwenden Sie separate Zertifikate und Konfigurieren der Host-Überwachungsdienst abgeschirmte VM, um beide Überwachungen (Verschlüsselung/Signieren der Zertifikat-Paare) in den geschützten Daten zu autorisieren. die Datei.

Klicken Sie dann aktualisieren Sie den Hyper-V-Hosts Windows Server-Version 1709 oder Windows Server-2019 aus, und führen Sie den folgenden Befehl aus:
```powershell
# Replace https://hgs.primary.com and https://hgs.backup.com with your own domain names and protocols
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation' -FallbackKeyProtectionServerUrl 'https://hgs.backup.com/KeyProtection' -FallbackAttestationServerUrl 'https://hgs.backup.com/Attestation'
```

Um die Konfiguration ein fallback-Servers aufheben, lassen Sie einfach beide fallback-Parameter:
```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation'
```

Damit für den Hyper-V-Host Nachweis mit den primären und fallback-Server übergeben können müssen Sie sicherstellen, dass Ihre Informationen zum Identitätsnachweis auf dem neuesten Stand mit beiden HGS-Clustern ist.
Darüber hinaus müssen die Zertifikate, die zum Entschlüsseln des virtuellen Computers TPM in beiden Clustern Host-Überwachungsdienst verfügbar sein.
Sie können konfigurieren jeder Host-Überwachungsdienst mit verschiedenen Zertifikaten und Konfigurieren des virtuellen Computers, um beide zu vertrauen, oder beide Cluster HGS einen gemeinsamen Satz von Zertifikaten hinzugefügt.

Weitere Informationen zum Konfigurieren von Host-Überwachungsdienst in einer Zweigstelle, die mithilfe von fallback-URLs finden Sie im Blogbeitrag [verbesserte Unterstützung von Filialen für abgeschirmte VMs in Windows Server, Version 1709](https://blogs.technet.microsoft.com/datacentersecurity/2017/11/15/improved-branch-office-support-for-shielded-vms-in-windows-server-version-1709/).


## <a name="offline-mode"></a>Offline-Modus

Offline-Modus können Ihre geschützte VM zu aktivieren, wenn Host-Überwachungsdienst nicht erreicht werden kann, solange die Sicherheitskonfiguration des Hyper-V-Hosts nicht geändert hat.
Offline-Modus funktioniert durch das Zwischenspeichern einer speziellen Version von der VM-TPM-Schlüsselschutzvorrichtung auf dem Hyper-V-Host.
Die Schlüsselschutzvorrichtung wird auf die aktuelle Sicherheitskonfiguration des Hosts (mit der virtualisierungsbasierten Sicherheit Identitätsschlüssel) verschlüsselt.
Wenn der Host ist für die Kommunikation mit HGS, und die Sicherheitskonfiguration wurde nicht geändert, werden sie die zwischengespeicherte Schlüsselschutzvorrichtung verwenden, um die abgeschirmte VM starten.
Beim Ändern von Sicherheitseinstellungen auf dem System, z. B. eine neue codeintegritätsrichtlinie angewendet wird oder der sichere Start deaktiviert werden, werden die zwischengespeicherten Schlüsselschutzvorrichtungen ungültig, und der Host muss mit einem Host-Überwachungsdienst vor allen bestätigen abgeschirmte VMs offline neu gestartet werden können.

Offline-Modus erfordert Windows Server Insider Preview Build 17609 oder höher für die Host-Überwachungsdienst-Cluster und Hyper-V-Host an.
Es wird durch eine Richtlinie auf den Host-Überwachungsdienst bietet gesteuert, die standardmäßig deaktiviert ist.
Um Unterstützung für offline-Modus zu aktivieren, führen Sie den folgenden Befehl auf einem Host-Überwachungsdienst-Knoten:

```powershell
Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
```

Da die zwischenspeicherbaren Schlüsselschutzvorrichtungen für jede geschützte VM eindeutig sind, müssen Sie vollständig heruntergefahren (kein Neustart), und starten Sie die abgeschirmten VMs auf eine zwischenspeicherbare schlüsselschutzkomponente zu erhalten, nachdem Sie diese Einstellung aktiviert ist, auf dem Host-Überwachungsdienst.
Wenn Ihre abgeschirmte VM auf einem Hyper-V-Host mit einer älteren Version von Windows Server migriert oder ruft einen neuen Schlüsselprotektor aus einer älteren Version von Host-Überwachungsdienst, ist nicht möglich, selbst im Offlinemodus starten, sondern können weiter im Onlinemodus ausgeführt wird, wenn es sich bei den Zugriff auf den Host-Überwachungsdienst Standbyspeicherlisten berechnet wird kann.
