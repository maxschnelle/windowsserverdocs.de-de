---
ms.assetid: 99a68050-8d19-4c58-ad86-e08a3dcdb4f7
title: Anhang L-zu überwachende Ereignisse
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 07/30/2018
ms.topic: article
ms.openlocfilehash: 2c54a4615cf998b4f8358c71079ebe166bbd1d52
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969807"
---
# <a name="appendix-l-events-to-monitor"></a>Anhang L: Zu überwachende Ereignisse

>Gilt für: Windows Server

In der folgenden Tabelle sind die Ereignisse aufgelistet, die Sie in Ihrer Umgebung überwachen sollten, entsprechend der Empfehlungen, die im [Überwachungs Active Directory für Anzeichen einer](../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)Gefährdung aufgeführt werden. In der folgenden Tabelle wird in der Spalte "aktuelle Windows-Ereignis-ID" die Ereignis-ID aufgelistet, da Sie in Versionen von Windows und Windows Server implementiert ist, die derzeit in der Mainstream-Unterstützung sind.

In der Spalte "Legacy-Windows-Ereignis-ID" ist die entsprechende Ereignis-ID in älteren Versionen von Windows (z. b. Client Computern unter Windows XP oder früher) und Server mit Windows Server 2003 oder früher aufgeführt. In der Spalte "potenzielle Gefährlichkeit" wird angegeben, ob das Ereignis bei der Erkennung von Angriffen als niedrig, Mittel oder hoch kritisch angesehen werden soll, und die Spalte "Ereignis Zusammenfassung" enthält eine kurze Beschreibung des Ereignisses.

Eine mögliche Wichtigkeit von "High" bedeutet, dass ein Vorkommen des Ereignisses untersucht werden sollte. Die potenzielle Gefährlichkeit "Mittel" oder "niedrig" bedeutet, dass diese Ereignisse nur untersucht werden sollten, wenn Sie unerwartet oder in Zahlen auftreten, die die erwartete Baseline in einem gemessenen Zeitraum erheblich überschreiten. Alle Organisationen sollten diese Empfehlungen in ihrer Umgebung testen, bevor Warnungen erstellt werden, die verbindliche Untersuchungen erfordern. Jede Umgebung ist anders, und einige der Ereignisse, die mit einer potenziellen Gefährlichkeit von High eingestuft werden, können aufgrund anderer harmloser Ereignisse auftreten.

