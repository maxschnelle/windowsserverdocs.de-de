---
title: Neues in DNS-Server unter Windows Server
description: Dieses Thema enthält eine Übersicht über neue Funktionen in DNS-Server unter Windows Server2016 und höher
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: c9cecb94-3cd5-4da7-9a3e-084148b8226b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3ddb8920c045f231dcf5286283d9895ef6ffff47
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dns-server-in-windows-server"></a>Neues in DNS-Server unter Windows Server

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema wird beschrieben, den Domain Name System (DNS)-Serverfunktionen, die neuen oder geänderten in Windows Server 2016.  
  
In Windows Server 2016 bietet DNS-Server verbesserte Unterstützung in den folgenden Bereichen.  
  
|Funktionen|Neue oder verbesserte|Beschreibung|  
|-----------------|-------------------|---------------|  
|DNS-Richtlinien|Neu|Sie können konfigurieren, dass DNS-Richtlinien, um anzugeben, wie ein DNS-Server auf DNS-Abfragen reagiert. DNS-Antworten können basierend auf Client-IP-Adresse (Standort), des Tages sowie einige andere Parameter. DNS-Richtlinien können Standortbestimmung DNS, Verwaltung, den Lastenausgleich, Split-Brain-DNS- und andere Szenarien.|  
|Antworten beschränken (RRL)|Neu|Sie können die Antwort die Begrenzung der Übertragungsrate die DNS-Server aktivieren. Auf diese Weise vermeiden Sie die Möglichkeit, schädliche Systeme, die mithilfe von DNS-Servern zum Initiieren eines Denial-of-Service-Angriff auf einen DNS-Client.|  
|DNS-basierte Authentifizierung von benannten Entitäten (DANE)|Neu|TLSA (Transport Layer Security-Authentifizierung) Datensätze können Sie Informationen zu DNS-Clients bereitzustellen, die welche Zertifizierungsstelle Zustand sollte ein Zertifikat für Ihren Domänennamen erwarten. Dies verhindert, dass Man-in-the-Middle-Angriffe, in denen ein Benutzer möglicherweise beschädigt werden den DNS-Cache auf ihrer eigenen Website verweisen, und geben ein Zertifikat, das sie von einer anderen Zertifizierungsstelle ausgestellt.|  
|Unterstützung für unbekannte Datensatz|Neu|Sie können Datensätze hinzufügen, die nicht explizit durch den Windows-DNS-Server mithilfe der Funktion unbekannten Eintrag unterstützt werden.|  
|IPv6-Stammhinweise|Neu|Sie können die systemeigene IPV6 verwenden, Stammhinweise zu unterstützen, um die Auflösung von Internetnamen verwenden die IPV6-Server ausführen.|  
|Windows PowerShell-Unterstützung|Verbesserte|Neue Windows PowerShell-Cmdlets sind für DNS-Server verfügbar.|  
  
## <a name="dns-policies"></a>DNS-Richtlinien

DNS-Richtlinien können für die Verwaltung von GeoLocation-positionsbasierte Datenverkehr, intelligente DNS-Antworten basierend auf der Tageszeit Sie einen DNS-Server für Split\-Brain-Bereitstellung konfiguriert verwalten Anwenden von Filtern auf DNS-Abfragen und vieles mehr. Die folgenden Artikel enthalten weitere Details zu diesen Funktionen.

-   **Anwendung für den Netzwerklastenausgleich.** Wenn Sie mehrere Instanzen einer Anwendung an verschiedenen Standorten bereitgestellt haben, können Sie DNS-Richtlinien, um den Datenverkehr zwischen den anderen Anwendung-Instanzen, die dynamische Zuweisung für die Anwendung von der Auslastung Lastenausgleich.

-   **Geo\-Location basierende Datenverkehrsverwaltung.** DNS-Richtlinien können auf primären und sekundären DNS-Server reagiert auf DNS-Clientabfragen basierend auf den geografischen Standort des Clients und die Ressource zu der der Client versucht, eine Verbindung herstellen können den Client mit der IP-Adresse der am nächsten gelegenen Ressource bereitstellen. 

