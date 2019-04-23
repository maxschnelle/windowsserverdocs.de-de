---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: Zertifikatanforderungen für Verbundserver
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 369c0e9e7ab1ef25baee1c35379cc66b886f20d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827101"
---
# <a name="certificate-requirements-for-federation-servers"></a>Zertifikatanforderungen für Verbundserver

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In jeder Active Directory Federation Services \(AD FS\) Design, verschiedene Zertifikate müssen zum Sichern der Kommunikation und erleichtern die Benutzerauthentifizierungen zwischen Internetclients und Verbundserver verwendet werden. Jeder Verbundserver benötigen ein dienstkommunikationszertifikat und ein Token\-Codesignaturzertifikat ein, bevor sie in AD FS-Kommunikation teilnehmen kann. Die folgende Tabelle beschreibt die Zertifikatstypen, die Verbundserver zugeordnet sind.  
  
|Zertifikattyp|Beschreibung|  
|--------------------|---------------|  
|Token\-Signaturzertifikat|Ein Token\-Signaturzertifikat ist ein X509 Zertifikat. Verbundserver verwenden zugeordnete öffentliche\/private Schlüsselpaare, um alle Sicherheitstoken digital zu signieren, die sie erstellen. Dazu gehört das Signieren von veröffentlichten Verbundmetadaten und Artefaktauflösungsanforderungen.<br /><br />Sie haben mehrere Token\-Signieren von Zertifikaten, die in der AD FS-Verwaltungs-Snap konfiguriert\-um zertifikatrollover zuzulassen, wenn ein Zertifikat nahezu abgelaufen ist. In der Standardeinstellung alle Zertifikate in der Liste veröffentlicht werden, aber nur das primäre Token\-Signaturzertifikat zum Signieren von Token tatsächlich von AD FS verwendet wird. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.<br /><br />Weitere Informationen finden Sie unter [Token-Signing Certificates](Token-Signing-Certificates.md) und [Add a Token-Signing Certificate](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md).|  
|Dienstkommunikationszertifikat|Verbundserver verwenden ein Serverauthentifizierungszertifikat, auch bekannt als eine Dienstkommunikation für Windows Communication Foundation \(WCF\) Nachrichtensicherheit. Standardmäßig ist dies dasselbe Zertifikat, das ein Verbundserver als Secure Sockets Layer verwendet \(SSL\) Zertifikats in Internet Information Services \(IIS\). **Hinweis**: Die AD FS-Verwaltungs-Snap\-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.<br /><br />Weitere Informationen finden Sie unter [Dienstkommunikationszertifikate](Service-Communications-Certificates.md) und [Festlegen eines Dienstkommunikationszertifikats](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md).<br /><br />Da das dienstkommunikationszertifikat Clientcomputer vertrauenswürdig sein muss, es wird empfohlen, dass Sie ein Zertifikat verwenden, die von einer vertrauenswürdigen Zertifizierungsstelle signiert ist \(Zertifizierungsstelle\). Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.|  
|Secure Sockets Layer \(SSL\) Zertifikat|Verbundserver verwenden ein SSL-Zertifikat, um den Webdienstdatenverkehr für die SSL-Kommunikation mit Webclients und Verbundserverproxies zu sichern.<br /><br />Da das SSL-Zertifikat für Clientcomputer vertrauenswürdig sein muss, wird empfohlen, ein Zertifikat zu verwenden, das von einer vertrauenswürdigen Zertifizierungsstelle signiert ist. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.|  
|Token\-Entschlüsselungszertifikat|Dieses Zertifikat wird zum Entschlüsseln von Token, die von dieser Verbundserver empfangen werden.<br /><br />Sie können mehrere Entschlüsselungszertifikate haben. Dadurch kann für einen Ressourcenverbundserver können Token entschlüsseln, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungszertifikat festgelegt wurde. Alle Zertifikate können verwendet werden, für die Entschlüsselung, aber nur das primäre Token\-Zertifikat entschlüsselt wird tatsächlich in den Verbundmetadaten veröffentlicht. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.<br /><br />Weitere Informationen finden Sie unter [ein Tokenentschlüsselungszertifikat hinzufügen](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md).|  
  
Sie können anfordern und installieren Sie ein SSL- oder dienstkommunikationszertifikat anfordern ein dienstkommunikationszertifikat über die Microsoft Management Console \(MMC\) ausrichten\-in für IIS. Weitere allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter [IIS 7.0: Konfigurieren von Secure Sockets Layer in IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108544) und [IIS 7.0: Konfigurieren von Serverzertifikaten in IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108545) .  
  
