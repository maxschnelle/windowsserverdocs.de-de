---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: Zertifikatanforderungen für Verbundserverproxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7fb8e71afed1c0eb6b55857835d95f2dd0ec9d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875721"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>Zertifikatanforderungen für Verbundserverproxys

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Server, die in der Verbundserverproxy-Rolle in Active Directory-Verbunddienste ausgeführt werden \(AD FS\) sind erforderlich, um Secure Sockets Layer verwenden \(SSL\) Serverauthentifizierungszertifikate. Verbundserverproxys verwenden SSL-Serverauthentifizierungszertifikate zum Schützen der Datenkommunikation von Webservern mit Webclients.  
  
Verbundserverproxys werden in der Regel die verfügbar gemacht, für Computer im Internet, die nicht in der public Key-Infrastruktur Ihres Unternehmens enthalten sind \(PKI\). Aus diesem Grund verwenden Sie ein Serverauthentifizierungszertifikat, das von einer öffentlichen ausgegeben wird \(dritte\-Partei\) Zertifizierungsstelle \(Zertifizierungsstelle\), z. B. VeriSign.  
  
Wenn Sie eine Verbundserverproxy-Farm verfügen, müssen alle Verbundserverproxy-Computer das gleiche Serverauthentifizierungszertifikat verwenden. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md).  
  
Es ist wichtig, stellen Sie sicher, dass der Antragstellername im Server-Authentifizierung Zertifikat Übereinstimmungen den Namen des Verbunddiensts Wert, der im AD FS-Verwaltungs-Snap-angegeben\-in. Öffnen Sie zum Suchen dieses Werts das Snap-in\-direkt in,\-klicken Sie auf **Service**, klicken Sie auf **Verbunddiensteigenschaften bearbeiten**, und suchen Sie dann den Wert im **Verbund Name des Diensts** Textfeld.  
  
Allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter Konfigurieren von Secure Sockets Layer in IIS 7.0 \( [http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkID\=108544](https://go.microsoft.com/fwlink/?LinkID=108544) \) und Konfigurieren von Serverzertifikaten in IIS 7.0 \( [http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkID\=108545](https://go.microsoft.com/fwlink/?LinkID=108545)\).  
  
> [!NOTE]  
> Clientauthentifizierungszertifikate sind nicht für AD FS-Verbundserverproxys erforderlich.  
  
Wenn alle, die Sie Zertifikat hat mit Zertifikatsperrlisten \(CRLs\), der Server mit dem konfigurierten Zertifikat muss in der Lage, den Server kontaktieren, die von die CRLs verteilt. Anhand des CRL-Typs wird vorgegeben, welche Ports verwendet werden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
