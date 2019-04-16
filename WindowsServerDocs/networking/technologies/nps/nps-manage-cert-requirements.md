---
title: Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen
description: Dieses Thema enthält Informationen zur Verwendung von Zertifikaten mit der Netzwerkrichtlinienserver und Remote Access in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2af0a1df-5c44-496b-ab11-5bc340dc96f0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e597a65982aeead907c9a41f17f1785a0bf81016
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-certificate-templates-for-peap-and-eap-requirements"></a>Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Alle Zertifikate, die für die Netzwerkzugriffsauthentifizierung mit Extensible Authentication Protocol\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\-Transport Layer Security \(PEAP\-TLS\) und PEAP\-Microsoft Challenge Handshake Authentication Protocol Version 2 verwendet werden \ (MS\ CHAP v2\) erfüllt die Anforderungen für x. 509-Zertifikate und für Verbindungen, die Secure Socket Layer/Transport Level Security (SSL/TLS) verwenden. Client- und Serverzertifikate gelten zusätzliche Anforderungen.

>[!IMPORTANT]
>Dieses Thema enthält Anweisungen zum Konfigurieren von Zertifikatvorlagen. Um diese Anweisungen zu verwenden, ist es erforderlich, dass Sie Ihre eigenen \(PKI\) Public Key-Infrastruktur mit Active Directory Certificate Services \(AD CS\) bereitgestellt haben.

## <a name="minimum-server-certificate-requirements"></a>Mindestanforderungen für Serverzertifikate

Mit PEAP\-MS\-CHAP v2, PEAP\-TLS oder EAP\-TLS als Authentifizierungsmethode muss der NPS-Server ein Serverzertifikat verwenden, die die Mindestanforderungen für Serverzertifikate entspricht. 

Client-Computer so konfiguriert werden, überprüfen Serverzertifikate mithilfe der **Serverzertifikat** Option auf dem Clientcomputer oder in der Gruppenrichtlinie. 

Der Client-Computer akzeptiert den Authentifizierungsversuch des Servers, wenn das Zertifikat die folgenden Anforderungen erfüllt:

- Der Name des Antragstellers enthält einen Wert. Wenn Sie ein Zertifikat mit dem Server mit Network Policy Server (NPS), die eine leerem Antragstellernamen ausstellen, ist das Zertifikat nicht verfügbar, auf den NPS-Server zu authentifizieren. So konfigurieren die Zertifikatvorlage mit einem Antragstellernamen an:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Format des Antragstellernamens**, wählen Sie einen Wert als **keine**.

- Das Zertifikat auf den Server-Ketten zu einer vertrauenswürdigen Stammzertifizierungsstelle (CA), jedoch keine Fehler auftreten, die überprüft, die vom CryptoAPI und, die ausgeführt werden, in der RAS-Richtlinie oder Netzwerkrichtlinie angegeben werden.

- Das Zertifikat für den NPS-Server oder VPN-Server wird mit Serverauthentifizierung in erweiterte Schlüsselverwendung (EKU)-Erweiterungen konfiguriert. (Die Objekt-ID für die Serverauthentifizierung ist 1.3.6.1.5.5.7.3.1.)

- Das Serverzertifikat ist konfiguriert, mit dem Algorithmuswert erforderlichen **RSA**. So konfigurieren Sie die erforderlichen Kryptografieeinstellung:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die **Kryptografie** Registerkarte. In **Name des Algorithmus**, klicken Sie auf **RSA**. Stellen Sie sicher, dass **minimale Schlüsselgröße** läuft **2048**.

- Verwendet, muss die Erweiterung alternativen Antragstellernamen (SubjectAltName) der DNS-Name des Servers enthalten. So konfigurieren die Zertifikatvorlage mit den Domain Name System (DNS)-Namen des Registrierungsservers: 

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Informationen im alternativen Antragstellernamen einbeziehen**Option **DNS-Namen**.

Bei Verwendung von PEAP und EAP-TLS zeigen NPS-Server eine Liste aller installierten Zertifikate im Zertifikatspeicher Computers mit den folgenden Ausnahmen:

- Zertifikate, die keine Serverauthentifizierung in EKU-Erweiterungen enthalten, werden nicht angezeigt.

- Zertifikate, die keinen Antragstellernamen enthalten, werden nicht angezeigt.

- Registrierungsbasierte und Smartcard-Anmeldung Zertifikate werden nicht angezeigt.

Weitere Informationen finden Sie unter [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="minimum-client-certificate-requirements"></a>Minimale Client-zertifikatanforderungen

Mit EAP-TLS oder PEAP-TLS akzeptiert der Server den Client Authentifizierungsversuch, wenn das Zertifikat die folgenden Anforderungen erfüllt:

- Das Clientzertifikat ist von einer Unternehmenszertifizierungsstelle ausgestellt oder um ein Benutzer- oder Computerkonto in Active Directory Domain Services \(AD DS\) zugeordnet.

- Das Zertifikat für Benutzer oder Computer auf die Client-Ketten zu einer vertrauenswürdigen Stammzertifizierungsstelle, enthält die Clientauthentifizierung in EKU-Erweiterungen \ (die Objekt-ID für die Clientauthentifizierung ist 1.3.6.1.5.5.7.3.2\), und ein Fehler auftritt, das überprüft werden, die von CryptoAPI ausgeführt und in der RAS-Richtlinie oder Netzwerkrichtlinie angegeben werden weder die Zertifikat-Objekt-ID überprüft, ob der in der NPS-Netzwerkrichtlinien angegeben sind.

- Der 802.1X-Client verwendet keine registrierungsbasierten Zertifikate, die entweder Smartcard-Anmeldung oder Zertifikate ein Kennwort geschützt.

- Für Benutzerzertifikate enthält die Erweiterung für die \(SubjectAltName\) Alternativer Antragstellername im Zertifikat den Benutzerprinzipalnamen \(UPN\) nennen. So konfigurieren Sie den UPN in einer Zertifikatvorlage

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Informationen im alternativen Antragstellernamen einbeziehen**Option **User Principal name \(UPN\)**.

- Bei Computerzertifikaten \(SubjectAltName\) Erweiterung der alternativen Antragstellernamen des Zertifikats muss den vollqualifizierten Domänennamen enthalten Namen \(FQDN\) des Clients, die auch aufgerufen wird, die *DNS-Namen*. Dieser Name in der Zertifikatvorlage konfigurieren:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailbereich mit der Maustaste der Zertifikatvorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die **Antragstellername** Registerkarte, und klicken Sie dann auf **aus diesen Informationen in Active Directory erstellen**.
    4. In **Informationen im alternativen Antragstellernamen einbeziehen**Option **DNS-Namen**.

Bei PEAP\-TLS und EAP\ TLS zeigen Clients eine Liste aller installierten Zertifikate im Zertifikate-Snap-in mit den folgenden Ausnahmen:

- Drahtlose Clients zeigen keine registrierungsbasierte und Smartcard-Anmeldung Zertifikate. 

- Drahtlose Clients und VPN-Clients zeigen keine kennwortgeschützten Zertifikate an. 

- Zertifikate, die nicht die Clientauthentifizierung in EKU-Erweiterungen enthalten, werden nicht angezeigt.


Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
