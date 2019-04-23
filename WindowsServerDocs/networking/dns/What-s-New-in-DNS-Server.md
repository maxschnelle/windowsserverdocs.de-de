---
title: Neues in DNS-Server unter WindowsServer
description: Dieses Thema bietet einen Überblick über neue Funktionen in DNS-Server in Windows Server 2016 und höher
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: c9cecb94-3cd5-4da7-9a3e-084148b8226b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 665e411eda834a59c6dbe3581611b9b58bd006f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833571"
---
# <a name="whats-new-in-dns-server-in-windows-server"></a>Neues in DNS-Server unter WindowsServer

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt die Serverfunktionalität der Domain Name System (DNS)-, die neue oder geänderte in Windows Server 2016.  
  
In Windows Server 2016 bietet DNS-Server verbesserte Unterstützung in den folgenden Bereichen.  
  
|Funktionalität|Neu oder verbessert|Beschreibung|  
|-----------------|-------------------|---------------|  
|DNS-Richtlinien|Neu|Sie können konfigurieren, dass DNS-Richtlinien, um anzugeben, wie ein DNS-Server auf DNS-Abfragen reagiert. DNS-Antworten können basierend auf IP-Adresse für die Clients (Standort), der den Tag und einige andere Parameter. DNS-Richtlinien ermöglichen die Speicherort-fähigen DNS-Verwaltung des Datenverkehrs, Lastenausgleich, Split-Brain-DNS- und andere Szenarien.|  
|Antwort-Ratenlimit (RRL)|Neu|Sie können die Antwort die Begrenzung der Übertragungsrate für Ihre DNS-Server aktivieren. Auf diese Weise vermeiden Sie die Möglichkeit, böswillige Systeme, die mit Ihrer DNS-Server um einen DoS-Angriff auf einen DNS-Client zu initiieren.|  
|DNS-basierte Authentifizierung von benannten Entitäten (DANE)|Neu|Sie können TLSA (Transport Layer Security-Authentifizierung)-Datensätze verwenden, um Informationen für DNS-Clients bereitzustellen, die welche Zertifizierungsstelle Zustand sie ein Zertifikat für Ihren Domänennamen zu erwarten. Dies verhindert, dass Man-in-the-Middle-Angriffe, in denen ein Benutzer möglicherweise beschädigen den DNS-Cache auf ihrer eigenen Website verweisen, und geben Sie ein Zertifikat, das sie von einer anderen Zertifizierungsstelle ausgestellt.|  
|Unterstützung für unbekannte Datensatz|Neu|Sie können Datensätze hinzufügen, die nicht explizit vom Windows-DNS-Server mithilfe der Funktion unbekannt Datensatz unterstützt werden.|  
|Stammhinweise für IPv6|Neu|Sie können die systemeigene IPv6-Adresse verwenden, Stammhinweise zu unterstützen, um die Auflösung von Internetnamen verwenden die IPV6-Server ausführen.|  
|Windows PowerShell-Unterstützung|Verbessert|Neue Windows PowerShell-Cmdlets sind für DNS-Server verfügbar.|  
  
## <a name="dns-policies"></a>DNS-Richtlinien

DNS-Richtlinien können für GeoLocation-Verwaltung des Datenverkehrs, intelligente DNS-Antworten basierend auf der Tageszeit basierte, zu verwalten eines einzelnen DNS-Servers für die Teilung konfiguriert\-Brain-Bereitstellung, Anwenden von Filtern auf DNS-Abfragen und vieles mehr. Die folgenden Elemente enthalten, weitere Details zu diesen Funktionen wird.

-   **Anwendungslastenausgleich.** Wenn Sie mehrere Instanzen einer Anwendung an verschiedenen Standorten bereitgestellt haben, können Sie die DNS-Richtlinien verwenden, um den Datenverkehr einen Lastenausgleich zwischen den verschiedenen Anwendungsinstanzen, dynamischen Zuweisung von der Auslastung für die Anwendung.

-   **Geografische\-standortbasierte Verwaltung des Datenverkehrs.** DNS-Richtlinien können Sie primäre und sekundäre DNS-Server auf DNS-Clientabfragen basierend auf den geografischen Standort des dem Client und die Ressource, zu der der Client versucht, eine Verbindung herstellen, können den Client bereitstellen, mit der IP-Adresse am nächsten die Ressource. 

