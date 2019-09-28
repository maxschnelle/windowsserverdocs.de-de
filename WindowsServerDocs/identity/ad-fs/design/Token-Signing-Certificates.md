---
ms.assetid: 98c5ef45-2bcb-4f87-86c8-5ac6c16a6097
title: Tokensignaturzertifikate
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 02c126fe0792872298a5512abf850af41e1db826
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407910"
---
# <a name="token-signing-certificates"></a>Tokensignaturzertifikate

Verbund Server benötigen Tokensignaturzertifikate\-, um zu verhindern, dass Angreifer Sicherheits Token ändern oder fälschen, um nicht autorisierten Zugriff auf Verbund Ressourcen zu erlangen. Die private\/öffentliche Schlüssel Kopplung, die mit Tokensignaturzertifikaten\-verwendet wird, ist der wichtigste Überprüfungsmechanismus jeder Verbund Partnerschaft, da diese Schlüssel überprüfen, ob ein Sicherheits Token von einem gültigen Partner ausgestellt wurde. der Verbund Server und das Token wurden während der Übertragung nicht geändert.  
  
## <a name="token-signing-certificate-requirements"></a>Anforderungen\-für Tokensignaturzertifikate  
Ein Tokensignaturzertifikat\-muss die folgenden Anforderungen erfüllen, um mit AD FS arbeiten zu können:  
  
-   Damit ein Tokensignaturzertifikat\-erfolgreich ein Sicherheits Token signieren kann\-, muss das Tokensignaturzertifikat einen privaten Schlüssel enthalten.  
  
-   Das AD FS-Dienst Konto muss auf den privaten Schlüssel\-des Tokensignaturzertifikats im persönlichen Speicher des lokalen Computers zugreifen können. Dies wird vom-Setup erledigt. Sie können das Snap\--in AD FS Verwaltung auch verwenden, um diesen Zugriff zu gewährleisten, wenn Sie anschließend das Tokensignaturzertifikat\-ändern.  
  
> [!NOTE]  
> Es handelt sich um eine Public \(Key-\) Infrastruktur-PKI-bewährte Vorgehensweise, um den privaten Schlüssel nicht für mehrere Zwecke freizugeben. Verwenden Sie daher nicht das Dienst Kommunikations Zertifikat, das Sie auf dem Verbund Server als Tokensignaturzertifikat\-installiert haben.  
  
## <a name="how-token-signing-certificates-are-used-across-partners"></a>Funktionsübergreifende\-Verwendung von Tokensignaturzertifikaten  
Jedes Tokensignaturzertifikat\-enthält kryptografische private Schlüssel und öffentliche Schlüssel, die verwendet werden \(, um mithilfe des privaten Schlüssels\) ein Sicherheits Token Digital zu signieren. Nachdem Sie später von einem Partner Verbund Server empfangen wurden, überprüfen diese Schlüssel die Authentizität \(mithilfe des öffentlichen Schlüssels\) des verschlüsselten Sicherheits Tokens.  
  
Da jedes Sicherheits Token vom Konto Partner digital signiert ist, kann der Ressourcen Partner überprüfen, ob das Sicherheits Token tatsächlich vom Konto Partner ausgestellt wurde und dass es nicht geändert wurde. Digitale Signaturen werden durch den Teil des öffentlichen Schlüssels des Tokensignaturzertifikats\-eines Partners überprüft. Nachdem die Signatur überprüft wurde, generiert der Ressourcen Verbund Server ein eigenes Sicherheits Token für seine Organisation und signiert das Sicherheits Token mit einem eigenen Tokensignaturzertifikat\-.  
  
Für Verbund Partner Umgebungen: Wenn das Tokensignaturzertifikat\-von einer Zertifizierungsstelle ausgestellt wurde, stellen Sie Folgendes sicher:  
  
1.  Der Zertifikat Sperr Listen \(\) des Zertifikats ist für vertrauende Seiten und Webserver verfügbar, die dem Verbund Server Vertrauen.  
  
2.  Das Stamm Zertifizierungsstellen Zertifikat wird von den vertrauenden Seiten und den Webservern, die dem Verbund Server Vertrauen, als vertrauenswürdig eingestuft.  
  
