---
ms.assetid: 98c5ef45-2bcb-4f87-86c8-5ac6c16a6097
title: Token-Signing Certificates
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 84e106ec87861960d7de651b4aaa0e88c952aa79
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="token-signing-certificates"></a>Token-Signing Certificates

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Verbundserver müssen Token\-Signierung Zertifikate hindert Angreifer daran ändern oder zu fälschen Sicherheitstoken versuchen, nicht autorisierten Zugriff auf verbundene Ressourcen. Die Kopplung, d.h. Private\ und öffentlichem Schlüssel ist mit Token\ Signieren von Zertifikaten verwendet der wichtigsten Überprüfung Mechanismus über alle federated Partnerschaften, da diese Schlüssel stellen Sie sicher, dass ein Sicherheitstoken von einem gültigen Partner-Verbundserver ausgestellt wurde und das Token nicht während der Übertragung geändert wurde.  
  
## <a name="token-signing-certificate-requirements"></a>Signieren von Token\ Zertifikatanforderungen  
Token\-Signaturzertifikat muss mit AD FS funktioniert die folgenden Anforderungen erfüllen:  
  
-   Für eine Token\-Signaturzertifikat erfolgreich ein Sicherheitstoken anmelden muss das Token\-Signaturzertifikat einen privaten Schlüssel enthalten.  
  
-   Der AD FS-Dienstkonto benötigen Zugriff auf das Token\-Signaturzertifikat den privaten Schlüssel im persönlichen Speicher des lokalen Computers. Dies wird von Setup durchgeführt. Sie können auch AD FS-Verwaltungs-Snap-in verwenden, um diesen Zugriff sicherzustellen, dass wenn Sie das Signaturzertifikat Token\ später ändern.  
  
> [!NOTE]  
> Es ist eine public Key-Infrastruktur \(PKI\) bewährte Methode nicht den privaten Schlüssel für mehrere Zwecke gemeinsam nutzen. Verwenden Sie daher nicht das dienstkommunikationszertifikat, das Sie auf dem Verbundserver als das Token\-Signaturzertifikat installiert.  
  
## <a name="how-token-signing-certificates-are-used-across-partners"></a>Verwendung Token\-Signaturzertifikaten für Partner  
Alle Token\-Signaturzertifikat enthält kryptografische private und öffentliche Schlüssel, die verwendet werden, zum digitalen Signieren \ (über die private für schlüssel\) ein Sicherheitstoken. Nachdem sie von einem Partnerverbundserver empfangen werden, überprüfen diese Schlüssel später die Echtheit \ (über den öffentlichen für schlüssel\) des verschlüsselten Sicherheitstokens.  
  
Da jedes Sicherheitstoken vom Kontopartner digital signiert ist, kann der Ressourcenpartner überprüfen Sie, dass das Sicherheitstoken tatsächlich vom Kontopartner ausgestellt wurde und nicht geändert wurde. Digitale Signaturen werden durch den öffentlichen Schlüssel Teil eines Partners Token\ singen Zertifikat überprüft. Nachdem die Signatur überprüft wird, der Ressourcenverbundserver generiert eine eigene Sicherheitstoken für die Organisation, und das Sicherheitstoken mit eigenen Token\-Signaturzertifikat signiert.  
  
Verbund-Partner-Umgebungen Wenn das Token\-Signaturzertifikat von einer Zertifizierungsstelle ausgestellt wurde, sicher, dass:  
  
1.  Das Zertifikat Revocation Lists \(CRLs\) des Zertifikats vertrauende Seiten und Webserver, die den Verbundserver vertrauen zugegriffen werden.  
  
2.  Die Stamm-CA-Zertifikat wird durch die vertrauende Seiten und Webserver, die den Verbundserver vertrauen vertraut.  
  
