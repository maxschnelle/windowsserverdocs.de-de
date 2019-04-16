---
ms.assetid: 3acaa977-ed63-4e38-ac81-229908c47208
title: Behandlung von LDAP-Server-Cookies
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 89369cb1e52a315520062ca5ecc96b66ac3e2bfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="how-ldap-server-cookies-are-handled"></a>Behandlung von LDAP-Server-Cookies

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Legen in LDAP ergeben einige Abfragen einen großen Ergebnissatz. Solche Abfragen stellen eine Herausforderung dar, mit dem Windows-Server.  
  
Die Erfassung und Zusammenstellung solcher großen Ergebnissätze bedeutet einen beträchtlichen Arbeitsaufwand. Viele Attribute müssen von einer internen Darstellung in der LDAP-Wire-Darstellung konvertiert werden. Einige Attribute muss eine Konvertierung aus einem internen, meist binären Format in ein textbasiertes UTF-8-Format im LDAP-Antwort Frame auftreten.  
  
Eine weitere Herausforderung stellt Ergebnis mit Zehntausenden von Objekten erreichen sehr einfach mehrere hundert schiere fest. Diese erfordern sehr viel virtuellen Adressraum, und auch die Übertragung über das Netzwerk kann problematisch werden, wenn die TCP-Sitzung während der Übertragung zusammenbricht.  
  
