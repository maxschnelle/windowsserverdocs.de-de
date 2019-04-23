---
title: Planen der Bereitstellung SSL
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b0d14ed33c9bf389433f59774c04ff15e37256cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839531"
---
# <a name="server-certificate-deployment-planning"></a>Planen der Bereitstellung SSL

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bevor Sie Server-Zertifikate bereitstellen, müssen Sie Folgendes planen:  
  
-   [Planen der grundlegenden Serverkonfiguration](#bkmk_basic)  
  
-   [Zugriff auf den Plan-Domäne](#bkmk_domain)  
  
-   [Planen Sie den Speicherort und Namen des virtuellen Verzeichnisses auf dem Webserver](#bkmk_virtual)  
  
-   [Planen Sie einen DNS-Alias (CNAME)-Eintrag für Ihre Web-server](#bkmk_cname)  
  
-   [Planen der Konfiguration der Datei "CAPolicy.inf"](#bkmk_capolicy)  
  
-   [Planen der Konfiguration der CDP- und AIA-Erweiterungen auf CA1](#bkmk_cdp)  
  
-   [Planen Sie den Kopiervorgang zwischen der CA und dem Webserver](#bkmk_copy)  
  
-   [Planen Sie die Konfiguration der Zertifikatvorlage für die Zertifizierungsstelle](#bkmk_template)  
  
## <a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration  
Nach der Installation von Windows Server 2016 auf den Computern, die Sie als Zertifizierungsstelle und Webserver verwenden möchten, müssen Sie Umbenennen des Computers und zuweisen und konfigurieren eine statische IP-Adresse für den lokalen Computer.  
  
Weitere Informationen finden Sie unter Windows Server 2016 [Core Network Guide](../../../core-network-guide/Core-Network-Guide.md).  
  
## <a name="bkmk_domain"></a>Zugriff auf den Plan-Domäne  
Zum Anmelden an der Domäne der Computer muss ein Domänenmitgliedscomputer sein, und das Benutzerkonto muss vor der Anmeldung in AD DS erstellt werden. Darüber hinaus erfordern die meisten Verfahren in diesem Handbuch an, dass das Benutzerkonto ist ein Mitglied der Gruppen "Organisations-Admins oder Domänen-Admins" in Active Directory-Benutzer und-Computer aus, damit Sie mit der Zertifizierungsstelle mit einem Konto anmelden müssen, die die entsprechende Gruppe Mitglied ist.  
  
Weitere Informationen finden Sie unter Windows Server 2016 [Core Network Guide](../../../core-network-guide/Core-Network-Guide.md).  
  
## <a name="bkmk_virtual"></a>Planen Sie den Speicherort und Namen des virtuellen Verzeichnisses auf dem Webserver  
Um Zugriff auf die Zertifikatsperrliste und das Zertifizierungsstellenzertifikat auf anderen Computern zu ermöglichen, müssen Sie diese Elemente in einem virtuellen Verzeichnis auf Ihrem Webserver speichern. In diesem Leitfaden befindet sich das virtuelle Verzeichnis auf dem Webserver WEB1. In diesem Ordner auf dem Laufwerk "C:" ist und Sie heißt "Pki". Sie können das virtuelle Verzeichnis auf dem Webserver auf einem beliebigen Ordner suchen, die für Ihre Bereitstellung geeignet ist.  
  
## <a name="bkmk_cname"></a>Planen Sie einen DNS-Alias (CNAME)-Eintrag für Ihre Web-server  
Alias (CNAME)-Ressourceneinträge werden manchmal auch kanonischen Namen-Ressourceneinträge genannt. Diese Datensätze können Sie mehr als einen Namen, zeigen Sie auf einen einzelnen Host, und Dies erleichtert u.a. der Host sowohl eines Protokolls FTP (File Transfer)-Servers als auch einen Webserver auf demselben Computer ausgeführt werden. Beispielsweise sind die bekannten Servernamen ("ftp", "Www") mithilfe von Aliasressourceneintrags (CNAME)-Ressourceneinträge, die an den Domain Name System (DNS) Hostnamen an, wie z. B. WEB1 für die Server-Computer, der als Host zuordnen dieser Dienste registriert.  
  
Dieses Handbuch enthält Anweisungen zum Konfigurieren von Ihrem Webserver zum Hosten der Zertifikatsperrliste (CRL) Ihrer Zertifizierungsstelle (CA). Da möglicherweise Sie auch den Webserver für andere Zwecke, z. B. zu verwenden, um eine FTP- oder -Website zu hosten möchten, ist es eine gute Idee, einen Aliasressourceneintrag im DNS für Ihre Web-Server zu erstellen. In diesem Handbuch der CNAME-Eintrag wird mit der Bezeichnung "Pki", jedoch können Sie einen Namen, der für Ihre Bereitstellung geeignet ist.  
  
## <a name="bkmk_capolicy"></a>Planen der Konfiguration der Datei "CAPolicy.inf"  
Vor der Installation von AD CS müssen Sie auf der Zertifizierungsstelle mit Informationen, die für die Bereitstellung richtig ist, die Datei "CAPolicy.inf" konfigurieren. Eine Datei "CAPolicy.inf" enthält die folgenden Informationen an:  
  
```  
[Version]  
Signature="$Windows NT$"  
[PolicyStatementExtension]  
Policies=InternalPolicy  
[InternalPolicy]  
OID=1.2.3.4.1455.67.89.5  
Notice="Legal Policy Statement"  
URL=https://pki.corp.contoso.com/pki/cps.txt  
[Certsrv_Server]  
RenewalKeyLength=2048  
RenewalValidityPeriod=Years  
RenewalValidityPeriodUnits=5  
CRLPeriod=weeks  
CRLPeriodUnits=1  
LoadDefaultTemplates=0  
AlternateSignatureAlgorithm=1  
```  
Sie müssen die folgenden Elemente für diese Datei planen:  
  
-   **URL**. Die Beispieldatei für die Datei "CAPolicy.inf" verfügt über einen URL-Wert, der **https://pki.corp.contoso.com/pki/cps.txt**. Dies ist daran, dass der Webserver in diesem Handbuch WEB1 heißt und verfügt über einen DNS CNAME-Ressourceneintrag PKI. Der Webserver ist auch mit der Domäne corp.contoso.com verknüpft. Darüber hinaus besteht ein virtuelles Verzeichnis auf dem Webserver, der mit dem Namen "Pki", in dem der Sperrliste gespeichert ist. Stellen Sie sicher, dass den Wert, den Sie für die URL in der Datei "CAPolicy.inf" in ein virtuelles Verzeichnis auf Ihrem Webserver in der Domäne bereitstellen.  
  
-   **RenewalKeyLength**. Die Standard-Erneuerung-Schlüssellänge für AD CS in Windows Server 2012 ist 2048. Die Länge des Schlüssels, die Sie auswählen sollten werden so lange wie möglich Gewährleistung der Kompatibilität mit Anwendungen, die Sie verwenden möchten.  
  
-   **RenewalValidityPeriodUnits**. Die Beispieldatei für die Datei "CAPolicy.inf" verfügt über einen RenewalValidityPeriodUnits-Wert von fünf Jahren. Dies ist, da die erwartete Lebensdauer von der Zertifizierungsstelle ca. zehn Jahren ist. Der Wert RenewalValidityPeriodUnits sollten wider, die allgemeine Gültigkeitsdauer der Zertifizierungsstelle oder der höchsten Anzahl von Jahren, die für die Sie die Registrierung bereitstellen möchten.  
  
-   **CRLPeriodUnits**. Die Beispieldatei für die Datei "CAPolicy.inf" verfügt über CRLPeriodUnits Wert 1. Dies ist, da das Beispiel-Aktualisierungsintervall für die Zertifikatsperrliste in diesem Handbuch 1 Woche ist. Bei dem Intervallwert, den Sie mit dieser Einstellung angeben, müssen Sie Veröffentlichen der Zertifikatsperrliste bei der Zertifizierungsstelle auf das Web Server virtuelle Verzeichnis, in dem Sie die Zertifikatsperrliste gespeichert, und ermöglichen den Zugriff auf die sie für Computer, die bei der Authentifizierung benötigt werden.  
  
-   **AlternateSignatureAlgorithm**. Diese Datei "CAPolicy.inf" implementiert einen Mechanismus für die Verbesserung der Sicherheit durch Implementieren von anderen Signatur Formate. Sie sollten diese Einstellung nicht implementieren, wenn Sie noch Windows XP-Clients verfügen, die Zertifikate von dieser Zertifizierungsstelle benötigen.  
  
Wenn Sie nicht zum Hinzufügen von jedem untergeordneten Zertifizierungsstellen zu Ihrer public Key-Infrastruktur zu einem späteren Zeitpunkt planen und Sie das Hinzufügen aller untergeordneten Zertifizierungsstellen verhindern möchten, können Sie den Schlüssel "pathLength" zu Ihrer Datei "CAPolicy.inf" mit einem Wert von 0 hinzufügen. Um diesen Schlüssel hinzuzufügen, kopieren Sie den folgenden Code in die Datei:  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> Es wird nicht empfohlen, dass Sie alle anderen Einstellungen in der Datei "CAPolicy.inf" ändern, es sei denn, Sie einen bestimmten Grund dafür haben.  
  
## <a name="bkmk_cdp"></a>Planen der Konfiguration der CDP- und AIA-Erweiterungen auf CA1  
Wenn Sie die Windows-Verwaltungsinstrumentation (Certificate Revocation List, CRL) Verteilungspunkt (CDP) und die Windows-Verwaltungsinstrumentation (Authority Information Access, AIA)-Einstellungen auf CA1 konfigurieren, benötigen Sie den Namen des Webservers sowie Ihren Domänennamen ein. Außerdem benötigen Sie den Namen des virtuellen Verzeichnisses, die Sie auf dem Webserver erstellen, wo die Zertifikatsperrliste (CRL) und das Zertifikat gespeichert werden.  
  
Die CDP-Speicherort, den Sie, während dieses Schritts für die Bereitstellung eingeben müssen hat das Format:  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
Z. B. wenn es sich bei Ihrem Webserver heißt WEB1 und Ihrem DNS-CNAME-Eintrag für den Webserver alias "Pki", Ihrer Domäne "corp.contoso.com", und das virtuelle Verzeichnis wird mit dem Namen Pki ist der CDP-Speicherort ist:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
Die AIA-Speicherort, den Sie eingeben müssen, hat das Format:  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
Z. B. wenn der Webserver heißt WEB1 und Ihrem DNS-CNAME-Eintrag für den Webserver alias "Pki", die Domäne ist "corp.contoso.com", und das virtuelle Verzeichnis wird mit dem Namen Pki, der AIA-Speicherort ist:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>Planen Sie den Kopiervorgang zwischen der CA und dem Webserver  
Um die Zertifikatsperrlisten und CA-Zertifikat von der Zertifizierungsstelle auf das virtuelle Verzeichnis des Web-Server zu veröffentlichen, können Sie den Certutil - Crl der Befehl ausführen, nachdem Sie die CDP- und AIA-Speicherorten für die Zertifizierungsstelle konfiguriert haben. Stellen Sie sicher, dass Sie die richtigen Pfade zu den Eigenschaften der Zertifizierungsstelle konfigurieren **Erweiterungen** Registerkarte vor dem Ausführen dieses Befehls mithilfe der Anweisungen in diesem Handbuch. Darüber hinaus um das Unternehmens-ZS-Zertifikat an den Webserver zu kopieren, müssen Sie bereits das virtuelle Verzeichnis auf dem Webserver erstellt und konfiguriert haben den Ordner als freigegebener Ordner.  
  
## <a name="bkmk_template"></a>Planen Sie die Konfiguration der Zertifikatvorlage für die Zertifizierungsstelle  
Um automatisch registrierte Serverzertifikate bereitzustellen, müssen Sie die Zertifikatvorlage, die mit dem Namen kopieren **RAS- und IAS-Server**. Standardmäßig heißt diese Kopie **Kopie von RAS- und IAS-Server**. Wenn Sie diese Kopie der Vorlage umbenennen möchten, sollten Sie den Namen, den Sie während dieses Schritts für die Bereitstellung verwenden möchten.  
  
> [!NOTE]  
> In den letzten drei Bereitstellung Abschnitten in diesem Handbuch – Was können Sie zum Konfigurieren der automatischen Registrierung von Serverzertifikaten Gruppenrichtlinie auf Servern aktualisieren, und stellen Sie sicher, dass die Server ein gültiges Serverzertifikat von der Zertifizierungsstelle erhalten haben - ist keine zusätzliche Planung erforderlich. die Schritte.  
  


