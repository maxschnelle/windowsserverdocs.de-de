---
ms.assetid: 709353b0-b913-4367-8580-44745183e2bc
title: Überprüfen der DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: identity-adds
ms.author: joflore
ms.date: 05/31/2017
ms.tgt_pltfrm: na
author: Femila
ms.openlocfilehash: a55b95ee516abda8bdbae6e9829a161ef060012e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871871"
---
# <a name="verify-dns-functionality-to-support-directory-replication"></a>Überprüfen der DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Um Domain Name System (DNS)-Einstellungen zu überprüfen, die Active Directory-Replikation behindert werden können, können Sie beginnen mit den grundlegenden Tests, der sicherstellt, dass DNS für Ihre Domäne ordnungsgemäß ausgeführt wird. Nachdem Sie die grundlegenden Test ausführen, können Sie andere Aspekte von DNS-Funktionalität, einschließlich der Registrierung eines Ressourceneintrags und an dynamischen Updates testen.

Obwohl Sie diesen Test ausführen, können DNS-Grundfunktionen auf jedem Domänencontroller, in der Regel führen Sie diesen Test auf Domänencontroller, auf denen Sie denken unter Umständen kommt es Probleme bei der Replikation, z. B. Domänencontrollern, die Ereignis-IDs 1844, 1925, 2087, melden oder 2088 im Event Viewer Directory-Dienst-DNS-Protokoll.



## <a name="running-the-domain-controller-basic-dns-testtitle"></a>Ausführen des Domain Controller grundlegende DNS-Tests</title>

Der DNS-Standardtest prüft die folgenden Aspekte von DNS-Funktionalität:


- **Konnektivität:** Der Test bestimmt, ob es sich bei Controller sind in DNS registrierten Domäne hergestellt werden kann, durch die <system>Ping</system> -Befehl aus, und haben Lightweight Directory Access Protocol / Remoteprozeduraufruf (LDAP/RPC)-Verbindung. Wenn der Test der Netzwerkverbindung auf einem Domänencontroller ein Fehler auftritt, werden keine weiteren Tests für diesen Domänencontroller ausgeführt. Der Verbindungstest wird automatisch ausgeführt, bevor alle anderen DNS-Test ausgeführt wird.
- **Erforderliche Dienste:** Der Test bestätigt, dass die folgenden Dienste ausgeführt werden und auf dem getesteten Domänencontroller verfügbar sind: DNS-Clientdienst, Netlogon-Dienst, Schlüsselverteilungscenter (Key Distribution Center, KDC)-Dienst und DNS-Serverdienst (sofern DNS auf dem Domänencontroller installiert ist).
- **DNS-Client-Konfiguration:**  Der Test bestätigt, dass alle Netzwerkadapter des Clientcomputers DNS-DNS-Server erreichbar sind.
- **Ressource Datensatz Registrierungen:** Der Test wird bestätigt, dass die Hostressourceneintrag (A) der einzelnen Domänencontroller registriert ist, auf mindestens einem DNS-Server, der auf dem Clientcomputer konfiguriert ist.
- **Zone und Autoritätsursprung (SOA):** Wenn der Domänencontroller den DNS-Serverdienst ausgeführt wird, bestätigt der Test an, dass die Zone von Active Directory-Domäne und den Start der Autoritätsursprung (SOA)-Ressourceneintrag für die Active Directory-Domäne-Zone vorhanden sind.
- **Stammzone:** Überprüft, ob die Stammzone (.) vorhanden ist.

Mitgliedschaft in der Organisations-Admins oder einer entsprechenden Gruppe ist die mindestvoraussetzung zum Abschließen dieser Verfahren.

Sie können das folgende Verfahren verwenden, um zu überprüfen, ob DNS-Grundfunktionen.
     
### <a name="to-verify-basic-dns-functionality"></a>Grundlegende DNS-Funktionalität zu überprüfen:


