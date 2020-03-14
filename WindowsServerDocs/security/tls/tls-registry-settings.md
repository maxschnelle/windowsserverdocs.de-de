---
title: Registrierungs Einstellungen für Transport Layer Security (TLS)
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 02/28/2019
ms.openlocfilehash: 60202e537093bd21515043ba56f70f3895c91d42
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322402"
---
# <a name="transport-layer-security-tls-registry-settings"></a>Registrierungs Einstellungen für Transport Layer Security (TLS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10

Dieses Referenz Thema für IT-Experten enthält unterstützte Registrierungs Einstellungs Informationen für die Windows-Implementierung des Transport Layer Security (TLS)-Protokolls und das Secure Sockets Layer (SSL)-Protokoll über die SChannel-Sicherheitsunterstützung. Anbieter (SSP). Die in diesem Thema behandelten Registrierungs Unterschlüssel und Einträge helfen Ihnen bei der Verwaltung und Problembehandlung des Schannel-SSP, insbesondere der TLS-und SSL-Protokolle. 

> [!CAUTION]
> Diese Informationen dienen als Referenz, die Sie nutzen, wenn Sie eine Problembehandlung durchführen oder prüfen, ob die erforderlichen Einstellungen vorhanden sind.
> Es wird empfohlen, die Registrierung nur dann direkt zu bearbeiten, wenn es keine andere Alternative gibt.
> Änderungen an der Registrierung werden weder vom Registrierungs-Editor noch vom Windows-Betriebssystem überprüft, bevor sie angewendet werden.
> Daher können falsche Werte gespeichert werden, was zu nicht behebbaren Fehlern im System führen kann.
> Anstatt die Registrierung direkt zu bearbeiten, verwenden Sie nach Möglichkeit Gruppenrichtlinien oder andere Windows-Tools wie die Microsoft Management Console (MMC) zum Ausführen von Aufgaben.
> Wenn Sie die Registrierung bearbeiten müssen, gehen Sie äußerst umsichtig vor.

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

Zutreffende Versionen: entsprechend der Angabe in der Liste **betrifft** am Anfang dieses Themas.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

## <a name="ciphers"></a>Ciphers

