---
title: Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen
description: Ein EAP-TLS-Client kann keine Verbindung herstellen, es sei denn, der Netzwerkrichtlinienserver abgeschlossen eine Überprüfung der Zertifikatkette ist (einschließlich des Stammzertifikats) des Clients und stellt sicher, dass Zertifikate gesperrt wurden.
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
ms.openlocfilehash: ac59c554c69a6138a106a648c3fab3ed4fe05b7b
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067372"
---
# Schritt 7.1. Konfigurieren von EAP-TLS, um ignorieren (Certificate Revocation List, CRL) überprüfen

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 7. (Optional) Bedingter Zugriff für VPN-Konnektivität mit Azure AD](ad-ca-vpn-connectivity-windows10.md)<br>
& #187; [ **Weiter:** Schritt 7.2. Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>Diese Änderung der Registrierung nicht implementiert bewirkt, dass IKEv2-Verbindungen, die mit der Cloud Zertifikate mit PEAP fehlschlägt, aber IKEv2-Verbindungen mit Client Auth Zertifikate, die von der lokalen Zertifizierungsstelle ausgestellt würde, funktionieren weiterhin.

In diesem Schritt können Sie **IgnoreNoRevocationCheck** hinzufügen und legen sie für die Authentifizierung von Clients zuzulassen, wenn das Zertifikat nicht Verteilungspunkte enthalten ist. Standardmäßig wird IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt.

>[!NOTE]
>Wenn ein Windows Routing- und RAS-Server (RRAS) verwendet NPS zum Proxy RADIUS aufruft, um eine zweite NPS, dann müssen Sie festlegen **IgnoreNoRevocationCheck = 1** auf beiden Servern.

Ein EAP-TLS-Client kann keine Verbindung herstellen, es sei denn, der Netzwerkrichtlinienserver eine Überprüfung der Zertifikatkette (einschließlich des Stammzertifikats) abgeschlossen ist. Cloud Zertifikaten für Benutzer von Azure AD müssen eine CRL keinen, da sie kurzlebige Zertifikate mit einer Lebensdauer von einer Stunde sind. EAP für NPS muss konfiguriert werden, um das Fehlen der Zertifikatsperrliste ignorieren. Standardmäßig wird IgnoreNoRevocationCheck auf 0 (deaktiviert) festgelegt. Fügen Sie IgnoreNoRevocationCheck hinzu, und legen sie den 1 um Authentifizierung von Clients zu ermöglichen, wenn das Zertifikat nicht Verteilungspunkte enthalten ist. 

Da die Authentifizierungsmethode EAP-TLS ist, ist dieses Registrierungswerts nur unter EAP\13 erforderlich. Wenn andere EAP-Authentifizierungsmethoden verwendet werden, sollte der Registrierungswert auch unter denen hinzugefügt. 

**Verfahren**

1. Öffnen Sie **regedit.exe** auf dem Netzwerkrichtlinienserver.

2. Navigieren Sie zu **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**.

3. Klicken Sie auf **Bearbeiten > neu** **DWORD-Wert (32-Bit)** wählen, und geben Sie **IgnoreNoRevocationCheck**.

4. Doppelklicken Sie auf **IgnoreNoRevocationCheck** , und legen Sie den Wert auf **1**.

5. Klicken Sie auf **OK** , und starten Sie den Server neu. Die Anzahl von RRAS NPS Dienste und reicht nicht aus.

Weitere Informationen finden Sie [Informationen zum Aktivieren oder deaktivieren Certificate Revocation überprüfen (CRL) auf Clients](https://technet.microsoft.com/library/bb680540.aspx).


|Registrierungspfad  |EAP-Erweiterung  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## Nächster Schritt

[Schritt 7.2. Erstellen von Stammzertifikaten für VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md): In diesem Schritt konfigurieren Sie Stammzertifikate bedingten Zugriff für VPN-Authentifizierung mit Azure AD automatisch eine VPN-Server Cloud-app im Mandanten erstellen. 

---