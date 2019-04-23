---
ms.assetid: 98c5ef45-2bcb-4f87-86c8-5ac6c16a6097
title: Tokensignaturzertifikate
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a047b94906cf703bb934c93f517b8874af91e092
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864061"
---
# <a name="token-signing-certificates"></a>Tokensignaturzertifikate

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verbundserver erfordern Token\-Signaturzertifikate zum hindert Angreifer daran, ändern oder zu fälschen Sicherheitstoken zu versuchen, Zugriff auf verbundene Ressourcen zu erlangen. Die Private\/öffentliche Schlüssel, die Kopplung, wird verwendet, mit Token\-Signieren von Zertifikaten ist der wichtigsten Überprüfungsmechanismus alle verbundenen Partnerschaft, da diese Schlüssel stellen Sie sicher, dass ein Sicherheitstoken von einem gültigen Partner ausgestellt wurde Verbundserver und, dass das Token während der Übertragung nicht geändert wurde.  
  
## <a name="token-signing-certificate-requirements"></a>Token\-signaturanforderungen für Zertifikat  
Ein Token\-Signaturzertifikat muss zur Verwendung von AD FS die folgenden Anforderungen erfüllen:  
  
-   Für ein Token\-Signaturzertifikat ein Sicherheitstokens, das Token wurde erfolgreich signiert\-Signaturzertifikat muss einen privaten Schlüssel enthalten.  
  
-   Das AD FS-Dienstkonto benötigen Zugriff auf das Token\-Signieren der private Schlüssel des Zertifikats im persönlichen Speicher des lokalen Computers. Dies wird vom Setup übernommen. Sie können auch die AD FS-Verwaltungs-Snap\-um diesen Zugriff sicherzustellen, wenn Sie anschließend das Token ändern\-Signaturzertifikat.  
  
> [!NOTE]  
> Es ist eine public Key-Infrastruktur \(PKI\) am besten, empfiehlt es sich nicht die Freigabe den privaten Schlüssel für mehrere Zwecke. Aus diesem Grund verwenden Sie nicht das dienstkommunikationszertifikat, die Sie installiert haben, auf dem Verbundserver als Token\-Signaturzertifikat.  
  
## <a name="how-token-signing-certificates-are-used-across-partners"></a>Wie die symbolische\-Signaturzertifikate dienen für Partner  
Jedes Token\-Signaturzertifikat enthält, kryptografische private und öffentliche Schlüssel, die verwendet werden, zum digitalen Signieren von \(mit dem privaten Schlüssel\) ein Sicherheitstoken. Nachdem sie von einem Partnerverbundserver empfangen wurden, überprüfen diese Schlüssel später die Echtheit \(mit dem öffentlichen Schlüssel\) des verschlüsselten Sicherheitstokens.  
  
Da jedes Sicherheitstoken vom Kontopartner digital signiert ist, kann der Ressourcenpartner überprüfen Sie, dass das Token tatsächlich vom Kontopartner ausgestellt wurde und dass er nicht geändert wurde. Digitale Signaturen werden von den öffentlichen Schlüsselteil eines Partners-Tokens überprüft\-Signaturzertifikat. Nachdem die Signatur wird überprüft, der Ressourcenverbundserver eine eigene Sicherheitstoken für eine Organisation generiert aus, und sie das Sicherheitstoken mit sein eigenes Token signiert\-Signaturzertifikat.  
  
Für Umgebungen für Verbund-Partner Wenn das Token\-Signaturzertifikat von einer Zertifizierungsstelle ausgegeben wurde, stellen sicher, dass:  
  
1.  Der Zertifikatssperrlisten \(CRLs\) des Zertifikats für vertrauende Seiten und Web-Server, der den Verbundserver vertrauen zugänglich sind.  
  
2.  Zertifikat der Stammzertifizierungsstelle ist vertrauenswürdig, durch die vertrauende Seiten und Web-Server, die dem Verbundserver zu vertrauen.  
  
