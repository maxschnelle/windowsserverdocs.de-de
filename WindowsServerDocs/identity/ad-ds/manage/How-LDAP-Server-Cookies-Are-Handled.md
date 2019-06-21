---
ms.assetid: 3acaa977-ed63-4e38-ac81-229908c47208
title: Behandlung von LDAP-Servercookies
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 873953155d22bafef5b042887b22e953ff580b5c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280568"
---
# <a name="how-ldap-server-cookies-are-handled"></a>Behandlung von LDAP-Servercookies

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In LDAP ergeben einige Abfragen einen großen Ergebnissatz. Solche Abfragen stellen Windows Server vor Herausforderungen.  
  
Die Erfassung und Zusammenstellung solcher großen Ergebnissätze bedeutet einen beträchtlichen Arbeitsaufwand. Viele Attribute müssen von einer internen Darstellung in die LDAP-Wire-Darstellung konvertiert werden. Einige Attribute müssen für den LDAP-Antwortframe auch von einem internen, meist binären Format in ein textbasiertes UTF-8-Format konvertiert werden.  
  
Eine weitere Herausforderung stellt die schiere Größe der Ergebnissätze dar. Ergebnissätze mit Zehntausenden von Objekten erreichen sehr schnell eine Größe von mehreren hundert Megabyte. Diese erfordern sehr viel virtuellen Adressraum, und auch die Übertragung über das Netzwerk kann problematisch werden, wenn die TCP-Sitzung während der Übertragung zusammenbricht.  
  