Diese Kapazität und Logistik führten die Microsoft-LDAP-Entwickler zum Erstellen einer LDAP-Erweiterungs, die als "Seitenweisen Abfrage" bezeichnet. Es ist ein LDAP-Steuerelement, um eine große Abfrage in Blöcke kleinerer Ergebnissätze trennen implementieren. RFC-Standard geworden [RFC 2696](http://www.ietf.org/rfc/rfc2696).  
  
## <a name="cookie-handling-on-client"></a>Handhabung clientseitiger Cookies  
Methode der seitenweisen Abfrage verwendet die Seitengröße vom Client oder über eine [LDAP-Richtlinie](https://support.microsoft.com/kb/315071/en-us) ("MaxPageSize"). Der Client muss die Auslagerung durch Senden einer LDAP-Steuerelement aktivieren.  

  
Wenn Sie eine Abfrage mit sehr vielen Ergebnissen arbeiten, zu einem bestimmten Zeitpunkt ist die maximale Anzahl der zulässigen Objekte erreicht. Der LDAP-Server verpackt die Antwortnachricht und fügt ein Cookie mit Informationen, die sie die Suche später fortsetzen muss.  
  
Die Clientanwendung muss das Cookie als nicht transparentes Blob behandeln. Sie können die Anzahl der Objekte in der Antwort abrufen und kann weiterhin die Suche auf das Vorhandensein des Cookies. Der Client wird die Suche fortgesetzt wird, indem Sie die Abfrage an den LDAP-Server mit denselben Parametern wie z. B. Basisobjekt und Filter erneut gesendet und enthält den Cookiewert, der von der vorherigen Antwort zurückgegeben wurde.  
  
Wenn die Anzahl der Objekte keine Seite mehr füllt, die LDAP-Abfrage abgeschlossen und die Antwort enthält kein seitencookie. Wenn kein Cookie vom Server zurückgegeben wird, berücksichtigen der Client die seitenweise Suche erfolgreich abgeschlossen wurde.  
  
Wenn ein Fehler vom Server zurückgegeben wird, berücksichtigen der Client die seitenweise Suche fehlgeschlagen ist. Wiederholen die Suche wird dazu, dass die Suche von der ersten Seite.  
  
## <a name="server-side-cookie-handling"></a>Serverseitige Verarbeitung von Cookies  
Die Windows-Server gibt das Cookie an den Client und manchmal speichert Informationen im Zusammenhang mit das Cookie auf dem Server. Diese Informationen werden in einem Cache auf dem Server gespeichert und bestimmten Einschränkungen unterliegt.  
  
In diesem Fall das vom Server an den Client gesendete Cookie auch vom Server dient zum Suchen der Informationen aus dem Cache auf dem Server. Wenn der Client die seitenweise Suche fortsetzt, wird der Windows Server das Clientcookie sowie alle relevanten Informationen aus dem Cookiecache des Servers verwendet zum Fortsetzen der Suche. Wenn der Server relevanten Informationen aus den Servercache aus irgendeinem Grund nicht finden kann, wird die Suche nicht mehr unterstützt und Fehler an den Client zurückgegeben wird.  
  
## <a name="how-the-cookie-pool-is-managed"></a>Verwaltung des cookiepools  
Natürlich der LDAP-Server bedient mehrere Clients gleichzeitig, und auch mehrere Clients gleichzeitig Abfragen ausführen, die Verwendung von Cookiecache des Servers starten. Daher gibt es die Windows Server-Implementierung ist eine Überwachung der Verwendung von Cookies Pool und Grenzen cookiepoolauslastung so, dass der cookiepool zu viele Ressourcen nicht ausgeführt wird. Die Grenzwerte können vom Administrator festgelegt werden, verwenden die folgenden Einstellungen in LDAP-Richtlinie. Die Standardeinstellungen und erläuterungen sind:  
  
**MinResultSets: 4**  
  
Der LDAP-Server wird nicht auf die maximale Poolgröße erläutert, gesucht, wenn weniger als MinResultSets-Einträge in der Cookiecache des Servers.  
  
**MaxResultSetSize: 262.144 bytes**  
  
Die gesamte Cookiecache auf dem Server darf maximal MaxResultSetSize in Bytes nicht überschreiten. Wenn dies der Fall ist, werden Cookies beginnend beim ältesten gelöscht, bis der Pool kleiner als MaxResultSetSize in Bytes ist oder weniger als MinResultSets Cookies befinden sich in den Pool. Dies bedeutet, dass mit den Standardeinstellungen der LDAP-Server einen Pool von 450KB OK sein berücksichtigt, wenn Sie nur 3 Cookies gespeichert.  
  
**MaxResultSetsPerConn: 10**  
  
Der LDAP-Server kann nicht mehr als MaxResultSetsPerConn Cookies pro LDAP-Verbindung im Pool.  
  
## <a name="handling-deleted-cookies"></a>Handhabung gelöschter Cookies  
Das Entfernen von Cookie-Informationen aus dem Cache des LDAP-Server führt nicht zu einem Anwendungsfehler in allen Fällen. Anwendungen möglicherweise neu starten die seitenweise Suche von Beginn und schließen Sie sie in einem weiteren Versuch. Einige Anwendungen verfügen über diese Art von Wiederholungsmechanismus einen Wiederholungsmechanismus.  
  
Einige Programme möglicherweise eine seitenweise Suche durchlaufen, und schließen Sie sie nie. Dadurch kann Einträge in der LDAP-Server Cookie-Cache beibehalten werden, über den Mechanismus in Abschnitt 4 behandelt wird. Dies ist wichtig, um Speicherplatz auf dem Server für aktive LDAP-Suchvorgänge freizugeben.  
  
Was geschieht, wenn solches Cookie auf dem Server gelöscht wird und des Clients die Suche mit diesem Cookiehandle? Der LDAP-Server nicht findet das Cookie auf dem Server Cookiecache und gibt einen Fehler für die Abfrage zurück, die Fehlerantwort ähnelt:  
  
```  
00000057: LdapErr: DSID-xxxxxxxx, comment: Error processing control, data 0, v1db1  
```  
  
> [!NOTE]  
> Der Hexadezimalwert "DSID" variiert je nach Buildversion der Binärdateien des LDAP-Server.  
  
## <a name="reporting-on-the-cookie-pool"></a>Berichterstattung über den cookiepool  
Der LDAP-Server hat die Möglichkeit zum Protokollieren von Ereignissen über die Kategorie "16 Ldap Interface" in der [NTDS-Diagnoseschlüssel](https://support.microsoft.com/kb/314980/en-us). Wenn Sie diese Kategorie auf "2" festlegen, erhalten Sie die folgenden Ereignisse:  
  
```  
Log Name:      Directory Service  
Source:        Microsoft-Windows-ActiveDirectory_DomainService  
Event ID:      2898  
Task Category: LDAP Interface  
Level:         Information  
Description:  
Internal event: The LDAP server has reached the limit of the number of Result Sets it will maintain for a single connection.  A stored Result Set will be discarded.  This will result in a client being unable to continue a paged LDAP search.  
Maximum number of Result Sets allowed per LDAP connection:  
10  
Current number of Result Sets for this LDAP connection:  
11  
  
User Action  
The client should consider a more efficient search filter.  The limit for Maximum Result Sets per Connection may also be increased.  
  
```  
  
```  
Log Name:      Directory Service  
Source:        Microsoft-Windows-ActiveDirectory_DomainService  
Event ID:      2899  
Task Category: LDAP Interface  
Level:         Information  
Description:  
Internal event: The LDAP server has exceeded the limit of the LDAP Maximum Result Set Size. A stored Result Set will be discarded.  This will result in a client being unable to continue a paged LDAP search.   
  
Number of result sets currently stored:   
4   
Current Result Set Size:   
263504   
Maximum Result Set Size:   
262144   
Size of single Result Set being discarded:   
40876   
User Action   
The client should consider a more efficient search filter.  The limit for Maximum Result Set Size may also be increased.  
  
```  
  
Diese Ereignisse signalisieren, dass ein gespeichertes Cookie entfernt wurde. Es bedeutet nicht, dass ein Client den LDAP-Fehler, aber nur eingelesen wurden, dass der LDAP-Server die Verwaltung Grenzen für den Cache erreicht hat.  In einigen Fällen wird ein LDAP-Client kann die seitenweise Suche abgebrochen haben und der Fehler wird möglicherweise nie angezeigt.  
  
## <a name="monitoring-the-cookie-pool"></a>Überwachen des cookiepools  
Wenn Sie in Ihrer Domäne nie LDAP-Suche Fehler auftreten, müssen Sie möglicherweise nie auf Seite Suchen-Cookie für LDAP-Serverpool überwachen. Für den Fall, dass Sie LDAP-Suchen Sie verwandte Fehler in Ihrer Umgebung angezeigt, haben Sie möglicherweise ein Problem mit der das Cookie vom Administrator festgelegten Grenzen.  
  
Die Ereignisse 2898 und 2899 sind der einzige wissen, dass der LDAP-Server die administratorgrenzen erreicht hat. Wenn Sie die LDAP-Abfragen Fehler aufgrund der oben aufgeführten steuerverarbeitungsfehler auftritt, sollten Sie überprüfen, höheren Einschränkungen auf einem oder mehreren der LDAP-Richtlinieneinstellungen, die gemäß Abschnitt 4, je nachdem, welches, die Ereignis Sie abrufen.  
  
Wenn Sie auf Ihrem DC/LDAP-Server Ereignis 2898 angezeigt werden, wird empfohlen, dass Sie MaxResultSetsPerConn auf 25 festgelegt. Mehr als 25 parallele ausgeführte seitenweise Suchen über eine LDAP-Verbindung sind ungewöhnlich. Wenn Sie Ereignis 2898 weiterhin, untersuchen Sie die LDAP-Clientanwendung, die der Fehler auftritt. Der Verdacht auf wäre, dass sie aus irgendeinem Grund bleibt Abrufen weiterer seitenweiser Ergebnisse hängen, bewirkt, das Cookie ausstehende dass und eine neue Abfrage startet. Um festzustellen, ob die Anwendung zu einem bestimmten Zeitpunkt ausreichend Cookies müssten für ihre Zwecke, Sie können auch den Wert der MaxResultSetsPerConn über 25. erhöhen, wenn Sie 2899-Ereignisse auf den Domänencontrollern finden Sie unter, der Plan wären unterschiedlich. Wenn Ihr DC/LDAP-Server auf einem Computer mit ausreichend Arbeitsspeicher (mehrere GB freien Speicher) ausgeführt wird, sollten Sie Sie MaxResultSetSize auf dem LDAP-Server > = 250MB. Dieser Grenzwert ist groß genug für große Mengen von LDAP-Seite-Suchen auch in sehr großen Verzeichnissen.  
  
Wenn Sie sind immer noch angezeigt Ereignisse 2899 einen Pool von 250MB oder mehr wahrscheinlich mit vielen Clients mit sehr hohe Anzahl von Objekten zurückgegeben werden, werden in einer Weise sehr häufig abgefragt. Die Daten, die Sie sammeln können, mit der [Active Directory Data Collector Set](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx) Gebucht-Informationen finden Sie wiederholte seitenweise Abfragen, die Ihre LDAP-Server können. Diese Abfragen werden alle mit einer Reihe von "zurückgegebenen Einträge" angezeigt, die die Größe der verwendeten Seite entspricht.  
  
Wenn möglich, sollten Sie das Anwendungsdesign überprüfen und implementieren einen anderen Ansatz mit einer niedrigeren Frequenz, Datenvolumen und/oder weniger Clientinstanzen, die diese Daten Abfragen. Im Fall von Anwendungen für die, die Sie über Zugriff auf den Quellcode, dieses Handbuchs [Erstellen von effizienten AD-Enabled Anwendungen](https://msdn.microsoft.com/en-us/library/ms808539.aspx) können Sie besser verstehen die optimale Methode für Anwendungen für den Zugriff auf Active Directory.  
  
Wenn das Abfrageverhalten nicht geändert werden kann, wird ein Ansatz auch Hinzufügen von mehr replizierten Instanzen von der benötigten Namenskontexte und zum Verteilen von den Clients und schließlich die Belastung der einzelnen LDAP-Server zu reduzieren.  
  