> [!NOTE]  
> In AD FS können Sie den sicheren Hashalgorithmus ändern \(SHA\) Ebene, die verwendet wird, für digitale Signaturen entweder SHA\-1 oder SHA\-256 \(sicherer\). AD FSdoes keine Unterstützung für die Verwendung von Zertifikaten mit anderen Hashmethoden als MD5 \(der Standardhashalgorithmus, der verwendet wird, mit dem Befehl Makecert.exe\-Tools "Linie"\). Als bewährte Sicherheitsmethode es wird empfohlen, die Verwendung von SHA\-256 \(der wird standardmäßig festgelegt\) für alle Signaturen. SHA\-1 wird empfohlen, nur in Szenarien, in denen Sie interoperieren müssen mit einem Produkt, das keine Kommunikation über SHA unterstützt\-256, z. B. ein nicht\-Microsoft-Produkt oder AD FS 1. *x*.  
  
## <a name="determining-your-ca-strategy"></a>Festlegen Ihrer CA-Strategie  
AD FS erfordert keine Zertifikate von einer Zertifizierungsstelle ausgestellt werden. Allerdings das SSL-Zertifikat \(das Zertifikat, das standardmäßig auch als dienstkommunikationszertifikat verwendet wird\) muss die AD FS-Clients vertrauenswürdig sein. Es wird empfohlen, dass Sie nicht selbst verwenden\-selbstsignierten Zertifikaten, für diese Typen Zertifikatspeicher.  
  
> [!IMPORTANT]  
> Verwenden des Self-Service\-angemeldet, SSL-Zertifikaten in einer produktionsumgebung können einen böswilligen Benutzer in einer Kontopartnerorganisation möglicherweise die Kontrolle der Verbundserver in einer Ressourcenpartnerorganisation übernehmen. Dieses Sicherheitsrisiko besteht, da selbst\-selbstsignierte Zertifikate sind Zertifikate der Stammzertifizierungsstelle. Sie müssen dem vertrauenswürdigen Stammspeicher eines anderen Federation Servers hinzugefügt werden \(z. B. der Ressourcenverbundserver\), dem können diesen Server anfällig für Angriffe.  
  
Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher auf dem lokalen Computer importiert werden. Sie können Zertifikate importieren, in den persönlichen Speicher mit dem Zertifikate-MMC-Snap\-in.  
  
Als Alternative zur Verwendung der Zertifikate ausrichten\-, können Sie auch das SSL-Zertifikat mit der IIS-Manager-Snap importieren\-im an die Zeit, die Sie, die SSL zuweisen-Zertifikats an die Standardwebsite. Weitere Informationen finden Sie unter [Importieren eines Serverauthentifizierungszertifikats auf die Standardwebsite](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
> [!NOTE]  
> Vor der Installation von AD FS-Software auf dem Computer, die der Verbundserver werden soll, stellen Sie sicher, dass beide Zertifikate in den persönlichen Zertifikatspeicher des lokalen Computers befinden und das SSL-Zertifikat auf der Standardwebsite zugewiesen ist. Weitere Informationen über die Reihenfolge der Aufgaben, die erforderlich sind, zum Einrichten eines Verbundservers finden Sie unter [Prüfliste: Das Einrichten eines Verbundservers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
Je nach Sicherheits- und Budgetanforderungen sollten Sie sorgfältig in Betracht ziehen, welche Ihrer Zertifikate von einer öffentlichen oder einer Unternehmenszertifizierungsstelle abgerufen werden. In der folgenden Abbildung sind die empfohlenen Zertifizierungsstellenaussteller für einen bestimmten Zertifikattyp dargestellt. Diese Empfehlung stellt empfohlene\-Ansatz in Bezug auf Sicherheit und Kosten zu üben.  
  
![CERT-Anforderungen](media/adfs2_fedserver_certstory_1.png)  
  
## <a name="certificate-revocation-lists"></a>Zertifikatsperrliste  
Falls ein von Ihnen verwendetes Zertifikat über Zertifikatsperrlisten (Certificate Revocation Lists, CRLs) verfügt, muss der Server mit dem konfigurierten Zertifikat den Server kontaktieren können, von dem die CRLs verteilt werden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
