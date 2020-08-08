---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: Zertifikatanforderungen für Verbundserver
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: fcf78fa6242c10d469320ce3803da94134576c8b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954366"
---
# <a name="certificate-requirements-for-federation-servers"></a>Zertifikatanforderungen für Verbundserver

In allen Active Directory-Verbunddienste (AD FS) \( AD FS \) Entwurf müssen verschiedene Zertifikate verwendet werden, um die Kommunikation zu sichern und Benutzer Authentifizierungen zwischen Internet Clients und Verbund Servern zu vereinfachen. Jeder Verbund Server muss über ein Dienst Kommunikations Zertifikat und ein \- Tokensignaturzertifikat verfügen, bevor er an AD FS-Kommunikation teilnehmen kann. In der folgenden Tabelle werden die Zertifikat Typen beschrieben, die dem Verbund Server zugeordnet sind.

|Zertifikattyp|BESCHREIBUNG|
|--------------------|---------------|
|\-Tokensignaturzertifikat|Ein \- Tokensignaturzertifikat ist ein X509-Zertifikat. Verbund Server verwenden zugeordnete öffentliche \/ private Schlüsselpaare, um alle von ihnen produzierten Sicherheits Token Digital zu signieren. Dazu gehört das Signieren von veröffentlichten Verbundmetadaten und Artefaktauflösungsanforderungen.<p>Sie können mehrere \- Tokensignaturzertifikate im AD FS-Verwaltungs-Snap \- in konfigurieren, um ein zertifikatrol Lover zuzulassen, wenn ein Zertifikat fast abläuft. Standardmäßig werden alle Zertifikate in der Liste veröffentlicht, aber nur das primäre \- Tokensignaturzertifikat wird von AD FS verwendet, um Token tatsächlich zu signieren. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.<p>Weitere Informationen finden Sie unter [Tokensignaturzertifikate](Token-Signing-Certificates.md) und [Hinzufügen eines Tokensignaturzertifikats](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md).|
|Dienstkommunikationszertifikat|Verbund Server verwenden ein Server Authentifizierungszertifikat, das auch als Dienst Kommunikation für Windows Communication Foundation \( WCF- \) Nachrichten Sicherheit bezeichnet wird. Standardmäßig handelt es sich hierbei um dasselbe Zertifikat, das ein Verbund Server \( in Internetinformationsdienste IIS als Secure Sockets Layer SSL- \) Zertifikat verwendet \( \) . **Hinweis:** Das Snap-in "AD FS-Verwaltung" \- bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.<p>Weitere Informationen finden Sie unter [Dienst Kommunikations Zertifikate](Service-Communications-Certificates.md) und [Festlegen eines Dienst Kommunikations Zertifikats](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md).<p>Da das Dienst Kommunikations Zertifikat für Client Computer vertrauenswürdig sein muss, wird empfohlen, ein Zertifikat zu verwenden, das von einer Zertifizierungsstellen-Zertifizierungsstelle signiert wurde \( \) . Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.|
|\(SSL- \) Zertifikat Secure Sockets Layer|Verbundserver verwenden ein SSL-Zertifikat, um den Webdienstdatenverkehr für die SSL-Kommunikation mit Webclients und Verbundserverproxies zu sichern.<p>Da das SSL-Zertifikat für Clientcomputer vertrauenswürdig sein muss, wird empfohlen, ein Zertifikat zu verwenden, das von einer vertrauenswürdigen Zertifizierungsstelle signiert ist. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.|
|\-Tokenentschlüsselungszertifikat|Dieses Zertifikat wird zum Entschlüsseln von Token verwendet, die von diesem Verbund Server empfangen werden.<p>Sie können mehrere Entschlüsselungszertifikate haben. Dies ermöglicht es einem Ressourcen Verbund Server, Token zu entschlüsseln, die mit einem älteren Zertifikat ausgestellt werden, nachdem ein neues Zertifikat als primäres Entschlüsselungs Zertifikat festgelegt wurde. Alle Zertifikate können für die Entschlüsselung verwendet werden, aber nur das primäre \- tokenentschlüsselungszertifikat wird tatsächlich in den Verbund Metadaten veröffentlicht. Alle von Ihnen ausgewählten Zertifikate müssen über einen entsprechenden privaten Schlüssel verfügen.<p>Weitere Informationen finden Sie unter [Hinzufügen eines tokenentschlüsselungszertifikats](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md).|

