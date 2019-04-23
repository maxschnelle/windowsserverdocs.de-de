---
title: Transport Layer Security (TLS)-registrierungseinstellungen
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 02/28/2019
ms.openlocfilehash: 0d618d465ee45245e98fbc6aa58b32b974be08e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880881"
---
# <a name="transport-layer-security-tls-registry-settings"></a>Transport Layer Security (TLS)-registrierungseinstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016, Windows 10

In diesem Referenzthema für IT-Spezialisten enthält unterstützte Einstellung Registrierungsinformationen für die Windows-Implementierung des Protokolls Transport Layer Security (TLS) und das Protokoll Secure Sockets Layer (SSL) über den Schannel Security Support Provider (SSP). Der Registrierungsunterschlüssel und-Einträge, die in der dieses Thema Hilfe, die Sie verwalten und Problembehandlung des Schannel-SSP behandelt insbesondere die Protokolle TLS und SSL. 

>[!Caution]
>Diese Informationen dienen als Referenz, die Sie nutzen, wenn Sie eine Problembehandlung durchführen oder prüfen, ob die erforderlichen Einstellungen vorhanden sind. Es wird empfohlen, die Registrierung nur dann direkt zu bearbeiten, wenn es keine andere Alternative gibt.
>Änderungen an der Registrierung werden weder vom Registrierungs-Editor noch vom Windows-Betriebssystem überprüft, bevor sie angewendet werden. Daher können falsche Werte gespeichert werden, was zu nicht behebbaren Fehlern im System führen kann. Anstatt die Registrierung direkt zu bearbeiten, verwenden Sie nach Möglichkeit Gruppenrichtlinien oder andere Windows-Tools wie die Microsoft Management Console (MMC) zum Ausführen von Aufgaben. Wenn Sie die Registrierung bearbeiten müssen, gehen Sie äußerst umsichtig vor. 

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist, dass alle vier unten aufgeführten Methoden für die Clientzertifikatzuordnung unterstützt werden.

Wenn eine Serveranwendung die Clientauthentifizierung anfordert, versucht Schannel automatisch das Zertifikat, das vom Clientcomputer bereitgestellt wird, einem Benutzerkonto zuzuordnen. Sie können Benutzer authentifizieren, die sich mit einem Clientzertifikat anmelden, indem Sie Zuordnungen erstellen, die die Zertifikatsinformationen einem Windows-Benutzerkonto zuordnen. Nachdem Sie eine Zertifikatzuordung erstellt und aktiviert haben, ordnet Ihre Serveranwendung immer dann, wenn ein Client ein Clientzertifikat vorlegt, diesen Benutzer dem entsprechenden Windows-Benutzerkonto zu.

In den meisten Fällen wird ein Zertifikat einem Benutzerkonto auf eine von zwei Arten zugeordnet: 

- Ein einzelnes Zertifikat wird einem einzelnen Benutzerkonto zugeordnet (1:1-Zuordnung).
- Mehrere Zertifikate werden einem Benutzerkonto zugeordnet (n:1-Zuordnung).

Der Schannel-Anbieter verwendet standardmäßig die folgenden vier Methoden für die Clientzertifikatzuordnung, die nach Priorität aufgeführt sind:

1. Kerberos-S4U-Clientzertifikatzuordnung (Service-for-User)
2. Zuordnung von Benutzerprinzipalnamen
3. 1:1-Zuordnung (auch bekannt als Antragsteller/Aussteller- Zuordnung)
4. n:1-Zuordnung

Zutreffende Versionen: Entsprechend der Angabe in der Liste **Betrifft** am Anfang dieses Themas

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>Ciphers

