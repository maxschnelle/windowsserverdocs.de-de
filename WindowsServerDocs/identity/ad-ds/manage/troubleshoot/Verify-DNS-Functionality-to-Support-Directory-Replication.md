---
ms.assetid: 709353b0-b913-4367-8580-44745183e2bc
title: Überprüfen der DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation
ms.author: iainfou
ms.date: 05/31/2017
author: Femila
ms.openlocfilehash: c59160cb3242a91ef8a86d9e8247e0f2d376395b
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88938060"
---
# <a name="verify-dns-functionality-to-support-directory-replication"></a>Überprüfen der DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Um Domain Name System (DNS)-Einstellungen zu überprüfen, die möglicherweise die Active Directory Replikation beeinträchtigen, können Sie zunächst den grundlegenden Test ausführen, mit dem sichergestellt wird, dass DNS für Ihre Domäne ordnungsgemäß funktioniert. Nachdem Sie den grundlegenden Test ausgeführt haben, können Sie andere Aspekte der DNS-Funktionalität testen, einschließlich der Registrierung des Ressourceneinsatzes und des dynamischen Updates.

Obwohl Sie diesen Test der grundlegenden DNS-Funktionalität auf allen Domänen Controllern ausführen können, führen Sie diesen Test in der Regel auf Domänen Controllern aus, bei denen möglicherweise Replikationsprobleme auftreten, z. b. Domänen Controller, die die Ereignis-IDs 1844, 1925, 2087 oder 2088 im DNS-Protokoll des Ereignisanzeige Verzeichnisses melden.



## <a name="running-the-domain-controller-basic-dns-testtitle"></a>Ausführen des grundlegenden DNS-Tests für den Domänen Controller</title>

Der grundlegende DNS-Test überprüft die folgenden Aspekte der DNS-Funktionalität:


- **Konnektivität:** Der Test bestimmt, ob Domänen Controller in DNS registriert sind, kann mit dem <system>Ping</system> -Befehl kontaktiert werden und über eine LDAP/RPC-Verbindung (Lightweight Directory Access Protocol/Remote Prozedur Aufruf) verfügen. Wenn der Konnektivitätstest auf einem Domänen Controller fehlschlägt, werden keine anderen Tests für diesen Domänen Controller ausgeführt. Der Konnektivitätstest wird automatisch ausgeführt, bevor ein anderer DNS-Test ausgeführt wird.
- **Wichtige Dienste:** Der Test bestätigt, dass die folgenden Dienste ausgeführt werden und auf dem getesteten Domänen Controller verfügbar sind: DNS-Client Dienst, Net Logon Service, Schlüsselverteilungscenter (KDC)-Dienst und DNS-Server Dienst (wenn DNS auf dem Domänen Controller installiert ist).
- **DNS-Client Konfiguration:**  Der Test bestätigt, dass die DNS-Server auf allen Netzwerkadaptern des DNS-Client Computers erreichbar sind.
- **Registrierungen von Ressourcen Einträgen:** Der Test bestätigt, dass der Host (A)-Ressourcen Datensatz jedes Domänen Controllers auf mindestens einem der DNS-Server registriert ist, die auf dem Client Computer konfiguriert sind.
- **Zone und Autoritäts Anfang (SOA):** Wenn auf dem Domänen Controller der DNS-Server Dienst ausgeführt wird, wird im Test bestätigt, dass die Active Directory Domänen Zone und der Ressourcen Daten Satz für den Start der Zertifizierungsstelle (SOA) für die Active Directory Domänen Zone vorhanden sind
- Stamm **Zone:** Überprüft, ob die Stamm Zone (.) vorhanden ist.

Sie müssen mindestens Mitglied der Gruppe Organisations-Admins oder einer entsprechenden Gruppe sein, um diese Verfahren auszuführen.

Mithilfe des folgenden Verfahrens können Sie grundlegende DNS-Funktionen überprüfen.

### <a name="to-verify-basic-dns-functionality"></a>So überprüfen Sie die grundlegende DNS-Funktionalität