-   **Teilen Sie Brain-DNS.** Mit Split\-Brain-DNS DNS-Einträge werden in verschiedenen Bereichen von Zone auf dem gleichen DNS-Server aufgeteilt, und DNS-Clients erhalten eine Antwort basierend auf, ob die Clients für interne oder externe Clients sind. Sie können Split\-Brain-DNS für Active Directory-integrierte Zonen oder für die Zonen auf eigenständigen DNS-Servern konfigurieren.

-   **Filtern.** Sie können konfigurieren, dass DNS-Richtlinie, um die Abfrage Filter erstellen, die auf Kriterien basieren, die Sie angeben. Abfragefiltern in DNS-Richtlinien können Sie so konfigurieren Sie den DNS-Server zum Reagieren auf eine benutzerdefinierte basierend auf dem DNS-Abfrage und die DNS-Client, der die DNS-Abfrage sendet. 
-   **Forensik.** DNS-Richtlinien können zum Umleiten von schädlichen DNS-Clients auf eine vorhandene IP-Adresse anstelle von Weiterleitung an den Computer, den sie erreichen möchten.

-   **Tageszeit-basierte Umleitung.** DNS-Richtlinien können Sie die Anwendungsdatenverkehr auf verschiedenen geografisch verteilten Instanzen einer Anwendung mithilfe von DNS-Richtlinien, die auf der Tageszeit basierende verteilen. 
  
Sie können auch DNS-Richtlinien für Active Directory-integrierten DNS-Zonen.

Weitere Informationen finden Sie in der [DNS-Gruppenrichtlinienszenarien](deploy/DNS-Policies-Overview.md).

## <a name="response-rate-limiting"></a>Antwort die Begrenzung der Übertragungsrate

Sie können steuern, wie auf einem DNS-Client-Anforderungen reagieren, wenn der Server verschiedene Anforderungen für den gleichen Client empfängt RRL-Einstellungen konfigurieren. Auf diese Weise können Sie verhindern einen Denial of Service (Dos)-Angriff mithilfe der DNS-Server senden. Beispielsweise kann ein Bot net Anforderungen zum DNS-Server die IP-Adresse von einem dritten Computer als Requestor mit senden. Ohne RRL möglicherweise die DNS-Server auf die Anforderungen den dritten Computer Überflutung reagieren. Wenn Sie RRL verwenden, können Sie die folgenden Einstellungen konfigurieren:  
  
-   **Antworten pro Sekunde**. Dies ist die maximale Anzahl von oft, die dieselbe Antwort an einen Client innerhalb einer Sekunde gewährt wird.  
  
-   **Fehler pro Sekunde**. Dies ist die maximale Anzahl an, wie oft, die eine Fehlerantwort an den gleichen Client innerhalb einer Sekunde gesendet wird.  
  
-   **Fenster**. Dies ist die Anzahl der Sekunden für die Antworten auf einem Client angehalten werden, wenn zu viele angefordert werden.  
  
-   **Speicherverluste Rate**. Dies ist wie häufig der DNS-Server eine Abfrage der Zeit antwortet, Antworten angehalten werden. Z. B. wenn der Server Reaktionen auf einem Client für 10 Sekunden angehalten und Datenverlust 5 ist, antwortet der Server weiterhin um eine Abfrage für alle 5-Abfragen gesendet. Dadurch können die legitime Clients Antworten erhalten, auch wenn der DNS-Server begrenzen auf dem Subnetz oder die FQDN-Antworten angewendet wird.  
  
-   **TC Rate**. Dies wird verwendet, weisen Sie den Client eine Verbindung herstellen mit TCP als Antworten an den Client angehalten werden. Beispielsweise wird der TC beträgt 3 des Servers unterbricht Reaktionen auf einen bestimmten Client und der Server ausstellen eine Anforderung für TCP-Verbindung für jeden 3 empfangenen Abfragen. Stellen Sie sicher, dass der Wert für TC Rate niedriger als der Verlust, damit dem Client eine Verbindung über TCP herstellen, bevor Sie Unternehmensdaten, Antworten können.  
  
-   **Maximale Antworten**. Dies ist die maximale Anzahl von Antworten, die der Server für einen Client ausstellt, und Antworten angehalten werden.  
  