TLS/SSL-Verschlüsselungen sollte kontrolliert werden, indem Sie die Reihenfolge der Verschlüsselungssammlungen konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von TLS Reihenfolge der Verschlüsselungssammlungen](manage-tls.md#configuring-tls-cipher-suite-order).

Weitere Informationen zu standardmäßigen Cipher Suites Reihenfolge an, die vom Schannel SSP verwendet werden, finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 

##<a name="ciphersuites"></a>CipherSuites

Konfigurieren von TLS/SSL-Verschlüsselungssammlungen erledigt werden mithilfe von Gruppenrichtlinien, die Verwaltung mobiler Geräte oder PowerShell, finden Sie unter [Konfigurieren von TLS Reihenfolge der Verschlüsselungssammlungen](manage-tls.md#configuring-tls-cipher-suite-order) Details.

Weitere Informationen zu standardmäßigen Cipher Suites Reihenfolge an, die vom Schannel SSP verwendet werden, finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 


## <a name="clientcachetime"></a>ClientCacheTime

Dieser Eintrag steuert die Dauer in Millisekunden, die das Betriebssystem benötigt, um Einträge im clientseitigen Cache ablaufen zu lassen. Der Wert 0 deaktiviert das Zwischenspeichern sicherer Verbindungen. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. 

Wenn sich ein Client über den Schannel SSP erstmals mit einem Server verbindet, erfolgt ein vollständiger TLS/SSL-Handshake. Wenn dieser abgeschlossen ist, werden der geheime Hauptschlüssel, die Verschlüsselungssammlung und Zertifikate im Sitzungscache auf dem jeweiligen Client und Server gespeichert.

Ab Windows Server 2008 und Windows Vista ist die standardmäßige clientcachezeiten 10 Stunden.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Standardmäßige Clientcachezeiten

## <a name="enableocspstaplingforsni"></a>EnableOcspStaplingForSni

Online Certificate Status-Protokoll (OCSP)-Heften kann ein Webserver, z. B. IIS (Internetinformationsdienste), um den aktuellen Status der Zertifikatsperre ein Serverzertifikat bereitzustellen, beim Senden des Serverzertifikats auf einem Client während des TLS-Handshake. Diese Funktion verringert die Last auf OCSP-Servern, da der Webserver den aktuellen OCSP-Status des Serverzertifikats Zwischenspeichern und für mehrere Webclients gesendet werden kann. Ohne diese Funktion würde jeder WebClient versucht, den aktuellen OCSP-Status des Serverzertifikats vom OCSP-Server abgerufen werden. Dies würde zu eine hohe Last auf diesem Server OCSP-generieren. 

Zusätzlich zu IIS können Webdienste über http.sys ebenfalls von dieser Einstellung, einschließlich Active Directory-Verbunddienste (AD FS) und Web Application Proxy (WAP) profitieren. 

Standardmäßig ist die OCSP-Unterstützung für IIS-Websites aktiviert, die eine einfache, sichere (SSL/TLS)-Bindung. Diese Unterstützung ist jedoch nicht standardmäßig aktiviert, wenn der IIS-Website eine oder beide der folgenden Typen von Bindungen der sicheren (SSL/TLS) verwendet wird:
- Servernamensanzeige anfordern
- Zentralisierten Zertifikatspeicher verwenden

In diesem Fall nicht die Hello-Antwort des Servers beim TLS-Handshake den geheftet OCSP-Status wird standardmäßig enthalten. Dieses Verhalten verbessert die Leistung: Die Windows OCSP-Heften-Implementierung eine Skalierung auf Hunderte von Serverzertifikaten. Da SNI und CCS aktivieren IIS für die Skalierung Tausender von Websites, die potenziell Tausende von Serverzertifikaten enthalten, kann durch Festlegen dieses Verhalten standardmäßig aktiviert werden Leistungsprobleme verursachen.

Zutreffende Versionen: Alle Versionen ab Windows Server 2012 und Windows 8. 

Registrierungspfad: [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL]

Fügen Sie den folgenden Schlüssel hinzu:

"EnableOcspStaplingForSni"=dword:00000001

Um deaktivieren, legen den DWORD-Wert auf 0 fest:

"EnableOcspStaplingForSni"=dword:00000000

>[!NOTE] 
>Aktivieren dieses Registrierungsschlüssels hat eine potenzielle Auswirkungen auf die Leistung.

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

Dieser Eintrag steuert die FIPS-Einhaltung (Federal Information Processing Standard). Der Standardwert ist 0.

Zutreffende Versionen: Alle Versionen ab Windows Server 2012 und Windows 8. 

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\LSA

Windows Server FIPS-Verschlüsselungssammlungen: Finden Sie unter [unterstützte Verschlüsselungssammlungen und Protokolle im Schannel SSP](https://technet.microsoft.com/library/dn786419.aspx).

## <a name="hashes"></a>Hashes

TLS/SSL-Hashalgorithmen sollte kontrolliert werden, indem Sie die Reihenfolge der Verschlüsselungssammlungen konfigurieren. Finden Sie unter [Konfigurieren von TLS Reihenfolge der Verschlüsselungssammlungen](manage-tls.md#configuring-tls-cipher-suite-order) Details.

## <a name="issuercachesize"></a>IssuerCacheSize

Dieser Eintrag steuert die Größe des Ausstellercaches und wird mit der Ausstellerzuordnung verwendet. Der Schannel SSP versucht, alle Aussteller in der Zertifikatkette des Clients und nicht nur den direkten Aussteller des Clientzertifikats zuzuordnen. Wenn die Aussteller keinem Konto zugeordnet werden, was der Normalfall ist, kann der Server versuchen, denselben Ausstellernamen wiederholt (unzählige Male pro Sekunde) zuzuordnen. 

Um dies zu verhindern, hat der Server einen negativen Cache. Wenn also ein Ausstellernamen keinem Konto zugeordnet ist, wird er dem Cache hinzugefügt, woraufhin Schannel SSP nicht versucht, den Ausstellernamen erneut zuzuordnen, bis der Cacheeintrag abläuft. Dieser Registrierungseintrag gibt die Cachegröße an. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 100. 

Zutreffende Versionen: Alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

Dieser Eintrag steuert das Zeitlimit für den Cache in Millisekunden. Der Schannel SSP versucht, alle Aussteller in der Zertifikatkette des Clients und nicht nur den direkten Aussteller des Clientzertifikats zuzuordnen. Wenn die Aussteller keinem Konto zugeordnet werden, was der Normalfall ist, kann der Server versuchen, denselben Ausstellernamen wiederholt (unzählige Male pro Sekunde) zuzuordnen.

Um dies zu verhindern, hat der Server einen negativen Cache. Wenn also ein Ausstellernamen keinem Konto zugeordnet ist, wird er dem Cache hinzugefügt, woraufhin Schannel SSP nicht versucht, den Ausstellernamen erneut zuzuordnen, bis der Cacheeintrag abläuft. Dieser Cache wird aus Leistungsgründen eingerichtet, damit das System nicht laufend versucht, dieselben Aussteller zuzuordnen. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert beträgt 10 Minuten.

Zutreffende Versionen: Alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm - Client RSA-Schlüssel Größen

Dieser Eintrag steuert die Client-RSA-Schlüsselgrößen an. 

Verwendung von Schlüsselaustauschalgorithmen sollte kontrolliert werden, indem Sie die Reihenfolge der Verschlüsselungssammlungen konfigurieren.

Hinzugefügt in Windows 10, Version 1507 und Windows Server 2016.

Registrierungspfad: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

Erstellen Sie zum Angeben einer minimalen unterstützten Bereich von RSA für schlüsselbits Länge für den TLS-Client eine **ClientMinKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert ist, werden weniger als 1.024 Bit mindestens. 

Um eine maximal unterstützten Bereich von RSA-Schlüssel Bitlänge für den TLS-Client anzugeben, erstellen Sie eine **ClientMaxKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert, wird ein Maximum nicht erzwungen.

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm - Diffie-Hellman-Schlüsselgröße

Dieser Eintrag steuert die Diffie-Hellman-Schlüsselgrößen an. 

Verwendung von Schlüsselaustauschalgorithmen sollte kontrolliert werden, indem Sie die Reihenfolge der Verschlüsselungssammlungen konfigurieren.

Hinzugefügt in Windows 10, Version 1507 und Windows Server 2016.

Registrierungspfad: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman

Um eine minimale unterstützten Bereich von Diffie-Helman Bitlänge für den TLS-Client anzugeben, erstellen Sie eine **ClientMinKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert ist, werden weniger als 1.024 Bit mindestens. 
 
Um eine maximale unterstützten Bereich von Diffie-Helman Bitlänge für den TLS-Client anzugeben, erstellen Sie eine **ClientMaxKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert, wird ein Maximum nicht erzwungen. 
 
Um die Diffie-Helman schlüsselbits Länge für den Standard-TLS-Server anzugeben, erstellen eine **ServerMinKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert, wird die 2048 Bits standardmäßig verwendet. 

## <a name="maximumcachesize"></a>MaximumCacheSize

Dieser Eintrag steuert die maximale Anzahl von Elementen im Cache. Durch Festlegen von "MaximumCacheSize" auf 0 werden der serverseitige Sitzungscache deaktiviert und erneute Verbindungen verhindert. Das Erhöhen von "MaximumCacheSize" über die Standardwerte hinaus bewirkt, dass "Lsass.exe" zusätzlichen Arbeitsspeicher beansprucht. Jedes Element im Sitzungscache erfordert in der Regel 2 bis 4 KB Arbeitsspeicher. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 20.000 Elemente. 

Zutreffende Versionen: Alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>Messaging – fragment analysieren

________________________________________
Dieser Eintrag steuert die maximale Größe der fragmentierten TLS-Handshake-Nachrichten, die akzeptiert werden. Nachrichten, die größer als die zulässige Größe werden nicht akzeptiert, und der TLS-Handshake schlägt fehl. Diese Einträge sind nicht standardmäßig in der Registrierung vorhanden. 

Wenn Sie den Wert auf 0 x 0 festlegen, fragmentierte Nachrichten werden nicht verarbeitet, und führt dazu, dass die TLS-Handshake fehlschlägt. Dadurch wird TLS-Clients oder Server auf dem aktuellen Computer mit der TLS-RFCs nicht kompatibel. 

Die maximal zulässige Größe kann erhöht werden, bis zu 2 ^ 24-1 Byte. Ermöglicht einem Client oder Server, zum Lesen und speichern große Mengen nicht überprüfte Daten über das Netzwerk ist keine gute Idee und erfordert zusätzlichen Arbeitsspeicher für jede Sicherheitskontext. 

Hinzugefügt in Windows 7 und Windows Server 2008 R2.
Ein Update, das Internet Explorer in Windows XP, Windows Vista oder in Windows Server 2008 fragmentierte TLS/SSL-Handshake-Nachrichten analysieren zu können, ist verfügbar.

Registrierungspfad: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

Um anzugeben, maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die der TLS-Client akzeptiert wird, erstellen Sie eine **MessageLimitClient** Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert ist, wird der Standardwert 0 x 8000 Bytes sein. 

Um anzugeben, maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die die TLS-Server akzeptiert werden, wenn keine Clientauthentifizierung vorhanden ist, erstellen Sie eine **MessageLimitServer** Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert ist, wird der Standardwert 0 x 4000 Bytes sein. 

Um anzugeben, maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die die TLS-Server akzeptiert werden, wenn die Clientauthentifizierung vorhanden ist, erstellen Sie eine **MessageLimitServerClientAuth** Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert, auf die gewünschte Bitlänge. Wenn nicht konfiguriert ist, wird der Standardwert 0 x 8000 Bytes sein. 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

Dieser Eintrag steuert das Kennzeichen, das verwendet wird, wenn die Liste der vertrauenswürdigen Aussteller gesendet wird. Bei Servern, die für die Clientauthentifizierung Hunderten von Zertifizierungsstellen vertrauen, gibt es zu viele Aussteller, die der Server nicht alle an den Clientcomputer senden kann, wenn die Clientauthentifizierung angefordert wird. In diesem Fall kann dieser Registrierungsschlüssel festgelegt werden. Anstatt eine Teilliste zu senden, sendet der Schannel SSP keine Liste an den Client.

Wenn keine Liste vertrauenswürdiger Aussteller gesendet wird, kann dies Auswirkungen darauf haben, was der Client sendet, wenn von ihm ein Clientzertifikat angefordert wird. Wenn z. B. Internet Explorer eine Anforderung für die Clientauthentifizierung empfängt, zeigt der Browser nur Clientzertifikate an, die mit einer der Zertifizierungsstellen verkettet sind, die vom Server gesendet wird. Wenn der Server keine Liste gesendet hat, zeigt Internet Explorer alle Clientzertifikate, die auf dem Client installiert sind. 

Dieses Verhalten ist möglicherweise wünschenswert. Wenn z. B. PKI-Umgebungen übergreifende Zertifikate enthalten, haben die Client- und Serverzertifikate nicht die gleiche Stammzertifizierungsstelle. Aus diesem Grund kann Internet Explorer kein Zertifikat wählen, das mit einer der Zertifizierungsstellen des Servers verkettet ist. Indem Sie konfigurieren, dass der Server keine Liste der vertrauenswürdigen Aussteller sendet, sendet Internet Explorer alle seine Zertifikate.

Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden.

Standardverhalten für die Liste der vertrauenswürdigen Aussteller senden

| Windows-Version | Zeit |
|-----------------|------|
| Windows Server 2012 und Windows 8 und höher | FALSE |
| Windows Server 2008 R2 und Windows 7 und früher | TRUE |

Zutreffende Versionen: Alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>ServerCacheTime

Dieser Eintrag steuert die Dauer, die das Betriebssystem in Millisekunden benötigt, um Einträge im serverseitigen Cache ablaufen zu lassen. Durch Festlegen auf 0 werden der serverseitige Sitzungscache deaktiviert und erneute Verbindungen verhindert. Das Erhöhen von "ServerCacheTime" über die Standardwerte bewirkt, dass "Lsass.exe" zusätzlichen Arbeitsspeicher beansprucht. Jedes Element im Sitzungscache erfordert in der Regel 2 bis 4 KB Arbeitsspeicher. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. 

Zutreffende Versionen: Alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Standardzeit im Servercache: 10 Stunden

## <a name="ssl-20"></a>SSL 2.0

Dieser Unterschlüssel steuert die Verwendung von SSL 2.0.

Ab Windows 10, Version 1607 und Windows Server 2016, SSL 2.0 wurde entfernt und wird nicht mehr unterstützt.
Eine SSL 2.0-Standardeinstellungen, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das SSL 2.0-Protokoll zu aktivieren, erstellen eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln SSL 2.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von SSL 2.0 auf dem SSL-Client. |
| Server | Steuert die Verwendung von SSL 2.0 auf dem Server SSL. |

Um SSL 2.0 für den Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest. Wenn eine SSPI-app-Anforderungen zur Verwendung von SSL 2.0, zugelassen wird. 

Um SSL 2.0 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app überschreiben anfordert, SSL 2.0 verwenden, kann es ausgehandelt werden. 

Im folgenden Beispiel wird das SSL 2.0, die in der Registrierung deaktiviert:

![SSL 2.0 deaktiviert](images/ssl-2-registry-setting.png)


## <a name="ssl-30"></a>SSL 3.0

Dieser Unterschlüssel steuert die Verwendung von SSL 3.0.

Ab Windows 10, Version 1607 und Windows Server 2016 wird wurde SSL 3.0 standardmäßig deaktiviert wurde. Standardeinstellungen für SSL 3.0, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das SSL 3.0-Protokoll zu aktivieren, erstellen eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben.  
Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln SSL 3.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von SSL 3.0 auf dem SSL-Client. |
| Server | Steuert die Verwendung von SSL 3.0 auf dem Server SSL. |

Um SSL 3.0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.
Wenn eine SSPI-app-Anforderungen zur Verwendung von SSL 3.0, zugelassen wird. 

Um SSL 3.0 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app, die explizit von SSL 3.0 angefordert wird, kann es ausgehandelt werden. 

Im folgenden Beispiel wird SSL 3.0, die in der Registrierung deaktiviert werden kann:

![SSL 3.0 deaktiviert](images/ssl-3-registry-setting.png)

## <a name="tls-10"></a>TLS 1.0

Dieser Unterschlüssel steuert die Verwendung von TLS 1.0.

TLS 1.0-Standard-Einstellungen finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das TLS 1.0-Protokoll zu aktivieren, erstellen eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln TLS 1.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1.0 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1.0 auf dem TLS-Server. |

Um TLS 1.0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.
Wenn eine SSPI-app-Anforderungen zur Verwendung von TLS 1.0, zugelassen wird. 

Um TLS 1.0 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app explizit anfordert, TLS 1.0 verwenden, kann es ausgehandelt werden. 

Im folgenden Beispiel wird die TLS 1.0 in der Registrierung deaktiviert:

![TLS 1.0 deaktiviert](images/tls-registry-setting.png)

## <a name="tls-11"></a>TLS 1.1

Dieser Unterschlüssel steuert die Verwendung von TLS 1.1.

Standardeinstellungen für TLS 1.1, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das TLS 1.1-Protokoll zu aktivieren, erstellen eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln TLS 1.1

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1.1 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1.1 auf dem TLS-Server. |

Um TLS 1.1 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.
Wenn eine SSPI-app-Anforderungen zur Verwendung von TLS 1.1, zugelassen wird. 

Um TLS 1.1 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app, die explizit zur Verwendung von TLS 1.1 angefordert wird, kann es ausgehandelt werden. 

Das folgende Beispiel zeigt, TLS 1.1 deaktiviert, in der Registrierung:

![TLS 1.1 deaktiviert](images/tls-11-registry-setting.png)

## <a name="tls-12"></a>TLS 1.2

Dieser Unterschlüssel steuert die Verwendung von TLS 1.2.

TLS 1.2-Standardeinstellungen, finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Erstellen Sie zum Aktivieren von TLS 1.2-Protokoll eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln TLS 1.2

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1.2 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1.2 auf dem TLS-Server. |

Um TLS 1.2 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.
Wenn eine SSPI-app anfordert, um die Verwendung von TLS 1.2, zugelassen wird. 

Um TLS 1.2 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app, die explizit auf die Verwendung von TLS 1.2 angefordert wird, kann es ausgehandelt werden. 

Im folgenden Beispiel wird die TLS 1.2 in der Registrierung deaktiviert:

![TLS 1.2 deaktiviert](images/tls-12-registry-setting.png)

## <a name="dtls-10"></a>DTLS 1.0

Dieser Unterschlüssel steuert die Verwendung von DTLS 1.0.

DTLS-1.0-Standard-Einstellungen finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das DTLS-1.0-Protokoll zu aktivieren, erstellen Sie eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln DTLS 1.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von DTLS 1.0 auf dem Client DTLS. |
| Server | Steuert die Verwendung von DTLS 1.0 auf dem DTLS-Server. |

Um DTLS 1.0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.
Wenn eine SSPI-app-Anforderungen von DTLS 1.0, zugelassen wird. 

Um DTLS 1.0 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app, die explizit von DTLS 1.0 angefordert wird, kann es ausgehandelt werden. 

Das folgende Beispiel zeigt die DTLS-1.0, die in der Registrierung deaktiviert:

![DTLS 1.0 deaktiviert](images/dtls-10-registry-setting.png)

## <a name="dtls-12"></a>DTLS 1.2

Dieser Unterschlüssel steuert die Verwendung von DTLS 1.2.

DTLS 1.2 Standardeinstellungen finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das DTLS-1.2-Protokoll zu aktivieren, erstellen eine **aktiviert** Eintrag in der Client oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. 

Tabelle mit den Unterschlüsseln DTLS 1.2

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von DTLS 1.2 auf dem Client DTLS. |
| Server | Steuert die Verwendung von DTLS 1.2 auf dem DTLS-Server. |


Um DTLS 1.2 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.
Wenn eine SSPI-app-Anforderungen von DTLS 1.0, zugelassen wird. 

Um DTLS 1.2 standardmäßig zu deaktivieren, erstellen eine **DisabledByDefault** Eintrag und ändern Sie den DWORD-Wert auf 1. Wenn eine SSPI-app, die explizit für die Verwendung DTLS 1.2 angefordert wird, kann es ausgehandelt werden. 

Das folgende Beispiel zeigt die DTLS-1.1, die in der Registrierung deaktiviert:

![DTLS 1.1 deaktiviert](images/dtls-11-registry-setting.png)


