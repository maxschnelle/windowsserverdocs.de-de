---
title: Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte
description: 'Sie können einen von zwei Methoden zum Erstellen von OMA-DM-basierten VPNv2-Profilen. '
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 1ce20d09c304b26e3708429cc45da06d020e5809
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031294"
---
# Schritt 7.5. Erstellen der OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 7.4. Bereitstellen von Stammzertifikate für bedingten Zugriff auf lokale AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)<br>
& #187; [ **Weiter:** erfahren Sie, wie bedingten Zugriff für VPN-funktioniert](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

In diesem Schritt erstellen Sie OMA-DM-basierten VPNv2-Profilen mithilfe von Intune zum Bereitstellen einer VPN-Gerätekonfiguration-Richtlinie. Wenn Sie SCCM oder PowerShell-Skript verwenden, um VPNv2-Profilen erstellen möchten, finden Sie unter [VPNv2-CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) , Weitere Informationen. 

## Verwaltete Bereitstellung mithilfe von Intune

Alles, was in diesem Abschnitt erläuterten ist mindestens benötigt, damit VPN mit bedingtem Zugriff arbeiten kann. Es werden keine Split-Tunneling, mithilfe von WIP, Erstellen von benutzerdefinierten Intune Gerät Konfigurationsprofile abzurufenden AutoVPN arbeiten oder SSO behandelt. Integrieren Sie die Einstellungen unter in das VPN-Profil, die, das Sie zuvor unter [Schritt 5 erstellt haben. Konfigurieren von Windows 10-Client immer auf VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md).In diesem Beispiel werden wir sie in der [Konfigurieren der VPN-Client mithilfe von Intune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) -Richtlinie integrieren. 

**Voraussetzung:**<p>
Windows 10-Clientcomputer wurde bereits mit einer VPN-Verbindung mithilfe von Intune konfiguriert wurde.   


**Verfahren:**

1. Klicken Sie im Azure-Portal auf **Intune** > **Gerätekonfiguration** > **Profile** und wählen Sie das VPN-Profil erstellt Sie weiter oben in [der VPN-Client mithilfe von Intune konfigurieren](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune).
    
2. Wählen Sie im Gruppenrichtlinien-Editor, **Eigenschaften** > **Einstellungen** > **Base VPN**. Erweitern Sie die vorhandenen **EAP-Xml** um einen Filter einzuschließen, der dem VPN-Client die Logik, die es das AAD bedingten Zugriff Zertifikat aus Zertifikatspeicher ermöglicht anstelle von verlassen, um Wahrscheinlichkeit ermöglicht das erste Zertifikat des Benutzers abrufen muss ermittelt.

    >[!NOTE]
    >Ohne diese konnte der VPN-Client das Zertifikat von der lokalen Zertifizierungsstelle ausgestellt abrufen, was zu einer fehlgeschlagenen VPN-Verbindung.

    ![Intune-portal](../../media/Always-On-Vpn/intune-eap-xml.png)

3. Suchen Sie den Abschnitt, der mit **\</AcceptServerName>\</EapType>** endet, und fügen Sie die folgende Zeichenfolge zwischen diesen beiden Werten bereitstellen den VPN-Client mit der Logik der AAD bedingten Zugriff Zertifikat auswählen:

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. Wählen Sie die **Bedingten Zugriff** Blatt und Toogle **Bedingter Zugriff für diese VPN-Verbindung** **aktiviert**.<p>Aktivieren dieser Einstellung ändert die **\<DeviceCompliance>\<Enabled>true\</Enabled>** in den VPNv2-Profil-XML-Code festlegen.

    ![Bedingter Zugriff für Always On VPN - Eigenschaften](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

6. Klicken Sie auf **OK**.

6. Wählen Sie **Aufgaben**unter einschließen, klicken Sie auf **Gruppen eingeschlossen auswählen**.

7. Wählen Sie die **VPN-Benutzer** -Gruppe, die diese Richtlinie empfängt, und klicken Sie auf **Speichern**.

    ![Obergrenze für die automatische VPN-Benutzer - Aufgaben](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## Erzwingen Sie MDM-Richtlinie Synchronisierung, auf dem Client
Wenn das VPN-Profil nicht auf dem Clientgerät unter Settings\\Network & Internet\\VPN, angezeigt wird, können Sie MDM-Richtlinie für die Synchronisierung erzwingen.

1. Melden Sie sich für einen Client Domäne als Mitglied der Gruppe **VPN-Benutzer** .

2. Das Menü "Start" Geben Sie **ein**, und drücken Sie die EINGABETASTE.

3.  Klicken Sie im linken Navigationsbereich auf **Arbeits- oder schulkonto zugreifen**.

5.  Klicken Sie unter Geschäfts- oder schulkonto öffnen auf **verbunden mit <\domain> MDM** , und klicken Sie auf **Informationen**.

6.  Klicken Sie auf **Synchronisieren** , und stellen Sie sicher, dass das VPN-Profil unter Settings\\Network & Internet\\VPN angezeigt wird.


## Nächster Schritt
Sie konfigurieren das VPN-Profil, um bedingte Azure AD-Zugang zu verwenden. 

|Wenn Sie möchten...  |Anzeige...  |
|---------|---------|
|Erfahren Sie mehr über wie bedingten Zugriff funktioniert mit VPNs  |[VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Diese Seite enthält weitere Informationen über den wie bedingten Zugriff funktioniert mit VPNs.      |
|Erfahren Sie mehr über die erweiterten VPN-features  |[Erweiterte VPN-Funktionen](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): Diese Seite enthält Informationen zum Aktivieren der VPN-Datenverkehrsfilter, so konfigurieren Sie die automatische VPN-Verbindungen mit App-Triggern und so konfigurieren Sie NPS, damit nur VPN-Verbindungen von Clients mithilfe von Azure ausgestellte Zertifikate AD.        |


---

## Verwandte Themen
- [VPNv2-CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp): in diesem Thema bietet eine Übersicht über VPNv2-CSP. Der VPNv2-Konfigurationsdienstanbieter ermöglicht den Verwaltungsserver mobiler Geräte (MDM) zum Konfigurieren von VPN-Profil des Geräts.

- [Konfigurieren von Windows 10 Client immer auf VPN-Verbindungen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): Dieses Thema enthält Informationen zu den ProfileXML-Optionen und Schema und so die ProfileXML VPN erstellen. Nach dem Einrichten der Server-Infrastruktur, müssen Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung konfigurieren. 

- [Konfigurieren der VPN-Client mithilfe von Intune](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune): Dieses Thema enthält Informationen zur Verwendung von Windows 10 Remote Access Always On VPN-Profile bereitzustellen. Intune verwendet nun Azure AD-Gruppen. Wenn Sie Azure AD Connect VPN-Gruppe Benutzer lokale Azure AD synchronisiert, dann besteht keine Notwendigkeit für die Konfiguration des VPN-Clients mithilfe von Intune.

---
