---
title: 'AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: ca942691a88465061ebbde2b78314844a694fbf2
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868202"
---
# <a name="perform-initial-recovery"></a>Anfängliche Wiederherstellung ausführen  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Dieser Abschnitt enthält die folgenden Schritte:  

- [Wiederherstellen des ersten beschreibbaren Domänen Controllers in jeder Domäne](#restore-the-first-writeable-domain-controller-in-each-domain)  
- [Verbinden Sie jeden wiederhergestellten beschreibbaren Domänen Controller erneut mit dem Netzwerk.](#reconnect-each-restored-writeable-domain-controller-to-a-common-network)  
- [Hinzufügen des globalen Katalogs zu einem Domänen Controller in der Stamm Domäne der Gesamtstruktur](#add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain)  

## <a name="restore-the-first-writeable-domain-controller-in-each-domain"></a>Wiederherstellen des ersten beschreibbaren Domänen Controllers in jeder Domäne  

Beginnen Sie mit einem beschreibbaren Domänen Controller in der Stamm Domäne der Gesamtstruktur, und führen Sie die Schritte in diesem Abschnitt aus, um den ersten DC wiederherzustellen. Die Stamm Domäne der Gesamtstruktur ist wichtig, da Sie die Gruppen Schema-Admins und Organisations-Admins speichert. Außerdem wird die Vertrauens Hierarchie in der Gesamtstruktur beibehalten. Außerdem enthält die Stamm Domäne der Gesamtstruktur in der Regel den DNS-Stamm Server für den DNS-Namespace der Gesamtstruktur. Folglich enthält die integrierte DNS-Zone Active Directory – für diese Domäne die Alias Ressourcen Einträge (CNAME) für alle anderen DCs in der Gesamtstruktur (die für die Replikation erforderlich sind) und die DNS-Ressourcen Einträge des globalen Katalogs. 
  
Nachdem Sie die Stamm Domäne der Gesamtstruktur wieder hergestellt haben, wiederholen Sie dieselben Schritte, um die übrigen Domänen in der Gesamtstruktur wiederherzustellen Sie können mehr als eine Domäne gleichzeitig wiederherstellen. Stellen Sie jedoch immer eine übergeordnete Domäne wieder her, bevor Sie ein untergeordnetes Element wiederherstellen, um eine Unterbrechung der Vertrauensstellungs Hierarchie oder der DNS 
  
Stellen Sie für jede wieder herzustellende Domäne nur einen beschreibbaren DC aus der Sicherung wieder her. Dies ist der wichtigste Teil der Wiederherstellung, da der Domänen Controller über eine Datenbank verfügen muss, die nicht von dem verursacht wurde, dass die Gesamtstruktur fehlgeschlagen ist. Es ist wichtig, eine vertrauenswürdige Sicherung zu erstellen, die gründlich getestet wird, bevor Sie in die Produktionsumgebung eingeführt wird. 
  
Führen Sie dann die folgenden Schritte aus. Verfahren zum Ausführen bestimmter Schritte finden Sie unter [Wiederherstellungsverfahren für die AD-](AD-Forest-Recovery-Procedures.md)Gesamtstruktur. 
  
1. Wenn Sie beabsichtigen, einen physischen Server wiederherzustellen, stellen Sie sicher, dass das Netzwerkkabel des Zieldomänen Controllers nicht angefügt ist und daher nicht mit dem Produktionsnetzwerk verbunden ist. Für einen virtuellen Computer können Sie den Netzwerkadapter entfernen oder einen Netzwerkadapter verwenden, der mit einem anderen Netzwerk verbunden ist, in dem Sie den Wiederherstellungsprozess testen können, während er vom Produktionsnetzwerk isoliert ist. 
  
2. Da dies der erste beschreibbare Domänen Controller in der Domäne ist, müssen Sie eine nicht autoritative Wiederherstellung AD DS und eine autoritative Wiederherstellung von SYSVOL durchführen. Der Wiederherstellungs Vorgang muss mithilfe einer Active Directory fähigen Sicherungs-und Wiederherstellungs Anwendung wie Windows Server-Sicherung abgeschlossen werden (d. h., Sie sollten den Domänen Controller nicht mit nicht unterstützten Methoden wie dem Wiederherstellen einer VM-Momentaufnahme wiederherstellen). 
   - Eine autoritative Wiederherstellung von SYSVOL ist erforderlich, da die Replikation des replizierten SYSVOL-Ordners nach der Wiederherstellung nach einem Notfall gestartet werden muss. Alle nachfolgenden DCS, die in der Domäne hinzugefügt werden, müssen ihren SYSVOL-Ordner mit einer Kopie des Ordners, der als autoritative ausgewählt wurde, neu synchronisieren, bevor der Ordner angekündigt werden kann. 

   > [!CAUTION]
   > Führen Sie einen autorisierenden (oder primären) Wiederherstellungs Vorgang von SYSVOL nur aus, damit der erste Domänen Controller in der Stamm Domäne der Gesamtstruktur wieder hergestellt wird. Das falsche Ausführen von primären Wiederherstellungs Vorgängen von SYSVOL auf anderen DCS führt zu Replikations Konflikten bei SYSVOL-Daten. 

   - Es gibt zwei Möglichkeiten, eine nicht autoritative Wiederherstellung AD DS und eine autoritative Wiederherstellung von SYSVOL durchzuführen:  
   - Führen Sie eine vollständige Server Wiederherstellung aus, und erzwingen Sie eine autoritative Synchronisierung von SYSVOL. Ausführliche Verfahren finden Sie unter [Durchführen einer vollständigen Server Wiederherstellung](AD-Forest-Recovery-Perform-a-Full-Recovery.md) und [Durchführen einer autorisierenden Synchronisierung von DFSR-replizierten SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md). 
   - Führen Sie eine vollständige Server Wiederherstellung aus, gefolgt von einer Systemstatus Wiederherstellung. Diese Option erfordert, dass Sie im Voraus beide Arten von Sicherungen erstellen: eine vollständige Server Sicherung und eine Systemstatus Sicherung. Ausführliche Verfahren finden Sie unter [Durchführen einer vollständigen Server Wiederherstellung](AD-Forest-Recovery-Perform-a-Full-Recovery.md) und [Durchführen einer nicht autorisierenden Wiederherstellung Active Directory Domain Services](AD-Forest-Recovery-Nonauthoritative-Restore.md). 
  
3. Nachdem Sie den beschreibbaren DC wieder hergestellt und neu gestartet haben, vergewissern Sie sich, dass sich der Fehler nicht auf die Daten auf dem DC ausgewirkt hat. Wenn die DC-Daten beschädigt sind, wiederholen Sie Schritt 2 mit einer anderen Sicherung. 
   - Wenn der wiederhergestellte Domänen Controller eine Betriebs Master Rolle hostet, müssen Sie möglicherweise den folgenden Registrierungs Eintrag hinzufügen, um zu verhindern, dass AD DS nicht verfügbar ist, bis die Replikation einer beschreibbaren Verzeichnis Partition abgeschlossen ist:  

      **Hklm\system\currentcontrolset\services\ntds\parameters\repl führt anfängliche Synchronisierung aus.**  
  
      Erstellen Sie den Eintrag mit dem-Datentyp **REG_DWORD** und einem Wert von **0**. Nachdem die Gesamtstruktur vollständig wieder hergestellt wurde, können Sie den Wert dieses Eintrags auf **1**zurücksetzen. hierfür ist ein Domänen Controller erforderlich, der neu gestartet wird und Betriebs Master Rollen für die erfolgreiche AD DS eingehender und ausgehender Replikation mit dem bekannten Replikat enthält. Partner, bevor Sie sich selbst als Domänen Controller ankündigen und damit beginnen, Dienste für Clients bereitzustellen. Weitere Informationen zu den Anforderungen für die anfängliche Synchronisierung finden Sie im KB-Artikel [305476](https://support.microsoft.com/kb/305476). 
  
      Fahren Sie mit den nächsten Schritten erst fort, nachdem Sie die Daten wieder hergestellt und überprüft haben und bevor Sie diesen Computer dem Produktionsnetzwerk hinzufügen. 
  
4. Wenn Sie vermuten, dass sich der Gesamtstruktur weite Fehler auf einen Netzwerk Eingriff oder böswillige Angriffe bezieht, setzen Sie die Konto Kennwörter für alle Administrator Konten zurück, einschließlich der Mitglieder der Organisations-Admins, Domänen-Admins, Schema Administratoren, Server Operatoren, Konto Operatoren Gruppen usw. Die zurück Setzung von Administrator Konto Kennwörtern sollte abgeschlossen werden, bevor während der nächsten Phase der Gesamtstruktur Wiederherstellung zusätzliche Domänen Controller installiert werden. 
5. Nehmen Sie auf dem ersten wiederhergestellten DC in der Stamm Domäne der Gesamtstruktur alle Domänen weiten und Gesamtstruktur weiten Betriebs Master Rollen an. Organisations-Admins und Schema-Admins-Anmelde Informationen sind erforderlich, um Gesamtstruktur weite Betriebs Master Rollen zu übernehmen. 
  
     Nehmen Sie in jeder untergeordneten Domäne Domänen weite Betriebs Master Rollen an. Obwohl Sie die Betriebs Master Rollen auf dem wiederhergestellten DC nur vorübergehend beibehalten können, gewährleistet die Übernahme dieser Rollen, dass Sie an diesem Punkt des Wiederherstellungsprozesses der Gesamtstruktur diese Hosts hosten. Im Rahmen des Prozesses nach der Wiederherstellung können Sie die Betriebs Master Rollen nach Bedarf weiterverteilen. Weitere Informationen zum Übernehmen von Betriebs Master Rollen finden Sie unter übernehmen [einer Betriebs Master Rolle](AD-forest-recovery-seizing-operations-master-role.md). Empfehlungen zum Platzieren von Betriebs Master Rollen finden Sie unter [Was sind Betriebs Master?](https://technet.microsoft.com/library/cc779716.aspx). 
  
6. Bereinigen Sie die Metadaten aller anderen beschreibbaren DCS in der Stamm Domäne der Gesamtstruktur, die Sie nicht aus der Sicherung wiederherstellen (Alle beschreibbaren DCS in der Domäne außer dem ersten DC). Wenn Sie die-Version von Active Directory Benutzer und Computer oder Active Directory Websites und-Dienste verwenden, die in Windows Server 2008 oder höher oder RSAT für Windows Vista oder höher enthalten sind, wird die Metadatenbereinigung automatisch ausgeführt, wenn Sie ein DC-Objekt löschen. Außerdem werden das Server Objekt und das Computer Objekt für den gelöschten Domänen Controller ebenfalls automatisch gelöscht. Weitere Informationen finden Sie unter [Bereinigen von Metadaten entfernter Beschreib barer DCS](AD-Forest-Recovery-Cleaning-Metadata.md). 
  
     Das Bereinigen von Metadaten verhindert eine mögliche Duplizierung von NTDS-Settings-Objekten, wenn AD DS auf einem DC an einem anderen Standort installiert ist. Dies könnte auch die Konsistenzprüfung (KCC) zum Erstellen von Replikations Verknüpfungen speichern, wenn die DCS selbst möglicherweise nicht vorhanden sind. Außerdem werden im Rahmen der Metadatenbereinigung die DNS-Ressourcen Einträge des Domänen Controller-Locators für alle anderen DCs in der Domäne aus dem DNS gelöscht. 
  
     Solange die Metadaten aller anderen Domänen Controller in der Domäne entfernt werden, geht dieser DC, wenn er vor der Wiederherstellung ein RID-Master war, nicht von der RID-Master Rolle aus und kann daher keine neuen RIDs ausstellen. Möglicherweise wird im System Protokoll die Ereignis-ID 16650 angezeigt, Ereignisanzeige die diesen Fehler anzeigt. Sie sollten jedoch sehen, dass die Ereignis-ID 16648 ein wenig anzeigt, wenn Sie die Metadaten bereinigt haben. 
  
7. Wenn Sie DNS-Zonen haben, die in AD DS gespeichert sind, stellen Sie sicher, dass der lokale DNS-Server Dienst auf dem von Ihnen wiederhergestellten DC installiert ist und ausgeführt wird. Wenn dieser Domänen Controller vor dem Gesamtstruktur Ausfall kein DNS-Server war, müssen Sie den DNS-Server installieren und konfigurieren. 
  
    > [!NOTE]
    > Wenn der wiederhergestellte Domänen Controller Windows Server 2008 ausführt, müssen Sie den Hotfix im KB-Artikel [975654](https://support.microsoft.com/kb/975654) installieren oder den Server vorübergehend mit einem isolierten Netzwerk verbinden, um den DNS-Server zu installieren. Der Hotfix ist für andere Versionen von Windows Server nicht erforderlich. 
  
     Konfigurieren Sie den wiederhergestellten Domänen Controller in der Stamm Domäne der Gesamtstruktur mit seiner eigenen IP-Adresse (oder einer Loopback Adresse wie 127.0.0.1) als bevorzugten DNS-Server. Sie können diese Einstellung in den TCP/IP-Eigenschaften des LAN-Adapters (Local Area Network) konfigurieren. Dies ist der erste DNS-Server in der Gesamtstruktur. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP für die Verwendung von DNS](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx). 
  
     Konfigurieren Sie in jeder untergeordneten Domäne den wiederhergestellten DC mit der IP-Adresse des ersten DNS-Servers in der Stamm Domäne der Gesamtstruktur als bevorzugten DNS-Server. Sie können diese Einstellung in den TCP/IP-Eigenschaften des LAN-Adapters konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP für die Verwendung von DNS](https://technet.microsoft.com/library/cc779282\(WS.10\).aspx). 
  
     Löschen Sie in den DNS-Zonen _msdcs und Domain die NS-Einträge von DCS, die nach der Metadatenbereinigung nicht mehr vorhanden sind. Überprüfen Sie, ob die SRV-Einträge der bereinigten DCS entfernt wurden. Führen Sie Folgendes aus, um die Entfernung von DNS-SRV-Einträgen zu beschleunigen:  
  
    ```  
    nltest.exe /dsderegdns:server.domain.tld  
    ```  
  
8. Erhöhen Sie den Wert des verfügbaren RID-Pools um 100.000. Weitere Informationen finden Sie unter [erhöhen des Werts von verfügbaren RID-Pools](AD-Forest-Recovery-Raise-RID-Pool.md). Wenn Sie der Meinung sind, dass das Erhöhen des RID-Pools durch 100.000 für ihre besondere Situation unzureichend ist, sollten Sie die niedrigste Erhöhung festlegen, die weiterhin sicher verwendet werden kann. RIDs sind eine begrenzte Ressource, die nicht unnötig verwendet werden sollte. 
  
     Wenn nach dem Zeitpunkt der Sicherung, die Sie für die Wiederherstellung verwenden, neue Sicherheits Prinzipale in der Domäne erstellt wurden, verfügen diese Sicherheits Prinzipale möglicherweise über Zugriffsrechte für bestimmte Objekte. Diese Sicherheits Prinzipale sind nach der Wiederherstellung nicht mehr vorhanden, da die Wiederherstellung auf die Sicherung zurückgesetzt wurde. Ihre Zugriffsrechte sind jedoch möglicherweise weiterhin vorhanden. Wenn der verfügbare RID-Pool nach einer Wiederherstellung nicht ausgelöst wird, erhalten neue Benutzer Objekte, die nach der Wiederherstellung der Gesamtstruktur erstellt werden, möglicherweise identische Sicherheits-IDs (SIDs) und könnten Zugriff auf diese Objekte haben, was ursprünglich nicht beabsichtigt war. 
  
     Um dies zu veranschaulichen, sehen Sie sich das Beispiel für den neuen, in der Einführung erwähnten Mitarbeiter mit dem Namen "Amy" an. Das Benutzerobjekt für Amy ist nach dem Wiederherstellungs Vorgang nicht mehr vorhanden, da es nach der Sicherung erstellt wurde, die zum Wiederherstellen der Domäne verwendet wurde. Alle Zugriffsrechte, die diesem Benutzerobjekt zugewiesen wurden, können jedoch nach dem Wiederherstellungs Vorgang beibehalten werden. Wenn die sid für dieses Benutzerobjekt nach dem Wiederherstellungs Vorgang einem neuen Objekt zugewiesen wird, erhält das neue-Objekt diese Zugriffsrechte. 
  
9. Macht den aktuellen RID-Pool ungültig. Der aktuelle RID-Pool wird nach einer Systemstatus Wiederherstellung ungültig. Wenn jedoch keine Systemstatus Wiederherstellung durchgeführt wurde, muss der aktuelle RID-Pool ungültig werden, um zu verhindern, dass der wiederhergestellte DC RIDs aus dem RID-Pool erneut ausgibt, der zum Zeitpunkt der Erstellung der Sicherung zugewiesen wurde. Weitere Informationen finden Sie unter [invalidieren des aktuellen RID-Pools](AD-Forest-Recovery-Invaildate-RID-Pool.md). 
  
    > [!NOTE]
    > Wenn Sie zum ersten Mal versuchen, ein Objekt mit einer SID zu erstellen, nachdem Sie den RID-Pool ungültig gemacht haben, wird eine Fehlermeldung angezeigt. Der Versuch, ein Objekt zu erstellen, löst eine Anforderung für einen neuen RID-Pool aus. Die Wiederholung des Vorgangs ist erfolgreich, da der neue RID-Pool zugeordnet wird. 
  
10. Setzen Sie das Computer Konto Kennwort für diesen DC zweimal zurück. Weitere Informationen finden Sie unter [Zurücksetzen des Computer Konto Kennworts des Domänen Controllers](AD-Forest-Recovery-Reset-Computer-Account-DC.md). 
  
11. Setzen Sie das krbtgt-Kennwort zweimal zurück. Weitere Informationen finden Sie unter [Zurücksetzen des krbtgt-Kennworts](AD-Forest-Recovery-Resetting-the-krbtgt-password.md). 
  
     Da der krbtgt-Kenn Wort Verlauf zwei Kenn Wörter ist, müssen Sie die Kenn Wörter zweimal zurücksetzen, um das ursprüngliche Kennwort (vorab Fehler) aus dem Kenn Wort Verlauf 
  
    > [!NOTE]
    > Wenn die Wiederherstellung der Gesamtstruktur als Reaktion auf eine Sicherheitsverletzung vorliegt, können Sie auch die Vertrauensstellungs Kennwörter zurücksetzen. Weitere Informationen finden Sie unter [Zurücksetzen eines Vertrauensstellungs Kennworts auf einer Seite der Vertrauens](AD-Forest-Recovery-Reset-Trust.md)Stellung. 
  
12. Wenn die Gesamtstruktur mehrere Domänen aufweist und der wiederhergestellte DC vor dem Auftreten des Fehlers ein globaler Katalogserver war, deaktivieren Sie in den NTDS-Einstellungs Eigenschaften das Kontrollkästchen **globaler Katalog** , um den globalen Katalog vom Domänen Controller zu entfernen. Eine Ausnahme von dieser Regel ist der häufige Fall einer Gesamtstruktur mit nur einer Domäne. In diesem Fall ist es nicht erforderlich, den globalen Katalog zu entfernen. Weitere Informationen finden Sie unter [Entfernen des globalen Katalogs](AD-Forest-Recovery-Remove-GC.md). 
  
     Wenn Sie einen globalen Katalog aus einer Sicherung wiederherstellen, die aktueller als andere Sicherungen ist, die zum Wiederherstellen von DCS in anderen Domänen verwendet werden, können Sie veraltete Objekte einführen. Sehen Sie sich das folgende Beispiel an. In Domäne A wird DC1 aus einer Sicherung wieder hergestellt, die zum Zeitpunkt t1 erstellt wurde. In Domäne B wird DC2 aus einer globalen Katalog Sicherung wieder hergestellt, die zum Zeitpunkt T2 erstellt wurde. Angenommen, T2 ist aktueller als T1, und einige Objekte wurden zwischen T1 und T2 erstellt. Nach der Wiederherstellung dieser DCS enthält DC2, ein globaler Katalog, neuere Daten für das Teil Replikat von Domäne a, als Domäne a sich selbst enthält. DC2 enthält in diesem Fall veraltete Objekte, da diese Objekte nicht auf DC1 vorhanden sind. 
  
     Das vorhanden sein von veralteten Objekten kann zu Problemen führen. Beispielsweise können e-Mail-Nachrichten nicht an einen Benutzer übermittelt werden, dessen Benutzerobjekt zwischen Domänen verschoben wurde. Nachdem Sie den veralteten DC oder globalen Katalogserver wieder online geschaltet haben, werden beide Instanzen des Benutzer Objekts im globalen Katalog angezeigt. Beide Objekte haben dieselbe e-Mail-Adresse. Daher können e-Mail-Nachrichten nicht zugestellt werden. 
  
     Ein zweites Problem besteht darin, dass ein Benutzerkonto, das nicht mehr vorhanden ist, möglicherweise weiterhin in der globalen Adressliste angezeigt wird. Ein drittes Problem besteht darin, dass eine universelle Gruppe, die nicht mehr vorhanden ist, möglicherweise weiterhin im Zugriffs Token eines Benutzers angezeigt wird. 
  
     Wenn Sie einen Domänen Controller wieder hergestellt haben, der ein globaler Katalog war – entweder versehentlich oder weil es sich dabei um die alleinige vertrauenswürdige Sicherung handelt, die Sie als vertrauenswürdig eingestuft haben – wird empfohlen, dass Sie das Vorkommen veralteter Objekte verhindern, indem Sie den globalen Katalog kurz nach dem Wiederherstellungs Vorgang ganz. Das Deaktivieren des globalen katalogitätsflags führt dazu, dass der Computer alle partiellen Replikate (Partitionen) verliert und sich in den regulären DC-Status verlagert. 
  
13. Konfigurieren Sie den Windows-Zeit Dienst. Konfigurieren Sie den PDC-Emulator in der Stamm Domäne der Gesamtstruktur so, dass er die Zeit von einer externen Zeit Quelle synchronisiert. Weitere Informationen finden Sie unter [Konfigurieren des Windows-Zeit Diensts auf dem PDC-Emulator in der Stamm Domäne der](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)Gesamtstruktur. 
  
## <a name="reconnect-each-restored-writeable-domain-controller-to-a-common-network"></a>Verbinden Sie jeden wiederhergestellten beschreibbaren Domänen Controller mit einem gemeinsamen Netzwerk erneut.

In dieser Phase sollte ein Domänen Controller (und Wiederherstellungsschritte) in der Stamm Domäne der Gesamtstruktur und in jeder der übrigen Domänen wieder hergestellt werden. Verknüpfen Sie diese DCS mit einem gemeinsamen Netzwerk, das vom Rest der Umgebung isoliert ist, und führen Sie die folgenden Schritte aus, um die Gesamtstruktur Integrität und-Replikation zu überprüfen.

> [!NOTE]
> Wenn Sie die physischen DCS mit einem isolierten Netzwerk verknüpfen, müssen Sie Ihre IP-Adressen möglicherweise ändern. Folglich sind die IP-Adressen der DNS-Einträge falsch. Da kein globaler Katalogserver verfügbar ist, können sichere dynamische Updates für DNS nicht ausgeführt werden. Virtuelle DCS sind in diesem Fall vorteilhafter, da Sie mit einem neuen virtuellen Netzwerk verknüpft werden können, ohne Ihre IP-Adressen zu ändern. Dies ist ein Grund, warum virtuelle DCS als erste Domänen Controller empfohlen werden, die während der Wiederherstellung der Gesamtstruktur wieder hergestellt werden müssen. 
  
Fügen Sie nach der Überprüfung die DCS zum Produktionsnetzwerk hinzu, und führen Sie die Schritte zum Überprüfen der Integrität der Gesamtstruktur Replikation

- Um die Namensauflösung zu beheben, erstellen Sie DNS-Delegierungs Einträge und konfigurieren DNS-Weiterleitung und Stamm Hinweise nach Bedarf. Führen Sie **repadmin/replsum** zum Überprüfen der Replikation zwischen DCS aus. 
- Wenn die wiederhergestellten Domänen Controller keine direkten Replikations Partner sind, wird die Replikations Wiederherstellung erheblich beschleunigt, indem temporäre Verbindungs Objekte zwischen Ihnen erstellt werden. 
- Um die Metadatenbereinigung zu überprüfen, führen Sie **repadmin/viewlist \\** * für eine Liste aller DCS in der Gesamtstruktur aus. Führen Sie **nltest/DCList:** *<\> Domäne* aus, um eine Liste aller DCS in der Domäne zu finden. 
- Führen Sie dcdiag/v aus, um Fehler für alle DCS in der Gesamtstruktur zu melden. 

## <a name="add-the-global-catalog-to-a-domain-controller-in-the-forest-root-domain"></a>Hinzufügen des globalen Katalogs zu einem Domänen Controller in der Stamm Domäne der Gesamtstruktur

Ein globaler Katalog ist aus diesen und anderen Gründen erforderlich:  
  
- , Um Anmeldungen für Benutzer zu aktivieren. 
- , Damit der Anmeldedienst, der auf den DCS in jeder untergeordneten Domäne ausgeführt wird, Datensätze auf dem DNS-Server in der Stamm Domäne registrieren und entfernen kann. 
  
Obwohl der Gesamtstruktur-Stamm Domänen Controller ein globaler Katalog wird, ist es möglich, jeden der wiederhergestellten DCS als globalen Katalog zu wählen. 
  
> [!NOTE]
> Ein Domänen Controller wird erst als globaler Katalogserver angekündigt, wenn er eine vollständige Synchronisierung aller Verzeichnis Partitionen in der Gesamtstruktur abgeschlossen hat. Daher sollte der DC die Replikation mit jedem der wiederhergestellten DCS in der Gesamtstruktur erzwingen. 
>
> Überwachen Sie das Verzeichnisdienst-Ereignisprotokoll in Ereignisanzeige für die Ereignis-ID 1119, das angibt, dass dieser Domänen Controller ein globaler Katalogserver ist, oder überprüfen Sie, ob der folgende Registrierungsschlüssel den Wert 1 hat:  
>
> **Hklm\system\currentcontrolset\services\ntds\parameters\global Catalog Promotion Complete**  
  
Weitere Informationen finden Sie unter [Hinzufügen des globalen Katalogs](AD-Forest-Recovery-Add-GC.md). 
  
Zu diesem Zeitpunkt sollten Sie über eine stabile Gesamtstruktur mit einem Domänen Controller für jede Domäne und einem globalen Katalog in der Gesamtstruktur verfügen. Erstellen Sie eine neue Sicherung der einzelnen DCS, die Sie soeben wieder hergestellt haben. Sie können nun beginnen, andere DCS in der Gesamtstruktur erneut bereitzustellen, indem Sie AD DS installieren. 

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md)  
