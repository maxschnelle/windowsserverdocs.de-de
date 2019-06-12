---
title: Bereitstellen von Stammzertifikate für bedingten Zugriff auf lokale AD
description: ''
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 4aaad98cd04c9b07bdea848294e10d9bcb602064
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749548"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale Active Directory

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

In diesem Schritt, Sie stellen das Stammzertifikat für den bedingten Zugriff als vertrauenswürdiges Stammzertifikat für die VPN-Authentifizierung auf Ihrem lokalen AD.

- [**Vorherige:** Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)
- [**nächster:** Schritt 7.5. Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. Auf der **VPN-Konnektivität** Seite **Zertifikat herunterladen**. 
   
    ![Herunterladen des Zertifikats für den bedingten Zugriff](../../media/Always-On-Vpn/06.png)

    >[!NOTE]
    >Die **base64-Zertifikat herunterladen** Option steht für einige Konfigurationen, die base64-Zertifikate für die Bereitstellung erforderlich sind. 

2. Melden Sie sich bei einem Computer einer Domäne mit dem Enterprise-Administratorrechten und führen Sie folgende Befehle über eine Eingabeaufforderung als Administrator der Cloud hinzufügen Zertifikate in Root der *Enterprise NTauth* speichern:

    >[!NOTE]
    >Für Umgebungen, in dem der VPN-Server nicht mit Active Directory-Domäne verknüpft ist, die Cloud-Stammzertifikate müssen hinzugefügt werden die _Trusted Root Certification Authorities_ manuell speichern.

    |Befehl  |Beschreibung  |  
    |---------|-------------| 
    |`certutil -dspublish -f VpnCert.cer RootCA`     |Erstellt zwei **Microsoft VPN-Stamm-CA-Generation 1** Container unter die **CN = AIA** und **CN = Zertifizierungsstellen** Container, und veröffentlicht Sie jedes Zertifikat der Stammzertifizierungsstelle als Wert für die _CA_ Attribut beider **Microsoft VPN-Stamm-CA-Generation 1** Container.|  
    |`certutil -dspublish -f VpnCert.cer NTAuthCA`   |Erstellt einen **CN = NTAuthCertificates** -Container unter die **CN = AIA** und **CN = Zertifizierungsstellen** Container, und veröffentlicht Sie jedes Zertifikat der Stammzertifizierungsstelle als Wert für die _CA_ Attribut der **CN = NTAuthCertificates** Container. |  
    |`gpupdate /force`     |Beschleunigt die Stammzertifikate für die Windows Server und Clientcomputer hinzufügen.  |

3.  Stellen Sie sicher, dass die Zertifikate der Stammzertifizierungsstelle in der Enterprise NTAuth-Speicher und werden als vertrauenswürdige vorhanden sind:

    a.  Melden Sie sich bei einem Server mit Administratorrechten für Unternehmen mit der **Tools zur Zertifikat** installiert.

    >[!NOTE]
    >In der Standardeinstellung die **Tools zur Zertifikat** sind installierte Server der Zertifizierungsstelle. Sie können auf anderen Servern Elemente als Teil des installiert werden die **Rollenverwaltungstools** im Server-Manager.

    b.  Geben Sie auf dem VPN-Server im Startmenü **pkiview.msc** auf das Unternehmens-PKI-Dialogfeld zu öffnen.

    c.  Geben Sie im Menü Start **pkiview.msc** auf das Unternehmens-PKI-Dialogfeld zu öffnen.

    d.  Mit der rechten Maustaste **Unternehmens-PKI** , und wählen Sie **Verwalten von AD-Container**.

    d.  Stellen Sie sicher, dass jedes Microsoft VPN-Stamm-CA-Gen 1-Zertifikat unter vorhanden ist:
      - NTAuthCertificates
      - AIA-Container
      - Certificate Authorities Container

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7.5: Erstellen Sie OMA-DM-basierte VPNv2-Profile auf Windows 10-Geräten](vpn-create-oma-dm-based-vpnv2-profiles.md): In diesem Schritt erstellen Sie können OMA-DM-basierte VPNv2-Profile, die mithilfe von Intune zum Bereitstellen einer Konfigurationsrichtlinie für VPN-Gerät. PowerShell-Skript zu SCCM VPNv2 Profile erstellen, finden Sie unter [VPNv2 CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) Weitere Details.
