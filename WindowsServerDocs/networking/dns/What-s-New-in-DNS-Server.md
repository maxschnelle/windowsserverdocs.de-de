---
title: Neues in DNS-Server unter Windows Server
description: Dieses Thema bietet einen Überblick über die neuen Features in DNS-Server unter Windows Server 2016 und höheren Versionen.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: c9cecb94-3cd5-4da7-9a3e-084148b8226b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: de502d7be023d12e3350063e467a60356b2472c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406235"
---
# <a name="whats-new-in-dns-server-in-windows-server"></a>Neues in DNS-Server unter Windows Server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden die Domain Name System (DNS)-Serverfunktionen beschrieben, die in Windows Server 2016 neu oder geändert wurden.  
  
In Windows Server 2016 bietet der DNS-Server eine verbesserte Unterstützung in den folgenden Bereichen.  
  
|Funktionalität|Neu oder verbessert|Beschreibung|  
|-----------------|-------------------|---------------|  
|DNS-Richtlinien|Neu|Sie können DNS-Richtlinien konfigurieren, um anzugeben, wie ein DNS-Server auf DNS-Abfragen antwortet. DNS-Antworten können auf der Client-IP-Adresse (Speicherort), der Tageszeit und mehreren anderen Parametern basieren. DNS-Richtlinien ermöglichen standortabhängige DNS, Datenverkehrs Verwaltung, Lastenausgleich, Split-Brain-DNS und andere Szenarien.|  
|Antwortraten Begrenzung (RRL)|Neu|Sie können die Reaktionsraten Begrenzung für Ihre DNS-Server aktivieren. Auf diese Weise können Sie verhindern, dass böswillige Systeme, die Ihre DNS-Server verwenden, einen Denial-of-Service-Angriff auf einen DNS-Client initiieren.|  
|DNS-basierte Authentifizierung benannter Entitäten (Dane)|Neu|Sie können die Datensätze von TLSA (Transport Layer Security Authentication) verwenden, um Informationen für DNS-Clients bereitzustellen, die angeben, von welcher Zertifizierungsstelle ein Zertifikat für Ihren Domänen Namen erwartet werden soll. Dadurch werden man-in-the-Middle-Angriffe verhindert, bei denen jemand den DNS-Cache beschädigen könnte, um auf seine eigene Website zu verweisen, und ein Zertifikat bereitstellen, das von einer anderen Zertifizierungsstelle ausgestellt wurde.|  
|Unbekannte Daten Satz Unterstützung|Neu|Sie können Datensätze hinzufügen, die vom Windows-DNS-Server nicht explizit unterstützt werden. verwenden Sie dazu die Funktion für unbekannte Einträge|  
|IPv6-Stamm Hinweise|Neu|Mithilfe der systemeigenen IPv6-Stamm Hinweis Unterstützung können Sie die Internet Namensauflösung mithilfe der IPv6-Stamm Server durchführen.|  
|Windows PowerShell-Unterstützung|Verbessert|Für den DNS-Server sind neue Windows PowerShell-Cmdlets verfügbar.|  
  
## <a name="dns-policies"></a>DNS-Richtlinien

Sie können die DNS-Richtlinie für die georeduntbasierte Datenverkehrs Verwaltung, intelligente DNS-Antworten basierend auf der Tageszeit, die Verwaltung eines einzelnen DNS-Servers, der für die Split @ no__t-0brain-Bereitstellung konfiguriert ist, das Anwenden von Filtern auf DNS-Abfragen usw. verwenden. Die folgenden Elemente bieten weitere Details zu diesen Funktionen.

-   **Anwendungs Lastenausgleich.** Wenn Sie mehrere Instanzen einer Anwendung an verschiedenen Speicherorten bereitgestellt haben, können Sie die DNS-Richtlinie verwenden, um die Auslastung des Datenverkehrs zwischen den verschiedenen Anwendungs Instanzen auszugleichen und die Datenverkehrs Last für die Anwendung dynamisch zuzuweisen.

-   **Geor@ no__t-1 Location based Traffic Management.** Mithilfe der DNS-Richtlinie können primäre und sekundäre DNS-Server auf DNS-Client Abfragen basierend auf dem geografischen Standort des Clients und der Ressource, mit der der Client eine Verbindung herzustellen versucht, Antworten, und dem Client wird die IP-Adresse des nächstgelegenen Ressource. 

