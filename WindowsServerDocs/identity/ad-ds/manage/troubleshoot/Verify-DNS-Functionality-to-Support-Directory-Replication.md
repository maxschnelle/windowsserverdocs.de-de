---
ms.assetid: 709353b0-b913-4367-8580-44745183e2bc
title: "Überprüfen Sie die DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: 
ms.suite: na
ms.technology: identity-adds
ms.author: billmath
ms.date: 05/31/2017
ms.tgt_pltfrm: na
author: Femila
ms.openlocfilehash: 49f2795e1042438a50850fcb7fd8224eff2cca37
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="verify-dns-functionality-to-support-directory-replication"></a>Überprüfen Sie die DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

 So überprüfen Sie die Einstellungen des Domain Name System (DNS), die mit Active Directory-Replikation beeinträchtigen könnten, können Sie beginnen, durch Ausführen des grundlegenden Tests, die sicherstellt, dass DNS ordnungsgemäß für Ihre Domäne ausgeführt wird. Nachdem Sie die grundlegenden Tests ausführen, können Sie andere Aspekte der DNS-Funktionalität, einschließlich der Registrierung eines Ressourceneintrags und dynamische Updates testen.

Obwohl Sie diesen Test der grundlegenden Funktionen von DNS auf einem beliebigen Domänencontroller ausführen können, führen Sie diesen Test in der Regel auf Domänencontrollern, die Sie der Meinung sind Probleme bei der Replikation, z. B. Domänencontroller Ereignis-IDs 1844 1925, 2087 oder 2088 Bericht möglicherweise auftretenden im Viewer DNS Verzeichnisdienstprotokoll aus.



## <a name="running-the-domain-controller-basic-dns-testtitle"></a>Ausführen des Domain Controller grundlegende DNS-Tests</title>

Die grundlegende DNS-Test überprüft die folgenden Aspekte des DNS-Funktionalität:


- **Konnektivität:** Prüfung wird bestimmt, ob die Domäne, die Domänencontroller in DNS registriert sind hergestellt werden kann die <system>Ping</system> Befehl, und haben Lightweight Directory Access Protocol / remote Procedure call, Remoteprozeduraufruf (LDAP/RPC)-Verbindung. Wenn der Verbindungstest auf einem Domänencontroller ein Fehler auftritt, werden keine weiteren Tests auf diesem Domänencontroller ausgeführt. Der Verbindungstest wird automatisch ausgeführt, bevor alle anderen DNS-Test ausgeführt wird.
- **Erforderliche Dienste:** Test bestätigt, dass die folgenden Dienste ausgeführt werden und auf dem getesteten Domänencontroller verfügbar sind: DNS-Clientdienst, Netlogon-Dienst, Dienst (Key Distribution Center, KDC) und DNS-Serverdienst (sofern DNS auf dem Domänencontroller installiert ist).
- **DNS-Clientkonfiguration:** Test bestätigt, dass alle Netzwerkadapter des Clientcomputers DNS-DNS-Server erreichbar sind.
- **Resource Record Registrierungen:** Test bestätigt, dass die Hostressourceneintrag (A) der einzelnen Domänencontroller registriert ist, auf mindestens einem DNS-Server, der auf dem Clientcomputer konfiguriert ist.
- **Sicherheitszonen und den Autoritätsursprung (SOA):** Wenn der Domänencontroller den DNS-Serverdienst ausgeführt wird, der Test überprüft, ob die Zone für Active Directory-Domäne und Autoritätsursprung (SOA)-Ressourceneintrag für die Active Directory-Domäne-Zone vorhanden sind.
- **Stammzone:** überprüft, ob die Stammzone (.) vorhanden ist.

Mitglied der Gruppe Organisations-Admins oder einer entsprechenden Gruppe ist mindestens erforderlich, um diese Verfahren abzuschließen.

Das folgende Verfahren können grundlegende DNS-Funktionalität überprüfen.
     
### <a name="to-verify-basic-dns-functionality"></a>So überprüfen Sie die grundlegenden DNS-Funktionen:


