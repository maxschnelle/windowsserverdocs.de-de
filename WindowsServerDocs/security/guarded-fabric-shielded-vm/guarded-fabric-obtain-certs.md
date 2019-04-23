---
title: Abrufen von Zertifikaten für die Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 14ee8eb6431a266d05897160d241d63e8cdb09a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887731"
---
# <a name="obtain-certificates-for-hgs"></a>Abrufen von Zertifikaten für die Host-Überwachungsdienst

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie Host-Überwachungsdienst bereitstellen, werden Sie aufgefordert, Signatur-und Verschlüsselungszertifikate bereitzustellen, die verwendet werden, um die vertraulichen Informationen, die zum Starten einer abgeschirmten VMs benötigt zu schützen.
Diese Zertifikate nicht behalten Sie die Host-Überwachungsdienst und dienen nur zum Entschlüsseln, die abgeschirmte VM-Schlüssel, wenn der Host, auf dem sie ausgeführt werden, dass sie fehlerfrei ist bewährt hat.
Mandanten (VM-Besitzer) verwenden, der öffentliche Hälfte der Zertifikate zum Autorisieren von Ihres Rechenzentrums auf die abgeschirmte VMs ausführen.
Dieser Abschnitt enthält die erforderlichen Schritte zum kompatibel Zertifikate für Signierung und Verschlüsselung für Host-Überwachungsdiensts zu erhalten.

## <a name="request-certificates-from-your-certificate-authority"></a>Anfordern von Zertifikaten von Ihrer Zertifizierungsstelle

Zwar nicht erforderlich, wird dringend empfohlen, dass Sie Ihre Zertifikate von einer vertrauenswürdigen Zertifizierungsstelle abrufen.
Auf diese Weise können VM-Besitzer, stellen Sie sicher, dass sie den richtigen Host-Überwachungsdienst-Server (d. h. Dienstanbieter oder Rechenzentrum) zum Ausführen ihrer geschützter VMs autorisiert sind.
In einem Unternehmensszenario können Sie Ihre eigenen Unternehmens-ZS zu verwenden, um diese Zertifikate ausstellen.
Verwenden Sie stattdessen eine bekannte, öffentliche Zertifizierungsstelle sollten gewährt Hostern und Dienstanbieter.

Signatur-und Verschlüsselungszertifikate müssen mit den folgenden Certificiate Eigenschaften ausgegeben werden (es sei denn, die "empfohlenen" gekennzeichnet):

Zertifikat-Template-Eigenschaft | Erforderlicher Wert 
------------------------------|----------------
Kryptografieanbieter               | Alle Schlüsselspeicheranbieter (KSP). Ältere Kryptografiedienstanbieter (CSPs) sind **nicht** unterstützt.
Schlüsselalgorithmus                 | RSA
Minimale Schlüsselgröße              | 2048 Bit
Signaturalgorithmus           | Empfohlen: SHA256
Schlüsselverwendung                     | Digitale Signatur *und* datenverschlüsselung
Erweiterte Schlüsselverwendung            | Serverauthentifizierung
Erneuerung des Schlüssels-Richtlinie            | Mit dem gleichen Schlüssel erneuern. Erneuern von Host-Überwachungsdienst-Zertifikaten mit unterschiedlichen Schlüsseln wird verhindert, dass geschützte VMs gestartet.
Antragstellername                  | Empfohlen: die Adresse des Unternehmens oder eine Webadressen. Diese Informationen werden VM-Besitzer in den Assistenten zum geschützten Daten angezeigt.

Diese Anforderungen gelten, ob Sie Zertifikate, gesichert durch Hardware oder Software verwenden.
Aus Sicherheitsgründen empfiehlt es sich, dass Sie Ihr HGS-Schlüssel in einem Hardwaresicherheitsmodul (HSM) zu verhindern, dass der private Schlüssel aus dem System kopiert erstellen.
Befolgen Sie die Anweisungen aus den HSM-Anbieter zum Anfordern von Zertifikaten mit der oben genannten Attribute aus, und achten Sie darauf, dass Sie zum Installieren und autorisieren das HSM KSP auf jedem Host-Überwachungsdienst-Knoten.

