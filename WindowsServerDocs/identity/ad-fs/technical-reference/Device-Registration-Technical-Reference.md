---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: Technische Referenz zur Geräteregistrierung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0956fc959a09a9d00a098203a83091553e917c62
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966772"
---
# <a name="device-registration-technical-reference"></a>Technische Referenz zur Geräteregistrierung
Der Geräte Registrierungsdienst \( DRS \) ist ein neuer Windows-Dienst, der in der Active Directory Verbunddienst-Rolle unter Windows Server 2012 R2 enthalten ist.  Der DRS muss auf allen Verbundservern der AD FS-Farm installiert und konfiguriert sein.  Informationen zum Bereitstellen des DRS finden Sie unter [Konfigurieren eines Verbundservers mit dem Geräteregistrierungsdienst](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486831(v=ws.11)).  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>Bei Registrierung eines Geräts erstellte Active Directory-Objekte  
Die folgenden Active Directory-Objekte werden als Teil des Geräteregistrierungsdiensts erstellt.  
  
### <a name="device-registration-configuration"></a>Geräteregistrierungskonfiguration  
Die Geräteregistrierungskonfiguration wird im Konfigurationsnamenskontext der Active Directory-Gesamtstruktur gespeichert. \(Beispiel: **CN- \= Geräte Registrierungs Konfiguration, CN- \= Dienste, <Konfigurations \- namens \- Kontext>** \) . Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung initialisiert wird.  
  
Die Geräteregistrierungskonfiguration umfasst die folgenden Elemente:  
  
-   **Schlüssel des Ausstellers**  
  
    Die öffentlichen und privaten Schlüssel, die zur Ausstellung des einem registrierten Gerät zugeordneten X.509-Zertifikats verwendet wurden.  Die privaten Schlüssel sind DKM (Distributed Key Management, verteilte Schlüsselverwaltung)-geschützt.  
  
-   **Konfiguration des Geräteregistrierungsdiensts**  
  
    Richtlinien, die im Zusammenhang mit dem Geräteregistrierungsdienst stehen.  
  
### <a name="registered-devices-container"></a>Container für registrierte Geräte  
Der Geräte-Objektcontainer wird unter einer der Domänen in der Active Directory-Gesamtstruktur erstellt.  Dieser Objektcontainer enthält alle Geräteobjekte für die Active Directory-Gesamtstruktur.  
  
Standardmäßig wird der Container in derselben Domäne wie AD FS erstellt.  \(Beispielsweise **>CN \= registereddevices, DC \=<Standard \- namens \- Kontext ** \) . Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung initialisiert wird.  
  
### <a name="registered-devices"></a>Registrierte Geräte  
Geräteobjekte sind neue Lightweight-Objekte in Active Directory.  Sie werden verwendet, um die Beziehung zwischen einem Benutzer, einem Gerät und dem Unternehmen darzustellen.  Geräteobjekte verwenden ein von AD FS signiertes Zertifikat, um das physische Gerät am logischen Geräteobjekt in Active Directory zu verankern.  
  
Registrierte Geräte umfassen die folgenden Elemente:  
  
-   **Anzeige Name**  
  
    Anzeigename des Geräts.  Bei Windows-Geräten ist dies der Hostname des Computers.  
  
-   **Geräte-ID**  
  
    Eine GUID, die vom Geräteregistrierungsserver generiert wird.  
  
-   **Zertifikatfingerabdruck**  
  
    Der Zertifikatfingerabdruck des X.509-Zertifikats, das mit dem registrierten Gerät verwendet wird.  
  
-   **Betriebs Systemtyp**  
  
    Der Typ des Betriebssystems auf dem Gerät.  
  
-   **Betriebssystemversion**  
  
    Die Version des Betriebssystems auf dem Gerät.  
  
-   **Ist aktiviert**  
  
    Ein boolescher Wert, der angibt, ob das Gerät in Active Directory aktiviert ist.  Nur aktivierte Geräte können auf Dienste zugreifen.  
  
-   **Ungefährer Zeitpunkt der letzten Verwendung**  
  
    Der ungefähre Zeitpunkt, zu dem das Gerät zum letzten Mal für den Zugriff auf eine Ressource verwendet wurde.  Um den Replikationsdatenverkehr zu beschränken, wird dieser Wert nur alle 14 Tage aktualisiert.  
  
-   **Registrierter Besitzer**  
  
    Die sicherheitsidentitäts- \( sid \) des Benutzers, der dieses Gerät mit dem Arbeitsplatz verknüpft hat.  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS \/ DRS-Server-SSL-Zertifikat Sperr Überprüfung  
Der Client für den Arbeitsplatzbeitritt überprüft die Gültigkeit des SSL-Zertifikats des AD FS-Servers.  Wenn das SSL-Zertifikat für den AD FS Server einen CRL-Endpunkt für die Zertifikat Sperr Liste enthält \( \) , muss der Client in der Lage sein, den zum Überprüfen des Zertifikats angegebenen Endpunkt zu erreichen.  
  
Wenn Sie eine Testumgebung und eine Zertifizierungsstellen-Zertifizierungsstelle \( \) zum Ausstellen Ihrer Server-SSL-Zertifikate verwenden, können Sie auswählen, dass der CRL-Endpunkt nicht in den von Ihrer Zertifizierungsstelle ausgestellten Server Zertifikaten enthalten sein soll.  Auf diese Weise kann der Client für den Arbeitsplatzbeitritt die CRL-Prüfung umgehen.  
  
> [!CAUTION]  
> Dies wird nicht für Produktionssysteme empfohlen.  
  