1. Öffnen Sie auf dem Domänencontroller, den Sie testen möchten, oder auf einem Domänenmitgliedscomputer, der Active Directory Domain Services (AD DS)-Tools installiert sind eine Eingabeaufforderung als Administrator an. Klicken Sie zum Öffnen einer Eingabeaufforderung als Administrator auf **Start**. 
2. Geben Sie unter Suche starten die Eingabeaufforderung. 
3. Klicken Sie am oberen Rand des Startmenüs Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
4. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s:<DCName> /DnsBasic /f:dcdiagreport.txt`
</br></br>Ersetzen Sie den tatsächlichen gekennzeichneten Namen, NetBIOS-Name oder DNS-Namen des Domänencontrollers für &lt;DCName&gt;. Als Alternative können Sie alle Domänencontroller in der Gesamtstruktur testen, e: anstelle von/s: geben. Die f-Option gibt an, einen Dateinamen, der im vorherigen Befehl dcdiagreport.txt ist. Wenn Sie die Datei in einem anderen Speicherort als das aktuelle Arbeitsverzeichnis platzieren möchten, können Sie einen Dateipfad an, wie z. B. /f:c:reportsdcdiagreport.txt angeben.

5. Öffnen Sie die dcdiagreport.txt-Datei in Notepad oder einem ähnlichen Texteditor ein. Klicken Sie zum Öffnen der Datei in Editor, an der Eingabeaufforderung Geben Sie Notepad dcdiagreport.txt, und drücken Sie dann die EINGABETASTE. Wenn Sie die Datei in ein anderes Arbeitsverzeichnis platzieren, enthalten Sie den Pfad zur Datei. Wenn Sie die Datei im C:reports platziert, z. B. Editor c:reportsdcdiagreport.txt geben, und dann die EINGABETASTE drücken.
6. Scrollen Sie nach der Tabelle "Zusammenfassung" im unteren Bereich der Datei. 
</br></br>Beachten Sie den Namen von allen Domänencontrollern, "Warnung" oder "Fail" Status in der Zusammenfassungstabelle des Berichts.  Versuchen Sie es, um festzustellen, ob ein Problem-Domänencontroller vorhanden ist, suchen Sie im Abschnitt ausführliche Breakout durch Suchen nach der Zeichenfolge "DC: DCName"angezeigt, in denen DCName der tatsächliche Name des Domänencontrollers ist.

Wenn Änderungen an der offensichtlichen Konfiguration angezeigt wird, die erforderlich sind, stellen sie nach Bedarf. Beispielsweise sollten Sie feststellen, dass ein Domänencontroller eine offensichtlich falsche IP-Adresse verfügt, können Sie ihn korrigieren. Führen Sie anschließend den Test erneut aus.

Um Änderungen an der Konfiguration zu überprüfen, führen Sie den Dcdiag/Test: DNS/v-Befehl mit dem Schalter/e: oder/s: nach Bedarf erneut aus. Wenn Sie keine IP-Version 6 (IPv6) auf dem Domänencontroller aktiviert haben, erwarten, dass des Host (AAAA) Überprüfung Teils der Test fehlschlägt, aber wenn Sie IPv6 nicht in Ihrem Netzwerk verwenden, sind diese Datensätze nicht erforderlich.
            
## <a name="verifying-resource-record-registration"></a>Überprüfen von Datensatz ressourcenregistrierung
    
Der Zieldomänencontroller verwendet den DNS-Alias (CNAME)-Ressourceneintrag, seinem Quellreplikationspartner für Domain-Controller gesucht werden soll. Auch wenn Domänencontroller unter Windows Server (ab Windows Server 2003 mit Service Pack 1 (SP1)) Quellreplikationspartner finden können, mithilfe des vollständig qualifizierten Domänennamen (FQDNs) oder, wenn es sich bei, die NetBIOS-Namesthe Anwesenheit des Alias (CNAME) ein Fehler auftritt, -Ressourceneintrag ist normal und sollte überprüft werden, für die ordnungsgemäße DNS funktioniert. 
      
Sie können das folgende Verfahren verwenden, zu überprüfen, ob Resource Record-Registrierung, einschließlich Aliasressourceneintrags (CNAME) Resource Record Registrierung.
      
### <a name="to-verify-resource-record-registrationtitle"></a>Überprüfen der Registrierung eines Ressourceneintrags</title>


1. Öffnen Sie eine Eingabeaufforderung mit Administratorrechten. Um eine Eingabeaufforderung als Administrator öffnen, klicken Sie auf "Start". Geben Sie unter Suche starten die Eingabeaufforderung. 
2. Klicken Sie am oberen Rand des Startmenüs Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.  </br></br>Können Sie das Dcdiag-Tool zu überprüfen, ob Registrierung aller Datensätze für die Ressource, die für die Domänencontrollersuche mit sind die `dcdiag /test:dns /DnsRecordRegistration` Befehl.

Mit diesem Befehl wird überprüft, ob die folgenden Ressourceneinträge in DNS-Registrierung:


- **Alias (CNAME):** die globally unique Identifier (GUID)-Ressourcendatensatz, der einen Replikationspartner sucht basierend
- **Host (A):** Hostressourceneintrag an, die die IP-Adresse des Domänencontrollers enthält.
- **LDAP SRV:** die Ressourceneinträge für Dienste (SRV), die LDAP-Server suchen
- **GC-SRV-**: Katalogserver für die Ressourceneinträge für Dienste (SRV), die globale Suchen
- **PDC SRV**: die Dienstressourceneinträge (SRV), das Suchen des primären Domänencontrollers (PDC)-Emulator-Betriebsmaster

Sie können das folgende Verfahren verwenden, Aliasressourceneintrags (CNAME) Registrierung eines Ressourceneintrags allein zu überprüfen.

### <a name="to-verify-alias-cname-resource-record-registration"></a>Überprüfen der Registrierung eines Ressourceneintrags Aliasressourceneintrags (CNAME)

1. Öffnen Sie das DNS-Snap-in. Klicken Sie auf "Start", um DNS zu öffnen. Klicken Sie unter Suche starten Geben Sie dnsmgmt.msc, und drücken Sie dann die EINGABETASTE. Wenn das Dialogfeld "Benutzerkontensteuerung" angezeigt wird, vergewissern Sie sich, dass die Aktion angezeigt wird, die Sie möchten, die und klicken Sie dann auf Weiter.
2. Das DNS-Snap-in verwenden Sie, um einen beliebigen Domänencontroller zu suchen, die den DNS-Serverdienst ausgeführt wird, in dem der Server den DNS-Zone mit dem gleichen Namen wie die Active Directory-Domäne des Domänencontrollers gehostet.
3. Klicken Sie in der Konsolenstruktur auf die Zone "_msdcs" mit dem Namen. DNS-Domänenname.
4. Stellen Sie sicher, dass die folgenden Ressourceneinträge vorhanden sind, klicken Sie im Bereich "Details": eines Aliasressourceneintrags (CNAME) mit dem Namen Dsa_Guid._msdcs. <placeholder>DNS-Domänenname</placeholder> und ein entsprechender Hosteintrag (A) Ressource für den Namen der DNS-Server.

Wenn die Aliasressourceneintrags (CNAME) nicht registriert ist, stellen Sie sicher, dass das dynamische Update ordnungsgemäß funktioniert. Verwenden Sie den Test im folgenden Abschnitt, um dynamische Updates zu überprüfen.
    
## <a name="verifying-dynamic-update"></a>Überprüfen die dynamischen Updates
    
Der DNS-Standardtest zeigt, dass es sich bei Ressourceneinträge in DNS nicht vorhanden sind, verwenden Sie Test für dynamische Updates, um zu bestimmen, warum der Anmeldedienst nicht die Ressourceneinträge automatisch registriert hat. Um sicherzustellen, dass die Zone der Active Directory-Domäne konfiguriert ist, um sichere dynamische Updates akzeptieren und Registrierung des einen Testdatensatz (_dcdiag_test_record) auszuführen, verwenden Sie das folgende Verfahren aus. Der Testdatensatz wird nach dem Test automatisch gelöscht.

### <a name="to-verify-dynamic-updatetitle"></a>Um dynamische Updates zu überprüfen.</title>


1. Öffnen Sie eine Eingabeaufforderung mit Administratorrechten. Um eine Eingabeaufforderung als Administrator öffnen, klicken Sie auf "Start". Geben Sie unter Suche starten die Eingabeaufforderung. Klicken Sie am oberen Rand des Startmenüs Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
2. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s:<DCName> /DnsDynamicUpdate`
   </br></br>Ersetzen Sie den distinguished Name, den NetBIOS-Namen oder die DNS-Namen des Domänencontrollers für &lt;DCName&gt;. Als Alternative können Sie alle Domänencontroller in der Gesamtstruktur testen, e: anstelle von/s: geben. Wenn Sie nicht über IPv6 aktiviert ist, auf dem Domänencontroller verfügen, sollten Sie den Host (AAAA) Ressource Datensatz Teil der Test fehlschlägt, erwarten, der ist ein normaler Zustand, wenn IPv6 nicht aktiviert ist.

