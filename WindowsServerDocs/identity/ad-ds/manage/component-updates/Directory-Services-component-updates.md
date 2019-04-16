---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: 'Directory Services: Komponentenupdates'
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac42591450038240ced273555fb01e66b1ff5546
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="directory-services-component-updates"></a>Directory Services: Komponentenupdates

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

**"Author"**: Justin Turner, Senior Support Escalation Engineer mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.  
  
In dieser Lektion wird erläutert, die Directory Services-Komponentenupdates in Windows Server2012 R2.  
  
## <a name="what-you-will-learn"></a>Lernziele  
Erläutern Sie die folgenden neuen Verzeichnisdienste Komponentenupdates zu suchen:  
  
-   Erläutern Sie die folgenden neuen Verzeichnisdienste Komponentenupdates zu suchen:  
  
    -   [Domänen- und Gesamtstrukturfunktionsebenen](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [Abschreibung von NTFRS](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [Änderungen des LDAP-Abfrageoptimierer](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [Ereignis 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Durchsatzverbesserung bei der Active Directory-Replikation](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="BKMK_FL"></a>Domänen- und Gesamtstrukturfunktionsebenen  
  
### <a name="overview"></a>(Übersicht)  
Der Abschnittenthält eine kurze Einführung in die Domänen- und Gesamtstrukturfunktionsebene auf Systemebene Änderungen.  
  
### <a name="new-dfl-and-ffl"></a>Neue DFL und FFL  
Es gibt neue Domänen- und Gesamtstrukturfunktionsebenen, mit der Veröffentlichung:  
  
-   Gesamtstrukturfunktionsebene: Windows Server2012 R2  
  
-   Die Domänenfunktionsebene: Windows Server2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server2012 R2 als Domänenfunktionsebene ermöglicht die Unterstützung für Folgendes:  
  
1.  DC-Seite Schutzmaßnahmen für *geschützte Benutzer*  
  
    *Geschützte Benutzer* Authentifizierung gegenüber einer Domäne Windows Server2012 R2 kann **nicht mehr**:  
  
    -   Authentifizieren mit NTLM-Authentifizierung  
  
    -   Verwenden von des- oder RC4-Verschlüsselungssammlungen in Kerberos-Vorauthentifizierung  
  
    -   Mit uneingeschränkter oder eingeschränkter Delegierung delegiert werden  
  
    -   Erneuern von Benutzertickets (TGTs) über die ersten 4 Stunden hinaus  
  
2.  Authentifizierungsrichtlinien  
  
    Neue Gesamtstruktur-Active Directory-Richtlinien die auf Konten in Windows Server2012 R2-Domänen zu steuern, welche Hosts angewendet werden können ein Konto kann aus anmelden und gelten zugriffssteuerungsbedingungen zur Authentifizierung für Dienste, die mit einem Konto ausgeführt werden.  
  
3.  Authentifizierungsrichtliniensilos  
  
    Neue Gesamtstruktur-basierten Active Directory-Objekt die eine Beziehung zwischen Benutzer, verwaltete und Computerkonten verwendet werden, die Konten für Authentifizierungsrichtlinien oder für die Authentifizierung Isolation klassifizieren erstellen können.  
  
Weitere Informationen finden Sie unter Konfigurieren geschützter Konten für Weitere Informationen.  
  
Zusätzlich zu den oben genannten Features gewährleistet die Domänenfunktionsebene Windows Server2012 R2, dass alle Domänencontroller in der Domäne mit Windows Server2012 R2 ausgeführt wird.  
Die Windows Server2012 R2-Gesamtstrukturfunktionsebene bietet neuen Funktionen, aber es wird sichergestellt, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf die Domänenfunktionsebene Windows Server2012 R2.  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>Minimale Domänenfunktionsebene erzwungen, auf die Erstellung einer neuen Domäne  
Windows Server2008-Domänenfunktionsebene ist mindestens die Funktionsebene der Erstellung einer neuen Domäne unterstützt.  
  
> [!NOTE]  
> Die Ablehnung von FRS erfolgt durch das Entfernen der Möglichkeit, eine neue Domäne mit einer Domänenfunktionsebene, die niedriger als Windows Server2008 mit Server-Manager oder über Windows PowerShell zu installieren.  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>Verringern die Funktionsebenen der Gesamtstruktur und Domäne  
Funktionsebenen der Gesamtstruktur und Domäne werden auf Windows Server2012 R2 standardmäßig auf die Erstellung einer neuen Domäne und neue Gesamtstruktur jedoch mithilfe von Windows PowerShell gesenkt werden können.  
  
Verwenden Sie zum Erhöhen oder verringern die Gesamtstrukturfunktionsebene auf Windows PowerShell verwenden, die **Set-ADForestMode** Cmdlet.  
  
**So setzen die contoso.com FFL auf Windows Server2008-Modus:**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Um zu erhöhen oder verringern die Domänenfunktionsebene auf Windows PowerShell verwenden, verwenden Sie das Cmdlet Set-ADDomainMode.  
  
**So setzen die contoso.com Domänenfunktionsebene auf Windows Server2008-Modus:**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
Heraufstufen eines Domänencontrollers unter Windows Server2012 R2 als ein zusätzliches Replikat in einer vorhandenen Domäne DFL 2003 ausführen kann.  
  
Erstellung einer neuen Domäne in einer vorhandenen Gesamtstruktur  
  
![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
Es gibt keine neue Gesamtstruktur oder Domäne Vorgänge in dieser Version.  
  
Diese LDF-Dateien enthalten Schemaänderungen für die **Device Registration Service**.  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**Arbeitsordner:**  
  
1.  Sch66  
  
**MSODS:**  
  
1.  Sch60  
  
**Authentifizierungsrichtlinien und Silos**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="BKMK_NTFRS"></a>Abschreibung von NTFRS  
  
### <a name="overview"></a>(Übersicht)  
FRS ist in Windows Server2012 R2 als veraltet.  Die Ablehnung von FRS erfolgt durch das Erzwingen einer minimalen Domänenfunktionsebene (DFL) von Windows Server2008.  Diese Voraussetzung ist nur vorhanden, wenn die neue Domäne mithilfe von Server-Manager oder Windows PowerShell erstellt wird.  
  
Mit den Cmdlets Install-ADDSForest oder Install-ADDSDomain verwenden Sie den DomainMode - Parameter, die Domänenfunktionsebene an.  Unterstützte Werte für diesen Parameter können es sich um eine gültige ganze Zahl oder einen entsprechenden Wert für die aufgelisteten Zeichenfolge sein. Zum Festlegen der Domänenebene für den Modus für Windows Server2008 R2 können Sie z.B. ein Wert von 4 oder %% Win2008R2"angeben.  Beim Ausführen dieser Cmdlets in Server2012 R2 gültige Werte sind für Windows Server2008 (3, Win2008) Windows Server2008 R2 (4, Win2008R2) Windows Server2012 (5, Win2012) und Windows Server2012 R2 (6, Win2012R2). Die Domänenfunktionsebene kann nicht niedriger als die Gesamtstrukturfunktionsebene auf kann, es jedoch höher.  Da FRS in dieser Version, Windows Server2003 (2, Win2003) veraltet ist ist kein erkannter Parameter mit diesen Cmdlets bei der Ausführung von Windows Server2012 R2.  
  
![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>Änderungen des LDAP-Abfrageoptimierer  
  
### <a name="overview"></a>(Übersicht)  
Der LDAP-Abfrageoptimierer-Algorithmus wurde neu ausgewertet und weiter optimiert.  Das Ergebnis ist die Leistungsverbesserung LDAP-Suche und bessere Suchzeiten bei komplexen Abfragen.  
  
> [!NOTE]  
> **Vom Entwickler:**Verbesserungen in Bezug auf die Leistung durchsucht Verbesserungen bei der Zuordnung von LDAP-Abfragen ESE-Abfrage.  LDAP-Filter über eine gewisse Komplexität zu verhindern, dass optimierten Index-Auswahl, drastisch Performance verringert (1000 X oder mehr). Diese Änderung ändert die Art und Weise, in der wir die Indizes für die LDAP-Abfragen zur Vermeidung dieses Problems auswählen.  
  
> [!NOTE]  
> Der LDAP-Abfrageoptimierer Algorithmus, was zu erfahren:  
>   
> -   Schnelleres Suchen  
> -   Effizienz können DCs mehr erreichen  
> -   Weniger Supportanrufe Probleme hinsichtlich AD-Leistung  
> -   Zurück zu Windows Server2008 R2 (KB 2862304) portiert  
  
### <a name="background"></a>Hintergrund  
Die Möglichkeit zum Durchsuchen von Active Directory ist ein Kerndienst, die vom Domänencontroller bereitgestellten.  Andere Dienste und Branchenanwendungen abhängig von Active Directory-Suche.  Wenn dieses Feature nicht verfügbar ist, können zum Stillstand Geschäftsvorgänge einzustellen.  Als Core und sehr häufig verwendete Service ist es unbedingt notwendig, dass Domänencontroller effizient LDAP-Suche-Datenverkehr behandeln.  Der LDAP-Abfrageoptimierer Algorithmus versucht, stellen Sie möglichst effizient LDAP-Suchvorgänge durch Zuordnen von LDAP-Suchfilter zu einem Resultset, die über Datensätze, die bereits in der Datenbank indiziert erfüllt werden kann.  Dieser Algorithmus wurde neu ausgewertet und weiter optimiert.  Das Ergebnis ist die Leistungsverbesserung LDAP-Suche und bessere Suchzeiten bei komplexen Abfragen.  
  
### <a name="details-of-change"></a>Detail der Änderung  
Eine LDAP-Suche enthält:  
  
-   Ein Speicherort (NC-Kopf, Organisationseinheit, Objekt) in der Hierarchie, um die Suche zu starten  
  
-   Suchfilter  
  
-   Eine Liste der Attribute zurückgegeben  
  
Der Search-Prozess kann wie folgt zusammengefasst werden:  
  
1.  Vereinfachen Sie nach Möglichkeit den Suchfilter.  
  
2.  Wählen Sie einen Satz von Index-Schlüssel, der die kleinste abgedeckte Gruppe zurückgibt.  
  
3.  Führen Sie einen oder mehrere kreuzungen Index-Schlüssel, um den betroffenen Satz zu reduzieren.  
  
4.  Bewerten Sie für jeden Datensatz in der betroffenen Satz der Filterausdruck als auch die Sicherheit. Wenn der Filter zu TRUE ausgewertet wird, und Zugriff gewährt wird, wird zurückgegeben Sie dieser Eintrag an den Client.  
  
Die LDAP-Abfrage Optimierung Arbeit ändert die Schritte2 und 3, zum Reduzieren der Größe des betroffenen ein. Genauer gesagt, die aktuelle Implementierung wählt doppelten Index-Schlüssel und redundante kreuzungen führt.  
  
### <a name="comparison-between-old-and-new-algorithm"></a>Vergleich zwischen der alten und neuen Algorithmus  
Das Ziel der ineffizient LDAP-Suche in diesem Beispiel ist ein Windows Server2012-Domänencontroller.  Die Suche in etwa 44Sekunden als Ergebnis findet einen effizienteren Index abgeschlossen ist.  
  
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
  
### <a name="sample-results-using-the-new-algorithm"></a>Beispiel für die Ergebnisse mit dem neuen  
In diesem Beispiel wiederholt die exakte gleiche Suche wie oben jedoch ausgerichtet ist einen Windows Server2012 R2-Domänencontroller.  In weniger als einer Sekunde aufgrund von Verbesserungen bei der LDAP-Abfrageoptimierer Algorithmus ist die gleiche Suche abgeschlossen.  
  
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
  
-   Wenn nicht, um die Struktur zu optimieren:  
  
    -   Beispiel: ein Ausdruck in der Struktur für eine Spalte nicht indiziert wurde  
  
    -   Zeichnen Sie eine Liste der Indizes, die eine Optimierung verhindern  
  
    -   Über die ETW-Ablaufverfolgung und der Ereignis-ID 1644 verfügbar gemacht  
  
        ![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>So aktivieren Sie das Steuerelement Statistiken in "Ldp"  
  
1.  Öffnen Sie LDP.exe, und Verbindung und eine Bindung zu einem Domänencontroller.  
  
2.  Auf der **Optionen** Menü klicken Sie auf **Steuerelemente**.  
  
3.  Erweitern Sie im Dialogfeld Steuerelemente der **laden vordefinierte** Pull-Down-Menü, klicken Sie auf **Suche Statistiken**, und klicken Sie dann auf **OK**.  
  
    ![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  Auf der **Durchsuchen** Menü klicken Sie auf **suchen**  
  
5.  Wählen Sie im Dialogfeld "Suchen" den **Optionen** Schaltfläche.  
  
6.  Stellen Sie sicher das **Extended** Kontrollkästchen im Dialogfeld Suchoptionen und wählen **OK**.  
  
    ![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>Versuchen Sie Folgendes: Verwendung LDP Abfragestatistiken zurückgegeben.  
Führen Sie die folgenden auf einem Domänencontroller oder eine Domäne eingebundenen Client oder Server, auf die AD DS-Tools installiert ist.  Wiederholen Sie die folgenden auf Ihrem Windows Server2012-Domänencontroller und der Windows Server2012 R2-Domänencontroller ausgerichtet.  
  
1.  Überprüfen der ["Creating mehr effizient Microsoft AD aktiviert Applications"](https://msdn.microsoft.com/library/ms808539.aspx) Artikel, und verweisen Sie bei Bedarf wieder zu.  
  
2.  Mithilfe von "Ldp", aktivieren Sie Statistik (finden Sie unter [So aktivieren Sie das Steuerelement Statistiken im LDP](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats))  
  
3.  Durchführen Sie mehrere LDAP-Suchvorgänge, und beobachten Sie die statistische Informationen am oberen Rand der Ergebnisse.  Wiederholen Sie die gleiche Suche in anderen Aktivitäten dokumentieren sie also in einer Editor-Textdatei.  
  
4.  Führen Sie eine LDAP-Suche, die der Abfrageoptimierer aufgrund von Attributen Indizes optimieren werden sollen  
  
5.  Eine Suche zu erstellen, die eine lange Zeit in Anspruch nimmt (Sie erhöhen möchten die **Zeitlimit** Option, damit die Suche nicht über ein Timeout verfügt).  
  
### <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Was sind Active Directory-Suche?](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Wie Active Directory-Arbeit Suchvorgänge](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[Erstellen eine effizientere Microsoft Active Directory-fähige Anwendungen](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP-Abfragen werden langsamer als erwartet in AD oder LDS/ADAM-Verzeichnisdienst und Ereignis-ID 1644 protokolliert werden können  
  
## <a name="BKMK_1644"></a>Ereignis 1644  
  
### <a name="overview"></a>(Übersicht)  
Dieses Update wird Ereignis-ID 1644 zur Fehlerbehebung bei Zwecke zusätzliche LDAP-Suche Statistiken hinzugefügt.  Es ist darüber hinaus ein neuen Registrierungswert, der die Protokollierung auf einem Schwellenwert zeitbasierte verwendet werden kann.  Diese Verbesserungen in Windows Server2012 und Windows Server2008 R2 SP1 über KB zur Verfügung gestellt wurden [2800945](https://support.microsoft.com/kb/2800945) und wird für Windows Server2008 SP2 verfügbar gemacht werden.  
  
> [!NOTE]  
> -   Ereignis-ID 1644 zur Fehlerbehebung bei ineffizient oder teure LDAP-Suchvorgänge werden zusätzliche LDAP-Suche-Statistiken hinzugefügt.  
> -   Sie können nun angeben einer Suchdauer-Schwellenwert (z. b. Protokollereignis 1644 für die Suche, die länger als 100 ms) anstatt kostspielig und ineffizient Ergebnis Schwellenwert Suchwerte anzugeben  
  
### <a name="background"></a>Hintergrund  
Bei der Problembehandlung für Active Directory-Leistungsprobleme, wird deutlich, dass LDAP-Suche Aktivität des Problems beitragen kann.  Aktivieren Sie die Protokollierung, damit Sie sehen können, teure oder ineffiziente LDAP-Abfragen, die vom Domänencontroller verarbeitet werden sollen.  Um die Protokollierung zu aktivieren, müssen Sie den Produktsupport Diagnose-Wert und können optional die teure / ineffizient Suche Ergebnisse Schwellenwerte angeben.  Beim Aktivieren der Produktsupport Protokolliergrad auf einen Wert von 5, wird eine Suche, die diese Kriterien erfüllen im Verzeichnisdienste-Ereignisprotokoll mit einem Ereignis-ID 1644 protokolliert.  
  
Das Ereignis enthält:  
  
-   Client IP und Port  
  
-   Knoten starten  
  
-   Filter  
  
-   Suchbereich  
  
-   Attribut-Auswahl  
  
-   Serversteuerelemente  
  
-   Besuchten Einträge  
  
-   Zurückgegebenen Einträge  
  
Wichtige Daten ist jedoch nicht in das Ereignis Index wurde verwendet, z.B. die Zeit auf dem Suchvorgang wird und was (sofern vorhanden) verbracht wurde.  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>Zusätzliche Statistik-Ereignis 1644 hinzugefügt  
  
-   Verwendete Indizes  
  
-   Seiten verwiesen wird  
  
-   Seiten vom Datenträger gelesen.  
  
-   Seiten vom Datenträger preread  
  
-   Saubere Seiten geändert  
  
-   Fehlerhafte Seiten geändert  
  
-   Zeit für Suche  
  
-   Attribute, die verhindern, dass die Optimierung  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>Neue zeitbasierte Registrierung Schwellenwert für die Protokollierung von Ereignis 1644  
Geben Sie anstelle der kostspielig und ineffizient Ergebnis Schwellenwert Suchwerte Suchdauer-Schwellenwert.  Wenn Sie sich alle Suchergebnisse die 50 ms benötigte erwünscht oder größer, Sie geben 50 decimal / 32 hex (zusätzlich zu den Produktsupport Wert festlegen).  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>Vergleich der alten und neuen Ereignis-ID 1644  
ALTE  
  
![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
Neu  
  
![Updates für die Verzeichnisdienste](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>Versuchen Sie Folgendes: Verwenden Sie das Ereignisprotokoll, um Abfragestatistiken zurückzugeben  
  
1.  Wiederholen Sie die folgenden auf Ihrem Windows Server2012-Domänencontroller und der Windows Server2012 R2-Domänencontroller ausgerichtet. Beachten Sie die Ereignis-ID 1644s auf beiden Domänencontrollern nach jeder Suche.  
  
2.  Verwenden "regedit" ein, aktivieren Sie einen Schwellenwert zeitbasierte auf dem Windows Server2012 R2-Domänencontroller und die alte Methode für die Windows Server2012-Domänencontroller mit Ereignis-ID 1644 Protokollierung.  
  
3.  Führen Sie mehrere LDAP-Suchvorgänge, die den Schwellenwert überschreitet, und beobachten Sie die statistische Informationen am oberen Rand der Ergebnisse.  Verwenden Sie die LDAP-Abfragen, die Sie weiter oben beschrieben, und wiederholen Sie die gleichen suchen.  
  
4.  Führen Sie eine LDAP-Suche, der der Abfrageoptimierer nicht optimieren, da ein oder mehrere Attribute nicht indiziert werden.  
  
## <a name="BKMK_ADRepl"></a>Durchsatzverbesserung bei der Active Directory-Replikation  
  
### <a name="overview"></a>(Übersicht)  
Active Directory-Replikation verwendet RPC für die Replikationstransport. Standardmäßig wird RPC verwendet, ein 8 KB-Puffer übertragen und eine 5 KB-Paketgröße. Dies hat den Effekt, in dem die sendende Instanz drei Pakete (etwa 15KB zu Daten) übertragen, und klicken Sie dann Roundtrip für ein Netzwerk warten, bevor Sie mehr senden müssen. Sofern eine 3ms Roundtrip-Zeit, wäre die höchste Durchsatz um 40Mbps, auch auf 1 Gbit/s oder 10 Gbit/s-Netzwerke.  
  
> [!NOTE]  
> -   Dieses Update wird den maximalen Durchsatz Active Directory-Replikation von 40Mbps auf ca. 600 Mbps angepasst.  
>   
>     -   Erhöht die RPC-Größe des Sendepuffers die reduziert die Anzahl der Roundtrips  
> -   Der Effekt werden besonders deutlich auf hoher Geschwindigkeit Netzwerk mit hoher Latenz.  
  
Diese Updates Erhöhen der maximalen Durchsatz auf ca. 600 Mbps durch Ändern der Größe des Sendepuffers RPC von 8KB auf 256KB.  Durch diese Änderung kann die TCP-Fenstergröße an überschreitet 8KB, Reduzieren der Anzahl der Netzwerk-Netzwerkroundtrips.  
  
> [!NOTE]  
> Es gibt keine Einstellungen konfiguriert, um dieses Verhalten zu ändern.  
  
### <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Wie funktioniert das Modell der Active Directory-Replikation](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