-   **Teilen Sie das Hirn-DNS.** Mit Split @ no__t-0brain-DNS werden DNS-Einträge in verschiedene Zonen Bereiche auf demselben DNS-Server aufgeteilt, und DNS-Clients erhalten eine Antwort, je nachdem, ob es sich bei den Clients um interne oder externe Clients handelt. Sie können Split @ no__t-0brain-DNS für Active Directory integrierte Zonen oder Zonen auf eigenständigen DNS-Servern konfigurieren.

-   **Filterung.** Sie können die DNS-Richtlinie konfigurieren, um Abfrage Filter basierend auf den von Ihnen angegebenen Kriterien zu erstellen. Mithilfe von Abfrage Filtern in der DNS-Richtlinie können Sie den DNS-Server so konfigurieren, dass er basierend auf der DNS-Abfrage und dem DNS-Client, der die DNS-Abfrage sendet, Benutzer definiert reagiert 
-   **Forensik.** Sie können DNS-Richtlinien verwenden, um böswillige DNS-Clients an eine nicht-@ no__t-0vorhandene IP-Adresse umzuleiten, anstatt Sie an den Computer weiterzuleiten, den Sie zu erreichen versuchen.

-   **Uhrzeit der täglichen Umleitung.** Mithilfe der DNS-Richtlinie können Sie den Anwendungs Datenverkehr mithilfe von DNS-Richtlinien, die auf der Tageszeit basieren, über verschiedene geografisch verteilte Instanzen einer Anwendung verteilen. 
  
DNS-Richtlinien können auch für Active Directory integrierte DNS-Zonen verwendet werden.

Weitere Informationen finden Sie im [Leitfaden zum DNS-Richtlinien Szenario](deploy/DNS-Policies-Overview.md).

## <a name="response-rate-limiting"></a>Beschränkung der Antwort Rate

Sie können die RRL-Einstellungen konfigurieren, um zu steuern, wie auf Anforderungen an einen DNS-Client reagiert werden soll, wenn der Server mehrere Anforderungen an denselben Client empfängt. Auf diese Weise können Sie verhindern, dass jemand einen Denial-of-Service-Angriff (DOS) mithilfe Ihrer DNS-Server sendet. Beispielsweise kann ein bot-Netzanforderungen mithilfe der IP-Adresse eines dritten Computers als Anforderer an den DNS-Server senden. Ohne RRL können Ihre DNS-Server auf alle Anforderungen reagieren und den dritten Computer überfluten. Wenn Sie RRL verwenden, können Sie die folgenden Einstellungen konfigurieren:  
  
-   **Antworten pro Sekunde**. Dies ist die maximale Häufigkeit, mit der die gleiche Antwort einem Client innerhalb einer Sekunde zugewiesen wird.  
  
-   **Fehler pro Sekunde**. Dies ist die maximale Häufigkeit, mit der eine Fehler Antwort innerhalb einer Sekunde an denselben Client gesendet wird.  
  
-   **Fenster**. Dies ist die Anzahl von Sekunden, für die Antworten auf einen Client angehalten werden, wenn zu viele Anforderungen gestellt werden.  
  
-   Die **Rate der Lecks**. Dies ist die Häufigkeit, mit der der DNS-Server während der Zeit, in der Antworten angehalten werden, auf eine Abfrage antwortet. Wenn beispielsweise der Server 10 Sekunden lang Antworten an einen Client hält und der Wert für die Dichte 5 beträgt, antwortet der Server immer noch auf eine Abfrage für alle fünf gesendeten Abfragen. Dies ermöglicht es den legitimen Clients, auch dann Antworten zu erhalten, wenn der DNS-Server die Antwortraten Begrenzung für das Subnetz oder den FQDN anwendet.  
  
-   **TC-Rate**. Hiermit wird der Client angewiesen, eine Verbindung mit TCP herzustellen, wenn Antworten auf den Client angehalten werden. Wenn die TC-Rate beispielsweise 3 beträgt und der Server Antworten an einen bestimmten Client hält, gibt der Server eine Anforderung für eine TCP-Verbindung für jede 3 empfangene Abfrage aus. Stellen Sie sicher, dass der Wert für die TC-Rate niedriger ist als die Verlustrate, um dem Client die Möglichkeit zu geben, über TCP eine Verbindung herzustellen, bevor Antworten wieder hergestellt werden.  
  
-   **Maximale Antworten**. Dies ist die maximale Anzahl von Antworten, die der Server für einen Client ausgibt, während Antworten angehalten werden.  
  
-   **Weiß Listen Domänen**. Dies ist eine Liste der Domänen, die von den RRL-Einstellungen ausgeschlossen werden sollen.  
  
