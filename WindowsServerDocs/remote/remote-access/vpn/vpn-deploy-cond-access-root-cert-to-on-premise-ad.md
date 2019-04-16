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
ms.openlocfilehash: 210540846f5d62dfc74a2e629a6b7675ccf9894d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067308"
---
# Schritt 7.4. Bereitstellen von Stammzertifikate bedingten Zugriff auf lokale AD

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

Sie stellen in diesem Schritt das Stammzertifikat für bedingten Zugriff als vertrauenswürdiges Stammzertifikat für VPN-Authentifizierung zu Ihrer lokalen AD.

& #171;  [ **Vorherigen:** Schritt 7.3. Konfigurieren Sie die Richtlinie für bedingten Zugriff](vpn-config-conditional-access-policy.md)<br>
& #187; [ **Weiter:** Schritt 7.5. Erstellen Sie OMA-DM-basierte VPNv2-Profile für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. Klicken Sie auf der Seite **VPN-Verbindung** auf **Zertifikat herunterladen**. 
   
    ![Download des Zertifikats für bedingten Zugriff](../../media/Always-On-Vpn/06.png)

    >[!NOTE]
    >Die Option **herunterladen base64-Zertifikat** ist für einige Konfigurationen, die base64-Zertifikate für die Bereitstellung erforderlich sind verfügbar. 

2. Melden Sie sich bei einer Domäne beigetretenen Computers mit Administratorrechten Enterprise, und führen Sie diese Befehle über eine Eingabeaufforderung mit Administratorrechten aus der Cloud Root-Zertifikate in den *Enterprise NTAuth-* Speicher hinzufügen:

    >[!NOTE]
    >Für Umgebungen, in denen der VPN-Server nicht zur Active Directory-Domäne verknüpft ist, müssen die Cloud Stammzertifikate im Speicher für _Vertrauenswürdige Stammzertifizierungsstellen_ manuell hinzugefügt werden.

    |Befehl  |Beschreibung  |  
    |---------|-------------| 
    |`certutil -dspublish -f VpnCert.cer RootCA`     |Erstellt zwei **Microsoft-VPN-Root CA Generation 1** -Container unter den **CN = AIA** und **CN = Zertifizierungsstellen** Container, und jede Stammzertifikat als Wert des Attributs _cACertificate_ beide **Microsoft VPN Stammknotens veröffentlicht Zertifizierungsstelle Generation 1** Container.|  
    |`certutil -dspublish -f VpnCert.cer NTAuthCA`   |Erstellt eine **CN = NTAuthCertificates** Container unter der **CN = AIA** und **CN = Zertifizierungsstellen** -Containern und veröffentlicht jeden Stammzertifikat als Wert des Attributs _cACertificate_ von der **CN = NTAuthCertificates** Container. |  
    |`gpupdate /force`     |Beschleunigt die Stammzertifikate für die WindowsServer und Clientcomputer hinzufügen.  |

3.  Stellen Sie sicher, dass die Stammzertifikate in den Enterprise NTAuth-Speicher und anzeigen als vertrauenswürdig vorhanden sind:

    a.  Melden Sie sich auf einem Server mit Unternehmensadministrators Rechte, der das **Zertifikat Autorität-Verwaltungstools** installiert sind.

    >[!NOTE]
    >Standardmäßig die **Certificate Authority Management-Tools** sind installierte Zertifizierungsstelle Server. Sie können auf anderen Servern Mitglieder im Rahmen der **Rollenverwaltungstools** im Server-Manager installiert werden.

    b.  Geben Sie auf der VPN-Server im Menü "Start" **pkiview.msc** , um das Dialogfeld "Unternehmens-PKI" zu öffnen.

    c.  Geben Sie aus dem Menü "Start" **pkiview.msc** , um das Dialogfeld "Unternehmens-PKI" zu öffnen.

    d.  Mit der rechten Maustaste **Unternehmens-PKI** , und wählen Sie **AD-Container verwalten**.

    d.  Stellen Sie sicher, dass jedes Zertifikat Microsoft VPN Stammzertifizierungsstelle Generation 1 unter vorhanden ist:<ul><li>NTAuthCertificates</li><li>AIA-Container</li><li>Zertifikat Behörden Container</li></ul>

    
## Nächster Schritt
[Schritt 7.5. Erstellen Sie OMA-DM-basierte VPNv2-Profile für Windows 10-Geräte](vpn-create-oma-dm-based-vpnv2-profiles.md): In diesem Schritt erstellen Sie OMA-DM-basierte VPNv2-Profilen mithilfe von Intune zum Bereitstellen einer VPN-Gerätekonfiguration Richtlinie. Wenn Sie SCCM oder PowerShell-Skript VPNv2-Profile erstellen möchten, finden Sie unter [VPNv2-CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) Weitere Details.

---
