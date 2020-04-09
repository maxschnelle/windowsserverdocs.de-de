---
ms.assetid: 68db7f26-d6e3-4e67-859b-80f352e6ab6a
title: Rolle der AD FS-Konfigurationsdatenbank
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9ffdd1876e2dfbc044cebb65d7d6ef80880a64b8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860163"
---
# <a name="the-role-of-the-ad-fs-configuration-database"></a>Rolle der AD FS-Konfigurationsdatenbank
Die AD FS Konfigurations Datenbank speichert alle Konfigurationsdaten, die eine einzelne Instanz von Active Directory-Verbunddienste (AD FS) \(AD FS\) \(Verbunddienst\). In der AD FS-Konfigurationsdatenbank sind die Parameter definiert, die für einen Verbunddienst benötigt werden, um Partner, Zertifikate, Attributspeicher, Ansprüche und verschiedene Daten zu diesen zugeordneten Entitäten zu identifizieren. Sie können diese Konfigurationsdaten entweder in einer Microsoft SQL Server&reg;-Datenbank oder in der internen Windows-Datenbank \(wid\) Feature speichern, das in Windows Server&reg; 2008, Windows Server 2008 R2 und Windows Server&reg; 2012 enthalten ist.  
  
> [!NOTE]  
> Sämtliche Inhalte der AD FS-Konfigurationsdatenbank können entweder in einer Instanz der internen Windows-Datenbank oder in einer Instanz der SQL-Datenbank gespeichert werden, jedoch nicht in beiden. Das bedeutet, Sie können nicht über einige Verbundserver verfügen, die die interne Windows-Datenbank verwenden, während andere Verbundserver eine SQL Server-Datenbank für dieselbe Instanz der AD FS-Konfigurationsdatenbank verwenden.  
  
