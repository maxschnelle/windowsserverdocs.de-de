---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: "Technische Referenz zu Gerät Registrierung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fac6437e9b6c3893064769a8279c2cf96cbc47d6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server 2016, Windows Server2012 R2

# <a name="device-registration-technical-reference"></a>Technische Referenz zu Gerät Registrierung
Die \(DRS\) Device Registration Service ist ein neuer Windowsdienst, der mit der Active Directory-Verbunddienstrolle unter Windows Server2012 R2 enthalten ist.  Der DRS muss installiert und auf allen Verbundservern der AD FS-Farm konfiguriert werden.  Informationen zum Bereitstellen des DRS finden Sie unter [Konfigurieren eines Verbundservers mit Device Registration Service](https://technet.microsoft.com/library/dn486831.aspx).  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>Active Directory-Objekte erstellt, wenn ein Gerät registriert ist  
Die folgenden Active Directory-Objekte werden als Teil des Geräteregistrierungsdiensts erstellt.  
  
### <a name="device-registration-configuration"></a>Geräteregistrierungskonfiguration  
Die Geräteregistrierungskonfiguration wird im Konfigurationsnamenskontext der Active Directory-Gesamtstruktur gespeichert. \ (Z.B. **CN\ = Device Registration Configuration CN\ = Services, < Konfiguration\-Naming\-Kontext >**\). Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung Geräteregistrierung initialisiert wird.  
  
Die Geräteregistrierungskonfiguration umfasst die folgenden Elemente:  
  
-   **Aussteller Schlüssel**  
  
    Die öffentlichen und privaten Schlüssel verwendet, um die x. 509-Zertifikat auszustellen, das mit einem registrierten Gerät verknüpft ist.  Die privaten Schlüssel sind DKM geschützt.  
  
-   **Konfiguration des Geräteregistrierungsdiensts**  
  
    Richtlinien, die im Zusammenhang mit dem Device Registration Service.  
  
### <a name="registered-devices-container"></a>Container für registrierte Geräte  
Die Geräte-Objektcontainer wird unter einer der Domänen in der Active Directory-Gesamtstruktur erstellt.  Dieser Objektcontainer enthält alle Geräteobjekte für die Active Directory-Gesamtstruktur.  
  
Standardmäßig ist der Container in derselben Domäne wie AD FS erstellt.  \ (Z.B. **CN\ = RegisteredDevices, DC\ = < Default\-Naming\-Kontext >**\). Dieses Objekt wird erstellt, wenn die Active Directory-Gesamtstruktur für die Geräteregistrierung Geräteregistrierung initialisiert wird.  
  
### <a name="registered-devices"></a>Registrierte Geräte  
Geräteobjekte sind neue Lightweight-Objekte in Active Directory.  Sie werden verwendet, um die Beziehung zwischen darstellen: ein Benutzer ein Gerät und das Unternehmen.  Geräteobjekte verwenden ein AD FS signiertes Zertifikat, um das physische Gerät am logischen Geräteobjekt in Active Directory zu verankern.  
  
Registrierte Geräte umfassen die folgenden Elemente:  
  
-   **Anzeigename**  
  
    Anzeigename des Geräts.  Für Windows-Geräten ist dies der Hostname des Computers.  
  
-   **Geräte-ID**  
  
    Eine GUID, die vom Geräteregistrierungsserver generiert wird.  
  
-   **Fingerabdruck des Zertifikats**  
  
    Der Zertifikatfingerabdruck des x. 509-Zertifikats, das mit dem registrierten Gerät verwendet wird.  
  
-   **BS-Typ**  
  
    Die Art des Betriebssystems auf dem Gerät.  
  
-   **Version des Betriebssystems**  
  
    Die Version des Betriebssystems auf dem Gerät.  
  
-   **Aktiviert ist**  
  
    Ein boolescher Wert, der angibt, ob das Gerät in Active Directory aktiviert ist.  Nur aktivierte Geräte können auf Dienste zugreifen.  
  
-   **Ungefähre Zeitpunkt der letzten Verwendung**  
  
    Die ungefähre Zeit, die das Gerät verwendet wurde, auf eine Ressource zuzugreifen.  Um den Replikationsdatenverkehr zu beschränken, ist dies nur alle 14Tage aktualisiert.  
  
-   **Registrierte Besitzer**  
  
    Die \(SID\) Sicherheits-ID des Benutzers, der dieses Gerät dem Arbeitsplatz hinzugefügt hat.  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS\/DRS-Server SSL Zertifikatsperrüberprüfung  
Der Arbeitsplatzbeitritt überprüft der Gültigkeit des AD FS-Server SSL-Zertifikats.  Wenn das AD FS-Server SSL-Zertifikat einen Zertifikatsperrliste \(CRL\) Endpunkt enthält, muss der Client erreichen den Endpunkt angegeben, das Zertifikat überprüfen können.  
  
Wenn Sie eine Testumgebung und eine Test-Zertifizierungsstelle verwenden \(CA\) auf dem Server die SSL-Zertifikate ausstellt, können Sie wählen, um die CRL-Endpunkt nicht von der Zertifizierungsstelle ausgestellten Zertifikate enthalten.  Auf diese Weise kann den Client Arbeitsplatzbeitritt die CRL-Prüfung umgehen.  
  
> [!CAUTION]  
> Dies wird nicht für Produktionssysteme empfohlen.  
  

