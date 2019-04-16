---
ms.assetid: 99a68050-8d19-4c58-ad86-e08a3dcdb4f7
title: "Anhang L – zu überwachende Ereignisse"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d153a16b31070f2bbfac4a47a814792ef66b472
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-l-events-to-monitor"></a>Anhang L: zu überwachende Ereignisse

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

  
## <a name="appendix-l-events-to-monitor"></a>Anhang L: zu überwachende Ereignisse  
Die folgende Tabelle enthält die Ereignisse, die Sie in Ihrer Umgebung entsprechend den Empfehlungen in überwachen sollte [Überwachung von Active Directory für Zeichen der Gefährdung](../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md). In der folgenden Tabelle sind die Spalte "Aktuelle Windows-Ereignis-ID" die Ereignis-ID ist Implementierung in Versionen von Windows und Windows Server, die derzeit im grundlegenden Support sind aufgeführt.  
  
Die Spalte "Ältere Windows-Ereignis-ID" enthält die entsprechenden Ereignis-ID in älteren Versionen von Windows wie Clientcomputern mit Windows XP oder früher und Server unter WindowsServer 2003 oder ältere Versionen. Die "potenzielle Gefährlichkeit", die Spalte gibt, ob das Ereignis mit geringer berücksichtigt werden sollten, Mittel oder hoch Gefährlichkeit Erkennen von Angriffen und der Spalte "Zusammenfassung" enthält eine kurze Beschreibung des Ereignisses.  
  
Der potenziellen Gefährlichkeit hoher bedeutet, dass ein Eintreten des Ereignisses untersucht werden. Potenzielle Gefährlichkeit Mittel oder niedrig bedeutet, dass diese Ereignisse nur untersucht werden sollte, wenn sie unerwartet beendet oder in Zahlen, die erheblich die erwartete messbasis in einem Messzeitraum überschreitet auftreten. Alle Organisationen sollten diese Empfehlungen in ihrer Umgebung vor dem Erstellen testen Warnungen, die verbindliche Untersuchungen erfordern. Jede Umgebung ist anders, und einige der Ereignisse, die mit der potenziellen Gefährlichkeit hoch aufgrund anderer harmloser Ereignisse auftreten.  
  