Der Webserver im Ressourcen Partner verwendet den öffentlichen Schlüssel des Tokensignaturzertifikats\-, um zu überprüfen, ob das Sicherheits Token vom Ressourcen Verbund Server signiert wurde. Der Webserver ermöglicht dann den entsprechenden Zugriff auf den Client.  
  
## <a name="deployment-considerations-for-token-signing-certificates"></a>Bereitstellungs Überlegungen\-für Tokensignaturzertifikate  
Wenn Sie den ersten Verbund Server in einer neuen AD FS-Installation bereitstellen, müssen Sie ein\-Tokensignaturzertifikat abrufen und im persönlichen Zertifikat Speicher des lokalen Computers auf dem Verbund Server installieren. Sie können ein Tokensignaturzertifikat\-abrufen, indem Sie eines von einer Unternehmens Zertifizierungsstelle oder einer öffentlichen Zertifizierungsstelle anfordern oder ein selbst\-signiertes Zertifikat erstellen.  
  
Beim Bereitstellen einer AD FS-Farm werden\-Tokensignaturzertifikate unterschiedlich installiert, je nachdem, wie Sie die Serverfarm erstellen.  
  
Es gibt zwei Serverfarm Optionen, die Sie beim Abrufen von Tokensignaturzertifikaten\-für die Bereitstellung in Erwägung ziehen können:  
  
-   Ein privater Schlüssel von einem Tokensignaturzertifikat\-wird von allen Verbund Servern in einer Farm gemeinsam genutzt.  
  
    In einer Verbund Serverfarm-Umgebung wird empfohlen, dass alle Verbund Server \(dasselbe Tokensignaturzertifikat\-gemeinsam verwenden oder wieder verwenden\) . Sie können ein einzelnes Tokensignaturzertifikat\-von einer Zertifizierungsstelle auf einem Verbund Server installieren und dann den privaten Schlüssel exportieren, sofern das ausgestellte Zertifikat als exportierbar markiert ist.  
  
    Wie in der folgenden Abbildung dargestellt, kann der private Schlüssel aus einem einzelnen\-Tokensignaturzertifikat für alle Verbund Server in einer Farm freigegeben werden. Diese Option – im Vergleich zur folgenden "eindeutigen Tokensignaturzertifikat\-" – reduziert die Kosten, wenn Sie planen, ein Tokensignaturzertifikat\-von einer öffentlichen Zertifizierungsstelle zu erhalten.  
  
![Tokensignierung](media/adfs2_fedserver_certstory_3.gif)  
  
-   Es gibt ein eindeutiges\-Tokensignaturzertifikat für jeden Verbund Server in einer Farm.  
  
    Wenn Sie mehrere eindeutige Zertifikate in der Farm verwenden, signiert jeder Server in dieser Farm Token mit einem eigenen eindeutigen privaten Schlüssel.  
  
    Wie in der folgenden Abbildung gezeigt, können Sie für jeden einzelnen Verbund\-Server in der Farm ein separates Tokensignaturzertifikat abrufen. Diese Option ist kostengünstiger, wenn Sie beabsichtigen, ihre Tokensignaturzertifikate\-von einer öffentlichen Zertifizierungsstelle zu erhalten.  
  
![Tokensignierung](media/adfs2_fedserver_certstory_4.gif)  
  
Informationen zum Installieren eines Zertifikats bei Verwendung von Microsoft-Zertifikat Diensten als Unternehmens Zertifizierungsstelle finden [Sie unter IIS 7,0: Erstellen Sie ein Domänen Server Zertifikat in](https://go.microsoft.com/fwlink/?LinkId=108548)IIS 7,0.  
  
Informationen zum Installieren eines Zertifikats von einer öffentlichen Zertifizierungsstelle finden [Sie unter IIS 7,0: Anfordern eines Internetserverzertifikats (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=108549).  
  
Informationen zum Installieren eines selbst\-signierten Zertifikats finden [Sie unter IIS 7,0: Erstellen Sie ein\-selbst signiertes Server Zertifikat in](https://go.microsoft.com/fwlink/?LinkID=108271)IIS 7,0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
