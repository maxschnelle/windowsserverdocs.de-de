---
title: Zertifikate für HGS abrufen
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 09/25/2019
ms.openlocfilehash: 0f9499402a5788cd3dc9ad9cd262d65636f9284c
ms.sourcegitcommit: 076504a92cddbd4b84bfcd89da1bf1c8c9e79495
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89427492"
---
# <a name="obtain-certificates-for-hgs"></a>Zertifikate für HGS abrufen

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Beim Bereitstellen von HGS werden Sie aufgefordert, Signatur-und Verschlüsselungs Zertifikate bereitzustellen, die zum Schutz der vertraulichen Informationen verwendet werden, die zum Starten einer abgeschirmten VM benötigt werden.
Diese Zertifikate verlassen niemals HGS und werden nur zum Entschlüsseln geschützter VM-Schlüssel verwendet, wenn der Host, auf dem Sie ausgeführt werden, bewiesen hat, dass Sie fehlerfrei ist.
Mandanten (VM-Besitzer) verwenden die öffentliche Hälfte der Zertifikate, um Ihr Rechenzentrum zum Ausführen ihrer abgeschirmten VMS zu autorisieren.
In diesem Abschnitt werden die erforderlichen Schritte zum Abrufen kompatibler Signatur-und Verschlüsselungs Zertifikate für HGS behandelt.

## <a name="request-certificates-from-your-certificate-authority"></a>Anfordern von Zertifikaten von Ihrer Zertifizierungsstelle

Es ist zwar nicht erforderlich, aber es wird dringend empfohlen, dass Sie Ihre Zertifikate von einer vertrauenswürdigen Zertifizierungsstelle abrufen.
Auf diese Weise können die VM-Besitzer überprüfen, ob Sie den richtigen HGS-Server (d. h. Dienstanbieter oder Datacenter) zum Ausführen ihrer abgeschirmten VMS autorisiert haben.
In einem Unternehmens Szenario können Sie Ihre eigene Unternehmens Zertifizierungsstelle verwenden, um diese Zertifikate auszugeben.
Hoster und Dienstanbieter sollten stattdessen eine bekannte öffentliche Zertifizierungsstelle verwenden.

Die Signatur-und Verschlüsselungs Zertifikate müssen mit den folgenden certificiate-Eigenschaften ausgestellt werden (es sei denn, Sie sind als "empfohlen" gekennzeichnet):

Zertifikat Vorlagen Eigenschaft | Erforderlicher Wert
------------------------------|----------------
Kryptografieanbieter               | Alle Schlüsselspeicher Anbieter (Key Storage Provider, KSP). Ältere Kryptografiedienstanbieter (CSPs) werden **nicht** unterstützt.
Schlüssel Algorithmus                 | RSA
Minimale Schlüsselgröße              | 2.048 Bits
Signaturalgorithmus           | Empfohlen: SHA256
Schlüsselverwendung                     | Digitale Signatur *und* Datenverschlüsselung
Erweiterte Schlüsselverwendung            | Serverauthentifizierung
Richtlinie zur Schlüssel Erneuerung            | Erneuern Sie mit demselben Schlüssel. Durch das Erneuern von HGS-Zertifikaten mit unterschiedlichen Schlüsseln wird verhindert, dass abgeschirmte VMS gestartet werden.
Antragstellername                  | Empfohlen: Name oder Webadresse Ihres Unternehmens. Diese Informationen werden den VM-Besitzern im Assistenten für die Schutz Datendatei angezeigt.

Diese Anforderungen gelten unabhängig davon, ob Sie Zertifikate verwenden, die von Hardware oder Software unterstützt werden.
Aus Sicherheitsgründen wird empfohlen, die HGS-Schlüssel in einem Hardware Sicherheitsmodul (HSM) zu erstellen, um zu verhindern, dass private Schlüssel vom System kopiert werden.
Befolgen Sie die Anweisungen des HSM-Anbieters, um Zertifikate mit den obigen Attributen anzufordern, und installieren und autorisieren Sie den HSM-KSP auf jedem HGS-Knoten.

