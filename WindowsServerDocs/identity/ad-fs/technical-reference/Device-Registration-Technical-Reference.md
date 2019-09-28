---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: Technische Referenz zur Geräteregistrierung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ab78a5847c52650f2a608dfc89e2001cc43153ff
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407354"
---
# <a name="device-registration-technical-reference"></a>Technische Referenz zur Geräteregistrierung
Der Geräte Registrierungsdienst \(drs @ no__t-1 ist ein neuer Windows-Dienst, der in der Active Directory Verbunddienst-Rolle unter Windows Server 2012 R2 enthalten ist.  Der DRS muss auf allen Verbundservern der AD FS-Farm installiert und konfiguriert sein.  Informationen zum Bereitstellen des DRS finden Sie unter [Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst](https://technet.microsoft.com/library/dn486831.aspx).  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>Bei Registrierung eines Geräts erstellte Active Directory-Objekte  
Die folgenden Active Directory-Objekte werden als Teil des Geräteregistrierungsdiensts erstellt.  
  
### <a name="device-registration-configuration"></a>Geräteregistrierungskonfiguration  
Die Geräteregistrierungskonfiguration wird im Konfigurationsnamenskontext der Active Directory-Gesamtstruktur gespeichert. \(z. b. **CN @ no__t-2device Registration Configuration, CN @ no__t-3services, < Configuration @ no__t-4naming @ no__t-5context >** \). Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung initialisiert wird.  
  
Die Geräteregistrierungskonfiguration umfasst die folgenden Elemente:  
  
-   **Aussteller Schlüssel**  
  
    Die öffentlichen und privaten Schlüssel, die zur Ausstellung des einem registrierten Gerät zugeordneten X.509-Zertifikats verwendet wurden.  Die privaten Schlüssel sind DKM (Distributed Key Management, verteilte Schlüsselverwaltung)-geschützt.  
  
-   **Konfiguration des Geräte Registrierungs Dienstanbieter**  
  
    Richtlinien, die im Zusammenhang mit dem Geräteregistrierungsdienst stehen.  
  
### <a name="registered-devices-container"></a>Container für registrierte Geräte  
Der Geräte-Objektcontainer wird unter einer der Domänen in der Active Directory-Gesamtstruktur erstellt.  Dieser Objektcontainer enthält alle Geräteobjekte für die Active Directory-Gesamtstruktur.  
  
Standardmäßig wird der Container in derselben Domäne wie AD FS erstellt.  \(z. b. **CN @ no__t-2registereddevices, DC @ no__t-3 < Standardwert @ no__t-4naming @ no__t-5context >** \). Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung initialisiert wird.  
  
### <a name="registered-devices"></a>Registrierte Geräte  
Geräteobjekte sind neue Lightweight-Objekte in Active Directory.  Sie werden verwendet, um die Beziehung zwischen einem Benutzer, einem Gerät und dem Unternehmen darzustellen.  Geräteobjekte verwenden ein von AD FS signiertes Zertifikat, um das physische Gerät am logischen Geräteobjekt in Active Directory zu verankern.  
  
Registrierte Geräte umfassen die folgenden Elemente:  
  
-   **Anzeige Name**  
  
    Anzeigename des Geräts.  Bei Windows-Geräten ist dies der Hostname des Computers.  
  
-   **Geräte-ID**  
  
    Eine GUID, die vom Geräteregistrierungsserver generiert wird.  
  
-   **Zertifikat Fingerabdruck**  
  
    Der Zertifikatfingerabdruck des X.509-Zertifikats, das mit dem registrierten Gerät verwendet wird.  
  
-   **Betriebs Systemtyp**  
  
    Der Typ des Betriebssystems auf dem Gerät.  
  
-   **Betriebssystem Version**  
  
    Die Version des Betriebssystems auf dem Gerät.  
  
-   **Ist aktiviert**  
  
    Ein boolescher Wert, der angibt, ob das Gerät in Active Directory aktiviert ist.  Nur aktivierte Geräte können auf Dienste zugreifen.  
  
-   **Ungefähre Zeit der letzten Verwendung**  
  
    Der ungefähre Zeitpunkt, zu dem das Gerät zum letzten Mal für den Zugriff auf eine Ressource verwendet wurde.  Um den Replikationsdatenverkehr zu beschränken, wird dieser Wert nur alle 14 Tage aktualisiert.  
  
-   **Registrierter Besitzer**  
  
    Die Sicherheitsidentität \(sid @ no__t-1 des Benutzers, der dieses Gerät dem Arbeitsplatz hinzugefügt hat.  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS @ no__t-0drs Server SSL-Zertifikats Sperr Überprüfung  
Der Client für den Arbeitsplatzbeitritt überprüft die Gültigkeit des SSL-Zertifikats des AD FS-Servers.  Wenn das SSL-Zertifikat des AD FS Servers eine Zertifikat Sperr Liste \(crl @ no__t-1-Endpunkt enthält, muss der Client in der Lage sein, den Endpunkt zu erreichen, der zum Überprüfen des Zertifikats angegeben wurde.  
  
Wenn Sie eine Testumgebung und eine Test Zertifizierungsstelle \(ca @ no__t-1 verwenden, um Ihre Server-SSL-Zertifikate auszustellen, können Sie festlegen, dass der CRL-Endpunkt nicht in den von Ihrer Zertifizierungsstelle ausgestellten Server Zertifikaten enthalten sein soll.  Auf diese Weise kann der Client für den Arbeitsplatzbeitritt die CRL-Prüfung umgehen.  
  
> [!CAUTION]  
> Dies wird nicht für Produktionssysteme empfohlen.  
  

