---
title: Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen
description: Ein EAP-TLS-Client kann keine Verbindung herstellen, es sei denn, der NPS-Server schließt eine Sperr Überprüfung der Zertifikatskette (einschließlich des Stamm Zertifikats) des Clients ab und überprüft, ob Zertifikate widerrufen wurden.
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: lizross
author: eross-msft
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: c58386467d632d77fdc96bf3bc18b5a85d1ecdaf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307706"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>Schritt 7.1. Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 7: Optionale Bedingter Zugriff für VPN-Konnektivität mithilfe von Azure AD](ad-ca-vpn-connectivity-windows10.md)
- [**Weiter:** Schritt 7,2. Stamm Zertifikate für die VPN-Authentifizierung mit Azure AD erstellen](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>Wenn diese Registrierungs Änderung nicht implementiert wird, treten bei IKEv2-Verbindungen mit cloudzertifikaten mit PEAP Fehler auf, aber IKEv2-Verbindungen mit Client Authentifizierungs Zertifikaten, die von der lokalen Zertifizierungsstelle ausgestellt werden, funktionieren weiterhin.

In diesem Schritt können Sie **IgnoreNoRevocationCheck** hinzufügen und festlegen, dass die Authentifizierung von Clients zulässig ist, wenn das Zertifikat keine CRL-Verteilungs Punkte enthält. Standardmäßig ist IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

>[!NOTE]
>Wenn ein Windows-Routing-und Remote Zugriffs Server (RRAS) NPS zum Proxy von RADIUS-Aufrufen an einen zweiten NPS verwendet, müssen Sie auf beiden Servern **IgnoreNoRevocationCheck = 1** festlegen.

Ein EAP-TLS-Client kann keine Verbindung herstellen, es sei denn, der NPS-Server schließt eine Sperr Überprüfung der Zertifikat Kette (einschließlich des Stamm Zertifikats) ab. Cloud-Zertifikate, die von Azure AD an den Benutzer ausgegeben werden, verfügen nicht über eine Zertifikat Sperr Liste, da es sich um kurzlebige Zertifikate mit einer Lebensdauer von einer Stunde handelt. EAP auf NPS muss so konfiguriert werden, dass das Fehlen einer CRL ignoriert wird. Standardmäßig ist IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt. Fügen Sie IgnoreNoRevocationCheck hinzu, und legen Sie es auf 1 fest, um die Authentifizierung von Clients zuzulassen, wenn das Zertifikat keine CRL-Verteilungs Punkte enthält. 

Da die Authentifizierungsmethode EAP-TLS ist, wird dieser Registrierungs Wert nur unter eap\13. benötigt. Wenn andere EAP-Authentifizierungsmethoden verwendet werden, sollte der Registrierungs Wert ebenfalls hinzugefügt werden. 

**Dringlichkeit**

1. Öffnen Sie " **Regedit. exe** " auf dem NPS-Server.

2. Navigieren Sie zu **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\rasman\ppp\eap\13**.

3. Wählen Sie **Edit > New** , und wählen Sie **DWORD-Wert (32-Bit)** aus, und geben Sie **IgnoreNoRevocationCheck**ein.

4. Doppelklicken Sie auf **IgnoreNoRevocationCheck** , und legen Sie die Wertdaten auf **1**fest.

5. Wählen Sie **OK** aus, und starten Sie den Server neu. Das Neustarten der RRAS-und NPS-Dienste genügt nicht.

Weitere Informationen finden Sie unter [Aktivieren oder Deaktivieren der Zertifikat Sperr Überprüfung (CRL) auf Clients](https://technet.microsoft.com/library/bb680540.aspx).


|Registrierungspfad  |EAP-Erweiterung  |
|---------|---------|
|Hklm\system\currentcontrolset\services\rasman\ppp\eap\13     |EAP-TLS         |
|Hklm\system\currentcontrolset\services\rasman\ppp\eap\25     |PEAP         |
|Hklm\system\currentcontrolset\services\rasman\ppp\eap\26     |EAP-MSCHAP V2         |

## <a name="next-steps"></a>Nächste Schritte

[Schritt 7,2. Erstellen von Stamm Zertifikaten für die VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md): in diesem Schritt konfigurieren Sie Stamm Zertifikate für den bedingten Zugriff für die VPN-Authentifizierung mit Azure AD, bei der automatisch eine VPN-Server-Cloud-App im Mandanten erstellt wird.