|**Aktuelle Windows-Ereignis-ID**|**Ältere Windows-Ereignis-ID**|**Potenzielle Gefährlichkeit**|**Ereigniszusammenfassung**|
|--|--|--|--|
|4618|Nicht zutreffend|Hoch|Ein überwachtes Sicherheitsmuster ist aufgetreten.|
|4649|Nicht zutreffend|Hoch|Ein Replay-Angriff wurde erkannt. Kann aufgrund eines fehl Konfigurations Fehlers ein harmloses falsch positives Ergebnis sein.|
|4719|612|Hoch|Die Systemüberwachungsrichtlinie wurde geändert.|
|4765|Nicht zutreffend|Hoch|Der SID-Verlauf eines Kontos wurde hinzugefügt.|
|4766|Nicht zutreffend|Hoch|Fehler beim Versuch, den SID-Verlauf einem Konto hinzuzufügen.|
|4794|Nicht zutreffend|Hoch|Es wurde versucht, den Verzeichnisdienst-Wiederherstellungsmodus einzustellen.|
|4897|801|Hoch|Rollentrennung ist aktiviert:|
|4964|Nicht zutreffend|Hoch|Sondergruppen wurden einer neuen Anmeldung zugewiesen.|
|5124|Nicht zutreffend|Hoch|Eine Sicherheitseinstellung wurde für den OCSP-Responder-Dienst aktualisiert.|
|Nicht zutreffend|550|Mittel bis hoch|Möglicher DOS-Angriff (Denial-of-Service)|
|1102|517|Mittel bis hoch|Das Überwachungs Protokoll wurde gelöscht.|
|4621|–|Medium|Der Administrator hat das System nach einem CrashOnAuditFail wiederhergestellt. Benutzer ohne Administratorrechte können sich jetzt anmelden. Einige überwachbare Aktivitäten wurden möglicherweise nicht aufgezeichnet.|
|4675|–|Medium|SIDs wurden gefiltert.|
|4692|–|Medium|Es wurde versucht, den Datenschutz-Hauptschlüssel zu sichern.|
|4693|–|Medium|Es wurde versucht, den Datenschutz-Hauptschlüssel wiederherzustellen.|
|4706|610|Medium|Eine neue Vertrauensstellung zu einer Domäne wurde erstellt.|
|4713|617|Medium|Die Kerberos-Richtlinie wurde geändert.|
|4714|618|Medium|Die Wiederherstellungsrichtlinie für verschlüsselte Daten wurde geändert.|
|4715|–|Medium|Die Überwachungsrichtlinie (SACL) für ein Objekt wurde geändert.|
|4716|620|Medium|Die Informationen bei einer vertrauenswürdigen Domäne wurden geändert.|
|4724|628|Medium|Es wurde versucht, das Kennwort eines Kontos zurückzusetzen.|
|4727|631|Medium|Eine sicherheitsaktivierte globale Gruppe wurde erstellt.|
|4735|639|Medium|Eine sicherheitsaktivierte lokale Gruppe wurde geändert.|
|4737|641|Medium|Eine sicherheitsaktivierte globale Gruppe wurde geändert.|
|4739|643|Medium|Die Domänenrichtlinie wurde geändert.|
|4754|658|Medium|Eine sicherheitsaktivierte universelle Gruppe wurde erstellt.|
|4755|659|Medium|Eine sicherheitsaktivierte universelle Gruppe wurde geändert.|
|4764|667|Medium|Eine Sicherheits deaktivierte Gruppe wurde gelöscht.|
|4764|668|Medium|Der Typ einer Gruppe wurde geändert.|
|4780|684|Medium|Die ACL wurde für Konten festgelegt, die Mitglieder der Gruppe „Administratoren“ sind.|
|4816|–|Medium|Der Remoteprozeduraufruf (RPC) hat bei der Entschlüsselung einer eingehenden Nachricht eine Integritätsverletzung festgestellt.|
|4865|–|Medium|Ein Informationseintrag für eine vertrauenswürdige Gesamtstruktur wurde hinzugefügt.|
|4866|–|Medium|Ein Informationseintrag für eine vertrauenswürdige Gesamtstruktur wurde entfernt.|
|4867|–|Medium|Ein Informationseintrag für eine vertrauenswürdige Gesamtstruktur wurde geändert.|
|4868|772|Medium|Die Zertifikatverwaltung hat eine anstehende Zertifikatanforderung abgelehnt.|
|4870|774|Medium|Die Zertifikatdienste haben ein Zertifikat gesperrt.|
|4882|786|Medium|Die Sicherheitsberechtigungen für die Zertifikatdienste wurden geändert.|
|4885|789|Medium|Der Überwachungsfilter für die Zertifikatdienste wurde geändert.|
|4890|794|Medium|Die Zertifikatverwaltungseinstellungen für die Zertifikatdienste wurden geändert.|
|4892|796|Medium|Es wurde eine Eigenschaft der Zertifikatdienste geändert.|
|4896|800|Medium|Eine oder mehrere Zeilen wurden aus der Zertifikatdatenbank gelöscht.|
|4906|–|Medium|Der CrashOnAuditFail-Wert wurde geändert.|
|4907|–|Medium|Die Überwachungseinstellungen für das Objekt wurden geändert.|
|4908|–|Medium|Eine Anmeldetabelle für Sondergruppen wurde geändert.|
|4912|807|Medium|Eine Benutzerüberwachungsrichtlinie wurde geändert.|
|4960|–|Medium|IPsec hat ein eingehendes Paket verworfen, das eine Integritätsüberprüfung nicht bestanden hat Wenn dieses Problem weiterhin besteht, kann dies darauf hinweisen, dass ein Netzwerkproblem vorliegt oder Pakete während der Übertragung an diesen Computer geändert werden. Vergewissern Sie sich, dass die vom Remotecomputer gesendeten Pakete mit den von diesem Computer empfangenen Paketen identisch sind. Dieser Fehler kann auch auf Interoperabilitätsprobleme mit anderen IPsec-Implementierungen hinweisen.|
|4961|–|Medium|IPsec hat ein eingehendes Paket verworfen, das eine Rahmenprüfung nicht bestanden hat. Wenn dieses Problem weiterhin besteht, kann dies auf einen Replay-Angriff auf diesen Computer hinweisen.|
|4962|–|Medium|IPsec hat ein eingehendes Paket verworfen, das eine Rahmenprüfung nicht bestanden hat. Die Sequenznummer des eingehenden Pakets war zu niedrig, um zu gewährleisten, dass es sich nicht um einen Replay-Angriff handelt.|
|4963|–|Medium|IPsec hat ein eingehendes Klartextpaket verworfen, das geschützt hätte sein sollen. Dies ist normalerweise darauf zurückzuführen, dass der Remotecomputer seine IPsec-Richtlinie ändert, ohne diesen Computer zu informieren. Es kann auch auf einen versuchten Spoofingangriff hinweisen.|
|4965|–|Medium|IPsec hat von einem Remotecomputer ein Paket mit einem falschen Sicherheitsparameterindex (SPI) empfangen. Dies ist normalerweise auf eine fehlerhafte Hardware zurückzuführen, die Pakete beschädigt. Vergewissern Sie sich, dass die vom Remotecomputer gesendeten Pakete mit den von diesem Computer empfangenen Paketen identisch sind, wenn diese Fehler weiterhin auftreten. Dieser Fehler kann auch auf Interoperabilitätsprobleme mit anderen IPsec-Implementierungen hinweisen. In diesem Fall können diese Ereignisse ignoriert werden, sofern die Konnektivität nicht beeinträchtigt ist.|
|4976|–|Medium|Während der Hauptmodusverhandlung hat IPsec ein ungültiges Verhandlungspaket empfangen. Wenn dieses Problem weiterhin besteht, kann dies darauf hinweisen, dass ein Netzwerkproblem vorliegt oder versucht wird, diese Verhandlung zu ändern oder durch einen Replay-Angriff zu manipulieren.|
|4977|–|Medium|Während der Schnellmodusverhandlung hat IPsec ein ungültiges Verhandlungspaket empfangen. Wenn dieses Problem weiterhin besteht, kann dies darauf hinweisen, dass ein Netzwerkproblem vorliegt oder versucht wird, diese Verhandlung zu ändern oder durch einen Replay-Angriff zu manipulieren.|
|4978|–|Medium|Während der Erweiterungsmodusverhandlung hat IPsec ein ungültiges Verhandlungspaket empfangen. Wenn dieses Problem weiterhin besteht, kann dies darauf hinweisen, dass ein Netzwerkproblem vorliegt oder versucht wird, diese Verhandlung zu ändern oder durch einen Replay-Angriff zu manipulieren.|
|4983|–|Medium|Fehler bei der Verhandlung des IPsec-Erweiterungsmodus. Die entsprechende Sicherheitszuordnung des Hauptmodus wurde gelöscht.|
|4984|–|Medium|Fehler bei der Verhandlung des IPsec-Erweiterungsmodus. Die entsprechende Sicherheitszuordnung des Hauptmodus wurde gelöscht.|
|5027|–|Medium|Der Windows-Firewalldienst konnte die Sicherheitsrichtlinie nicht aus dem lokalen Speicher abrufen. Der Dienst wendet weiterhin die aktuelle Richtlinie an.|
|5028|–|Medium|Der Windows-Firewalldienst konnte die neue Sicherheitsrichtlinie nicht analysieren. Der Dienst wendet weiterhin die aktuelle Richtlinie an.|
|5029|–|Medium|Der Windows-Firewalldienst konnte den Treiber nicht initialisieren. Der Dienst wendet weiterhin die aktuelle Richtlinie an.|
|5030|–|Medium|Der Windows-Firewalldienst konnte nicht gestartet werden.|
|5035|–|Medium|Der Windows-Firewalltreiber konnte nicht gestartet werden.|
|5037|–|Medium|Der Windows-Firewalltreiber hat einen kritischen Laufzeitfehler erkannt. Der Treiber wird beendet.|
|5038|–|Medium|Die Codeintegrität hat festgestellt, dass der Abbildhash einer Datei nicht gültig ist. Die Datei wurde möglicherweise durch eine nicht autorisierte Änderung beschädigt. Dieses Problem kann auch auf einen potenziellen Fehler des Datenträgergeräts hinweisen.|
|5120|–|Medium|OCSP-Responder-Dienst wurde gestartet.|
|5121|–|Medium|OCSP-Responder-Dienst wurde beendet.|
|5122|–|Medium|Ein Konfigurationseintrag wurde im OCSP-Responder-Dienst geändert.|
|5123|–|Medium|Ein Konfigurationseintrag wurde im OCSP-Responder-Dienst geändert.|
|5376|–|Medium|Anmeldeinformationen der Anmeldeinformationsverwaltung wurden gesichert.|
|5377|–|Medium|Anmeldeinformationen der Anmeldeinformationsverwaltung wurden von einer Sicherung wiederhergestellt.|
|5453|–|Medium|Eine IPsec-Aushandlung mit einem Remotecomputer war nicht erfolgreich, da der IKE- und AuthIP IPsec-Schlüsselerstellungsmodul-Dienst (IKEEXT) nicht gestartet wurde.|
|5480|–|Medium|Die IPsec-Dienste konnten die vollständige Liste von Netzwerkschnittstellen auf dem Computer nicht abrufen. Dies stellt ein potenzielles Sicherheitsrisiko dar, da einige Netzwerkschnittstellen möglicherweise nicht durch die angewendeten IPsec-Filter geschützt werden. Verwenden Sie das Snap-In „IP-Sicherheitsmonitor“, um das Problem zu diagnostizieren.|
|5483|–|Medium|Die IPsec-Dienste konnten den RPC-Server nicht initialisieren. Die IPsec-Dienste konnten nicht gestartet werden.|
|5484|–|Medium|In den IPsec-Diensten ist ein kritischer Fehler aufgetreten, und die Dienste wurden beendet. Das Beenden der IPsec-Dienste kann das Risiko von Netzwerkangriffen auf den Computer und potenzielle Sicherheitsrisiken erhöhen.|
|5485|–|Medium|Die IPsec-Dienste konnten einige IPsec-Filter für ein Plug-and-Play-Ereignis für Netzwerkschnittstellen nicht verarbeiten. Dies stellt ein potenzielles Sicherheitsrisiko dar, da einige Netzwerkschnittstellen möglicherweise nicht durch die angewendeten IPsec-Filter geschützt werden. Verwenden Sie das Snap-In „IP-Sicherheitsmonitor“, um das Problem zu diagnostizieren.|
|6145|–|Medium|Beim Verarbeiten der Sicherheitsrichtlinie in den Gruppenrichtlinie Objekten ist mindestens ein Fehler aufgetreten.|
|6273|–|Medium|Der Netzwerkrichtlinienserver verweigerte einem Benutzer den Zugriff.|
|6274|–|Medium|Der Netzwerkrichtlinienserver hat die Anforderung für einen Benutzer verworfen.|
|6275|–|Medium|Der Netzwerkrichtlinienserver hat die Kontoführungsanforderung für einen Benutzer verworfen.|
|6276|–|Medium|Der Netzwerkrichtlinienserver hat einen Benutzer unter Quarantäne gestellt.|
|6277|–|Medium|Der Netzwerkrichtlinienserver hat einem Benutzer den Zugriff gewährt, ihn aber auf Probe gesetzt, da der Host die definierten Integritätsrichtlinien nicht erfüllt.|
|6278|–|Medium|Der Netzwerkrichtlinienserver hat einem Benutzer Vollzugriff erteilt, da der Host die Integritätsrichtlinien erfüllt.|
|6279|–|Medium|Der Netzwerkrichtlinienserver hat das Benutzerkonto aufgrund mehrerer erfolgloser Authentifizierungsversuche gesperrt.|
|6280|–|Medium|Der Netzwerkrichtlinienserver hat die Sperre des Benutzerkontos aufgehoben.|
|-|640|Medium|Allgemeine Konto Datenbank geändert|
|-|619|Medium|Quality of Service Richtlinie geändert|
|24586|–|Medium|Beim Umrechnen des Volumes ist ein Fehler aufgetreten.|
|24592|–|Medium|Fehler beim automatischen Neustart der Konvertierung auf Volume "%2".|
|24593|–|Medium|Metadaten schreiben: Volume %2 gibt Fehler zurück, wenn versucht wird, Metadaten zu ändern. Wenn Fehler weiterhin auftreten, entschlüsseln Sie das Volume.|
|24594|–|Medium|Metadatenneu Erstellung: Fehler beim Schreiben einer Kopie der Metadaten auf Volume "%2". Wenn der Fehler weiterhin besteht, entschlüsseln Sie das Volume.|
|4608|512|Niedrig|Windows wird gestartet.|
|4609|513|Niedrig|Windows wird heruntergefahren.|
|4610|514|Niedrig|Ein Authentifizierungspaket wurde durch die lokale Sicherheitsinstanz geladen.|
|4611|515|Niedrig|Ein vertrauenswürdiger Anmeldeprozess wurde bei der lokalen Sicherheitsautorität registriert.|
|4612|516|Niedrig|Die für die Überwachung reservierten internen Ressourcen sind ausgelastet. Dies wird zu einem Verlust von Überwachungsereignissen führen.|
|4614|518|Niedrig|Die Sicherheitskontenverwaltung hat ein Benachrichtigungspaket geladen.|
|4615|519|Niedrig|Unzulässige Verwendung des LPC-Ports.|
|4616|520|Niedrig|Die Systemzeit wurde geändert.|
|4622|Nicht zutreffend|Niedrig|Die LSA (Local Security Authority) hat ein Sicherheitspaket geladen.|
|4624|528.540|Niedrig|Ein Konto wurde erfolgreich angemeldet.|
|4625|529-537539|Niedrig|Fehler beim Anmelden eines Kontos.|
|4634|538|Niedrig|Ein Konto wurde abgemeldet.|
|4646|Nicht zutreffend|Niedrig|Der IKE-DoS-Präventions Modus wurde gestartet.|
|4647|551|Niedrig|Benutzerinitiierte Abmeldung.|
|4648|552|Niedrig|Anmeldeversuch mit expliziten Anmeldeinformationen.|
|4.650|Nicht zutreffend|Niedrig|Eine Sicherheitszuordnung des IPsec-Hauptmodus wurde eingerichtet. Der Erweiterungsmodus wurde nicht aktiviert. Zertifikatauthentifizierung wurde nicht verwendet.|
|4651|Nicht zutreffend|Niedrig|Eine Sicherheitszuordnung des IPsec-Hauptmodus wurde eingerichtet. Der Erweiterungsmodus wurde nicht aktiviert. Zertifikatauthentifizierung wurde verwendet.|
|4652|Nicht zutreffend|Niedrig|Fehler bei einer IPsec-Hauptmodusverhandlung.|
|4653|Nicht zutreffend|Niedrig|Fehler bei einer IPsec-Hauptmodusverhandlung.|
|4654|Nicht zutreffend|Niedrig|Fehler bei der IPSec-Schnellmodus-Aushandlung.|
|4655|Nicht zutreffend|Niedrig|Beendigung einer IPsec-Hauptmodusverhandlung.|
|4656|560|Niedrig|Ein Handle zu einem Objekt wurde angefordert.|
|4657|567|Niedrig|Ein Registrierungswert wurde geändert.|
|4658|562|Niedrig|Ein Handle zu einem Objekt wurde geschlossen.|
|4659|Nicht zutreffend|Niedrig|Ein Handle zu einem Objekt wurde angefordert mit der Absicht, es zu löschen.|
|4660|564|Niedrig|Ein Objekt wurde gelöscht.|
|4661|565|Niedrig|Ein Handle zu einem Objekt wurde angefordert.|
|4662|566|Niedrig|Für ein Objekt wurde ein Vorgang ausgeführt.|
|4663|567|Niedrig|Es wurde versucht, auf das Objekt zuzugreifen.|
|4664|Nicht zutreffend|Niedrig|Es wurde versucht, eine feste Verknüpfung herzustellen.|
|4665|Nicht zutreffend|Niedrig|Es wurde versucht, einen Anwendungsclientkontext zu erstellen.|
|4666|Nicht zutreffend|Niedrig|Eine Anwendung hat einen Vorgang versucht:|
|4667|Nicht zutreffend|Niedrig|Löschung des Anwendungsclientkontexts.|
|4668|Nicht zutreffend|Niedrig|Initialisierung einer Anwendung.|
|4670|Nicht zutreffend|Niedrig|Berechtigungen für ein Objekt wurden geändert.|
|4671|Nicht zutreffend|Niedrig|Eine Anwendung hat versucht, über den TBS-Dienst auf eine blockierte Ordnungszahl zuzugreifen.|
|4672|576|Niedrig|Einer neuen Anmeldung wurden besondere Rechte zugewiesen.|
|4673|577|Niedrig|Ein privilegierter Dienst wurde aufgerufen.|
|4674|578|Niedrig|Es wurde versucht, einen Vorgang für ein privilegiertes Objekt auszuführen.|
|4688|592|Niedrig|Ein neuer Prozess wurde erstellt.|
|4689|593|Niedrig|Ein Prozess wurde beendet.|
|4690|594|Niedrig|Es wurde versucht, ein Handle zu einem Objekt zu duplizieren.|
|4.691|595|Niedrig|Der indirekte Zugriff auf ein Objekt wurde angefordert.|
|4694|Nicht zutreffend|Niedrig|Es wurde versucht, überwachbare geschützte Daten zu schützen.|
|4695|Nicht zutreffend|Niedrig|Es wurde versucht, den Schutz überwachbarer geschützter Daten aufzuheben.|
|4696|600|Niedrig|Ein primäres Token wurde der Verarbeitung zugewiesen.|
|4697|601|Niedrig|Es wurde versucht, einen Dienst zu installieren|
|4698|602|Niedrig|Eine geplante Aufgabe wurde erstellt.|
|4699|602|Niedrig|Eine geplante Aufgabe wurde gelöscht.|
|4700|602|Niedrig|Eine geplante Aufgabe wurde aktiviert.|
|4701|602|Niedrig|Eine geplante Aufgabe wurde deaktiviert.|
|4702|602|Niedrig|Eine geplante Aufgabe wurde aktualisiert.|
|4704|608|Niedrig|Eine Benutzerberechtigung wurde zugewiesen.|
|4705|609|Niedrig|Eine Benutzerberechtigung wurde entfernt.|
|4707|611|Niedrig|Eine Vertrauensstellung zu einer Domäne wurde entfernt.|
|4709|Nicht zutreffend|Niedrig|Die IPsec-Dienste wurden gestartet.|
|4710|Nicht zutreffend|Niedrig|Die IPsec-Dienste wurden deaktiviert.|
|4711|Nicht zutreffend|Niedrig|Kann eine der folgenden folgenden Zeichen enthalten: eine lokal zwischengespeicherte Kopie der IPSec-Richtlinie des Active Directory Speichers auf dem Computer. Das PAStore-Modul hat eine Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet. Das PAStore-Modul hat eine Speicher-IPsec-Richtlinie der lokalen Registrierung auf dem Computer angewendet. Das PAStore-Modul konnte die lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie nicht auf dem Computer anwenden. Das PAStore-Modul konnte die Active Directory-Speicher-IPsec-Richtlinie nicht auf dem Computer anwenden. Das PAStore-Modul konnte die Speicher-IPsec-Richtlinie der lokalen Registrierung nicht auf dem Computer anwenden. Das PAStore-Modul konnte einige Regeln der aktiven IPsec-Richtlinie nicht auf dem Computer anwenden. Das PAStore-Modul konnte die Verzeichnisspeicher-IPsec-Richtlinie nicht auf dem Computer laden. Das PAStore-Modul hat die Verzeichnisspeicher-IPsec-Richtlinie auf dem Computer geladen. Das PAStore-Modul konnte die lokale Speicher-IPsec-Richtlinie nicht auf dem Computer laden. Die Speicher-Engine hat die IPSec-Richtlinie des lokalen Speichers auf dem Computer geladen. Die Store-Engine hat Änderungen an der aktiven IPSec-Richtlinie abgerufen, und es wurden keine Änderungen erkannt. |
|4712|Nicht zutreffend|Niedrig|Schwerwiegender Fehler beim IPsec-Dienst.|
|4717|621|Niedrig|Einem Konto wurde der Zugriff auf die Systemsicherheit gewährt.|
|4718|622|Niedrig|Der Zugriff auf die Systemsicherheit wurde von einem Konto entfernt.|
|4720|624|Niedrig|Ein Benutzerkonto wurde erstellt.|
|4722|626|Niedrig|Ein Benutzerkonto wurde aktiviert.|
|4723|627|Niedrig|Es wurde versucht, das Kennwort eines Kontos zu ändern.|
|4725|629|Niedrig|Ein Benutzerkonto wurde deaktiviert.|
|4726|630|Niedrig|Ein Benutzerkonto wurde gelöscht.|
|4728|632|Niedrig|Ein Mitglied einer sicherheitsaktivierten globalen Gruppe wurde hinzugefügt.|
|4729|633|Niedrig|Ein Mitglied einer sicherheitsaktivierten globalen Gruppe wurde entfernt.|
|4730|634|Niedrig|Eine sicherheitsaktivierte globale Gruppe wurde gelöscht.|
|4731|635|Niedrig|Eine sicherheitsaktivierte lokale Gruppe wurde erstellt.|
|4732|636|Niedrig|Ein Mitglied einer sicherheitsaktivierten lokalen Gruppe wurde hinzugefügt.|
|4733|637|Niedrig|Ein Mitglied einer sicherheitsaktivierten lokalen Gruppe wurde entfernt.|
|4734|638|Niedrig|Eine sicherheitsaktivierte lokale Gruppe wurde gelöscht.|
|4738|642|Niedrig|Ein Benutzerkonto wurde geändert.|
|4740|644|Niedrig|Ein Benutzerkonto wurde gesperrt.|
|4741|645|Niedrig|Ein Computerkonto wurde geändert.|
|4742|646|Niedrig|Ein Computerkonto wurde geändert.|
|4743|647|Niedrig|Ein Computerkonto wurde gelöscht.|
|4744|648|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde erstellt.|
|4745|649|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde geändert.|
|4746|650|Niedrig|Ein Mitglied einer sicherheitsdeaktivierten lokalen Gruppe wurde hinzugefügt.|
|4747|651|Niedrig|Ein Mitglied einer sicherheitsdeaktivierten lokalen Gruppe wurde entfernt.|
|4748|652|Niedrig|Eine sicherheitsdeaktivierte lokale Gruppe wurde gelöscht.|
|4749|653|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde erstellt.|
|4750|654|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde geändert.|
|4751|655|Niedrig|Ein Mitglied einer sicherheitsdeaktivierten globalen Gruppe wurde hinzugefügt.|
|4752|656|Niedrig|Ein Mitglied einer sicherheitsdeaktivierten globalen Gruppe wurde entfernt.|
|4753|657|Niedrig|Eine sicherheitsdeaktivierte globale Gruppe wurde gelöscht.|
|4756|660|Niedrig|Ein Mitglied einer sicherheitsaktivierten universellen Gruppe wurde hinzugefügt.|
|4757|661|Niedrig|Ein Mitglied einer sicherheitsaktivierten universellen Gruppe wurde entfernt.|
|4758|662|Niedrig|Eine sicherheitsaktivierte universelle Gruppe wurde gelöscht.|
|4759|663|Niedrig|Eine sicherheitsdeaktivierte universelle Gruppe wurde erstellt.|
|4760|664|Niedrig|Eine sicherheitsdeaktivierte universelle Gruppe wurde geändert.|
|4.761|665|Niedrig|Ein Mitglied einer sicherheitsdeaktivierten universellen Gruppe wurde hinzugefügt.|
|4762|666|Niedrig|Ein Mitglied einer sicherheitsdeaktivierten universellen Gruppe wurde entfernt.|
|4767|671|Niedrig|Die Sperrung eines Benutzerkontos wurde aufgehoben.|
|4768|672.676|Niedrig|Ein Kerberos-Authentifizierungsticket (TGT) wurde angefordert.|
|4769|673|Niedrig|Ein Kerberos-Dienstticket wurde angefordert.|
|4770|674|Niedrig|Ein Kerberos-Dienstticket wurde erneuert.|
|4771|675|Niedrig|Die Kerberos-Vorauthentifizierung ist fehlgeschlagen.|
|4772|672|Niedrig|Fehler bei einer Kerberos-Authentifizierungsticketanforderung.|
|4774|678|Niedrig|Ein Konto wurde für die Anmeldung zugeordnet.|
|4775|679|Niedrig|Es konnte kein Konto für die Anmeldung zugeordnet werden.|
|4776|680.681|Niedrig|Der Domänencontroller hat versucht, die Anmeldeinformationen für ein Konto zu bestätigen.|
|4777|Nicht zutreffend|Niedrig|Der Domänencontroller konnte die Anmeldeinformationen für ein Konto nicht bestätigen.|
|4778|682|Niedrig|Eine Sitzung wurde erneut mit einer Arbeitsstation verbunden.|
|4779|683|Niedrig|Eine Sitzung wurde von einer Arbeitsstation getrennt.|
|4781|685|Niedrig|Der Name eines Kontos wurde geändert:|
|4782|Nicht zutreffend|Niedrig|Der Kenn Wort Hash, auf den ein Konto zugegriffen hat.|
|4783|667|Niedrig|Eine Basisanwendungsgruppe wurde erstellt.|
|4784|Nicht zutreffend|Niedrig|Eine Basisanwendungsgruppe wurde geändert.|
|4785|689|Niedrig|Einer Basisanwendungsgruppe wurde ein Mitglied hinzugefügt.|
|4786|690|Niedrig|Ein Mitglied einer Basisanwendungsgruppe wurde entfernt.|
|4787|691|Niedrig|Ein nicht Mitglied wurde einer einfachen Anwendungs Gruppe hinzugefügt.|
|4788|692|Niedrig|Ein nicht Mitglied wurde aus einer einfachen Anwendungs Gruppe entfernt.|
|4789|693|Niedrig|Eine Basisanwendungsgruppe wurde gelöscht.|
|4790|694|Niedrig|Eine LDAP-Abfragegruppe wurde erstellt.|
|4793|Nicht zutreffend|Niedrig|Die Kennwortrichtlinienprüfungs-API wurde aufgerufen.|
|4800|Nicht zutreffend|Niedrig|Die Arbeitsstation wurde gesperrt.|
|4801|Nicht zutreffend|Niedrig|Die Arbeitsstation wurde entsperrt.|
|4802|Nicht zutreffend|Niedrig|Der Bildschirmschoner wurde aktiviert.|
|4803|Nicht zutreffend|Niedrig|Der Bildschirmschoner wurde deaktiviert.|
|4864|Nicht zutreffend|Niedrig|Ein Namespacekonflikt wurde erkannt.|
|4869|773|Niedrig|Die Zertifikatdienste haben eine erneut eingereichte Zertifikatanforderung erhalten.|
|4871|775|Niedrig|Die Zertifikatdienste haben eine Anforderung zum Veröffentlichen der Zertifikatssperrliste erhalten.|
|4872|776|Niedrig|Die Zertifikatdienste haben die Zertifikatsperrliste veröffentlicht.|
|4873|777|Niedrig|Eine Zertifikatanforderungserweiterung wurde geändert.|
|4874|778|Niedrig|Ein oder mehrere Zertifikatanforderungsattribute wurden geändert.|
|4875|779|Niedrig|Die Zertifikatdienste haben eine Anforderung zum Herunterfahren erhalten.|
|4876|780|Niedrig|Die Sicherung der Zertifikatdienste wurde gestartet.|
|4877|781|Niedrig|Die Sicherung der Zertifikatdienste wurde abgeschlossen.|
|4878|782|Niedrig|Die Wiederherstellung der Zertifikatdienste wurde gestartet.|
|4879|783|Niedrig|Die Wiederherstellung der Zertifikatdienste wurde beendet.|
|4880|784|Niedrig|Die Zertifikatdienste wurden gestartet.|
|4881|785|Niedrig|Die Zertifikatdienste wurden beendet.|
|4883|787|Niedrig|Die Zertifikatdienste haben einen archivierten Schlüssel abgerufen.|
|4884|788|Niedrig|Die Zertifikatdienste haben ein Zertifikat in ihre Datenbank importiert.|
|4886|790|Niedrig|Die Zertifikatdienste haben eine Zertifikatanforderung empfangen.|
|4887|791|Niedrig|Die Zertifikatdienste haben eine Zertifikatanforderung genehmigt und ein Zertifikat ausgestellt.|
|4888|792|Niedrig|Die Zertifikatdienste haben eine Zertifikatanforderung abgelehnt.|
|4889|793|Niedrig|Die Zertifikatdienste haben den Status einer Zertifikatanforderung als "anstehend" festgelegt.|
|4891|795|Niedrig|Es wurde ein Konfigurationseintrag in den Zertifikatdiensten geändert.|
|4893|797|Niedrig|Zertifikatdienste haben einen Schlüssel archiviert.|
|4894|798|Niedrig|Zertifikatdienste haben einen Schlüssel importiert und archiviert.|
|4895|799|Niedrig|Die Zertifikatdienste haben das Zertifizierungsstellenzertifikat bei den Active Directory-Domänendiensten veröffentlicht.|
|4898|802|Niedrig|Die Zertifikatdienste haben eine Vorlage geladen.|
|4902|Nicht zutreffend|Niedrig|Eine Benutzerrichtlinien-Überwachungstabelle wurde erstellt.|
|4904|Nicht zutreffend|Niedrig|Es wurde versucht, eine Sicherheitsereignisquelle zu registrieren|
|4905|Nicht zutreffend|Niedrig|Es wurde versucht, die Registrierung einer Sicherheitsereignisquelle aufzuheben.|
|4909|Nicht zutreffend|Niedrig|Die lokalen Richtlinieneinstellungen für den TBS-Dienst wurden geändert.|
|4910|Nicht zutreffend|Niedrig|Die Gruppenrichtlinie Einstellungen für die TSB wurden geändert.|
|4928|Nicht zutreffend|Niedrig|Ein Namenskontext für Active Directory-Replikatquellen wurde eingerichtet.|
|4929|Nicht zutreffend|Niedrig|Ein Namenskontext für Active Directory-Replikatquellen wurde entfernt.|
|4930|Nicht zutreffend|Niedrig|Ein Namenskontext für Active Directory-Replikatquellen wurde geändert.|
|4931|Nicht zutreffend|Niedrig|Ein Namenskontext für Active Directory-Replikatziele wurde eingerichtet.|
|4932|Nicht zutreffend|Niedrig|Die Synchronisierung eines Replikats eines Active Directory-Namenskontextes wurde gestartet.|
|4933|Nicht zutreffend|Niedrig|Die Synchronisierung eines Replikats eines Active Directory-Namenskontextes wurde beendet.|
|4934|Nicht zutreffend|Niedrig|Die Attribute eines Active Directory-Objekts wurden repliziert.|
|4935|Nicht zutreffend|Niedrig|Beginn des Replikationsfehlers.|
|4936|Nicht zutreffend|Niedrig|Ende des Replikationsfehlers.|
|4937|Nicht zutreffend|Niedrig|Ein veraltetes Objekt wurde aus einem Replikat entfernt.|
|4944|Nicht zutreffend|Niedrig|Die folgende Richtlinie war beim Start der Windows-Firewall aktiv.|
|4945|Nicht zutreffend|Niedrig|Beim Start der Windows-Firewall wurde eine Regel aufgelistet.|
|4946|Nicht zutreffend|Niedrig|Die Ausnahmeliste der Windows-Firewall wurde geändert. Eine Regel wurde hinzugefügt.|
|4947|Nicht zutreffend|Niedrig|Die Ausnahmeliste der Windows-Firewall wurde geändert. Eine Regel wurde geändert.|
|4948|Nicht zutreffend|Niedrig|Die Ausnahmeliste der Windows-Firewall wurde geändert. Eine Regel wurde gelöscht.|
|4949|Nicht zutreffend|Niedrig|Die Einstellungen der Windows-Firewall wurden auf die Standardwerte zurückgesetzt.|
|4950|Nicht zutreffend|Niedrig|Eine Windows-Firewalleinstellung wurde geändert.|
|4951|Nicht zutreffend|Niedrig|Eine Regel wurde ignoriert, da ihre Hauptversionsnummer nicht von der Windows-Firewall erkannt wurde.|
|4952|Nicht zutreffend|Niedrig|Eine Regel wurde teilweise ignoriert, da ihre Nebenversionsnummer nicht von der Windows-Firewall erkannt wurde. Die anderen Teile der Regel werden angewendet.|
|4953|Nicht zutreffend|Niedrig|Eine Regel wurde von der Windows-Firewall ignoriert, da die Regel nicht analysiert werden konnte.|
|4954|Nicht zutreffend|Niedrig|Die Windows-Firewall-Gruppenrichtlinieneinstellungen wurden geändert. Die neuen Einstellungen wurden angewendet.|
|4956|Nicht zutreffend|Niedrig|Die Windows-Firewall hat das aktive Profil geändert.|
|4957|Nicht zutreffend|Niedrig|Die Windows-Firewall hat die folgende Regel nicht angewendet:|
|4958|Nicht zutreffend|Niedrig|Die Windows-Firewall hat die folgende Regel nicht angewendet, da die Regel auf Elemente verweist, die auf diesem Computer nicht konfiguriert sind:|
|4979|Nicht zutreffend|Niedrig|Sicherheitszuordnungen für den IPsec-Hauptmodus und -Erweiterungsmodus wurden eingerichtet.|
|4980|Nicht zutreffend|Niedrig|Sicherheitszuordnungen für den IPsec-Hauptmodus und -Erweiterungsmodus wurden eingerichtet.|
|4981|Nicht zutreffend|Niedrig|Sicherheitszuordnungen für den IPsec-Hauptmodus und -Erweiterungsmodus wurden eingerichtet.|
|4982|Nicht zutreffend|Niedrig|Sicherheitszuordnungen für den IPsec-Hauptmodus und -Erweiterungsmodus wurden eingerichtet.|
|4985|Nicht zutreffend|Niedrig|Der Status einer Transaktion wurde geändert.|
|5024|Nicht zutreffend|Niedrig|Der Windows-Firewalldienst wurde erfolgreich gestartet.|
|5025|Nicht zutreffend|Niedrig|Der Windows-Firewalldienst wurde beendet.|
|5031|Nicht zutreffend|Niedrig|Der Windows-Firewalldienst hat eine Anwendung blockiert, sodass sie keine eingehenden Verbindungen im Netzwerk annehmen kann|
|5032|Nicht zutreffend|Niedrig|Der Windows-Firewalldienst konnte den Benutzer nicht darüber benachrichtigen, dass eine Anwendung blockiert wurde und keine eingehenden Verbindungen im Netzwerk annehmen kann.|
|5033|Nicht zutreffend|Niedrig|Der Windows-Firewalltreiber wurde erfolgreich gestartet.|
|5034|Nicht zutreffend|Niedrig|Der Windows-Firewalltreiber wurde beendet.|
|5039|Nicht zutreffend|Niedrig|Ein Registrierungsschlüssel wurde virtualisiert.|
|5040|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Ein Authentifizierungssatz wurde hinzugefügt.|
|5041|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Ein Authentifizierungssatz wurde geändert.|
|5042|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Ein Authentifizierungssatz wurde gelöscht.|
|5043|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Eine Verbindungssicherheitsregel wurde hinzugefügt.|
|5044|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Eine Verbindungssicherheitsregel wurde geändert.|
|5045|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Eine Verbindungssicherheitsregel wurde gelöscht.|
|5046|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Ein Kryptografiesatz wurde hinzugefügt.|
|5047|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Ein Kryptografiesatz wurde geändert.|
|5048|Nicht zutreffend|Niedrig|Die IPSec-Einstellungen wurden geändert. Ein Kryptografiesatz wurde gelöscht.|
|5050|Nicht zutreffend|Niedrig|Es wurde versucht, die Windows-Firewall mithilfe eines INetFwProfile. firewallaktivierten Aufrufens (false) Programm gesteuert zu deaktivieren.|
|5051|Nicht zutreffend|Niedrig|Eine Datei wurde virtualisiert.|
|5056|Nicht zutreffend|Niedrig|Ein kryptografischer Self-Test wurde ausgeführt.|
|5057|Nicht zutreffend|Niedrig|Fehler bei einem einfachen kryptografischen Vorgang.|
|5058|Nicht zutreffend|Niedrig|Schlüsseldateivorgang.|
|5059|Nicht zutreffend|Niedrig|Schlüsselmigrationsvorgang.|
|5060|Nicht zutreffend|Niedrig|Fehler bei der Überprüfung der Kryptografiesignatur.|
|5061|Nicht zutreffend|Niedrig|Kryptografievorgang.|
|5062|Nicht zutreffend|Niedrig|Ein kryptografischer kernelmodustest wurde ausgeführt.|
|5063|Nicht zutreffend|Niedrig|Es wurde versucht, einen Kryptografieanbietervorgang auszuführen.|
|5064|Nicht zutreffend|Niedrig|Es wurde versucht, einen Kryptografiekontextvorgang auszuführen.|
|5065|Nicht zutreffend|Niedrig|Es wurde versucht, einen Kryptografiekontext zu ändern.|
|5066|Nicht zutreffend|Niedrig|Es wurde versucht, einen Kryptografiefunktionsvorgang auszuführen.|
|5067|Nicht zutreffend|Niedrig|Es wurde versucht, eine Kryptografiefunktion zu ändern.|
|5068|Nicht zutreffend|Niedrig|Es wurde versucht, einen Vorgang für einen Kryptografiefunktionsanbieter auszuführen.|
|5069|Nicht zutreffend|Niedrig|Es wurde versucht, einen Vorgang für eine Kryptografiefunktionseigenschaft auszuführen.|
|5070|Nicht zutreffend|Niedrig|Es wurde versucht, eine Kryptografiefunktionseigenschaft zu ändern.|
|5125|Nicht zutreffend|Niedrig|Eine Anforderung wurde an den OCSP-Responder-Dienst übermittelt.|
|5126|Nicht zutreffend|Niedrig|Das Signaturzertifikat wurde vom OCSP-Responder-Dienst automatisch aktualisiert.|
|5127|Nicht zutreffend|Niedrig|Der OCSP-Sperr Anbieter hat die Sperrinformationen erfolgreich aktualisiert.|
|5136|566|Niedrig|Ein Verzeichnisdienstobjekt wurde geändert|
|5137|566|Niedrig|Ein Verzeichnisdienstobjekt wurde erstellt.|
|5138|Nicht zutreffend|Niedrig|Ein Verzeichnisdienstobjekt wurde wiederhergestellt.|
|5139|Nicht zutreffend|Niedrig|Ein Verzeichnisdienstobjekt wurde verschoben.|
|5140|Nicht zutreffend|Niedrig|Es wurde auf ein Netzwerkfreigabeobjekt zugegriffen.|
|5141|Nicht zutreffend|Niedrig|Ein Verzeichnisdienstobjekt wurde gelöscht.|
|5152|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat ein Paket blockiert.|
|5153|Nicht zutreffend|Niedrig|Ein stärker einschränkender Windows-Filterplattformfilter hat ein Paket blockiert.|
|5154|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat es einer Anwendung oder einem Dienst gestattet, einen Port auf eingehende Verbindungen abzuhören.|
|5155|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat eine Anwendung oder einen Dienst daran gehindert, einen Port auf eingehende Verbindungen abzuhören.|
|5156|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat eine Verbindung zugelassen.|
|5157|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat eine Verbindung blockiert.|
|5158|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat eine Bindung an einen lokalen Port zugelassen.|
|5159|Nicht zutreffend|Niedrig|Die Windows-Filterplattform hat eine Bindung an einen lokalen Port blockiert.|
|5378|Nicht zutreffend|Niedrig|Die angeforderte Delegierung von Anmeldeinformationen wurde von einer Richtlinie nicht zugelassen.|
|5440|Nicht zutreffend|Niedrig|Beim Start des Basisfiltermoduls der Windows-Filterplattform war der folgende Callout vorhanden.|
|5441|Nicht zutreffend|Niedrig|Beim Start des Basisfiltermoduls der Windows-Filterplattform war der folgende Filter vorhanden.|
|5442|Nicht zutreffend|Niedrig|Beim Start des Basisfiltermoduls der Windows-Filterplattform war der folgende Anbieter vorhanden.|
|5443|Nicht zutreffend|Niedrig|Beim Start des Basisfiltermoduls der Windows-Filterplattform war der folgende Anbieterkontext vorhanden|
|5444|Nicht zutreffend|Niedrig|Die folgende untergeordnete Ebene war vorhanden, als die Basis Filter-Engine der Windows-Filter Plattform gestartet wurde.|
|5446|Nicht zutreffend|Niedrig|Ein Callout der Windows-Filterplattform wurde geändert.|
|5447|Nicht zutreffend|Niedrig|Ein Filter der Windows-Filterplattform wurde geändert.|
|5448|Nicht zutreffend|Niedrig|Ein Anbieter der Windows-Filterplattform wurde geändert.|
|5449|Nicht zutreffend|Niedrig|Ein Anbieterkontext der Windows-Filterplattform wurde geändert.|
|5450|Nicht zutreffend|Niedrig|Eine Windows-Filter Platt Form Unterschicht wurde geändert.|
|5451|Nicht zutreffend|Niedrig|Eine IPsec-Schnellmodus-Sicherheitszuordnung wurde eingerichtet.|
|5452|Nicht zutreffend|Niedrig|Eine IPsec-Schnellmodus-Sicherheitszuordnung wurde beendet.|
|5456|Nicht zutreffend|Niedrig|Das PAStore-Modul hat eine Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet.|
|5457|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte die Active Directory-Speicher-IPsec-Richtlinie nicht auf dem Computer anwenden.|
|5458|Nicht zutreffend|Niedrig|Das PAStore-Modul hat eine lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie auf dem Computer angewendet.|
|5.459|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte die lokal zwischengespeicherte Kopie der Active Directory-Speicher-IPsec-Richtlinie nicht auf dem Computer anwenden.|
|5460|Nicht zutreffend|Niedrig|Das PAStore-Modul hat eine Speicher-IPsec-Richtlinie der lokalen Registrierung auf dem Computer angewendet.|
|5461|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte die Speicher-IPsec-Richtlinie der lokalen Registrierung nicht auf dem Computer anwenden.|
|5462|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte einige Regeln der aktiven IPsec-Richtlinie nicht auf dem Computer anwenden. Verwenden Sie das Snap-In „IP-Sicherheitsmonitor“, um das Problem zu diagnostizieren.|
|5463|Nicht zutreffend|Niedrig|Das PAStore-Modul hat die aktive IPSec-Richtlinie auf Änderungen überprüft und keine Änderungen ermittelt.|
|5464|Nicht zutreffend|Niedrig|Das PAStore-Modul hat beim Abfragen von Änderungen für die aktive IPsec-Richtlinie Änderungen erkannt und diese auf die IPsec-Dienste angewendet.|
|5465|Nicht zutreffend|Niedrig|Das PAStore-Modul hat eine Steuerung, die das erneute Laden der IPSec-Richtlinie erzwingt, ermittelt, und hat die Steuerung erfolgreich verarbeitet.|
|5466|Nicht zutreffend|Niedrig|Das PAStore-Modul hat beim Abfragen von Änderungen für die Active Directory-IPsec-Richtlinie festgestellt, dass Active Directory nicht erreichbar ist. Stattdessen wird die zwischengespeicherte Kopie der Active Directory-IPsec-Richtlinie verwendet. Alle seit der letzten Abfrage an der Active Directory-IPsec-Richtlinie vorgenommenen Änderungen konnten nicht angewendet werden.|
|5467|Nicht zutreffend|Niedrig|Das PAStore-Modul hat beim Abfragen von Änderungen für die Active Directory-IPsec-Richtlinie festgestellt, dass Active Directory erreichbar ist und keine Änderungen der Richtlinie vorliegen. Die zwischengespeicherte Kopie der Active Directory-IPsec-Richtlinie wird nicht mehr verwendet.|
|5468|Nicht zutreffend|Niedrig|Das PAStore-Modul hat beim Abfragen von Änderungen für die Active Directory-IPsec-Richtlinie festgestellt, dass Active Directory erreichbar ist und Änderungen der Richtlinie vorliegen. Die gefundenen Änderungen wurden angewendet. Die zwischengespeicherte Kopie der Active Directory-IPsec-Richtlinie wird nicht mehr verwendet.|
|5471|Nicht zutreffend|Niedrig|Das PAStore-Modul hat die lokale Speicher-IPsec-Richtlinie auf dem Computer geladen.|
|5472|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte die lokale Speicher-IPsec-Richtlinie nicht auf dem Computer laden.|
|5473|Nicht zutreffend|Niedrig|Das PAStore-Modul hat die Verzeichnisspeicher-IPsec-Richtlinie auf dem Computer geladen.|
|5474|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte die Verzeichnisspeicher-IPsec-Richtlinie nicht auf dem Computer laden.|
|5477|Nicht zutreffend|Niedrig|Das PAStore-Modul konnte den Schnellmodusfilter nicht laden.|
|5479|Nicht zutreffend|Niedrig|Die IPsec-Dienste wurden erfolgreich beendet. Das Beenden der IPsec-Dienste kann das Risiko von Netzwerkangriffen auf den Computer und potenzielle Sicherheitsrisiken erhöhen.|
|5632|Nicht zutreffend|Niedrig|Die Authentifizierung bei einem Drahtlosnetzwerk wurde angefordert.|
|5633|Nicht zutreffend|Niedrig|Die Authentifizierung bei einem verkabelten Netzwerk wurde angefordert.|
|5712|Nicht zutreffend|Niedrig|Es wurde versucht, einen Remoteprozeduraufruf (RPC) auszuführen.|
|5888|Nicht zutreffend|Niedrig|Ein Objekt im COM+-Katalog wurde geändert.|
|5889|Nicht zutreffend|Niedrig|Ein Objekt wurde aus dem COM+-Katalog gelöscht.|
|5890|Nicht zutreffend|Niedrig|Dem COM+-Katalog wurde ein Objekt hinzugefügt.|
|6008|Nicht zutreffend|Niedrig|Das vorherige System wurde unerwartet heruntergefahren.|
|6.144|Nicht zutreffend|Niedrig|Die Sicherheitsrichtlinie in den Gruppenrichtlinie Objekten wurde erfolgreich angewendet.|
|6272|Nicht zutreffend|Niedrig|Der Netzwerkrichtlinienserver hat einem Benutzer den Zugriff gewährt.|
|Nicht zutreffend|561|Niedrig|Ein Handle zu einem Objekt wurde angefordert.|
|Nicht zutreffend|563|Niedrig|Objekt zum Löschen geöffnet|
|Nicht zutreffend|625|Niedrig|Benutzer Kontotyp geändert|
|Nicht zutreffend|613|Niedrig|IPSec-Richtlinien-Agent gestartet|
|Nicht zutreffend|614|Niedrig|IPSec-Richtlinien-Agent deaktiviert|
|Nicht zutreffend|615|Niedrig|IPSec-Richtlinien-Agent|
|Nicht zutreffend|616|Niedrig|Schwerwiegender Fehler bei IPSec-Richtlinien-Agent.|
|24577|Nicht zutreffend|Niedrig|Verschlüsselung des Volumes wurde gestartet.|
|24578|Nicht zutreffend|Niedrig|Die Verschlüsselung des Volumes wurde beendet.|
|24579|Nicht zutreffend|Niedrig|Verschlüsselung des Volumes abgeschlossen|
|24580|Nicht zutreffend|Niedrig|Die Entschlüsselung des Volumes wurde gestartet.|
|24581|Nicht zutreffend|Niedrig|Die Entschlüsselung des Volumes wurde beendet.|
|24582|Nicht zutreffend|Niedrig|Entschlüsselung des Volumes abgeschlossen|
|24583|Nicht zutreffend|Niedrig|Konvertierungsarbeitsthread für das Volume wurde gestartet.|
|24584|Nicht zutreffend|Niedrig|Der konvertierungsarbeitsthread für das Volume wurde vorübergehend beendet.|
|24588|Nicht zutreffend|Niedrig|Fehler beim Konvertierungs Vorgang auf Volume "%2". Überprüfen Sie die Daten auf diesem Volume.|
|24595|Nicht zutreffend|Niedrig|Volume "%2" enthält fehlerhafte Cluster. Diese Cluster werden während der Konvertierung übersprungen.|
|24621|Nicht zutreffend|Niedrig|Anfängliche Status Überprüfung: parallele volumekonvertierungstransaktion auf %2.|
|5049|Nicht zutreffend|Niedrig|Eine IPSec-Sicherheitszuordnung wurde gelöscht.|
|5478|Nicht zutreffend|Niedrig|Die IPSec-Dienste wurden erfolgreich gestartet.|

> [!NOTE]
> Eine Liste mit vielen Sicherheits Ereignis-IDs und deren Bedeutung finden Sie unter [Windows-Sicherheits Überwachungs Ereignisse](https://www.microsoft.com/download/details.aspx?id=50034) .
>
> Führen Sie **wevtutil GP Microsoft-Windows-Security-Auditing/GE/GM: true** aus, um eine sehr ausführliche Liste aller Sicherheits Ereignis-IDs abzurufen.

Weitere Informationen zu den Windows-Sicherheits Ereignis-IDs und deren Bedeutung finden Sie im Microsoft-Support Artikel [Beschreibung von Sicherheits Ereignissen in Windows 7 und Windows Server 2008 R2](https://support.microsoft.com/kb/977519). Sie können auch [Sicherheits Überwachungs Ereignisse für Windows 7-und Windows Server 2008 R2](https://www.microsoft.com/download/details.aspx?id=21561) -und Windows [8-und Windows Server 2012-Sicherheits Ereignis Details](https://www.microsoft.com/download/details.aspx?id=35753)herunterladen, die ausführliche Ereignis Informationen für die Betriebssysteme, auf die verwiesen wird, im Tabellenformat bereitstellen.
