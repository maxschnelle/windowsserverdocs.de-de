---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: Directory Services-Komponentenupdates
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fe27b61abe196a2148ced18806be904ebd555fcc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442889"
---
# <a name="directory-services-component-updates"></a>Directory Services-Komponentenupdates

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autor**: Justin Turner, Senior Support Escalation Engineer für die Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
In dieser Lektion wird erläutert, die Verzeichnisdienste Aktualisierungen von Komponenten in Windows Server 2012 R2.  
  
## <a name="what-you-will-learn"></a>Lernziele  
Erläutern Sie die folgenden neuen Directory Services-Komponentenupdates:  
  
-   Erläutern Sie die folgenden neuen Directory Services-Komponentenupdates:  
  
    -   [Domänen- und Gesamtstrukturfunktionsebenen](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [Abschreibung von NTFRS](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [Änderungen am LDAP-Abfrageoptimierer](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [Verbesserungen am Ereignis 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Durchsatzverbesserung bei der Active Directory-Replikation](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="BKMK_FL"></a>Domänen- und Gesamtstruktur-Funktionsebenen  
  
### <a name="overview"></a>Übersicht  
Der Abschnitt enthält eine kurze Einführung in die Domäne und Gesamtstruktur funktionale Änderungen auf Anwendungsebene.  
  
### <a name="new-dfl-and-ffl"></a>Neue Domänenfunktionsebene und FFL  
Es gibt neue Domänen- und Gesamtstruktur-Funktionsebenen, mit der Version:  
  
-   Gesamtstrukturfunktionsebene: Windows Server 2012 R2  
  
-   Domänen-Funktionsebene: Windows Server 2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server 2012 R2 Funktionsebene der Domäne ermöglicht die Unterstützung für Folgendes:  
  
1.  DC-Seite Schutzmaßnahmen für *geschützte Benutzer*  
  
    *Geschützte Benutzer* Authentifizierung gegenüber einer Domäne Windows Server 2012 R2 kann **mehr**:  
  
    -   Authentifizieren mit NTLM-Authentifizierung  
  
    -   Verwenden von des- oder RC4-Verschlüsselungssammlungen in Kerberos-vorabauthentifizierung  
  
    -   Mit uneingeschränkter oder eingeschränkter Delegierung delegiert werden  
  
    -   Erneuern von Benutzertickets (TGTs) nach Ablauf der Lebensdauer der ersten 4 Stunden  
  
2.  Authentifizierungsrichtlinien  
  
    Neue Gesamtstruktur-basierten Active Directory-Richtlinien die Konten in Windows Server 2012 R2-Domänen zu steuern, welche Hosts angewendet werden können ein Konto kann aus anmelden und Anwenden von Bedingungen für die Zugriffssteuerung für die Authentifizierung an Dienste, die mit einem Konto ausgeführt  
  
3.  Authentifizierungsrichtliniensilos  
  
    Neue Gesamtstruktur-basierten Active Directory-Objekt die eine Beziehung zwischen Benutzer, verwalteter Dienst, und Computerkonten, zum Klassifizieren von Konten für Authentifizierungsrichtlinien oder für die Authentifizierung Isolation verwendet werden soll, erstellen können.  
  
Finden Sie unter Konfigurieren geschützter Konten für Weitere Informationen.  
  
Zusätzlich zu den oben genannten Features gewährleistet die Domänenfunktionsebene Windows Server 2012 R2, dass alle Domänencontroller in der Domäne auf Windows Server 2012 R2 ausgeführt wird.  
Die Gesamtstrukturfunktionsebene Windows Server 2012 R2 bietet keine neuen Features, aber es wird sichergestellt, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf die Domänenfunktionsebene von Windows Server 2012 R2 ausgeführt wird.  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>Minimale Domänenfunktionsebene erzwungen, die bei der Erstellung der neuen Domäne  
Windows Server 2008-Domänenfunktionsebene ist die minimale Funktionsebene für die Erstellung der neuen Domäne unterstützt.  
  
> [!NOTE]  
> Veralten des Dateireplikationsdiensts (FRS) erfolgt durch das Entfernen der Möglichkeit, eine neue Domäne mit einer Domänenfunktionsebene auf, die niedriger als Windows Server 2008 mit Server-Manager oder über Windows PowerShell zu installieren.  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>Verringern die Funktionsebenen der Gesamtstruktur und Domäne  
Die Funktionsebenen der Gesamtstruktur und Domäne, die für Windows Server 2012 R2 wird standardmäßig auf die Erstellung einer neuen Domäne und Gesamtstruktur festgelegt werden, aber können mithilfe von Windows PowerShell verringert werden.  
  
Verwenden Sie zum Erhöhen oder verringern die Gesamtstrukturfunktionsebene auf mithilfe von Windows PowerShell, die **Set-ADForestMode** Cmdlet.  
  
**So setzen die "contoso.com" FFL auf Windows Server 2008-Modus:**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Zum Erhöhen oder verringern die Domänenfunktionsebene auf Windows PowerShell verwenden, verwenden Sie das Cmdlet Set-ADDomainMode.  
  
**So legen Sie die Domänenfunktionsebene von "contoso.com" in Windows Server 2008-Modus fest**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
Heraufstufen eines Domänencontrollers unter Windows Server 2012 R2 als ein zusätzliches Replikat in einer vorhandenen Domäne DFL (2003) ausführen kann.  
  
Erstellung einer neuen Domäne in einer vorhandenen Gesamtstruktur  
  
![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
Es gibt keine neue Gesamtstruktur oder Domänenvorgänge in dieser Version.  
  
Diese LDF-Dateien enthalten, schemaänderungen, die für die **Device Registration Service**.  
  
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
  
### <a name="overview"></a>Übersicht  
Dateireplikationsdienst (FRS) ist in Windows Server 2012 R2 als veraltet markiert.  Veralten des Dateireplikationsdiensts (FRS) erfolgt durch Erzwingen einer minimalen Domänenfunktionsebene (DFL) von Windows Server 2008.  Diese Voraussetzung ist nur vorhanden, wenn die neue Domäne mithilfe von Server-Manager oder Windows PowerShell erstellt wird.  
  
Können Sie den Domänenmodus - Parameter mit dem Install-ADDSForest oder Install-ADDSDomain Cmdlets Geben Sie die Domänenfunktionsebene auf.  Unterstützte Werte für diesen Parameter können entweder eine gültige ganze Zahl oder einen entsprechenden Wert der aufgelisteten Zeichenfolge sein. Um die modusebene der Domäne auf Windows Server 2008 R2 festgelegt werden soll, können Sie z. B. ein Wert von 4 oder "Win2008R2" angeben.  Beim Ausführen dieser Cmdlets von Server 2012 R2 gültige Werte sind für Windows Server 2008 (3, Win2008) Windows Server 2008 R2 (4, Win2008R2) Windows Server 2012 (5, Win2012) und Windows Server 2012 R2 (6, Win2012R2). Die Domänenfunktionsebene kann nicht niedriger als die Funktionsebene der Gesamtstruktur sein. Sie kann jedoch höher sein.  Da FRS, in dieser Version, Windows Server 2003 (2, Win2003 veraltet ist) ist kein erkannter Parameter mit diesen Cmdlets, die beim Ausführen von Windows Server 2012 R2.  
  
![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>Änderungen des LDAP-Abfrageoptimierer  
  
### <a name="overview"></a>Übersicht  
Der LDAP-Abfrage-Optimierer-Algorithmus wurde neu ausgewertet und weiter optimiert.  Das Ergebnis ist die Verbesserung der Leistung in LDAP-Suche und LDAP-Suchdauer komplexer Abfragen.  
  
> [!NOTE]
> <strong>Seitens des Entwicklers:</strong>Verbesserungen in Bezug auf die Leistung Suchvorgänge in Verbesserungen in der Zuordnung von LDAP-Abfragen auf das ESE-Abfrage.  LDAP-Filter über ein gewisses Maß an Komplexität zu verhindern, dass optimierter Index-Auswahl, drastisch verringert die Leistung beeinträchtigt (1000 X oder mehr). Diese Änderung ändert die Weise, in der Bereich wir die Indizes für die LDAP-Abfragen wählen, um dieses Problem zu vermeiden.  
> 
> [!NOTE]
> Vollständige Überarbeitung des LDAP-Abfrage-Optimierer-Algorithmus, was zu:  
> 
> -   Schnellere Suche  
> -   Effizienz können DCs mehr zu erreichen  
> -   Weniger Supportanrufe Probleme in Bezug auf AD-Leistung  
> -   Zurück zu Windows Server 2008 R2 (KB 2862304) portiert  
  
### <a name="background"></a>Hintergrund  
Die Möglichkeit, Active Directory zu suchen ist ein Basisdienst, der von Domänencontrollern bereitgestellt.  Andere Dienste und LOB-Anwendungen, abhängig von Active Directory-Suche ab.  Business-Vorgänge können zum Stillstand beendet, wenn dieses Feature nicht verfügbar ist.  Als Kern und häufig verwendete Service ist es zwingend erforderlich, dass Domänencontroller LDAP-suchdatenverkehr effizient zu verarbeiten.  Der LDAP-Abfrage-Optimierer-Algorithmus versucht, LDAP-Suchvorgänge effizient wie möglich durch Zuordnen von LDAP-Suchfilter auf einem Resultset, die über die Datensätze in der Datenbank bereits indiziert erfüllt werden.  Dieser Algorithmus wurde neu ausgewertet und weiter optimiert.  Das Ergebnis ist die Verbesserung der Leistung in LDAP-Suche und LDAP-Suchdauer komplexer Abfragen.  
  
### <a name="details-of-change"></a>Details der Änderung  
Eine LDAP-Suche enthält:  
  
-   Eine Position (NC-Kopf, OU, Objekt) der Hierarchie, um die Suche zu starten  
  
-   Ein Suchfilter  
  
-   Eine Liste der zurückzugebenden Attribute an  
  
Der Suchprozess kann wie folgt zusammengefasst werden:  
  
1.  Vereinfachen Sie wenn möglich den Suchfilter.  
  
2.  Wählen Sie einen Satz von Indexschlüssel, die die kleinste, abgedeckte Menge zurückgibt.  
  
3.  Führen Sie eine oder mehrere Schnittpunkte Indexschlüssel, abgedeckte festgelegtem zu reduzieren.  
  
4.  Für jeden Datensatz in der betroffenen Menge ausgewertet werden sowohl der Filter-Ausdruck als auch die Sicherheit. Wenn der Filter auf "true" ausgewertet wird, und der Zugriff wird gewährt, klicken Sie dann zurückgeben Sie diesen Datensatz an den Client.  
  
Die LDAP-Abfrage-Optimierungsaufgaben ändert die Schritte 2 und 3, zum Verringern der Größe der abgedeckte Menge. Genauer gesagt wird die aktuelle Implementierung wählt Doppelte Indexschlüssel und redundante Schnittpunkte führt.  
  
### <a name="comparison-between-old-and-new-algorithm"></a>Vergleich zwischen den alten und neuen Algorithmus  
Das Ziel der ineffizienten LDAP-Suche in diesem Beispiel ist ein Windows Server 2012-Domänencontroller.  In ungefähr 44 Sekunden aufgrund einen effizienteren Index nicht findet, wird die Suche abgeschlossen.  
  
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
  
### <a name="sample-results-using-the-new-algorithm"></a>Beispielergebnisse mit den neuen Algorithmus  
In diesem Beispiel wird wiederholt, die genaue gleiche Suche wie oben, jedoch ist einen Windows Server 2012 R2-Domänencontroller.  Die gleiche Suche, die in weniger als einer Sekunde aufgrund der verbesserten im LDAP-Abfrage-Optimierer Algorithmus abgeschlossen werden.  
  
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
  
-   Wenn dies nicht möglich, um die Struktur zu optimieren:  
  
    -   Zum Beispiel: ein Ausdruck in der Struktur wurde für eine nicht indizierte Spalte  
  
    -   Zeichnen Sie eine Liste von Indizes, die verhindern, Optimierung  
  
    -   Über ETW-Ablaufverfolgung und Ereignis-ID 1644 verfügbar gemacht  
  
        ![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>So aktivieren Sie die Stats-Steuerelement in "Ldp"  
  
1.  Öffnen Sie LDP.exe und Verbindung und eine Bindung zu einem Domänencontroller.  
  
2.  Auf der **Optionen** Menü klicken Sie auf **Steuerelemente**.  
  
3.  Erweitern Sie auf das Dialogfeld Steuerelemente, die **Load Predefined** Pulldown-Menü, klicken Sie auf **Suchstatistik** , und klicken Sie dann auf **OK**.  
  
    ![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  Auf der **Durchsuchen** Menü klicken Sie auf **suchen**  
  
5.  Wählen Sie in das Dialogfeld Suchen, die **Optionen** Schaltfläche.  
  
6.  Stellen Sie sicher die **erweiterte** das Kontrollkästchen aktiviert ist, auf die Durchsuchen-Optionen (Dialogfeld), und wählen **OK**.  
  
    ![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>Versuchen Sie Folgendes aus: Verwenden Sie "Ldp" zum Zurückgeben von Abfragestatistiken  
Führen Sie die folgenden Schritte aus, auf einem Domänencontroller oder eine Domäne eingebundenen Client oder Server, auf die AD DS-Tools installiert ist.  Wiederholen Sie die folgenden für Ihre Windows Server 2012-Domänencontroller und Ihre Windows Server 2012 R2-Domänencontroller.  
  
1.  Überprüfen Sie die ["Erstellen von mehr effizienten Microsoft AD aktiviert Anwendungen"](https://msdn.microsoft.com/library/ms808539.aspx) Artikel und darauf zurückgreifen je nach Bedarf.  
  
2.  Verwendung von "Ldp" Suchstatistik aktivieren (finden Sie unter [So aktivieren Sie die Stats-Steuerelement in "Ldp"](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats))  
  
3.  Durchführen Sie mehrere LDAP-Suchvorgänge, und beobachten Sie die statistische Informationen am Anfang der Ergebnisse.  Sie werden wiederholt, die gleiche Suche in anderen Aktivitäten dokumentieren sie also in einer Editor-Textdatei.  
  
4.  Führen Sie eine LDAP-Suche, die die Abfrageoptimierer aufgrund von Attributen Indizes optimiert werden soll  
  
5.  Versucht, eine Suche zu erstellen, die eine lange Zeit in Anspruch nimmt (Sie erhöhen möchten die **Zeitlimit** option aus, damit die Suche nicht zu einem Timeout führt).  
  
### <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Was sind Active Directory-Suche?](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Wie das Durchsuchen von Active Directory-Aufgaben](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[Erstellen eine effizientere Microsoft Active Directory-fähige Anwendungen](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP-Abfragen werden langsamer als erwartet in AD oder LDS/ADAM-Verzeichnisdienst und Ereignis-ID 1644 kann protokolliert werden  
  
## <a name="BKMK_1644"></a>Verbesserungen am Ereignis 1644  
  
### <a name="overview"></a>Übersicht  
Dieses Update fügt zusätzliche LDAP-Suche Statistiken auf Ereignis-ID 1644 zur Unterstützung der Problembehandlung zu.  Es ist außerdem ein neuen Registrierungswert, der zum Aktivieren der Protokollierung auf einem Schwellenwert zeitbasierte verwendet werden kann.  Diese Verbesserungen wurden in Windows Server 2012 und Windows Server 2008 R2 SP1 über KB [2800945](https://support.microsoft.com/kb/2800945) und wird auf Windows Server 2008 SP2 verfügbar gemacht werden.  
  
> [!NOTE]  
> -   Ereignis-ID 1644 zur Fehlerbehebung bei ineffizient oder teure LDAP-Suchvorgänge werden zusätzliche Statistiken der LDAP-Suche hinzugefügt.  
> -   Sie können jetzt eine Suchdauer-Schwellenwert (z.B.) angeben. Log-Ereignis 1644 für Suchvorgänge, die mehr als 100 ms) anstatt die kostspielig und ineffizient. Search-Ergebnis-Schwellenwerte  
  
### <a name="background"></a>Hintergrund  
Bei der Problembehandlung von Leistungsproblemen von Active Directory wird deutlich, dass der LDAP-Suchvorgänge des Problems beitragen kann.  Sie beschließen, aktivieren Sie die Protokollierung, damit Sie sehen können, teuer oder ineffiziente LDAP-Abfragen, die vom Domain Controller verarbeitet werden.  Um die Protokollierung zu aktivieren, Sie müssen den Field Engineering-Diagnose-Wert festlegen und können optional die teure / ineffizient Suche Ergebnisse Schwellenwerte angeben.  Beim Aktivieren der Field Engineering-Protokolliergrad festlegen auf einen Wert von 5, wird Suche, die diese Kriterien erfüllt im Verzeichnisdienste-Ereignisprotokoll mit einem Ereignis-ID 1644 protokolliert.  
  
Das Ereignis enthält:  
  
-   Client-IP- und -Port  
  
-   Startknoten  
  
-   Filter  
  
-   Suchbereich  
  
-   Attribut-Auswahl  
  
-   Serversteuerelemente  
  
-   Besuchten Einträge  
  
-   Zurückgegebenen Entitäten  
  
Jedoch wichtige Daten fehlt das Ereignis wie z. B. die den Suchvorgang und für welche (sofern vorhanden) aufgewendete Zeit Index verwendet wurde.  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>Zusätzliche Suchbedingung Statistics-Ereignis 1644 hinzugefügt  
  
-   Verwendete Indizes  
  
-   Seiten, die auf die verwiesen wird  
  
-   Vom Datenträger gelesenen Seiten  
  
-   Seiten vom Datenträger preread  
  
-   Modifizierte Seiten geändert  
  
-   Modifizierte Seiten geändert  
  
-   Zeit für Suche  
  
-   Attribute, die Optimierung verhindern  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>Neuen zeitbasierte Registrierung Schwellenwert für die Protokollierung von Ereignis 1644  
Anstatt die kostspielig und ineffizient. Search-Ergebnis-Schwellenwerte, können Sie die Suchdauer-Schwellenwert angeben.  Wenn Sie also alle Suchergebnisse zu protokollieren, die 50 ms gedauert hat oder höher, das Sie angeben möchten 50 decimal / 32 hex (zusätzlich zum Festlegen des Field Engineering-Werts).  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>Vergleich zwischen der alten und neuen Ereignis-ID 1644  
OLD  
  
![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
NEU  
  
![Directory services-updates](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>Versuchen Sie Folgendes aus: Verwenden Sie das Ereignisprotokoll, um Statistiken für Abfragen zurückzugeben  
  
1.  Wiederholen Sie die folgenden für Ihre Windows Server 2012-Domänencontroller und Ihre Windows Server 2012 R2-Domänencontroller. Beachten Sie das Ereignis-ID 1644s auf beiden Domänencontrollern nach jeder Suche an.  
  
2.  Verwenden "regedit" ein, aktivieren Sie die Ereignis-ID 1644-Protokollierung, die einen zeitbasierten Schwellenwert für die Windows Server 2012 R2-Domänencontroller und die alte Methode für die Windows Server 2012-Domänencontroller mit.  
  
3.  Führen Sie mehrere LDAP-Suchvorgänge, die den Schwellenwert überschreiten, und beobachten Sie die statistische Informationen am Anfang der Ergebnisse.  Verwenden Sie die LDAP-Abfragen, die Sie weiter oben beschrieben aus, und wiederholen Sie die gleichen Suchvorgänge.  
  
4.  Führen Sie eine LDAP-Suche, die die Abfrageoptimierer nicht optimieren, da ein oder mehrere Attribute nicht indiziert werden.  
  
## <a name="BKMK_ADRepl"></a>Durchsatzverbesserung bei der Active Directory-Replikation  
  
### <a name="overview"></a>Übersicht  
Active Directory-Replikation verwendet RPC für den Replikationstransport. Standardmäßig verwendet RPC einen 8-KB-Puffer übertragen und eine Paketgröße 5 KB. Dies hat den Effekt, in denen die sendende Instanz überträgt drei Pakete (ca. 15K sollte der Daten) und müssen dann die Roundtripzeit für ein Netzwerk warten Sie vor dem Senden weiterer. Sofern eine 3ms Roundtrip-Zeit, wäre der höchste Durchsatz zu 40Mbps, sogar auf 1 Gbit/s oder 10 Gbit/s-Netzwerke.  
  
> [!NOTE]  
> -   Dieses Update wird den maximalen Durchsatz Active Directory-Replikation von 40Mbps auf ca. 600 Mbps angepasst.  
>   
>     -   Sie erhöht die RPC-Größe des Sendepuffers dadurch die Anzahl von Roundtrips  
> -   Der Effekt wird besonders deutlich auf hoher Geschwindigkeit und hoher Latenz Netzwerk.  
  
Diese Updates wurde die Anzahl des maximalen Durchsatzes auf ca. 600 Mbps durch Ändern der Größe des Sendepuffers RPC von 8K auf 256KB.  Diese Änderung ermöglicht die TCP-Fenstergröße, über 8 KB, vergrößern reduziert die Anzahl von Roundtrips.  
  
> [!NOTE]  
> Es gibt keine konfigurierbaren Einstellungen, um dieses Verhalten zu ändern.  
  
### <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Funktionsweise der Active Directory-Replikationsmodell](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