Weitere Informationen zu den Vor- und Nachteilen bei der Wahl zwischen interner Windows-Datenbank oder SQL Server zum Speichern der AD FS-Konfigurationsdatenbank erhalten Sie in den folgenden Informationen in diesem Abschnitt sowie in den unter [Überlegungen zur AD FS-Bereitstellungstopologie](https://technet.microsoft.com/library/gg982489.aspx) bereitgestellten Inhalten:  
  
WID verwendet einen relationalen Datenspeicher und verfügt nicht über eine eigene Verwaltungs Benutzeroberfläche \(UI-\). Stattdessen können Administratoren den Inhalt der AD FS Konfigurations Datenbank entweder mithilfe der AD FS Verwaltungs-Snap\-in, fsconfig. exe oder Windows PowerShell-&trade;-Cmdlets ändern.  
  
## <a name="using-wid-to-store-the-ad-fs-configuration-database"></a>Verwenden der internen Windows-Datenbank zum Speichern der AD FS-Konfigurationsdatenbank  
Sie können die AD FS Konfigurations Datenbank mithilfe von wid als Speicher erstellen, indem Sie entweder das\-Befehlszeilen Tool "fsconfig. exe" oder den Assistenten für die Konfiguration des AD FS-Verbund Servers verwenden. Wenn Sie eines dieser Tools verwenden, können Sie eine der folgenden Optionen zum Erstellen Ihrer Verbundservertopologie auswählen. Jede dieser Optionen verwendet die interne Windows-Datenbank zum Speichern der AD FS-Konfigurationsdatenbank:  
  
-   Erstellen eines eigenständigen\-Verbund Servers  
  
-   Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
-   Hinzufügen eines Verbundservers zu einer Verbundserverfarm  
  
Wenn Sie die Option eigenständige\-eigen auswählen, wird die Anwendung wid verwendet, um eine einzelne Instanz der AD FS Konfigurations Datenbank zu speichern. Diese Instanz kann nicht vom mehreren Verbundservern gemeinsam genutzt werden. Sie ist nur für Testumgebungen vorgesehen. Weitere Informationen zur Option eigenständiger Verbund Server (\-eigenständig) oder zum Einrichten eines eigenständigen Verbund Servers finden Sie unter [eigenständiger Verbund Server mit wid](https://technet.microsoft.com/library/gg982486.aspx) oder [Erstellen eines eigenständigen Verbund Servers](https://technet.microsoft.com/library/ee913579.aspx).  
  
Wenn Sie den ersten Verbundserver einer Verbundserverfarmoption auswählen, wird die interne Windows-Datenbank für die Skalierbarkeit konfiguriert, die das spätere Hinzufügen zusätzlicher Verbundserver zur Farm gestattet. Weitere Informationen zum Bereitstellen oder Einrichten einer internen Windows-Datenbankfarm finden Sie unter [Verbundserverfarm mit WID](https://technet.microsoft.com/library/gg982492.aspx) oder [Erstellen des ersten Verbundservers in einer Verbundserverfarm](https://technet.microsoft.com/library/dd807070.aspx).  
  
Wenn Sie die Option zum Hinzufügen eines Verbundservers auswählen, wird die interne Windows-Datenbank für die Replikation der Konfigurationsdatenbankänderungen in festgelegten Intervallen auf dem neuen Verbundserver konfiguriert. Weitere Informationen zum Hinzufügen eines Verbundservers zu einer internen Windows-Datenbankfarm finden Sie unter [Verbundserverfarm mit WID](https://technet.microsoft.com/library/gg982492.aspx) oder [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](https://technet.microsoft.com/library/ee913575.aspx).  
  
> [!NOTE]  
> Beim Bereitstellen einer Verbund Serverfarm mit wid sind einige Features von AD FS möglicherweise nicht verfügbar. Damit Sie beim Konfigurieren Ihrer Serverfarm Zugriff auf die vollständige Featuregruppe haben, erwägen Sie stattdessen die Verwendung von Microsoft SQL Server zum Speichern der AD FS-Konfigurationsdatenbank. Weitere Informationen finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](https://technet.microsoft.com/library/gg982489(v=ws.11).aspx).  
  
### <a name="how-a-wid-federation-server-farm-works"></a>Funktionsweise einer Verbundserverfarm mit internen Windows-Datenbanken  
In diesem Abschnitt werden wichtige Konzepte erläutert, die beschreiben, wie die Verbundserverfarm mit internen Windows-Datenbanken Daten zwischen einem primären Verbundserver und sekundären Verbundservern replizieren. .  
  
#### <a name="primary-federation-server"></a>Primärer Verbundserver  
Ein primärer Verbund Server ist ein Computer, auf dem Windows Server 2008, Windows Server 2008 R2 oder Windows Server&reg; 2012 ausgeführt wird, der in der Verbund Server Rolle mit dem Konfigurations-Assistenten für AD FS-Verbund Server konfiguriert wurde und der über eine Lese-/Schreibkopie der AD FS Konfigurations Datenbank verfügt. Der primäre Verbund Server wird immer erstellt, wenn Sie den Konfigurations-Assistenten für den AD FS-Verbund Server verwenden und die Option zum Erstellen eines neuen Verbunddienst auswählen und diesen Computer zum ersten Verbund Server in der Farm machen. Alle anderen Verbundserver in dieser Farm, die auch als sekundäre Verbundserver bezeichnet werden, müssen die am primären Verbundserver vorgenommenen Änderungen mit einer Kopie der AD FS-Konfigurationsdatenbank synchronisieren, die lokal gespeichert wird.  
  
#### <a name="secondary-federation-servers"></a>Sekundäre Verbundserver  
Sekundäre Verbund Server speichern eine Kopie der AD FS Konfigurations Datenbank vom primären Verbund Server, diese Kopien werden jedoch nur\-gelesen. Sekundäre Verbundserver stellen eine Verbindung zum primären Verbundserver in der Farm her und führen eine Synchronisierung durch, indem sie den Server in regelmäßigen Intervallen abfragen, um auf geänderte Daten zu prüfen. Die sekundären Verbund Server sind vorhanden, um Fehlertoleranz für den primären Verbund Server zu gewährleisten und gleichzeitig zu Lasten\-auszugleichen, die an verschiedenen Standorten in der gesamten Netzwerkumgebung vorgenommen werden.  
  
> [!NOTE]  
> Wenn ein primärer Verbundserver abstürzt und offline ist, werden Anforderungen weiterhin von allen sekundären Verbundservern verarbeitet. Es können jedoch keine neuen Änderungen am Verbunddienst vorgenommen werden, bis der primäre Verbundserver wieder online ist. Sie können mithilfe von Windows PowerShell auch einen sekundären Verbundserver als neuen primären Verbundserver festlegen. Weitere Informationen finden Sie unter [AD FS Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
#### <a name="how-the-adfs-configuration-database-is-synchronized"></a>Synchronisieren der AD FS-Konfigurationsdatenbank  
Aufgrund der wichtigen Rolle, die die AD FS-Konfigurations Datenbank spielt, wird Sie auf allen Verbund Servern im Netzwerk zur Verfügung gestellt, um Fehlertoleranz und Lasten\-Ausgleichs Funktionen bei der Verarbeitung von Anforderungen \(zu ermöglichen, wenn die Netzwerk Last\-Ausgleichs Module\)verwendet werden. Die auf dem primären Verbundserver gespeicherte AD FS-Konfigurationsdatenbank muss jedoch synchronisiert werden, damit die sekundären Verbundserver diese Aufgabe übernehmen können.  
  
Wenn Sie einen Verbundserver zur Farm hinzufügen, stellt der neue Computer, der zu einem sekundären Verbundserver wird, eine Verbindung zum primären Verbundserver her, um die Kopie der AD FS-Konfigurationsdatenbank zu replizieren. Von diesem Punkt an ruft der neue Verbundserver regelmäßig Aktualisierungen vom primären Verbundserver ab, wie in der folgenden Abbildung veranschaulicht.  
  
![Rollen AD FS](media/adfs2_WID.png)  
  
Jeder sekundäre Verbundserver prüft den primären Verbundserver alle fünf Minuten auf Änderungen. Mithilfe eines Windows PowerShell-Cmdlets können Sie diesen Standardwert von fünf\-Minuten anpassen oder eine sofortige Synchronisierung erzwingen. Weitere Informationen hierzu finden Sie unter [AD FS Verwaltung mit Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).  
  
Der Synchronisierungsprozess der internen Windows-Datenbank unterstützt auch inkrementelle Übertragungen, um zwischenzeitliche Änderungen effizienter zu übertragen. Der inkrementelle Übertragungsprozess erzeugt erheblich weniger Datenverkehr im Netzwerk und die Übertragungen sind dadurch wesentlich schneller abgeschlossen.  
  
> [!NOTE]  
> Die Migration einer AD FS-Konfigurationsdatenbank aus einer internen Windows-Datenbank zu einer Instanz von SQL Server wird unterstützt. Weitere Informationen hierzu finden Sie unter [AD FS: Migrieren Ihrer AD FS-Konfigurations Datenbank zu SQL Server](https://go.microsoft.com/fwlink/?LinkId=192232) auf der TechNet Wiki-Website.  
  
## <a name="using-sql-server-to-store-the-ad-fs-configuration-database"></a>Verwenden von SQL Server zum Speichern der AD FS-Konfigurationsdatenbank  
Sie können die AD FS Konfigurations Datenbank mithilfe einer einzelnen SQL Server Daten Bank Instanz als Speicher erstellen, indem Sie das\-Befehlszeilen Tool "fsconfig. exe" verwenden. Die Verwendung einer SQL Server-Datenbank als AD FS-Konfigurationsdatenbank bietet gegenüber der internen Windows-Datenbank die folgenden Vorteile:  
  
-   Administratoren können die Features für hohe Verfügbarkeit von SQL Server nutzen.  
  
-   Sie bietet zusätzliche Leistungssteigerungen bei hohem Datenverkehr.  
  
-   Es bietet Funktionen zur Unterstützung von SAML-artefaktauflösung und SAML/WS\-\(der Verbund Token-Wiedergabe, die unten\)beschrieben werden.  
  
Der Begriff "primärer Verbund Server" trifft nicht zu, wenn die AD FS Konfigurations Datenbank in einer SQL-Daten Bank Instanz gespeichert wird, da alle Verbund Server gleichermaßen Lese-und Schreibzugriff auf die AD FS Konfigurations Datenbank haben, die dieselbe gruppierte SQL Server Instanz verwendet, wie in der folgenden Abbildung dargestellt.  
  
![Rollen AD FS](media/adfs2_SQL.png)  
  
Sie können SQL Server verwenden, um zwei oder mehr Server so zu konfigurieren, dass Sie als Server Cluster zusammenarbeiten, um sicherzustellen, dass AD FS hoch verfügbar gemacht wird, um eingehende Client Anforderungen zu verarbeiten. Hohe Verfügbarkeit bietet eine Architektur mit horizontaler Skalierung\-Out, in der Sie die Serverkapazität durch Hinzufügen zusätzlicher Server erhöhen können. Einzelne Fehlerquellen werden durch automatische Clusterfailover verringert.  
  
Sie können Hochverfügbarkeit erreichen, indem Sie die Netzwerk Last\-Ausgleichs-und Failoverdienste verwenden, die SQL-Clustering-Technologien bereitstellen. Weitere Informationen zum Konfigurieren von SQL Server für Hochverfügbarkeit finden Sie unter [Übersicht über Lösungen mit hoher verfüg](https://go.microsoft.com/fwlink/?LinkId=179853)barkeit.  
  
### <a name="saml-artifact-resolution"></a>SAML-Artefaktauflösung  
Security Assertion Markup Language \(SAML-\) artefaktauflösung ist ein Endpunkt, der auf dem Teil des SAML 2,0-Protokolls basiert und beschreibt, wie eine vertrauende Seite ein Token direkt von einem Anspruchs Anbieter abrufen kann. In der ersten Phase des Auflösungsprozesses kontaktiert ein Browserclient einen Ressourcenverbundserver und stellt diesem ein Artefakt bereit. In der zweiten Phase wird das Artefakt von Ressourcenverbundservern zum Auflösen der Artefaktnachricht an die URL eines SAML-Artefaktendpunkts gesendet, der in einer Kontopartnerorganisation gehostet wird. In der letzten Phase sendet der Kontoverbundserver das Token im Namen des Browserclients an den Verbundserver.  
  
> [!NOTE]  
> Wenn Sie Administrator in einer Konto Partnerorganisation sind, stellen Sie sicher, dass Sie ein SSL-Zertifikat, das mit einem Stamm Zertifikat eines Mitglieds des Windows-Programms für Stamm Zertifikate verkettet ist, der passiven Website in IIS \(<ComputerName>\\Sites\\Standard Website\\\\ls\) auf allen Konto Verbund Servern in der Farm zuweisen oder binden. Dies ist wichtig, um zu verhindern, dass Ressourcenverbundserver das SSL-Zertifikat manuell zum Zertifikatspeicher für vertrauenswürdige Personen des lokalen Computers hinzufügen müssen. Zudem soll es verhindern, dass Sie das in Ihrer Organisation veröffentlichte Artefakt nicht auflösen können.  
  
### <a name="samlws---federation-token-replay-detection"></a>Wiedergabe Erkennung für SAML/WS-Verbund Token  
Der Begriff *Tokenwiedergabe* bezieht sich auf den Vorgang, bei dem ein Browserclient in einer Kontopartnerorganisation versucht, dasselbe Token zu senden, das er von einem Kontoverbundserver mehrmals erhalten hat, um sich für einen Ressourcenverbundserver zu authentifizieren.  Dieser Vorgang tritt auf, wenn ein Benutzer auf die Schaltfläche **zurück** des Browsers klickt, um die Authentifizierungsseite erneut zu übermitteln.  
  
AD FS stellt das Feature *Tokenwiedergabeerkennung* bereit, mit dem mehrere Tokenanforderungen erkannt und verworfen werden können, die dasselbe Token verwenden. Wenn diese Funktion aktiviert ist, schützt die tokenwiedergabe-Erkennung die Integrität der Authentifizierungsanforderungen sowohl im passiven Profil des WS\--Verbunds als auch im SAML-WebSSO-Profil, indem sichergestellt wird, dass das gleiche Token nie mehrmals verwendet wird. Dieses Feature sollte in Situationen aktiviert sein, in denen die Sicherheit eine wichtige Rolle spielt, z. B. bei der Verwendung von Kioskcomputern.  
  
Im Kioskbeispiel kann sich ein Benutzer bei allen Websites abmelden und ein böswilliger Benutzer später versuchen, den Browserverlauf zu verwenden, um die Verbundauthentifizierungsseite erneut zu übermitteln, die vom vorherigen Benutzer geladen wurde. Diese Funktion mindert dieses Problem, indem zusätzliche Informationen zu jeder erfolgreichen Authentifizierung von einer Konto Partnerorganisation gespeichert werden, um nachfolgende Wiederholungen des Tokens zu erkennen und zu verhindern, dass mehrere Authentifizierungs Versuche erfolgreich durchgeführt werden.  
  

