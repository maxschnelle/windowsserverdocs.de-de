---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: Zertifikatanforderungen für Verbundserver
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7eeff82ef3311f18c8252c44c96310fcf3c18217
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359181"
---
# <a name="certificate-requirements-for-federation-servers"></a>Zertifikatanforderungen für Verbundserver

In allen Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Entwurf müssen verschiedene Zertifikate verwendet werden, um die Kommunikation zu sichern und Benutzer Authentifizierungen zwischen Internet Clients und Verbund Servern zu vereinfachen. Jeder Verbund Server muss über ein Dienst Kommunikations Zertifikat und ein Token @ no__t-0signaturzertifikat verfügen, bevor es an AD FS-Kommunikation teilnehmen kann. In der folgenden Tabelle werden die Zertifikat Typen beschrieben, die dem Verbund Server zugeordnet sind.  
  
|Zertifikattyp|Beschreibung|  
|--------------------|---------------|  
|Token @ no__t-0signaturzertifikat|Ein Token @ no__t-0signaturzertifikat ist ein X509-Zertifikat. Verbund Server verwenden zugeordnete öffentliche @ no__t-0private-Schlüsselpaare, um alle von Ihnen erzeugten Sicherheits Token Digital zu signieren. Dazu gehört das Signieren von veröffentlichten Verbundmetadaten und Artefaktauflösungsanforderungen.<br /><br />Sie können mehrere Token @ no__t-0signing-Zertifikate konfigurieren, die im AD FS Verwaltungs-Snap @ no__t-1In konfiguriert sind, um ein zertifikatrol Lover zuzulassen, wenn ein Zertifikat fast abläuft. Standardmäßig werden alle Zertifikate in der Liste veröffentlicht, aber nur das primäre Token @ no__t-0signing Certificate wird von AD FS verwendet, um Token tatsächlich zu signieren. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.<br /><br />Weitere Informationen finden Sie unter [Token-Signing Certificates](Token-Signing-Certificates.md) und [Add a Token-Signing Certificate](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md).|  
|Dienstkommunikationszertifikat|Verbund Server verwenden ein Server Authentifizierungszertifikat, das auch als Dienst Kommunikation für Windows Communication Foundation \(wcf @ no__t-1-Nachrichten Sicherheit bezeichnet wird. Standardmäßig handelt es sich hierbei um dasselbe Zertifikat, das ein Verbund Server in Internetinformationsdienste \(iis @ no__t-3 als Secure Sockets Layer \(ssl @ no__t-1-Zertifikat verwendet. **Hinweis**: Das AD FS-Verwaltungs-Snap @ no__t-0in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.<br /><br />Weitere Informationen finden Sie unter [Dienst Kommunikations Zertifikate](Service-Communications-Certificates.md) und [Festlegen eines Dienst Kommunikations Zertifikats](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md).<br /><br />Da das Dienst Kommunikations Zertifikat für Client Computer vertrauenswürdig sein muss, wird empfohlen, ein Zertifikat zu verwenden, das von einer vertrauenswürdigen Zertifizierungsstelle signiert ist \(ca @ no__t-1. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.|  
|Secure Sockets Layer \(ssl @ no__t-1 Zertifikat|Verbundserver verwenden ein SSL-Zertifikat, um den Webdienstdatenverkehr für die SSL-Kommunikation mit Webclients und Verbundserverproxies zu sichern.<br /><br />Da das SSL-Zertifikat für Clientcomputer vertrauenswürdig sein muss, wird empfohlen, ein Zertifikat zu verwenden, das von einer vertrauenswürdigen Zertifizierungsstelle signiert ist. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.|  
|Token @ no__t-0entschlüsselungs Zertifikat|Dieses Zertifikat wird zum Entschlüsseln von Token verwendet, die von diesem Verbund Server empfangen werden.<br /><br />Sie können mehrere Entschlüsselungszertifikate haben. Dies ermöglicht es einem Ressourcen Verbund Server, Token zu entschlüsseln, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungs Zertifikat festgelegt wurde. Alle Zertifikate können für die Entschlüsselung verwendet werden, aber nur das primäre Token @ no__t-0entschlüsselungszertifikat wird tatsächlich in den Verbund Metadaten veröffentlicht. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.<br /><br />Weitere Informationen finden Sie unter [Hinzufügen eines tokenentschlüsselungszertifikats](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md).|  
  
Sie können ein SSL-Zertifikat oder Dienst Kommunikations Zertifikat anfordern und installieren, indem Sie ein Dienst Kommunikations Zertifikat über die Microsoft Management Console \(mmc @ no__t-1 Snap @ no__t-2in für IIS anfordern. Weitere allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter [iis 7,0: Konfigurieren von Secure Sockets Layer in IIS 7.0 @ no__t-0 und [iis 7,0: Konfigurieren von Server Zertifikaten in IIS 7.0 @ no__t-0.  
  
> [!NOTE]  
> In AD FS Sie \(die SHA\) -Ebene des Secure-Hash-Algorithmus, die für digitale Signaturen verwendet wird\-, entweder in\-SHA 1 oder\)SHA 256 \(sicherer ändern. AD fsunter stützt nicht die Verwendung von Zertifikaten mit anderen Hash Methoden, wie z. b. MD5 \(der Standard Hash Algorithmus, der mit dem Makecert. exe-Befehl @ no__t-1line-Tool @ no__t-2 verwendet wird. Als bewährte Sicherheitsmaßnahme empfiehlt es sich, SHA\-256 \(zu verwenden, das standardmäßig\) für alle Signaturen festgelegt wird. SHA @ no__t-01 wird nur in Szenarien empfohlen, in denen Sie mit einem Produkt interoperieren müssen, das keine Kommunikation mit SHA @ no__t-1256 unterstützt, wie z. b. ein nicht-@ no__t-2microsoft-Produkt oder AD FS 1. *x*.  
  
## <a name="determining-your-ca-strategy"></a>Festlegen Ihrer CA-Strategie  
AD FS ist nicht erforderlich, dass Zertifikate von einer Zertifizierungsstelle ausgestellt werden. Das SSL-Zertifikat \(Das Zertifikat, das standardmäßig auch als Dienst Kommunikations Zertifikat @ no__t-1 verwendet wird, muss von den AD FS Clients als vertrauenswürdig eingestuft werden. Es wird empfohlen, für diese Zertifikat Typen keine selbst signierten Zertifikate zu verwenden.  
  
> [!IMPORTANT]  
> Durch die Verwendung von selbst @ no__t-0signierten SSL-Zertifikaten in einer Produktionsumgebung kann ein böswilliger Benutzer in einer Konto Partnerorganisation die Kontrolle über Verbund Server in einer Ressourcen Partnerorganisation übernehmen. Dieses Sicherheitsrisiko besteht, weil selbst @ no__t-0 signierte Zertifikate Stamm Zertifikate sind. Sie müssen dem vertrauenswürdigen Stamm Speicher eines anderen Verbund Servers hinzugefügt werden \(z. b. dem Ressourcen Verbund Server @ no__t-1, der den Server anfällig für Angriffe machen kann.  
  
Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher auf dem lokalen Computer importiert werden. Zertifikate können mit dem MMC-Snap\--in "Zertifikate" in den persönlichen Speicher importiert werden.  
  
Als Alternative zur Verwendung des Zertifikate-Snap-Ins @ no__t-0in können Sie das SSL-Zertifikat auch mit dem IIS-Manager-Snap @ no__t-1In importieren, wenn Sie das SSL-Zertifikat der Standard Website zuweisen. Weitere Informationen finden Sie unter [Importieren eines Server Authentifizierungs Zertifikats auf die Standard Website](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
> [!NOTE]  
> Vergewissern Sie sich, dass sich beide Zertifikate im persönlichen Zertifikat Speicher des lokalen Computers befinden und das SSL-Zertifikat der Standard Website zugewiesen ist, bevor Sie die AD FS Software auf dem Computer installieren, der als Verbund Server verwendet werden soll. Weitere Informationen zur Reihenfolge der Aufgaben, die zum Einrichten eines Verbund Servers erforderlich sind, finden Sie unter [checkliste: Einrichten eines Verbund Servers @ no__t-0.  
  
Je nach Sicherheits- und Budgetanforderungen sollten Sie sorgfältig in Betracht ziehen, welche Ihrer Zertifikate von einer öffentlichen oder einer Unternehmenszertifizierungsstelle abgerufen werden. In der folgenden Abbildung sind die empfohlenen Zertifizierungsstellenaussteller für einen bestimmten Zertifikattyp dargestellt. Diese Empfehlung spiegelt einen bestmöglichen @ no__t-0practice-Ansatz in Bezug auf Sicherheit und Kosten wider.  
  
![Zertifikat Anforderungen](media/adfs2_fedserver_certstory_1.png)  
  
## <a name="certificate-revocation-lists"></a>Zertifikatsperrliste  
Falls ein von Ihnen verwendetes Zertifikat über Zertifikatsperrlisten (Certificate Revocation Lists, CRLs) verfügt, muss der Server mit dem konfigurierten Zertifikat den Server kontaktieren können, von dem die CRLs verteilt werden.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
