---
ms.assetid: 98c5ef45-2bcb-4f87-86c8-5ac6c16a6097
title: Tokensignaturzertifikate
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 24b095827ad074dbe249a9d4decd8edeecbb3603
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858783"
---
# <a name="token-signing-certificates"></a>Tokensignaturzertifikate

Verbund Server benötigen Token\-Signatur Zertifikate, um zu verhindern, dass Angreifer Sicherheits Token ändern oder fälschen, um nicht autorisierten Zugriff auf Verbund Ressourcen zu erlangen. Die private\/öffentliche Schlüssel Kopplung, die mit Token\-Signatur Zertifikaten verwendet wird, ist der wichtigste Überprüfungsmechanismus jeder Verbund Partnerschaft, da diese Schlüssel überprüfen, ob ein Sicherheits Token von einem gültigen Partner Verbund Server ausgestellt wurde und dass das Token während der Übertragung nicht geändert wurde.  
  
## <a name="token-signing-certificate-requirements"></a>Anforderungen an das Signaturzertifikat des Tokens\-  
Ein Token\-Signaturzertifikat muss die folgenden Anforderungen erfüllen, um mit AD FS arbeiten zu können:  
  
-   Damit ein Token\-Signaturzertifikat erfolgreich ein Sicherheits Token signieren kann, muss das Token\-Signaturzertifikat einen privaten Schlüssel enthalten.  
  
-   Das AD FS-Dienst Konto muss auf den privaten Schlüssel des Tokens\-Signatur Zertifikats im persönlichen Speicher des lokalen Computers zugreifen können. Dies wird vom-Setup erledigt. Sie können das\-Snap-in "AD FS-Verwaltung" auch verwenden, um diesen Zugriff zu gewährleisten, wenn Sie anschließend das Token\-Signaturzertifikat ändern.  
  
> [!NOTE]  
> Es handelt sich um eine Public Key-Infrastruktur \(PKI\) bewährte Vorgehensweise, um den privaten Schlüssel nicht für mehrere Zwecke freizugeben. Verwenden Sie daher nicht das Dienst Kommunikations Zertifikat, das Sie auf dem Verbund Server als Token\-Signaturzertifikat installiert haben.  
  
## <a name="how-token-signing-certificates-are-used-across-partners"></a>Funktionsübergreifende Verwendung von Token\--Signatur Zertifikaten  
Jedes Token\-Signaturzertifikat enthält kryptografische private Schlüssel und öffentliche Schlüssel, die verwendet werden, um \(mithilfe des privaten Schlüssels\) einem Sicherheits Token Digital zu signieren. Nachdem Sie später von einem Partner Verbund Server empfangen wurden, überprüfen diese Schlüssel die Authentizität \(mithilfe des öffentlichen Schlüssels\) des verschlüsselten Sicherheits Tokens.  
  
Da jedes Sicherheits Token vom Konto Partner digital signiert ist, kann der Ressourcen Partner überprüfen, ob das Sicherheits Token tatsächlich vom Konto Partner ausgestellt wurde und dass es nicht geändert wurde. Digitale Signaturen werden durch den Teil des öffentlichen Schlüssels des Tokens eines Partners\-Signatur Zertifikats überprüft. Nachdem die Signatur überprüft wurde, generiert der Ressourcen Verbund Server ein eigenes Sicherheits Token für seine Organisation und signiert das Sicherheits Token mit einem eigenen Token\-Signaturzertifikat.  
  
Stellen Sie für Verbund Partner Umgebungen, wenn das Token\-Signaturzertifikat von einer Zertifizierungsstelle ausgestellt wurde, Folgendes sicher:  
  
1.  Die Zertifikat Sperr Liste \(CRLs,\) des Zertifikats von den vertrauenden Seiten und Webservern, die dem Verbund Server Vertrauen, zugänglich ist.  
  
2.  Das Stamm Zertifizierungsstellen Zertifikat wird von den vertrauenden Seiten und den Webservern, die dem Verbund Server Vertrauen, als vertrauenswürdig eingestuft.  
  