1. Öffnen Sie auf dem Domänen Controller, den Sie testen möchten, oder auf einem Domänen Mitglieds Computer, auf dem Active Directory Domain Services (AD DS)-Tools installiert sind, eine Eingabeaufforderung als Administrator. Klicken Sie zum Öffnen einer Eingabeaufforderung als Administrator auf **Start**.
2. Geben Sie in Suche starten Command Prompt ein.
3. Klicken Sie am oberen Rand des Menüs Start mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf Als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
4. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s:<DCName> /DnsBasic /f:dcdiagreport.txt`
</br></br>Ersetzen Sie den tatsächlichen Distinguished Name, den NetBIOS-Namen oder den DNS-Namen des Domänen Controllers für &lt; DCNAME &gt; . Als Alternative können Sie alle Domänen Controller in der Gesamtstruktur testen, indem Sie/e: anstelle von/s: eingeben.
Der/f-Schalter gibt einen Dateinamen an, der im vorherigen Befehl dcdiagreport.txt ist. Wenn Sie die Datei an einem anderen Speicherort als dem aktuellen Arbeitsverzeichnis platzieren möchten, können Sie einen Dateipfad angeben, z. b./f:c:reportsdcdiagreport.txt.

5. Öffnen Sie die Datei dcdiagreport.txt im Editor oder in einem ähnlichen Text-Editor. Wenn Sie die Datei im Editor öffnen möchten, geben Sie an der Eingabeaufforderung Editor dcdiagreport.txt ein, und drücken Sie dann die EINGABETASTE. Wenn Sie die Datei in einem anderen Arbeitsverzeichnis abgelegt haben, schließen Sie den Pfad der Datei ein. Wenn Sie die Datei z. b. in c:Reports abgelegt haben, geben Sie Editor c:reportsdcdiagreport.txt ein, und drücken Sie dann die EINGABETASTE.
6. Scrollen Sie zu der Zusammenfassungs Tabelle am Ende der Datei.
</br></br>Notieren Sie sich die Namen aller Domänen Controller, die den Status "Warnung" oder "fehlgeschlagen" in der Zusammenfassungs Tabelle melden.  Versuchen Sie zu bestimmen, ob ein Problem Domänen Controller vorhanden ist, indem Sie nach der Zeichenfolge "DC: DCNAME" suchen, wobei DCNAME der tatsächliche Name des Domänen Controllers ist.

Wenn Sie offensichtliche Konfigurationsänderungen sehen, die erforderlich sind, machen Sie Sie entsprechend. Wenn Sie z. b. feststellen, dass einer ihrer Domänen Controller über eine offensichtlich falsche IP-Adresse verfügt, können Sie Sie korrigieren. Führen Sie den Test dann erneut aus.

Um die Konfigurationsänderungen zu überprüfen, führen Sie ggf. den Befehl dcdiag/Test: DNS/v mit dem Switch/e: oder/s: erneut aus. Wenn auf dem Domänen Controller keine IP-Version 6 (IPv6) aktiviert ist, sollten Sie davon ausgehen, dass bei der Überprüfung des Hosts (AAAA) der Test fehlschlägt. Wenn Sie jedoch nicht IPv6 in Ihrem Netzwerk verwenden, sind diese Datensätze nicht erforderlich.

## <a name="verifying-resource-record-registration"></a>Überprüfen der Registrierung von Ressourcen Einträgen

Der Zieldomänen Controller verwendet den DNS-Alias Ressourcen-Datensatz (CNAME), um den Quell Domänen Controller-Replikations Partner zu suchen. Obwohl Domänen Controller unter Windows Server (beginnend mit Windows Server 2003 mit Service Pack 1 (SP1)) Quell Replikations Partner mithilfe von vollständig qualifizierten Domänen Namen (FQDNs) suchen können oder wenn dies fehlschlägt, wird das vorhanden sein des Alias Ressourceneinsatzes (CNAME) erwartet und sollte auf eine ordnungsgemäße DNS-Funktion überprüft werden.

Mithilfe des folgenden Verfahrens können Sie die Registrierung von Ressourcen Einträgen einschließlich der Registrierung des Ressourceneinsatzes von Alias (CNAME) überprüfen.

### <a name="to-verify-resource-record-registrationtitle"></a>So überprüfen Sie die Registrierung des Ressourcen</title>


1. Öffnen Sie als Administrator eine Eingabeaufforderung. Klicken Sie zum Öffnen einer Eingabeaufforderung als Administrator auf Start. Geben Sie in Suche starten Command Prompt ein.
2. Klicken Sie am oberen Rand des Menüs Start mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf Als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.  </br></br>Sie können das DCDiag-Tool verwenden, um die Registrierung aller Ressourcen Datensätze zu überprüfen, die für den Domänen Controller Standort unverzichtbar sind, indem Sie den `dcdiag /test:dns /DnsRecordRegistration` Befehl ausführen.

Mit diesem Befehl wird die Registrierung der folgenden Ressourcen Einträge in DNS überprüft:


- **Alias (CNAME):** der auf der Globally Unique Identifier (GUID) basierende Ressourcen Daten Satz, der einen Replikations Partner anmeldert.
- **Host (A):**  der Host Ressourcen Daten Satz, der die IP-Adresse des Domänen Controllers enthält.
- **LDAP SRV:** der Dienst (SRV)-Ressourcen Einträge, die LDAP-Server suchen
- **GC SRV**: Ressourcen Einträge für den Dienst (SRV), die nach globalen Katalog Servern suchen
- **PDC SRV**: die Ressourcen Einträge des Diensts (SRV), die Emulator-Betriebs Master des primären Domänen Controllers (PDC) finden

Mithilfe des folgenden Verfahrens können Sie die Registrierung des Alias Ressourceneinsatzes (CNAME) allein überprüfen.

### <a name="to-verify-alias-cname-resource-record-registration"></a>So überprüfen Sie die Registrierung des Alias Ressourceneinsatzes (CNAME)

1. Öffnen Sie das DNS-Snap-in. Klicken Sie zum Öffnen von DNS auf Start. Geben Sie in Suche starten den Namen dnsmgmt. msc ein, und drücken Sie dann die EINGABETASTE. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
2. Verwenden Sie das DNS-Snap-in, um einen beliebigen Domänen Controller zu suchen, auf dem der DNS-Server Dienst ausgeführt wird, auf dem der Server die DNS-Zone mit dem gleichen Namen wie die Active Directory Domäne des Domänen Controllers hostet.
3. Klicken Sie in der Konsolen Struktur auf die Zone mit dem Namen _msdcs. Dns_Domain_Name.
4. Überprüfen Sie im Detailbereich, ob die folgenden Ressourcen Einträge vorhanden sind: ein Alias Ressourcen Eintrag (CNAME) mit dem Namen Dsa_Guid. _msdcs. <placeholder>Dns_Domain_Name</placeholder> und einen entsprechenden Host Ressourcen Daten Satz (a) für den Namen des DNS-Servers.

Wenn der Alias Ressourcen Daten Satz (CNAME) nicht registriert ist, überprüfen Sie, ob das dynamische Update ordnungsgemäß funktioniert. Verwenden Sie den Test im folgenden Abschnitt, um das dynamische Update zu überprüfen.

## <a name="verifying-dynamic-update"></a>Dynamisches Update wird überprüft

Wenn der grundlegende DNS-Test anzeigt, dass Ressourcen Einträge in DNS nicht vorhanden sind, verwenden Sie den Test für dynamisches Update, um zu ermitteln, warum der Anmeldedienst die Ressourcen Einträge nicht automatisch registriert hat. Verwenden Sie das folgende Verfahren, um zu überprüfen, ob die Active Directory Domänen Zone für das akzeptieren sicherer dynamischer Updates und das Ausführen der Registrierung eines Test Datensatzes (_dcdiag_test_record) konfiguriert ist. Der Testdatensatz wird nach dem Test automatisch gelöscht.

### <a name="to-verify-dynamic-updatetitle"></a>So überprüfen Sie das dynamische Update</title>


1. Öffnen Sie als Administrator eine Eingabeaufforderung. Klicken Sie zum Öffnen einer Eingabeaufforderung als Administrator auf Start. Geben Sie in Suche starten Command Prompt ein. Klicken Sie am oberen Rand des Menüs Start mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf Als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
2. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s:<DCName> /DnsDynamicUpdate`
   </br></br>Ersetzen Sie für DCNAME den Distinguished Name, den NetBIOS-Namen oder den DNS-Namen des Domänen Controllers &lt; &gt; . Als Alternative können Sie alle Domänen Controller in der Gesamtstruktur testen, indem Sie/e: anstelle von/s: eingeben. Wenn Sie IPv6 auf dem Domänen Controller nicht aktiviert haben, sollten Sie davon ausgehen, dass der Teil des Tests des Host (AAAA)-Ressourcen Satzes fehlschlägt. Dies ist ein normaler Zustand, wenn IPv6 nicht aktiviert ist.

