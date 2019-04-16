---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: Certificate Requirements for Federation Servers
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 369c0e9e7ab1ef25baee1c35379cc66b886f20d8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="certificate-requirements-for-federation-servers"></a>Certificate Requirements for Federation Servers

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In jedem Entwurf \(AD FS\) Active Directory Federation Services müssen verschiedene Zertifikate auf sichere Kommunikation und die Benutzerauthentifizierungen zwischen Internetclients und Verbundserver verwendet werden. Jeder Verbundserver muss über ein dienstkommunikationszertifikat und Token\-Signaturzertifikat verfügen, bevor es in AD FS-Kommunikation teilnehmen kann. Die folgende Tabelle beschreibt die Zertifikatstypen, die Verbundserver zugeordnet sind.  
  
|Zertifikattyp|Beschreibung|  
|--------------------|---------------|  
|Token\-Signaturzertifikat|Token\-Signaturzertifikat ist ein X509 Zertifikat. Verbundserver verwenden zugeordnete Public\/Private Schlüsselpaare, um alle Sicherheitstoken digital zu signieren, die sie erstellen. Dazu gehört das Signieren von veröffentlichten Verbundmetadaten und artefaktauflösungsanforderungen Auflösung Anforderungen.<br /><br />Sie können mehrere Token\-Signaturzertifikaten in AD FS-Verwaltungs-Snap-in zum zertifikatrollover zuzulassen, wenn ein Zertifikat nahezu abgelaufen ist konfiguriert haben. Standardmäßig werden alle Zertifikate in der Liste veröffentlicht, aber nur das primäre Token\-Signaturzertifikat wird von AD FS für das tatsächliche Signieren von Token verwendet. Alle, die von Ihnen ausgewählten Zertifikate müssen einen entsprechenden privaten Schlüssel verfügen.<br /><br />Weitere Informationen finden Sie unter [Tokensignaturzertifikate](Token-Signing-Certificates.md) und [hinzufügen ein Tokensignaturzertifikat](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md).|  
|Dienstkommunikationszertifikat|Verbundserver verwenden ein Serverauthentifizierungszertifikat, auch bekannt als eine Kommunikation zwischen für Windows Communication Foundation \(WCF\) Message Security. Standardmäßig ist dies dasselbe Zertifikat, das ein Verbundserver als \(SSL\) Secure Sockets Layer-Zertifikat in Internetinformationsdienste \(IIS\) verwendet. **Hinweis:** AD FS-Verwaltungs-Snap-In bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.<br /><br />Weitere Informationen finden Sie unter [Dienstkommunikationszertifikate](Service-Communications-Certificates.md) und [Festlegen eines Dienstkommunikationszertifikats](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md).<br /><br />Da das dienstkommunikationszertifikat Clientcomputer vertrauenswürdig sein muss, empfiehlt es sich, dass Sie ein Zertifikat verwenden, die von einer vertrauenswürdigen Zertifizierungsstelle signiert ist \(CA\). Alle, die von Ihnen ausgewählten Zertifikate müssen einen entsprechenden privaten Schlüssel verfügen.|  
|Secure Sockets Layer \(SSL\) Zertifikat|Verbundserver verwenden ein SSL-Zertifikat Webdienstdatenverkehr für die SSL-Kommunikation mit Webclients und verbundserverproxies zu sichern.<br /><br />Da das SSL-Zertifikat Clientcomputer vertrauenswürdig sein muss, wird empfohlen, dass Sie ein Zertifikat verwenden, die von einer vertrauenswürdigen Zertifizierungsstelle signiert wurde. Alle, die von Ihnen ausgewählten Zertifikate müssen einen entsprechenden privaten Schlüssel verfügen.|  
|Token\-Entschlüsselungszertifikat|Dieses Zertifikat wird verwendet, um Token entschlüsseln, die von diesem Verbundserver empfangen werden.<br /><br />Sie können mehrere entschlüsselungszertifikate haben. Dadurch können für einen Ressourcenverbundserver zu Token entschlüsseln, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungszertifikat festgelegt ist. Alle Zertifikate können für die Entschlüsselung verwendet werden, aber nur das primäre Token\ entschlüsseln Zertifikat ist tatsächlich in den Verbundmetadaten veröffentlicht. Alle, die von Ihnen ausgewählten Zertifikate müssen einen entsprechenden privaten Schlüssel verfügen.<br /><br />Weitere Informationen finden Sie unter [Hinzufügen einer Tokenverschlüsselungszertifikats](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md).|  
  