Sie können ein SSL-Zertifikat oder Dienst Kommunikations Zertifikat anfordern und installieren, indem Sie über das MMC-Snap-in Microsoft Management Console \( \) für IIS ein Dienst Kommunikations Zertifikat anfordern \- . Weitere allgemeine Informationen zur Verwendung von SSL-Zertifikaten finden Sie unter [IIS 7,0: Konfigurieren von Secure Sockets Layer in IIS 7,0](https://go.microsoft.com/fwlink/?LinkID=108544) und [IIS 7,0: Konfigurieren von Server Zertifikaten in IIS 7,0](https://go.microsoft.com/fwlink/?LinkID=108545) .

> [!NOTE]
> In AD FS Sie die SHA-Ebene des Secure-Hash-Algorithmus \( \) , die für digitale Signaturen verwendet wird, entweder in Sha \- 1 oder SHA 256 sicherer ändern \- \( \) . AD fsunter stützt nicht die Verwendung von Zertifikaten mit anderen Hash Methoden, wie z. b. MD5, \( dem Standard Hash Algorithmus, der mit dem Makecert.exe-Befehls \- Zeilen Tool verwendet wird \) . Als bewährte Sicherheitsmaßnahme empfiehlt es sich, SHA \- 256 zu verwenden, \( das standardmäßig \) für alle Signaturen festgelegt wird. SHA \- 1 wird nur in Szenarien empfohlen, in denen Sie mit einem Produkt interoperieren müssen, das keine Kommunikation über SHA 256 unterstützt \- , wie z. b. ein nicht- \- Microsoft-Produkt oder AD FS 1. *x*.

## <a name="determining-your-ca-strategy"></a>Festlegen Ihrer CA-Strategie
AD FS ist nicht erforderlich, dass Zertifikate von einer Zertifizierungsstelle ausgestellt werden. Das SSL-Zertifikat für das \( Zertifikat, das standardmäßig auch als Dienst Kommunikations Zertifikat verwendet wird, \) muss jedoch von den AD FS Clients als vertrauenswürdig eingestuft werden. Es wird empfohlen, \- für diese Zertifikat Typen keine selbst signierten Zertifikate zu verwenden.

> [!IMPORTANT]
> Durch die Verwendung von selbst \- signierten SSL-Zertifikaten in einer Produktionsumgebung kann ein böswilliger Benutzer in einer Konto Partnerorganisation die Kontrolle über Verbund Server in einer Ressourcen Partnerorganisation übernehmen. Dieses Sicherheitsrisiko besteht, weil selbst \- signierte Zertifikate Stamm Zertifikate sind. Sie müssen dem vertrauenswürdigen Stamm Speicher eines anderen Verbund Servers hinzugefügt werden, \( z. b. dem Ressourcen Verbund Server \) , der diesen Server anfällig für Angriffe machen kann.

Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher auf dem lokalen Computer importiert werden. Zertifikate können mit dem MMC-Snap-in "Zertifikate" in den persönlichen Speicher importiert werden \- .

Als Alternative zur Verwendung des Snap-Ins "Zertifikate" \- können Sie das SSL-Zertifikat auch mit dem Snap-in "IIS-Manager" importieren, wenn \- Sie das SSL-Zertifikat der Standard Website zuweisen. Weitere Informationen finden Sie unter [Importieren eines Server Authentifizierungs Zertifikats auf die Standard Website](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).

> [!NOTE]
> Vergewissern Sie sich, dass sich beide Zertifikate im persönlichen Zertifikat Speicher des lokalen Computers befinden und das SSL-Zertifikat der Standard Website zugewiesen ist, bevor Sie die AD FS Software auf dem Computer installieren, der als Verbund Server verwendet werden soll. Weitere Informationen zur Reihenfolge der Aufgaben, die zum Einrichten eines Verbund Servers erforderlich sind, finden Sie unter Prüfliste [: Einrichten eines Verbund Servers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).

Je nach Sicherheits- und Budgetanforderungen sollten Sie sorgfältig in Betracht ziehen, welche Ihrer Zertifikate von einer öffentlichen oder einer Unternehmenszertifizierungsstelle abgerufen werden. In der folgenden Abbildung sind die empfohlenen Zertifizierungsstellenaussteller für einen bestimmten Zertifikattyp dargestellt. Diese Empfehlung stellt einen bewährten \- Ansatz hinsichtlich Sicherheit und Kosten dar.

![Zertifikat Anforderungen](media/adfs2_fedserver_certstory_1.png)

## <a name="certificate-revocation-lists"></a>Zertifikatsperrliste
Falls ein von Ihnen verwendetes Zertifikat über Zertifikatsperrlisten (Certificate Revocation Lists, CRLs) verfügt, muss der Server mit dem konfigurierten Zertifikat den Server kontaktieren können, von dem die CRLs verteilt werden.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