Jeder HGS-Knoten benötigt Zugriff auf dieselben Signatur-und Verschlüsselungs Zertifikate.
Wenn Sie softwaregestützte Zertifikate verwenden, können Sie Ihre Zertifikate in eine PFX-Datei mit einem Kennwort exportieren und zulassen, dass HGS die Zertifikate für Sie verwaltet.
Sie haben auch die Möglichkeit, die Zertifikate im Zertifikat Speicher des lokalen Computers auf jedem HGS-Knoten zu installieren und den Fingerabdruck für HGS bereitzustellen.
Beide Optionen werden im Thema [Initialisieren des HGS-Clusters](guarded-fabric-initialize-hgs.md) erläutert.

## <a name="create-self-signed-certificates-for-test-scenarios"></a>Erstellen selbst signierter Zertifikate für Testszenarien

Wenn Sie eine HGS-Lab-Umgebung erstellen und nicht über eine Zertifizierungsstelle verfügen oder diese verwenden möchten, können Sie selbst signierte Zertifikate erstellen.
Beim Importieren der Zertifikat Informationen im Assistenten für Schutz Datendateien wird eine Warnung angezeigt, aber alle Funktionen bleiben unverändert.

Führen Sie die folgenden Befehle in PowerShell aus, um selbst signierte Zertifikate zu erstellen und in eine PFX-Datei zu exportieren:

```powershell
$certificatePassword = Read-Host -AsSecureString -Prompt "Enter a password for the PFX file"

$signCert = New-SelfSignedCertificate -Subject "CN=HGS Signing Certificate" -KeyUsage DataEncipherment, DigitalSignature
Export-PfxCertificate -FilePath .\signCert.pfx -Password $certificatePassword -Cert $signCert
Remove-Item $signCert.PSPath

$encCert = New-SelfSignedCertificate -Subject "CN=HGS Encryption Certificate" -KeyUsage DataEncipherment, DigitalSignature
Export-PfxCertificate -FilePath .\encCert.pfx -Password $certificatePassword -Cert $encCert
Remove-Item $encCert.PSPath
```

## <a name="request-an-ssl-certificate"></a>Anfordern eines SSL-Zertifikats

Alle Schlüssel und vertraulichen Informationen, die zwischen Hyper-V-Hosts und HGS übertragen werden, werden auf der Nachrichten Ebene verschlüsselt, d. h., die Informationen werden mit Schlüsseln verschlüsselt, die HGS oder Hyper-v genannt werden. Dadurch wird verhindert, dass ein Benutzer den Netzwerk Datenverkehr ausfängt und Schlüssel für Ihre VMS stiehlt.
Wenn Sie jedoch Kompatibilitätsanforderungen haben oder einfach die gesamte Kommunikation zwischen Hyper-V und HGS verschlüsseln möchten, können Sie HGS mit einem SSL-Zertifikat konfigurieren, mit dem alle Daten auf der Transport Ebene verschlüsselt werden.

Die Hyper-V-Hosts und HGS-Knoten müssen das von Ihnen bereitgestellte SSL-Zertifikat als vertrauenswürdig einstufen. Daher wird empfohlen, dass Sie das SSL-Zertifikat von Ihrer Unternehmens Zertifizierungsstelle anfordern. Wenn Sie das Zertifikat anfordern, müssen Sie Folgendes angeben:

SSL-Zertifikat Eigenschaft | Erforderlicher Wert
-------------------------|---------------
Antragstellername             | Der Name des HGS-Clusters (als Name des verteilten Netzwerks oder des FQDN des virtuellen Computer Objekts bezeichnet). Dabei handelt es sich um die Verkettung Ihres für bereitgestellten HGS-Dienst namens `Initialize-HgsServer` und ihren HGS-Domänen Namen.
Alternativer Antragstellername | Wenn Sie einen anderen DNS-Namen verwenden, um Ihren HGS-Cluster zu erreichen (z. b. wenn er sich hinter einem Load Balancer befindet), müssen Sie diese DNS-Namen in das Feld San ihrer Zertifikat Anforderung einschließen.

Die Optionen zum Angeben dieses Zertifikats beim Initialisieren des HGS-Servers finden Sie unter [Konfigurieren des ersten HGS-Knotens](guarded-fabric-initialize-hgs.md).
Sie können das SSL-Zertifikat auch zu einem späteren Zeitpunkt mit dem Cmdlet [Set-hgsserver](/powershell/module/hgsserver/set-hgsserver?view=win10-ps) hinzufügen oder ändern.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Installieren von HGS](guarded-fabric-choose-where-to-install-hgs.md)