-   Die **Subnetze der weißen Liste**. Dies ist eine Liste von Subnetzen, die von den RRL-Einstellungen ausgeschlossen werden sollen.  
  
-   **White List-Server Schnittstellen**. Dies ist eine Liste von DNS-Server Schnittstellen, die von den RRL-Einstellungen ausgeschlossen werden sollen.  
  
## <a name="dane-support"></a>Unterstützung von Dane

Sie können die DCS-Unterstützung \(rfc 6394 und 6698 @ no__t-1 verwenden, um für Ihre DNS-Clients anzugeben, von welcher Zertifizierungsstelle die Zertifikate für Domänen Namen, die auf Ihrem DNS-Server gehostet werden, ausgestellt werden sollen. Dies verhindert eine Art von man-in-the-Middle-Angriff, bei dem jemand einen DNS-Cache beschädigen und einen DNS-Namen auf seine eigene IP-Adresse verweisen kann.  
  
Stellen Sie sich beispielsweise vor, dass Sie eine sichere Website hosten, die SSL unter www.contoso.com verwendet, indem Sie ein Zertifikat von einer bekannten Autorität namens CA1 verwenden. Möglicherweise kann ein Benutzer ein Zertifikat für www.contoso.com von einer anderen, nicht so bekannten Zertifizierungsstelle mit dem Namen "Ca2" erhalten. Anschließend kann die Entität, die die Fake www.contoso.com-Website gehostet, den DNS-Cache eines Clients oder Servers beschädigen, um www.contoto.com auf die gefälschte Website zu verweisen. Dem Endbenutzer wird ein Zertifikat von "Ca2" angezeigt, und er kann es einfach bestätigen und eine Verbindung mit dem gefälschten Standort herstellen. Bei der Verwendung von "Dane" würde der Client eine Anforderung an den DNS-Server für contoso.com stellen, die den TLSA-Datensatz fragt und erfährt, dass das Zertifikat für www.contoso.com von CA1 ausgegeben wurde. Wenn ein Zertifikat von einer anderen Zertifizierungsstelle angezeigt wird, wird die Verbindung abgebrochen.  
  
## <a name="unknown-record-support"></a>Unbekannte Daten Satz Unterstützung

Ein "Unbekannter Datensatz" ist ein RR, dessen rdata-Format dem DNS-Server nicht bekannt ist. Die neu hinzugefügte Unterstützung für die Typen "Unbekannter Datensatz" (RFC 3597) bedeutet, dass Sie die nicht unterstützten Daten Satz Typen in den Windows DNS-Server Zonen im Binärformat "Binärformat" hinzufügen können. Der Windows Caching-Konflikt Löser ist bereits in der Lage, unbekannte Daten Satz Typen zu verarbeiten. Der Windows-DNS-Server führt keine Daten Satz spezifische Verarbeitung für unbekannte Datensätze aus, sendet Sie jedoch zurück in Antworten, wenn Abfragen für Sie empfangen werden.  
  
## <a name="ipv6-root-hints"></a>IPv6-Stamm Hinweise

Die IPv6-Stamm Hinweise, wie Sie von IANA veröffentlicht wurden, wurden dem Windows-DNS-Server hinzugefügt. Die Internet Namen Abfragen können jetzt IPv6-Stamm Server zum Durchführen von namens Auflösungen verwenden.

## <a name="windows-powershell-support"></a>Windows PowerShell-Unterstützung

Die folgenden neuen Windows PowerShell-Cmdlets und-Parameter werden in Windows Server 2016 eingeführt.
  
-   **Add-dnsserverrecursionscope**. Mit diesem Cmdlet wird ein neuer Rekursions Bereich auf dem DNS-Server erstellt. Rekursions Bereiche werden von DNS-Richtlinien verwendet, um eine Liste der Weiterleitungen anzugeben, die in einer DNS-Abfrage verwendet werden sollen.  
  
-   **Remove-dnsserverrecursionscope**. Mit diesem Cmdlet werden vorhandene Rekursions Bereiche entfernt.  
  
-   **Set-dnsserverrecursionscope**. Mit diesem Cmdlet werden die Einstellungen eines vorhandenen Rekursions Bereichs geändert.  
  
-   **Get-dnsserverrecursionscope**. Mit diesem Cmdlet werden Informationen zu vorhandenen Rekursions Bereichen abgerufen.  
  
-   **Add-dnsserverclientsubnet**. Dieses Cmdlet erstellt ein neues DNS-clientsubnetz. Subnetze werden von DNS-Richtlinien verwendet, um zu ermitteln, wo sich ein DNS-Client befindet.  
  
-   **Remove-dnsserverclientsubnet**. Mit diesem Cmdlet werden vorhandene DNS-Clientsubnetze entfernt.  
  
-   **Set-dnsserverclientsubnet**. Mit diesem Cmdlet werden die Einstellungen eines vorhandenen DNS-Clientsubnetzes geändert.  
  
-   **Get-dnsserverclientsubnet**. Mit diesem Cmdlet werden Informationen über vorhandene DNS-Clientsubnetze abgerufen.  
  
-   **Add-dnsserverqueryresolutionpolicy**. Dieses Cmdlet erstellt eine neue Richtlinie für die DNS-Abfrage Auflösung. DNS-Abfrage Auflösungs Richtlinien werden verwendet, um anzugeben, wie oder ob eine Abfrage auf Grundlage unterschiedlicher Kriterien antwortet.  
  
-   **Remove-dnsserverqueryresolutionpolicy**. Mit diesem Cmdlet werden vorhandene DNS-Richtlinien entfernt.  
  
-   **Set-dnsserverqueryresolutionpolicy**. Mit diesem Cmdlet werden die Einstellungen einer vorhandenen DNS-Richtlinie geändert.  
  
-   **Get-dnsserverqueryresolutionpolicy**. Dieses Cmdlet ruft Informationen über vorhandene DNS-Richtlinien ab.  
  
-   **Enable-dnsserverpolicy**. Mit diesem Cmdlet werden vorhandene DNS-Richtlinien aktiviert.  
  
-   **Deaktivieren Sie-dnsserverpolicy**. Mit diesem Cmdlet werden vorhandene DNS-Richtlinien deaktiviert.  
  
-   **Add-dnsserverzonetransferpolicy**. Mit diesem Cmdlet wird eine neue Richtlinie für die DNS-Server Zonen Übertragung erstellt. DNS-Zonen Übertragungs Richtlinien geben an, ob eine Zonen Übertragung basierend auf unterschiedlichen Kriterien verweigert oder ignoriert werden soll.  
  
-   **Remove-dnsserverzonetransferpolicy**. Mit diesem Cmdlet werden vorhandene Richtlinien für die DNS-Server Zonen Übertragung entfernt.  
  
-   **Set-dnsserverzonetransferpolicy**. Mit diesem Cmdlet werden die Einstellungen einer vorhandenen Richtlinie für die Zonen Übertragung von DNS-Servern geändert.  
  
-   **Get-dnsserverresponse Server**. Mit diesem Cmdlet werden RRL-Einstellungen abgerufen.  
  
-   **Set-dnsserverresponse Server**. Dieses Cmdlet ändert RRL-Aufstellungen.  
  
-   **Add-dnsserverresponse seratelimitingexceptionlist**. Dieses Cmdlet erstellt eine RRL-Ausnahmeliste auf dem DNS-Server.  
  
-   **Get-dnsserverresponseratelimitingexceptionlist**. Dieses Cmdlet ruft die RRL-excception-Listen ab.  
  
-   **Remove-dnsserverresponseratelimitingexceptionlist**. Mit diesem Cmdlet wird eine vorhandene RRL-Ausnahmeliste entfernt.  
  
-   **Set-dnsserverresponse seratelimitingexceptionlist**. Dieses Cmdlet ändert die RRL-Ausnahme Listen.  
  
-   **Add-dnsserverresourcerecord**. Dieses Cmdlet wurde aktualisiert, um einen unbekannten Daten Satz Typen zu unterstützen.  
  
-   **Get-dnsserverresourcerecord**. Dieses Cmdlet wurde aktualisiert, um einen unbekannten Daten Satz Typen zu unterstützen.  
  
-   **Remove-dnsserverresourcerecord**. Dieses Cmdlet wurde aktualisiert, um einen unbekannten Daten Satz Typen zu unterstützen.  
  
-   **Set-dnsserverresourcerecord**. Dieses Cmdlet wurde aktualisiert und unterstützt einen unbekannten Daten Satz.

Weitere Informationen finden Sie in den folgenden Windows Server 2016 Windows PowerShell-Befehlsreferenz Themen.

- [DNSServer-Modul](https://docs.microsoft.com/powershell/module/dnsserver/?view=win10-ps)
- [Dnsclient-Modul](https://docs.microsoft.com/powershell/module/dnsclient/?view=win10-ps)

## <a name="see-also"></a>Siehe auch  
  
-   [Neues im DNS-Client](What-s-New-in-DNS-Client.md)  
  

  

