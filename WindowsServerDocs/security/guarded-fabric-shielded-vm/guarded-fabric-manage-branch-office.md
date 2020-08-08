---
title: Überlegungen zu Zweigstellen
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.openlocfilehash: 140888bdaa27d5040ff723b94df2e28f3bbab167
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996161"
---
# <a name="branch-office-considerations"></a>Überlegungen zu Filialen

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal),

Dieser Artikel beschreibt bewährte Methoden für die Ausführung von abgeschirmten virtuellen Computern in Zweigniederlassungen und in anderen Remote Szenarien, in denen Hyper-V-Hosts Zeiträume mit eingeschränkter Konnektivität zu HGS aufweisen können.

## <a name="fallback-configuration"></a>Fall Back Konfiguration

Ab Windows Server, Version 1709, können Sie einen zusätzlichen Satz von Host-Überwachungsdienst-URLs auf Hyper-V-Hosts konfigurieren, die verwendet werden, wenn Ihre primäre HGS nicht reagiert.
Auf diese Weise können Sie einen lokalen HGS-Cluster ausführen, der als primärer Server verwendet wird, um eine bessere Leistung zu erzielen. Sie können dann auf die HGS Ihres Unternehmens Rechenzentrums zurückgreifen, wenn die lokalen Server ausfallen.

Wenn Sie die Fall Back-Option verwenden möchten, müssen Sie zwei HGS-Server einrichten. Sie können Windows Server 2019 oder Windows Server 2016 ausführen und sind entweder Teil desselben oder unterschiedlichen Clusters. Wenn es sich um verschiedene Cluster handelt, sollten Sie operative Verfahren einrichten, um sicherzustellen, dass die Nachweis Richtlinien zwischen den beiden Servern synchronisiert werden. Beide müssen in der Lage sein, den Hyper-V-Host ordnungsgemäß zu autorisieren, um abgeschirmte VMS auszuführen, und Sie müssen über das Schlüsselmaterial verfügen, das zum Starten der abgeschirmten VMS Sie können entweder ein paar frei gegebener Verschlüsselungs-und Signatur Zertifikate zwischen den beiden Clustern verwenden oder separate Zertifikate verwenden und die abgeschirmte HGS-VM so konfigurieren, dass beide Wächter (Verschlüsselungs-/Signatur-zertifikatpaare) in der Schutz Datendatei autorisiert werden.

Aktualisieren Sie dann Ihre Hyper-V-Hosts auf Windows Server-Version 1709 oder Windows Server 2019, und führen Sie den folgenden Befehl aus:
```powershell
# Replace https://hgs.primary.com and https://hgs.backup.com with your own domain names and protocols
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation' -FallbackKeyProtectionServerUrl 'https://hgs.backup.com/KeyProtection' -FallbackAttestationServerUrl 'https://hgs.backup.com/Attestation'
```

Wenn Sie die Konfiguration eines Fall Back Servers aufheben möchten, lassen Sie einfach beide Fall back Parameter aus:
```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation'
```

Damit der Hyper-V-Host den Nachweis sowohl mit dem primären als auch dem Fall Back Server übergibt, müssen Sie sicherstellen, dass Ihre Nachweis Informationen mit beiden HGS-Clustern auf dem neuesten Stand sind.
Außerdem müssen die Zertifikate, mit denen das TPM des virtuellen Computers entschlüsselt wird, in beiden HGS-Clustern verfügbar sein.
Sie können jeden HGS mit verschiedenen Zertifikaten konfigurieren und den virtuellen Computer so konfigurieren, dass er sowohl vertrauenswürdig ist, als auch einen freigegebenen Satz von Zertifikaten zu beiden HGS-Clustern hinzufügen.

Weitere Informationen zum Konfigurieren von HGS in einer Zweigstelle mithilfe von Fall Back-URLs finden Sie im Blogbeitrag [verbesserte Unterstützung für Zweigstellen für abgeschirmte VMs in Windows Server, Version 1709](/archive/blogs/datacentersecurity/improved-branch-office-support-for-shielded-vms-in-windows-server-version-1709).


## <a name="offline-mode"></a>Offline Modus

Im Offline Modus kann die abgeschirmte VM aktiviert werden, wenn HGS nicht erreicht werden kann, solange die Sicherheitskonfiguration des Hyper-V-Hosts nicht geändert wurde.
Der Offline Modus funktioniert, indem eine spezielle Version der TPM-Schlüssel Schutzvorrichtung des virtuellen Computers auf dem Hyper-V-Host zwischengespeichert wird.
Die Schlüssel Schutzvorrichtung wird in die aktuelle Sicherheitskonfiguration des Hosts (mit dem virtualisierungsbasierten Sicherheits Identitätsschlüssel) verschlüsselt.
Wenn der Host nicht mit HGS kommunizieren kann und seine Sicherheitskonfiguration nicht geändert wurde, kann er die zwischengespeicherte Schlüssel Schutzvorrichtung zum Starten der abgeschirmten VM verwenden.
Wenn sich die Sicherheitseinstellungen auf dem System ändern, z. b. eine neue Code Integritätsrichtlinie, die angewendet wird, oder der sichere Start deaktiviert wird, werden die zwischengespeicherten Schlüssel Schutzvorrichtungen für ungültig erklärt, und der Host muss einen HGS bestätigen, damit alle abgeschirmten VMS erneut offline gestartet werden können.

Der Offline Modus erfordert Windows Server Insider Preview Build 17609 oder höher sowohl für den Host-Überwachungsdienst Cluster als auch für den Hyper-V-Host.
Sie wird durch eine Richtlinie auf HGS gesteuert, die standardmäßig deaktiviert ist.
Um die Unterstützung für den Offline Modus zu aktivieren, führen Sie den folgenden Befehl auf einem HGS-Knoten aus:

```powershell
Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
```

Da die zwischen speicherbaren Schlüssel Schutzvorrichtungen für jeden abgeschirmten virtuellen Computer eindeutig sind, müssen Sie den vollständigen Herunterfahren (kein Neustart) durchlaufen und die abgeschirmten VMs starten, um eine zwischen speicherbare Schlüssel Schutzvorrichtung zu erhalten, nachdem diese Einstellung auf HGS aktiviert wurde.
Wenn Ihre abgeschirmte VM zu einem Hyper-V-Host migriert wird, auf dem eine ältere Version von Windows Server ausgeführt wird, oder eine neue Schlüssel Schutzvorrichtung aus einer älteren Version von HGS erhält, kann Sie nicht im Offline Modus gestartet werden, Sie kann jedoch weiterhin im Online Modus ausgeführt werden, wenn der Zugriff auf HGS verfügbar ist.