Wenn sichere dynamische Updates nicht konfiguriert sind, können Sie das folgende Verfahren verwenden, um Sie zu konfigurieren.

### <a name="to-enable-secure-dynamic-updates"></a>So aktivieren Sie sichere dynamische Updates


1. Öffnen Sie das DNS-Snap-in. Klicken Sie zum Öffnen von DNS auf Start.
2. Geben Sie in Suche starten den Namen dnsmgmt. msc ein, und drücken Sie dann die EINGABETASTE. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
3. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die entsprechende Zone, und klicken Sie dann auf Eigenschaften.
4. Überprüfen Sie auf der Registerkarte Allgemein, ob der Zonentyp Active Directory integriert ist.
5. Klicken Sie in dynamische Updates auf nur sichern.

## <a name="registering-dns-resource-records"></a>DNS-Ressourcen Einträge werden registriert

Wenn DNS-Ressourcen Einträge nicht in DNS für den Quell Domänen Controller angezeigt werden und Sie die DNS-Ressourcen Einträge sofort registrieren möchten, können Sie die Registrierung mithilfe des folgenden Verfahrens manuell erzwingen. Der Anmeldedienst auf einem Domänen Controller registriert die DNS-Ressourcen Einträge, die für die Suche des Domänen Controllers im Netzwerk erforderlich sind. Der DNS-Client Dienst registriert den Host (A)-Ressourcen Daten Satz, auf den der Alias (CNAME)-Datensatz verweist.