-   **Weiße Liste Domänen**. Dies ist eine Liste der Domänen, die von RRL Einstellungen ausgeschlossen werden.  
  
-   **Weiße Liste Subnetze**. Hierbei handelt es sich um eine Liste der Subnetze aus RRL Einstellungen ausgeschlossen werden.  
  
-   **Weiße Liste Serverschnittstellen**. Dies ist eine Liste der DNS-Server-Schnittstellen, die von RRL Einstellungen ausgeschlossen werden.  
  
## <a name="dane-support"></a>DANE-Unterstützung

DANE Unterstützung können \ (RFC 6394 und 6698\), um die DNS-Clients anzugeben, was Zertifizierungsstelle, die sie erwarten, dass Zertifikate für Domänen Namen von ausgestellt werden in der DNS-Server gehostet. Dies verhindert, dass Man-in-the-Middle-Angriffe, die Person handelt, können Sie einen DNS-Cache beschädigt, und zeigen Sie einen DNS-Namen auf ihrer eigenen IP-Adresse.  
  
Angenommen Sie, z. B. Host eine sichere Website, die SSL an www.contoso.com verwendet wird, mithilfe eines Zertifikats von einer bekannten Zertifizierungsstelle mit dem Namen CA1. Eine Person vielleicht dennoch ein Zertifikat für www.contoso.com zu einem anderen, nicht-damit-Well-bekannten, Zertifikat Autorität für die CA2 mit dem Namen abgerufen. Klicken Sie dann die Entität, die falsche www.contoso.com-Website hostet den DNS-Cache Gruppenseite gefälschte www.contoto.com auf Client oder Server beschädigt möglicherweise zu. Der Benutzer kann wird ein Zertifikat von CA2, angezeigt werden und einfach bestätigen es und mit dem falschen Standort verbinden. Mit DANE würde der Client wenden Sie sich an dem DNS-Server für "contoso.com" für den Datensatz TLSA gefragt werden, und erfahren Sie, dass das Zertifikat für www.contoso.com Probleme nach CA1 war. Wenn Sie mit einem Zertifikat von einer anderen Zertifizierungsstelle angegeben wird, wird die Verbindung abgebrochen.  
  
## <a name="unknown-record-support"></a>Unterstützung für unbekannte Datensatz

Einen Eintrag"Unbekannt" ist ein Ressourceneintrag, deren RDATA Format nicht dem DNS-Server bekannt ist. Die neu hinzugefügte Unterstützung für unbekannte Datensatztypen (RFC 3597) bedeutet, dass Sie die nicht unterstützten Datentypen in der Windows-DNS-Server-Zonen im Binärformat über das Netzwerk hinzufügen können. Die Windows Zwischenspeichern Resolver hat bereits die Möglichkeit, unbekannte Datensatztypen zu verarbeiten. Windows DNS-Server aufzeichnen spezifische Verarbeitungsvorgänge unbekannte Datensätze nicht, aber sendet diese wieder in Antworten Wenn Abfragen für sie empfangen werden.  
  
## <a name="ipv6-root-hints"></a>IPv6-Stammhinweise

Die IPV6-Stammhinweise wurden von IANA, veröffentlichte Windows-DNS-Server hinzugefügt. Die Internet-Namensabfragen können jetzt IPv6-Stammserver verwenden, für die Durchführung von Name-Lösungen.

## <a name="windows-powershell-support"></a>Windows PowerShell-Unterstützung

Die folgenden neuen Windows PowerShell-Cmdlets und Parameter sind in Windows Server 2016 eingeführt.
  
-   **Hinzufügen DnsServerRecursionScope**. Dieses Cmdlet erstellt einen neuen Bereich der Rekursion auf dem DNS-Server. Rekursion Bereiche werden von DNS-Richtlinien verwendet, eine Liste der Weiterleitungen, die in einer DNS-Abfrage verwendet werden sollen.  
  
-   **Remove-DnsServerRecursionScope**. Dieses Cmdlet entfernt die vorhandene Rekursion Bereiche.  
  
-   **Set-DnsServerRecursionScope**. Dieses Cmdlet ändert die Einstellungen für einen vorhandenen Rekursion Bereich.  
  
