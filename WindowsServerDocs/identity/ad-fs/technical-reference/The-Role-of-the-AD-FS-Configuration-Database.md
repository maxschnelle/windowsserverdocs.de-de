---
ms.assetid: 68db7f26-d6e3-4e67-859b-80f352e6ab6a
title: Die Rolle des AD FS-Konfigurationsdatenbank
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3372e1f051ba7f900753a4961d948ddabdef6f4d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-the-ad-fs-configuration-database"></a>Die Rolle des AD FS-Konfigurationsdatenbank
Die AD FS-Konfigurationsdatenbank speichert alle Konfigurationsdaten, die eine einzelne Instanz von Active Directory Federation Services \(AD FS\) \(that is, the Federation Service\) darstellt. Die AD FS-Konfigurationsdatenbank definiert den Satz von Parametern, die einen Verbunddienst benötigt, um Partner, Zertifikate, Attributspeicher, Ansprüche und verschiedene Daten zu diesen zugeordneten Entitäten zu identifizieren. Sie können diese Konfigurationsdaten speichern, in einer Datenbank Microsoft SQL Server® oder die Windows Internal Database \(WID\)-Funktion, die mit Windows Server® 2008, Windows Server2008 R2 und Windows Server® 2012 enthalten ist.  
  
> [!NOTE]  
> Der gesamte Inhalt der AD FS-Konfigurationsdatenbank können entweder in einer Instanz der internen Windows-Datenbank oder in einer Instanz der SQL-Datenbank gespeichert, aber nicht beides sein. Dies bedeutet, dass Sie einige Verbundserver mit WID und andere Benutzer zu einer SQL Server-Datenbank für dieselbe Instanz der AD FS-Konfigurationsdatenbank haben können.  
  