### <a name="to-register-dns-resource-records-manuallytitle"></a>So registrieren Sie DNS-Ressourcen Einträge manuell</title>


1. Öffnen Sie als Administrator eine Eingabeaufforderung. Klicken Sie zum Öffnen einer Eingabeaufforderung als Administrator auf Start.
2. Geben Sie in Suche starten Command Prompt ein.
3. Klicken Sie oben im Startmenü mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
4. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die Registrierung der Ressourcen Einträge für Domänen Controller-Serverlocatorpunkt manuell auf dem Quell Domänen Controller zu initiieren: `net stop netlogon && net start netlogon`
5. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die Registrierung des Host Ressourceneinsatzes (A) manuell zu initiieren: `ipconfig /flushdns && ipconfig /registerdns`
6. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s:<DCName>` </br></br>Ersetzen Sie für DCNAME den Distinguished Name, den NetBIOS-Namen oder den DNS-Namen des Domänen Controllers &lt; &gt; . Überprüfen Sie die Ausgabe des Tests, um sicherzustellen, dass die DNS-Tests bestanden wurden. Wenn Sie IPv6 auf dem Domänen Controller nicht aktiviert haben, sollten Sie davon ausgehen, dass der Teil des Tests des Host (AAAA)-Ressourcen Satzes fehlschlägt. Dies ist ein normaler Zustand, wenn IPv6 nicht aktiviert ist.