Jeder Host-Überwachungsdienst-Knoten benötigen Zugriff auf die gleiche Signierung und Verschlüsselungszertifikate.
Wenn Sie Software-Zertifikate verwenden, können exportieren Ihre Zertifikate in eine PFX-Datei mit einem Kennwort und Host-Überwachungsdienst, der Zertifikate für die Sie verwalten können.
Sie können auch auswählen, zum Installieren der Zertifikate in den Zertifikatspeicher des lokalen Computers, auf jedem Host-Überwachungsdienst-Knoten, und geben Sie den Fingerabdruck, Host-Überwachungsdienst.
Beide Optionen werden in erläutert die [initialisiert den Host-Überwachungsdienst Cluster](guarded-fabric-initialize-hgs.md) Thema.

## <a name="create-self-signed-certificates-for-test-scenarios"></a>Erstellen Sie selbstsignierte Zertifikate für Testszenarien

Wenn Sie eine Host-Überwachungsdienst-Lab-Umgebung erstellen und führen Sie nicht haben oder eine Zertifizierungsstelle verwenden möchten, können Sie selbstsignierte Zertifikate erstellen.
Sie erhalten eine Warnung auf, wenn die Zertifikatinformationen in den Assistenten zum geschützten Daten zu importieren, aber die gesamte Funktionalität bleibt gleich.

Zum Erstellen selbstsignierter Zertifikate, und in eine PFX-Datei exportieren, führen Sie die folgenden Befehle in PowerShell aus:

```powershell
$certificatePassword = Read-Host -AsSecureString -Prompt "Enter a password for the PFX file"

$signCert = New-SelfSignedCertificate -Subject "CN=HGS Signing Certificate"
Export-PfxCertificate -FilePath .\signCert.pfx -Password $certificatePassword -Cert $signCert
Remove-Item $signCert.PSPath

$encCert = New-SelfSignedCertificate -Subject "CN=HGS Encryption Certificate"
Export-PfxCertificate -FilePath .\encCert.pfx -Password $certificatePassword -Cert $encCert
Remove-Item $encCert.PSPath
```

## <a name="request-an-ssl-certificate"></a>Fordern Sie ein SSL-Zertifikat

Alle Schlüssel und vertrauliche Informationen übertragen werden, zwischen Hyper-V-Hosts und -Host-Überwachungsdiensts werden verschlüsselt, auf der Nachrichtenebene –, also die Informationen werden mit den Schlüsseln, die bekannte zur Host-Überwachungsdienst oder Hyper-V verwendet wird, die verhindern, dass andere sniffing Ihres Netzwerkdatenverkehrs und Diebstahl von Schlüsseln verschlüsselt für Ihre virtuellen Computer.
Jedoch wenn Sie Kompatibilität Reqiurements haben oder einfach die gesamte Kommunikation zwischen Hyper-V und Host-Überwachungsdienst verschlüsseln möchten, können Sie Host-Überwachungsdienst mit einem SSL-Zertifikat konfigurieren, die alle Daten auf der Transportebene verschlüsselt wird.

Sowohl die Host-Überwachungsdienst-Knoten die Hyper-V-Hosts müssen die SSL-Zertifikat, die, das Sie bereitstellen, das vertrauen, daher wird empfohlen, dass Sie das SSL-Zertifikat von Ihrer Unternehmenszertifizierungsstelle anfordern. Wenn Sie das Zertifikat anfordern möchten, achten Sie darauf, dass Sie Folgendes angeben:

SSL-Zertifikat-Eigenschaft | Erforderlicher Wert
-------------------------|---------------
Antragstellername             | Der Name Ihres Clusters Host-Überwachungsdienst (distributed Network Name). Hier werden die Verkettung der Namen des Host-Überwachungsdienst-Diensts bereitgestellt, um `Initialize-HgsServer` sowie Ihren HGS-Domänennamen ein.
Alternativer Antragstellername | Wenn Sie einen anderen DNS-Namen verwenden, erreichen Ihr HGS-Cluster (z. B. wenn er sich hinter einem Load Balancer befindet), achten Sie darauf, dass Sie diese DNS-Namen in das SAN-Feld, der die zertifikatanforderung eingeschlossen.

Die Optionen zum Festlegen dieses Zertifikats, bei der Initialisierung des HGS-Servers finden Sie im [konfigurieren Sie den ersten Knoten für den Host-Überwachungsdienst](guarded-fabric-initialize-hgs.md).
Sie können auch hinzufügen oder ändern Sie das SSL-Zertifikat zu einem späteren Zeitpunkt mithilfe der [Set-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver?view=win10-ps) Cmdlet.

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Installieren von Host-Überwachungsdienst](guarded-fabric-choose-where-to-install-hgs.md)