Diese Kapazität und Logistik brachten die Microsoft-LDAP-Entwickler geführt, erstellen eine LDAP-Erweiterung, die als "Seitenweisen Abfrage" bezeichnet. Diese Erweiterung implementiert ein LDAP-Steuerelement, das eine große Abfrage in mehrere Chunks kleinerer Ergebnissätze aufteilt. RFC-Standard geworden [RFC 2696](http://www.ietf.org/rfc/rfc2696).  
  
## <a name="cookie-handling-on-client"></a>Handhabung clientseitiger Cookies  
Methode der seitenweisen Abfrage verwendet die Seitengröße, legen Sie entweder vom Client oder über, eine [LDAP-Richtlinie](https://support.microsoft.com/kb/315071/en-us) ("MaxPageSize"). Der Client muss die Auslagerung durch die Übergabe eines LDAP-Steuerelements aktivieren.  

  
Eine Abfrage mit sehr vielen Ergebnissen gelangt irgendwann an einen Punkt, an dem die maximale Anzahl der zulässigen Objekte erreicht ist. Der LDAP-Server verpackt die Antwortnachricht und fügt ihr ein Cookie mit Informationen hinzu, die er später zur Fortsetzung der Suche benötigt.  
  
Die Clientanwendung muss das Cookie als nicht transparentes BLOB behandeln. Der Client kann die Anzahl der Objekte in der Antwort abrufen und die Suche mithilfe dieses Cookies fortsetzen. Dazu sendet er die Abfrage mit denselben Parametern (z. B. Basisobjekt und Filter) zurück an den LDAP-Server, wobei er den mit der vorherigen Antwort zurückgegebenen Cookiewert einfügt.  
  
Wenn die Anzahl der Objekte keine Seite füllt mehr, die LDAP-Abfrage abgeschlossen ist, und die Antwort enthält kein seitencookie. Wenn vom Server kein Cookie mehr zurückgegeben wird, kann der Client davon ausgehen, dass die seitenweise Suche erfolgreich abgeschlossen wurde.  
  
Wenn vom Server ein Fehler zurückgegeben wird, muss der Client davon ausgehen, dass die seitenweise Suche fehlgeschlagen ist. Eine Wiederholung der Suche führt dazu, dass die Suche erneut bei der ersten Seite beginnt.  
  
## <a name="server-side-cookie-handling"></a>Handhabung serverseitiger Cookies  
Windows Server gibt das Cookie an den Client zurück. Gelegentlich werden auf dem Server auch Informationen zum Cookie gespeichert. Diese Informationen werden in einem Server-Cache gespeichert, der bestimmten Einschränkungen unterliegt.  
  
Falls Informationen im Cache gespeichert werden, wird das vom Server an den Client gesendete Cookie auch vom Server zum Suchen der Informationen aus dem Server-Cache verwendet. Wenn der Client die seitenweise Suche fortsetzt, verwendet Windows Server das Clientcookie wie auch alle relevanten Informationen aus dem Cookiecache des Servers zum Fortsetzen der Suche. Findet der Server, aus welchem Grund auch immer, im Servercache keine relevanten Cookieinformationen, so wird die Suche abgebrochen und ein Fehler an den Client zurückgegeben.  
  
## <a name="how-the-cookie-pool-is-managed"></a>Verwaltung des Cookiepools  
Der LDAP-Server bedient mehrere Clients gleichzeitig und natürlich können auch mehrere Clients gleichzeitig Abfragen ausführen, die den Cookiecache des Servers beanspruchen. Aus diesem Grund wird die Cookiepoolauslastung vom Windows Server überwacht, wobei die Windows Server-Implementierung Grenzwerte vorsieht, um zu verhindern, dass der Cookiepool zu viele Ressourcen an sich zieht. Diese Grenzwerte können vom Administrator in der LDAP-Richtlinie mit den folgenden Einstellungen festgelegt werden. Nachfolgend sind die Standardwerte mit Erläuterungen angegeben:  
  
**MinResultSets: 4**  
  
Der LDAP-Server ignoriert die nachfolgend beschriebene maximale Poolgröße, wenn der Cookiecache weniger als MinResultSets-Einträge enthält.  
  
**MaxResultSetSize: 262.144 bytes**  
  
Die Gesamtgröße des Cookiecache auf dem Server darf  MaxResultSetSize in Bytes nicht überschreiten. Andernfalls werden Cookies beginnend beim ältesten Cookie gelöscht, bis die Größe des Pools wieder kleiner als MaxResultSetSize in Bytes ist oder sich im Pool weniger als MinResultSets Cookies befinden. Mit den Standardeinstellungen akzeptiert der LDAP-Server also einen Pool mit einer Größe von 450 KB, wenn der Pool nur 3 Cookies enthält.  
  
**MaxResultSetsPerConn: 10**  
  
Der LDAP-Server lässt im Pool nicht mehr als MaxResultSetsPerConn Cookies pro LDAP-Verbindung zu.  
  
## <a name="handling-deleted-cookies"></a>Handhabung gelöschter Cookies  
Das Entfernen von Cookie-Informationen aus dem Cache des LDAP-Servers führt nicht in jedem Fall sofort zu einem Anwendungsfehler. Vielmehr können die Anwendungen die seitenweise Suche von Beginn an neu starten und in einem weiteren Versuch erfolgreich zu Ende führen. Einige Anwendungen verfügen aus Stabilitätsgründen über diese Art von Wiederholungsmechanismus.  
  
Andere Anwendungen hingegen schließen eine seitenweise Suche eventuell nie ab. Dadurch können im Cookiecache des LDAP-Servers Einträge zurückbleiben, in welchem Fall der in Abschnitt 4 beschriebene Mechanismus zum Zuge kommt. Diese Behandlung ist wichtig, um den Speicherplatz des Servers wieder für aktive LDAP-Suchvorgänge freizugeben.  
  
Was passiert aber, wenn ein solches Cookie auf dem Server gelöscht wird und der Client die Suche mit diesem Cookiehandle fortsetzt? Der LDAP-Server findet das Cookie in diesem Fall nicht in seinem Cookiecache und gibt für die Abfrage eine Fehlermeldung wie die Folgende zurück:  
  
```  
00000057: LdapErr: DSID-xxxxxxxx, comment: Error processing control, data 0, v1db1  
```  
  
> [!NOTE]  
> Der Hexadezimalwert "DSID" variieren je nach Buildversion der Binärdateien des LDAP-Server.  
  
## <a name="reporting-on-the-cookie-pool"></a>Rückmeldungen über den Cookiepool  
Der LDAP-Server hat die Möglichkeit, Ereignisse über die Kategorie "16 Ldap Interface" Melden Sie sich in der [NTDS-Diagnoseschlüssel](https://support.microsoft.com/kb/314980/en-us). Wenn Sie diese Kategorie auf "2" festlegen, erhalten Sie die folgenden Ereignisse:  
  
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
  
Diese Ereignisse signalisieren, dass ein gespeichertes Cookie entfernt wurde. Es bedeutet nicht, dass der LDAP-Fehler bereits bis zu einem Client durchgedrungen ist, sondern lediglich, dass der LDAP-Server die vom Administrator festgelegten Grenzen für den Cache erreicht hat.  In einigen Fällen hat der LDAP-Client seine seitenweise Suche auch schon abgebrochen, so dass der Fehler bei ihm gar nicht in Erscheinung tritt.  
  
## <a name="monitoring-the-cookie-pool"></a>Überwachen des Cookiepools  
Wenn in Ihrer Domäne noch nie ein LDAP-Suchfehler aufgetreten ist, brauchen Sie den Cookiepool des LDAP-Servers für die seitenweise Suche gar nicht zu überwachen. Treten in Ihrer Umgebung hingegen Fehler in Verbindung mit der seitenweisen LDAP-Suche auf, liegt eventuell ein Problem mit den vom Administrator festgelegten Grenzen für den Cookiepool vor.  
  
Die Ereignisse 2898 und 2899 sind der einzige sichere Hinweis darauf, dass der LDAP-Server die Administratorgrenzen erreicht hat. Wenn Sie feststellen, dass LDAP-Abfragen aufgrund der oben aufgeführten Steuerverarbeitungsfehler fehlschlagen, sollten Sie je nach zurückgegebenem Ereignis die Grenzwerte der in Abschnitt 4 beschriebenen LDAP-Richtlinieneinstellungen heraufsetzen.  
  
Erhalten Sie auf Ihrem DC/LDAP-Server Ereignis 2898, empfiehlt sich eine Erhöhung von MaxResultSetsPerConn auf 25. Mehr als 25 parallel ausgeführte seitenweise Suchen über eine einzige LDAP-Verbindung sind ungewöhnlich. Falls Sie Ereignis 2898 weiterhin erhalten, sollten Sie die LDAP-Clientanwendung überprüfen, in der der Fehler auftritt. In diesem Fall liegt es nahe, dass die Anwendung beim Abrufen weiterer seitenweiser Ergebnisse hängen bleibt, das Cookie daraufhin im Status „Ausstehend“ belässt und eine neue Abfrage startet. Um festzustellen, ob der Anwendung an einem bestimmten Punkt für ihre Zwecke ausreichend Cookies zur Verfügung stehen, können Sie MaxResultSetsPerConn auch auf einen höheren Wert als 25 einstellen. Werden Ihren Domänencontrollern hingegen 2899-Ereignisse zurückgegeben, sähe die Strategie anders aus. Läuft Ihr DC/LDAP-Server in diesem Fall auf einem Computer mit ausreichend Arbeitsspeicher (d. h. es sind mehrere GB Arbeitsspeicher frei), sollten Sie MaxResultsetSize auf dem LDAP-Server auf einen Wert größer oder gleich 250 MB setzen. Dieser Grenzwert ist auch für große Mengen umfangreicher seitenweiser LDAP-Suchen auch in sehr großen Verzeichnissen mehr als ausreichend.  
  
Wenn Sie bei einem Pool mit dieser Größe nach wie vor 2899-Ereignisse erhalten, ist zu vermuten, dass auf dicht aufeinander folgende Abfragen sehr vieler Clients große Mengen an Objekten in kürzester Folge zurückgegeben werden. Die Daten, die Sie sammeln können, mit der [Active Directory Data Collector Set](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx) Hilfe finden Sie wiederholte seitenweise Abfragen, die Ihre LDAP-Server können gebucht werden. Diese Abfragen werden alle mit einer Anzahl von "zurückgegebenen Einträge" angezeigt, die die Größe der verwendeten Seite entspricht.  
  
Wenn möglich, sollten Sie das Anwendungsdesign überprüfen und implementieren einen anderen Ansatz mit einer niedrigeren Häufigkeit, Datenvolumen und/oder weniger Clientinstanzen, die die Abfrage dieser Daten. Bei den Anwendungen, die für die Sie Zugriff auf den Quellcode, dieses Handbuchs haben [effiziente AD-Enabled anwendungserstellung](https://msdn.microsoft.com/library/ms808539.aspx) ermöglicht Ihnen die optimale Methode zugreifen AD-Anwendungen zu verstehen.  
  
Wenn das Abfrageverhalten kann nicht geändert werden, wird ein Ansatz auch hinzugefügt mehr replizierte Instanzen der benötigten Namenskontexte und um die Clients verteilen und schließlich reduzieren die Last auf den einzelnen LDAP-Servern.  
  