TLS/SSL-Chiffren sollten gesteuert werden, indem die Reihenfolge der Verschlüsselungs Sammlung konfiguriert wird. Weitere Informationen finden Sie unter [Konfigurieren der Reihenfolge der TLS](manage-tls.md#configuring-tls-cipher-suite-order)-Verschlüsselungs Sammlungen.

Weitere Informationen über die Reihenfolge der Standard Verschlüsselungs Sammlungen, die vom Schannel SSP verwendet werden, finden Sie unter Verschlüsselungs Sammlungen [in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 

## <a name="ciphersuites"></a>CipherSuites

Das Konfigurieren von TLS/SSL-Verschlüsselungs Sammlungen sollte mithilfe von Gruppenrichtlinien, MDM oder PowerShell erfolgen. Weitere Informationen finden Sie unter [Konfigurieren der Reihenfolge der TLS](manage-tls.md#configuring-tls-cipher-suite-order) -Verschlüsselungs Sammlungen.

Weitere Informationen über die Reihenfolge der Standard Verschlüsselungs Sammlungen, die vom Schannel SSP verwendet werden, finden Sie unter Verschlüsselungs Sammlungen [in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 


## <a name="clientcachetime"></a>ClientCacheTime

Dieser Eintrag steuert die Dauer in Millisekunden, die das Betriebssystem benötigt, um Einträge im clientseitigen Cache ablaufen zu lassen. Der Wert 0 deaktiviert das Zwischenspeichern sicherer Verbindungen. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. 

Wenn sich ein Client über den Schannel SSP erstmals mit einem Server verbindet, erfolgt ein vollständiger TLS/SSL-Handshake. Wenn dieser abgeschlossen ist, werden der geheime Hauptschlüssel, die Verschlüsselungssammlung und Zertifikate im Sitzungscache auf dem jeweiligen Client und Server gespeichert.

Ab Windows Server 2008 und Windows Vista beträgt die standardmäßige Client Cache Zeit 10 Stunden.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

Standardmäßige Clientcachezeiten

## <a name="enableocspstaplingforsni"></a>Enableocspstaplingforsni

Das Online Certificate Status-Protokoll (OCSP) ermöglicht einem Webserver, z. b. Internetinformationsdienste (IIS), den aktuellen Sperr Status eines Serverzertifikats bereitzustellen, wenn das Serverzertifikat während des TLS-Handshake an einen Client gesendet wird. Diese Funktion reduziert die Auslastung der OCSP-Server, da der Webserver den aktuellen OCSP-Status des Serverzertifikats Zwischenspeichern und an mehrere Webclients senden kann. Ohne diese Funktion würde jeder WebClient versuchen, den aktuellen OCSP-Status des Serverzertifikats vom OCSP-Server abzurufen. Dies würde eine hohe Auslastung auf diesem OCSP-Server generieren. 

Zusätzlich zu IIS können auch Webdienste über http. sys von dieser Einstellung profitieren, einschließlich Active Directory-Verbunddienste (AD FS) (AD FS) und webanwendungsproxy (WAP). 

Standardmäßig ist die OCSP-Unterstützung für IIS-Websites aktiviert, die über eine einfache sichere (SSL/TLS)-Bindung verfügen. Diese Unterstützung ist jedoch nicht standardmäßig aktiviert, wenn die IIS-Website einen oder beide der folgenden Typen von sicheren (SSL/TLS)-Bindungen verwendet:
- Servernamensanzeige anfordern
- Zentralisierten Zertifikatspeicher verwenden

In diesem Fall enthält die Server-Hello-Antwort während des TLS-Handshakes standardmäßig keinen OCSP-Status. Dieses Verhalten verbessert die Leistung: bei der Windows OCSP Heften-Implementierung werden hunderte von Server Zertifikaten skaliert. Da mit SNI und CCS IIS auf Tausende von Websites skaliert werden kann, die potenziell Tausende von Server Zertifikaten enthalten, kann das Festlegen dieses Verhaltensstandard mäßig zu Leistungsproblemen führen.

Anwendbare Versionen: alle Versionen ab Windows Server 2012 und Windows 8. 

Registrierungs Pfad: [HKEY_LOCAL_MACHINE \system\currentcontrolset\control\securityproviders\schannel]

Fügen Sie den folgenden Schlüssel hinzu:

"Enableocspstaplingforsni" = DWORD: 00000001

Legen Sie zum Deaktivieren von den DWORD-Wert auf 0 fest:

"Enableocspstaplingforsni" = DWORD: 00000000

> [!NOTE] 
> Die Aktivierung dieses Registrierungsschlüssels hat eine potenzielle Auswirkung auf die Leistung.

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

Dieser Eintrag steuert die FIPS-Einhaltung (Federal Information Processing Standard). Der Standard ist 0.

Anwendbare Versionen: alle Versionen ab Windows Server 2012 und Windows 8. 

Registrierungs Pfad: HKLM SYSTEM\CurrentControlSet\Control\Lsa

Windows Server FIPS-Verschlüsselungs Sammlungen: Weitere Informationen finden Sie [unter Unterstützte Verschlüsselungs Sammlungen und Protokolle im Schannel-SSP](https://technet.microsoft.com/library/dn786419.aspx).

## <a name="hashes"></a>Hashes

TLS/SSL-Hash Algorithmen sollten gesteuert werden, indem die Reihenfolge der Verschlüsselungs Sammlung konfiguriert wird. Weitere Informationen finden Sie unter [Konfigurieren der Reihenfolge der TLS](manage-tls.md#configuring-tls-cipher-suite-order) -Verschlüsselungs Sammlungen.

## <a name="issuercachesize"></a>IssuerCacheSize

Dieser Eintrag steuert die Größe des Ausstellercaches und wird mit der Ausstellerzuordnung verwendet. Der Schannel SSP versucht, alle Aussteller in der Zertifikat Kette des Clients zuzuordnen – nicht nur den direkten Aussteller des Client Zertifikats. Wenn die Aussteller keinem Konto zugeordnet werden, was der Normalfall ist, kann der Server versuchen, denselben Ausstellernamen wiederholt (unzählige Male pro Sekunde) zuzuordnen. 

Um dies zu verhindern, hat der Server einen negativen Cache. Wenn also ein Ausstellernamen keinem Konto zugeordnet ist, wird er dem Cache hinzugefügt, woraufhin Schannel SSP nicht versucht, den Ausstellernamen erneut zuzuordnen, bis der Cacheeintrag abläuft. Dieser Registrierungseintrag gibt die Cachegröße an. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 100. 

Anwendbare Versionen: alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

## <a name="issuercachetime"></a>IssuerCacheTime

Dieser Eintrag steuert das Zeitlimit für den Cache in Millisekunden. Der Schannel SSP versucht, alle Aussteller in der Zertifikat Kette des Clients zuzuordnen – nicht nur den direkten Aussteller des Client Zertifikats. Wenn die Aussteller keinem Konto zugeordnet werden, was der Normalfall ist, kann der Server versuchen, denselben Ausstellernamen wiederholt (unzählige Male pro Sekunde) zuzuordnen.

Um dies zu verhindern, hat der Server einen negativen Cache. Wenn also ein Ausstellernamen keinem Konto zugeordnet ist, wird er dem Cache hinzugefügt, woraufhin Schannel SSP nicht versucht, den Ausstellernamen erneut zuzuordnen, bis der Cacheeintrag abläuft. Dieser Cache wird aus Leistungsgründen eingerichtet, damit das System nicht laufend versucht, dieselben Aussteller zuzuordnen. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert beträgt 10 Minuten.

Anwendbare Versionen: alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>Keyexchangealgorithmus-Client-RSA-Schlüsselgrößen

Dieser Eintrag steuert die Größe des RSA-Schlüssels für den Client. 

Die Verwendung von Schlüsselaustausch Algorithmen sollte gesteuert werden, indem die Reihenfolge der Verschlüsselungs Sammlung konfiguriert wird.

In Windows 10, Version 1507 und Windows Server 2016 hinzugefügt.

Registrierungs Pfad: hklm\system\currentcontrolset\control\securityproviders\schannel\keyexchangealgorithms\pkcs

Um einen minimal unterstützten Bereich der RSA-Schlüssel Bit Länge für den TLS-Client anzugeben, erstellen Sie einen **clientminkeybitlength** -Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn keine Konfiguration erfolgt, sind 1024 Bits das minimale. 

Um einen maximalen unterstützten Bereich der RSA-Schlüssel Bit Länge für den TLS-Client anzugeben, erstellen Sie einen **clientmaxkeybitlength** -Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn diese nicht konfiguriert ist, wird ein Maximum nicht erzwungen.

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>Keyexchangealgorithmus-Diffie-Hellman-Schlüsselgrößen

Dieser Eintrag steuert die Diffie-Hellman-Schlüsselgrößen. 

Die Verwendung von Schlüsselaustausch Algorithmen sollte gesteuert werden, indem die Reihenfolge der Verschlüsselungs Sammlung konfiguriert wird.

In Windows 10, Version 1507 und Windows Server 2016 hinzugefügt.

Registrierungs Pfad: hklm\system\currentcontrolset\control\securityproviders\schannel\keyexchangealgorithms\diffie-Hellman

Um einen minimal unterstützten Bereich von Diffie-Helman Key Bit length für den TLS-Client anzugeben, erstellen Sie einen **clientminkeybitlength** -Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn keine Konfiguration erfolgt, sind 1024 Bits das minimale. 
 
Wenn Sie einen maximal unterstützten Bereich von Diffie-Helman Key Bit length für den TLS-Client angeben möchten, erstellen Sie einen **clientmaxkeybitlength** -Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn diese nicht konfiguriert ist, wird ein Maximum nicht erzwungen. 
 
Erstellen Sie einen **serverminkeybitlength** -Eintrag, um die Diffie-Helman-Schlüssel Bit Länge für den TLS-Server Standard anzugeben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn diese Einstellung nicht konfiguriert ist, werden 2048 Bits als Standard verwendet. 

## <a name="maximumcachesize"></a>MaximumCacheSize

Dieser Eintrag steuert die maximale Anzahl von Elementen im Cache. Durch Festlegen von "MaximumCacheSize" auf 0 werden der serverseitige Sitzungscache deaktiviert und erneute Verbindungen verhindert. Das Erhöhen von "MaximumCacheSize" über die Standardwerte hinaus bewirkt, dass "Lsass.exe" zusätzlichen Arbeitsspeicher beansprucht. Jedes Session-Cache-Element benötigt in der Regel 2 bis 4 KB Arbeitsspeicher. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 20.000 Elemente. 

Anwendbare Versionen: alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

## <a name="messaging--fragment-parsing"></a>Messaging – fragmentverarbeitung

________________________________________
Dieser Eintrag steuert die maximal zulässige Größe von fragmentierten TLS-Handshake-Nachrichten, die akzeptiert werden. Nachrichten, die größer als die zulässige Größe sind, werden nicht akzeptiert, und der TLS-Handshake schlägt fehl. Diese Einträge sind nicht standardmäßig in der Registrierung vorhanden. 

Wenn Sie den Wert auf 0x0 festlegen, werden fragmentierte Nachrichten nicht verarbeitet und bewirken, dass der TLS-Handshake fehlschlägt. Dadurch werden TLS-Clients oder-Server auf dem aktuellen Computer nicht mit den TLS-RFCs kompatibel. 

Die maximal zulässige Größe kann bis zu 2 ^ 24-1 Byte betragen. Es ist keine gute Idee, einem Client oder Server das Lesen und Speichern großer Mengen nicht überprüfter Daten aus dem Netzwerk zu ermöglichen, und es wird zusätzlicher Arbeitsspeicher für jeden Sicherheitskontext beansprucht. 

Hinzugefügt in Windows 7 und Windows Server 2008 R2.
Ein Update, mit dem Internet Explorer in Windows XP, Windows Vista oder Windows Server 2008 zur Analyse fragmentierter TLS/SSL-Hand Shake Nachrichten verwendet werden kann.

Registrierungs Pfad: hklm\system\currentcontrolset\control\securityproviders\schannel\messaging

Erstellen Sie einen **messagelimitclient** -Eintrag, um eine maximal zulässige Größe von fragmentierten TLS-Hand Shake Nachrichten anzugeben, die vom TLS-Client akzeptiert werden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn keine Konfiguration erfolgt, ist der Standardwert 0X8000 bytes. 

Erstellen Sie einen **messagelimitserver** -Eintrag, um eine maximal zulässige Größe von fragmentierten TLS-Hand Shake Nachrichten anzugeben, die vom TLS-Server akzeptiert werden, wenn keine Client Authentifizierung vorhanden ist. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn diese Einstellung nicht konfiguriert ist, wird der Standardwert 0x4000 Bytes betragen. 

Zum Angeben einer maximal zulässigen Größe von fragmentierten TLS-Handshake-Nachrichten, die der TLS-Server bei der Client Authentifizierung akzeptieren wird, erstellen Sie einen **messagelimitserverclientauth** -Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn keine Konfiguration erfolgt, ist der Standardwert 0X8000 bytes. 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

Dieser Eintrag steuert das Kennzeichen, das verwendet wird, wenn die Liste der vertrauenswürdigen Aussteller gesendet wird. Bei Servern, die für die Clientauthentifizierung Hunderten von Zertifizierungsstellen vertrauen, gibt es zu viele Aussteller, die der Server nicht alle an den Clientcomputer senden kann, wenn die Clientauthentifizierung angefordert wird. In diesem Fall kann dieser Registrierungsschlüssel festgelegt werden. Anstatt eine Teilliste zu senden, sendet der Schannel SSP keine Liste an den Client.

Wenn keine Liste vertrauenswürdiger Aussteller gesendet wird, kann dies Auswirkungen darauf haben, was der Client sendet, wenn von ihm ein Clientzertifikat angefordert wird. Wenn z. B. Internet Explorer eine Anforderung für die Clientauthentifizierung empfängt, zeigt der Browser nur Clientzertifikate an, die mit einer der Zertifizierungsstellen verkettet sind, die vom Server gesendet wird. Wenn der Server keine Liste gesendet hat, zeigt Internet Explorer alle Clientzertifikate, die auf dem Client installiert sind. 

Dieses Verhalten ist möglicherweise wünschenswert. Wenn z. b. PKI-Umgebungen Übergreifende Zertifikate enthalten, haben die Client-und Server Zertifikate nicht die gleiche Stamm Zertifizierungsstelle. aus diesem Grund kann Internet Explorer kein Zertifikat auswählen, das mit einem der Server-CAS verknüpft ist. Indem Sie konfigurieren, dass der Server keine Liste der vertrauenswürdigen Aussteller sendet, sendet Internet Explorer alle seine Zertifikate.

Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden.

Standardverhalten der Liste vertrauenswürdiger Aussteller senden

| Windows-Version | Zeit |
|-----------------|------|
| Windows Server 2012 und Windows 8 und höher | FALSE |
| Windows Server 2008 R2 und Windows 7 und früher | TRUE |

Anwendbare Versionen: alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

## <a name="servercachetime"></a>ServerCacheTime

Dieser Eintrag steuert die Dauer, die das Betriebssystem in Millisekunden benötigt, um Einträge im serverseitigen Cache ablaufen zu lassen. Durch Festlegen auf 0 werden der serverseitige Sitzungscache deaktiviert und erneute Verbindungen verhindert. Das Erhöhen von "ServerCacheTime" über die Standardwerte bewirkt, dass "Lsass.exe" zusätzlichen Arbeitsspeicher beansprucht. Jedes Sitzungs Cache Element benötigt in der Regel 2 bis 4 KB Arbeitsspeicher. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. 

Anwendbare Versionen: alle Versionen ab Windows Server 2008 und Windows Vista.

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel

Standard Server Cache-Zeit: 10 Stunden

## <a name="ssl-20"></a>SSL 2.0

Dieser Unterschlüssel steuert die Verwendung von SSL 2,0.

Ab Windows 10, Version 1607 und Windows Server 2016, wurde SSL 2,0 entfernt und wird nicht mehr unterstützt.
Die Standardeinstellungen für SSL 2,0 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das SSL 2,0-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

SSL 2,0-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von SSL 2,0 auf dem SSL-Client. |
| Server | Steuert die Verwendung von SSL 2,0 auf dem SSL-Server. |

Um SSL 2,0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0. Wenn eine SSPI-APP die Verwendung von SSL 2,0 anfordert, wird Sie verweigert. 

Um SSL 2,0 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App für die Verwendung von SSL 2,0-Anforderungen aufgefordert wird, kann Sie ausgehandelt werden. 

Das folgende Beispiel zeigt SSL 2,0, das in der Registrierung deaktiviert ist:

![SSL 2,0 deaktiviert](images/ssl-2-registry-setting.png)


## <a name="ssl-30"></a>SSL 3.0

Dieser Unterschlüssel steuert die Verwendung von SSL 3,0.

Ab Windows 10, Version 1607 und Windows Server 2016, wurde SSL 3,0 standardmäßig deaktiviert. Die Standardeinstellungen für SSL 3,0 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das SSL 3,0-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben.  
Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

SSL 3,0-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von SSL 3,0 auf dem SSL-Client. |
| Server | Steuert die Verwendung von SSL 3,0 auf dem SSL-Server. |

Um SSL 3,0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0.
Wenn eine SSPI-APP die Verwendung von SSL 3,0 anfordert, wird Sie verweigert. 

Um SSL 3,0 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App explizit die Verwendung von SSL 3,0 anfordert, wird Sie möglicherweise ausgehandelt. 

Das folgende Beispiel zeigt SSL 3,0, das in der Registrierung deaktiviert ist:

![SSL 3,0 deaktiviert](images/ssl-3-registry-setting.png)

## <a name="tls-10"></a>TLS 1.0

Dieser Unterschlüssel steuert die Verwendung von TLS 1,0.

Die Standardeinstellungen für TLS 1,0 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das TLS 1,0-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

TLS 1,0-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1,0 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1,0 auf dem TLS-Server. |

Um TLS 1,0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0.
Wenn eine SSPI-APP die Verwendung von TLS 1,0 anfordert, wird Sie verweigert. 

Um TLS 1,0 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App explizit die Verwendung von TLS 1,0 anfordert, wird Sie möglicherweise ausgehandelt. 

Im folgenden Beispiel wird das in der Registrierung deaktivierte TLS 1,0 angezeigt:

![TLS 1,0 deaktiviert](images/tls-registry-setting.png)

## <a name="tls-11"></a>TLS 1.1

Dieser Unterschlüssel steuert die Verwendung von TLS 1,1.

Die Standardeinstellungen für TLS 1,1 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das TLS 1,1-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

TLS 1,1-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1,1 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1,1 auf dem TLS-Server. |

Um TLS 1,1 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0.
Wenn eine SSPI-APP die Verwendung von TLS 1,1 anfordert, wird Sie verweigert. 

Um TLS 1,1 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App explizit die Verwendung von TLS 1,1 anfordert, wird Sie möglicherweise ausgehandelt. 

Im folgenden Beispiel wird das in der Registrierung deaktivierte TLS 1,1 angezeigt:

![TLS 1,1 deaktiviert](images/tls-11-registry-setting.png)

## <a name="tls-12"></a>TLS 1.2

Dieser Unterschlüssel steuert die Verwendung von TLS 1,2.

Die Standardeinstellungen für TLS 1,2 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das TLS 1,2-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

TLS 1,2-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1,2 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1,2 auf dem TLS-Server. |

Um TLS 1,2 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0.
Wenn eine SSPI-APP die Verwendung von TLS 1,2 anfordert, wird Sie verweigert. 

Um TLS 1,2 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App explizit die Verwendung von TLS 1,2 anfordert, wird Sie möglicherweise ausgehandelt. 

Im folgenden Beispiel wird das in der Registrierung deaktivierte TLS 1,2 angezeigt:

![TLS 1,2 deaktiviert](images/tls-12-registry-setting.png)

## <a name="dtls-10"></a>DTLS 1.0

Dieser Unterschlüssel steuert die Verwendung von DTLS 1,0.

Die Standardeinstellungen für DTLS 1,0 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das DTLS 1,0-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

DTLS 1,0-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von DTLS 1,0 auf dem DTLS-Client. |
| Server | Steuert die Verwendung von DTLS 1,0 auf dem DTLS-Server. |

Um DTLS 1,0 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0.
Wenn eine SSPI-APP die Verwendung von DTLS 1,0 anfordert, wird Sie verweigert. 

Um DTLS 1,0 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App explizit die Verwendung von DTLS 1,0 anfordert, wird Sie möglicherweise ausgehandelt. 

Im folgenden Beispiel wird die in der Registrierung deaktivierte DTLS 1,0 angezeigt:

![DTLS 1,0 deaktiviert](images/dtls-10-registry-setting.png)

## <a name="dtls-12"></a>DTLS 1,2

Dieser Unterschlüssel steuert die Verwendung von DTLS 1,2.

Die Standardeinstellungen für DTLS 1,2 finden Sie unter [Protokolle in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungs Pfad: HKLM system\currentcontrolset\control\securityproviders\schannel\protokolle

Um das DTLS 1,2-Protokoll zu aktivieren, erstellen Sie einen **aktivierten** Eintrag im Client-oder Server-Unterschlüssel, wie in der folgenden Tabelle beschrieben. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. 

DTLS 1,2-Unterschlüssel Tabelle

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von DTLS 1,2 auf dem DTLS-Client. |
| Server | Steuert die Verwendung von DTLS 1,2 auf dem DTLS-Server. |


Um DTLS 1,2 für Client oder Server zu deaktivieren, ändern Sie den DWORD-Wert in 0.
Wenn eine SSPI-APP die Verwendung von DTLS 1,0 anfordert, wird Sie verweigert. 

Um DTLS 1,2 standardmäßig zu deaktivieren, erstellen Sie einen **disabledbydefault** -Eintrag und ändern den DWORD-Wert in 1. Wenn eine SSPI-App explizit die Verwendung von DTLS 1,2 anfordert, wird Sie möglicherweise ausgehandelt. 

Im folgenden Beispiel wird die in der Registrierung deaktivierte DTLS 1,1 angezeigt:

![DTLS 1,1 deaktiviert](images/dtls-11-registry-setting.png)