Der Webserver beim Ressourcenpartner verwendet den öffentlichen Schlüssel des Tokens\-Signaturzertifikat zu überprüfen, ob das Sicherheitstoken von der Ressourcenverbundserver signiert ist. Der Webserver können Sie dann den entsprechenden Zugriff auf den Client.  
  
## <a name="deployment-considerations-for-token-signing-certificates"></a>Überlegungen zur Bereitstellung für Token\-Signieren von Zertifikaten  
Wenn Sie den ersten Verbundserver in einer neuen AD FS-Installation bereitstellen, müssen Sie ein Token abrufen\-Zertifikat signieren, und installieren Sie es in den persönlichen Zertifikatspeicher lokaler Computer auf diesem Server Federation. Sie können ein Token abrufen\-Codesignaturzertifikat vom anfordernden aus einem Enterprise-Zertifizierungsstelle oder einer öffentlichen Zertifizierungsstelle oder erstellen ein selbstsigniertes\-signiertes Zertifikat.  
  
Wenn Sie eine AD FS-Farm bereitstellen, token\-Signaturzertifikate unterschiedlich, je nachdem, wie Sie die Serverfarm erstellen installiert sind.  
  
Es gibt zwei Server-Farm-Optionen, die Sie berücksichtigen können, wenn Sie Sie erhalten Zugriffstoken\-Signieren von Zertifikaten für Ihre Bereitstellung:  
  
-   Einen privaten Schlüssel von einem Token\-Signaturzertifikat alle Verbundserver in einer Farm freigegeben ist.  
  
    In einer Verbundserverfarm-Umgebung, empfiehlt es sich, dass alle Verbundserver freigeben \(oder wiederverwenden\) das gleiche Token\-Signaturzertifikat. Sie können ein einzelnes Token installieren\-Zertifikat von einer Zertifizierungsstelle auf einem Verbundserver signieren, und klicken Sie dann den privaten Schlüssel exportieren, solange das ausgestellte Zertifikat als exportierbar markiert ist.  
  
    Wie in der folgenden Abbildung wird der private Schlüssel aus einem einzelnen token dargestellt\-Signaturzertifikat für alle Verbundserver in einer Farm freigegeben werden kann. Diese Option, im Vergleich zu den folgenden "eindeutiges Token\-Signaturzertifikat" Option – Kosten reduziert, wenn Sie, zum Abrufen eines Tokens planen\-Signaturzertifikat von einer öffentlichen Zertifizierungsstelle.  
  
![Tokensignatur](media/adfs2_fedserver_certstory_3.gif)  
  
-   Es gibt ein eindeutiges Token\-Signaturzertifikat für jeden Verbundserver in einer Farm.  
  
    Bei Verwendung von mehreren signiert eindeutige Zertifikate in der Farm, jeden Server in dieser Farm Token mit seinen eigenen eindeutigen privaten Schlüssel.  
  
    Wie in der folgenden Abbildung gezeigt wird, erhalten Sie ein separates Token\-Signaturzertifikat für jedes einzelnen Verbundservers in der Farm. Diese Option ist teurer, wenn Sie planen, Ihr Token abrufen\-Signieren von Zertifikaten von einer öffentlichen Zertifizierungsstelle.  
  
![Tokensignatur](media/adfs2_fedserver_certstory_4.gif)  
  
Informationen zum Installieren eines Zertifikats aus, wenn Sie Microsoft Certificate Services als Zertifizierungsstelle Ihres Unternehmens verwenden, finden Sie unter [IIS 7.0: Erstellen Sie ein Serverzertifikat für die Domäne in IIS 7.0](https://go.microsoft.com/fwlink/?LinkId=108548).  
  
Informationen zum Installieren eines Zertifikats von einer öffentlichen Zertifizierungsstelle finden Sie unter [IIS 7.0: Anfordern eines Internetserverzertifikats (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=108549).  
  
Informationen zum Installieren eines\-signierten Zertifikat, finden Sie unter [IIS 7.0: Erstellen Sie ein selbstsigniertes\-signierte Zertifikat des Servers in IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108271).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