1. Öffnen Sie auf dem Domänencontroller, den Sie testen möchten, oder auf einem Domänenmitgliedscomputer, der Active Directory-Domänendienste (AD DS)-Tools installiert sind ein Eingabeaufforderungsfenster als Administrator. Klicken Sie zum Öffnen einer Eingabeaufforderung als Administrator **starten**. 
2. Geben Sie unter Suche starten Befehlszeile. 
3. Klicken Sie oben im Menü "Start" Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, stellen Sie sicher, dass die gewünschte Aktion angezeigt wird, was soll, und klicken Sie dann auf Weiter.
4. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s: &lt;DCName&gt; /DnsBasic f:/dcdiagreport.txt`
</br></br>Ersetzen Sie die tatsächlichen definierten Namen, NetBIOS-Name oder DNS-Namen des Domänencontrollers für &lt;DCName&gt;. Als Alternative können Sie alle Domänencontroller in der Gesamtstruktur e: anstatt Entwurfsordner Eingabe testen. Die Option/f Gibt einen Dateinamen, der in den vorherigen Befehl dcdiagreport.txt ist. Wenn Sie die Datei in einem anderen Speicherort als das aktuelle Arbeitsverzeichnis platzieren möchten, können Sie einen Dateipfad, z. B. /f:c:reportsdcdiagreport.txt angeben.

5. Öffnen Sie die dcdiagreport.txt-Datei in Notepad oder einer ähnlichen Text-Editor. Um die Datei im Editor an der Eingabeaufforderung zu öffnen, geben Sie Editor dcdiagreport.txt, und drücken Sie dann die EINGABETASTE. Wenn Sie die Datei in einem anderen Arbeitsverzeichnis platziert, geben Sie den Pfad zur Datei. Wenn Sie die Datei im C:reports platziert, z. B. Geben Sie Editor c:reportsdcdiagreport.txt, und drücken Sie dann die EINGABETASTE.
6. Scrollen Sie zu der Zusammenfassungstabelle fast am Ende der Datei. 
</br></br>Notieren Sie die Namen aller Domänencontroller, "Warnung" oder "Fail" Status in der Zusammenfassungstabelle des Berichts.  Versuchen Sie, um festzustellen, ob ein Problem Domänencontroller finden im Abschnitt detaillierte Unterteilung wird mithilfe der Suche nach der Zeichenfolge "DC: DCName", wobei DCName den tatsächlichen Namen des Domänencontrollers ist.

Offensichtlich konfigurationsänderungen angezeigt, die erforderlich sind, stellen Sie diese nach Bedarf. Beispielsweise, wenn Sie feststellen, dass ein Domänencontroller eine offensichtlich falsche IP-Adresse verfügt, können Sie es beheben. Führen Sie den Test klicken Sie dann erneut.

Um die Änderungen an der Konfiguration zu überprüfen, wiederholen Sie den Befehl Dcdiag/Test: DNS/v, mit dem Schalter/e: oder Entwurfsordner. Wenn Sie keine IP-Version 6 (IPv6) auf dem Domänencontroller aktiviert haben, sollten Sie erwarten, dass des Host (AAAA) Überprüfung Teils der Test fehlschlägt, aber wenn Sie IPv6 nicht in Ihrem Netzwerk verwenden, sind diese Datensätze nicht erforderlich.
            
## <a name="verifying-resource-record-registration"></a>Überprüfen der Resource Record Registrierung
    
Der Zieldomänencontroller verwendet den DNS-Alias (CNAME)-Ressourceneintrag zum Auffinden von seinem Quellreplikationspartner für Domain Controller. Auch wenn Domänencontroller unter Windows Server (beginnend mit Windows Server 2003 mit Service Pack 1 (SP1)) Quellreplikationspartner finden können, mithilfe von vollständig qualifizierten Domänennamen (FQDNs) oder wenn dies nicht möglich ist, NetBIOS-Namesthe den Aliasressourceneintrag (CNAME) wird erwartet, und sollten für die ordnungsgemäße Funktionsweise DNS überprüft werden. 
      
Das folgende Verfahren können die Ressource Registrierung, einschließlich der Alias (CNAME) Resource Record Registrierung überprüfen.
      
### <a name="to-verify-resource-record-registrationtitle"></a>So überprüfen Sie die Registrierung eines Ressourceneintrags</title>


1. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator. Klicken Sie auf "Start", um ein Eingabeaufforderungsfenster als Administrator zu öffnen. Geben Sie unter Suche starten Befehlszeile. 
2. Klicken Sie oben im Menü "Start" Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, stellen Sie sicher, dass die gewünschte Aktion angezeigt wird, was soll, und klicken Sie dann auf Weiter.  </br></br>Sie können das Tool "Dcdiag" Registrierung der Ressourceneinträge überprüfen, die unerlässlich für die Adresse des Domänencontrollers durch Ausführen der `dcdiag /test:dns /DnsRecordRegistration` Befehl.

Dieser Befehl überprüft die folgenden Ressourceneinträge in DNS-Registrierung:


- **Alias (CNAME):** die globally unique Identifier (GUID)-basierte Ressourceneintrag, das einen Replikationspartner sucht
- **Host (A):** der Host-Ressourceneintrag, die die IP-Adresse des Domänencontrollers enthält
- **LDAP SRV:** die Ressourceneinträge für Dienste (SRV), die LDAP-Server zu suchen.
- **GC SRV-**: Katalogserver für die Ressourceneinträge für Dienste (SRV), die globale Suchen
- **PDC SRV**: die Ressourceneinträge für Dienste (SRV), die primären Domänencontroller (PDC) Emulator Betriebsmaster suchen

Das folgende Verfahren können Sie Alias (CNAME) Resource Record allein überprüfen die Registrierung.

### <a name="to-verify-alias-cname-resource-record-registration"></a>So überprüfen Sie die Registrierung eines Alias (CNAME)-Ressourceneintrags

1. Öffnen Sie das DNS-Snap-in. Klicken Sie auf Start, klicken Sie zum Öffnen von DNS. Klicken Sie unter Suche starten Geben Sie dnsmgmt.msc, und drücken Sie dann die EINGABETASTE. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, stellen Sie sicher, dass die Aktion angezeigt wird, die Sie möchten, die und klicken Sie dann auf Weiter.
2. Das DNS-Snap-in verwenden Sie, um einen beliebigen Domänencontroller zu suchen, die den DNS-Serverdienst auf dem Server befinden, in denen die DNS-Zone mit dem gleichen Namen wie die Active Directory-Domäne des Domänencontrollers ausgeführt wird.
3. Klicken Sie in der Konsolenstruktur auf die Zone mit dem Namen "_msdcs". DNS-Domänenname.
4. Klicken Sie im Detailbereich, stellen Sie sicher, dass die folgenden Ressourceneinträge vorhanden sind: eines Aliasressourceneintrags (CNAME) mit dem Namen Dsa_Guid._msdcs. <placeholder>DNS-Domänenname</placeholder> sowie einen entsprechenden (A)-Ressourceneintrag für den Namen des DNS-Servers.

Wenn Aliasressourceneintrags (CNAME) nicht registriert ist, überprüfen Sie, ob das dynamische Update ordnungsgemäß funktioniert. Verwenden Sie den Test im folgenden Abschnitt, um dynamische Updates zu überprüfen.
    
## <a name="verifying-dynamic-update"></a>Überprüfen der dynamischen Updates
    
Der grundlegenden DNS-Test zeigt, dass die Ressourceneinträge in DNS nicht vorhanden sind, verwenden Sie Test für dynamische Updates, um zu bestimmen, warum der Anmeldedienst nicht die Ressourceneinträge automatisch registriert hat. Um sicherzustellen, dass die Active Directory-Domänenzone um sichere dynamische Updates zu übernehmen und zur Registrierung von einen Testdatensatz (_dcdiag_test_record) konfiguriert ist, verwenden Sie das folgende Verfahren. Der Testdatensatz wird nach dem Test automatisch gelöscht.

### <a name="to-verify-dynamic-updatetitle"></a>So überprüfen Sie dynamisches update</title>


1. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator. Klicken Sie auf "Start", um ein Eingabeaufforderungsfenster als Administrator zu öffnen. Geben Sie unter Suche starten Befehlszeile. Klicken Sie oben im Menü "Start" Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, stellen Sie sicher, dass die gewünschte Aktion angezeigt wird, was soll, und klicken Sie dann auf Weiter.
2. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE: 

    Dcdiag/Test: DNS/v/s:&lt;DCName&gt; /DnsDynamicUpdate
</br></br>Ersetzen Sie den definierten Namen, NetBIOS-Name oder DNS-Namen des Domänencontrollers für &lt;DCName&gt;. Als Alternative können Sie alle Domänencontroller in der Gesamtstruktur e: anstatt Entwurfsordner Eingabe testen. Wenn Sie nicht über IPv6 aktiviert, auf dem Domänencontroller verfügen, erwarten den Host (AAAA) Resource Record Teil der Test fehlschlägt, der eine normale Bedingung ist, wenn IPv6 nicht aktiviert ist.

Wenn sichere dynamische Updates nicht konfiguriert sind, können Sie das folgende Verfahren, zu deren Konfiguration.

### <a name="to-enable-secure-dynamic-updates"></a>So aktivieren Sie sichere dynamische updates


1. Öffnen Sie das DNS-Snap-in. Klicken Sie auf Start, klicken Sie zum Öffnen von DNS. 
2. Klicken Sie unter Suche starten Geben Sie dnsmgmt.msc, und drücken Sie dann die EINGABETASTE. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, stellen Sie sicher, dass die Aktion angezeigt werden soll, und klicken Sie dann auf Weiter.
3. Klicken Sie in der Konsolenstruktur mit der rechten Maustaste der entsprechenden Zone, und klicken Sie dann auf Eigenschaften.
4. Überprüfen Sie auf der Registerkarte Allgemein der Zonentyp Active Directory-integriert ist.
5. Klicken Sie in der dynamische Updates nur auf sichere.

## <a name="registering-dns-resource-records"></a>Registrieren von DNS-Ressourceneinträgen
    
Wenn DNS-Ressourceneinträge in DNS für den Quelldomänencontroller nicht angezeigt werden, dynamische Updates überprüft haben und Sie DNS-Ressourceneinträge sofort registrieren möchten, können Sie Registrierung mithilfe des folgenden Verfahrens manuell erzwingen. Der Anmeldedienst auf einem Domänencontroller registriert die DNS-Ressourceneinträge, die für den Domänencontroller im Netzwerk befinden erforderlich sind. Der DNS-Clientdienst registriert den Hostressourceneintrag (A), dem auf der Aliaseintrag (CNAME) verweist.

### <a name="to-register-dns-resource-records-manuallytitle"></a>DNS-Ressourceneinträge manuell registrieren</title>


1. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator. Klicken Sie auf "Start", um ein Eingabeaufforderungsfenster als Administrator zu öffnen. 
2. Geben Sie unter Suche starten Befehlszeile. 
3. Klicken Sie am oberen Rand der Startseite Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, stellen Sie sicher, dass die gewünschte Aktion angezeigt wird, was soll, und klicken Sie dann auf Weiter.
4. So initiieren Sie die Registrierung der Domain Controller Locator Ressource Datensätze manuell auf dem Quelldomänencontroller, an der Eingabeaufforderung Geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE: `net stop net logon &amp; net start net logon`
5. So initiieren Sie die Registrierung des Hosts (A)-Ressourceneintrag manuell, an der Eingabeaufforderung, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE: `ipconfig /flushdns &amp; ipconfig /registerdns`
6. Geben Sie an der Eingabeaufforderung den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE: Dcdiag/test: DNS/v/s:&lt;DCName&gt; </br>,</br>Ersetzen Sie den definierten Namen, NetBIOS-Name oder DNS-Namen des Domänencontrollers für &lt;DCName&gt;. Überprüfen Sie die Ausgabe des Tests, um sicherzustellen, dass die DNS-Tests bestanden hat. Wenn Sie nicht über IPv6 aktiviert, auf dem Domänencontroller verfügen, erwarten den Host (AAAA) Resource Record Teil der Test fehlschlägt, der eine normale Bedingung ist, wenn IPv6 nicht aktiviert ist.
