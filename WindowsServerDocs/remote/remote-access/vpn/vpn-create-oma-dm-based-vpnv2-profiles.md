---
title: Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte
description: 'Sie können eine von zwei Methoden zum Erstellen von OMA-DM-basierte VPNv2-Profile. '
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
ms.openlocfilehash: 9051a5b4dc8055885bdc1f8f727514b6e049d74d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749503"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>Schritt 7.5. Erstellen Sie OMA-DM-basierte VPNv2-Profile für Windows 10-Geräte

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 7.4. Stammzertifikate für den bedingten Zugriff bereitstellen, auf das lokale Active Directory](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)
- [**nächster:** Erfahren Sie, wie der bedingte Zugriff für VPN-funktioniert](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

In diesem Schritt erstellen Sie können OMA-DM-basierte VPNv2-Profile, die mithilfe von Intune zum Bereitstellen einer Konfigurationsrichtlinie für VPN-Gerät. Wenn Sie SCCM oder PowerShell-Skript zum Erstellen von VPNv2-Profilen finden Sie unter verwenden möchten [VPNv2 CSP-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) Weitere Details. 

## <a name="managed-deployment-using-intune"></a>Verwaltete Bereitstellung mit Intune

Alles, was in diesem Abschnitt beschriebenen ist die Mindestanforderung für das VPN mit dem bedingten Zugriff funktionieren vornehmen. Es wird nicht als getrenntes Tunneln, WIP verwenden, Erstellen von benutzerdefinierten Intune-gerätekonfigurationsprofilen abzurufenden AutoVPN arbeiten oder SSO behandelt. Integrieren Sie die folgenden Einstellungen in das VPN-Profil, die Sie zuvor erstellt haben unter [Schritt 5. Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md).  In diesem Beispiel werden wir integrieren Sie sie in der [konfigurieren den VPN-Client mithilfe von Intune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) Richtlinie. 

**Voraussetzung:**

Windows 10-Client-Computer wurde bereits mit einer VPN-Verbindung mithilfe von Intune konfiguriert.   


**Vorgehensweise:**

1. Wählen Sie im Azure-Portal **Intune** > **Gerätekonfiguration** > **Profile** , und wählen Sie das VPN-Profil, die Sie zuvor erstellt[ Konfigurieren den VPN-Client mithilfe von Intune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune).
    
2. Wählen Sie in den Editor für Gruppenrichtlinien, **Eigenschaften** > **Einstellungen** > **Basis-VPN**. Erweitern Sie den vorhandenen **EAP-Xml** einen Filter enthalten, die dem VPN-Client die Logik bietet muss das Zertifikat für den bedingten Zugriff von AAD aus dem Zertifikatspeicher des Benutzers, statt dem Zufall ermöglicht es der ersten Verwendung bleiben abrufen das Zertifikat ermittelt.

    >[!NOTE]
    >Ohne diesen Schritt konnte der VPN-Client das Zertifikat ausgestellt, die von der Zertifizierungsstelle von einem lokalen abrufen, was zu einer fehlerhaften VPN-Verbindung.

    ![Intune-portal](../../media/Always-On-Vpn/intune-eap-xml.png)

3. Suchen Sie den Abschnitt mit der Endung  **\</AcceptServerName >\</EapType >** und fügen Sie die folgende Zeichenfolge zwischen diesen beiden Werten für die Logik für die AAD-bedingte wählen Sie den VPN-Client bereit Zertifikat für den Zugriff:

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. Wählen Sie die **für den bedingten Zugriff** auf dem Blatt "und" Toogle **Bedingter Zugriff für diese VPN-Verbindung** zu **aktiviert**.
   
   Aktivieren diese Einstellung ändert sich die  **\<DeviceCompliance >\<aktiviert > "true"\</aktiviert >** in der XML-VPNv2-Profil festlegen.

    ![Bedingter Zugriff für Always On-VPN - Eigenschaften](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

5. Wählen Sie **OK**.

6. Wählen Sie **Zuweisungen**, wählen Sie unter gehören **einzuschließende Gruppen auswählen**.

7. Wählen Sie die **VPN-Benutzer** Gruppe, die diese Richtlinie, und wählen Sie empfängt **speichern**.

    ![Obergrenze für die automatische VPN-Benutzer - Zuweisungen](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>Richtliniensynchronisierung für die Verwaltung mobiler Geräte auf dem Client zu erzwingen.

Wenn das VPN-Profil nicht auf dem Client-Gerät unter "Einstellungen" angezeigt wird\\Netzwerk und Internet\\VPN, Sie können erzwingen, dass MDM-Richtlinie, um zu synchronisieren.

1. Melden Sie sich bei einer Domäne eingebundenen Client-Computer als Mitglied der **VPN-Benutzer** Gruppe.

2. Geben Sie auf im Menü Start **Konto**, und drücken Sie EINGABETASTE.

3. Wählen Sie im linken Navigationsbereich **Zugriff auf Geschäfts-, Schul- oder unikonto**.

4. Wählen Sie unter den Zugriff auf Geschäfts-, Schul- oder unikonto, **< \domain > Verwaltung mobiler Geräte verbunden**, und wählen Sie dann **Informationen**.

5. Wählen Sie **Sync** und überprüfen Sie, ob das VPN-Profil wird angezeigt, unter "Einstellungen"\\Netzwerk und Internet\\VPN.


## <a name="next-steps"></a>Nächste Schritte

Sie anschließend das VPN-Profil, um die Verwendung des bedingten Zugriffs von Azure AD konfigurieren. 

|Wenn Sie möchten...  |Anzeige...  |
|---------|---------|
|Weitere Informationen zur Funktionsweise des bedingten Zugriffs mit VPNs  |[VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Diese Seite enthält weitere Informationen zur Funktionsweise des bedingten Zugriffs mit VPNs funktioniert.      |
|Erfahren Sie mehr über die erweiterten VPN-Funktionen  |[Erweiterte VPN-Features](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): Diese Seite enthält Anleitungen zur VPN-IP-Filter aktivieren, konfigurieren Sie automatische VPN-Verbindungen mithilfe von App-Trigger und Gewusst wie: Konfigurieren von NPS, um VPN-Verbindungen nur von Clients mithilfe von Azure AD ausgestellten Zertifikaten zu ermöglichen.        |


## <a name="related-topics"></a>Verwandte Themen

- [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):  Dieses Thema bietet einen Überblick über die VPNv2 CSP. Die Konfigurationsdienstanbieter VPNv2 kann die Verwaltungsserver mobiler Geräte (MDM) so konfigurieren Sie das VPN-Profil des Geräts.

- [Konfigurieren Sie Windows 10-Clientsysteme Always On-VPN-Verbindungen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): Dieses Thema enthält Informationen zu den Optionen für "profileXML" und das Schema, und wie Sie das ProfileXML VPN erstellen. Nachdem der Server-Infrastruktur eingerichtet haben, müssen Sie die Windows 10-Clientcomputern für die Kommunikation mit dieser Infrastruktur mit einer VPN-Verbindung konfigurieren. 

- [Konfigurieren den VPN-Client mithilfe von Intune](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune): Dieses Thema enthält Informationen zum Bereitstellen von Windows 10 Remote Access Always On-VPN-Profilen. Intune verwendet jetzt die Azure AD-Gruppen. Wenn Azure AD Connect die VPN-Benutzer-Gruppe aus dem lokalen mit Azure AD synchronisiert wird, klicken Sie dann besteht keine Notwendigkeit für die Konfiguration des VPN-Clients mithilfe von Intune.
