---
ms.assetid: 68db7f26-d6e3-4e67-859b-80f352e6ab6a
title: Rolle der AD FS-Konfigurationsdatenbank
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3372e1f051ba7f900753a4961d948ddabdef6f4d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867621"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-the-ad-fs-configuration-database"></a>Rolle der AD FS-Konfigurationsdatenbank
Die AD FS-Konfigurationsdatenbank speichert alle Konfigurationsdaten, die eine einzelne Instanz von Active Directory Federation Services stellt \(AD FS\) \(d. h. den Verbunddienst\). In der AD FS-Konfigurationsdatenbank sind die Parameter definiert, die für einen Verbunddienst benötigt werden, um Partner, Zertifikate, Attributspeicher, Ansprüche und verschiedene Daten zu diesen zugeordneten Entitäten zu identifizieren. Sie können diese Konfigurationsdaten in einer Datenbank Microsoft SQL Server® oder der internen Windows-Datenbank speichern \(WID\) -Funktion, die mit Windows Server® 2008, Windows Server 2008 R2 und Windows Server® 2012 enthalten ist.  
  
> [!NOTE]  
> Sämtliche Inhalte der AD FS-Konfigurationsdatenbank können entweder in einer Instanz der internen Windows-Datenbank oder in einer Instanz der SQL-Datenbank gespeichert werden, jedoch nicht in beiden. Das bedeutet, Sie können nicht über einige Verbundserver verfügen, die die interne Windows-Datenbank verwenden, während andere Verbundserver eine SQL Server-Datenbank für dieselbe Instanz der AD FS-Konfigurationsdatenbank verwenden.  
  