-   **Split-Brain-DNS.** Mit Teilung\--Brain-DNS, DNS-Einträge werden in verschiedenen Bereichen von Zone auf dem gleichen DNS-Server geteilt werden soll, und DNS-Clients erhalten eine Antwort basierend auf der gibt an, ob die Clients interne oder externe Kunden sind. Sie können konfigurieren, Split\--Brain-DNS für Active Directory-integrierte Zonen oder Zonen auf eigenständigen DNS-Servern.

-   **Filtern.** Sie können konfigurieren, dass DNS-Richtlinien zum Abfragefilter erstellen, die auf Kriterien basieren, die Sie angeben. Abfragefilter in DNS-Richtlinien können Sie konfigurieren die DNS-Server zum Antworten auf benutzerdefinierte Weise basierend auf dem DNS-Abfrage und die DNS-Client, der die DNS-Abfrage sendet. 
-   **Ermöglicht forensische Analysen.** Sie können DNS-Richtlinien verwenden, zum Umleiten von böswilligen DNS-Clients auf einem Nichtstandard\-vorhandene IP-Adresse anstelle der Weiterleitung an den Computer, die sie erreichen möchten.

-   **Zeit des Tages basierend Umleitung.** Sie können DNS-Richtlinien verwenden, Verteilen von Datenverkehr in verschiedenen geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf die Uhrzeit basieren. 
  
Sie können den DNS-Richtlinien auch verwenden, für die Active Directory-integrierten DNS-Zonen.

Weitere Informationen finden Sie unter den [DNS-Gruppenrichtlinienszenarien](deploy/DNS-Policies-Overview.md).

## <a name="response-rate-limiting"></a>Antwort Übertragungsbegrenzung zuverlässig verwaltet.

Sie können konfigurieren, dass RRL-Einstellungen, um zu steuern, wie Sie reagieren auf Anforderungen an einen DNS-Client, wenn der Server mehrere Anforderungen, die auf dem gleichen Client empfängt. Auf diese Weise können Sie eine Person verhindern einen Denial-of-Service (Dos)-Angriff über Ihre DNS-Server zu senden. Beispielsweise kann eine Bot-net Anforderungen an Ihre DNS-Server verwenden die IP-Adresse von einem dritten Computer als dem anforderer senden. Ohne RRL möglicherweise die DNS-Server auf alle Anforderungen, den dritten Computer Überflutung reagieren. Wenn Sie RRL verwenden, können Sie die folgenden Einstellungen konfigurieren:  
  
-   **Antworten pro Sekunde**. Dies ist die maximale Anzahl der Häufigkeit, mit die gleiche Antwort innerhalb einer Sekunde auf einem Client übergeben wird.  
  
-   **Fehler pro Sekunde**. Dies ist die maximale Anzahl der Häufigkeit, mit die eine Fehlerantwort mit dem gleichen Client innerhalb einer Sekunde gesendet wird.  
  
-   **Window**. Dies ist die Anzahl der Sekunden, die für die Antworten an einen Client angehalten werden, wenn zu viele Anforderungen gestellt werden.  
  
-   **Rate des Arbeitsspeicherverlusts**. Dies ist die Häufigkeit der DNS-Server auf eine Abfrage während des Zeitraums reagiert, die Antworten angehalten werden. Z. B. wenn der Server hält die Antworten an einen Client für 10 Sekunden und die Rate von Speicherverlusten 5 ist, reagiert der Server immer noch eine Abfrage für jede 5 Abfragen gesendet auf. Dies ermöglicht den legitimen Clients Antworten auch, wenn der DNS-Server Antwortquote beschränken, auf dem Subnetz oder den FQDN angewendet wird.  
  
-   **TC Rate**. Dies wird verwendet, weisen Sie den Client, eine Verbindung mit TCP, wenn Antworten an den Client angehalten werden. Z. B. wenn die TC-Rate 3 beträgt und der Server hält die Antworten auf einem Client, gibt der Server eine Anforderung für TCP-Verbindung für alle empfangenen 3 Abfragen. Stellen Sie sicher, dass der Wert für die TC-Rate niedriger als der Verlust, auf dem Client die Möglichkeit, die über TCP eine Verbindung herstellen, vor dem Verlust von Antworten zu geben.  
  
