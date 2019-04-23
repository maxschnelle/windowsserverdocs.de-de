---
title: rpcping
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7382aa0d-90fc-47c0-84b3-15f52dd656d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cfa1d08c81f8b26507a5cae5f688923a7b226e1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829991"
---
# <a name="rpcping"></a>rpcping

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Bestätigt die RPC-Verbindung zwischen dem Computer mit Microsoft Exchange Server und keines der unterstützten Microsoft Exchange-Client-Arbeitsstationen im Netzwerk. Dieses Dienstprogramm kann verwendet werden, zu überprüfen, ob die Microsoft Exchange Server-Dienste über den die Clientarbeitsstationen über das Netzwerk auf RPC-Anforderungen reagiert. 

## <a name="syntax"></a>Syntax
```
rpcping [/t <protseq>] [/s <server_addr>] [/e <endpoint>
        |/f <interface UUID>[,Majorver]] [/O <Interface Object UUID]
        [/i <#_iterations>] [/u <security_package_id>] [/a <authn_level>]
        [/N <server_princ_name>] [/I <auth_identity>] [/C <capabilities>]
        [/T <identity_tracking>] [/M <impersonation_type>]
        [/S <server_sid>] [/P <proxy_auth_identity>] [/F <RPCHTTP_flags>]
        [/H <RPC/HTTP_authn_schemes>] [/o <binding_options>]
        [/B <server_certificate_subject>] [/b] [/E] [/q] [/c]
        [/A <http_proxy_auth_identity>] [/U <HTTP_proxy_authn_schemes>]
        [/r <report_results_interval>] [/v <verbose_level>] [/d]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|/t \<protseq>|Gibt die Protokollsequenz verwenden. Kann eine der standardmäßigen RPC-Protokollsequenzen, z. B.: Ncacn_ip_tcp, Verwendung, oder Ncacn_http.<br /><br />Wenn nicht angegeben, ist die Standardeinstellung Ncacn_ip_tcp.|
|/s \<server_addr>|Gibt die Adresse des Servers an. Wenn nicht angegeben, wird der lokale Computer ein Pingsignal gesendet werden.|
|/ e \<Endpunkt >|Gibt den Endpunkt einen Ping. Wenn keine Angabe erfolgt, wird die endpunktzuordnung auf dem Zielcomputer ein Pingsignal gesendet werden.<br /><br />Diese Option ist mit der Benutzeroberfläche sich gegenseitig ausschließende (**/f**) Option.|
|/o \<binding_options>|Gibt die Bindungsoptionen für das RPC-Ping an.|
|/ f \<Schnittstelle UUID > [, Majorver]|Gibt die Schnittstelle einen Ping. Diese Option ist nicht zusammen mit der Option "Endpunkt". Die Schnittstelle wird als eine UUID angegeben.<br /><br />Wenn die *Majorver* nicht angegeben ist, wird die Version 1 der-Schnittstelle gesucht werden.<br /><br />Wenn die Schnittstelle angegeben wird, **Rpcping** fragt die endpunktzuordnung auf dem Zielcomputer, um den Endpunkt für die angegebene Schnittstelle abzurufen. Die endpunktzuordnung wird mit den Optionen, die in der Befehlszeile angegebene abgefragt werden.|
|/ O \<Objekt UUID >|Gibt die Objekt-UUID an, ob es sich bei die Schnittstelle registriert.|
|/i \<#_iterations>|Gibt die Anzahl der Aufrufe vornehmen. Der Standardwert ist 1. Diese Option ist hilfreich beim Messen Verbindungslatenz, wenn mehrere Iterationen angegeben werden.|
|/u \<security_package_id>|Gibt an, das Sicherheitspaket (Security Provider) RPC für den Aufruf verwendet wird. Das Sicherheitspaket wird als eine Zahl oder einen Namen identifiziert. Wenn eine Zahl verwendet wird, ist die gleiche Zahl wie in der RpcBindingSetAuthInfoEx-API. Die folgende Liste zeigt die Namen und Zahlen. Namen sind nicht in der Groß-/Kleinschreibung beachtet:<br /><br />– Negotiate / 9 oder eine der Nego, Snego oder aushandeln<br />-NTLM / 10 oder NTLM<br />-SChannel / 14 oder SChannel<br />-Kerberos / 16 oder Kerberos<br />-Kernelmodus / 20 oder den Kernel<br />    Wenn Sie diese Option angeben, müssen Sie die Authentifizierungsebene als none angeben. Es gibt keinen Standardwert für diese Option aus. Wenn sie nicht angegeben ist, wird RPC keine Sicherheit für das Senden des pingsignals verwendet.|
|/ a \<Authn_level >|Gibt die Authentifizierungsebene zu verwenden. Dabei sind folgende Werte möglich:<br /><br />-eine Verbindung herstellen<br />-Aufrufen<br />-   pkt<br />-Integrität<br />-Datenschutz<br /><br />Wenn diese Option angegeben wird, die Sicherheit Paket-ID (/ u) muss ebenfalls angegeben werden. Es gibt keinen Standardwert für diese Option aus.<br /><br />Wenn diese Option nicht angegeben ist, wird RPC keine Sicherheit für das Senden des pingsignals verwendet.|
|/N \<server_princ_name>|Gibt einen Serverprinzipalnamen an.<br /><br />Dieses Feld kann nur verwendet werden, wenn Authentifizierungspaket auf und Sicherheit ausgewählt werden.|
|/I \<auth_identity>|Ermöglicht Ihnen die Angabe der alternativen Identität eine Verbindung mit dem Server herstellen. Die Identität ist im Formularbenutzer, Domäne, das Kennwort. Wenn der Benutzername, Domäne, oder das Kennwort Sonderzeichen, die von der Shell interpretiert werden kann verfügen, wird schließen Sie die Identität in doppelte Anführungszeichen ein. Sie können angeben, **\*** anstelle des Kennworts und RPC-werden Sie aufgefordert, das Kennwort eingeben, ohne es auf dem Bildschirm ausgeben. Wenn dieses Feld nicht angegeben ist, wird die Identität des angemeldeten Benutzers verwendet.<br /><br />Dieses Feld kann nur verwendet werden, wenn Authentifizierungspaket auf und Sicherheit ausgewählt werden.|
|/C \<capabilities>|Gibt eine hexadezimale Bitmaske von Flags an. Dieses Feld kann nur verwendet werden, wenn Authentifizierungspaket auf und Sicherheit ausgewählt werden.|
|/T \<identity_tracking>|Gibt an, statisch oder dynamisch. Wenn nicht angegeben wird, dynamische ist die Standardeinstellung.<br /><br />Dieses Feld kann nur verwendet werden, wenn Authentifizierungspaket auf und Sicherheit ausgewählt werden.|
|/M \<impersonation_type>|Gibt an, anonym, zu identifizieren, multiserverlösung angenommen oder delegiert. Standardmäßig ist die Identität annehmen.<br /><br />Dieses Feld kann nur verwendet werden, wenn Authentifizierungspaket auf und Sicherheit ausgewählt werden.|
|/S \<server_sid>|Gibt die erwartete SID des Servers.<br /><br />Dieses Feld kann nur verwendet werden, wenn Authentifizierungspaket auf und Sicherheit ausgewählt werden.|
|/P \<proxy_auth_identity>|Gibt die Identität mit der RPC/HTTP-Proxy zu authentifizieren. Hat das gleiche Format wie bei der Option/i. Sie müssen angeben, Sicherheitspaket (/ u), Authentifizierungsebene (/ a), und die Authentifizierungsschemas (/ H) um diese Option verwenden.|
|/F \<RPCHTTP_flags>|Gibt die Flags für die Authentifizierung für RPC/HTTP-Front-End übergeben. Die Flags können angegeben werden, als Zahlen oder den Namen, die die aktuell erkannten Flags sind:<br /><br />– Verwenden Sie SSL / 1 oder Ssl oder Use_ssl<br />-Erste Authentifizierungsschema in Use / 2 oder erste oder Use_first<br /><br />Sie müssen angeben, Sicherheitspaket (/ u) und die Authentifizierungsebene (/ a) um diese Option verwenden.|
|/H \<RPC/HTTP_authn_schemes>|Gibt an, die Authentifizierungsschemas für RPC/HTTP-Front-End-Authentifizierung verwenden. Diese Option ist eine Liste von numerischen Werten oder Namen durch Komma getrennt. Beispiel: Basic, NTLM. Gültige Werte sind (die Namen sind keine Groß-/Kleinschreibung beachten):<br /><br />-Basic / 1 oder Basic<br />-NTLM / 2 oder NTLM<br />-Zertifikat / 65536 oder Zertifikat<br /><br />Sie müssen angeben, Sicherheitspaket (/ u) und die Authentifizierungsebene (/ a) um diese Option verwenden.|
|/B \<server_certificate_subject>|Gibt den Antragsteller des Zertifikats Server an. Sie müssen SSL für diese Option verwenden, funktioniert.<br /><br />Sie müssen angeben, Sicherheitspaket (/ u) und die Authentifizierungsebene (/ a) um diese Option verwenden.|
|/b|Ruft den Antragsteller des Zertifikats Server aus dem Zertifikat, das vom Server gesendet wird, und gibt sie an einen Bildschirm oder eine Protokolldatei. Nur gültig, wenn der Proxy echo die Option (/ E) und die verwenden SSL-Optionen angegeben werden.<br /><br />Sie müssen angeben, Sicherheitspaket (/ u) und die Authentifizierungsebene (/ a) um diese Option verwenden.|
|/R|Gibt den HTTP-Proxy an. Wenn *keine*, der RPC-Proxy verwendet wird. Der Wert *Standard* bedeutet, dass die Internet Explorer-Einstellungen auf Ihrem Clientcomputer verwendet. Jeder andere Wert wird als explizite HTTP-Proxys behandelt. Wenn Sie dieses Flag nicht angeben, der Standardwert wird davon ausgegangen, d. h., die IE-Einstellungen aktiviert sind. Dieses Flag ist nur gültig, wenn die **/e** (nur Echo)-Flag aktiviert ist.|
|/E|Schränkt der Ping-Befehl an den RPC/HTTP-Proxy. Der Ping-Befehl wird den Server nicht erreicht werden. Nützlich, wenn Sie versuchen, um herauszufinden, ob die RPC/HTTP-Proxy erreichbar ist. Um einen HTTP-Proxy anzugeben, verwenden Sie das Flag/r. Wenn ein HTTP-Proxy im/o-Flag angegeben ist, wird diese Option wird ignoriert.<br /><br />Sie müssen angeben, Sicherheitspaket (/ u) und die Authentifizierungsebene (/ a) um diese Option verwenden.|
|/q|Gibt den stillen Modus. Gibt keine aufforderungen ausgenommen hiervon sind Kennwörter aus. Geht davon aus *Y* als Antwort auf alle Abfragen. Verwenden Sie diese Option mit Vorsicht.|
|/c|Smartcard-Zertifikat verwenden. RpcPing fordert den Benutzer, einer Smartcard.|
|/A|Gibt die Identität mit der der HTTP-Proxy zu authentifizieren. Hat das gleiche Format wie bei der Option/i.<br /><br />Sie müssen angeben, dass Authentifizierungsschemas (/ U), Sicherheitspaket (/ u) und Authentifizierungsebene (/ a) um diese Option verwenden.|
|/U|Gibt an, die Authentifizierungsschemas, die für HTTP-Proxy-Authentifizierung verwendet. Diese Option ist eine Liste von numerischen Werten oder Namen durch Komma getrennt. Beispiel: Basic, NTLM. Gültige Werte sind (die Namen sind keine Groß-/Kleinschreibung beachten):<br /><br />-Basic / 1 oder Basic<br />-NTLM / 2 oder NTLM<br /><br />Sie müssen angeben, Sicherheitspaket (/ u) und die Authentifizierungsebene (/ a) um diese Option verwenden.|
|/r|Wenn mehrere Iterationen angegeben werden, kann diese Option veranlasst **Rpcping** zeigt aktuelle Statistiken zur Ausführung in regelmäßigen Abständen stattdessen nach dem letzten Aufruf. Das Berichtintervall wird in Sekunden angegeben. Standardwert ist 15.|
|/v|Teilt **Rpcping** wie verbose, um die Ausgabe zu machen. Standardwert ist 1. 2 und 3 Geben Sie weitere Ausgabe **Rpcping**.|
|/d|Startet RPC Netzwerk diagnostic-Benutzeroberfläche.|
|/p|Gibt an, um zur Eingabe von Anmeldeinformationen aufgefordert werden, wenn die Authentifizierung fehlschlägt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_Examples"></a>Beispiele für
Um herauszufinden, ob es sich bei Ihrem Exchange-Server, die Sie über RPC/HTTP-Verbindung zugegriffen werden kann, geben Sie Folgendes ein:
```
rpcping /t ncacn_http /s exchange_server /o RpcProxy=front_end_proxy /P "username,domain,*" /H Basic /u NTLM /a connect /F 3
```

## <a name="additional-references"></a>Weitere Verweise
-   [Befehlszeilensyntax](command-line-syntax-key.md)