---
title: Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 9883d337520c3920f8638ddfe5f6bd393e31fd2f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442860"
---
# <a name="perform-initial-recovery"></a>Erste Wiederherstellung ausführen  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieser Abschnitt enthält die folgenden Schritte aus:  

- [Wiederherstellen von den ersten beschreibbaren Domänencontroller in jeder Domäne](#restore-the-first-writeable-domain-controller-in-each-domain)  
- [Verbinden Sie jede wiederhergestellte beschreibbarer Domänencontroller mit dem Netzwerk](#reconnect-each-restored-writeable-domain-controller-to-a-common-network)  
- [Hinzufügen des globalen Katalogs zu einem Domänencontroller in der Gesamtstruktur-Stammdomäne](#add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain)  

## <a name="restore-the-first-writeable-domain-controller-in-each-domain"></a>Wiederherstellen von den ersten beschreibbaren Domänencontroller in jeder Domäne  

Beginnen mit einem beschreibbaren Domänencontroller in der Gesamtstruktur-Stammdomäne, die Schritte in diesem Abschnitt zum Wiederherstellen des ersten Domänencontrollers. Gesamtstruktur-Stammdomäne ist wichtig, da sie die Gruppen Schema-Admins und Organisations-Admins speichert. Darüber hinaus können die Vertrauenshierarchie in der Gesamtstruktur verwalten. Darüber hinaus enthält die Gesamtstruktur-Stammdomäne in der Regel die Stamm-DNS-Server für die Gesamtstruktur DNS-Namespace. Die Active Directory-integrierte DNS-Zone für diese Domäne enthält daher die Aliasressourceneintrags (CNAME)-Ressourceneinträge für alle anderen DCs in der Gesamtstruktur (die für die Replikation erforderlich sind) und der globale Katalog DNS-Ressourceneinträge an. 
  
Nach der Wiederherstellung der Gesamtstruktur-Stammdomäne, wiederholen Sie die gleichen Schritte zum Wiederherstellen der verbleibenden Domänen in der Gesamtstruktur. Sie können gleichzeitig mehrere Domänen wiederherzustellen. allerdings immer eine übergeordnete Domäne vor dem Wiederherstellen der ein untergeordnetes Element, um zu verhindern, dass Unterbrechung in der Vertrauenshierarchie oder DNS-namensauflösung wiederhergestellt. 
  
Für jede Domäne, die Sie wiederherstellen, müssen wiederherstellen Sie nur einen beschreibbaren Domänencontroller von Sicherung. Dies ist der wichtigste Teil der Wiederherstellung, weil der Domänencontroller eine Datenbank, die nicht beeinflusst wurden wurde durch die Ursache der Gesamtstruktur nicht benötigen. Es ist wichtig, die über eine vertrauenswürdige Sicherung verfügen, die gründlich getestet wird, bevor es in die produktionsumgebung eingeführt wird. 
  
Führen Sie dann die folgenden Schritte aus. Prozeduren zum Ausführen bestimmter Schritte sind in [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md). 
  
1. Wenn Sie einen physischen Server wiederherstellen möchten, stellen Sie sicher, dass das Netzwerkkabel des Ziels DC nicht angefügt ist und daher nicht mit dem Produktionsnetzwerk verbunden ist. Für einen virtuellen Computer können Sie Entfernen des Netzwerkadapters oder verwenden einen Netzwerkadapter, der mit einem anderen Netzwerk verbunden ist, können Sie den Wiederherstellungsprozess während vom Produktionsnetzwerk isoliert testen. 
  
2. Da dies das erste beschreibbare Domänencontroller in der Domäne ist, müssen Sie eine nicht autoritative Wiederherstellung von AD DS und eine autorisierende Wiederherstellung von SYSVOL ausführen. Der Restore-Vorgang mit einer Active Directory-kompatiblen Sicherung abgeschlossen werden muss und die Anwendung, z. B. Windows Server-Sicherung wiederherstellen (d. h., Sie sollten nicht wiederherstellen den DC mit nicht unterstützten Methoden, z.B. das Wiederherstellen einer VM-Momentaufnahme). 
   - Eine autorisierende Wiederherstellung von SYSVOL ist erforderlich, da die Replikation von SYSVOL repliziert, dass die Ordner nach der Wiederherstellung nach einem Notfall gestartet werden muss. Alle nachfolgenden DCs, die in der Domäne hinzugefügt werden, müssen ihren Ordner "SYSVOL" mit einer Kopie des Ordners synchronisieren, die ausgewählt wurde maßgeblich sein, bevor Sie der Ordner angekündigt werden kann. 

   > [!CAUTION]
   > Führen Sie einen autorisierenden (oder primäre) Wiederherstellungsvorgang von SYSVOL nur für des ersten Domänencontrollers in der Gesamtstruktur-Stammdomäne wiederhergestellt werden. Führt falsch Durchführung von Vorgängen für primäre Wiederherstellung von SYSVOL auf anderen Domänencontrollern zu Konflikten bei der SYSVOL-Daten. 

   - Es gibt zwei Optionen führen Sie eine nicht autoritative Wiederherstellung von AD DS und eine autorisierende Wiederherstellung von SYSVOL:  
   - Ausführen einer vollständigen Wiederherstellungs, und klicken Sie dann eine autoritative Synchronisierung von SYSVOL zu erzwingen. Ausführliche Verfahren finden Sie unter [Ausführen einer vollständigen Wiederherstellungs](AD-Forest-Recovery-Perform-a-Full-Recovery.md) und [eine autoritative Synchronisierung von DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md). 
   - Führen Sie eine vollständige Wiederherstellung des Servers eine Wiederherstellung des Systemstatus gefolgt. Diese Option erfordert, dass Sie beide Arten von Sicherungen im Voraus erstellen: eine vollständige serversicherung und eine Sicherung des Systemstatus. Ausführliche Verfahren finden Sie unter [Ausführen einer vollständigen Wiederherstellungs](AD-Forest-Recovery-Perform-a-Full-Recovery.md) und [Ausführen eine nicht autoritative Wiederherstellung von Active Directory Domain Services](AD-Forest-Recovery-Nonauthoritative-Restore.md). 
  
3. Nachdem Sie wiederhergestellt und neu der beschreibbare Domänencontroller starten, stellen Sie sicher, dass der Fehler nicht die Daten auf dem DC ausgewirkt hat. Wenn die Domänencontroller Daten beschädigt ist, wiederholen Sie Schritt 2 mit einer anderen Sicherung. 
   - Wenn es sich bei der wiederhergestellten Domänencontroller eine Betriebsmasterrolle hostet, müssen Sie möglicherweise, fügen den folgenden Registrierungseintrag zur Vermeidung von AD DS nicht verfügbar ist, bis er eine schreibbare Verzeichnispartition Replikation abgeschlossen wurde:  

      **HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations**  
  
      Erstellen Sie den Eintrag mit dem Datentyp **REG_DWORD** und den Wert **0**. Nach die Gesamtstruktur vollständig wiederhergestellt wird, können Sie den Wert dieses Eintrags zum Zurücksetzen **1**, erfordert einen Domänencontroller, die neu gestartet wird und Betriebsmasterrollen haben erfolgreiche AD DS enthält eingehende und ausgehende Replikation mit der Replikat-Partner bezeichnet, bevor er sich selbst als Domänencontroller kündigt und startet die Dienste für Clients bereitstellt. Weitere Informationen zu den Anforderungen der erstsynchronisierung, KB-Artikel finden Sie unter [305476](https://support.microsoft.com/kb/305476). 
  
      Die nächsten Schritte weiterhin nur auf, nachdem Sie wiederhergestellt, und überprüfen Sie die Daten, und bevor Sie diese Computer im Produktionsnetzwerk hinzugefügt. 
  
4. Wenn Sie vermuten, dass der Gesamtstruktur-Fehler im Zusammenhang mit der Netzwerk-Eindringversuchen oder böswilligen Angriffen, Zurücksetzen der Kennwörter für alle Administratorkonten, einschließlich Elementen der Organisations-Admins, Domänen-Admins, Schema-Admins, Server-Operatoren, Konto Gruppen von Operatoren und So weiter. Das Zurücksetzen von Kennwörtern für Administratorkonto sollte vor dem weitere Domäne abgeschlossen werden, die Controller während der nächsten Phase der Wiederherstellung der Gesamtstruktur installiert werden. 
5. Auf der ersten wiederhergestellten DC in der Gesamtstruktur-Stammdomäne Betriebsmasterrollen alle Domänen- und Gesamtstruktur. Organisations-Admins und Schema-Admins-Anmeldeinformationen sind erforderlich, um gesamtstrukturweite Betriebsmasterfunktionen übernehmen. 
  
     Betriebsmasterrollen Sie in untergeordneten Domänen domänenweite. Obwohl Sie möglicherweise die Betriebsmasterrollen auf dem wiederhergestellten DC nur vorübergehend beibehalten, diese Rollen übernehmen stellt sicher im Hinblick auf die Domänencontroller werden an diesem Punkt im Wiederherstellungsprozess Gesamtstruktur hostet. Im Rahmen Ihrer nach der Wiederherstellung können Sie die Betriebsmasterfunktionen weiterverteilen, je nach Bedarf. Weitere Informationen zu Betriebsmasterrollen, finden Sie unter [übernehmen eine Betriebsmasterfunktion](AD-forest-recovery-seizing-operations-master-role.md). Empfehlungen zum Platzieren von Betriebsmasterrollen finden Sie [Was sind Betriebsmaster?](https://technet.microsoft.com/library/cc779716.aspx). 
  
6. Der Cleanup von Metadaten von anderen beschreibbaren DCs in der Gesamtstruktur-Stammdomäne, die Sie nicht aus einer Sicherung (alle beschreibbaren DCs in der Domäne, mit Ausnahme von dieser ersten Domänencontrollers) wiederherstellen. Wenn Sie verwenden die Version des Active Directory-Benutzer und Computer oder Active Directory-Standorte und Dienste, die im Lieferumfang von Windows Server 2008 oder höher ausgeführt wird oder Remoteserver-Verwaltungstools für Windows Vista oder höher Metadatencleanup automatisch ausgeführt wird, wenn Sie ein DC-Objekt löschen. Darüber hinaus werden die Server-Objekt und das Computerobjekt für den gelöschten DC auch automatisch gelöscht. Weitere Informationen finden Sie unter [Bereinigen von Metadaten von beschreibbaren DCs entfernt](AD-Forest-Recovery-Cleaning-Metadata.md). 
  
     Mögliches Duplikat des NTDS-Einstellungsobjekten Bereinigen von Metadaten verhindert werden, wenn AD DS auf einem Domänencontroller an einem anderen Standort installiert ist. Möglicherweise kann dies auch die Konsistenzprüfung (KCC) speichern Replikationslinks erstellen, wenn die DCs selbst möglicherweise nicht vorhanden. DC-Locators DNS-Ressourceneinträge für alle anderen DCs in der Domäne werden darüber hinaus kann als Teil der Metadatenbereinigung, aus dem DNS gelöscht werden. 
  
     Bis die Metadaten von allen anderen Domänencontrollern innerhalb der Domäne entfernt wird, dieser DC, wäre es eine RID-Master vor der Wiederherstellung übernimmt nicht die RID-Masterrolle und aus diesem Grund ist nicht möglich, neue RIDs ausstellen. Ereignis-ID 16650 im Systemprotokoll in der Ereignisanzeige angezeigt, die dieser Fehler wird möglicherweise angezeigt, aber die Ereignis-ID 16648 Anzeigen des Erfolgs einige Zeit nach dem Sie die Metadaten bereinigt haben sollte angezeigt werden. 
  
7. Wenn Sie DNS-Zonen, die in AD DS gespeichert sind verfügen, stellen Sie sicher, dass der lokale DNS-Server-Dienst ist, installiert ist und ausgeführt, auf dem DC, der Sie wiederhergestellt haben. Wenn Sie diesen Domänencontroller nicht über einen DNS-Server vor dem Ausfall für die Gesamtstruktur war, müssen Sie installieren und konfigurieren den DNS-Server. 
  
    > [!NOTE]
    > Wenn der wiederhergestellte DC mit Windows Server 2008 ausgeführt wird, müssen Sie den Hotfix zu installieren, im KB-Artikel [975654](https://support.microsoft.com/kb/975654) oder Verbinden Sie den Server mit einem isolierten Netzwerk vorübergehend um DNS-Server zu installieren. Der Hotfix ist nicht für andere Versionen von Windows Server erforderlich. 
  
     Konfigurieren Sie in der Gesamtstruktur-Stammdomäne den wiederhergestellten DC mit eigener IP-Adresse (oder eine Loopback-Adresse, z. B. 127.0.0.1) als bevorzugten DNS-Server. Sie können diese Einstellung in den TCP/IP-Eigenschaften des lokalen Netzwerks (LAN)-Adapters konfigurieren. Dies ist der erste DNS-Server in der Gesamtstruktur. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP, DNS zu verwenden](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx). 
  
     Konfigurieren Sie in untergeordneten Domänen den wiederhergestellten DC mit der IP-Adresse des ersten DNS-Servers in der Gesamtstruktur-Stammdomäne als bevorzugten DNS-Server. Sie können diese Einstellung in den TCP/IP-Eigenschaften der LAN-Adapter konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP, DNS zu verwenden](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx). 
  
     Löschen Sie NS-Einträge von DCs, die nicht mehr nach der Metadatenbereinigung vorhanden sind, in die "_msdcs" und die Domäne DNS-Zonen. Überprüfen Sie, ob die SRV-Einträge der bereinigten Domänencontroller entfernt wurden. Damit DNS SRV-Datensatz entfernt beschleunigen können, führen Sie Folgendes aus:  
  
    ```  
    nltest.exe /dsderegdns:server.domain.tld  
    ```  
  
8. Erhöhen Sie den Wert des verfügbaren RID-Pools, indem Sie 100.000. Weitere Informationen finden Sie unter [auslösen den Wert des verfügbaren RID-Pools](AD-Forest-Recovery-Raise-RID-Pool.md). Falls Sie Grund zu glauben, dass der RID-Pool von 100.000 auslösen, für Ihre spezifische Situation nicht ausreicht, sollten Sie die Erhöhung der niedrigsten ermitteln, die immer noch sicher verwendet werden kann. RIDs sind eine begrenzte Ressource, die nicht unnötigerweise verbraucht werden sollte. 
  
     Neue Sicherheitsprinzipale in der Domäne nach dem Zeitpunkt der Sicherung erstellt wurden, die Sie für die Wiederherstellung verwenden, können diese Sicherheitsprinzipale Zugriffsrechte für bestimmte Objekte verfügen. Diese Sicherheitsprinzipale ist nach der Wiederherstellung nicht mehr vorhanden, da es sich bei die Wiederherstellung der Sicherung wiederhergestellt wurde; Ihre Zugriffsrechte können jedoch weiterhin vorhanden. Wenn der RID-Pool verfügbar sind, nicht nach einer Wiederherstellung ausgelöst wird, wird neuer Benutzer-Objekte, die erstellt werden, nachdem die Wiederherstellung der Gesamtstruktur identischen Sicherheits-IDs (SIDs) abgerufen werden kann und möglicherweise Zugriff auf diese Objekte, die nicht ursprünglich beabsichtigt war. 
  
     Um zu veranschaulichen, betrachten Sie das Beispiel des neuen Mitarbeiters, der mit dem Namen Amy, die in der Einleitung erwähnt wurde aus. Das Benutzerobjekt für Amy ist nach der Wiederherstellung nicht mehr vorhanden, da sie nach der Sicherung erstellt wurde, die beim Wiederherstellen der Domäne verwendet wurde. Allerdings können keine Zugriffsrechte, die dieses User-Objekt zugewiesen wurden, nach dem Wiederherstellungsvorgang beibehalten. Wenn die SID für dieses User-Objekt nach dem Wiederherstellungsvorgang ein neues Objekt zugewiesen ist, wird das neue Objekt diese Zugriffsrechte erhalten. 
  
9. Den aktuelle RID-Pool wird ungültig. Der aktuelle RID-Pool wird ungültig, nachdem eine den Systemstatus wiederherstellen. Aber wenn eine Wiederherstellung des Systemstatus nicht ausgeführt wurde, muss der aktuelle RID-Pool ungültig gemacht werden, um zu verhindern, dass den wiederhergestellten DC erneut RIDs ausstellen, über den RID-Pool, der zum Zeitpunkt zugewiesen wurde, die die Sicherung erstellt wurde. Weitere Informationen finden Sie unter [den aktuelle RID-Pool ungültig](AD-Forest-Recovery-Invaildate-RID-Pool.md). 
  
    > [!NOTE]
    > Beim ersten, die Sie versuchen, nachdem Sie den RID-Pool ungültig machen, erstellen Sie ein Objekt mit einer SID erhalten Sie einen Fehler. Der Versuch, ein Objekt zu erstellen, löst eine Anforderung für ein neuer RID-Pool. Wiederholung des Vorgangs ist erfolgreich, da der neue RID-Pool zugeordnet wird. 
  
10. Das Kennwort des Computerkontos dieses Domänencontrollers zweimal zurückgesetzt. Weitere Informationen finden Sie unter [Zurücksetzen des Kennworts für das Computerkonto des Domänencontrollers](AD-Forest-Recovery-Reset-Computer-Account-DC.md). 
  
11. Das Krbtgt-Kennwort zweimal zurücksetzen. Weitere Informationen finden Sie unter [Zurücksetzen des Kennworts Krbtgt](AD-Forest-Recovery-Resetting-the-krbtgt-password.md). 
  
     Da der Kennwortverlauf Krbtgt zwei Kennwörter ist, Zurücksetzen von Kennwörtern zweimal aus, um das ursprüngliche (Prefailure) Kennwort aus Kennwort und Verlauf zu entfernen. 
  
    > [!NOTE]
    > Wenn die Wiederherstellung der Gesamtstruktur als Reaktion auf sicherheitsverletzungen ist, können Sie auch die Kennwörter für die Vertrauensstellung zurücksetzen. Weitere Informationen finden Sie unter [Zurücksetzen eines Kennworts vertrauen auf einer Seite der Vertrauensstellung](AD-Forest-Recovery-Reset-Trust.md). 
  
12. Wenn die Gesamtstruktur verfügt über mehrere Domänen und der wiederhergestellte DC ein globaler Katalogserver vor Auftreten des Fehlers wurde, deaktivieren Sie die **globalen Katalog** Kontrollkästchen in den Eigenschaften des NTDS-Einstellungen Entfernen des globalen Katalogs des Domänencontrollers. Die Ausnahme von dieser Regel wird die häufiges Szenario für eine Gesamtstruktur mit nur einer Domäne. In diesem Fall ist es nicht erforderlich, um den globalen Katalog zu entfernen. Weitere Informationen finden Sie unter [Entfernen des globalen Katalogs](AD-Forest-Recovery-Remove-GC.md). 
  
     Durch das Wiederherstellen von eines globalen Katalogs aus einer Sicherung, die weitere möglicherweise vor dem anderen Sicherungen, die verwendet werden, um DCs in anderen Domänen wiederherzustellen Sie veraltete Objekte einführen. Betrachten Sie das folgende Beispiel aus. In Domäne A wird DC1 aus einer Sicherung wiederhergestellt, die zum Zeitpunkt T1 erstellt wurde. In Domäne B wird DC2 von einer Sicherung des globalen Katalogs wiederhergestellt, die zum Zeitpunkt T2 erstellt wurde. Angenommen Sie, T2 ist aktueller als T1 und einige Objekte, die zwischen T1 und T2 erstellt wurden. Nachdem diese DCs wiederhergestellt wurden, enthält DC2, die einen globalen Katalog handelt, neuere Daten für die Domäne, die ein partielles Replikat als Domäne A enthält selbst. DC2 enthält veraltete Objekte in diesem Fall, da diese Objekte nicht auf DC1 vorhanden sind. 
  
     Das Vorhandensein von veralteten Objekten kann zu Problemen führen. E-Mail-Nachrichten können beispielsweise nicht zu einem Benutzer übermittelt werden, dessen Objekt zwischen Domänen verschoben wurde. Nachdem Sie die veralteten Domänencontroller oder globalen Katalogserver wieder online schalten, werden Sie beide Instanzen des Benutzerobjekts in den globalen Katalog angezeigt. Beide Objekte über die gleiche e-Mail-Adresse verfügen; aus diesem Grund können keine e-Mail-Nachrichten übermittelt werden. 
  
     Ein zweite Problem ist, dass ein Benutzerkonto, das nicht mehr vorhanden ist immer noch in der globalen Adressliste angezeigt werden kann. Ein drittes Problem ist, dass eine universelle Gruppe, die nicht mehr vorhanden ist immer noch im Zugriffstoken eines Benutzers angezeigt werden kann. 
  
     Wenn Sie einen DC wiederhergestellt, die einen globalen Katalog wurde – entweder versehentlich oder weil die einzelne Sicherung, die Sie als vertrauenswürdig war – es wird empfohlen, dass Sie verhindern, das Vorhandensein der veraltete Objekte dass durch das Deaktivieren des globalen Katalogs, sobald der Wiederherstellungsvorgang vollständig. Deaktivieren das Flag für den globalen Katalog führt der Computer verloren gehen alle seine Teilreplikate (Partitionen), und die Verbannung selbst zu regulären DC-Status. 
  
13. Konfigurieren Sie Windows-Zeitdienst. Konfigurieren Sie in der Gesamtstruktur-Stammdomäne den PDC-Emulator, um die Zeit mit einer externen Zeitquelle synchronisieren. Weitere Informationen finden Sie unter [konfigurieren den Windows-Zeitdienst auf dem PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29). 
  
## <a name="reconnect-each-restored-writeable-domain-controller-to-a-common-network"></a>Verbinden Sie jede wiederhergestellte beschreibbarer Domänencontroller mit einem gemeinsamen Netzwerk

In dieser Phase sollten Sie einen DC wiederhergestellt (und Wiederherstellungsschritte ausgeführt) in der Stammdomäne der Gesamtstruktur und in jeder der verbleibenden Domänen verfügen. Verknüpfen Sie diese DCs mit einem gemeinsamen Netzwerk, das von der übrigen Umgebung isoliert ist, und führen Sie folgende Schritte zum Überprüfen der Integrität der Gesamtstruktur und die Replikation.

> [!NOTE]
> Wenn Sie die physischen Domänencontroller mit einem isolierten Netzwerk verbinden, müssen Sie ihre IP-Adressen ändern. Daher werden die IP-Adressen von DNS-Einträgen falsch sein. Da ein globaler Katalogserver nicht verfügbar ist, misslingt sichere dynamische Updates für DNS. Virtuelle DCs sind in diesem Fall mehr vorteilhaft, da sie mit einem neuen virtuellen Netzwerk verknüpft werden können, ohne die IP-Adressen zu ändern. Dies ist ein Grund, warum virtuelle DCs als ersten Domänencontroller empfohlen werden, während der Wiederherstellung der Gesamtstruktur wiederhergestellt werden. 
  
Fügen Sie nach der Überprüfung die DCs im Produktionsnetzwerk, und führen Sie die Schritte zum Überprüfen der Integrität der Gesamtstruktur-Replikation.

- Um die namensauflösung zu beheben, erstellen Sie DNS-Delegierungseinträge aus, und konfigurieren Sie DNS-Weiterleitung und Stamm Stammhinweisen je nach Bedarf. Führen Sie **Repadmin/replsum** Replikation zwischen DCs zu überprüfen. 
- Wenn des wiederhergestellten DC nicht direkten Replikationspartner sind, werden replikationswiederherstellung viel schneller durch das Erstellen von temporären Verbindungsobjekte zwischen ihnen. 
- Um Metadaten bereinigen zu überprüfen, führen **Repadmin /viewlist \\** * eine Liste mit allen Domänencontrollern in der Gesamtstruktur. Führen Sie **Nltest /DCList:** *< Domäne\>*  eine Liste mit allen Domänencontrollern in der Domäne. 
- Um Domänencontroller- und DNS-Integrität zu überprüfen, führen Sie DCDiag/v um Fehler zu melden, für alle Domänencontroller in der Gesamtstruktur. 

## <a name="add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain"></a>Hinzufügen des globalen Katalogs zu einem Domänencontroller in der Gesamtstruktur-Stammdomäne

Ein globaler Katalog ist für diesen und anderen Gründen erforderlich:  
  
- Um die Anmeldungen für Benutzer zu aktivieren. 
- Zum Aktivieren der Netlogon-Dienst ausgeführt wird, auf den DCs in jeder untergeordneten Domäne registrieren und Entfernen von Einträgen in der DNS-Server in der Stammdomäne an. 
  
Es wird jedoch empfohlen, dass der Gesamtstruktur-Stammdomäne DC ein globaler Katalog sind, ist es möglich, die festlegen, ob eines der wiederhergestellte Domänencontroller zu einem globalen Katalog. 
  
> [!NOTE]
> Ein Domänencontroller wird nicht als ein globaler Katalogserver angekündigt werden, bis sie eine vollständige Synchronisierung aller Verzeichnispartitionen in der Gesamtstruktur abgeschlossen ist. Aus diesem Grund sollte der DC erzwungen werden, mit der wiederhergestellten Domänencontroller in der Gesamtstruktur repliziert. 
>
> Überwachen Sie den Verzeichnisdienst-Ereignisprotokoll in der Ereignisanzeige für Ereignis-ID 1119, der angibt, dass dieser Domänencontroller ein globaler Katalogserver ist, oder stellen Sie sicher, dass der folgende Registrierungsschlüssel den Wert 1 hat:  
>
> **HKLM\System\CurrentControlSet\Services\NTDS\Parameters\Global Katalog heraufstufung abgeschlossen**  
  
Weitere Informationen finden Sie unter [Hinzufügen des globalen Katalogs](AD-Forest-Recovery-Add-GC.md). 
  
In dieser Phase sollten Sie eine stabile Gesamtstruktur, mit einem Domänencontroller für jede Domäne und einen globalen Katalog in der Gesamtstruktur verfügen. Sie sollten eine neue Sicherung der einzelnen Domänencontroller vornehmen, die Sie gerade erst wiederhergestellt haben. Sie können jetzt beginnen, anderen DCs in der Gesamtstruktur, die durch die Installation von AD DS erneut bereitstellen. 

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md)  
