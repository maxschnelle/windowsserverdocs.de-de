---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: Directory Services-Komponentenupdates
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d79f31572bc30d0f4fa3af45671c58b799e40f02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390019"
---
# <a name="directory-services-component-updates"></a>Directory Services-Komponentenupdates

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autor**: Justin Turner, Senior Support Eskalations Ingenieur bei der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
In dieser Lektion werden die Updates der Verzeichnisdienst Komponenten in Windows Server 2012 R2 erläutert.  
  
## <a name="what-you-will-learn"></a>Lernziele  
Erläutern der folgenden neuen Updates der Verzeichnisdienst Komponente:  
  
-   Erläutern der folgenden neuen Updates der Verzeichnisdienst Komponente:  
  
    -   [Domänen- und Gesamtstrukturfunktionsebenen](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [Abschreibung von NTFRS](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [Änderungen am LDAP-Abfrageoptimierer](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [Verbesserungen am Ereignis 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Durchsatzverbesserung bei der Active Directory-Replikation](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="BKMK_FL"></a>Domänen-und Gesamtstruktur Funktionsebenen  
  
### <a name="overview"></a>Übersicht  
Der Abschnitt enthält eine kurze Einführung in die Änderungen an der Domänen-und Gesamtstruktur Funktionsebene.  
  
### <a name="new-dfl-and-ffl"></a>Neue DFL und FFL  
Mit der-Version gibt es neue Domänen-und Gesamtstruktur Funktionsebenen:  
  
-   Gesamtstrukturfunktionsebene: Windows Server 2012 R2  
  
-   Domänen Funktionsebene: Windows Server 2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Die Domänen Funktionsebene Windows Server 2012 R2 bietet Unterstützung für Folgendes:  
  
1.  Domänen Controller seitiger Schutz für *geschützte Benutzer*  
  
    *Geschützte Benutzer* , die sich bei einer Windows Server 2012 R2-Domäne authentifizieren, können **nicht mehr**:  
  
    -   Authentifizieren mit NTLM-Authentifizierung  
  
    -   Verwenden von des-oder RC4-Verschlüsselungs Sammlungen in der Kerberos-Vorauthentifizierung  
  
    -   Delegiert mit eingeschränkter oder eingeschränkter Delegierung  
  
    -   Verlängern von Benutzer Tickets (TGTs) über die anfängliche Dauer von 4 Stunden hinaus  
  
2.  Authentifizierungsrichtlinien  
  
    Neue Gesamtstruktur basierte Active Directory Richtlinien, die auf Konten in Windows Server 2012 R2-Domänen angewendet werden können, um zu steuern, von welchen Hosts ein Konto angemeldet werden kann, und Zugriffs Steuerungs Bedingungen zur Authentifizierung auf Dienste anzuwenden, die als Konto ausgeführt werden.  
  
3.  Authentifizierungsrichtliniensilos  
  
    Neues Gesamtstruktur basiertes Active Directory Objekt, das eine Beziehung zwischen Benutzer, verwaltetem Dienst und Computer Konten erstellen kann, die zum Klassifizieren von Konten für Authentifizierungs Richtlinien oder zur Authentifizierungs Isolation verwendet werden.  
  
Weitere Informationen finden Sie unter Konfigurieren geschützter Konten.  
  
Zusätzlich zu den oben genannten Features stellt die Windows Server 2012 R2-Domänen Funktionsebene sicher, dass alle Domänen Controller in der Domäne Windows Server 2012 R2 ausführen.  
Die Funktionsebene der Windows Server 2012 R2-Gesamtstruktur bietet keine neuen Features, Sie stellt jedoch sicher, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf der Domänen Funktionsebene von Windows Server 2012 R2 ausgeführt werden.  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>Mindestens durch erzwingen der Erstellung einer neuen Domäne  
Windows Server 2008-DFL ist die minimale Funktionsebene, die bei der Erstellung neuer Domänen unterstützt wird.  
  
> [!NOTE]  
> Die Veraltung von FRS erfolgt durch die Möglichkeit, eine neue Domäne mit einer Domänen Funktionsebene zu installieren, die niedriger als Windows Server 2008 mit Server-Manager oder über Windows PowerShell ist.  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>Herabstufen der Gesamtstruktur-und Domänen Funktionsebene  
Die Gesamtstruktur-und Domänen Funktionsebenen werden standardmäßig auf Windows Server 2012 R2 bei neuer Domäne und neuer Gesamtstruktur Erstellung festgelegt, können jedoch mithilfe von Windows PowerShell gesenkt werden.  
  
Verwenden Sie das Cmdlet **Set-adforestmode** , um die Gesamtstruktur Funktionsebene mithilfe von Windows PowerShell zu erhöhen oder zu verringern.  
  
**So legen Sie contoso.com FFL auf den Windows Server 2008-Modus fest:**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Verwenden Sie das Cmdlet Set-addomainmode, um die Domänen Funktionsebene mithilfe von Windows PowerShell zu erhöhen oder zu verringern.  
  
**So legen Sie die contoso.com-DFL auf den Windows Server 2008-Modus fest:**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
Das herauf Stufen eines Domänen Controllers unter Windows Server 2012 R2 als zusätzliches Replikat in eine vorhandene Domäne mit 2003 DFL funktioniert.  
  
Erstellung einer neuen Domäne in einer vorhandenen Gesamtstruktur  
  
![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
In dieser Version sind keine neuen Gesamtstruktur-oder Domänen Vorgänge vorhanden.  
  
Diese LDF-Dateien enthalten Schema Änderungen für den **Geräte Registrierungsdienst**.  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**Arbeitsordner:**  
  
1.  Sch66  
  
**MSODS**  
  
1.  Sch60  
  
**Authentifizierungs Richtlinien und Silos**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="BKMK_NTFRS"></a>Veraltung von NTFRS  
  
### <a name="overview"></a>Übersicht  
FRS ist in Windows Server 2012 R2 veraltet.  Die Veraltung von FRS erfolgt durch Erzwingen einer minimalen Domänen Funktionsebene (Windows Server 2008).  Diese Erzwingung ist nur vorhanden, wenn die neue Domäne mithilfe von Server-Manager oder Windows PowerShell erstellt wird.  
  
Verwenden Sie den-DomainMode-Parameter mit den Cmdlets install-addsforest oder install-addsdomain, um die Domänen Funktionsebene anzugeben.  Unterstützte Werte für diesen Parameter können entweder eine gültige ganze Zahl oder ein entsprechender enumerationszeichen folgen Wert sein. Wenn Sie z. b. die Domänen Modus-Ebene auf Windows Server 2008 R2 festlegen möchten, können Sie entweder den Wert "4" oder "Win2008R2" angeben.  Wenn Sie diese Cmdlets von Server 2012 R2 ausführen, sind gültige Werte für Windows Server 2008 (3, Win2008) Windows Server 2008 R2 (4, Win2008R2) Windows Server 2012 (5, Win2012) und Windows Server 2012 R2 (6, Win2012R2). Die Domänenfunktionsebene kann nicht niedriger als die Funktionsebene der Gesamtstruktur sein. Sie kann jedoch höher sein.  Da FRS in dieser Version veraltet ist, ist Windows Server 2003 (2, Win2003) bei der Ausführung von Windows Server 2012 R2 kein erkannter Parameter mit diesen Cmdlets.  
  
![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>Änderungen am LDAP-Abfrageoptimierer  
  
### <a name="overview"></a>Übersicht  
Der Algorithmus für den LDAP-Abfrageoptimierer wurde neu ausgewertet und weiter optimiert.  Das Ergebnis ist die Leistungsverbesserung bei der LDAP-Such Effizienz und der LDAP-Suchzeit komplexer Abfragen.  
  
> [!NOTE]
> <strong>Vom Entwickler:</strong>Verbesserungen bei der Leistung von Such Vorgängen durch Verbesserungen bei der Zuordnung von LDAP-Abfragen zu ESE-Abfragen.  LDAP-Filter über einen bestimmten Grad an Komplexität verhindern die optimierte Index Auswahl, was zu einer deutlich geringeren Leistung führt (1000 x oder mehr). Diese Änderung ändert die Art und Weise, wie Indizes für LDAP-Abfragen ausgewählt werden, um dieses Problem zu vermeiden.  
> 
> [!NOTE]
> Eine umfassende Überarbeitung des Algorithmus für den LDAP-Abfrageoptimierer, was zu folgendem führt:  
> 
> -   Schnellere Suchzeiten  
> -   Effizienzsteigerungen ermöglichen DCS mehr  
> -   Weniger Support Anrufe bezüglich AD-Leistungsproblemen  
> -   Zurückportiert zu Windows Server 2008 R2 (KB 2862304)  
  
### <a name="background"></a>Hintergrund  
Die Möglichkeit, Active Directory zu durchsuchen, ist ein Kerndienst von Domänen Controllern.  Andere Dienste und Branchen Anwendungen basieren auf Active Directory suchen.  Wenn dieses Feature nicht verfügbar ist, können Geschäftsvorgänge angehalten werden.  Als Kerndienst und stark verwendeter Dienst ist es zwingend erforderlich, dass Domänen Controller den LDAP-Such Datenverkehr effizient verarbeiten.  Der Algorithmus des LDAP-Abfrage Optimierers versucht, LDAP-Suchvorgänge so effizient wie möglich zu machen, indem LDAP-Suchfilter einem Resultset entsprechend der bereits in der Datenbank indizierten Datensätze zuordnet werden.  Dieser Algorithmus wurde neu ausgewertet und weiter optimiert.  Das Ergebnis ist die Leistungsverbesserung bei der LDAP-Such Effizienz und der LDAP-Suchzeit komplexer Abfragen.  
  
### <a name="details-of-change"></a>Details der Änderung  
Eine LDAP-Suche enthält Folgendes:  
  
-   Ein Speicherort (NC-Head, ou, Objekt) innerhalb der Hierarchie, um mit der Suche zu beginnen  
  
-   Ein Suchfilter  
  
-   Eine Liste der zurück zugebende Attribute.  
  
Der Suchvorgang kann wie folgt zusammengefasst werden:  
  
1.  Vereinfachen Sie den Suchfilter, wenn möglich.  
  
2.  Wählen Sie einen Satz von Index Schlüsseln aus, die den kleinsten abgedeckten Satz zurückgeben.  
  
3.  Führen Sie einen oder mehrere Schnittpunkte der Index Schlüssel aus, um die abgedeckte Menge zu verringern.  
  
4.  Evaluieren Sie für jeden Datensatz in der abgedeckten Gruppe den Filter Ausdruck und die Sicherheit. Wenn der Filter als true ausgewertet wird und der Zugriff gewährt wird, geben Sie diesen Datensatz an den Client zurück.  
  
Der Arbeitsaufwand für die LDAP-Abfrageoptimierung ändert die Schritte 2 und 3, um die Größe der abgedeckten Gruppe zu verringern. Genauer gesagt wählt die aktuelle Implementierung doppelte Index Schlüssel aus und führt redundante Schnittmengen aus.  
  
### <a name="comparison-between-old-and-new-algorithm"></a>Vergleich zwischen altem und neuem Algorithmus  
Das Ziel der ineffizienten LDAP-Suche in diesem Beispiel ist ein Windows Server 2012-Domänen Controller.  Die Suche wird in ungefähr 44 Sekunden abgeschlossen, weil ein effizienterer Index nicht gefunden werden konnte.  
  
```  
adfind -b dc=blue,dc=contoso,dc=com -f "(| (& (|(cn=justintu) (postalcode=80304) (userprincipalname=justintu@blue.contoso.com)) (|(objectclass=person) (cn=justintu)) ) (&(cn=justintu)(objectclass=person)))" -stats >>adfind.txt  
  
Using server: WINSRV-DC1.blue.contoso.com:389  
  
<removed search results>  
  
Statistics  
=====  
Elapsed Time: 44640 (ms)  
Returned 324 entries of 553896 visited - (0.06%)  
  
Used Filter:  
 ( |  ( &  ( |  (cn=justintu)  (postalCode=80304)  (userPrincipalName=justintu@blue.contoso.com) )  ( |  (objectClass=person)  (cn=justintu) ) )  ( &  (cn=justintu)  (objectClass=person) ) )   
  
Used Indices:  
 DNT_index:516615:N  
  
Pages Referenced          : 4619650  
Pages Read From Disk      : 973  
Pages Pre-read From Disk  : 180898  
Pages Dirtied             : 0  
Pages Re-Dirtied          : 0  
Log Records Generated     : 0  
Log Record Bytes Generated: 0  
```  
  
### <a name="sample-results-using-the-new-algorithm"></a>Beispiel Ergebnisse mit dem neuen Algorithmus  
In diesem Beispiel wird genau dieselbe Suche wie oben wiederholt, aber es ist ein Windows Server 2012 R2-Domänen Controller.  Die gleiche Suche wird in weniger als einer Sekunde aufgrund der Verbesserungen des Algorithmus für den LDAP-Abfrageoptimierer durchgeführt.  
  
```  
adfind -b dc=blue,dc=contoso,dc=com -f "(| (& (|(cn=justintu) (postalcode=80304) (userprincipalname=dhunt@blue.contoso.com)) (|(objectclass=person) (cn=justintu)) ) (&(cn=justintu)(objectclass=person)))" -stats >>adfindBLUE.txt  
  
Using server: winblueDC1.blue.contoso.com:389  
  
.<removed search results>  
  
Statistics  
=====  
Elapsed Time: 672 (ms)  
Returned 324 entries of 648 visited - (50.00%)  
  
Used Filter:  
 ( |  ( &  ( |  (cn=justintu)  (postalCode=80304)  (userPrincipalName=justintu@blue.contoso.com) )  ( |  (objectClass=person)  (cn=justintu) ) )  ( &  (cn=justintu)  (objectClass=person) ) )   
  
Used Indices:  
 idx_userPrincipalName:648:N  
 idx_postalCode:323:N  
 idx_cn:1:N  
  
Pages Referenced          : 15350  
Pages Read From Disk      : 176  
Pages Pre-read From Disk  : 2  
Pages Dirtied             : 0  
Pages Re-Dirtied          : 0  
Log Records Generated     : 0  
Log Record Bytes Generated: 0  
```  
  
-   Wenn die Struktur nicht optimiert werden kann:  
  
    -   Beispiel: ein Ausdruck in der Struktur befand sich über einer nicht indizierten Spalte.  
  
    -   Aufzeichnen einer Liste von Indizes, die eine Optimierung verhindern  
  
    -   Verfügbar über die ETW-Ablauf Verfolgung und die Ereignis-ID 1644  
  
        ![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>So aktivieren Sie das stats-Steuerelement in LDP  
  
1.  Öffnen Sie "Ldp. exe", und verbinden und binden Sie einen Domänen Controller.  
  
2.  Klicken Sie im Menü **Optionen** auf Steuer **Elemente**.  
  
3.  Erweitern Sie im Dialogfeld Steuerelemente das Dropdown Menü **Load vordefinierten** , klicken Sie auf **Statistiken suchen** , und klicken Sie dann auf **OK**.  
  
    ![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  Klicken Sie im Menü **Durchsuchen** auf **Suchen** .  
  
5.  Wählen Sie im Dialogfeld Suchen die Schaltfläche **Optionen** aus.  
  
6.  Vergewissern Sie sich, dass im Dialogfeld Suchoptionen das Kontrollkästchen **erweitert** aktiviert ist, und wählen Sie **OK**aus.  
  
    ![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>Versuchen Sie Folgendes: Verwenden von LDP zum Zurückgeben von Abfrage Statistiken  
Führen Sie Folgendes auf einem Domänen Controller oder einem in eine Domäne eingebundenen Client oder Server aus, auf dem die AD DS Tools installiert sind.  Wiederholen Sie die folgenden Punkte für Ihren Windows Server 2012-DC und Ihren Windows Server 2012 R2-DC.  
  
1.  Weitere Informationen finden Sie im Artikel ["erstellen effizienterer Microsoft AD-fähiger Anwendungen"](https://msdn.microsoft.com/library/ms808539.aspx) .  
  
2.  Aktivieren Sie die Such Statistik mithilfe von LDP (siehe so [Aktivieren Sie das stats-Steuerelement in LDP](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats)).  
  
3.  Führen Sie mehrere LDAP-Suchvorgänge durch, und beobachten Sie die statistischen Informationen am Anfang der Ergebnisse.  Die gleiche Suche wird in anderen Aktivitäten wiederholt, sodass Sie in einer Editor-Textdatei dokumentiert werden.  
  
4.  Führen Sie eine LDAP-Suche aus, die der Abfrageoptimierer aufgrund von Attribut Indizes optimieren kann.  
  
5.  Es wurde versucht, eine Suche zu erstellen, die eine lange Zeit in Anspruch nimmt (möglicherweise möchten Sie die **Zeit Limit** -Option erhöhen, sodass die Suche kein Timeout ist).  
  
### <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Was sind Active Directory suchen?](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Funktionsweise von Active Directory suchen](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[Erstellen effizienterer Microsoft Active Directory-fähiger Anwendungen](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP-Abfragen werden langsamer als erwartet im AD-oder LDS/ADAM-Verzeichnisdienst ausgeführt, und die Ereignis-ID 1644 kann protokolliert werden.  
  
## <a name="BKMK_1644"></a>1644 Ereignis Verbesserungen  
  
### <a name="overview"></a>Übersicht  
Dieses Update fügt der Ereignis-ID 1644 zusätzliche Ergebnisse der LDAP-Suchergebnisse hinzu, um die Problembehandlung zu unterstützen.  Außerdem gibt es einen neuen Registrierungs Wert, der verwendet werden kann, um die Protokollierung für einen zeitbasierten Schwellenwert zu aktivieren.  Diese Verbesserungen wurden in Windows Server 2012 und Windows Server 2008 R2 SP1 über KB [2800945](https://support.microsoft.com/kb/2800945) verfügbar gemacht und werden für Windows Server 2008 SP2 zur Verfügung gestellt.  
  
> [!NOTE]  
> -   Der Ereignis-ID 1644 werden zusätzliche LDAP-Such Statistiken hinzugefügt, um die Problembehandlung bei ineffizienten oder teuren LDAP-Suchen  
> -   Sie können jetzt einen Schwellenwert für die Such Zeit angeben (z. b. Protokollieren Sie das Ereignis 1644 für Suchvorgänge, die länger als 100 ms dauern), anstatt die teuren und ineffizienten Suchergebnis Schwellenwerte anzugeben.  
  
### <a name="background"></a>Hintergrund  
Bei der Behandlung von Active Directory Leistungsproblemen wird deutlich, dass die LDAP-Such Aktivität möglicherweise zum Problem beiträgt.  Sie beschließen, die Protokollierung zu aktivieren, damit Sie teure oder ineffiziente LDAP-Abfragen anzeigen können, die vom Domänen Controller verarbeitet werden  Um die Protokollierung zu aktivieren, müssen Sie den Wert für die Feld Engineering-Diagnose festlegen und optional die Schwellenwerte für teure/ineffiziente Suchergebnisse angeben.  Wenn Sie den Protokolliergrad der feldentwicklung auf den Wert 5 aktivieren, wird jede Suche, die diese Kriterien erfüllt, im Verzeichnisdienst-Ereignisprotokoll mit der Ereignis-ID 1644 protokolliert.  
  
Das Ereignis enthält Folgendes:  
  
-   Client-IP und Port  
  
-   Startknoten  
  
-   Filter  
  
-   Suchbereich  
  
-   Attribut Auswahl  
  
-   Server Steuerelemente  
  
-   Besuchte Einträge  
  
-   Zurückgegebene Einträge  
  
Im Ereignis fehlen jedoch Schlüsseldaten, z. b. die Zeitspanne, die für den Suchvorgang aufgewendet wurde, und der (sofern vorhanden) Index.  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>Dem Ereignis 1644 wurden zusätzliche Such Statistiken hinzugefügt.  
  
-   Verwendete Indizes  
  
-   Referenzierte Seiten  
  
-   Vom Datenträger Gelesene Seiten  
  
-   Seiten werden vom Datenträger vorab registriert  
  
-   Geänderte Seiten wurden geändert.  
  
-   Geänderte Seiten geändert  
  
-   Suchzeit  
  
-   Attribute, die Optimierung verhindern  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>Neuer zeitbasierter Schwellenwert Registrierungs Wert für die Protokollierung von Ereignis 1644  
Anstatt die teuren und ineffizienten Suchergebnis Schwellenwerte anzugeben, können Sie den Schwellenwert für die Such Zeit angeben.  Wenn Sie alle Suchergebnisse protokollieren möchten, bei denen mindestens 50 ms benötigt werden, geben Sie 50 Decimal/32 Hex an (zusätzlich zum Festlegen des Field Engineering-Werts).  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>Vergleich der alten und neuen Ereignis-ID 1644  
JÄHRIGEN  
  
![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
NEU  
  
![Verzeichnisdienst Updates](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>Versuchen Sie Folgendes: Verwenden des Ereignis Protokolls zum Zurückgeben von Abfrage Statistiken  
  
1.  Wiederholen Sie die folgenden Punkte für Ihren Windows Server 2012-DC und Ihren Windows Server 2012 R2-DC. Beachten Sie die Ereignis-ID 1644s auf beiden DCS nach jeder Suche.  
  
2.  Aktivieren Sie mithilfe von regedit die Ereignis-ID 1644-Protokollierung mithilfe eines zeitbasierten Schwellenwerts für den Windows Server 2012 R2-DC und die alte Methode auf dem Windows Server 2012-DC.  
  
3.  Führen Sie mehrere LDAP-Suchvorgänge durch, die den Schwellenwert überschreiten, und beobachten Sie die statistischen Informationen am Anfang der Ergebnisse.  Verwenden Sie die zuvor dokumentierten LDAP-Abfragen, und wiederholen Sie die gleichen Suchvorgänge.  
  
4.  Führen Sie eine LDAP-Suche durch, die vom Abfrageoptimierer nicht optimiert werden kann, da mindestens ein Attribut nicht indiziert ist.  
  
## <a name="BKMK_ADRepl"></a>Active Directory Replikations Durchsatz Verbesserung  
  
### <a name="overview"></a>Übersicht  
Die AD-Replikation verwendet RPC für den Replikations Transport. Standardmäßig verwendet RPC einen 8-k-Übertragungs Puffer und eine Paketgröße von 5K. Dies hat den Nettoeffekt, bei dem die sendende Instanz drei Pakete überträgt (ca. 15K Daten) und dann auf einen Netzwerkroundtrip warten muss, bevor mehr gesendet wird. Bei einer Roundtrip-Zeit von 3 MS beträgt der höchste Durchsatz etwa 40 MBit/s, auch bei Netzwerken mit 1 Gbit/s oder 10 Gbit/s.  
  
> [!NOTE]  
> -   Mit diesem Update wird der maximale AD Replication-Durchsatz von 40Mbit/s auf ungefähr 600 MBit/s angepasst.  
>   
>     -   Es erhöht die Größe des RPC-Sendepuffers, wodurch die Anzahl der Netzwerkroundtrips reduziert wird.  
> -   Die Auswirkung auf das Netzwerk mit hoher Geschwindigkeit und hoher Latenz ist am deutlichsten.  
  
Diese Updates erhöhen den maximalen Durchsatz auf ca. 600 MBit/s, indem die RPC-Sendepuffer Größe von 8K in 256 KB geändert wird.  Diese Änderung ermöglicht es, dass die TCP-Fenstergröße über 8K hinaus anwächst und so die Anzahl von Netzwerkroundtrips reduziert.  
  
> [!NOTE]  
> Es gibt keine konfigurierbaren Einstellungen, um dieses Verhalten zu ändern.  
  
### <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Funktionsweise des Active Directory Replikations Modells](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