Sie können anfordern und installieren Sie ein SSL- oder dienstkommunikationszertifikat durch die Anforderung ein dienstkommunikationszertifikat über die Microsoft Management Console \(MMC\) snap\-in für IIS. Weitere allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter [IIS 7.0: Konfigurieren von Secure Sockets Layer in IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108544) und [IIS 7.0: Konfigurieren von Serverzertifikaten in IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108545) .  
  
> [!NOTE]  
> In AD FS können Sie die Secure Hash Algorithm \(SHA\) Ebene ändern, die für digitale Signaturen SHA\-1 oder SHA\-256 \(more secure\) verwendet wird. AD FSdoes keine Unterstützung für die Verwendung von Zertifikaten mit anderen Hashmethoden wie MD5 \ (der Standardhashalgorithmus, der mit dem Makecert.exe Befehlszeilenoption Tool\ verwendet wird). Als bewährte Sicherheitsmethode wir empfehlen die Verwendung von SHA\-256 \ (durch Default\ festgelegt) für alle Signaturen. SHA\-1 wird nur in Szenarien empfohlen, in dem Sie mit einem Produkt interoperieren müssen, das keine Kommunikation über SHA\-256 unterstützt, z. B. ein-Microsoft-Produkt oder AD FS 1. *x*.  
  
## <a name="determining-your-ca-strategy"></a>Ermitteln Ihrer CA-Strategie  
AD FS erfordert keine Zertifikate von einer Zertifizierungsstelle ausgestellt werden. Allerdings das SSL-Zertifikat \ (das Zertifikat, das auch als der Dienst Communications Certificate\ standardmäßig verwendet wird) muss die AD FS-Clients vertrauenswürdig sein. Es wird empfohlen, dass Sie deren Hilfe-signierte Zertifikate nicht für diese Zertifikattypen verwenden.  
  
> [!IMPORTANT]  
> Mit deren Hilfe signiert, SSL-Zertifikaten in einer produktionsumgebung einen böswilligen Benutzer in einer Kontopartnerorganisation möglicherweise die Kontrolle der Verbundserver in einer Ressourcenpartnerorganisation übernehmen können. Dieses Sicherheitsrisiko besteht, da deren Hilfe signierte Zertifikate Stammzertifikate sind. Sie müssen dem vertrauenswürdigen Stammspeicher eines anderen Federation Servers hinzugefügt werden \ (z. B. die Ressource Federation Server\), die können diesen Server anfällig für Angriffe.  
  
Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher des lokalen Computers importiert werden. Sie können Zertifikate in den persönlichen Speicher mit dem Zertifikate-MMC-Snap-in importieren.  
  
Als Alternative zur Verwendung der Zertifikate-Snap-in können Sie das SSL-Zertifikat mit dem IIS-Manager-Snap-in zum Zeitpunkt importieren, die Sie das SSL-Zertifikat der Standardwebsite zuweisen. Weitere Informationen finden Sie unter [importieren Sie ein Serverauthentifizierungszertifikat auf der Standardwebsite](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
> [!NOTE]  
> Bevor Sie die AD FS-Software auf dem Computer, die der Verbundserver verwendet werden sollen installieren, stellen Sie sicher, dass beide Zertifikate in den persönlichen Zertifikatspeicher des lokalen Computers befinden und das SSL-Zertifikat auf der Standardwebsite zugewiesen ist. Weitere Informationen zur Reihenfolge der Aufgaben, die erforderlich sind, zum Einrichten eines Verbundservers finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
Abhängig von Ihren Sicherheits- und budgetanforderungen berücksichtigen Sie welche Ihrer Zertifikate von einer öffentlichen Zertifizierungsstelle oder einer Unternehmenszertifizierungsstelle abgerufen werden. Die folgende Abbildung zeigt die empfohlenen zertifizierungsstellenaussteller für einen bestimmten Zertifikattyp. Diese Empfehlung stellt einen Ansatz Best\ Methoden in Bezug auf Sicherheit und Kosten.  
  
![CERT-Anforderungen](media/adfs2_fedserver_certstory_1.png)  
  
## <a name="certificate-revocation-lists"></a>Zertifikatsperrlisten  
Wenn jedes Zertifikat, das Sie verwenden, um Zertifikatsperrlisten verfügt, muss der Server mit dem konfigurierten Zertifikat eine Verbindung mit den Server herstellen, mit dem die CRLs verteilt.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
