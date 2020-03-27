---
title: Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen
description: Dieses Thema enthält Informationen zur Verwendung von Zertifikaten mit dem Netzwerk Richtlinien Server und Remote Zugriff in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2af0a1df-5c44-496b-ab11-5bc340dc96f0
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c2593c2739728704a59cde169de28ed0ae979419
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316086"
---
# <a name="configure-certificate-templates-for-peap-and-eap-requirements"></a>Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Alle Zertifikate, die für die Netzwerk Zugriffs Authentifizierung mit dem Extensible Authentication-Protokoll\-Transport Layer Security \(EAP\-TLS\), Protected Extensible Authentication Protocol\-Transport Layer Security \(PEAP\-TLS\)und PEAP\-Microsoft Challenge Handshake Authentication Protocol Version 2 \(MS\-CHAP v2\) verwendet werden, müssen die Anforderungen für X. 509-Zertifikate erfüllen und für Verbindungen mit SSL/TLS (Secure Socket Layer)/Transport Level Security (SSL/TLS). Sowohl Client-als auch Server Zertifikate haben zusätzliche Anforderungen.

>[!IMPORTANT]
>Dieses Thema enthält Anweisungen zum Konfigurieren von Zertifikat Vorlagen. Um diese Anweisungen zu verwenden, ist es erforderlich, dass Sie Ihre eigene Public Key-Infrastruktur \(PKI-\) mit Active Directory Zertifikat Diensten \(AD CS-\)bereitgestellt haben.

## <a name="minimum-server-certificate-requirements"></a>Mindestanforderungen für Server Zertifikate

Mit PEAP\-MS\-CHAP v2, PEAP\-TLS oder EAP\-TLS als Authentifizierungsmethode muss der NPS ein Serverzertifikat verwenden, das die Mindestanforderungen für das Serverzertifikat erfüllt. 

Client Computer können mithilfe der Option **Serverzertifikat** überprüfen auf dem Client Computer oder in Gruppenrichtlinie für die Überprüfung von Server Zertifikaten konfiguriert werden. 

Der Client Computer akzeptiert den Authentifizierungs Versuch des Servers, wenn das Serverzertifikat die folgenden Anforderungen erfüllt:

- Der Antragsteller Name enthält einen Wert. Wenn Sie für den Server, auf dem der Netzwerk Richtlinien Server (Network Policy Server, NPS) mit einem leeren Antragsteller Namen ausgeführt wird, ein Zertifikat ausstellen, ist das Zertifikat nicht zum Authentifizieren Ihres NPS verfügbar. So konfigurieren Sie die Zertifikat Vorlage mit einem Antragsteller Namen:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailfenster mit der rechten Maustaste auf die Zertifikat Vorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .
    3. Klicken Sie auf die Registerkarte Antragsteller **Name** , und klicken Sie dann auf **aus diesen Active Directory Informationen erstellen**.
    4. Wählen Sie unter Format des Antragsteller **namens**einen anderen Wert als **None**aus.

- Das Computer Zertifikat auf dem-Server ist mit einer vertrauenswürdigen Stamm Zertifizierungsstelle (Certification Authority, ca) verkettet. bei den Überprüfungen, die von CryptoAPI ausgeführt werden und die in der RAS-Richtlinie oder der Netzwerk Richtlinie angegeben sind, tritt ein Fehler auf.

- Das Computer Zertifikat für den NPS-oder VPN-Server wird in Erweiterungen der erweiterten Schlüssel Verwendung (Extended Key Usage, EKU) mit dem Zweck der Server Authentifizierung konfiguriert. (Der Objekt Bezeichner für die Server Authentifizierung lautet 1.3.6.1.5.5.7.3.1.)

- Konfigurieren Sie das Serverzertifikat mit der erforderlichen Kryptografieeinstellung:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailfenster mit der rechten Maustaste auf die Zertifikat Vorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die Registerkarte **Cryptography** , und stellen Sie sicher, dass Sie Folgendes konfigurieren:
       - **Anbieter Kategorie:** Schlüsselspeicher Anbieter
       - **Algorithmusname:** RSA
       - **Anbieter:** Kryptografieanbieter von Microsoft Platform
       - **Minimale Schlüsselgröße:** 2048
       - **Hash Algorithmus:** SHA2
    4. Klicken Sie auf **Weiter**.