Der Webserver im Ressourcen Partner verwendet den öffentlichen Schlüssel des Tokens\-Signatur Zertifikats, um zu überprüfen, ob das Sicherheits Token vom Ressourcen Verbund Server signiert wurde. Der Webserver ermöglicht dann den entsprechenden Zugriff auf den Client.  
  
## <a name="deployment-considerations-for-token-signing-certificates"></a>Überlegungen zur Bereitstellung für Token\-Signatur Zertifikate  
Wenn Sie den ersten Verbund Server in einer neuen AD FS-Installation bereitstellen, müssen Sie ein Token\-Signatur Zertifikats abrufen und im persönlichen Zertifikat Speicher des lokalen Computers auf dem Verbund Server installieren. Sie können ein Token\-Signatur Zertifikats abrufen, indem Sie eines von einer Unternehmens Zertifizierungsstelle oder einer öffentlichen Zertifizierungsstelle anfordern oder ein selbst\-signiertes Zertifikat erstellen.  
  
Beim Bereitstellen einer AD FS-Farm werden Token\-Signatur Zertifikate unterschiedlich installiert, je nachdem, wie Sie die Serverfarm erstellen.  
  
Es gibt zwei Serverfarm Optionen, die Sie beim Abrufen von Token\-Signatur Zertifikaten für die Bereitstellung in Erwägung ziehen können:  
  
-   Ein privater Schlüssel aus einem Token,\-Signaturzertifikat von allen Verbund Servern in einer Farm gemeinsam genutzt wird.  
  
    In einer Verbund Serverfarm-Umgebung wird empfohlen, dass alle Verbund Server \(oder\) demselben Token\-Signaturzertifikat verwenden. Sie können ein einzelnes Token\-Signaturzertifikat von einer Zertifizierungsstelle auf einem Verbund Server installieren und dann den privaten Schlüssel exportieren, sofern das ausgestellte Zertifikat als exportierbar markiert ist.  
  
    Wie in der folgenden Abbildung dargestellt, kann der private Schlüssel aus einem einzelnen Token\-Signaturzertifikat für alle Verbund Server in einer Farm freigegeben werden. Diese Option – im Vergleich zur folgenden "Unique Token\-Signing Certificate"-Option – reduziert die Kosten, wenn Sie planen, ein Token\-Signaturzertifikat von einer öffentlichen Zertifizierungsstelle zu erhalten.  
  
![Tokensignierung](media/adfs2_fedserver_certstory_3.gif)  
  
-   Es gibt ein eindeutiges Token\-Signaturzertifikat für jeden Verbund Server in einer Farm.  
  
    Wenn Sie mehrere eindeutige Zertifikate in der Farm verwenden, signiert jeder Server in dieser Farm Token mit einem eigenen eindeutigen privaten Schlüssel.  
  
    Wie in der folgenden Abbildung gezeigt, können Sie für jeden einzelnen Verbund Server in der Farm ein separates Token\-Signatur Zertifikats abrufen. Diese Option ist kostengünstiger, wenn Sie beabsichtigen, Ihr Token\-Signatur Zertifikate von einer öffentlichen Zertifizierungsstelle zu erhalten.  
  
![Tokensignierung](media/adfs2_fedserver_certstory_4.gif)  
  
Informationen zum Installieren eines Zertifikats bei Verwendung von Microsoft-Zertifikat Diensten als Unternehmens Zertifizierungsstelle finden Sie unter [IIS 7,0: Erstellen eines Domänen Server Zertifikats in IIS 7,0](https://go.microsoft.com/fwlink/?LinkId=108548).  
  
Informationen zum Installieren eines Zertifikats von einer öffentlichen Zertifizierungsstelle finden Sie unter [IIS 7,0: Anfordern eines Internet Server Zertifikats](https://go.microsoft.com/fwlink/?LinkId=108549).  
  
Weitere Informationen zum Installieren eines selbst\-signierten Zertifikats finden Sie unter [IIS 7,0: Erstellen eines selbst\-signierten Server Zertifikats in IIS 7,0](https://go.microsoft.com/fwlink/?LinkID=108271).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
