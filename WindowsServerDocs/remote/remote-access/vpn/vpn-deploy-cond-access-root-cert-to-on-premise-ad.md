---
title: Bereitstellen von Stammzertifikate für bedingten Zugriff auf lokale AD
description: ''
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 67d361db7a2dd3f2879e8beb924075dae68d52a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404314"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>Schritt 7.4. Bereitstellen von Stamm Zertifikaten für den bedingten Zugriff im lokalen AD

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

In diesem Schritt stellen Sie das Stamm Zertifikat für den bedingten Zugriff als vertrauenswürdiges Stamm Zertifikat für die VPN-Authentifizierung in Ihrem lokalen AD bereit.

- [**Vorher** Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)
- [**Weiter** Schritt 7.5. Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. Wählen Sie auf der Seite **VPN-Konnektivität die Option** **Zertifikat herunterladen**aus.

   >[!NOTE]
   >Die Option **Base64-Zertifikat herunterladen** ist für einige Konfigurationen verfügbar, die für die Bereitstellung Base64-Zertifikate erfordern.

2. Melden Sie sich bei einem in die Domäne eingebundenen Computer mit Unternehmens Administratorrechten an, und führen Sie diese Befehle an einer Administrator Eingabeaufforderung aus, um die Cloud-Stamm Zertifikate dem *Enterprise NTAuth* -Speicher hinzuzufügen:

   >[!NOTE]
   >Für Umgebungen, in denen der VPN-Server nicht mit der Active Directory Domäne verknüpft ist, müssen die Stamm Zertifikate der Cloud manuell zum Speicher der _vertrauenswürdigen Stamm Zertifizierungs_ stellen hinzugefügt werden.

   | Befehl | Beschreibung |
   | --- | --- |
   | `certutil -dspublish -f VpnCert.cer RootCA` | Erstellt zwei Container der Microsoft-VPN-Stamm Zertifizierungsstelle **Gen 1** unter den Containern **CN = AIA** und **CN = Certification Autoritäten** und veröffentlicht jedes Stamm Zertifikat als Wert für das _cACertificate_ -Attribut von **Microsoft VPN root. CA Gen 1** -Container. |
   | `certutil -dspublish -f VpnCert.cer NTAuthCA` | Erstellt einen **CN = ntauthcertificate** -Container unter den Containern **CN = AIA** und **CN = Certification Autoritäten** und veröffentlicht jedes Stamm Zertifikat als Wert für das _cACertificate_ -Attribut der **CN = Ntauthzertifikate** -Container. |
   | `gpupdate /force` | Hiermit wird das Hinzufügen der Stamm Zertifikate zu den Windows Server-und Client Computern beschleunigt. |

3. Vergewissern Sie sich, dass die Stamm Zertifikate im Enterprise NTAuth-Speicher vorhanden sind und als vertrauenswürdig angezeigt werden:
   1. Melden Sie sich bei einem Server mit Unternehmens Administratorrechten an, auf dem die **Verwaltungs Tools** für die Zertifizierungsstelle installiert sind.

   >[!NOTE]
   >Die Zertifizierungsstellen- **Verwaltungs Tools** werden standardmäßig als Zertifizierungsstellen Server installiert. Sie können auf anderen Mitglieds Servern als Teil der **Rollen Verwaltungs Tools** in Server-Manager installiert werden.

   1. Geben Sie auf dem VPN-Server im Startmenü **PKIView. msc** ein, um das Dialogfeld Unternehmens-PKI zu öffnen.
   1. Geben Sie im Startmenü **PKIView. msc** ein, um das Dialogfeld Unternehmens-PKI zu öffnen.
   1. Klicken Sie mit der rechten Maustaste auf **Enterprise PKI** , und wählen Sie die Option **Verwalten**
   1. Stellen Sie sicher, dass jedes Zertifikat der Microsoft-VPN-Stamm Zertifizierungsstelle Gen 1 unter:
      - NTAuthCertificates
      - AIA-Container
      - Zertifizierungsstellen Container

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7.5: Erstellen von OMA-DM-basierten VPNv2-Profilen auf Windows 10-Geräten @ no__t-0: In diesem Schritt können Sie OMA-DM-basierte VPNv2-Profile mithilfe von InTune erstellen, um eine VPN-Geräte Konfigurationsrichtlinie bereitzustellen. Wenn Sie SCCM-oder PowerShell-Skripts zum Erstellen von VPNv2-Profilen erstellen möchten, finden Sie weitere Informationen unter [VPNv2 CSP Settings](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) .