- Bei Verwendung der Erweiterung alternativer Antragsteller Name (Subjektname) muss der DNS-Name des Servers enthalten sein. So konfigurieren Sie die Zertifikat Vorlage mit dem Domain Name System (DNS)-Namen des Registrierungs Servers: 

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailfenster mit der rechten Maustaste auf die Zertifikat Vorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften** .
    3. Klicken Sie auf die Registerkarte Antragsteller **Name** , und klicken Sie dann auf **aus diesen Active Directory Informationen erstellen**.
    4. Wählen Sie unter **diese Informationen in alternativen Antragsteller Namen einbeziehen**die Option **DNS-Name**aus.

Wenn Sie PEAP und EAP-TLS verwenden, zeigen Sie mit den folgenden Ausnahmen eine Liste aller installierten Zertifikate im Zertifikat Speicher des Computers an:

- Zertifikate, die den Zweck der Server Authentifizierung in EKU-Erweiterungen nicht enthalten, werden nicht angezeigt.

- Zertifikate, die keinen Antragsteller Namen enthalten, werden nicht angezeigt.

- Registrierungs basierte und Smartcard-Anmelde Zertifikate werden nicht angezeigt.

Weitere Informationen finden Sie unter Bereitstellen [von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="minimum-client-certificate-requirements"></a>Mindestanforderungen für Client Zertifikate

Mit EAP-TLS oder PEAP-TLS akzeptiert der Server den Client Authentifizierungs Versuch, wenn das Zertifikat die folgenden Anforderungen erfüllt:

- Das Client Zertifikat wird von einer Unternehmens Zertifizierungsstelle ausgestellt oder einem Benutzer-oder Computer Konto in Active Directory Domain Services \(AD DS\)zugeordnet.

- Das Benutzer-oder Computer Zertifikat auf dem Client ist mit einer vertrauenswürdigen Stamm Zertifizierungsstelle verkettet, umfasst den Zweck der Client Authentifizierung in EKU-Erweiterungen, \(der Objekt Bezeichner für die Client Authentifizierung 1.3.6.1.5.5.7.3.2\)ist und weder die von CryptoAPI ausgeführten Überprüfungen, die in der Remote Zugriffs Richtlinie bzw

- Der 802.1 x-Client verwendet keine Registrierungs basierten Zertifikate, bei denen es sich entweder um Smartcard-Anmelde-oder Kenn Wort geschützte Zertifikate handelt.

- Bei Benutzer Zertifikaten enthält der alternative Antragsteller Name \(subjetaltname\) Erweiterung im Zertifikat den Benutzer Prinzipal Namen \(UPN-\). So konfigurieren Sie den UPN in einer Zertifikat Vorlage:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailfenster mit der rechten Maustaste auf die Zertifikat Vorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die Registerkarte Antragsteller **Name** , und klicken Sie dann auf **aus diesen Active Directory Informationen erstellen**.
    4. Wählen Sie unter **diese Informationen in alternativen Antragsteller Namen einbeziehen**die Option **Benutzer Prinzipal Name \(UPN\)** aus.

- Für Computer Zertifikate muss der alternative Antragsteller Name \("subjetaltname"\) Erweiterung im Zertifikat den voll qualifizierten Domänen Namen \(FQDN\) des Clients enthalten, der auch als *DNS-Name*bezeichnet wird. So konfigurieren Sie diesen Namen in der Zertifikat Vorlage:

    1. Öffnen Sie Zertifikatvorlagen.
    2. Klicken Sie im Detailfenster mit der rechten Maustaste auf die Zertifikat Vorlage, die Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.
    3. Klicken Sie auf die Registerkarte Antragsteller **Name** , und klicken Sie dann auf **aus diesen Active Directory Informationen erstellen**.
    4. Wählen Sie unter **diese Informationen in alternativen Antragsteller Namen einbeziehen**die Option **DNS-Name**aus.

Mit PEAP\-TLS und EAP\-TLS zeigen Clients eine Liste aller installierten Zertifikate im Zertifikate-Snap-in mit den folgenden Ausnahmen an:

- Drahtlose Clients zeigen keine Registrierungs basierten und Smartcard-Anmelde Zertifikate an. 

- Bei drahtlosen Clients und VPN-Clients werden Kenn Wort geschützte Zertifikate nicht angezeigt. 

- Zertifikate, die nicht den Client Authentifizierungs Zweck in EKU-Erweiterungen enthalten, werden nicht angezeigt.


Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
