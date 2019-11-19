---
title: Planen der Bereitstellung SSL
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ec5bc315381f85434753f9becc94409a74271b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356105"
---
# <a name="server-certificate-deployment-planning"></a>Planen der Bereitstellung SSL

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Vor dem Bereitstellen von Server Zertifikaten müssen Sie die folgenden Elemente planen:  
  
-   [Planen der grundlegenden Serverkonfiguration](#bkmk_basic)  
  
-   [Planen des Domänen Zugriffs](#bkmk_domain)  
  
-   [Planen Sie den Speicherort und den Namen des virtuellen Verzeichnisses auf dem Webserver.](#bkmk_virtual)  
  
-   [Planen eines DNS-Alias Satzes (CNAME) für Ihren Webserver](#bkmk_cname)  
  
-   [Planen der Konfiguration von "capolicy. inf"](#bkmk_capolicy)  
  
-   [Planen der Konfiguration der CDP-und AIA-Erweiterungen auf CA1](#bkmk_cdp)  
  
-   [Planen des Kopiervorgangs zwischen der Zertifizierungsstelle und dem Webserver](#bkmk_copy)  
  
-   [Planen der Konfiguration der Serverzertifikat Vorlage für die Zertifizierungsstelle](#bkmk_template)  
  
## <a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration  
Nachdem Sie Windows Server 2016 auf den Computern installiert haben, die Sie als Zertifizierungsstelle und Webserver verwenden möchten, müssen Sie den Computer umbenennen und eine statische IP-Adresse für den lokalen Computer zuweisen und konfigurieren.  
  
Weitere Informationen finden Sie im Windows Server 2016- [Kern Netzwerk Handbuch](../../../core-network-guide/Core-Network-Guide.md).  
  
## <a name="bkmk_domain"></a>Planen des Domänen Zugriffs  
Wenn Sie sich bei der Domäne anmelden möchten, muss es sich bei dem Computer um einen Domänen Mitglieds Computer handeln, und das Benutzerkonto muss vor dem Anmeldeversuch in AD DS erstellt werden. Außerdem erfordern die meisten Prozeduren in diesem Handbuch, dass das Benutzerkonto Mitglied der Gruppe Organisations-Admins oder Domänen-Admins in Active Directory Benutzer und Computer ist. Daher müssen Sie sich bei der Zertifizierungsstelle mit einem Konto anmelden, das über die entsprechende Gruppenmitgliedschaft verfügt.  
  
Weitere Informationen finden Sie im Windows Server 2016- [Kern Netzwerk Handbuch](../../../core-network-guide/Core-Network-Guide.md).  
  
## <a name="bkmk_virtual"></a>Planen Sie den Speicherort und den Namen des virtuellen Verzeichnisses auf dem Webserver.  
Zum Bereitstellen des Zugriffs auf die CRL und das Zertifizierungsstellen Zertifikat auf anderen Computern müssen Sie diese Elemente in einem virtuellen Verzeichnis auf dem Webserver speichern. In diesem Handbuch befindet sich das virtuelle Verzeichnis auf dem Webserver WEB1. Dieser Ordner befindet sich auf dem Laufwerk "C:" und hat den Namen "PKI". Sie finden Ihr virtuelles Verzeichnis auf dem Webserver an einem beliebigen Ordner Speicherort, der für Ihre Bereitstellung geeignet ist.  
  
## <a name="bkmk_cname"></a>Planen eines DNS-Alias Satzes (CNAME) für Ihren Webserver  
Alias Ressourcen Einträge (CNAME) werden manchmal auch als kanonische namens Ressourcen Einträge bezeichnet. Mit diesen Datensätzen können Sie mehr als einen Namen verwenden, um auf einen einzelnen Host zu verweisen, sodass es einfach ist, sowohl einen Dateiübertragungsprotokoll (FTP)-Server als auch einen Webserver auf demselben Computer zu hosten. Beispielsweise werden die bekannten Servernamen (FTP, www) mithilfe von Alias Ressourcen Einträge (CNAME) registriert, die dem Domain Name System (DNS)-Hostnamen (z. b. WEB1) für den Server Computer zugeordnet sind, der diese Dienste hostet.  
  
Dieses Handbuch enthält Anweisungen zum Konfigurieren des Webservers zum Hosten der Zertifikat Sperr Liste (CRL) für Ihre Zertifizierungsstelle (Certification Authority, ca). Da Sie den Webserver möglicherweise auch für andere Zwecke verwenden möchten, z. b. zum Hosten einer FTP-oder-Website, empfiehlt es sich, einen Alias Ressourcen Daten Satz in DNS für Ihren Webserver zu erstellen. In dieser Anleitung heißt der CNAME-Datensatz "PKI", aber Sie können einen Namen auswählen, der für Ihre Bereitstellung geeignet ist.  
  
## <a name="bkmk_capolicy"></a>Planen der Konfiguration von "capolicy. inf"  
Vor der Installation von AD CS müssen Sie CAPolicy. inf auf der Zertifizierungsstelle mit Informationen konfigurieren, die für die Bereitstellung korrekt sind. Eine CAPolicy. inf-Datei enthält die folgenden Informationen:  
  
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
  
-   **URL**. Die CAPolicy. inf-Beispieldatei hat den URL-Wert **https://pki.corp.contoso.com/pki/cps.txt** . Der Grund hierfür ist, dass der Webserver in dieser Anleitung den Namen "WEB1" hat und über einen DNS CNAME-Ressourcen Datensatz der PKI verfügt. Der Webserver wird auch der Corp.contoso.com-Domäne hinzugefügt. Außerdem gibt es ein virtuelles Verzeichnis auf dem Webserver mit dem Namen "PKI", in dem die Zertifikat Sperr Liste gespeichert wird. Stellen Sie sicher, dass der Wert, den Sie für die URL in der CAPolicy. inf-Datei angeben, auf ein virtuelles Verzeichnis auf dem Webserver in Ihrer Domäne verweist.  
  
-   **RenewalKeyLength**. Der Standardwert für die Erneuerungs Schlüssellänge für AD CS in Windows Server 2012 ist 2048. Die Schlüssellänge, die Sie auswählen, sollte so lange wie möglich sein, während Sie weiterhin Kompatibilität mit den Anwendungen bereitstellt, die Sie verwenden möchten.  
  
-   **RenewalValidityPeriodUnits**. Die CAPolicy. inf-Beispieldatei weist den Wert "RenewalValidityPeriodUnits" von 5 Jahren auf. Dies liegt daran, dass die erwartete Lebensdauer der Zertifizierungsstelle ungefähr zehn Jahre beträgt. Der Wert von RenewalValidityPeriodUnits sollte die Gesamt Gültigkeitsdauer der Zertifizierungsstelle oder die höchste Anzahl von Jahren widerspiegeln, für die Sie die Registrierung bereitstellen möchten.  
  
-   **CRLPeriodUnits**. Die CAPolicy. inf-Beispieldatei weist einen CRLPeriodUnits-Wert von 1 auf. Dies liegt daran, dass das Aktualisierungs Intervall für die Zertifikat Sperr Liste in dieser Anleitung 1 Woche beträgt. Mit dem Intervall Wert, den Sie mit dieser Einstellung festlegen, müssen Sie die Zertifikat Sperr Liste für die Zertifizierungsstelle auf dem virtuellen Webserver Verzeichnis veröffentlichen, in dem Sie die Zertifikat Sperr Liste speichern und für Computer, die sich im Authentifizierungsprozess befinden, Zugriff darauf gewähren.  
  
-   " **Alternativen**Wert" Mit dieser CAPolicy. inf-Datei wird ein verbesserter Sicherheitsmechanismus implementiert, indem Alternative Signatur Formate implementiert werden. Diese Einstellung sollte nicht implementiert werden, wenn Sie noch über Windows XP-Clients verfügen, die Zertifikate von dieser Zertifizierungsstelle benötigen.  
  
Wenn Sie nicht beabsichtigen, der Public Key-Infrastruktur zu einem späteren Zeitpunkt untergeordnete Zertifizierungsstellen hinzuzufügen, und wenn Sie das Hinzufügen von untergeordneten Zertifizierungsstellen verhindern möchten, können Sie den Schlüssel "pathLength" der Datei "capolicy. inf" mit dem Wert "0" hinzufügen. Kopieren Sie den folgenden Code, und fügen Sie ihn in die Datei ein, um diesen Schlüssel hinzuzufügen:  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> Es wird nicht empfohlen, andere Einstellungen in der Datei "capolicy. inf" zu ändern, es sei denn, Sie haben einen bestimmten Grund dafür.  
  
## <a name="bkmk_cdp"></a>Planen der Konfiguration der CDP-und AIA-Erweiterungen auf CA1  
Wenn Sie die Zertifikat Sperr Listen-Verteilungs Punkte (CRL) und die AIA-Einstellungen (Authority Information Access) auf CA1 konfigurieren, benötigen Sie den Namen des Webservers und den Domänen Namen. Außerdem benötigen Sie den Namen des virtuellen Verzeichnisses, das Sie auf dem Webserver erstellen, auf dem die Zertifikat Sperr Liste (CRL) und das Zertifikat der Zertifizierungsstelle gespeichert werden.  
  
Der CDP-Speicherort, den Sie während dieses Bereitstellungs Schritts eingeben müssen, hat folgendes Format:  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
Wenn Ihr Webserver z. b. den Namen WEB1 hat und Ihr DNS-Alias CNAME-Datensatz für den Webserver "PKI", Ihre Domäne "Corp.contoso.com" lautet und Ihr virtuelles Verzeichnis "PKI" lautet, lautet der CDP-Speicherort wie folgt:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
Der AIA-Speicherort, den Sie eingeben müssen, hat folgendes Format:  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
Wenn Ihr Webserver z. b. den Namen WEB1 hat und Ihr DNS-Alias CNAME-Datensatz für den Webserver "PKI", Ihre Domäne "Corp.contoso.com" lautet und Ihr virtuelles Verzeichnis "PKI" lautet, ist der AIA-Speicherort:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>Planen des Kopiervorgangs zwischen der Zertifizierungsstelle und dem Webserver  
Wenn Sie die Zertifikat Sperr Liste und das Zertifizierungsstellen Zertifikat von der Zertifizierungsstelle auf dem virtuellen Webserver Verzeichnis veröffentlichen möchten, können Sie den Befehl certutil-crl ausführen, nachdem Sie die CDP-und AIA-Standorte der Zertifizierungsstelle konfiguriert haben. Stellen Sie sicher, dass Sie die richtigen Pfade auf der Registerkarte **Erweiterungen** der Zertifizierungsstellen Eigenschaften konfigurieren, bevor Sie diesen Befehl mithilfe der Anweisungen in diesem Handbuch ausführen. Wenn Sie das Zertifikat der Unternehmens Zertifizierungsstelle auf den Webserver kopieren möchten, müssen Sie das virtuelle Verzeichnis auf dem Webserver bereits erstellt und als freigegebenen Ordner konfiguriert haben.  
  
## <a name="bkmk_template"></a>Planen der Konfiguration der Serverzertifikat Vorlage für die Zertifizierungsstelle  
Zum Bereitstellen von automatisch registrierten Server Zertifikaten müssen Sie die Zertifikat Vorlage **RAS-und IAS-Server**kopieren. Standardmäßig wird diese Kopie als **Kopie der RAS-und IAS-Server verwendet**. Wenn Sie diese Vorlagen Kopie umbenennen möchten, planen Sie den Namen, den Sie während dieses Bereitstellungs Schritts verwenden möchten.  
  
> [!NOTE]  
> In den letzten drei Bereitstellungs Abschnitten in diesem Handbuch wird beschrieben, wie Sie die automatische Registrierung von Server Zertifikaten konfigurieren, Gruppenrichtlinie auf Servern aktualisieren und überprüfen, ob die Server ein gültiges Serverzertifikat von der Zertifizierungsstelle erhalten haben. zusätzliche Planung ist nicht erforderlich. nehmen.  
  