Der Webserver beim Ressourcenpartner verwendet den öffentlichen Schlüssel des Token\-Signaturzertifikat um zu überprüfen, ob das Token vom Ressourcenverbundserver angemeldet ist. Der Webserver kann dann den entsprechenden Zugriff auf dem Client.  
  
## <a name="deployment-considerations-for-token-signing-certificates"></a>Bereitstellungsüberlegungen für Token\-Signaturzertifikaten  
Bei der Bereitstellung des ersten Verbundservers in einer neuen AD FS-Installation müssen Sie Token\-Signaturzertifikat abrufen und installieren Sie es in den persönlichen Zertifikatspeicher lokalen Computers auf diesem Verbundserver. Erhalten Sie eine Token\-signing certificate durch Anfordern einer von einem Unternehmen oder einer öffentlichen Zertifizierungsstelle oder durch Erstellen eines Zertifikats mit deren Hilfe signiert.  
  
Wenn Sie eine AD FS-Farm bereitstellen, werden Token\-Signaturzertifikaten unterschiedlich, je nachdem, wie Sie die Serverfarm erstellen installiert.  
  
Es gibt zwei Server-Farm-Optionen, die Sie berücksichtigen können, wenn Sie Token\-Signaturzertifikaten für Ihre Bereitstellung erhalten:  
  
-   Ein privater Schlüssel von einem Token\-Signaturzertifikat wird von allen Verbundservern in einer Farm gemeinsam verwendet.  
  
    In einer Verbundserverfarm-Umgebung empfehlen wir, dass alle Verbundserver \(or reuse\) das gleiche Token\-Signaturzertifikat freigeben. Können Sie eine einzelne Token\-Signaturzertifikat von einer Zertifizierungsstelle auf einem Verbundserver installieren und dann den privaten Schlüssel exportieren, solange das ausgestellte Zertifikat als exportierbar markiert ist.  
  
    Wie in der folgenden Abbildunggezeigt wird, kann der private Schlüssel von einem einzelnen Token\-Signaturzertifikat auf allen Verbundservern in einer Farm freigegeben werden. Diese Option – im Vergleich zu den folgenden "eindeutige Token\-Signaturzertifikat" Option-Kosten reduziert, wenn Sie vorhaben, ein Token\-Signaturzertifikat von einer öffentlichen Zertifizierungsstelle erhalten.  
  
![Signieren von Token](media/adfs2_fedserver_certstory_3.gif)  
  
-   Es gibt eine eindeutige Token\-Signaturzertifikat für jeden Verbundserver in einer Farm.  
  
    Wenn Sie mehrere verwenden, signiert eindeutige Zertifikate in der Farm, jeden Server in dieser Farm Token mit seinen eigenen eindeutigen privaten Schlüssel.  
  
    Wie in der folgenden Abbildunggezeigt, können Sie eine separate Token\-Signaturzertifikat für jeden einzelnen Verbundserver in der Farm abrufen. Diese Option ist mehr Aufwand bedeuten, wenn Sie Ihre Token\-Signierung Zertifikate von einer öffentlichen Zertifizierungsstelle erhalten möchten.  
  
![Signieren von Token](media/adfs2_fedserver_certstory_4.gif)  
  
Informationen zum Installieren eines Zertifikats, wenn Sie Microsoft Zertifikatdienste als Ihre Unternehmenszertifizierungsstelle verwenden, finden Sie unter [IIS 7.0: Erstellen Sie ein Serverzertifikat für die Domäne in IIS 7.0](https://go.microsoft.com/fwlink/?LinkId=108548).  
  
Informationen zum Installieren eines Zertifikats von einer öffentlichen Zertifizierungsstelle finden Sie unter [IIS 7.0: Anfordern eines Serverzertifikats Internet](https://go.microsoft.com/fwlink/?LinkId=108549).  
  
Informationen zum Installieren eines Zertifikats mit deren Hilfe-Signatur finden Sie unter [IIS 7.0: Erstellen Sie ein Serverzertifikat Self\-Signed in IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108271).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