Sie können die folgende Informationen in diesem Thema sowie die Inhalte [Überlegungen zur AD FS-Bereitstellungstopologie](https://technet.microsoft.com/library/gg982489.aspx) Informationen zu den vor- und Nachteile der entweder WID oder SQL Server zum Speichern der AD FS-Konfigurationsdatenbank auswählen:  
  
Interne Windows-Datenbank verwendet einen relationalen Daten speichern und eine eigene Management-Benutzer verfügt nicht über die Schnittstelle \(UI\). Stattdessen können Administratoren den Inhalt der AD FS-Konfigurationsdatenbank mithilfe von AD FS-Verwaltung Snap\-in, Fsconfig.exe oder Windows PowerShell™ Cmdlets ändern.  
  
## <a name="using-wid-to-store-the-ad-fs-configuration-database"></a>Verwendung von WID zum Speichern der AD FS-Konfigurationsdatenbank  
Sie können die AD FS-Konfigurationsdatenbank mithilfe der internen Windows-Datenbank als Speicher Fsconfig.exe-Befehlszeilentools oder AD FS Federation Server-Konfigurations-Assistenten erstellen. Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen Ihrer Verbundservertopologie auswählen. Jede dieser Optionen verwendet interne Windows-Datenbank zum Speichern der AD FS-Konfigurationsdatenbank:  
  
-   Erstellen Sie einen eigenständige Verbundserver  
  
-   Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm  
  
Wenn Sie die eigenständige Option auswählen, wird WID verwendet, um eine einzelne Instanz der AD FS-Konfigurationsdatenbank speichern. Diese Instanz kann nicht vom mehreren Verbundservern gemeinsam genutzt werden. Hierbei handelt es sich für Testumgebungen nur. Weitere Informationen über die Option für eigenständige Federation Server oder zum Einrichten finden Sie unter [Stand-Alone Federation Server mit WID](https://technet.microsoft.com/library/gg982486.aspx) oder [Erstellen eines eigenständigen Verbundservers](https://technet.microsoft.com/library/ee913579.aspx).  
  
Wenn Sie den ersten Verbundserver in einer Federation Serverfarm-Option auswählen, wird WID für Skalierbarkeit konfiguriert, die zusätzliche Verbundserver der Farm zu einem späteren Zeitpunkt hinzugefügt werden, ermöglicht wird. Weitere Informationen zum Bereitstellen einer WID-Farm oder zum Einrichten finden Sie unter [Verbundserver mit WID](https://technet.microsoft.com/library/gg982492.aspx) oder [Erstellen des ersten Verbundservers in einer Verbundserverfarm](https://technet.microsoft.com/library/dd807070.aspx)  
  
Wenn Sie das Hinzufügen einer Federation Server-Option auswählen, wird WID so konfiguriert, dass um Configuration datenbankänderungen an der neuen Verbundserver in festgelegten Intervallen zu replizieren. Weitere Informationen zum Hinzufügen eines Verbundservers zu einer Windows-datenbankfarm finden Sie unter [Verbundserver mit WID](https://technet.microsoft.com/library/gg982492.aspx) oder [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](https://technet.microsoft.com/library/ee913575.aspx).  
  
> [!NOTE]  
> Bei der Bereitstellung einer Verbundserverfarm mit WID möglicherweise einige Funktionen von AD FS nicht verfügbar. Um den Zugriff auf die vollständige Featuregruppe, wenn Sie Ihrer Serverfarm konfigurieren, sollten Sie in Betracht ziehen, Microsoft SQL Server zum Speichern von der AD FS-Konfigurationsdatenbank stattdessen zu verwenden. Weitere Informationen finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](https://technet.microsoft.com/library/gg982489(v=ws.11).aspx).  
  
### <a name="how-a-wid-federation-server-farm-works"></a>Funktionsweise eine Verbundserverfarm  
Dieser Abschnittenthält wichtige Konzepte, die beschreiben, wie die Verbundserverfarm Daten zwischen einem primären Verbundserver und sekundären Verbundservern repliziert. .  
  
#### <a name="primary-federation-server"></a>Primärer Verbundserver  
Ein primärer Verbundserver ist ein Computer unter Windows Server2008, Windows Server2008 R2 oder Windows Server® 2012 in der Verbundserver-Rolle mit AD FS Federation Server-Konfigurations-Assistenten konfiguriert wurde und, das über eine Lese-/Schreibkopie der AD FS-Konfigurationsdatenbank verfügt. Der primäre Verbundserver wird immer erstellt, wenn Sie AD FS Federation Server-Konfigurations-Assistenten verwenden, und wählen Sie die Option zum Erstellen eines neuen Verbunddiensts und dem Computer des ersten Verbundservers in der Farm machen. Änderungen, die auf dem primären Verbundserver zu einer Kopie der AD FS-Konfigurationsdatenbank vorgenommen werden, die lokal gespeichert ist, müssen alle anderen Verbundserver in dieser Farm, auch bekannt als sekundäre Verbundserver synchronisieren.  
  
#### <a name="secondary-federation-servers"></a>Sekundäre Verbundserver  
Sekundäre Verbundserver speichern eine Kopie der AD FS-Konfigurationsdatenbank aus dem primären Verbundserver, aber diese Kopien sind schreibgeschützte. Sekundäre Verbundserver mit und synchronisiert die Daten des primären Verbundservers in der Farm Abfragen, in regelmäßigen Abständen zu überprüfen, ob Daten geändert wurden. Die sekundären Verbundserver vorhanden, um Fehlertoleranz für den primären Verbundserver berechtigen Load\ Lastenausgleich Zugriff Anfragen, die an verschiedenen Standorten in der gesamten Netzwerkumgebung vorgenommen werden.  
  
> [!NOTE]  
> Wenn ein primärer Verbundserver abstürzt und offline ist, weiterhin alle sekundären Verbundserver Anforderungen normal verarbeitet werden. Allerdings können keine neuen Änderungen an den Verbunddienst vorgenommen werden, bis der primäre Verbundserver wieder online geschaltet. Sie können auch einen sekundären Verbundserver der primäre Verbundserver wird mithilfe von Windows PowerShell benennen. Weitere Informationen finden Sie in der [AD FS-Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
#### <a name="how-the-ad-fs-configuration-database-is-synchronized"></a>Wie die AD FS-Konfigurationsdatenbank synchronisiert werden  
Aufgrund der wichtige Rolle, die die AD FS-Konfigurationsdatenbank wiedergibt, verfügbar gemacht auf allen Verbundservern im Netzwerk Bereitstellen von Fehlertoleranz und Lastenausgleich Load\ Funktionen beim Verarbeiten von Anforderungen \ (wenn die Netzwerk-Load\-Lastenausgleich Used\ sind). Für die sekundären Verbundserver diese Aufgabe übernehmen, muss die AD FS-Konfigurationsdatenbank, die auf dem primären Verbundserver gespeichert sind jedoch synchronisiert werden.  
  
Wenn Sie einen Verbundserver der Farm hinzufügen, verbindet sich der neue Computer, der als sekundäre Verbundserver wird an den primären Verbundserver die Kopie der AD FS-Konfigurationsdatenbank replizieren. Ab diesem Punkt weiterhin die neuen Verbundserver Updates abrufen, von dem primären Verbundserver in regelmäßigen Abständen, wie in der folgenden Abbildungdargestellt.  
  
![AD FS-Rollen](media/adfs2_WID.png)  
  
Jeder sekundäre Verbundserver prüft den primären Verbundserver alle fünf Minuten auf Änderungen. Sie können diesen Five\-Minuten-Standardwert anpassen oder eine sofortige Synchronisierung jederzeit erzwingen, mithilfe eines Windows PowerShell-Cmdlets. Weitere Informationen hierzu finden Sie unter [AD FS-Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
Der Synchronisierungsprozess der internen Windows-Datenbank unterstützt auch inkrementelle Übertragungen, um zwischenzeitliche Änderungen effizienter zu übertragen. Der inkrementelle Übertragungsprozess erzeugt erheblich weniger Datenverkehr im Netzwerk, und die Übertragungen sind dadurch wesentlich schneller abgeschlossen.  
  
> [!NOTE]  
> Die Migration von einem AD FS-Konfigurationsdatenbank von WID zu einer Instanz von SQL Server wird unterstützt. Weitere Informationen hierzu finden Sie unter [AD FS: Migrieren der AD FS-Konfigurationsdatenbank zu SQL Server](https://go.microsoft.com/fwlink/?LinkId=192232) auf der TechNet-Wiki-Website.  
  
## <a name="using-sql-server-to-store-the-ad-fs-configuration-database"></a>Mithilfe von SQL Server zum Speichern der AD FS-Konfigurationsdatenbank  
Sie können die AD FS-Konfigurationsdatenbank mithilfe einer einzelnen SQL Server-Datenbankinstanz als Speicher Fsconfig.exe-Befehlszeilentools erstellen. Mithilfe von SQL Server-Datenbank als AD FS-Konfigurationsdatenbank bietet die folgenden Vorteile gegenüber der internen Windows:  
  
-   Administratoren können die Funktionen für hohe Verfügbarkeit von SQL Server nutzen.  
  
-   Es bietet zusätzliche Leistungssteigerungen bei hohem Datenverkehr.  
  
-   Es enthält die Feature-Unterstützung des SAML-Artefaktauflösung und SAML/WS-Federation tokenwiederholungen Erkennung \(described below\).  
  
Der Begriff "primärer Verbundserver" trifft nicht, wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbankinstanz gespeichert ist, da alle Verbundserver gleichermaßen lesen und Schreiben mit der AD FS-Konfigurationsdatenbank, die den gleiche gruppierte SQL Server-Instanz verwendet wird, wie in der folgenden Abbildunggezeigt können.  
  
![AD FS-Rollen](media/adfs2_SQL.png)  
  
Sie können SQL Server verwenden, so konfigurieren Sie zwei oder mehr Servern für die Zusammenarbeit als Servercluster um sicherzustellen, dass AD FS für eingehende Clientanforderungen hoch verfügbar gemacht wird. Hoher Verfügbarkeit bietet eine Scale\ Out-Architektur, die in der Sie Serverkapazität durch Hinzufügen weiterer Server erhöhen können. Einzelne Fehlerquellen werden durch automatische Clusterfailover verringert.  
  
Erzielen Sie hohen Verfügbarkeit mithilfe des Load\-Netzwerklastenausgleich und Failover-Dienste, die SQL-Clustertechnologie bereitgestellt. Weitere Informationen zur Vorgehensweise beim Konfigurieren von SQL Server für hohe Verfügbarkeit finden Sie unter [Übersicht über Lösungen mit hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853).  
  
### <a name="saml-artifact-resolution"></a>SAML-Artefaktauflösung  
Security Assertion Markup Language \(SAML\) Artefaktauflösung ist ein Endpunkt basierten seitens des SAML 2.0-Protokolls, die beschreibt, wie eine vertrauende Seite ein Token direkt von einem Anspruchsanbieter abrufen kann. In der ersten Phase des Auflösungsprozesses ein Browserclient einen Ressourcenverbundserver kontaktiert und stellt diesem ein Artefakt bereit. In der zweiten Phase senden Ressourcenverbundserver das Artefakt zu einem SAML Artefakt-Endpunkt-URL, die irgendwo in einer Kontopartnerorganisation gehostet wird, um das Artefakt von ressourcenverbundservern zum Auflösen. In der letzten Phase sendet der Kontoverbundserver an den Verbundserver das Token im Namen des Browserclients an.  
  
> [!NOTE]  
> Wenn Sie ein Administrator in einer Kontopartnerorganisation sind, stellen Sie sicher zuweisen, oder binden ein SSL-Zertifikat mit einem Stammzertifikat eines Mitglieds der Windows-Programm für Stammzertifikate verknüpft ist, an der passiven Verbund-Website in IIS \ (<ComputerName>\\Sites\\Default WebSite\\adfs\\ls\) auf allen Konto Verbundservern in der Farm. Dies ist wichtig, zu verhindern, dass Ressourcenverbundserver das SSL-Zertifikat im Zertifikatspeicher des lokalen Computern vertrauenswürdige Personen manuell hinzufügen müssen oder nicht auf das Artefakt zu beheben, das in Ihrer Organisation veröffentlicht wird.  
  
### <a name="samlws---federation-token-replay-detection"></a>SAML/WS - Federation Erkennung von tokenwiederholungen  
Der Begriff *tokenwiederholungen* bezeichnet den Vorgang, mit dem ein Browserclient in einer Kontopartnerorganisation versucht, die sie von einem Kontoverbundserver mehrmals erhalten für dasselbe Token zur Authentifizierung an einen Ressourcenverbundserver zu senden.  Dieser Vorgang tritt auf, wenn ein Benutzer klickt auf die **wieder** Schaltfläche des Browsers zu die Authentifizierungsseite.  
  
AD FS bietet ein Feature, das so genannte *Token-Erkennung von tokenwiederholungen* dem mehrere tokenanforderungen mit dem gleichen Token kann erkannt und verworfen. Wenn dieses Feature aktiviert ist, schützt Erkennung von tokenwiederholungen die Integrität von Authentifizierungsanforderungen passiven WS-Federation-Profil und das SAML WebSSO-Profil, indem Sie sicherstellen, dass dasselbe Token niemals mehr als einmal verwendet wird. Diese Funktion muss aktiviert sein, in Situationen, in denen Sicherheit eine wichtige Rolle spielt wie z.B. bei Verwendung von Kiosks.  
  
Im kioskbeispiel kann sich ein Benutzer auf alle Websites anmelden, und später kann ein böswilliger Benutzer versuchen, auf den Browserverlauf zu verwenden, um die verbundauthentifizierungsseite, die vom vorherigen Benutzer geladen wurde. Dieses Feature entschärft dieses Problem, indem Sie zusätzliche Informationen zu den einzelnen erfolgreichen Authentifizierungen einer Kontopartnerorganisation um nachfolgende Wiedergabe des Tokens zu erkennen und zu verhindern, dass mehrere Authentifizierungsversuche erfolgreich zu speichern.  
  

