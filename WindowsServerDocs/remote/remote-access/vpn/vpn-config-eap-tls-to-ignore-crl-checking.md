---
title: Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen
description: Ein EAP-TLS-Client keine Verbindung herstellen, es sei denn, der NPS-Server eine sperrungsüberprüfung der Zertifikatkette des Clients (einschließlich des Stammzertifikats) abgeschlossen, und stellt sicher, dass Zertifikate widerrufen wurden.
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
ms.openlocfilehash: 781239f45b9b260b7d374c2a6972cdb8faad2879
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749595"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>Schritt 7.1. Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 7 (Optional) Bedingter Zugriff für VPN-Verbindungen mithilfe von Azure AD](ad-ca-vpn-connectivity-windows10.md)
- [**nächster:** Schritt 7.2. Erstellen von Stammzertifikaten für die VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>Fehler beim Implementieren Sie diese registrierungsänderung führt dazu, dass IKEv2-Verbindungen mithilfe von Cloud-Zertifikaten mit PEAP fehlschlägt, aber die IKEv2-Verbindungen, die von der lokalen-Zertifizierungsstelle ausgestellten Zertifikate für Client-Authentifizierung verwenden würde auch weiterhin funktionieren.

Sie können in diesem Schritt hinzufügen **IgnoreNoRevocationCheck** und legen Sie ihn auf die Authentifizierung von Clients zuzulassen, wenn das Zertifikat keine Sperrlisten-Verteilungspunkte enthält. Standardmäßig wird die IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

>[!NOTE]
>Wenn eine Windows-Routing und RAS-Server (RRAS) verwendet NPS zum Proxy RADIUS aufruft, um eine zweite NPS, dann müssen Sie festlegen **IgnoreNoRevocationCheck = 1** auf beiden Servern.

Ein EAP-TLS-Client keine Verbindung herstellen, es sei denn, der NPS-Server eine sperrungsüberprüfung der Zertifikatkette (einschließlich des Stammzertifikats) abgeschlossen ist. Cloud-Zertifikate, die für den Benutzer von Azure AD ausgestellten müssen keine Zertifikatsperrliste, da sie kurzlebige Zertifikate über eine Gültigkeitsdauer von einer Stunde sind. EAP für NPS muss konfiguriert werden, um das Fehlen einer Zertifikatsperrliste zu ignorieren. Standardmäßig wird die IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt. Fügen Sie IgnoreNoRevocationCheck hinzu, und legen Sie ihn auf 1 fest, um die Authentifizierung von Clients zuzulassen, wenn das Zertifikat keine Sperrlisten-Verteilungspunkte enthält. 

Da die Authentifizierungsmethode EAP-TLS ist, ist dieser Wert nur unter EAP\13 erforderlich. Wenn andere EAP-Authentifizierungsmethoden verwendet werden, sollte der Registrierungswert sowie unterhalb dieser hinzugefügt. 

**Verfahren**

1. Open **regedit.exe** auf dem NPS-Server.

2. Navigieren Sie zu **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**.

3. Wählen Sie **Bearbeiten > New** , und wählen Sie **DWORD-Wert (32-Bit)** , und geben Sie **IgnoreNoRevocationCheck**.

4. Doppelklicken Sie auf **IgnoreNoRevocationCheck** und legen Sie die Wertdaten auf **1**.

5. Wählen Sie **OK** und starten Sie den Server. Es reicht nicht aus, das RRAS und NPS-Dienste neu zu starten.

Weitere Informationen finden Sie unter [aktivieren oder Deaktivieren von Zertifikat-Sperrung überprüfen (CRL) auf Clients](https://technet.microsoft.com/library/bb680540.aspx).


|Registrierungspfad  |EAP-Erweiterung  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7.2: Stammzertifikate für die VPN-Authentifizierung mit Azure AD erstellen](vpn-create-root-cert-for-vpn-auth-azure-ad.md): In diesem Schritt konfigurieren Sie die Stammzertifikate für den bedingten Zugriff für VPN-Authentifizierung mit Azure AD, die automatisch eine VPN-Server-Cloud-app im Mandanten erstellt.
