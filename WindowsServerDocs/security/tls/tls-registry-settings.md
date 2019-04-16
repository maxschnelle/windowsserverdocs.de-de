---
title: Transport Layer Security (TLS)-Registrierungseinstellungen
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
ms.date: 08/07/2017
ms.openlocfilehash: 8ccfacc367a5d32438bebf22798479a07f6cbdfc
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="transport-layer-security-tls-registry-settings"></a>Transport Layer Security (TLS)-Registrierungseinstellungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016, Windows Server2008 R2, Windows Server 2008, Windows10, Windows8.1, Windows8, Windows7, windowsvista

Dieses Referenzthema für IT-Experten enthält unterstützten Einstellung Registrierungsinformationen für die Windows-Implementierung des Protokolls Transport Layer Security (TLS) und das Protokoll Secure Sockets Layer (SSL) über den Schannel Security Support Provider (SSP). Die Registrierungsunterschlüssel und die Einträge, die in diesem Thema Hilfe, Verwaltung und Problembehandlung des Schannel-SSP, behandelt speziell die Protokolle TLS und SSL. 

>[!Caution]
>Diese Informationen werden bereitgestellt, als Referenz verwenden, wenn Sie eine Problembehandlung durchführen oder überprüfen, dass die erforderlichen Einstellungen angewendet werden. Es wird empfohlen, dass Sie nicht direkt die Registrierung bearbeiten, wenn keine andere Alternative vorhanden ist.
>Änderungen an der Registrierung werden durch den Registrierungs-Editor oder durch das Windows-Betriebssystem nicht überprüft, bevor sie angewendet werden. Daher können falsche Werte gespeichert werden, und dies kann dazu führen nicht behebbaren Fehlern im System. Anstatt das direkte Bearbeiten der Registrierungs verwenden Sie nach Möglichkeit Gruppenrichtlinien oder anderen Windows-Tools wie z.B. Microsoft Management Console (MMC) um Aufgaben auszuführen. Wenn Sie die Registrierung bearbeiten müssen, verwenden Sie äußerst vorsichtig vor. 

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist, dass alle vier unten aufgeführten Methoden, unterstützt werden.

Wenn eine Serveranwendung die Clientauthentifizierung erforderlich ist, versucht Schannel automatisch, das Zertifikat zuzuordnen, das vom Clientcomputer zu einem Benutzerkonto bereitgestellt werden. Sie können Benutzer authentifizieren, die sich mit einem Clientzertifikat anmelden, von Zuordnungen erstellen, die die Zertifikatsinformationen einem Windows-Benutzerkonto zu verknüpfen. Nach dem Erstellen und eine Zuordnung des Clientzertifikats aktivieren, ordnet Ihre Serveranwendung bei jedes Mal, wenn ein Client ein Clientzertifikat vorlegt automatisch diesen Benutzers mit dem entsprechenden Windows-Benutzerkonto.

In den meisten Fällen wird ein Zertifikat einem Benutzerkonto auf zwei Arten zugeordnet: 

- Ein einzelnes Zertifikat wird einem einzelnen Benutzerkonto (1: 1-Zuordnung) zugeordnet.
- Mehrere Zertifikate werden einem Benutzerkonto (n-1-Zuordnung) zugeordnet.

Standardmäßig verwendet der Schannel-Anbieter die folgenden vier Methoden, in der Reihenfolge ihrer Priorität aufgeführt:

1. Kerberos Service-for-User (S4U)-Clientzertifikatszuordnung
2. Zuordnung von Benutzerprinzipalnamen
3. 1: 1-Zuordnung (auch bekannt als Antragsteller/Aussteller-Zuordnung)
4. N-1-Zuordnung

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>Verschlüsselungen

