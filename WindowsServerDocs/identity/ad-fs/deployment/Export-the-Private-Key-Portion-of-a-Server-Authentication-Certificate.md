---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: dcc6332881fa4ff0143604eebb491f8ed48283c2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972217"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats

Jeder Verbund Server in einer Active Directory-Verbunddienste (AD FS) \( AD FS \) Farm muss Zugriff auf den privaten Schlüssel des Server Authentifizierungs Zertifikats haben. Wenn Sie eine Serverfarm mit Verbund Servern oder Webservern implementieren, benötigen Sie ein einzelnes Authentifizierungszertifikat. Dieses Zertifikat muss von einer Zertifizierungsstellen-Zertifizierungsstellen Zertifizierungsstelle ausgestellt werden \( \) , und es muss über einen exportierbaren privaten Schlüssel verfügen. Der private Schlüssel des Serverauthentifizierungszertifikats muss exportierbar sein, damit er für alle Server in der Farm zur Verfügung gestellt werden kann.

Dasselbe Konzept gilt für Verbund Server Proxy-Farmen in dem Sinne, dass alle Verbund Server Proxys in einer Farm den privaten Schlüsselteil desselben Server Authentifizierungs Zertifikats gemeinsam nutzen müssen.

> [!NOTE]
> Das Snap-in "AD FS-Verwaltung" \- bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.

Abhängig von der Rolle, die dieser Computer wieder gibt, verwenden Sie dieses Verfahren auf dem Verbund Server Computer oder dem Verbund Server Proxy-Computer, auf dem Sie das Server Authentifizierungszertifikat mit dem privaten Schlüssel installiert haben. Wenn das Verfahren abgeschlossen ist, können Sie dieses Zertifikat dann auf der Standardwebsite jedes Servers in der Farm importieren. Weitere Informationen finden Sie unter [Importieren eines Server Authentifizierungs Zertifikats auf die Standard Website](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>So exportieren Sie den Bereich mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats

1. Geben Sie auf dem **Start** Bildschirm**Internetinformationsdienste \( IIS- \) Manager**ein, und drücken Sie dann die EINGABETASTE.

2. Klicken Sie in der Konsolenstruktur auf **ComputerName**.

3. Doppelklicken Sie im mittleren Bereich \- auf **Server Zertifikate**.

4. Klicken Sie im mittleren Bereich mit \- der rechten Maustaste auf das Zertifikat, das Sie exportieren möchten, und klicken Sie dann auf **exportieren**.

5. Klicken Sie im Dialogfeld **Zertifikat exportieren** auf die **...** .

6. Geben Sie unter **Dateiname den Namen** ** \\ C:**<em>nameof Certificate</em>ein, und klicken Sie dann auf **Öffnen**.

7. Geben Sie das Kennwort für das Zertifikat ein, bestätigen Sie das Kennwort, und klicken Sie dann auf **OK**.

8. Überprüfen Sie den Erfolg Ihres Exportvorgangs, indem Sie bestätigen, dass die von Ihnen angegebene Daten am angegebenen Standort erstellt wird.

   > [!IMPORTANT]
   > Damit dieses Zertifikat in den lokalen Zertifikatspeicher auf dem neuen Server importiert werden, müssen Sie die Datei auf ein physisches Speichermedium übertragen und ihre Sicherheit während des Transports auf den neuen Server sichern. Es ist äußerst wichtig, die Sicherheit des privaten Schlüssels zu gewähren. Wenn dieser Schlüssel gefährdet ist, wird die Sicherheit Ihrer gesamten AD FS Bereitstellung, \( einschließlich der Ressourcen in Ihrer Organisation und in Ressourcen Partnerorganisationen, \) beeinträchtigt.

9. Importieren Sie das exportierte Serverauthentifizierungszertifikat in den Zertifikatspeicher auf dem neuen Server, bevor Sie den Verbunddienst installieren. Weitere Informationen zum Importieren des Zertifikats finden Sie unter Importieren eines Server Zertifikats \( [http: \/ \/ go.Microsoft.com \/ fwlink \/ ? LinkId \= 108283](https://go.microsoft.com/fwlink/?LinkId=108283) \) .

## <a name="additional-references"></a>Weitere Verweise
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)

[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)

[Zertifikatanforderungen für Verbundserver](../design/certificate-requirements-for-federation-servers.md)

[Zertifikatanforderungen für Verbundserverproxys](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807054(v=ws.11))