-   **Maximale Antworten**. Dies ist die maximale Anzahl von Antworten, die der Server an einen Client ausstellt, während Antworten angehalten werden.  
  
-   **Domänen der Positivliste**. Dies ist eine Liste der Domänen aus RRL Einstellungen ausgeschlossen werden sollen.  
  
-   **Whitelist Subnetze**. Dies ist eine Liste mit Subnetzen von RRL Einstellungen ausgenommen werden sollen.  
  
-   **Whitelist-Server-Netzwerkschnittstellen**. Dies ist eine Liste der DNS-Server-Netzwerkschnittstellen aus RRL Einstellungen ausgeschlossen werden sollen.  
  
## <a name="dane-support"></a>DANE-Unterstützung

Können Sie DANE Unterstützung \(RFC 6394 und 6698\) an für Ihre DNS-Clients welche Zertifizierungsstelle sie erwarten, dass Zertifikate für den Domänennamen aus ausgestellt werden gehostet in Ihrem DNS-Server. Dies verhindert, dass ein Man-in-the-Middle-Angriff, in denen ein Benutzer kann einen DNS-Cache beschädigt, und zeigen einen DNS-Namen in ihre eigenen IP-Adresse.  
  
Angenommen Sie, z. B. Host eine sichere Website, die mithilfe eines Zertifikats von einer bekannten Zertifizierungsstelle, die mit dem Namen CA1 SSL unter www.contoso.com zu verwendet. Ein Benutzer weiterhin möglicherweise um ein Zertifikat für www.contoso.com aus einer unterschiedlich, nicht damit-bekanntes, Autorität CA2 genannte Zertifikat zu erhalten. Klicken Sie dann möglicherweise die Entität, die die gefälschte www.contoso.com Website hosten können beschädigt werden DNS-Cache von einem Client oder Server, um www.contoto.com an den falschen Standort zu verweisen. Der Endbenutzer kann wird ein Zertifikat von CA2 angezeigt und einfach bestätigen es und eine Verbindung die gefälschte Website. Mit DANE wäre der Client kann eine Anforderung an dem DNS-Server für "contoso.com" in der der Datensatz TLSA und erfahren Sie, dass das Zertifikat für www.contoso.com Probleme nach CA1 war. Wenn Sie mit einem Zertifikat von einer anderen Zertifizierungsstelle angezeigt wird, wird die Verbindung abgebrochen.  
  
## <a name="unknown-record-support"></a>Unterstützung für unbekannte Datensatz

Ein Eintrag"Unbekannt" ist ein RR, deren RDATA-Format an den DNS-Server nicht bekannt ist. Die neu hinzugefügte Unterstützung für unbekannte Datensatztypen (RFC 3597) bedeutet, dass Sie den nicht unterstützten Record-Typen in der Windows DNS-Server-Zonen im Binärformat über das Netzwerk hinzufügen können. Die Windows cachekonfliktlöser hat bereits die Möglichkeit, unbekannte Record-Typen zu verarbeiten. Windows DNS-Server werden keine Datensätze spezifische Verarbeitung für die unbekannte Datensätze, aber senden in Antworten zurück, wenn Sie Abfragen empfangen werden.  
  
## <a name="ipv6-root-hints"></a>Stammhinweise für IPv6

Die IPV6-Stammhinweise, wurden veröffentlicht von IANA, für die Windows-DNS-Server hinzugefügt. Die Internet-Namensabfragen können jetzt die IPv6-Stammserver verwenden, für die Durchführung der namensauflösung.

## <a name="windows-powershell-support"></a>Windows PowerShell-Unterstützung

Die folgenden neuen Windows PowerShell-Cmdlets und Parameter werden in Windows Server 2016 eingeführt.
  
-   **Add-DnsServerRecursionScope**. Dieses Cmdlet erstellt einen neuen Bereich der Rekursion, auf dem DNS-Server. Rekursion Bereiche werden von DNS-Richtlinien zum Angeben einer Liste der Weiterleitungen, die in einer DNS-Abfrage verwendet werden.  
  
-   **Remove-DnsServerRecursionScope**. Dieses Cmdlet entfernt die vorhandenen Rekursion Bereiche.  
  