Weitere Informationen zu den Vor- und Nachteilen bei der Wahl zwischen interner Windows-Datenbank oder SQL Server zum Speichern der AD FS-Konfigurationsdatenbank erhalten Sie in den folgenden Informationen in diesem Abschnitt sowie in den unter [Überlegungen zur AD FS-Bereitstellungstopologie](https://technet.microsoft.com/library/gg982489.aspx) bereitgestellten Inhalten:  
  
WID verwendet einen relationalen Datenspeicher und verfügt nicht über eine eigene Benutzeroberfläche \(UI\). Stattdessen können Administratoren den Inhalt der AD FS-Konfigurationsdatenbank ändern, indem Sie mithilfe von entweder der AD FS-Verwaltungs-Snap\-in "," Fsconfig.exe, oder Windows PowerShell™-Cmdlets.  
  
## <a name="using-wid-to-store-the-ad-fs-configuration-database"></a>Verwenden der internen Windows-Datenbank zum Speichern der AD FS-Konfigurationsdatenbank  
Sie können die Verwendung von WID als Speicher mit AD FS-Konfigurationsdatenbank Befehls Fsconfig.exe erstellen\-Befehlszeilentool oder dem AD FS Konfigurations-Assistenten. Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen Ihrer Verbundservertopologie auswählen. Jede dieser Optionen verwendet die interne Windows-Datenbank zum Speichern der AD FS-Konfigurationsdatenbank:  
  
-   Erstellen Sie einen eigenständigen\-allein Verbundserver  
  
-   Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm  
  
Bei Auswahl von dem eigenständigen\-allein Option WID wird verwendet, um eine einzelne Instanz der AD FS-Konfigurationsdatenbank zu speichern. Diese Instanz kann nicht vom mehreren Verbundservern gemeinsam genutzt werden. Sie ist nur für Testumgebungen vorgesehen. Weitere Informationen zu dem eigenständigen\-allein verbundoption-Server oder eine einrichten, finden Sie unter [Stand-Alone Federation Server mit WID](https://technet.microsoft.com/library/gg982486.aspx) oder [Erstellen eines eigenständigen Verbundservers](https://technet.microsoft.com/library/ee913579.aspx).  
  
Wenn Sie den ersten Verbundserver einer Verbundserverfarmoption auswählen, wird die interne Windows-Datenbank für die Skalierbarkeit konfiguriert, die das spätere Hinzufügen zusätzlicher Verbundserver zur Farm gestattet. Weitere Informationen zum Bereitstellen oder Einrichten einer internen Windows-Datenbankfarm finden Sie unter [Verbundserverfarm mit WID](https://technet.microsoft.com/library/gg982492.aspx) oder [Erstellen des ersten Verbundservers in einer Verbundserverfarm](https://technet.microsoft.com/library/dd807070.aspx).  
  
Wenn Sie die Option zum Hinzufügen eines Verbundservers auswählen, wird die interne Windows-Datenbank für die Replikation der Konfigurationsdatenbankänderungen in festgelegten Intervallen auf dem neuen Verbundserver konfiguriert. Weitere Informationen zum Hinzufügen eines Verbundservers zu einer internen Windows-Datenbankfarm finden Sie unter [Verbundserverfarm mit WID](https://technet.microsoft.com/library/gg982492.aspx) oder [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](https://technet.microsoft.com/library/ee913575.aspx).  
  
> [!NOTE]  
> Bei der Bereitstellung einer Verbundserverfarm mit WID möglicherweise einige Funktionen von AD FS nicht verfügbar. Damit Sie beim Konfigurieren Ihrer Serverfarm Zugriff auf die vollständige Featuregruppe haben, erwägen Sie stattdessen die Verwendung von Microsoft SQL Server zum Speichern der AD FS-Konfigurationsdatenbank. Weitere Informationen finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](https://technet.microsoft.com/library/gg982489(v=ws.11).aspx).  
  
### <a name="how-a-wid-federation-server-farm-works"></a>Funktionsweise einer Verbundserverfarm mit internen Windows-Datenbanken  
In diesem Abschnitt werden wichtige Konzepte erläutert, die beschreiben, wie die Verbundserverfarm mit internen Windows-Datenbanken Daten zwischen einem primären Verbundserver und sekundären Verbundservern replizieren. .  
  
#### <a name="primary-federation-server"></a>Primärer Verbundserver  
Ein primärer Verbundserver ist ein Computer, die unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server® 2012 in der Verbundserver-Rolle mit der AD FS Konfigurations-Assistenten konfiguriert wurde und dessen, dass eine Lese-/Schreibkopie der AD FS die Konfigurationsdatenbank. Der primäre Verbundserver wird immer erstellt, wenn Sie die AD FS Konfigurations-Assistenten verwenden, und wählen Sie die Option zum Erstellen eines neuen Verbunddiensts und dem Computer des ersten Verbundservers in der Farm machen. Alle anderen Verbundserver in dieser Farm, die auch als sekundäre Verbundserver bezeichnet werden, müssen die am primären Verbundserver vorgenommenen Änderungen mit einer Kopie der AD FS-Konfigurationsdatenbank synchronisieren, die lokal gespeichert wird.  
  
#### <a name="secondary-federation-servers"></a>Sekundäre Verbundserver  
Sekundäre Verbundserver eine Kopie der AD FS-Konfigurationsdatenbank aus dem primären Verbundserver speichern, aber diese Kopien werden gelesen,\-nur. Sekundäre Verbundserver stellen eine Verbindung zum primären Verbundserver in der Farm her und führen eine Synchronisierung durch, indem sie den Server in regelmäßigen Intervallen abfragen, um auf geänderte Daten zu prüfen. Die sekundären Verbundserver sind vorhanden, um Fehlertoleranz für den primären Verbundserver während agieren laden\-Ausgleichen der Anforderungen, die an verschiedenen Standorten in Ihrer Netzwerkumgebung vorgenommen werden.  
  
> [!NOTE]  
> Wenn ein primärer Verbundserver abstürzt und offline ist, werden Anforderungen weiterhin von allen sekundären Verbundservern verarbeitet. Es können jedoch keine neuen Änderungen am Verbunddienst vorgenommen werden, bis der primäre Verbundserver wieder online ist. Sie können mithilfe von Windows PowerShell auch einen sekundären Verbundserver als neuen primären Verbundserver festlegen. Weitere Informationen finden Sie unter den [AD FS-Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
#### <a name="how-the-adfs-configuration-database-is-synchronized"></a>Synchronisieren der AD FS-Konfigurationsdatenbank  
Aufgrund der wichtige Rolle, die die AD FS-Konfigurationsdatenbank spielt es für verfügbar gemacht wird auf allen Verbundservern im Netzwerk Bereitstellen von Fehlertoleranz und den\-integrierten Funktionen, bei der Verarbeitung von Anforderungen \(bei Netzwerklast\-werden Lastenausgleichsmodule verwendet\). Die auf dem primären Verbundserver gespeicherte AD FS-Konfigurationsdatenbank muss jedoch synchronisiert werden, damit die sekundären Verbundserver diese Aufgabe übernehmen können.  
  
Wenn Sie einen Verbundserver zur Farm hinzufügen, stellt der neue Computer, der zu einem sekundären Verbundserver wird, eine Verbindung zum primären Verbundserver her, um die Kopie der AD FS-Konfigurationsdatenbank zu replizieren. Von diesem Punkt an ruft der neue Verbundserver regelmäßig Aktualisierungen vom primären Verbundserver ab, wie in der folgenden Abbildung veranschaulicht.  
  
![AD FS-Rollen](media/adfs2_WID.png)  
  
Jeder sekundäre Verbundserver prüft den primären Verbundserver alle fünf Minuten auf Änderungen. Sie können diese Standardeinstellung fünf anpassen\-minute Wert oder eine sofortige Synchronisierung mithilfe eines Windows PowerShell-Cmdlets jederzeit erzwingen. Weitere Informationen hierzu finden Sie unter [AD FS-Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
Der Synchronisierungsprozess der internen Windows-Datenbank unterstützt auch inkrementelle Übertragungen, um zwischenzeitliche Änderungen effizienter zu übertragen. Der inkrementelle Übertragungsprozess erzeugt erheblich weniger Datenverkehr im Netzwerk und die Übertragungen sind dadurch wesentlich schneller abgeschlossen.  
  
> [!NOTE]  
> Die Migration einer AD FS-Konfigurationsdatenbank aus einer internen Windows-Datenbank zu einer Instanz von SQL Server wird unterstützt. Weitere Informationen hierzu finden Sie unter [AD FS: Migrieren der AD FS-Konfigurationsdatenbank zu SQL Server](https://go.microsoft.com/fwlink/?LinkId=192232) auf der TechNet-Wiki-Website.  
  
## <a name="using-sql-server-to-store-the-ad-fs-configuration-database"></a>Verwenden von SQL Server zum Speichern der AD FS-Konfigurationsdatenbank  
Sie können die AD FS-Konfigurationsdatenbank verwenden eine einzelne SQL Server-Datenbankinstanz als Speicher mithilfe des Befehls Fsconfig.exe erstellen\-Tools "Linie". Die Verwendung einer SQL Server-Datenbank als AD FS-Konfigurationsdatenbank bietet gegenüber der internen Windows-Datenbank die folgenden Vorteile:  
  
-   Administratoren können die Features für hohe Verfügbarkeit von SQL Server nutzen.  
  
-   Sie bietet zusätzliche Leistungssteigerungen bei hohem Datenverkehr.  
  
-   Es bietet die featureunterstützung der SAML-artefaktauflösung und SAML/WS-\-Erkennung einer tokenmehrfachverwendung Verbund \(unten beschriebenen\).  
  
Der Begriff "primärer Verbundserver" trifft nicht zu, wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbankinstanz gespeichert wird, da alle Verbundserver gleichermaßen aus der AD FS-Konfigurationsdatenbank lesen bzw. in diese schreiben können, die dieselbe SQL Server-Clusterinstanz verwendet, wie in der folgenden Abbildung veranschaulicht.  
  
![AD FS-Rollen](media/adfs2_SQL.png)  
  
Sie können SQL Server verwenden, konfigurieren Sie zwei oder mehr Servern Zusammenarbeit als Servercluster um sicherzustellen, dass AD FS eingehender Clientanforderungen eine hohe Verfügbarkeit erfolgt. Hohe Verfügbarkeit bietet eine Skala\-Architektur, in dem Sie Serverkapazität durch Hinzufügen zusätzlicher Server erhöhen können. Einzelne Fehlerquellen werden durch automatische Clusterfailover verringert.  
  
Sie erreichen hochverfügbarkeit mithilfe der Netzwerk-Load\-Lastenausgleich und Failover-Dienste, die SQL-Clustertechnologie bereitgestellt. Weitere Informationen zum Konfigurieren von SQL Server für hohe Verfügbarkeit finden Sie unter [Übersicht über Lösungen von hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853).  
  
### <a name="saml-artifact-resolution"></a>SAML-Artefaktauflösung  
Security Assertion Markup Language \(SAML\) artefaktauflösung ist eine Endpunkt-basierten seitens des SAML 2.0-Protokolls, die beschreibt, wie eine vertrauende Seite ein Token direkt von einem Anspruchsanbieter abrufen kann. In der ersten Phase des Auflösungsprozesses kontaktiert ein Browserclient einen Ressourcenverbundserver und stellt diesem ein Artefakt bereit. In der zweiten Phase wird das Artefakt von Ressourcenverbundservern zum Auflösen der Artefaktnachricht an die URL eines SAML-Artefaktendpunkts gesendet, der in einer Kontopartnerorganisation gehostet wird. In der letzten Phase sendet der Kontoverbundserver das Token im Namen des Browserclients an den Verbundserver.  
  
> [!NOTE]  
> Wenn Sie ein Administrator in einer Kontopartnerorganisation sind, stellen Sie sicher, zuweisen, oder binden ein SSL-Zertifikat mit einem Stammzertifikat eines Mitglieds von der Windows-Programm für Stammzertifikate untergeordnet ist, an die passiven Verbund-Website in IIS \( <ComputerName> \\Websites\\Default Web Site\\Adfs\\ls\) auf allen kontoverbundservern in der Farm. Dies ist wichtig, um zu verhindern, dass Ressourcenverbundserver das SSL-Zertifikat manuell zum Zertifikatspeicher für vertrauenswürdige Personen des lokalen Computers hinzufügen müssen. Zudem soll es verhindern, dass Sie das in Ihrer Organisation veröffentlichte Artefakt nicht auflösen können.  
  
### <a name="samlws---federation-token-replay-detection"></a>SAML/WS - Verbund-token-Replay-Erkennung  
Der Begriff *Tokenwiedergabe* bezieht sich auf den Vorgang, bei dem ein Browserclient in einer Kontopartnerorganisation versucht, dasselbe Token zu senden, das er von einem Kontoverbundserver mehrmals erhalten hat, um sich für einen Ressourcenverbundserver zu authentifizieren.  Dieser Vorgang tritt auf, wenn ein Benutzer auf die Schaltfläche **Zurück** seines Browsers klickt, um die Authentifizierungsseite erneut zu übermitteln.  
  
AD FS stellt das Feature *Tokenwiedergabeerkennung* bereit, mit dem mehrere Tokenanforderungen erkannt und verworfen werden können, die dasselbe Token verwenden. Wenn dieses Feature aktiviert ist, schützt der Erkennung einer tokenmehrfachverwendung die Integrität von authentifizierungsanforderungen sowohl WS\-Federation passive Profile und die SAML WebSSO-Profil, indem Sie sicherstellen, dass dasselbe Token niemals mehr als einmal verwendet wird. Dieses Feature sollte in Situationen aktiviert sein, in denen die Sicherheit eine wichtige Rolle spielt, z. B. bei der Verwendung von Kioskcomputern.  
  
Im Kioskbeispiel kann sich ein Benutzer bei allen Websites abmelden und ein böswilliger Benutzer später versuchen, den Browserverlauf zu verwenden, um die Verbundauthentifizierungsseite erneut zu übermitteln, die vom vorherigen Benutzer geladen wurde. Dieses Feature entschärft dieses Problem, indem zusätzliche Informationen zu den einzelnen erfolgreichen Authentifizierungen einer Kontopartnerorganisation gespeichert werden, um die nachfolgende Wiedergabe des Tokens zu erkennen und zu verhindern, dass mehrere Authentifizierungsversuche erfolgreich ausgeführt werden.  
  

