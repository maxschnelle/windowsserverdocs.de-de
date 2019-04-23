---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: Technische Referenz zur Geräteregistrierung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fac6437e9b6c3893064769a8279c2cf96cbc47d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833781"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2

# <a name="device-registration-technical-reference"></a>Technische Referenz zur Geräteregistrierung
Der Device Registration Service \(DRS\) ist ein neuer Windows-Dienst, der mit der Active Directory-Verbunddienstrolle unter Windows Server 2012 R2 enthalten ist.  Der DRS muss auf allen Verbundservern der AD FS-Farm installiert und konfiguriert sein.  Informationen zum Bereitstellen des DRS finden Sie unter [Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst](https://technet.microsoft.com/library/dn486831.aspx).  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>Bei Registrierung eines Geräts erstellte Active Directory-Objekte  
Die folgenden Active Directory-Objekte werden als Teil des Geräteregistrierungsdiensts erstellt.  
  
### <a name="device-registration-configuration"></a>Geräteregistrierungskonfiguration  
Die Geräteregistrierungskonfiguration wird im Konfigurationsnamenskontext der Active Directory-Gesamtstruktur gespeichert. \(Z. B. **CN\=Device Registration Configuration, CN\=Services, < Konfiguration\-Benennung\-Kontext >**\). Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung initialisiert wird.  
  
Die Geräteregistrierungskonfiguration umfasst die folgenden Elemente:  
  
-   **Schlüssel des Ausstellers**  
  
    Die öffentlichen und privaten Schlüssel, die zur Ausstellung des einem registrierten Gerät zugeordneten X.509-Zertifikats verwendet wurden.  Die privaten Schlüssel sind DKM (Distributed Key Management, verteilte Schlüsselverwaltung)-geschützt.  
  
-   **Konfiguration des Geräteregistrierungsdiensts**  
  
    Richtlinien, die im Zusammenhang mit dem Geräteregistrierungsdienst stehen.  
  
### <a name="registered-devices-container"></a>Container für registrierte Geräte  
Der Geräte-Objektcontainer wird unter einer der Domänen in der Active Directory-Gesamtstruktur erstellt.  Dieser Objektcontainer enthält alle Geräteobjekte für die Active Directory-Gesamtstruktur.  
  
Standardmäßig wird der Container in derselben Domäne wie AD FS erstellt.  \(Z. B. **CN\=RegisteredDevices, DC\=< Standard\-Benennung\-Kontext >**\). Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung initialisiert wird.  
  
### <a name="registered-devices"></a>Registrierte Geräte  
Geräteobjekte sind neue Lightweight-Objekte in Active Directory.  Sie werden verwendet, um die Beziehung zwischen einem Benutzer, einem Gerät und dem Unternehmen darzustellen.  Geräteobjekte verwenden ein von AD FS signiertes Zertifikat, um das physische Gerät am logischen Geräteobjekt in Active Directory zu verankern.  
  
Registrierte Geräte umfassen die folgenden Elemente:  
  
-   **Anzeigename**  
  
    Anzeigename des Geräts.  Bei Windows-Geräten ist dies der Hostname des Computers.  
  
-   **Geräte-Id**  
  
    Eine GUID, die vom Geräteregistrierungsserver generiert wird.  
  
-   **Fingerabdruck des Zertifikats**  
  
    Der Zertifikatfingerabdruck des X.509-Zertifikats, das mit dem registrierten Gerät verwendet wird.  
  
-   **Betriebssystemtyp**  
  
    Der Typ des Betriebssystems auf dem Gerät.  
  
-   **Betriebssystemversion**  
  
    Die Version des Betriebssystems auf dem Gerät.  
  
-   **Aktiviert ist**  
  
    Ein boolescher Wert, der angibt, ob das Gerät in Active Directory aktiviert ist.  Nur aktivierte Geräte können auf Dienste zugreifen.  
  
-   **Ungefährer Zeitpunkt der letzten Verwendung**  
  
    Der ungefähre Zeitpunkt, zu dem das Gerät zum letzten Mal für den Zugriff auf eine Ressource verwendet wurde.  Um den Replikationsdatenverkehr zu beschränken, wird dieser Wert nur alle 14 Tage aktualisiert.  
  
-   **Registrierten Besitzer**  
  
    Die Sicherheits-ID \(SID\) des Benutzers, der dieses Gerät dem Arbeitsplatz hinzugefügt.  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS\/DRS-Server-SSL-Zertifikat-sperrüberprüfung  
Der Client für den Arbeitsplatzbeitritt überprüft die Gültigkeit des SSL-Zertifikats des AD FS-Servers.  Wenn das AD FS-Server SSL-Zertifikat eine Zertifikatsperrliste enthält \(CRL\) -Endpunkt, der Client muss die zum Überprüfen des Zertifikats angegebenen Endpunkt erreichen können.  
  
Wenn Sie eine testumgebung und eine Test-Zertifizierungsstelle verwenden \(Zertifizierungsstelle\) auf Ihrem Server SSL-Zertifikate ausstellt, können Sie wählen, um die CRL-Endpunkt nicht von der Zertifizierungsstelle ausgestellten Zertifikate enthalten.  Auf diese Weise kann der Client für den Arbeitsplatzbeitritt die CRL-Prüfung umgehen.  
  
> [!CAUTION]  
> Dies wird nicht für Produktionssysteme empfohlen.  
  