|||||  
|-|-|-|-|  
|**Aktuelle Windows-Ereignis-ID**|**Ältere Windows-Ereignis-ID**|**Potenzielle Gefährlichkeit**|**Ereignis-Zusammenfassung**|  
|4618|N/V|Hoch|Ein überwachtes sicherheitsmuster ist aufgetreten.|  
|4649|N/V|Hoch|Ein Replay-Angriff wurde erkannt. Möglicherweise ein harmloser falsch positiven aufgrund einer fehlerhaften Konfiguration Fehler.|  
|4719|612|Hoch|Systemüberwachungsrichtlinie wurde geändert.|  
|4765|N/V|Hoch|Ein Konto wurde SID History hinzugefügt.|  
|4766|N/V|Hoch|Fehler beim Konto-SID History hinzu.|  
|4794|N/V|Hoch|Es wurde versucht, den Modus "Verzeichnisdienste wiederherstellen" fest.|  
|4897|801|Hoch|Rollentrennung ist aktiviert:|  
|4964|N/V|Hoch|Sondergruppen wurden einer neuen Anmeldung zugewiesen.|  
|5124|N/V|Hoch|Eine Sicherheitsrichtlinie wurde auf die OCSP-Responder-Dienst aktualisiert.|  
|N/V|550|Mittel bis hoch|Angriff möglichen Denial-of-Service (DoS)|  
|1102|517|Mittel bis hoch|Das Überwachungsprotokoll wurde gelöscht.|  
|4621|N/V|Mittel|Administrator System aus "CrashOnAuditFail" wiederhergestellt. Benutzer, die keine Administratoren sind nun kann sich anmelden. Einige überwachbare Aktivitäten wurden möglicherweise nicht aufgezeichnet.|  
|4675|N/V|Mittel|SIDs wurden gefiltert.|  
|4692|N/V|Mittel|Sicherung der Datenschutz-Hauptschlüssel wurde versucht.|  
|4693|N/V|Mittel|Wiederherstellung der Datenschutz-Hauptschlüssel wurde versucht.|  
|4706|610|Mittel|Eine neue Vertrauensstellung wurde zu einer Domäne erstellt.|  
|4713|617|Mittel|Kerberos-Richtlinie wurde geändert.|  
|4714|618|Mittel|Die Wiederherstellungsrichtlinie für verschlüsselte Daten wurde geändert.|  
|4715|N/V|Mittel|Die Überwachungsrichtlinie (SACL) für ein Objekt wurde geändert.|  
|4716|620|Mittel|Informationen zu vertrauenswürdigen Domänen wurde geändert.|  
|4724|628|Mittel|Es wurde versucht, um das Kennwort eines Kontos zurückzusetzen.|  
|4727|631|Mittel|Eine sicherheitsaktivierte globale Gruppe wurde erstellt.|  
|4735|639|Mittel|Eine sicherheitsaktivierte lokale Gruppe wurde geändert.|  
|4737|641|Mittel|Eine sicherheitsaktivierte globale Gruppe wurde geändert.|  
|4739|643|Mittel|Die Domänenrichtlinie wurde geändert.|  
|4754|658|Mittel|Eine sicherheitsaktivierte universelle Gruppe wurde erstellt.|  
|4755|659|Mittel|Eine sicherheitsaktivierte universelle Gruppe wurde geändert.|  
|4764|667|Mittel|Eine Gruppe mit deaktivierter Sicherheit wurde gelöscht.|  
|4764|668|Mittel|Der Typ einer Gruppe wurde geändert.|  
|4780|684|Mittel|Die ACL wurde für Konten festgelegt, die Mitglieder der Administratorgruppe sind.|  
|4816|N/V|Mittel|Bei der Entschlüsselung einer eingehenden Nachricht eine integritätsverletzung (RPC) hat.|  
|4865|N/V|Mittel|Ein Informationseintrag für eine vertrauenswürdige Gesamtstruktur wurde hinzugefügt.|  
|4866|N/V|Mittel|Ein Informationseintrag für eine vertrauenswürdige Gesamtstruktur wurde entfernt.|  
|4867|N/V|Mittel|Ein Informationseintrag für eine vertrauenswürdige Gesamtstruktur wurde geändert.|  
|4868|772|Mittel|Die Zertifikat-Manager verweigert ausstehender Zertifikate.|  
|4870|774|Mittel|Ein Zertifikat wurde gesperrt.|  
|4882|786|Mittel|Die Sicherheitsberechtigungen für die Zertifikatdienste wurden geändert.|  
|4885|789|Mittel|Der überwachungsfilter für Zertifikatdienste geändert.|  
|4890|794|Mittel|Die Zertifikat-Manager-Einstellungen für Zertifikatdienste geändert.|  
|4892|796|Mittel|Eine Eigenschaft der Zertifikatdienste geändert.|  
|4896|800|Mittel|Eine oder mehrere Zeilen wurden aus der Zertifikatdatenbank gelöscht.|  
|4906|N/V|Mittel|Der CrashOnAuditFail-Wert wurde geändert.|  
|4907|N/V|Mittel|Überwachungseinstellungen für das Objekt wurden geändert.|  
|4908|N/V|Mittel|Anmeldetabelle für Sondergruppen geändert.|  
|4912|807|Mittel|Benutzerüberwachungsrichtlinie wurde geändert.|  
|4960|N/V|Mittel|IPsec hat ein eingehendes Paket, das eine integritätsüberprüfung nicht bestanden verworfen. Wenn dieses Problem weiterhin auftritt, kann dies hinweisen, dass ein Netzwerkproblem vorliegt oder Pakete während der Übertragung an diesen Computer geändert werden. Stellen Sie sicher, dass die vom Remotecomputer gesendeten Pakete identisch mit denen von diesem Computer empfangen sind. Dieser Fehler kann auch auf Interoperabilitätsprobleme mit anderen IPsec-Implementierungen hinweisen.|  
|4961|N/V|Mittel|IPsec hat ein eingehendes Paket, das eine rahmenprüfung nicht bestanden hat verworfen. Wenn dieses Problem weiterhin auftritt, kann dies einen Replay-Angriff auf diesen Computer hinweisen.|  
|4962|N/V|Mittel|IPsec hat ein eingehendes Paket, das eine rahmenprüfung nicht bestanden hat verworfen. Des eingehenden Pakets war zu niedrig eine Sequenznummer, um sicherzustellen, dass es sich nicht um eine Wiederholung war.|  
|4963|N/V|Mittel|IPsec hat ein eingehendes Klartextpaket, das geschützt hätte sein sollen verworfen. Dies ist in der Regel aufgrund der Remotecomputer seine IPsec-Richtlinie ändern, ohne zu diesem Computer zu informieren. Dies kann auch einen versuchten Spoofingangriff sein.|  
|4965|N/V|Mittel|IPsec hat ein Paket von einem Remotecomputer mit einer falschen Sicherheit Sicherheitsparameterindex (SPI) empfangen. Dies wird normalerweise durch eine fehlerhafte Hardware verursacht, die Pakete beschädigt ist. Wenn dieser Fehler weiterhin auftritt, stellen Sie sicher, dass die vom Remotecomputer gesendeten Pakete identisch mit denen von diesem Computer empfangen sind. Dieser Fehler kann auch auf Interoperabilitätsprobleme mit anderen IPsec-Implementierungen hinweisen. In diesem Fall, wenn Konnektivität nicht beeinträchtigt ist, können diese Ereignisse ignoriert werden.|  
|4976|N/V|Mittel|Während der Hauptmodusverhandlung hat IPsec ein ungültiges verhandlungspaket empfangen. Wenn dieses Problem weiterhin auftritt, kann dies auf ein Netzwerkproblem oder zu ändern oder diese Aushandlung replay hinweisen.|  
|4977|N/V|Mittel|Während der Schnellmodusverhandlung hat IPsec ein ungültiges verhandlungspaket empfangen. Wenn dieses Problem weiterhin auftritt, kann dies auf ein Netzwerkproblem oder zu ändern oder diese Aushandlung replay hinweisen.|  
|4978|N/V|Mittel|Während der erweiterungsmodusverhandlung hat IPsec ein ungültiges verhandlungspaket empfangen. Wenn dieses Problem weiterhin auftritt, kann dies auf ein Netzwerkproblem oder zu ändern oder diese Aushandlung replay hinweisen.|  
|4983|N/V|Mittel|Eine Aushandlung der IPsec-Erweiterungsmodus ist fehlgeschlagen. Die entsprechenden Hauptmodus-sicherheitszuordnung wurde gelöscht.|  
|4984|N/V|Mittel|Eine Aushandlung der IPsec-Erweiterungsmodus ist fehlgeschlagen. Die entsprechenden Hauptmodus-sicherheitszuordnung wurde gelöscht.|  
|5027|N/V|Mittel|Der Windows-Firewall-Dienst konnte die Sicherheitsrichtlinie aus dem lokalen Speicher abrufen. Der Dienst wird weiterhin die aktuelle Richtlinie zu erzwingen.|  
|5028|N/V|Mittel|Der Windows-Firewall-Dienst konnte die neue Sicherheitsrichtlinie nicht analysieren. Der Dienst weiterhin derzeit erzwungene Richtlinie.|  
|5029|N/V|Mittel|Der Windows-Firewalldienst konnte den Treiber nicht initialisieren. Der Dienst wird weiterhin die aktuelle Richtlinie zu erzwingen.|  
|5030|N/V|Mittel|Der Windows-Firewall-Dienst konnte nicht gestartet werden.|  
|5035|N/V|Mittel|Der Windows-Firewalltreiber konnte nicht gestartet werden.|  
|5037|N/V|Mittel|Der Windows-Firewalltreiber erkannt kritischen Laufzeitfehler. Beendet.|  
|5038|N/V|Mittel|Die Codeintegrität hat festgestellt, dass der abbildhash einer Datei nicht gültig ist. Die Datei aufgrund nicht autorisierte Änderung beschädigt oder des Datenträgergeräts kann auf einen potenziellen Fehler des Datenträgergeräts hinweisen.|  
|5120|N/V|Mittel|OCSP-Responder-Dienst wurde gestartet.|  
|5121|N/V|Mittel|OCSP-Responder-Dienst wurde beendet.|  
|5122|N/V|Mittel|OCSP-Responder-Dienst wurde ein Konfigurationseintrag|  
|5123|N/V|Mittel|OCSP-Responder-Dienst wurde ein Konfigurationseintrag|  
|5376|N/V|Mittel|Anmeldeinformationen der Anmeldeinformationsverwaltung wurden gesichert.|  
|5377|N/V|Mittel|Anmeldeinformationen der Anmeldeinformationsverwaltung wurden von einer Sicherung wiederhergestellt.|  
|5453|N/V|Mittel|Eine IPSec-Aushandlung mit einem Remotecomputer ist fehlgeschlagen, da der IKE- und AuthIP IPsec-Schlüsselerstellungsmodul-Module (IKEEXT)-Dienst nicht gestartet wurde.|  
|5480|N/V|Mittel|IPSec-Dienste konnten die vollständige Liste von Netzwerkschnittstellen auf dem Computer abzurufen. Dies stellt ein potenzielles Sicherheitsrisiko dar, da einige Netzwerkschnittstellen des Schutzes durch die angewendeten IPsec-Filter möglicherweise nicht. Das IP-Sicherheitsmonitor-Snap-in verwenden Sie, um das Problem zu diagnostizieren.|  
|5483|N/V|Mittel|Die IPsec-Dienste Fehler beim RPC-Server zu initialisieren. Die IPsec-Dienste konnten nicht gestartet werden.|  
|5484|N/V|Mittel|Die IPsec-Dienste Schwerwiegender Fehler ist aufgetreten und wurde heruntergefahren. Das Herunterfahren der IPsec-Dienste können Sie den Computer Risiko von Netzwerkangriffen versetzen oder den Computer und potenzielle Sicherheitsrisiken.|  
|5485|N/V|Mittel|IPsec-Dienste konnten einige IPSec-Filter für ein Plug & Play Ereignis für Netzwerkschnittstellen verarbeiten. Dies stellt ein potenzielles Sicherheitsrisiko dar, da einige Netzwerkschnittstellen des Schutzes durch die angewendeten IPsec-Filter möglicherweise nicht. Das IP-Sicherheitsmonitor-Snap-in verwenden Sie, um das Problem zu diagnostizieren.|  
|6145|N/V|Mittel|Verarbeitung der Sicherheitsrichtlinie in den Gruppenrichtlinienobjekten ist mindestens ein Fehler aufgetreten.|  
|6273|N/V|Mittel|Der Netzwerkrichtlinienserver verweigerte Zugriff für einen Benutzer.|  
|6274|N/V|Mittel|Der Netzwerkrichtlinienserver hat die Anforderung für einen Benutzer verworfen.|  
|6275|N/V|Mittel|Der Netzwerkrichtlinienserver hat die kontoführungsanforderung für einen Benutzer verworfen.|  
|6276|N/V|Mittel|Der Netzwerkrichtlinienserver unter Quarantäne gestellt ein Benutzers.|  
|6277|N/V|Mittel|Netzwerkrichtlinienserver-Zugriff für einen Benutzer ihn aber auf Probe gesetzt, da der Host die Integritätsrichtlinien nicht erfüllt.|  
|6278|N/V|Mittel|Der Netzwerkrichtlinienserver erteilt Vollzugriff für einen Benutzer, da der Host die Integritätsrichtlinien erfüllt.|  
|6279|N/V|Mittel|Das Benutzerkonto aufgrund mehrerer erfolgloser Authentifizierungsversuche gesperrt, Network Policy Server.|  
|6280|N/V|Mittel|Der Netzwerkrichtlinienserver entsperrt das Benutzerkonto.|  
|-|640|Mittel|Allgemeine Kontodatenbank geändert|  
|-|619|Mittel|Quality of Service-Richtlinie geändert|  
|24586|N/V|Mittel|Konvertieren von Volume ist ein Fehler aufgetreten|  
|24592|N/V|Mittel|Fehler beim Konvertierung auf dem Volume %2 automatisch neu gestartet.|  
|24593|N/V|Mittel|Metadaten schreiben: Volume %2 zurückgegebenen Fehler beim Versuch, Metadaten zu ändern. Wenn der Fehler weiterhin, Entschlüsseln von Volumes|  
|24594|N/V|Mittel|Metadaten neu erstellen: Schreiben Sie eine Kopie der Metadaten auf dem Volume %2 konnte nicht und als Beschädigtes Laufwerk angezeigt. Wenn der Fehler weiterhin, entschlüsseln Sie Volume.|  
|4608|512|Niedrig|Windows wird gestartet.|  
|4609|513|Niedrig|Windows wird heruntergefahren.|  
|4610|514|Niedrig|Ein Authentifizierungspaket wurde durch die lokale Sicherheitsinstanz geladen.|  
|4611|515|Niedrig|Ein vertrauenswürdiger Anmeldeprozess wurde bei der lokalen Sicherheitsautorität registriert.|  
|4612|516|Niedrig|Für die Queuing-Überwachung reservierte interne Ressourcen sind ausgelastet zu einem Verlust von Überwachungsereignissen.|  
|4614|518|Niedrig|Durch die Sicherheitskontenverwaltung hat ein Benachrichtigungspaket geladen.|  
|4615|519|Niedrig|Unzulässige Verwendung des LPC-Ports.|  
|4616|520|Niedrig|Die Systemzeit wurde geändert.|  
|4622|N/V|Niedrig|Durch die lokale Sicherheitsautorität hat ein Sicherheitspaket geladen wurde.|  
|4624|528,540|Niedrig|Ein Konto wurde erfolgreich angemeldet.|  
|4625|529-537,539|Niedrig|Ein Konto konnte sich nicht anmelden.|  
|4634|538|Niedrig|Ein Konto wurde abgemeldet.|  
|4646|N/V|Niedrig|IKE-DoS-Schutzmodus gestartet.|  
|4647|551|Niedrig|Benutzerinitiierte Abmeldung.|  
|4648|552|Niedrig|Anmeldeversuch mit expliziten Anmeldeinformationen.|  
|4650|N/V|Niedrig|Eine IPsec-Hauptmodus-sicherheitszuordnung wurde eingerichtet. Erweiterungsmodus wurde nicht aktiviert. Zertifikatauthentifizierung wurde nicht verwendet.|  
|4651|N/V|Niedrig|Eine IPsec-Hauptmodus-sicherheitszuordnung wurde eingerichtet. Erweiterungsmodus wurde nicht aktiviert. Ein Zertifikat wurde für die Authentifizierung verwendet.|  
|4652|N/V|Niedrig|Eine IPsec-Hauptmodus-Aushandlung ist fehlgeschlagen.|  
|4653|N/V|Niedrig|Eine IPsec-Hauptmodus-Aushandlung ist fehlgeschlagen.|  
|4654|N/V|Niedrig|Eine IPsec-Schnellmodus-Aushandlung ist fehlgeschlagen.|  
|4655|N/V|Niedrig|Eine IPsec-Hauptmodus-sicherheitszuordnung wurde beendet.|  
|4656|560|Niedrig|Ein Handle zu einem Objekt wurde angefordert.|  
|4657|567|Niedrig|Ein Registrierungswert wurde geändert.|  
|4658|562|Niedrig|Das Handle zu einem Objekt wurde geschlossen.|  
|4659|N/V|Niedrig|Ein Handle zu einem Objekt wurde mit Absicht löschen angefordert.|  
|4660|564|Niedrig|Ein Objekt wurde gelöscht.|  
|4661|565|Niedrig|Ein Handle zu einem Objekt wurde angefordert.|  
|4662|566|Niedrig|Für ein Objekt wurde ein Vorgang ausgeführt.|  
|4663|567|Niedrig|Es wurde versucht, auf ein Objekt zuzugreifen.|  
|4664|N/V|Niedrig|Es wurde versucht, einen festen Link zu erstellen.|  
|4665|N/V|Niedrig|Es wurde versucht, zum Erstellen eines anwendungsclientkontexts.|  
|4666|N/V|Niedrig|Eine Anwendung hat einen Vorgang versucht:|  
|4667|N/V|Niedrig|Eine Anwendung Clientkontext wurde gelöscht.|  
|4668|N/V|Niedrig|Initialisierung einer Anwendung.|  
|4670|N/V|Niedrig|Berechtigungen für ein Objekt wurden geändert.|  
|4671|N/V|Niedrig|Eine Anwendung hat versucht, auf eine blockierte über die Ordnungszahl zuzugreifen.|  
|4672|576|Niedrig|Besondere Rechte neuen Anmeldung zugewiesen.|  
|4673|577|Niedrig|Ein privilegierter Dienst wurde aufgerufen.|  
|4674|578|Niedrig|Es wurde ein Vorgang für ein privilegiertes Objekt versucht.|  
|4688|592|Niedrig|Ein neuer Prozess wurde erstellt.|  
|4689|593|Niedrig|Ein Prozess wurde beendet.|  
|4690|594|Niedrig|Es wurde versucht, einen Handle zu einem Objekt zu duplizieren.|  
|4691|595|Niedrig|Der indirekte Zugriff auf ein Objekt wurde angefordert.|  
|4694|N/V|Niedrig|Schutz überwachbarer geschützter Daten wurde versucht.|  
|4695|N/V|Niedrig|Wurde versucht, überwachbare geschützte Daten Unprotection.|  
|4696|600|Niedrig|Prozess wurde ein primäres Token zugewiesen.|  
|4697|601|Niedrig|Der Versuch, einen Dienst zu installieren|  
|4698|602|Niedrig|Eine geplante Aufgabe wurde erstellt.|  
|4699|602|Niedrig|Eine geplante Aufgabe wurde gelöscht.|  
|4700|602|Niedrig|Eine geplante Aufgabe wurde aktiviert.|  
|4701|602|Niedrig|Eine geplante Aufgabe wurde deaktiviert.|  
|4702|602|Niedrig|Eine geplante Aufgabe wurde aktualisiert.|  
|4704|608|Niedrig|Eine Benutzerberechtigung wurde zugewiesen.|  
|4705|609|Niedrig|Eine Benutzerberechtigung wurde entfernt.|  
|4707|611|Niedrig|Eine Vertrauensstellung zu einer Domäne wurde entfernt.|  
|4709|N/V|Niedrig|IPSec-Dienste wurden gestartet.|  
|4710|N/V|Niedrig|IPSec-Dienste wurden deaktiviert.|  
|4711|N/V|Niedrig|Kann eine der folgenden enthalten: das PAStore-Modul lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet. Das PAStore-Modul Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet. Das PAStore-Modul die lokale Registrierung Speicher-IPsec-Richtlinie auf dem Computer angewendet. Das PAStore-Modul konnte nicht lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie auf dem Computer anwenden. Das PAStore-Modul konnte Active Directory-Speicher-IPsec-Richtlinie auf dem Computer anwenden. Das PAStore-Modul konnte nicht lokalen Registrierung Speicher-IPsec-Richtlinie auf dem Computer anwenden. Das PAStore-Modul konnte einige Regeln der aktiven IPsec-Richtlinie auf dem Computer anwenden. Das PAStore-Modul konnte die Verzeichnisspeicher-IPsec-Richtlinie auf dem Computer zu laden. Das PAStore-Modul geladen Verzeichnisspeicher-IPSec-Richtlinie auf dem Computer. Das PAStore-Modul konnte nicht geladen werden lokalen Speicher-IPSec-Richtlinie auf dem Computer. Das PAStore-Modul geladen, lokalen Speicher-IPSec-Richtlinie auf dem Computer. Das PAStore-Modul Änderungen für die aktive IPsec-Richtlinie und keine Änderungen ermittelt.|  
|4712|N/V|Niedrig|Die IPsec-Dienste ist einen schwerwiegenden Fehler aufgetreten.|  
|4717|621|Niedrig|Ein Konto wurde Zugriff auf die Systemsicherheit gewährt.|  
|4718|622|Niedrig|Zugriff auf die Systemsicherheit wurde von einem Konto entfernt.|  
|4720|624|Niedrig|Ein Benutzerkonto wurde erstellt.|  
|4722|626|Niedrig|Ein Benutzerkonto wurde aktiviert.|  
|4723|627|Niedrig|Es wurde versucht, das Kennwort eines Kontos zu ändern.|  
|4725|629|Niedrig|Ein Benutzerkonto wurde deaktiviert.|  
|4726|630|Niedrig|Ein Benutzerkonto wurde gelöscht.|  
|4728|632|Niedrig|Eine sicherheitsaktivierte globale Gruppe wurde ein Mitglied hinzugefügt.|  
|4729|633|Niedrig|Eine sicherheitsaktivierte globale Gruppe wurde ein Mitglied entfernt.|  
|4730|634|Niedrig|Eine sicherheitsaktivierte globale Gruppe wurde gelöscht.|  
|4731|635|Niedrig|Eine sicherheitsaktivierte lokale Gruppe wurde erstellt.|  
|4732|636|Niedrig|Eine sicherheitsaktivierte lokale Gruppe wurde ein Mitglied hinzugefügt.|  
|4733|637|Niedrig|Eine sicherheitsaktivierte lokale Gruppe wurde ein Mitglied entfernt.|  
|4734|638|Niedrig|Eine sicherheitsaktivierte lokale Gruppe wurde gelöscht.|  
|4738|642|Niedrig|Ein Benutzerkonto wurde geändert.|  
|4740|644|Niedrig|Ein Benutzerkonto wurde gesperrt.|  
|4741|645|Niedrig|Ein Computerkonto wurde geändert.|  
|4742|646|Niedrig|Ein Computerkonto wurde geändert.|  
|4743|647|Niedrig|Ein Computerkonto wurde gelöscht.|  
|4744|648|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde erstellt.|  
|4745|649|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde geändert.|  
|4746|650|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde ein Mitglied hinzugefügt.|  
|4747|651|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde ein Mitglied entfernt.|  
|4748|652|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde gelöscht.|  
|4749|653|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde erstellt.|  
|4750|654|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde geändert.|  
|4751|655|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde ein Mitglied hinzugefügt.|  
|4752|656|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde ein Mitglied entfernt.|  
|4753|657|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde gelöscht.|  
|4756|660|Niedrig|Eine sicherheitsaktivierte universelle Gruppe wurde ein Mitglied hinzugefügt.|  
|4757|661|Niedrig|Eine sicherheitsaktivierte universelle Gruppe wurde ein Mitglied entfernt.|  
|4758|662|Niedrig|Eine sicherheitsaktivierte universelle Gruppe wurde gelöscht.|  
|4759|663|Niedrig|Eine sicherheitsdeaktivierte universelle Gruppe wurde erstellt.|  
|4760|664|Niedrig|Eine sicherheitsdeaktivierte universelle Gruppe wurde geändert.|  
|4761|665|Niedrig|Eine sicherheitsdeaktivierte universelle Gruppe wurde ein Mitglied hinzugefügt.|  
|4762|666|Niedrig|Eine sicherheitsdeaktivierte universelle Gruppe wurde ein Mitglied entfernt.|  
|4767|671|Niedrig|Ein Benutzerkonto wurde aufgehoben.|  
|4768|672,676|Niedrig|Ein Kerberos-Authentifizierungsticket (TGT) wurde angefordert.|  
|4769|673|Niedrig|Ein Kerberos-Dienstticket wurde angefordert.|  
|4770|674|Niedrig|Ein Kerberos-Dienstticket wurde erneuert.|  
|4771|675|Niedrig|Fehler bei der Kerberos-Vorauthentifizierung.|  
|4772|672|Niedrig|Ein Kerberos-authentifizierungsticketanforderung.|  
|4774|678|Niedrig|Ein Konto wurde für die Anmeldung zugeordnet.|  
|4775|679|Niedrig|Kein konnte Konto für die Anmeldung zugeordnet werden.|  
|4776|680,681|Niedrig|Der Domänencontroller hat versucht, die Anmeldeinformationen für ein Konto zu bestätigen.|  
|4777|N/V|Niedrig|Der Domänencontroller konnte die Anmeldeinformationen für ein Konto zu bestätigen.|  
|4778|682|Niedrig|Eine Sitzung wurde erneut mit einer Arbeitsstation verbunden werden.|  
|4779|683|Niedrig|Eine Sitzung wurde von einer Arbeitsstation getrennt.|  
|4781|685|Niedrig|Der Name eines Kontos wurde geändert:|  
|4782|N/V|Niedrig|Auf den Kennworthash eines Kontos wurde zugegriffen.|  
|4783|667|Niedrig|Eine Basisanwendungsgruppe wurde erstellt.|  
|4784|N/V|Niedrig|Eine Basisanwendungsgruppe wurde geändert.|  
|4785|689|Niedrig|Eine Basisanwendungsgruppe wurde ein Mitglied hinzugefügt.|  
|4786|690|Niedrig|Ein Mitglied wurde einer Basisanwendungsgruppe entfernt.|  
|4787|691|Niedrig|Eine Basisanwendungsgruppe wurde eine Memberfunktion hinzugefügt.|  
|4788|692|Niedrig|Ein nicht-Member wurde einer Basisanwendungsgruppe entfernt.|  
|4789|693|Niedrig|Eine Basisanwendungsgruppe wurde gelöscht.|  
|4790|694|Niedrig|Eine LDAP-Abfragegruppe wurde erstellt.|  
|4793|N/V|Niedrig|Die Kennwortrichtlinienprüfungs-API wurde aufgerufen.|  
|4800|N/V|Niedrig|Die Arbeitsstation wurde gesperrt.|  
|4801|N/V|Niedrig|Die Arbeitsstation wurde entsperrt.|  
|4802|N/V|Niedrig|Der Bildschirmschoner wurde aktiviert.|  
|4803|N/V|Niedrig|Der Bildschirmschoner wurde deaktiviert.|  
|4864|N/V|Niedrig|Ein Namespacekonflikt wurde erkannt.|  
|4869|773|Niedrig|Die Zertifikatdienste haben eine erneut eingereichte zertifikatanforderung erhalten.|  
|4871|775|Niedrig|Die Zertifikatdienste haben eine Anforderung zum Veröffentlichen der Zertifikatssperrliste (CRL) erhalten.|  
|4872|776|Niedrig|Die Zertifikatdienste haben die Zertifikatsperrliste (CRL) veröffentlicht.|  
|4873|777|Niedrig|Eine zertifikatanforderungserweiterung wurde geändert.|  
|4874|778|Niedrig|Eine oder mehrere Zertifikatanforderungsattribute wurden geändert.|  
|4875|779|Niedrig|Die Zertifikatdienste haben eine Anforderung zum Herunterfahren erhalten.|  
|4876|780|Niedrig|Die Sicherung der Zertifikatdienste wurde gestartet.|  
|4877|781|Niedrig|Die Sicherung der Zertifikatdienste wurde abgeschlossen.|  
|4878|782|Niedrig|Die Wiederherstellung der Zertifikatdienste wurde gestartet.|  
|4879|783|Niedrig|Beendet die Wiederherstellung der Zertifikatdienste.|  
|4880|784|Niedrig|Die Zertifikatdienste wurden gestartet.|  
|4881|785|Niedrig|Die Zertifikatdienste wurden beendet.|  
|4883|787|Niedrig|Zertifikatdienste abgerufen ein archivierten Schlüssels.|  
|4884|788|Niedrig|Zertifikatdienste importiert ein Zertifikat in seiner Datenbank.|  
|4886|790|Niedrig|Die Zertifikatdienste haben eine zertifikatanforderung erhalten.|  
|4887|791|Niedrig|Zertifikatdienste eine zertifikatanforderung genehmigt und ein Zertifikat ausgestellt hat.|  
|4888|792|Niedrig|Eine zertifikatanforderung wurde abgelehnt.|  
|4889|793|Niedrig|Zertifikatdienste legen Sie den Status einer zertifikatanforderung auf Ausstehend.|  
|4891|795|Niedrig|Es wurde ein Konfigurationseintrag in den Zertifikatdiensten geändert.|  
|4893|797|Niedrig|Zertifikatdienste haben einen Schlüssel archiviert.|  
|4894|798|Niedrig|Zertifikatdienste nicht importiert und haben einen Schlüssel archiviert.|  
|4895|799|Niedrig|Zertifikatsdienste veröffentlicht das Zertifizierungsstellenzertifikat auf dem Active Directory-Domänendiensten.|  
|4898|802|Niedrig|Zertifikatdienste haben eine Vorlage geladen.|  
|4902|N/V|Niedrig|Die Benutzerrichtlinien-Überwachungstabelle wurde erstellt.|  
|4904|N/V|Niedrig|Es wurde versucht, eine sicherheitsereignisquelle zu registrieren.|  
|4905|N/V|Niedrig|Es wurde versucht, eine sicherheitsereignisquelle aufzuheben.|  
|4909|N/V|Niedrig|Die lokalen Richtlinieneinstellungen für den TBS-Dienst wurden geändert.|  
|4910|N/V|Niedrig|Die gruppenrichtlinieneinstellungen für den TBS-Dienst wurden geändert.|  
|4928|N/V|Niedrig|Ein Active Directory replikatquellen wurde eingerichtet.|  
|4929|N/V|Niedrig|Ein Active Directory replikatquellen wurde entfernt.|  
|4930|N/V|Niedrig|Ein Active Directory replikatquellen wurde geändert.|  
|4931|N/V|Niedrig|Eine Active Directory-Replikat Ziel-Namenskontext wurde geändert.|  
|4932|N/V|Niedrig|Die Synchronisierung eines Replikats eines Active Directory-Namenskontextes wurde gestartet.|  
|4933|N/V|Niedrig|Synchronisierung eines Replikats eines Active Directory-Namenskontextes wurde beendet.|  
|4934|N/V|Niedrig|Attribute eines Active Directory-Objekts wurden repliziert.|  
|4935|N/V|Niedrig|Beginn des Replikationsfehlers.|  
|4936|N/V|Niedrig|Ende des Replikationsfehlers.|  
|4937|N/V|Niedrig|Ein veraltetes Objekt wurde aus einem Replikat entfernt.|  
|4944|N/V|Niedrig|Die folgende Richtlinie war beim Start der Windows-Firewall.|  
|4945|N/V|Niedrig|Beim Start der Windows-Firewall wurde eine Regel aufgelistet.|  
|4946|N/V|Niedrig|Um Ausnahmeliste der Windows-Firewall wurde eine Änderung vorgenommen wurde. Eine Regel wurde hinzugefügt.|  
|4947|N/V|Niedrig|Um Ausnahmeliste der Windows-Firewall wurde eine Änderung vorgenommen wurde. Eine Regel wurde geändert.|  
|4948|N/V|Niedrig|Um Ausnahmeliste der Windows-Firewall wurde eine Änderung vorgenommen wurde. Eine Regel wurde gelöscht.|  
|4949|N/V|Niedrig|Windows-Firewall-Einstellungen wurden auf die Standardwerte zurückgesetzt.|  
|4950|N/V|Niedrig|Eine Einstellung für die Windows-Firewall wurde geändert.|  
|4951|N/V|Niedrig|Eine Regel wurde ignoriert, da ihre Hauptversionsnummer nicht von der Windows-Firewall erkannt wurde.|  
|4952|N/V|Niedrig|Eine Regel wurde teilweise ignoriert, da ihre Nebenversionsnummer nicht von Windows-Firewall erkannt wurde. Die anderen Teile der Regel werden erzwungen.|  
|4953|N/V|Niedrig|Eine Regel wurde von der Windows-Firewall ignoriert, da die Regel nicht analysiert werden konnte.|  
|4954|N/V|Niedrig|Windows-Firewall-gruppenrichtlinieneinstellungen wurden geändert. Die neuen Einstellungen wurden angewendet.|  
|4956|N/V|Niedrig|Windows-Firewall hat das aktive Profil geändert.|  
|4957|N/V|Niedrig|Windows-Firewall hat die folgende Regel nicht angewendet:|  
|4958|N/V|Niedrig|Windows-Firewall hat die folgende Regel nicht angewendet, da die Regel auf Elemente, die auf diesem Computer nicht konfiguriert verwiesen:|  
|4979|N/V|Niedrig|IPsec-Hauptmodus und erweiterte sicherheitszuordnungen eingerichtet wurden.|  
|4980|N/V|Niedrig|IPsec-Hauptmodus und erweiterte sicherheitszuordnungen eingerichtet wurden.|  
|4981|N/V|Niedrig|IPsec-Hauptmodus und erweiterte sicherheitszuordnungen eingerichtet wurden.|  
|4982|N/V|Niedrig|IPsec-Hauptmodus und erweiterte sicherheitszuordnungen eingerichtet wurden.|  
|4985|N/V|Niedrig|Der Status einer Transaktion wurde geändert.|  
|5024|N/V|Niedrig|Der Windows-Firewalldienst wurde erfolgreich gestartet.|  
|5025|N/V|Niedrig|Der Windows-Firewall-Dienst wurde beendet.|  
|5031|N/V|Niedrig|Der Windows-Firewalldienst hat eine Anwendung keine eingehende Verbindungen im Netzwerk blockiert.|  
|5032|N/V|Niedrig|Windows-Firewall konnte den Benutzer benachrichtigen, dass eine Anwendung keine eingehende Verbindungen im Netzwerk blockiert.|  
|5033|N/V|Niedrig|Der Windows-Firewalltreiber wurde erfolgreich gestartet.|  
|5034|N/V|Niedrig|Der Windows-Firewalltreiber wurde beendet.|  
|5039|N/V|Niedrig|Ein Registrierungsschlüssel wurde virtualisiert.|  
|5040|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Ein Authentifizierungssatz wurde hinzugefügt.|  
|5041|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Ein Authentifizierungssatz wurde geändert.|  
|5042|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Ein Authentifizierungssatz wurde gelöscht.|  
|5043|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Eine Verbindungssicherheitsregel wurde hinzugefügt.|  
|5044|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Eine Verbindungssicherheitsregel wurde geändert.|  
|5045|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Eine Verbindungssicherheitsregel wurde gelöscht.|  
|5046|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Ein Kryptografiesatz wurde hinzugefügt.|  
|5047|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Ein Kryptografiesatz wurde geändert.|  
|5048|N/V|Niedrig|IPsec-Einstellungen hat eine Änderung vorgenommen wurde. Ein Kryptografiesatz wurde gelöscht.|  
|5050|N/V|Niedrig|Versuch, die Windows-Firewall mit einem Aufruf von InetFwProfile.FirewallEnabled(False) programmgesteuert deaktivieren|  
|5051|N/V|Niedrig|Eine Datei wurde virtualisiert.|  
|5056|N/V|Niedrig|Ein kryptografischer Selbsttest wurde ausgeführt.|  
|5057|N/V|Niedrig|Ein einfachen kryptografischer Vorgang ist fehlgeschlagen.|  
|5058|N/V|Niedrig|Schlüsseldateivorgang.|  
|5059|N/V|Niedrig|Schlüsselmigrationsvorgang.|  
|5060|N/V|Niedrig|Fehler bei der Überprüfung der Kryptografiesignatur.|  
|5061|N/V|Niedrig|Kryptografischen Vorgang.|  
|5062|N/V|Niedrig|Ein Kernelmodus-Selbsttest ausgeführt wurde.|  
|5063|N/V|Niedrig|Wurde versucht, ein kryptografieanbietervorgang auszuführen.|  
|5064|N/V|Niedrig|Wurde versucht, ein kryptografiekontextvorgang auszuführen.|  
|5065|N/V|Niedrig|Wurde versucht, eine Kryptografiekontext zu ändern.|  
|5066|N/V|Niedrig|Wurde versucht, ein kryptografiefunktionsvorgang auszuführen.|  
|5067|N/V|Niedrig|Wurde versucht, eine Kryptografiefunktion zu ändern.|  
|5068|N/V|Niedrig|Wurde versucht, ein kryptografiefunktionsvorgang-Anbieter.|  
|5069|N/V|Niedrig|Wurde versucht, ein kryptografiefunktionsvorgang-Eigenschaft.|  
|5070|N/V|Niedrig|Wurde versucht, eine kryptografiefunktionseigenschaft zu ändern.|  
|5125|N/V|Niedrig|Eine Anforderung wurde an die OCSP-Responder-Dienst übermittelt.|  
|5126|N/V|Niedrig|Signaturzertifikat wurde durch die OCSP-Responder-Dienst automatisch aktualisiert.|  
|5127|N/V|Niedrig|Der OCSP-Sperranbieter aktualisiert erfolgreich die Sperrinformationen|  
|5136|566|Niedrig|Ein Verzeichnisdienstobjekt wurde geändert.|  
|5137|566|Niedrig|Ein Verzeichnisdienstobjekt wurde erstellt.|  
|5138|N/V|Niedrig|Ein Verzeichnisdienstobjekt wurde wiederhergestellt.|  
|5139|N/V|Niedrig|Ein Verzeichnisdienstobjekt wurde verschoben.|  
|5140|N/V|Niedrig|Es wurde ein netzwerkfreigabeobjekt zugegriffen.|  
|5141|N/V|Niedrig|Ein Verzeichnisdienstobjekt wurde gelöscht.|  
|5152|N/V|Niedrig|Windows-Filterplattform hat ein Paket blockiert.|  
|5153|N/V|Niedrig|Ein stärker einschränkender Windows-Filterplattform-Filter hat ein Paket blockiert.|  
|5154|N/V|Niedrig|Windows-Filterplattform hat eine Anwendung oder einem Dienst auf einem Port auf eingehende Verbindungen abzuhören zugelassen.|  
|5155|N/V|Niedrig|Windows-Filterplattform hat eine Anwendung oder ein Dienst einen Port auf eingehende Verbindungen daran gehindert, blockiert.|  
|5156|N/V|Niedrig|Windows-Filterplattform hat eine Verbindung zugelassen.|  
|5157|N/V|Niedrig|Windows-Filterplattform hat eine Verbindung blockiert.|  
|5158|N/V|Niedrig|Windows-Filterplattform hat eine Bindung an einen lokalen Port zugelassen.|  
|5159|N/V|Niedrig|Windows-Filterplattform hat eine Bindung an einen lokalen Port blockiert.|  
|5378|N/V|Niedrig|Die angeforderten Anmeldeinformationen-Delegierung wurde durch eine Richtlinie nicht zugelassen.|  
|5440|N/V|Niedrig|Es war der folgende Callout vorhanden ist, wenn die Windows Filtering Basisfiltermoduls gestartet.|  
|5441|N/V|Niedrig|Es war der folgende Filter vorhanden ist, wenn die Windows Filtering Basisfiltermoduls gestartet.|  
|5442|N/V|Niedrig|Es war der folgende Anbieter vorhanden ist, wenn die Windows Filtering Basisfiltermoduls gestartet.|  
|5443|N/V|Niedrig|Der folgende Anbieterkontext war vorhanden, beim Starten von Windows Filtering Platform Basisfiltermoduls der.|  
|5444|N/V|Niedrig|Die folgende Unterebene wurde vorhanden ist, wenn die Windows Filtering Basisfiltermoduls gestartet.|  
|5446|N/V|Niedrig|Ein Callout der Windows-Filterplattform wurde geändert.|  
|5447|N/V|Niedrig|Ein Filter der Windows-Filterplattform wurde geändert.|  
|5448|N/V|Niedrig|Ein Anbieter der Windows-Filterplattform wurde geändert.|  
|5449|N/V|Niedrig|Ein Anbieterkontext der Windows-Filterplattform wurde geändert.|  
|5450|N/V|Niedrig|Eine Unterebene der Windows-Filterplattform wurde geändert.|  
|5451|N/V|Niedrig|Eine IPsec-Schnellmodus-sicherheitszuordnung wurde eingerichtet.|  
|5452|N/V|Niedrig|Eine IPsec-Schnellmodus-sicherheitszuordnung wurde beendet.|  
|5456|N/V|Niedrig|Das PAStore-Modul Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet.|  
|5457|N/V|Niedrig|Das PAStore-Modul konnte Active Directory-Speicher-IPsec-Richtlinie auf dem Computer anwenden.|  
|5458|N/V|Niedrig|Das PAStore-Modul lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet.|  
|5459|N/V|Niedrig|Das PAStore-Modul konnte nicht lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie auf dem Computer anwenden.|  
|5460|N/V|Niedrig|Das PAStore-Modul die lokale Registrierung Speicher-IPsec-Richtlinie auf dem Computer angewendet.|  
|5461|N/V|Niedrig|Das PAStore-Modul konnte nicht lokalen Registrierung Speicher-IPsec-Richtlinie auf dem Computer anwenden.|  
|5462|N/V|Niedrig|Das PAStore-Modul konnte einige Regeln der aktiven IPsec-Richtlinie auf dem Computer anwenden. Das IP-Sicherheitsmonitor-Snap-in verwenden Sie, um das Problem zu diagnostizieren.|  
|5463|N/V|Niedrig|Das PAStore-Modul Änderungen für die aktive IPsec-Richtlinie und keine Änderungen ermittelt.|  
|5464|N/V|Niedrig|Das PAStore-Modul Änderungen für die aktive IPsec-Richtlinie, Änderungen erkannt und sie auf die IPsec-Dienste angewendet.|  
|5465|N/V|Niedrig|Das PAStore-Modul hat eine Steuerung für das erneute Laden der IPsec-Richtlinie und die Steuerung erfolgreich verarbeitet.|  
|5466|N/V|Niedrig|Das PAStore-Modul abgerufen werden Änderungen an der Active Directory-IPsec-Richtlinie festgestellt, dass Active Directory kann nicht erreicht werden, und es die zwischengespeicherte Kopie der Active Directory-IPsec-Richtlinie stattdessen wird. Alle Änderungen, die für die Active Directory-IPsec-Richtlinie, die seit die letzte Abfrage nicht angewendet werden kann.|  
|5467|N/V|Niedrig|Das PAStore-Modul abgerufen werden Änderungen für die Active Directory-IPsec-Richtlinie festgestellt, dass Active Directory erreicht, und keine der Richtlinie Änderungen werden können. Die zwischengespeicherte Kopie der Active Directory-IPsec-Richtlinie wird nicht mehr verwendet.|  
|5468|N/V|Niedrig|Das PAStore-Modul abgerufen Änderungen für die Active Directory-IPsec-Richtlinie festgestellt, dass Active Directory erreicht werden kann, finden Sie Änderungen an der Richtlinie und die Änderungen angewendet werden. Die zwischengespeicherte Kopie der Active Directory-IPsec-Richtlinie wird nicht mehr verwendet.|  
|5471|N/V|Niedrig|Das PAStore-Modul geladen, lokalen Speicher-IPSec-Richtlinie auf dem Computer.|  
|5472|N/V|Niedrig|Das PAStore-Modul konnte nicht geladen werden lokalen Speicher-IPSec-Richtlinie auf dem Computer.|  
|5473|N/V|Niedrig|Das PAStore-Modul geladen Verzeichnisspeicher-IPSec-Richtlinie auf dem Computer.|  
|5474|N/V|Niedrig|Das PAStore-Modul konnte die Verzeichnisspeicher-IPsec-Richtlinie auf dem Computer zu laden.|  
|5477|N/V|Niedrig|Das PAStore-Modul konnte nicht Schnellmodusfilter.|  
|5479|N/V|Niedrig|Die IPsec-Dienste wurde erfolgreich beendet. Das Herunterfahren der IPsec-Dienste können Sie den Computer Risiko von Netzwerkangriffen versetzen oder den Computer und potenzielle Sicherheitsrisiken.|  
|5632|N/V|Niedrig|Eine Anforderung wurde mit einem drahtlosen Netzwerk authentifizieren.|  
|5633|N/V|Niedrig|Eine Anforderung wurde mit einem verkabelten Netzwerk authentifizieren.|  
|5712|N/V|Niedrig|Wurde versucht, einen Remoteprozeduraufruf (RPC).|  
|5888|N/V|Niedrig|Ein Objekt im COM+-Katalog wurde geändert.|  
|5889|N/V|Niedrig|Ein Objekt wurde aus dem COM+-Katalog gelöscht.|  
|5890|N/V|Niedrig|COM+-Katalog wurde ein Objekt hinzugefügt.|  
|6008|N/V|Niedrig|Das vorherige System wurde unerwartet heruntergefahren|  
|6144|N/V|Niedrig|Die Sicherheitsrichtlinie in den Gruppenrichtlinienobjekten wurde erfolgreich angewendet.|  
|6272|N/V|Niedrig|Der Netzwerkrichtlinienserver für einen Benutzer der Zugriff gewährt.|  
|N/V|561|Niedrig|Ein Handle zu einem Objekt wurde angefordert.|  
|N/V|563|Niedrig|Objekt kann zum Löschen|  
|N/V|625|Niedrig|Typ des Benutzerkontos geändert|  
|N/V|613|Niedrig|IPSec-Richtlinien-Agent gestartet|  
|N/V|614|Niedrig|IPSec-Richtlinien-Agent deaktiviert|  
|N/V|615|Niedrig|IPSec-Richtlinien-agent|  
|N/V|616|Niedrig|IPSec-Richtlinien-Agent hat einen potenziellen schwerwiegenden Fehler festgestellt.|  
|24577|N/V|Niedrig|Verschlüsselung von Volume gestartet|  
|24578|N/V|Niedrig|Verschlüsselung des Volumes wurde beendet.|  
|24579|N/V|Niedrig|Verschlüsselung von Volumes, die abgeschlossen|  
|24580|N/V|Niedrig|Entschlüsselung des Volumes wurde gestartet|  
|24581|N/V|Niedrig|Entschlüsselung des Volumes wurde beendet.|  
|24582|N/V|Niedrig|Entschlüsselung des Volumes abgeschlossen|  
|24583|N/V|Niedrig|Konvertierung Workerthread Volume gestartet|  
|24584|N/V|Niedrig|Konvertierung der Workerthread für Volume wurde vorübergehend angehalten.|  
|24588|N/V|Niedrig|Der Konvertierungsvorgang auf dem Volume %2 Fehler fehlerhafte Sektoren. Überprüfen Sie die Daten auf diesem volume|  
|24595|N/V|Niedrig|Datenträger %2 enthält fehlerhafte Cluster. Diese Cluster werden während der Konvertierung übersprungen.|  
|24621|N/V|Niedrig|Erste Status: für Volume-Konvertierung Transaktion ein auf %2.|  
|5049|N/V|Niedrig|Eine IPsec-Sicherheitszuordnung wurde gelöscht.|  
|5478|N/V|Niedrig|Die IPsec-Dienste wurde erfolgreich gestartet.|  
  
> [!NOTE]  
> Finden Sie unter [Microsoft Support-Artikel 947226](https://support.microsoft.com/kb/947226) für Listen der viele Sicherheits-IDs und deren Bedeutungen.  
>   
> Führen Sie **Wevtutil Gp Microsoft-Windows-Security-Auditing/ge /gm:true** eine detaillierte Liste der alle Ereignis-IDs abrufen  
  
Weitere Informationen zur Ereignis-IDs für Windows-Sicherheit und ihre Bedeutung finden Sie unter Microsoft Support-Artikel [Beschreibung von Sicherheitsereignissen in Windows Vista und Windows Server 2008](https://support.microsoft.com/kb/947226) und [Beschreibung von Sicherheitsereignissen in Windows 7 und Windows Server 2008 R2](https://support.microsoft.com/kb/977519). Sie können auch herunterladen [Sicherheit überwachen Ereignisse für Windows 7 und Windows Server 2008 R2](https://www.microsoft.com/download/details.aspx?id=21561) und [Windows 8 und Windows Server 2012 Einzelheiten zu Sicherheitsereignissen](https://www.microsoft.com/download/details.aspx?id=35753), die bieten detaillierte Informationen für die referenzierten Betriebssysteme im Kalkulationstabellenformat.  
  