Wenn sichere dynamische Updates nicht konfiguriert werden, können Sie wie folgt vor, für deren Konfiguration.

### <a name="to-enable-secure-dynamic-updates"></a>Sichere dynamische Updates aktivieren


1. Öffnen Sie das DNS-Snap-in. Klicken Sie auf "Start", um DNS zu öffnen. 
2. Klicken Sie unter Suche starten Geben Sie dnsmgmt.msc, und drücken Sie dann die EINGABETASTE. Wenn das Dialogfeld "Benutzerkontensteuerung" angezeigt wird, vergewissern Sie sich, dass die Aktion angezeigt wird, die Sie möchten, und klicken Sie dann auf Weiter.
3. Klicken Sie in der Konsolenstruktur mit der rechten Maustaste in der entsprechenden Zone, und klicken Sie dann auf Eigenschaften.
4. Stellen Sie sicher, dass die Zone Active Directory-integriert ist, auf der Registerkarte Allgemein.
5. Klicken Sie in der dynamische Updates nur auf sichere.

## <a name="registering-dns-resource-records"></a>Registrieren von DNS-Ressourceneinträgen
    
Wenn DNS-Ressourceneinträge in DNS für den Quelldomänencontroller nicht angezeigt werden, Sie haben überprüft, ob dynamische Updates, und Sie DNS-Ressourceneinträge sofort registrieren möchten, Sie können erzwingen, dass Registrierung manuell mithilfe des folgenden Verfahrens. Der Anmeldedienst auf einem Domänencontroller registriert die DNS-Ressourceneinträge, die für den Domänencontroller im Netzwerk befinden, erforderlich sind. Der DNS-Clientdienst registriert die Hostressourceneintrag (A), dem auf der Aliaseintrag (CNAME) verweist.

