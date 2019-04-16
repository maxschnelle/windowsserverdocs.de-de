---
title: "Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: fc2ec09c5b96b76229d532adc6a254c8108d8940
ms.sourcegitcommit: ac73f0f0dca04be731b928183bfdffc97d82c277
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="perform-initial-recovery"></a>Führen Sie erste wiederherstellen  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Dieser Abschnittenthält die folgenden Schritteaus:  
  
-   [Stellen Sie den ersten beschreibbaren Domänencontroller in jeder Domäne wieder her.](#Restore-the-first-writeable-domain-controller-in-each-domain)  

-   [Schließen Sie jeden wiederhergestellten beschreibbaren Domänencontroller mit dem Netzwerk](#Reconnect-each-restored-writeable-domain-controller-to-a-common-network)  
  
-   [Hinzufügen des globalen Katalogs zu einem Domänencontroller in der Gesamtstruktur-Stammdomäne](#Add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain)  
  
  
## <a name="restore-the-first-writeable-domain-controller-in-each-domain"></a>Stellen Sie den ersten beschreibbaren Domänencontroller in jeder Domäne wieder her.  
 Beginnen mit einem beschreibbaren Domänencontroller in der Gesamtstruktur-Stammdomäne, führen Sie die Schrittein diesem Abschnittzum Wiederherstellen des ersten Domänencontrollers. Gesamtstruktur-Stammdomäne ist wichtig, da die Gruppen Schema-Admins und Organisations-Admins gespeichert. Darüber hinaus unterstützt die Vertrauenshierarchie in der Gesamtstruktur zu verwalten. Darüber hinaus enthält die Gesamtstruktur-Stammdomäne in der Regel die Stamm-DNS-Server für die Gesamtstruktur-DNS-Namespace. Daher enthält die Active Directory-integrierte DNS-Zone für diese Domäne den Alias (CNAME)-Ressourceneinträge für alle anderen Domänencontroller in der Gesamtstruktur (die für die Replikation erforderlich sind) und die DNS-Ressourceneinträge des globalen Katalogs.  
  
 Nachdem Sie die Gesamtstruktur-Stammdomäne wiederherstellen, wiederholen Sie die gleichen Schritteaus, um die verbleibenden Domänen in der Gesamtstruktur wiederherzustellen. Sie können mehr als eine Domäne gleichzeitig wiederherzustellen. jedoch immer wiederherstellen Sie eine übergeordnete Domäne vor der Wiederherstellung ein untergeordnetes Element, um zu eine Unterbrechung der Vertrauenshierarchie oder DNS-Namensauflösung verhindern.  
  
 Stellen Sie für jede Domäne, die Sie wiederherstellen nur einen beschreibbaren Domänencontroller aus einer Sicherung wieder her. Dies ist der wichtigste Teil der Wiederherstellung, da der Domänencontroller eine Datenbank, die nicht verfügt über die Ursache der Gesamtstruktur beeinflusst wurden nicht benötigen. Es ist wichtig, eine vertrauenswürdige Sicherung verfügen, die gründlich getestet wird, bevor es in der Produktionsumgebung eingeführt wird.  
  
 Klicken Sie dann die folgenden Schritteausführen. Verfahren zum Ausführen bestimmter Schrittesind [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren ](AD-Forest-Recovery-Procedures.md).  
  
1.  Wenn Sie einen physischen Server wiederherstellen möchten, sicher, dass das Netzwerkkabel des Ziels DC angefügt ist und daher nicht für das Produktionsnetzwerk verbunden ist. Für eine virtuelle Maschine können Sie Entfernen des Netzwerkadapters oder verwenden einen Netzwerkadapter, der mit einem anderen Netzwerk verbunden ist, können Sie den Wiederherstellungsvorgang während vom Produktionsnetzwerk isoliert testen.  
  
2.  Da dies das erste beschreibbare Domänencontroller in der Domäne ist, müssen Sie eine nicht autoritative Wiederherstellung von AD DS und eine autorisierende Wiederherstellung von SYSVOL durchführen. Die Wiederherstellung mithilfe einer Active Directory-kompatiblen Sicherung abgeschlossen werden muss und Anwendung, z.B. Windows Server-Sicherung wiederherstellen (d.h., Sie sollten wiederherstellen den Domänencontroller mit nicht unterstützten Methoden wie z.B. eine VM-Momentaufnahme wiederherstellen).  
  
     Eine autorisierende Wiederherstellung von SYSVOL ist erforderlich, da die Replikation von SYSVOL repliziert, dass Ordner gestartet werden muss, wenn Sie nach einem Notfall wiederherstellen. Alle Domänencontroller, die in der Domäne hinzugefügt werden müssen den SYSVOL-Ordner mit einer Kopie des Ordners neu synchronisiert werden, die ausgewählt hat, um die autorisierende sein, bevor der Ordner angekündigt werden kann.  
  
    > [!CAUTION]
    >  Führen Sie eine autorisierende (oder primäre) Wiederherstellung von SYSVOL nur für den ersten Domänencontroller in der Gesamtstruktur-Stammdomäne wiederhergestellt werden. Falsch Vorgänge primäre Wiederherstellung von SYSVOL auf anderen Domänencontrollern führt zu Replikationskonflikten der SYSVOL-Daten.  
  
     Es gibt zwei Optionen führen Sie eine nicht autoritative Wiederherstellung von AD DS und eine autorisierende Wiederherstellung von SYSVOL:  
  
    -   Ausführen einer vollständigen Wiederherstellungs, und klicken Sie dann eine autoritative Synchronisierung von SYSVOL erzwingen. Ausführliche Informationen finden Sie [Ausführen einer vollständigen Wiederherstellungs](AD-Forest-Recovery-Perform-a-Full-Recovery.md) und [eine autoritative Synchronisierung von SYSVOL mit DFS-Replikation ausgeführt ](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).  
  
    -   Führen Sie eine vollständige Wiederherstellung des Servers eine Wiederherstellung des Systemstatus gefolgt. Diese Option ist erforderlich, dass Sie beide Arten der Sicherung im Voraus erstellen: einer vollständigen serversicherung und eine Sicherung des Systemstatus. Ausführliche Informationen finden Sie [Ausführen einer vollständigen Wiederherstellungs](AD-Forest-Recovery-Perform-a-Full-Recovery.md) und [eine nicht autoritative Wiederherstellung der Active Directory-Domänendienste ausführen ](AD-Forest-Recovery-Nonauthoritative-Restore.md).  
  
3.  Nach dem Wiederherstellen und starten Sie die beschreibbaren Domänencontroller neu, stellen Sie sicher, dass der Fehler keinen Einfluss auf die Daten auf dem Domänencontroller. Wenn die DC-Daten beschädigt ist, wiederholen Sie Schritt2 mit einer anderen Sicherung.  
  
     Wenn der wiederhergestellte Domänencontroller eine Betriebsmasterrolle hostet, müssen Sie möglicherweise den folgenden Registrierungseintrag zur Vermeidung von AD DS wird nicht verfügbar, bis zum Abschluss der Replikation für eine schreibbare Verzeichnispartition hinzufügen:  
  
     **HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Repl anfängliche Synchronisierung ausführen**  
  
     Erstellen Sie den Eintrag mit dem Datentyp **REG_DWORD** und einem Wert von **0**. Nachdem die Gesamtstruktur vollständig wiederhergestellt wird, können Sie den Wert für diesen Eintrag, um zurücksetzen **1**, die einen Domänencontroller erfordert, wird neu gestartet, und enthält Operations master Rollen haben erfolgreich, AD DS eingehende und ausgehende Replikation mit seinen Partnern bekannte Replikat, bevor sie sich selbst als Domänencontroller ankündigt und Bereitstellen von Diensten für Clients. Weitere Informationen zu den Anforderungen der ersten Synchronisierung, finden Sie im KB-Artikel [305476](https://support.microsoft.com/kb/305476).  
  
     Fahren Sie mit den nächsten Schrittennur nach dem Wiederherstellen und überprüfen Sie die Daten und bevor Sie diese Computer im Produktionsnetzwerk hinzugefügt.  
  
4.  Wenn Sie vermuten, dass der Fehler bei der Gesamtstruktur Angriffe auf das Netzwerk oder böswillige Angriffe verbunden war, Zurücksetzen der Kennwörter für alle Administratorkonten, einschließlich der Mitglieder der Organisations-Admins, Domänen-Admins, Schema-Admins, Server-Operatoren, Konten-Operatoren Gruppen usw. Das Zurücksetzen von Kennwörtern Administratorkonto sollte vor dem zusätzliche Domäne abgeschlossen werden, die während der nächsten Phase der Wiederherstellung der Gesamtstruktur installiert sind.  
  
5.  In der ersten wiederhergestellten Domänencontroller in der Gesamtstruktur-Stammdomäne Betriebsmasterrollen alle Domänen- und Gesamtstrukturebene. Organisations-Admins und Schema-Admins-Anmeldeinformationen sind erforderlich, um gesamtstrukturweite Betriebsmasterfunktionen.  
  
     Betriebsmasterrollen Sie in jeder Domäne untergeordnete domänenweite. Obwohl Sie die Betriebsmasterrollen auf dem wiederhergestellten Domänencontroller nur temporär beibehalten möglicherweise diese Rollen übernehmen sicher in Bezug auf die Domänencontroller werden an dieser Stelle in der Gesamtstruktur-Wiederherstellungsprozess hostet. Im Rahmen der nach der Wiederherstellung können Sie die Betriebsmasterrollen verteilen, je nach Bedarf. Weitere Informationen zum Übernehmen von Betriebsmasterrollen finden Sie unter [übernehmen eine Betriebsmasterfunktion](AD-forest-recovery-seizing-operations-master-role.md). Empfehlungen zum Platzieren von Betriebsmasterrollen, finden Sie unter [was die Betriebsmaster sind?](https://technet.microsoft.com/en-us/library/cc779716.aspx).  
  
6.  Bereinigen von Metadaten für alle anderen beschreibbaren Domänencontroller in der Stammdomäne der Gesamtstruktur, die Sie nicht aus einer Sicherung (alle beschreibbaren Domänencontroller in der Domäne mit Ausnahme dieses ersten DC) wiederherstellen. Wenn Sie die Version des Active Directory-Benutzer und -Computer oder Active Directory-Standorte und -Dienste, die bei Windows Server2008 oder höher enthalten ist oder Remoteserver-Verwaltungstools für Windows Vista oder höher, Metadatenbereinigung automatisch erfolgt, wenn ein DC-Objekt zu löschen. Darüber hinaus werden die Server und Computerobjekt für den gelöschten Domänencontroller ebenfalls automatisch gelöscht. Weitere Informationen finden Sie unter [Bereinigen von Metadaten beschreibbaren Domänencontroller entfernt](AD-Forest-Recovery-Cleaning-Metadata.md).  
  
     Mögliche Duplizierung der NTDS-Einstellungsobjekte Bereinigen von Metadaten verhindert werden, wenn AD DS auf einem Domänencontroller an einem anderen Standort installiert ist. Möglicherweise kann dies auch (Knowledge Consistency Checker, KCC) speichern, Replikationslinks erstellen, wenn der Domänencontroller sich möglicherweise nicht vorhanden. DC-Locator-DNS-Ressourceneinträgen für alle anderen Domänencontroller in der Domäne werden darüber hinaus als Teil des Metadatenbereinigung, von DNS gelöscht werden.  
  
     Bis die Metadaten für alle anderen Domänencontroller in der Domäne entfernt wird, diesen Domänencontroller wäre es ein RID-Master vor der Wiederherstellung, die RID-Masterrolle wird nicht davon ausgehen und aus diesem Grund werden neue RIDs ausstellen. Ereignis-ID 16650 im Systemprotokoll in der Ereignisanzeige angezeigt, die dieser Fehler wird möglicherweise angezeigt, aber Sie Ereignis-ID 16648 Erfolgsmeldung eine Weile, nachdem Sie die Metadaten bereinigt haben sollte angezeigt werden.  
  
7.  Wenn Sie DNS-Zonen, die in AD DS gespeichert sind verfügen, stellen Sie sicher, dass der lokale DNS-Serverdienst ist installiert und ausgeführt, auf dem Domänencontroller, die Sie wiederhergestellt haben. Wenn dieser Domänencontroller keinem DNS-Server vor dem Fehler Gesamtstruktur wurde, müssen Sie installieren und konfigurieren den DNS-Server.  
  
    > [!NOTE]
    >  Wenn der wiederhergestellte Domänencontroller mit Windows Server2008 ausgeführt wird, müssen Sie den Hotfix im KB-Artikel installieren [975654](https://support.microsoft.com/kb/975654) oder den Server vorübergehend mit einem isolierten Netzwerk verbinden um DNS-Server installieren. Das Update ist nicht für alle anderen Versionen von Windows Server erforderlich.  
  
     Konfigurieren Sie den wiederhergestellten Domänencontroller in der Gesamtstruktur-Stammdomäne mit seiner eigenen IP-Adresse (oder eine Loopback-Adresse, z.B. 127.0.0.1) als der bevorzugte DNS-Server. Sie können diese Einstellung in den TCP/IP-Eigenschaften des lokalen Netzwerks (LAN)-Adapters konfigurieren. Dies ist der erste DNS-Server in der Gesamtstruktur. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP für DNS](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx).  
  
     Konfigurieren Sie den wiederhergestellten Domänencontroller in untergeordneten Domänen mit der IP-Adresse des ersten DNS-Servers in der Gesamtstruktur-Stammdomäne als der bevorzugte DNS-Server. Sie können diese Einstellung in den TCP/IP-Eigenschaften des Netzwerkadapters konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP für DNS](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx).  
  
     Löschen Sie die "_msdcs" und der Domäne DNS-Zonen Namenservereinträge von Domänencontrollern, die nicht mehr nach Metadatenbereinigung vorhanden sind. Überprüfen Sie, ob der SRV-Einträge der Aufräumarbeiten Domänencontroller entfernt wurden. Führen Sie zum Beschleunigen von DNS SRV-Eintrag entfernen:  
  
    ```  
    nltest.exe /dsderegdns:server.domain.tld  
    ```  
  
8.  Erhöhen Sie den Wert des verfügbaren RID-Pools um 100.000. Weitere Informationen finden Sie unter [auslösen den Wert des verfügbaren RID-Pools](AD-Forest-Recovery-Raise-RID-Pool.md). Besitzen Sie Grund zu der Annahme, dass das Auslösen der RID-Pool durch 100.000 für Ihre spezifische Situation nicht ausreichend ist, sollten Sie die niedrigste Erhöhung ermitteln, die weiterhin sicher ist. RIDs sind eine begrenzte Ressource, die nicht unnötig verwendet werden soll.  
  
     Wenn neue Sicherheitsprinzipale in der Domäne nach dem Zeitpunkt der Sicherung, die Sie für die Wiederherstellung verwenden erstellt wurden, möglicherweise diese Sicherheitsprinzipale Zugriffsrechte auf bestimmte Objekte. Diese Sicherheitsprinzipale sind nach der Wiederherstellung nicht mehr vorhanden, da die Wiederherstellung der Sicherung wiederhergestellt wurde; Zugriffsrechte können jedoch immer noch vorhanden sein. Wenn der verfügbare RID-Pool nach der Wiederherstellung nicht ausgelöst wird, neue Benutzer Objekte enthält, die erstellt werden, nachdem die Wiederherstellung der Gesamtstruktur identische Sicherheits-IDs (SIDs) abrufen kann, und Sie werden möglicherweise Zugriff auf Objekte, die Sie nicht ursprünglich wurde.  
  
     Um dies zu veranschaulichen, betrachten Sie das Beispiel mit dem Namen Andrea, die in der Einführung erwähnt wurden neue Mitarbeiter aus. Das Benutzerobjekt für Amy ist nach dem Wiederherstellungsvorgang nicht mehr vorhanden, da sie nach der Sicherung erstellt wurde, die zum Wiederherstellen der Domänenbenutzers verwendet wurde. Allerdings können keine Zugriffsrechte, die die User-Objekt zugewiesen wurden, nach dem Wiederherstellungsvorgang beibehalten werden. Wenn die SID für dieses Benutzerobjekt nach der Wiederherstellung ein neues Objekt zugewiesen ist, würde das neue Objekt diese Zugriffsrechte erhalten.  
  
9. Den aktuellen RID-Pool wird ungültig. Der aktuelle RID-Pool wird ungültig gemacht, nachdem eine den Systemstatus wiederherstellen. Aber wenn eine Wiederherstellung des Systemstatus nicht ausgeführt wurde, muss der aktuelle RID-Pool ungültig gemacht werden, um zu verhindern, dass den wiederhergestellten Domänencontroller erneut RIDs ausstellen, von der RID-Pool, der bei der Erstellung zugeordnet wurde, für die Sicherung erstellt wurde. Weitere Informationen finden Sie unter [den aktuellen RID-Pool ungültig](AD-Forest-Recovery-Invaildate-RID-Pool.md).  
  
    > [!NOTE]
    >  Beim ersten, die Sie versuchen, ein Objekt mit einer SID erstellen, nachdem Sie den RID-Pool ungültig erhalten Sie einen Fehler. Der Versuch, ein Objekt zu erstellen, wird eine Anforderung für eine neue RID-Pool ausgelöst. Wiederholung des Vorgangs erfolgreich ist, da der neue RID-Pool zugeordnet werden kann.  
  
10. Das Kennwort des Computerkontos von diesem Domänencontroller zweimal zurückgesetzt. Weitere Informationen finden Sie unter [Zurücksetzen des Kennworts für das Computerkonto des Domänencontrollers](AD-Forest-Recovery-Reset-Computer-Account-DC.md).  
  
11. Setzen Sie das Krbtgt-Kennwort zweimal zurück. Weitere Informationen finden Sie unter [Zurücksetzen des Krbtgt-Kennworts](AD-Forest-Recovery-Resetting-the-krbtgt-password.md).  
  
     Da die Kennwortchronik Krbtgt zwei Kennwörter ist, Zurücksetzen von Kennwörtern zweimal, um das ursprüngliche (Prefailure) Kennwort aus Kennwortchronik zu entfernen.  
  
    > [!NOTE]
    >  Ist die Wiederherstellung der Gesamtstruktur in Reaktion auf eine sicherheitsverletzung, können Sie auch die Kennwörter zurücksetzen. Weitere Informationen finden Sie unter [Zurücksetzen des Kennworts Vertrauensstellung auf einer Seite der Vertrauensstellung](AD-Forest-Recovery-Reset-Trust.md).  
  
12. Wenn die Gesamtstruktur verfügt über mehrere Domänen und der wiederhergestellte Domänencontroller ein globaler Katalogserver vor Auftreten des Fehlers wurde, deaktivieren Sie die **globalen Katalog** Kontrollkästchen in den Eigenschaften des NTDS-Einstellungen des globalen Katalogs des Domänencontrollers zu entfernen. Die Ausnahme von dieser Regel wird üblicherweise eine Gesamtstruktur mit nur einer Domäne. In diesem Fall ist es nicht erforderlich, um den globalen Katalog zu entfernen. Weitere Informationen finden Sie unter [Entfernen des globalen Katalogs](AD-Forest-Recovery-Remove-GC.md).  
  
     Durch Wiederherstellen von einem globalen Katalog aus einer Sicherung, die weitere ist möglicherweise neuer sind als andere Sicherungen, die zum Wiederherstellen der Domänencontroller in anderen Domänen verwendet werden Sie veraltete Objekte einführen. Betrachten Sie das folgende Beispiel. In Domäne A wird DC1 aus einer Sicherung wiederhergestellt, die zum Zeitpunkt T1 durchgeführt wurde. In Domäne B wird DC2 aus einem globalen Katalog Sicherung wiederhergestellt, die zum Zeitpunkt T2 durchgeführt wurde. Angenommen Sie, T2 ist neuer als T1 und einige Objekte, die zwischen T1 und T2 erstellt wurden. Nachdem diese Domänencontroller wiederhergestellt werden, befinden sich DC2, also einen globalen Katalog neuere Daten für die Domäne des Teilreplikat als Domäne A enthält selbst. DC2 enthält veraltete Objekte in diesem Fall, da diese Objekte nicht auf DC1 vorhanden sind.  
  
     Das Vorhandensein von veralteten Objekten kann zu Problemen führen. E-Mail-Nachrichten können beispielsweise nicht für einen Benutzer übermittelt werden, dessen Benutzerobjekt zwischen Domänen verschoben wurde. Nachdem Sie den veralteten Domänencontroller oder globalen Katalogserver wieder online schalten, werden beide Instanzen des Benutzerobjekts in den globalen Katalog angezeigt. Beide Objekte haben die gleiche E-Mail-Adresse. Daher können die E-Mail-Nachrichten zugestellt werden.  
  
     Ein zweites Problem ist, dass ein Benutzerkonto, das nicht mehr vorhanden ist noch in der globalen Adressliste angezeigt werden kann. Eine dritte ist eine universelle Gruppe, die nicht mehr vorhanden ist immer noch im Zugriffstoken des Benutzers angezeigt werden kann.  
  
     Wenn Sie einen Domänencontroller wiederhergestellt wurden, die einen globalen Katalog wurde – entweder versehentlich oder weil die einsame Sicherung, die Sie als vertrauenswürdig eingestuft wurde – es wird empfohlen, dass Sie verhindern, das auftreten dass von veralteten Objekten durch die Deaktivierung des globalen Katalogs, sobald die Wiederherstellung abgeschlossen ist. Deaktivieren das Flag für den globalen Katalog führt der Computer verloren gehen alle seine Teilreplikate (Partitionen) und die Verbannung selbst regulären DC-Status.  
  
13. Konfigurieren Sie Windows-Zeitdienst. Konfigurieren Sie in der Stammdomäne der Gesamtstruktur den PDC-Emulator, um die Zeit mit einer externen Zeitquelle synchronisieren. Weitere Informationen finden Sie unter [konfigurieren den Windows-Zeitdienst auf dem PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).  
  
 

## <a name="reconnect-each-restored-writeable-domain-controller-to-a-common-network"></a>Schließen Sie jeden wiederhergestellten beschreibbaren Domänencontroller mit einem gemeinsamen Netzwerk  
 An diesem Punkt sollten Sie einen Domänencontroller wiederhergestellt (und Schrittezur Wiederherstellung ausgeführt) in der Gesamtstruktur-Stammdomäne und in jedem der verbleibenden Domänen verfügen. Treten Sie diese Domänencontroller mit einem gemeinsamen Netzwerk, das von der restlichen Umgebung isoliert ist, und gehen Sie folgendermaßen vor, um die Integrität der Gesamtstruktur und die Replikation zu überprüfen.  
  
> [!NOTE]
>  Wenn Sie die physischen Domänencontroller mit einem isolierten Netzwerk verbinden, müssen Sie möglicherweise ihre IP-Adressen zu ändern. Die IP-Adressen von DNS-Einträgen werden daher falsch sein. Da ein globaler Katalogserver nicht verfügbar ist, tritt ein sichere dynamische Updates für DNS. Virtuelle DCs sind in diesem Fall mehr vorteilhaft, da sie auf ein neues virtuelles Netzwerk hinzugefügt werden können, ohne die IP-Adressen zu ändern. Dies ist ein Grund, warum virtuelle Domänencontroller als ersten Domänencontroller empfohlen werden, während der Wiederherstellung der Gesamtstruktur wiederhergestellt werden.  
  
 Beitreten Sie nach der Überprüfung der Domänencontroller zum Produktionsnetzwerk, und führen Sie die Schrittezum Überprüfen der Integrität der Gesamtstruktur Replikation.  
  
-   Um Namensauflösung zu beheben, erstellen Sie DNS-Delegierungseinträge, und konfigurieren Sie DNS-Weiterleitung und Stamm Stammhinweisen nach Bedarf. Führen Sie **Repadmin/replsum** Replikation zwischen Domänencontrollern zu überprüfen.  
  
-   Wenn der wiederhergestellte Domänencontroller keine direkte Replikationspartner sind, werden Wiederherstellung der Replikation schneller durch das Erstellen von temporären Verbindungsobjekte zwischen ihnen.  
  
-   Um Metadatenbereinigung zu überprüfen, führen Sie **Repadmin /viewlist \ *** eine Liste mit allen Domänencontrollern in der Gesamtstruktur. Führen Sie **Nltest /DCList:***< Domäne\ >* eine Liste mit allen Domänencontrollern in der Domäne.  
  
-   Führen Sie zum Überprüfen der Integrität der Domänencontroller und DNS-DCDiag /v zum Melden von Fehlern auf alle Domänencontroller in der Gesamtstruktur.  
  
  

## <a name="add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain"></a>Hinzufügen des globalen Katalogs zu einem Domänencontroller in der Gesamtstruktur-Stammdomäne  
 Ein globaler Katalog ist für diesen und anderen Gründen erforderlich:  
  
-   Um die Anmeldung für Benutzer aktivieren.  
  
-   So aktivieren Sie den Anmeldedienst auf den Domänencontrollern in jeder untergeordneten Domäne registrieren, und entfernen Datensätze auf dem DNS-Server in der Stammdomäne.  
  
 Obwohl empfohlen wird, dass der Stamm der Gesamtstruktur Domänencontroller einen globalen Katalog werden, ist es möglich, wählen Sie eines der wiederhergestellten Domänencontroller zum globalen Katalog.  
  
> [!NOTE]
>  Domänencontroller wird nicht als globalen Katalogserver angekündigt werden, bis sie eine vollständige Synchronisierung aller Verzeichnispartitionen in der Gesamtstruktur abgeschlossen ist. Aus diesem Grund sollte der Domänencontroller gezwungen, die mit den wiederhergestellten Domänencontroller in der Gesamtstruktur repliziert werden.  
>   
>  Überwachen Sie das Verzeichnisdienst-Ereignisprotokoll in der Ereignisanzeige nach Ereignis-ID 1119, was darauf hindeutet, dass dieser Domänencontroller ein globaler Katalogserver ist, oder stellen Sie sicher, dass die folgenden Registrierungsschlüssel den Wert 1 hat:  
>   
>  **HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Global Katalog Promotion-abgeschlossen**  
  
 Weitere Informationen finden Sie unter [Hinzufügen des globalen Katalogs](AD-Forest-Recovery-Add-GC.md).  
  
 An diesem Punkt sollten Sie eine stabile Gesamtstruktur, mit einem Domänencontroller für jede Domäne und einen globalen Katalog in der Gesamtstruktur verfügen. Sie sollten eine neue Sicherung aller Domänencontroller erstellen, die Sie gerade wiederhergestellt haben. Sie können nun mit dem anderen Domänencontroller in der Gesamtstruktur erneut bereitstellen, durch die Installation von AD DS beginnen.  

## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md)  
  
