---
title: Planen der Bereitstellung SSL
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: eacfa404da91d14a7a7328646c2320be8220000c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment-planning"></a>Planen der Bereitstellung SSL

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Bevor Sie Serverzertifikate bereitstellen, müssen Sie Folgendes planen:  
  
-   [Planen der grundlegenden Serverkonfiguration](#bkmk_basic)  
  
-   [Planen der Domänenzugriff](#bkmk_domain)  
  
-   [Planen Sie den Speicherort und Namen des virtuellen Verzeichnisses auf dem Webserver](#bkmk_virtual)  
  
-   [Planen eines DNS-Alias (CNAME)-Eintrags für den Webserver](#bkmk_cname)  
  
-   [Planen der Konfiguration des CAPolicy.inf](#bkmk_capolicy)  
  
-   [Planen der Konfiguration von CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1](#bkmk_cdp)  
  
-   [Planen des Kopiervorgangs zwischen der Zertifizierungsstelle und den Webserver](#bkmk_copy)  
  
-   [Planen der Konfiguration der Vorlage für das auf der Zertifizierungsstelle](#bkmk_template)  
  
## <a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration  
Nach der Installation von Windows Server2016 auf den Computern, die Sie als Zertifizierungsstelle und Webserver verwenden möchten, müssen Sie Umbenennen des Computers und zuweisen und konfigurieren eine statische IP-Adresse für den lokalen Computer.  
  
Weitere Informationen finden Sie unter Windows Server2016 [Kernnetzwerkhandbuch](../../../core-network-guide/Core-Network-Guide.md).  
  
## <a name="bkmk_domain"></a>Planen der Domänenzugriff  
Um mit der Domäne anmelden zu können, muss der Computer einen Domänenmitgliedscomputer sein und muss das Benutzerkonto in AD DS vor der Anmeldung erstellt werden. Darüber hinaus müssen die meisten Verfahren in diesem Handbuch das Benutzerkonto ein Mitglied der Gruppen Organisations-Admins oder Domänen-Admins in Active Directory-Benutzer und -Computer ist, damit Sie auf der Zertifizierungsstelle mit einem Konto anmelden müssen, die Mitglied der entsprechenden Gruppe verfügt.  
  
Weitere Informationen finden Sie unter Windows Server2016 [Kernnetzwerkhandbuch](../../../core-network-guide/Core-Network-Guide.md).  
  
## <a name="bkmk_virtual"></a>Planen Sie den Speicherort und Namen des virtuellen Verzeichnisses auf dem Webserver  
Um den Zugriff auf die Zertifikatsperrliste und das Zertifizierungsstellenzertifikat auf anderen Computern zu ermöglichen, müssen Sie diese Elemente in einem virtuellen Verzeichnis auf dem Webserver speichern. In diesem Handbuch befindet sich das virtuelle Verzeichnis auf dem Webserver WEB1. In diesem Ordner auf dem Laufwerk "C:" und ist mit der Bezeichnung "Pki". Das virtuelle Verzeichnis können Sie auf Ihrem Webserver an jedem beliebigen Ordnerspeicherort suchen, die für Ihre Bereitstellung geeignet ist.  
  
## <a name="bkmk_cname"></a>Planen eines DNS-Alias (CNAME)-Eintrags für den Webserver  
Alias (CNAME)-Ressourceneinträge werden auch als Ressourceneinträge kanonischen Namen bezeichnet. Mithilfe dieser Einträge können Sie mehr als einem Namen auf einem einzelnen Host, z.B. Host führen Sie einen Server File Transfer Protocol (FTP) und einem Webserver auf demselben Computer vereinfacht. Beispielsweise werden die bekannten Servernamen (ftp, Www) mit Alias (CNAME)-Ressourceneinträge, die der Domain Name System (DNS) Host ein, z.B. WEB1 für den Servercomputer, der als Host zuordnen dieser Dienste registriert.  
  
Dieses Handbuch enthält Anweisungen zum Konfigurieren des Webservers zum Hosten der Zertifikatssperrliste (CRL) für die Zertifizierungsstelle (CA). Da Sie auch Ihre Web-Server für andere Zwecke verwenden, z.B. verwenden, um eine FTP- oder eine Website hosten möchten, ist es sinnvoll, ein Aliasressourceneintrags in DNS für den Webserver zu erstellen. In diesem Handbuch der CNAME-Eintrag lautet "Pki", aber Sie können einen geeigneten Namen für die Bereitstellung auswählen.  
  
## <a name="bkmk_capolicy"></a>Planen der Konfiguration des CAPolicy.inf  
Vor der Installation von AD CS müssen Sie auf der Zertifizierungsstelle mit Informationen, die für Ihre Bereitstellung korrekt ist, die CAPolicy.inf konfigurieren. Eine CAPolicy.inf-Datei enthält die folgende Informationen:  
  
```  
[Version]  
Signature="$Windows NT$"  
[PolicyStatementExtension]  
Policies=InternalPolicy  
[InternalPolicy]  
OID=1.2.3.4.1455.67.89.5  
Notice="Legal Policy Statement"  
URL=http://pki.corp.contoso.com/pki/cps.txt  
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
  
-   **URL**. Die Beispiel-CAPolicy.inf-Datei verfügt über eine URL-Wert des **http://pki.corp.contoso.com/pki/cps.txt**. Dies ist, da der Webserver in diesem Handbuch wird mit dem Namen WEB1 und verfügt über einen DNS CNAME-Ressourceneintrag PKI. Der Webserver ist auch der Domäne corp.contoso.com hinzugefügt. Darüber hinaus besteht ein virtuelles Verzeichnis auf dem Webserver, der mit dem Namen "Pki", in dem die Zertifikatsperrliste gespeichert ist. Sicherstellen Sie, dass den Wert, den Sie für die URL in der CAPolicy.inf-Datei in ein virtuelles Verzeichnis auf dem Webserver in der Domäne bereitstellen.  
  
-   **RenewalKeyLength**. Die Verlängerung für AD CS in Windows Server2012 beträgt 2048. Die Länge des Schlüssels, die Sie auswählen sollten werden so lange wie möglich dabei aber nicht auf Kompatibilität mit Anwendungen, die Sie verwenden möchten.  
  
-   **RenewalValidityPeriodUnits**. Die Beispiel-CAPolicy.inf-Datei hat RenewalValidityPeriodUnits Wert 5Jahre. Dies liegt daran die erwartete Lebensdauer von der Zertifizierungsstelle rund zehn Jahren. Der Wert der RenewalValidityPeriodUnits sollte die gesamten Gültigkeitsdauer der die Zertifizierungsstelle oder die höchste Anzahl von Jahren, die für die Anmeldung bereitstellen möchten widerspiegeln.  
  
-   **CRLPeriodUnits**. Die Beispiel-CAPolicy.inf-Datei hat "CRLPeriodUnits" der Wert 1. Dies ist das Aktualisierungsintervall Beispiel für die Zertifikatssperrliste in dieser Anleitung ist 1 Woche. Bei der Intervallwert, den Sie mit dieser Einstellung angeben, müssen Sie die Zertifikatsperrliste der Zertifizierungsstelle auf Server virtuelle Verzeichnis der Website Sie die Zertifikatsperrliste speichern veröffentlichen und ermöglichen den Zugriff auf diese für Computer, die bei der Authentifizierung werden.  
  
-   **AlternateSignatureAlgorithm**. Diese CAPolicy.inf implementiert einen Mechanismus für die erhöhte Sicherheit durch die Implementierung der Signatur Formate. Sie sollten diese Einstellung nicht implementieren, besitzen Sie immer noch Windows XP-Clients, die von dieser Zertifizierungsstelle Zertifikate erforderlich sind.  
  
Wenn Sie nicht beabsichtigen, auf alle untergeordneten Zertifizierungsstellen die public Key-Infrastruktur zu einem späteren Zeitpunkt hinzufügen und Sie möchten, dass das Hinzufügen aller untergeordneten Zertifizierungsstellen, können Sie den Schlüssel "pathLength" in die Datei "CAPolicy.inf" mit dem Wert 0 hinzufügen. Um diesen Schlüssel hinzuzufügen, kopieren Sie, und fügen Sie den folgenden Code in die Datei:  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> Es wird nicht empfohlen, dass Sie alle anderen Einstellungen in der CAPolicy.inf-Datei ändern, es sei denn, Sie einen bestimmten Grund haben dafür.  
  
## <a name="bkmk_cdp"></a>Planen der Konfiguration von CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1  
Wenn Sie die Windows-Verwaltungsinstrumentation (Certificate Revocation List, CRL) Verteilungspunkt (CDP) und die Einstellungen (Authority Information Access, AIA) für Zertifizierungsstelle 1 konfigurieren, benötigen Sie den Namen des Webservers und Ihren Domänennamen. Außerdem benötigen Sie den Namen des virtuellen Verzeichnisses, die Sie auf Ihrem Webserver erstellen, in dem die Zertifikatssperrliste (CRL) und das Zertifikat der Zertifizierungsstelle gespeichert sind.  
  
Die CDP-Speicherort, den Sie, während dieses Bereitstellungsschritts eingeben müssen hat das Format:  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
Wenn beispielsweise Webservers WEB1 den Namen und Ihr DNS-alias CNAME-Eintrag für den Webserver "Pki", Ihre Domäne ist corp.contoso.com, und das virtuelle Verzeichnis ist mit dem Namen Pki, der CDP-Speicherort ist:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
Die AIA-Speicherort, den Sie eingeben müssen, hat das Format:  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
Wenn beispielsweise Webservers WEB1 den Namen und Ihr DNS-alias CNAME-Eintrag für den Webserver "Pki", Ihre Domäne ist corp.contoso.com, und das virtuelle Verzeichnis ist mit dem Namen Pki, der AIA-Speicherort ist:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>Planen des Kopiervorgangs zwischen der Zertifizierungsstelle und den Webserver  
Zum Veröffentlichen der Zertifikatsperrliste und des Zertifizierungsstellenzertifikats Zertifikat von der Zertifizierungsstelle zum virtuellen Verzeichnis Web-Server können Sie den Certutil - Crl der Befehl ausführen, nach dem Konfigurieren der CDP- und AIA-Speicherorten auf der Zertifizierungsstelle. Stellen Sie sicher, dass Sie die korrekten Pfade zu den Eigenschaften der Zertifizierungsstelle konfigurieren **Erweiterungen** Registerkarte vor dem Ausführen dieses Befehls anhand der Anweisungen in diesem Handbuch. Darüber hinaus um das Unternehmens-ZS-Zertifikat an den Webserver zu kopieren, müssen Sie bereits das virtuelle Verzeichnis auf dem Webserver erstellt und konfiguriert haben den Ordner als freigegebener Ordner.  
  
## <a name="bkmk_template"></a>Planen der Konfiguration der Vorlage für das auf der Zertifizierungsstelle  
Um automatisch registrierte Zertifikate bereitzustellen, müssen Sie die Zertifikatvorlage, die mit dem Namen kopieren **RAS- und IAS-Server**. Standardmäßig heißt diese Kopie **Kopie von RAS- und IAS-Server**. Wenn Sie diese vorlagenkopie umbenennen möchten, Planen Sie den Namen, den Sie während dieses Bereitstellungsschritts verwenden möchten.  
  
> [!NOTE]  
> In den letzten drei Bereitstellung Abschnitten in diesem Handbuch - die können Sie zum Konfigurieren von Serverzertifikaten, aktualisieren die Gruppenrichtlinie auf Servern, und stellen Sie sicher, dass der Server ein gültiges Serverzertifikat von der Zertifizierungsstelle erhalten haben – erfordern keine weiteren Planungsschritte erforderlich.  
  