TLS/SSL-Verschlüsselungen sollten durch Konfigurieren der Reihenfolge der Verschlüsselungssammlungen gesteuert werden. Weitere Informationen finden Sie unter [Konfigurieren von TLS Reihenfolge Verschlüsselungssammlungen](manage-tls.md#configuring-tls-cipher-suite-order).

Informationen zu Cipher Suites Standardreihenfolge, die vom Schannel SSP verwendet werden, finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 

##<a name="ciphersuites"></a>CipherSuites

Konfigurieren von TLS/SSL-Verschlüsselungssammlungen erfolgen mithilfe von Gruppenrichtlinien, MDM oder PowerShell finden Sie unter [Konfigurieren von TLS Reihenfolge Verschlüsselungssammlungen](manage-tls.md#configuring-tls-cipher-suite-order) für Details.

Informationen zu Cipher Suites Standardreihenfolge, die vom Schannel SSP verwendet werden, finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 


## <a name="clientcachetime"></a>ClientCacheTime

Dieser Eintrag steuert die Dauer, die das Betriebssystem in Millisekunden dauert, Einträge im clientseitigen Cache ablaufen. Der Wert 0 deaktiviert das Zwischenspeichern sicherer Verbindungen. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. 

Beim ersten ein Client eine zu einem Server über den Schannel-SSP, ein vollständiger Verbindung TLS/SSL-Handshake erfolgt. Wenn dies abgeschlossen ist, werden der geheime Hauptschlüssel, Verschlüsselungssammlung und Zertifikate im Sitzungscache auf dem jeweiligen Client und Server gespeichert.

Beginnend mit Windows Server2008 und Windows Vista ist die standardmäßige clientcachezeiten 10 Stunden.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Standardmäßige clientcachezeiten

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

Dieser Eintrag steuert (FIPS = Federal Information Processing)-Kompatibilität. Der Standardwert ist 0.

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas. 

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\LSA

Windows Server FIPS-Verschlüsselungssammlungen: finden Sie unter [unterstützten Verschlüsselungssammlungen und Protokolle im Schannel-SSP](https://technet.microsoft.com/library/dn786419.aspx).

## <a name="hashes"></a>Hashes

TLS/SSL-Hashalgorithmen sollten durch Konfigurieren der Reihenfolge der Verschlüsselungssammlungen gesteuert werden. Weitere Informationen finden Sie unter [Konfigurieren von TLS Reihenfolge Verschlüsselungssammlungen](manage-tls.md#configuring-tls-cipher-suite-order) für Detail.

## <a name="issuercachesize"></a>IssuerCacheSize

Dieser Eintrag steuert die Größe des ausstellercaches, und es wird mit der ausstellerzuordnung verwendet. Der Schannel SSP versucht, alle Aussteller in der Zertifikatkette des Clients zugeordnet – nicht nur den direkten Aussteller des Clientzertifikats. Wenn die Aussteller nicht auf ein Konto, was der Normalfall ist zugeordnet sind, der Server versuchen, denselben Ausstellernamen wiederholt, unzählige Male pro Sekunde. 

Um dies zu verhindern, verfügt der Server einen negativen Cache, wenn ein Ausstellernamen keinem Konto zugeordnet, er dem Cache hinzugefügt wird und der Schannel SSP nicht versucht, ordnen Sie den Namen des Ausstellers erst dann wieder der Cacheeintrag abläuft. Dieser Registrierungseintrag gibt die Cachegröße an. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 100. 

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

Dieser Eintrag steuert das Timeoutintervall Cache in Millisekunden. Der Schannel SSP versucht, alle Aussteller in der Zertifikatkette des Clients zugeordnet – nicht nur den direkten Aussteller des Clientzertifikats. In Fällen, in denen der Aussteller kein Konto, was der Normalfall ist zugeordnet, der Server versuchen, denselben Ausstellernamen wiederholt, unzählige Male pro Sekunde.

Um dies zu verhindern, verfügt der Server einen negativen Cache, wenn ein Ausstellernamen keinem Konto zugeordnet, er dem Cache hinzugefügt wird und der Schannel SSP nicht versucht, ordnen Sie den Namen des Ausstellers erst dann wieder der Cacheeintrag abläuft. Dieser Cache wird aus Leistungsgründen gespeichert, sodass das System nicht versucht laufend, dieselben Aussteller zuzuordnen. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 10Minuten.

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm – Client RSA-Schlüssel Größen

Dieser Eintrag steuert die Client-RSA-Schlüsselgrößen. 

Verwendung von Schlüsselaustauschalgorithmen sollten durch Konfigurieren der Reihenfolge der Verschlüsselungssammlungen gesteuert werden.

In Windows10, Version 1507 und Windows Server2016 hinzugefügt.

Registrierungspfad: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

Erstellen Sie zum Angeben einer minimalen unterstützten Bereich von RSA Bitlänge für den TLS-Client eine **ClientMinKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn nicht konfiguriert ist, werden 1024Bit der Minimalwert sein. 

Erstellen Sie zum Angeben einer Bitlänge maximal unterstützten Bereich von RSA für den TLS-Client eine **ClientMaxKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Nicht konfiguriert, wird eine maximale nicht erzwungen.

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm – Diffie-Hellman-Schlüsselgrößen

Dieser Eintrag steuert die Diffie-Hellman-Schlüsselgrößen. 

Verwendung von Schlüsselaustauschalgorithmen sollten durch Konfigurieren der Reihenfolge der Verschlüsselungssammlungen gesteuert werden.

In Windows10, Version 1507 und Windows Server2016 hinzugefügt.

Registrierungspfad: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman

Erstellen Sie zum Angeben einer minimalen unterstützten Bereich von Diffie-Helman Bitlänge für den TLS-Client eine **ClientMinKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn nicht konfiguriert ist, werden 1024Bit der Minimalwert sein. 
 
Erstellen Sie eine maximale unterstützten Bereich von Diffie-Helman Bitlänge der TLS-Client zum Angeben einer **ClientMaxKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Nicht konfiguriert, wird eine maximale nicht erzwungen. 
 
Erstellen Sie zum Angeben der Diffie-Helman Bitlänge für die TLS-Server standardmäßig eine **ServerMinKeyBitLength** Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Nicht konfiguriert, ist 2048Bit der Standardwert festgelegt. 

## <a name="maximumcachesize"></a>"Maximumcachesize"

Dieser Eintrag steuert die maximale Anzahl von Elementen im Cache. Festlegen von "maximumcachesize" auf 0 werden der serverseitige Sitzungscache deaktiviert und erneute Verbindungen verhindert. Das Erhöhen von "maximumcachesize" über die Standardwerte bewirkt, dass Lsass.exe zusätzlichen Arbeitsspeicher beansprucht. Jede Sitzung-Element im Sitzungscache belegt in der Regel 2 bis 4KB Arbeitsspeicher. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Der Standardwert ist 20.000 Elemente. 

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>Messaging-fragment-Analyse

________________________________________
Dieser Eintrag steuert die maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die akzeptiert werden. Nachrichten, die größer als die zulässige Größe jedoch nicht akzeptiert, und der TLS-Handshake schlägt fehl. Diese Einträge sind nicht standardmäßig in der Registrierung vorhanden. 

Wenn Sie den Wert auf 0 x 0 festlegen, werden fragmentierte Nachrichten werden nicht verarbeitet und bewirkt, dass den TLS-Handshake zu Fehlern bei. Dadurch TLS-Clients oder Server auf dem aktuellen Computer nicht kompatibel mit der TLS-RFCs. 

Die maximal zulässige Größe erhöht werden kann, bis zu 2 ^ 24-1 Byte. Ein Client oder Server zum Lesen und zum Speichern großer Datenmengen nicht verifizierten über das Netzwerk wird nicht empfohlen und zusätzlichen Arbeitsspeicher für jeden Sicherheitskontext wird verbraucht. 

Hinzugefügt in Windows7 und Windows Server2008 R2.
Ein Update, das ermöglicht Internet Explorer in Windows XP, Windows Vista oder Windows Server2008, fragmentierte TLS/SSL-Handshake-Nachrichten zu analysieren verfügbar ist.

Registrierungspfad: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

Erstellen Sie zum Angeben der maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die der TLS-Client akzeptiert ein **MessageLimitClient** Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn nicht konfiguriert ist, wird der Standardwert 0 x 8000 Bytes sein. 

Um anzugeben, maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die der TLS-Server akzeptiert werden, wenn keine Clientauthentifizierung vorliegt, Erstellen einer **MessageLimitServer** Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn nicht konfiguriert ist, wird der Standardwert 0 x 4000 Bytes sein. 

Um anzugeben, maximal zulässige Größe von fragmentierte TLS-Handshake-Nachrichten, die der TLS-Server akzeptiert werden, wenn die Clientauthentifizierung vorliegt, erstellen Sie eine **MessageLimitServerClientAuth** Eintrag. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in die gewünschte Bitlänge. Wenn nicht konfiguriert ist, wird der Standardwert 0 x 8000 Bytes sein. 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

Dieser Eintrag steuert die Kennzeichen, die verwendet wird, wenn die Liste der vertrauenswürdigen Aussteller gesendet wird. Bei Servern, die Hunderte von Zertifizierungsstellen für die Clientauthentifizierung vertrauen, sind zu viele Aussteller, für den Server senden können alle auf dem Clientcomputer beim Anfordern von Client-Authentifizierung. In diesem Fall kann dieser Registrierungsschlüssel festgelegt werden, und anstatt eine Teilliste Schannel-SSP werden keine Liste an den Client senden.

Nicht senden eine Liste vertrauenswürdiger Aussteller kann Auswirkungen auf, was der Client sendet, wenn es für ein Clientzertifikat angefordert wird. Angenommen, wenn Internet Explorer eine Anforderung für die Clientauthentifizierung empfängt, zeigt der Browser nur Clientzertifikate, die verkettet mit einer der Zertifizierungsstellen, die vom Server gesendet wird. Wenn der Server keine Liste gesendet hat, zeigt Internet Explorer alle Clientzertifikate, die auf dem Client installiert werden. 

Dieses Verhalten ist möglicherweise wünschenswert. Z.B. bei der PKI-Umgebungen übergreifende Zertifikate enthalten, ist die Client- und Serverzertifikate nicht die gleiche Stammzertifizierungsstelle. aus diesem Grund kann nicht Internet Explorer gewählt, ein Zertifikat, das mit einer der Zertifizierungsstellen des Servers verkettet ist. Konfigurieren Sie den Server, um die Liste der vertrauenswürdigen Aussteller nicht senden, sendet Internet Explorer alle seine Zertifikate.

Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden.

Standardverhalten für die Liste der vertrauenswürdigen Aussteller senden

| Windows-Version | Zeit |
|-----------------|------|
| Windows Server2012 und Windows8 oder höher | "FALSE" |
| Windows Server2008 R2 und Windows7 und frühere Versionen | "TRUE" |

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>"Servercachetime"

Dieser Eintrag steuert die Dauer in Millisekunden, die das Betriebssystem benötigt, um Einträge im serverseitigen Cache ablaufen. Der Wert 0 werden der serverseitige Sitzungscache deaktiviert und erneute Verbindungen verhindert. Das Erhöhen von "servercachetime" über die Standardwerte bewirkt, dass Lsass.exe zusätzlichen Arbeitsspeicher beansprucht. Jedes Element im Sitzungscache belegt in der Regel 2 bis 4KB Arbeitsspeicher. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. 

Zutreffende Versionen: entsprechend der Angabe in der **gilt für** Liste am Anfang dieses Themas.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Standardmäßig im Servercache: 10 Stunden

## <a name="ssl-20"></a>SSL 2.0

Dieser Unterschlüssel steuert die Verwendung von SSL 2.0.

Ab Windows10, Version 1607 und Windows Server2016, SSL 2.0 wurde entfernt und wird nicht mehr unterstützt.
Eine SSL 2.0-Standardeinstellungen finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das SSL 2.0-Protokoll zu aktivieren, erstellen Sie eine **aktiviert** im entsprechenden Unterschlüssel den Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. Um das Protokoll zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.

Tabelle mit den Unterschlüsseln SSL 2.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von SSL 2.0 auf dem SSL-Client. |
| Server | Steuert die Verwendung von SSL 2.0 auf dem SSL-Server. |
| DisabledByDefault | Kennzeichen Sie, um SSL 2.0 standardmäßig zu deaktivieren. |

## <a name="ssl-30"></a>SSL 3.0

Dieser Unterschlüssel steuert die Verwendung von SSL 3.0.

Ab Windows10, Version 1607 und Windows Server2016, wurde SSL 3.0 standardmäßig deaktiviert. Standardeinstellungen für SSL 3.0, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das SSL 3.0-Protokoll zu aktivieren, erstellen Sie einen Eintrag aktiviert im entsprechenden Unterschlüssel. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. Um das Protokoll zu deaktivieren, ändern Sie den DWORD-Wert auf 0 fest.

Tabelle mit den Unterschlüsseln SSL 3.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von SSL 3.0 auf dem SSL-Client. |
| Server | Steuert die Verwendung von SSL 3.0 auf dem SSL-Server. |
| DisabledByDefault | Kennzeichen Sie, um SSL 3.0 standardmäßig zu deaktivieren. |

## <a name="tls-10"></a>TLS 1.0

Dieser Unterschlüssel steuert die Verwendung von TLS 1.0.

Standardeinstellungen für TLS 1.0, finden Sie unter finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das TLS 1.0-Protokoll zu deaktivieren, Erstellen einer **aktiviert** im entsprechenden Unterschlüssel den Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 0 fest. Um das Protokoll zu aktivieren, ändern Sie den DWORD-Wert auf 1 fest.

Tabelle mit den Unterschlüsseln TLS 1.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1.0 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1.0 auf dem TLS-Server. |
| DisabledByDefault | Kennzeichen Sie, um TLS 1.0 standardmäßig zu deaktivieren. |

## <a name="tls-11"></a>TLS 1.1

Dieser Unterschlüssel steuert die Verwendung von TLS 1.1.

Standardeinstellungen für TLS 1.1, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

>[!Note] 
>Bei TLS 1.1 aktiviert und auf Servern mit Windows Server2008 R2 ausgehandelt werden, müssen Sie erstellen die **DisabledByDefault** Eintrag im entsprechenden Unterschlüssel (Client oder Server) und auf "0" festlegen. Der Eintrag in der Registrierung nicht sichtbar, und es ist standardmäßig auf "1" festgelegt.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das TLS 1.1-Protokoll zu deaktivieren, Erstellen einer **aktiviert** im entsprechenden Unterschlüssel den Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 0 fest. Um das Protokoll zu aktivieren, ändern Sie den DWORD-Wert auf 1 fest.

Tabelle mit den Unterschlüsseln TLS 1.1

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1.1 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1.1 auf dem TLS-Server. |
| DisabledByDefault | Kennzeichen Sie, um TLS 1.1 standardmäßig zu deaktivieren. |

## <a name="tls-12"></a>TLS 1.2

Dieser Unterschlüssel steuert die Verwendung von TLS 1.2.

Standardeinstellungen für TLS 1.2, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

>[!Note] 
>Bei TLS 1.2 aktiviert und auf Servern mit Windows Server2008 R2 ausgehandelt werden, müssen Sie erstellen die **DisabledByDefault** Eintrag im entsprechenden Unterschlüssel (Client oder Server) und auf "0" festlegen. Der Eintrag in der Registrierung nicht sichtbar, und es ist standardmäßig auf "1" festgelegt.

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das TLS 1.2-Protokoll zu deaktivieren, Erstellen einer **aktiviert** im entsprechenden Unterschlüssel den Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 0 fest. Um das Protokoll zu aktivieren, ändern Sie den DWORD-Wert auf 1 fest.

Tabelle mit den Unterschlüsseln TLS 1.2

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von TLS 1.2 auf dem TLS-Client. |
| Server | Steuert die Verwendung von TLS 1.2 auf dem TLS-Server. |
| DisabledByDefault | Kennzeichen Sie, um TLS 1.2 standardmäßig zu deaktivieren. |

## <a name="dtls-10"></a>DTLS 1.0

Dieser Unterschlüssel steuert die Verwendung von DTLS 1.0.

DTLS 1.0-Standardeinstellungen, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das DTLS 1.0-Protokoll zu deaktivieren, Erstellen einer **aktiviert** im entsprechenden Unterschlüssel den Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 0 fest. Um das Protokoll zu aktivieren, ändern Sie den DWORD-Wert auf 1 fest.

Tabelle mit den Unterschlüsseln DTLS 1.0

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von DTLS 1.0 auf dem Client DTLS. |
| Server | Steuert die Verwendung von DTLS 1.0 auf dem DTLS-Server. |
| DisabledByDefault | Kennzeichen Sie, um DTLS 1.0 standardmäßig zu deaktivieren. |

## <a name="dtls-12"></a>DTLS 1.2

Dieser Unterschlüssel steuert die Verwendung von DTLS 1.2.

DTLS-1.2-Standardeinstellungen, finden Sie unter [Protokolle TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Registrierungspfad: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Um das DTLS-1.2-Protokoll zu deaktivieren, Erstellen einer **aktiviert** im entsprechenden Unterschlüssel den Eintrag. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 0 fest. Um das Protokoll zu aktivieren, ändern Sie den DWORD-Wert auf 1 fest.

Tabelle mit den Unterschlüsseln DTLS 1.2

| Unterschlüssel | Beschreibung |
|--------|-------------|
| Client | Steuert die Verwendung von DTLS 1.2 auf dem Client DTLS. |
| Server | Steuert die Verwendung von DTLS 1.2 auf dem DTLS-Server. |
| DisabledByDefault | Kennzeichen Sie, um DTLS 1.2 standardmäßig zu deaktivieren. |

