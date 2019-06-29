---
title: Bereitstellen von Stammzertifikate für bedingten Zugriff auf lokale AD
description: ''
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 200d3b96ee24b5e1264b4bf2e42d636f9e07fbef
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469679"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale Active Directory

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

In diesem Schritt, Sie stellen das Stammzertifikat für den bedingten Zugriff als vertrauenswürdiges Stammzertifikat für die VPN-Authentifizierung auf Ihrem lokalen AD.

- [**Vorherige:** Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)
- [**nächster:** Schritt 7.5. Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. Auf der **VPN-Konnektivität** Seite **Zertifikat herunterladen**.

   >[!NOTE]
   >Die **base64-Zertifikat herunterladen** Option steht für einige Konfigurationen, die base64-Zertifikate für die Bereitstellung erforderlich sind.

2. Melden Sie sich bei einem Computer einer Domäne mit dem Enterprise-Administratorrechten und führen Sie folgende Befehle über eine Eingabeaufforderung als Administrator der Cloud hinzufügen Zertifikate in Root der *Enterprise NTauth* speichern:

   >[!NOTE]
   >Für Umgebungen, in dem der VPN-Server nicht mit Active Directory-Domäne verknüpft ist, die Cloud-Stammzertifikate müssen hinzugefügt werden die _Trusted Root Certification Authorities_ manuell speichern.

   | Befehl | Beschreibung |
   | --- | --- |
   | `certutil -dspublish -f VpnCert.cer RootCA` | Erstellt zwei **Microsoft VPN-Stamm-CA-Generation 1** Container unter die **CN = AIA** und **CN = Zertifizierungsstellen** Container, und veröffentlicht Sie jedes Zertifikat der Stammzertifizierungsstelle als Wert für die _CA_ Attribut beider **Microsoft VPN-Stamm-CA-Generation 1** Container. |
   | `certutil -dspublish -f VpnCert.cer NTAuthCA` | Erstellt einen **CN = NTAuthCertificates** -Container unter die **CN = AIA** und **CN = Zertifizierungsstellen** Container, und veröffentlicht Sie jedes Zertifikat der Stammzertifizierungsstelle als Wert für die _CA_ Attribut der **CN = NTAuthCertificates** Container. |
   | `gpupdate /force` | Beschleunigt die Stammzertifikate für die Windows Server und Clientcomputer hinzufügen. |

3. Stellen Sie sicher, dass die Zertifikate der Stammzertifizierungsstelle in der Enterprise NTAuth-Speicher und werden als vertrauenswürdige vorhanden sind:
   1. Melden Sie sich bei einem Server mit Administratorrechten für Unternehmen mit der **Tools zur Zertifikat** installiert.

   >[!NOTE]
   >In der Standardeinstellung die **Tools zur Zertifikat** sind installierte Server der Zertifizierungsstelle. Sie können auf anderen Servern Elemente als Teil des installiert werden die **Rollenverwaltungstools** im Server-Manager.

   1. Geben Sie auf dem VPN-Server im Startmenü **pkiview.msc** auf das Unternehmens-PKI-Dialogfeld zu öffnen.
   1. Geben Sie im Menü Start **pkiview.msc** auf das Unternehmens-PKI-Dialogfeld zu öffnen.
   1. Mit der rechten Maustaste **Unternehmens-PKI** , und wählen Sie **Verwalten von AD-Container**.
   1. Stellen Sie sicher, dass jedes Microsoft VPN-Stamm-CA-Gen 1-Zertifikat unter vorhanden ist:
      - NTAuthCertificates
      - AIA-Container
      - Certificate Authorities Container

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7.5: Erstellen Sie OMA-DM-basierte VPNv2-Profile auf Windows 10-Geräten](vpn-create-oma-dm-based-vpnv2-profiles.md): In diesem Schritt erstellen Sie können OMA-DM-basierte VPNv2-Profile, die mithilfe von Intune zum Bereitstellen einer Konfigurationsrichtlinie für VPN-Gerät. PowerShell-Skript zu SCCM VPNv2 Profile erstellen, finden Sie unter [VPNv2 CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) Weitere Details.