-   **Set-DnsServerRecursionScope**. Dieses Cmdlet ändert die Einstellungen eines vorhandenen Bereichs von Rekursion.  
  
-   **Get-DnsServerRecursionScope**. Dieses Cmdlet Ruft Informationen zu vorhandenen Rekursion Bereiche ab.  
  
-   **Add-DnsServerClientSubnet**. Dieses Cmdlet erstellt ein neues Subnetz der DNS-Client. Subnetze werden von DNS-Richtlinien verwendet, um zu identifizieren, in dem ein DNS-Client befindet.  
  
-   **Remove-DnsServerClientSubnet**. Dieses Cmdlet entfernt die vorhandene DNS-Client-Subnetze.  
  
-   **Set-DnsServerClientSubnet**. Dieses Cmdlet ändert die Einstellungen eines vorhandenen DNS-Client-Subnetzes.  
  
-   **Get-DnsServerClientSubnet**. Dieses Cmdlet Ruft Informationen zu vorhandenen Subnetzen von DNS-Clients ab.  
  
-   **Add-DnsServerQueryResolutionPolicy**. Dieses Cmdlet erstellt eine neue Richtlinie zur DNS-Abfrage. Richtlinien für DNS-Abfrage werden verwendet, um anzugeben, oder wenn Sie eine Abfrage zu geantwortet wird, anhand verschiedener Kriterien.  
  
-   **Remove-DnsServerQueryResolutionPolicy**. Dieses Cmdlet entfernt die vorhandene DNS-Richtlinien.  
  
-   **Set-DnsServerQueryResolutionPolicy**. Dieses Cmdlet ändert die Einstellungen einer vorhandenen DNS-Richtlinie.  
  
-   **Get-DnsServerQueryResolutionPolicy**. Dieses Cmdlet Ruft Informationen zu vorhandenen DNS-Richtlinien ab.  
  
-   **Enable-DnsServerPolicy**. Mit diesem Cmdlet können vorhandene DNS-Richtlinien.  
  
-   **Disable-DnsServerPolicy**. Dieses Cmdlet deaktiviert die vorhandene DNS-Richtlinien.  
  
-   **Add-DnsServerZoneTransferPolicy**. Dieses Cmdlet erstellt eine neue DNS-Zone Übertragungsrichtlinie. DNS-Zone Übertragung Richtlinien angeben, ob eine zonenübertragung, basierend auf anderen Kriterien zu ignorieren oder verweigern.  
  
-   **Remove-DnsServerZoneTransferPolicy**. Dieses Cmdlet entfernt die vorhandene DNS-Server Zone Übertragung Richtlinien.  
  
-   **Set-DnsServerZoneTransferPolicy**. Dieses Cmdlet ändert die Einstellungen einer vorhandenen DNS-Zone datenübertragungsrichtlinie.  
  
-   **Get-DnsServerResponseRateLimiting**. Dieses Cmdlet ruft RRL Einstellungen ab.  
  
-   **Set-DnsServerResponseRateLimiting**. Dieses Cmdlet ändert die RRL vertrauen.  
  
-   **Add-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet erstellt eine Ausnahmeliste RRL auf dem DNS-Server.  
  
-   **Get-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet ruft RRL Excception Listen ab.  
  
-   **Remove-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet entfernt eine vorhandene Liste der RRL-Ausnahme.  
  
-   **Set-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet ändert die RRL Ausnahme enthält.  
  
-   **Add-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um Unbekannter Datensatztyp zu unterstützen.  
  
-   **Get-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um Unbekannter Datensatztyp zu unterstützen.  
  
-   **Remove-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um Unbekannter Datensatztyp zu unterstützen.  
  
-   **Set-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um die Unterstützung Unbekannter Datensatztyp

Weitere Informationen finden Sie unter den folgenden Referenzthemen für Windows Server 2016, Windows PowerShell-Befehl.

- [DNS-Server-Modul](https://docs.microsoft.com/powershell/module/dnsserver/?view=win10-ps)
- [DnsClient-Modul](https://docs.microsoft.com/powershell/module/dnsclient/?view=win10-ps)

## <a name="see-also"></a>Siehe auch  
  
-   [Neues in DNS-Client](What-s-New-in-DNS-Client.md)  
  

  

