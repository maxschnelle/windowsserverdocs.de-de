---
title: Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen
description: Dieses Thema enthält Informationen zur Verwendung von Zertifikaten mit des Netzwerkrichtlinienservers und Remotezugriff in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2af0a1df-5c44-496b-ab11-5bc340dc96f0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 41f6f88705fa3d58be695fd825d960e7df21cd24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885881"
---
# <a name="configure-certificate-templates-for-peap-and-eap-requirements"></a>Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Alle Zertifikate, die zum Authentifizieren des Netzwerkzugriffs mit Extensible Authentication-Protokoll verwendet werden\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\- Transport Layer Security \(PEAP\-TLS\), und PEAP\-Microsoft Challenge Handshake Authentication Protocol Version 2 \(MS\-CHAP-v2\) müssen erfüllen die Anforderungen für x. 509-Zertifikate und funktioniert für Verbindungen, die Secure Socket Layer/Transport Level Security (SSL/TLS) verwenden. Sowohl Client-als auch Zertifikate gelten zusätzliche Anforderungen.

>[!IMPORTANT]
>Dieses Thema enthält Anweisungen zum Konfigurieren von Zertifikatvorlagen. Um diese Anweisungen verwenden zu können, ist es erforderlich, dass Sie Ihre eigenen Public Key-Infrastruktur bereitgestellt haben \(PKI\) mit Active Directory Certificate Services \(AD CS\).

## <a name="minimum-server-certificate-requirements"></a>Mindestanforderungen für Serverzertifikate

Mit PEAP\-MS\-CHAPv2 PEAP\-TLS oder EAP\-TLS als Authentifizierungsmethode aus, den NPS muss ein Serverzertifikat, das erfüllt die Mindestanforderungen für Serverzertifikate verwenden. 

Clientcomputer können so konfiguriert werden, dass die Serverzertifikate validieren, indem die **Serverzertifikat überprüfen** Option auf dem Clientcomputer oder in der Gruppenrichtlinie. 

Der Clientcomputer akzeptiert den Authentifizierungsversuch des Servers, wenn das Serverzertifikat die folgenden Anforderungen erfüllt:

- Der Name des Antragstellers enthält einen Wert an. Wenn Sie ein Zertifikat auf Ihrem Server unter Network Policy Server (NPS), die einem leerem Antragstellernamen ausgeben, ist das Zertifikat nicht verfügbar, um den NPS zu authentifizieren. So konfigurieren Sie die Zertifikatvorlage mit einem Antragstellernamen an:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Format des Antragstellernamens**, wählen Sie einen Wert als **keine**.

- Das Zertifikat auf dem Server-Ketten einer vertrauenswürdigen Stammzertifizierungsstelle (CA) und wird nicht einem Fehler der Überprüfungen, die von der CryptoAPI und, die ausgeführt werden in der RAS-Richtlinie oder eine Netzwerkrichtlinie angegeben werden.

- Das Zertifikat für den NPS oder VPN-Server wird mit den Zertifizierungszweck der Serverauthentifizierung in erweiterte Schlüsselverwendung (EKU)-Erweiterungen konfiguriert. (Die Objekt-ID für die Serverauthentifizierung ist 1.3.6.1.5.5.7.3.1.)

- Konfigurieren Sie das Serverzertifikat, mit der Einstellung für die Kryptografie erforderlich sind:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die **Kryptografie** Registerkarte, und stellen Sie sicher, dass Folgendes zu konfigurieren:
       - **Anbieterkategorie:** Schlüsselspeicheranbieter
       - **Name des Algorithmus:** RSA
       - **Anbieter:** Kryptografieanbieter für Microsoft-Plattform
       - **Minimale Schlüsselgröße:** 2.048
       - **Hashalgorithmus:** SHA2
    4. Klicken Sie auf **Weiter**.

- Wenn verwendet, muss die Erweiterung des alternativen Antragstellernamen (SubjectAltName), den DNS-Namen des Servers enthalten. So konfigurieren Sie die Zertifikatvorlage mit der Domain Name System (DNS) Name des Servers, der Registrierung 

    1. Öffnen Sie Zertifikatvorlagen.
    2. Im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Informationen im alternativen Antragstellernamen einbeziehen**Option **DNS-Namen**.

Bei Verwendung von PEAP und EAP-TLS anzeigen NPSs eine Liste aller installierten Zertifikate im Zertifikatspeicher Computers mit den folgenden Ausnahmen:

- Zertifikate, die nicht den Zertifizierungszweck der Serverauthentifizierung in EKU-Erweiterungen enthalten, werden nicht angezeigt.

- Zertifikate, die keinen Antragstellernamen enthalten, werden nicht angezeigt.

- Registrierungsbasierte und Smartcard-Anmeldung – Zertifikate werden nicht angezeigt.

Weitere Informationen finden Sie unter [Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="minimum-client-certificate-requirements"></a>Minimale Client-zertifikatanforderungen

EAP-TLS oder PEAP-TLS akzeptiert der Server den Authentifizierungsversuch Client, wenn das Zertifikat die folgenden Anforderungen erfüllt:

- Das Clientzertifikat von einer Unternehmenszertifizierungsstelle ausgestellt ist, oder eine Benutzer- oder Computerkonto in Active Directory Domain Services zugeordnet \(AD DS\).

- Die Benutzer- oder Computerzertifikats für die Client-Ketten für vertrauenswürdige Stamm-ZS, enthält den Zertifizierungszweck der Clientauthentifizierung im EKU-Erweiterungen \(die Objekt-ID für die Clientauthentifizierung wird 1.3.6.1.5.5.7.3.2\), und schlägt fehl, weder die überprüft, die von der CryptoAPI ausgeführt werden und dem angegebenen in RAS-Richtlinie oder Netzwerkrichtlinie und der Objekt-ID überprüft, die in der Netzwerkrichtlinie für NPS angegeben werden.

- Der 802.1X-Client verwendet nicht die Registrierung basierende Zertifikate, die entweder einer Smartcard-Anmeldung oder Zertifikate ein Kennwort geschützt.

- Für Benutzerzertifikate, die den alternativen Antragstellernamen \(SubjectAltName\) Erweiterung des Zertifikats enthält den Benutzerprinzipalnamen \(UPN\). So konfigurieren den UPN in einer Zertifikatvorlage:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Informationen im alternativen Antragstellernamen einbeziehen**Option **Benutzerprinzipalname \(UPN\)**.

- Für Computerzertifikate, die den alternativen Antragstellernamen \(SubjectAltName\) Erweiterung des Zertifikats muss den vollständig qualifizierten Domänennamen enthalten \(FQDN\) des Clients, die auch die aufgerufenwird *DNS-Namen*. So konfigurieren diesen Namen in der Zertifikatvorlage:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Informationen im alternativen Antragstellernamen einbeziehen**Option **DNS-Namen**.

Mit PEAP\-TLS und EAP\-TLS, Clients, die zeigen einer Liste aller installierten Zertifikate im Zertifikate-Snap-in mit den folgenden Ausnahmen:

- Drahtlose Clients nicht registrierungsbasierte anzeigen und Zertifikate für Smartcard-Anmeldung. 

- Drahtlose Clients und VPN-Clients werden keine Zertifikate ein Kennwort geschützt angezeigt. 

- Zertifikate, die nicht den Zertifizierungszweck der Clientauthentifizierung im EKU-Erweiterungen enthalten, werden nicht angezeigt.


Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