-   **Get-DnsServerRecursionScope**. Dieses Cmdlet Ruft Informationen zu vorhandenen Rekursion Bereiche ab.  
  
-   **Hinzufügen DnsServerClientSubnet**. Dieses Cmdlet erstellt ein neues DNS-Client-Subnetz. Subnetze werden von DNS-Richtlinien verwendet, um zu identifizieren, wo ein DNS-Client befindet.  
  
-   **Remove-DnsServerClientSubnet**. Dieses Cmdlet entfernt die vorhandene DNS-Client-Subnetzen.  
  
-   **Set-DnsServerClientSubnet**. Dieses Cmdlet ändert die Einstellungen für eine vorhandene DNS-Client-Subnetz.  
  
-   **Get-DnsServerClientSubnet**. Dieses Cmdlet Ruft Informationen zu vorhandenen DNS-Client-Subnetzen.  
  
-   **Hinzufügen DnsServerQueryResolutionPolicy**. Dieses Cmdlet erstellt eine neue Richtlinie für DNS-Abfrage Auflösung. DNS-Abfrage Auflösung Richtlinien werden verwendet, um anzugeben, oder wenn Sie eine Abfrage eingeht, basierend auf anderen Kriterien.  
  
-   **Remove-DnsServerQueryResolutionPolicy**. Dieses Cmdlet entfernt die vorhandene DNS-Richtlinien.  
  
-   **Set-DnsServerQueryResolutionPolicy**. Dieses Cmdlet ändert die Einstellungen für eine vorhandene DNS-Richtlinie.  
  
-   **Get-DnsServerQueryResolutionPolicy**. Dieses Cmdlet Ruft Informationen zu vorhandenen DNS-Richtlinien ab.  
  
-   **Enable-DnsServerPolicy**. Dieses Cmdlet aktiviert die vorhandene DNS-Richtlinien.  
  
-   **Disable-DnsServerPolicy**. Dieses Cmdlet deaktiviert die vorhandene DNS-Richtlinien.  
  
-   **Hinzufügen DnsServerZoneTransferPolicy**. Dieses Cmdlet erstellt eine neue DNS-Zone Übertragung Serverrichtlinie. DNS-Zone Übertragung Richtlinien angeben, ob eine zonenübertragung basierend auf unterschiedliche Kriterien zu ignorieren oder verweigert.  
  
-   **Remove-DnsServerZoneTransferPolicy**. Dieses Cmdlet entfernt die vorhandene DNS-Zone Übertragung Serverrichtlinien.  
  
-   **Set-DnsServerZoneTransferPolicy**. Dieses Cmdlet ändert die Einstellungen von einer vorhandenen DNS-Zone Übertragungsrichtlinie.  
  
-   **Get-DnsServerResponseRateLimiting**. Dieses Cmdlet ruft RRL-Einstellungen.  
  
-   **Set-DnsServerResponseRateLimiting**. Dieses Cmdlet ändert die RRL Settigns.  
  
-   **Hinzufügen DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet erstellt eine Ausnahmeliste RRL auf dem DNS-Server.  
  
-   **Get-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet ruft RRL Excception Listen.  
  
-   **Remove-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet entfernt eine vorhandene RRL Ausnahmeliste.  
  
-   **Set-DnsServerResponseRateLimitingExceptionlist**. Dieses Cmdlet ändert die RRL Ausnahmelisten.  
  
-   **Hinzufügen DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um unbekannte Datensatztyp zu unterstützen.  
  
-   **Get-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um unbekannte Datensatztyp zu unterstützen.  
  
-   **Remove-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, um unbekannte Datensatztyp zu unterstützen.  
  
-   **Set-DnsServerResourceRecord**. Dieses Cmdlet wurde aktualisiert, damit unbekannte Datensatztyp unterstützt

Weitere Informationen finden Sie unter den folgenden Themen der Windows Server 2016 Windows PowerShell-Befehl.

- [DNS-Server-Modul](https://technet.microsoft.com/itpro/powershell/windows/dns-server/index)
- [DnsClient-Modul](https://technet.microsoft.com/itpro/powershell/windows/dns-client/index)

## <a name="see-also"></a>Siehe auch  
  
-   [Neues in DNS-Client](What-s-New-in-DNS-Client.md)  
  

  