### <a name="to-register-dns-resource-records-manuallytitle"></a>DNS-Ressourceneinträge manuell registrieren.</title>


1. Öffnen Sie eine Eingabeaufforderung mit Administratorrechten. Um eine Eingabeaufforderung als Administrator öffnen, klicken Sie auf "Start". 
2. Geben Sie unter Suche starten die Eingabeaufforderung. 
3. Klicken Sie am oberen Rand der Start Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf Weiter.
4. Zum Initiieren der Registrierung des Domain Controller Locator-Ressource Datensätze manuell auf dem Quelldomänencontroller, an der Eingabeaufforderung, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE: `net stop netlogon && net start netlogon`
5. Zum Initiieren der Registrierung des Hosts (A)-Ressourceneintrag manuell an der Eingabeaufforderung, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE: `ipconfig /flushdns && ipconfig /registerdns`
6. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE: `dcdiag /test:dns /v /s:<DCName>` </br></br>Ersetzen Sie den distinguished Name, den NetBIOS-Namen oder die DNS-Namen des Domänencontrollers für &lt;DCName&gt;. Überprüfen Sie die Ausgabe des Tests stellen Sie sicher, dass der DNS-Tests bestanden wurden. Wenn Sie nicht über IPv6 aktiviert ist, auf dem Domänencontroller verfügen, sollten Sie den Host (AAAA) Ressource Datensatz Teil der Test fehlschlägt, erwarten, der ist ein normaler Zustand, wenn IPv6 nicht aktiviert ist.
