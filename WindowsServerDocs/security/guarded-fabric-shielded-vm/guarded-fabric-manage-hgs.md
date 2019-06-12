---
title: Verwalten von Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: eecb002e-6ae5-4075-9a83-2bbcee2a891c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: dab27e71e42970507f321271edda90f6d161c691
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447393"
---
# <a name="managing-the-host-guardian-service"></a>Verwalten von Host-Überwachungsdienst

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die Host Guardian Service (HGS) ist das Kernstück der überwachten Fabric-Lösung.
Er ist verantwortlich für sicherstellen, dass die Hoster oder Enterprise Hyper-V-Hosts im Fabric bekannt sind und vertrauenswürdige Software ausführen und für die Verwaltung der Schlüssel für abgeschirmte virtuelle Computer zu starten.
Wenn ein Mandant entscheidet, die Sie zum Hosten ihrer abgeschirmte VMs als vertrauenswürdig einstufen, werden sie das Vertrauen in Ihre Konfiguration und Verwaltung von Host-Überwachungsdienst platzieren.
Aus diesem Grund ist es sehr wichtig, die empfohlenen Vorgehensweisen beim Host-Überwachungsdienst, um sicherzustellen, dass die Sicherheit, Verfügbarkeit und Zuverlässigkeit des geschützten Fabrics zu verwalten.
Die Anleitungen in den folgenden Abschnitten behandelt die am häufigsten auftretenden operative Probleme mit der Administratoren des Host-Überwachungsdienst.

## <a name="limiting-admin-access-to-hgs"></a>Beschränken Administratorzugriff auf den Host-Überwachungsdienst
Aufgrund der Sicherheit vertraulicher Art des Host-Überwachungsdienst ist es wichtig sicherzustellen, dass die Administratoren sehr vertrauenswürdige Mitglieder Ihrer Organisation sind und im Idealfall von den Administratoren der Ihr Fabric-Ressourcen getrennt.
Darüber hinaus empfiehlt es sich, dass Sie Host-Überwachungsdienst nur von sicheren Arbeitsstationen, die mithilfe von sicheren Kommunikationsprotokollen, z. B. WinRM über HTTPS verwalten.

### <a name="separation-of-duties"></a>Trennung von Aufgaben
Beim Einrichten von Host-Überwachungsdienst erhalten Sie die Option zum Erstellen isolierte Active Directory-Gesamtstruktur, nur für die Host-Überwachungsdienst oder Host-Überwachungsdienst mit einer vorhandenen, vertrauenswürdigen Domäne zu verknüpfen.
Diese Entscheidung sowie die Rollen, die Sie die Administratoren in Ihrer Organisation zuweisen, Bestimmen der Vertrauensgrenze für Host-Überwachungsdienst.
Personen Zugriff auf Host-Überwachungsdienst bietet hat, als ein Administrator direkt oder indirekt als Administrator eines anderen (z. B. Active Directory), die Host-Überwachungsdienst bietet beeinflussen können hat die Kontrolle über Ihre geschützten Fabrics.
Host-Überwachungsdienst-Administratoren auswählen, welche Hyper-V-Hosts abgeschirmte VMs ausführen und Verwalten der Zertifikate erforderlich, starten Sie abgeschirmte VMs autorisiert sind.
Ein Angreifer oder böswillige Admin, wer Zugriff auf den Host-Überwachungsdienst hat können dieser Leistung Sie autorisieren gefährdeten Hosts abgeschirmte VMs ausführen, einen Denial-of-Service-Angriff durch das Entfernen des Schlüsselmaterials und vieles mehr zu initiieren.

Um dieses Risiko zu vermeiden, ist es *stark* empfohlen, die Überlappung zwischen Ihrem Host-Überwachungsdienst (einschließlich der Domäne, die Host-Überwachungsdienst hinzugefügt wird) die Administratoren zu beschränken und Hyper-V-Umgebungen.
Indem Sie sicherstellen, dass keine ein Administrator den Zugriff auf beide Systeme verfügt, müsste ein Angreifer 2 verschiedene Konten von 2 Einzelpersonen seine Aufgabe zum Ändern der Richtlinien für die Host-Überwachungsdiensts ausführen zu kompromittieren.
Dies bedeutet auch, dass die Domäne und zu den Enterprise-Administratoren für die zwei Active Directory-Umgebungen sollten nicht dieselbe Person sein, noch sollte Host-Überwachungsdienst derselben Active Directory-Gesamtstruktur als Hyper-V-Hosts verwendet.
Jeder, der sich Zugriff auf Weitere Ressourcen gewähren kann, stellt ein Sicherheitsrisiko dar.

### <a name="using-just-enough-administration"></a>Verwenden von Just Enough Administration
Im Lieferumfang von Host-Überwachungsdienst [Just Enough Administration](https://aka.ms/JEAdocs) (JEA) Rollen, die erstellt werden, können Sie ihn noch sicherer zu verwalten.
JEA kann Sie bei, sodass Sie zum Delegieren von Verwaltungsaufgaben auf nicht-Administratorbenutzern, was bedeutet, dass Personen, die Host-Überwachungsdienst-Richtlinien verwalten Administratoren den ganzen Computer oder die Domäne nicht tatsächlich sein müssen.
JEA basiert, beschränken welche Befehle ein Benutzer in einer PowerShell-Sitzung ausführen kann und ein temporäres lokales Konto im Hintergrund (eindeutig für jede benutzersitzung) zum Ausführen der Befehle, die normalerweise die erhöhte Rechte erforderlich sind.

Im Lieferumfang von Host-Überwachungsdienst ist 2 JEA-Rollen, die vorkonfiguriert:
- **Host-Überwachungsdienst Administratoren** wodurch der Benutzer zum Verwalten von Richtlinien für alle Host-Überwachungsdienst, einschließlich Autorisieren des neuen Hosts zum Ausführen von abgeschirmten VMs.
- **Host-Überwachungsdienst Reviewer** der erlaubt nur Benutzern des rechts vor, die vorhandene Richtlinien zu überwachen. Sie können keine Änderungen an der Konfiguration des Host-Überwachungsdienst vornehmen.

Um JEA verwenden zu können, müssen Sie zunächst einen neuen Standardbenutzer erstellen, und ein Mitglied der HGS-Administratoren oder Host-Überwachungsdienst reviewergruppe machen.
Bei Verwendung `Install-HgsServer` zum Einrichten einer neuen Gesamtstruktur für Host-Überwachungsdienst, diese Gruppen erhält "*Servicename*Administratoren" und "*Servicename*Reviewer", in denen *Servicename*  ist der Netzwerkname des Host-Überwachungsdienst-Clusters.
Wenn Sie Host-Überwachungsdiensts zu einer vorhandenen Domäne beigetreten, lesen Sie den Gruppennamen, die Sie in angegeben `Initialize-HgsServer`.

**Erstellen von Standardbenutzern für die HGS-Administrator und Prüfer**

```powershell
$hgsServiceName = (Get-ClusterResource HgsClusterResource | Get-ClusterParameter DnsName).Value
$adminGroup = $hgsServiceName + "Administrators"
$reviewerGroup = $hgsServiceName + "Reviewers"

New-ADUser -Name 'hgsadmin01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Admin Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $adminGroup -Members 'hgsadmin01'

New-ADUser -Name 'hgsreviewer01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Reviewer Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $reviewerGroup -Members 'hgsreviewer01'
```

**Überwachen von Richtlinien mit der Prüferrolle**

Führen Sie auf einem Remotecomputer, der über eine Netzwerkverbindung zum Host-Überwachungsdienst verfügt die folgenden Befehle in PowerShell, um die JEA-Sitzung mit den Anmeldeinformationen des Reviewers eingeben.
Es ist wichtig zu beachten, dass seit der Reviewer-Konto nur ein Standardbenutzer ist, es für reguläre Windows PowerShell-Remoting remotedesktopzugriff auf den Host-Überwachungsdienst usw. verwendet werden kann.

```powershell
Enter-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsreviewer01' -ConfigurationName 'microsoft.windows.hgs'
```

Sie können dann prüfen, welche Befehle erlaubt sind, in der Sitzung mit `Get-Command` , und führen Sie alle zulässigen Befehle aus, um die Konfiguration überwachen.
In der folgenden Beispiel werden wir überprüfen, welche Richtlinien auf Host-Überwachungsdienst aktiviert sind.

```powershell
Get-Command

Get-HgsAttestationPolicy
```

Geben Sie den Befehl `Exit-PSSession` oder dessen Alias `exit`, wenn Sie fertig sind arbeiten mit der JEA-Sitzung. 

**Hinzufügen einer neuen Richtlinie zu-Host-Überwachungsdienst, der mit der Rolle "Administrator"**

Um eine Richtlinie tatsächlich ändern zu können, müssen Sie den JEA-Endpunkt mit einer Identität herstellen, für die der Gruppe "HgsAdministrators" angehört.
In der folgenden Beispiel können wir angezeigt werden, wie Sie eine neue codeintegritätsrichtlinie auf Host-Überwachungsdienst kopieren und registrieren Sie ihn mithilfe von JEA.
Die Syntax möglicherweise unterscheiden, was Ihnen bereits vertraut ist.
Dadurch werden einige der Einschränkungen in JEA zu berücksichtigen, z. B., wenn kein Zugriff auf das gesamte Dateisystem.

```powershell
$cipolicy = Get-Item "C:\temp\cipolicy.p7b"
$session = New-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsadmin01' -ConfigurationName 'microsoft.windows.hgs'
Copy-Item -Path $cipolicy -Destination 'User:' -ToSession $session

# Now that the file is copied, we enter the interactive session to register it with HGS
Enter-PSSession -Session $session
Add-HgsAttestationCiPolicy -Name 'New CI Policy via JEA' -Path 'User:\cipolicy.p7b'

# Confirm it was added successfully
Get-HgsAttestationPolicy -PolicyType CiPolicy

# Finally, remove the PSSession since it is no longer needed
Exit-PSSession
Remove-PSSession -Session $session
```

## <a name="monitoring-hgs"></a>Überwachen von Host-Überwachungsdienst
### <a name="event-sources-and-forwarding"></a>Ereignisquellen und Weiterleitung
Ereignisse von Host-Überwachungsdienst werden im Windows-Ereignisprotokoll unter 2 Quellen angezeigt:
- **HostGuardianService-Attestation**
- **HostGuardianService-KeyProtection**

Sie können diese Ereignisse anzeigen, Öffnen der Ereignisanzeige und navigieren Sie zum Microsoft-Windows-HostGuardianService-Nachweis und Microsoft-Windows-HostGuardianService-KeyProtection.

In einer großen Umgebung ist es oft besser, Weiterleiten von Ereignissen an einen zentralen Windows-Ereignissammlung um die Analyse von Ereignissen zu vereinfachen.
Weitere Informationen finden Sie in der [Dokumentation zu Windows-Ereignisweiterleitung](https://msdn.microsoft.com/library/windows/desktop/bb427443.aspx).

### <a name="using-system-center-operations-manager"></a>Verwenden von System Center Operationsmanager
Sie können auch System Center 2016 – Operations Manager zum Überwachen von Host-Überwachungsdienst und Ihrer überwachten Hosts verwenden.
Das geschütztes Fabric-Management Pack verfügt über ereignisüberwachung für häufige Konfigurationsfehler zu überprüfen, die zu Ausfallzeiten des Datencenters, einschließlich Hosts, die nicht bestanden, Nachweis und Erstellen von Fehlerberichten HGS-Servern führen können.

Zu den ersten Schritten [installieren und Konfigurieren von SCOM-2016](https://technet.microsoft.com/system-center-docs/om/welcome-to-operations-manager) und [das geschütztes Fabric-Management Pack herunterladen](https://www.microsoft.com/download/details.aspx?id=52764).
Enthaltenen Management Pack-Handbuch erläutert das Konfigurieren des Management Packs und den Arbeitsumfang der Monitore zu verstehen.

## <a name="backing-up-and-restoring-hgs"></a>Sichern und Wiederherstellen von Host-Überwachungsdienst
### <a name="disaster-recovery-planning"></a>Planung der notfallwiederherstellung
Wenn Ihre Pläne zur notfallwiederherstellung entwerfen können, ist es wichtig, die individuellen Anforderungen der Host-Überwachungsdienst in Ihr geschütztes Fabric zu berücksichtigen.
Einige oder alle Ihrer Host-Überwachungsdienst-Knoten sollten Sie verlieren, möglicherweise Probleme bei der sofortigen Verfügbarkeit treten, die Benutzer geschützten virtuelle Maschinen starten verhindern.
In einem Szenario, in dem Sie Ihre gesamten Host-Überwachungsdienst Cluster verlieren, müssen Sie vollständige Sicherungen der HGS-Konfiguration auf Seite zum Wiederherstellen Ihres Clusters Host-Überwachungsdienst und normal fortgesetzt.
Dieser Abschnitt enthält die erforderlichen Schritte zum Vorbereiten für ein solches Szenario.

Zunächst ist es wichtig zu verstehen, was für die Host-Überwachungsdienst zu sichernden wichtig ist.
Host-Überwachungsdienst behält mehrere Arten von Informationen, die helfen zu bestimmen, welche Hosts zum Ausführen geschützter VMs autorisiert sind.
Dazu zählen:
1. Active Directory-Sicherheits-IDs für die Gruppen, die mit vertrauenswürdigen Hosts (bei Verwendung von Active Directory-Nachweis);
2. Eindeutige TPM Bezeichner für jeden Host in Ihrer Umgebung
3. TPM-Richtlinien für jede eindeutige Konfiguration des Hosts; und
4. Anwendungssteuerungscode-Integritätsrichtlinien, die bestimmen, welche Software auf den Hosts ausgeführt werden darf.

Diese Artefakte Nachweis koordiniert werden müssen mit dem Administratoren Ihre hosting Fabric abgerufen werden, möglicherweise darum nur schwer zum Abrufen dieser Informationen nach einem Notfall erneut.

Host-Überwachungsdienst erfordert darüber hinaus den Zugriff auf mindestens 2-Zertifikate, die zum Verschlüsseln und Signieren die erforderlichen Informationen zum Starten einer abgeschirmten VMs (die Schlüsselschutzvorrichtung).
Diese Zertifikate sind bekannte (verwendet von den Besitzern der abgeschirmten VMs zum Autorisieren von Fabrics für die Ausführung ihrer VMs) und nach einem Notfall für eine Umgebung für eine nahtlose Wiederherstellung wiederhergestellt werden müssen.
Host-Überwachungsdienst nicht die gleichen Zertifikate nach einem Notfall wiederhergestellt werden sollen, müssen jeden virtuellen Computer aktualisiert werden, um Ihre neue Schlüssel zum Entschlüsseln der ihre Informationen zu autorisieren.
Aus Gründen der Sicherheit kann nur der Besitzer des virtuellen Computers aktualisieren die VM-Konfiguration zum Autorisieren von diesen neuen Schlüssel, die Bedeutung-Fehler Ihre Schlüssel wiederherstellen nach ein Notfall jede VM-Besitzer müssen Maßnahmen ergreifen führt, um ihre virtuellen Computer wieder zu erhalten.

#### <a name="preparing-for-the-worst"></a>Vorbereiten für den schlimmsten Fall
Zur Vorbereitung der vollständigen Verlust der Host-Überwachungsdienst sind 2 Schritte, die Sie ausführen müssen:
1. Sichern Sie die Host-Überwachungsdienst-Nachweis-Richtlinien
2. Sichern Sie die Host-Überwachungsdienst-Schlüssel

Anleitungen dazu, wie beide Schritte ausführen finden Sie unter den [Sichern von Host-Überwachungsdienst](#backing-up-hgs) Abschnitt.

Es wird außerdem empfohlen, jedoch nicht erforderlich, dass Sie die Liste der Benutzer autorisiert zum Verwalten von Host-Überwachungsdienst in der Active Directory-Domäne oder Active Directory sichern.

Sicherungen sollten regelmäßig erstellt werden, um sicherzustellen, dass die Informationen auf dem neuesten Stand und sicher an der Manipulation und Diebstahl vermeiden gespeichert sind.

Es ist **nicht empfohlen,** zu sichern, oder versuchen, ein Image Gesamtsystem eine Host-Überwachungsdienst-Knoten wiederherzustellen.
Falls Sie Ihren gesamten Cluster verloren haben, werden die bewährte Methode richten Sie eine neue Host-Überwachungsdienst-Knoten und nur-Host-Überwachungsdienst Zustand wiederherstellen, nicht den gesamten Server Betriebssystem.

#### <a name="recovering-from-the-loss-of-one-node"></a>Wiederherstellung nach dem Verlust eines Knotens
Wenn Sie einen oder mehrere Knoten (aber nicht jeder Knoten) in Ihrem Cluster für die Host-Überwachungsdienst verlieren, können Sie einfach [Hinzufügen von Knoten zum Cluster](guarded-fabric-configure-additional-hgs-nodes.md) anhand der Anweisungen im Bereitstellungshandbuch.
Die Nachweis-Richtlinien werden automatisch synchronisiert werden, wie sämtliche Zertifikate die Host-Überwachungsdienst als PFX-Dateien zur Verfügung gestellt wurden werden mit zugehörigen Kennwörter.
Für Zertifikate, die über einen Fingerabdruck des Host-Überwachungsdienst hinzugefügt (nicht exportierbare und hardwaregestützten Zertifikate häufig), Sie müssen sicherstellen, jeden neuer Knoten hat Zugriff auf den privaten Schlüssel für jedes Zertifikat.

#### <a name="recovering-from-the-loss-of-the-entire-cluster"></a>Wiederherstellung nach dem Verlust des gesamten Clusters
Wenn der gesamte Cluster für die Host-Überwachungsdienst ausfällt und Sie nicht wieder online zu schalten, müssen Sie den Host-Überwachungsdienst aus einer Sicherung wiederherstellen.
Umfasst die ersten Einrichten eines neuen Clusters von Host-Überwachungsdienst pro Host-Überwachungsdienst aus einer Sicherung wiederherstellen der [Anweisungen im Bereitstellungshandbuch](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).
Es wird dringend empfohlen, aber nicht erforderlich, um dem gleichen Clusternamen verwenden, wenn die Host-Überwachungsdienst-wiederherstellungsumgebung einrichten zur Unterstützung bei der namensauflösung von Hosts.
Mit dem gleichen Namen vermeidet Hosts mit neuen Nachweis- und Schlüsselschutz-URLs zu konfigurieren.
Wenn Sie mit der Active Directory-Domäne Sichern von Host-Überwachungsdienst Objekte wiederhergestellt haben, empfiehlt es sich, zu, die Objekte entfernen, die Host-Überwachungsdienst-Cluster, Computer, Dienstkonto und JEA-Gruppen vor der Initialisierung des HGS-Servers darstellen.

Nachdem Sie Ihre erste HGS-Knoten eingerichtet haben (z. B. es installiert und initialisiert wurde), gehen Sie die Schritte unter [Wiederherstellen von Host-Überwachungsdienst aus einer Sicherung](#restoring-hgs-from-a-backup) Nachweis Richtlinien und öffentliche Hälften der Schutz für den Schlüssel wiederherstellen Zertifikate.
Sie benötigen zum Wiederherstellen der private Schlüssel für Ihre Zertifikate manuell gemäß den Anweisungen Ihres Anbieters Zertifikat (z. B. importieren Sie das Zertifikat in Windows, oder Konfigurieren des Zugriffs auf das HSM-gesicherten Zertifikate).
Nach der erste Knoten haben eingerichtet, können Sie weiterhin [zusätzliche Knoten im Cluster installieren](guarded-fabric-configure-additional-hgs-nodes.md) , bis Sie die Kapazität und die gewünschte resilienz erreicht haben.

### <a name="backing-up-hgs"></a>Sichern von Host-Überwachungsdienst
Der HGS-Administrator soll für das Sichern von Host-Überwachungsdienst in regelmäßigen Abständen zuständig sein.
Eine vollständige Sicherung enthält vertrauliche Daten, die entsprechend gesichert werden müssen.
Eine nicht vertrauenswürdige Entität den Zugriff auf diese Schlüssel erlangen sollte, können sie, dass Material, das Einrichten einer böswilligen Host-Überwachungsdienst-Umgebung für die Beeinträchtigung von VMs abgeschirmten verwenden.

**Sichern die Richtlinien Nachweis** wieder um die Richtlinien für den Host-Überwachungsdienst-Nachweis, den folgenden Befehl auf einem beliebigen arbeiten HGS-Server-Knoten ausgeführt.
Sie werden aufgefordert, ein Kennwort anzugeben.
Dieses Kennwort wird verwendet, um alle Zertifikate, die mit einer PFX-Datei (anstatt den Fingerabdruck eines Zertifikats) Host-Überwachungsdienst hinzugefügt zu verschlüsseln.

```powershell
Export-HgsServerState -Path C:\temp\HGSBackup.xml
```

> [!NOTE]
> Wenn Sie Admin-vertrauenswürdiger Nachweis verwenden, müssen Sie die Mitgliedschaft in den Sicherheitsgruppen, die Host-Überwachungsdiensts für überwachte Hosts zu autorisieren separat sichern.
> Host-Überwachungsdienst wird die SID der Sicherheitsgruppen, nicht die Mitgliedschaft in ihnen nur sichern.
> Den Fall, dass diese Gruppen während eines Notfalls verloren gegangen sind, müssen Sie die Gruppen neu zu erstellen, und fügen Sie jeden überwachten Host auf diese erneut hinzu.

**Sichern von Zertifikaten**

Die `Export-HgsServerState` Befehl sichert alle PFX-Zertifikate Host-Überwachungsdienst hinzugefügt, die zum Zeitpunkt der Befehl ausgeführt wird.
Wenn Sie Host-Überwachungsdienst Zertifikate hinzugefügt müssen mit einem Fingerabdruck (typisch für nicht exportierbare und hardwaregestützten Zertifikate), Sie die privaten Schlüssel für die Zertifikate manuell zu sichern.
Um zu ermitteln, welche Zertifikate bei HGS registriert werden und müssen manuell gesichert werden, führen Sie den folgenden PowerShell-Befehl auf einem beliebigen arbeiten HGS-Server-Knoten.

```powershell
Get-HgsKeyProtectionCertificate | Where-Object { $_.CertificateData.GetType().Name -eq 'CertificateReference' } | Format-Table Thumbprint, @{ Label = 'Subject'; Expression = { $_.CertificateData.Certificate.Subject } }
```

Für jede der aufgeführten Zertifikate müssen Sie den privaten Schlüssel manuell sichern.
Wenn Sie Software-basiertes Zertifikat, die nicht exportiert wird verwenden, sollten Sie Ihrer Zertifizierungsstelle, um sicherzustellen, dass sie über eine Sicherung des Zertifikats verfügen, bzw. können sie bei Bedarf neu ausstellen wenden.
Für Zertifikate, die Erstellung und Speicherung in Hardwaresicherheitsmodulen sollten Sie die Dokumentation für Ihr Gerät Anleitungen zur Planung der notfallwiederherstellung sprechen.

Sie sollten die Zertifikat-Sicherungen zusammen mit Ihrer Nachweis Richtlinie Sicherungen an einem sicheren Ort speichern, sodass beide zusammen wiederhergestellt werden können.

**Zusätzliche Konfiguration zum Sichern**

Die gesicherte HGS-Serverstatus umfasst nicht den Namen Ihres Clusters HGS-Informationen aus Active Directory oder SSL-Zertifikate zum Sichern der Kommunikation mit HGS-APIs verwendet.
Diese Einstellungen sind wichtig für Konsistenz jedoch nicht kritisch ist, um nach einem Notfall Ihren HGS-Cluster wieder online zu erhalten.

Führen Sie zum Erfassen der Namen des Host-Überwachungsdienst-Diensts `Get-HgsServer` und notieren Sie den flachen Namen in den Nachweis- und Schlüsselschutz-URLs für Schlüssel.
Wenn die Nachweis-URL ist beispielsweise "<http://hgs.contoso.com/Attestation>", "Host-Überwachungsdienst" ist der Host-Überwachungsdienst-Dienstname.

Active Directory-Domäne ein, die Host-Überwachungsdienst muss wie alle anderen Active Directory-Domäne verwaltet werden.
Wenn Sie Host-Überwachungsdienst nach einem Notfall wiederherstellen zu können, müssen nicht unbedingt Sie der exakt die Objekte neu erstellen, die in der aktuellen Domäne vorhanden sind.
Allerdings wird es leichter Wiederherstellung, wenn Sie Active Directory sichern, und halten eine Liste mit den JEA-Benutzern, berechtigt, das System als auch die Mitgliedschaft der keiner Sicherheitsgruppe an, die Admin-vertrauenswürdiger Nachweis für das Autorisieren von überwachten Hosts zu verwalten.

Um den Fingerabdruck des SSL-Zertifikats konfiguriert, die für die Host-Überwachungsdiensts zu ermitteln, führen Sie den folgenden Befehl in PowerShell aus.
Sie können die SSL-Zertifikate entsprechend den Anweisungen des Anbieters für Ihr Zertifikat sichern.

```powershell
Get-WebBinding -Protocol https | Select-Object certificateHash
```

### <a name="restoring-hgs-from-a-backup"></a>Host-Überwachungsdienst aus einer Sicherung wiederherstellen
Die folgenden Schritte beschreiben, wie Sie HGS-Einstellungen aus einer Sicherung wiederherstellen.
Die Schritte sind für beide Situationen, in dem Sie versuchen, Änderungen, die für Ihre bereits ausgeführten Host-Überwachungsdienst-Instanzen, und wenn Sie einen neuen Host-Überwachungsdienst-Cluster nach einem vollständigen Verlust von der vorherigen App ständigen sind rückgängig zu machen.

#### <a name="set-up-a-replacement-hgs-cluster"></a>Einrichten eines Ersatz-Host-Überwachungsdienst-Clusters
Bevor Sie die Host-Überwachungsdienst wiederherstellen können, benötigen Sie einen initialisierten HGS-Cluster, den Sie die Konfiguration wiederherstellen können.
Wenn Sie einfach Einstellungen, die versehentlich gelöscht wurden zu einem vorhandenen (wird ausgeführt)-Cluster importieren, können Sie diesen Schritt überspringen.
Wenn Sie von einem vollständigen Verlust der Host-Überwachungsdienst wiederherstellen, müssen Sie Sie installieren und Initialisieren mindestens einen Host-Überwachungsdienst Knoten hinter dem [Anweisungen im Bereitstellungshandbuch](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).

Insbesondere müssen Sie:
1. [Richten Sie die Domäne für die Host-Überwachungsdienst](guarded-fabric-choose-where-to-install-hgs.md) oder Host-Überwachungsdienst mit einer vorhandenen Domäne verknüpfen
2. [Initialisieren Sie den Server-Host-Überwachungsdienst](guarded-fabric-initialize-hgs.md) mithilfe Ihrer vorhandenen Schlüssel *oder* einen Satz von temporären Schlüsseln. Sie können [entfernen Sie die temporäre Schlüssel](#renewing-or-replacing-keys) Sicherungsdateien nach dem Importieren von Ihrer tatsächlichen Schlüssel aus der Host-Überwachungsdienst.
3. [HGS-Einstellungen importieren](#import-settings-from-a-backup) aus der Sicherung zum Wiederherstellen der vertrauenswürdigen Hostgruppen, anwendungssteuerungscode-Integritätsrichtlinien, TPM-Baselines und TPM-Bezeichner

> [!TIP]
> Der neue Host-Überwachungsdienst-Cluster muss nicht die gleichen Zertifikate, Dienstname oder Domäne wie die Host-Überwachungsdienst-Instanz verwenden, aus denen Ihre Sicherungsdatei exportiert wurde.

#### <a name="import-settings-from-a-backup"></a>Importieren von Einstellungen aus einer Sicherung

Richtlinien, PFX-Zertifikate und die öffentlichen Schlüssel der nicht-PFX-Zertifikate auf Ihrem Host-Überwachungsdienst-Knoten aus einer Sicherungsdatei, und führen den folgenden Befehl zum Nachweis wiederherstellen auf einem Knoten der initialisierten HGS-Server.
Sie werden aufgefordert, das Kennwort einzugeben, die, das Sie beim Erstellen der sicherungs angegeben.

```powershell
Import-HgsServerState -Path C:\Temp\HGSBackup.xml
```

Wenn Sie nur die Admin-vertrauenswürdiger Nachweis oder TPM-vertrauenswürdiger Nachweis Richtlinien importieren möchten, erreichen Sie dies durch Angabe der `-ImportActiveDirectoryModeState` oder `-ImportTpmModeState` flags [Import-HgsServerState](https://technet.microsoft.com/library/mt652168.aspx).

Stellen Sie das neueste kumulative Update für Windows Server 2016, vor der Ausführung installiert ist sicher `Import-HgsServerState`.
Bei unterlassen kann ein Importfehler führen.

> [!NOTE]
> Wenn Sie Richtlinien auf einem vorhandenen Host-Überwachungsdienst-Knoten wiederherstellen, die bereits eine oder mehrere der diese Richtlinien, die installiert wird, wird der Importbefehl ein Fehler für jede duplizierungsrichtlinie angezeigt.
> Dies ist ein erwartetes Verhalten und kann ignoriert werden in den meisten Fällen.

#### <a name="reinstall-private-keys-for-certificates"></a>Installieren von privaten Schlüsseln für Zertifikate
Wenn eines der Zertifikate, die auf der Host-Überwachungsdienst, der aus dem die Sicherung erstellt wurde, verwendet die Fingerabdrücke mit hinzugefügt wurden, wird nur der öffentliche Schlüssel dieser Zertifikate in der Sicherungsdatei enthalten sein.
Dies bedeutet, dass Sie benötigen, manuell zu installieren bzw. zu gewähren Zugriff auf die privaten Schlüssel für jede dieser Zertifikate, bevor Anforderungen von Hyper-V-Hosts von Host-Überwachungsdienst verarbeitet werden können.
Die erforderlichen Aktionen zum Abschluss dieses Schritts wird, hängt davon ab, wie das Zertifikat ursprünglich ausgestellt wurde.
Für Software-Zertifikate von einer Zertifizierungsstelle ausgestellt, Sie benötigen, wenden Sie sich an die Zertifizierungsstelle aus, um den privaten Schlüssel zu ermitteln und installieren Sie es auf **jedes** HGS-Knoten gemäß ihren Anweisungen.
Falls Ihre Zertifikate hardwaregestützten sind, müssen Sie analog dazu finden Sie in der Hardware Security Module Dokumentation des Herstellers zum Installieren der erforderlichen Treiber auf jedem Host-Überwachungsdienst-Knoten das HSM herstellen, und jeder Computerzugriff auf den privaten Schlüssel zu gewähren.

Zur Erinnerung: müssen die Zertifikate, die Host-Überwachungsdienst mit Fingerabdrücke hinzugefügt manuelle Replikation der private Schlüssel für jeden Knoten.
Sie müssen diesen Schritt für jeden zusätzlichen Knoten zu wiederholen, die Sie den wiederhergestellten HGS-Cluster hinzufügen.

#### <a name="review-imported-attestation-policies"></a>Überprüfen Sie importierte Attestation-Richtlinien
Nachdem Sie Ihre Einstellungen aus einer Sicherung importiert haben, es wird empfohlen, genau die importierten Richtlinien mithilfe von überprüfen alle `Get-HgsAttestationPolicy` um sicherzustellen, dass nur die Hosts, die Ihnen als vertrauenswürdig eingestufter abgeschirmte VMs ausführen kann erfolgreich bestätigen.
Wenn Sie alle Richtlinien gefunden haben, die mit Ihren Sicherheitsstatus nicht mehr übereinstimmen, können Sie [deaktivieren oder entfernen sie](#review-attestation-policies).

#### <a name="run-diagnostics-to-check-system-state"></a>Führen Sie Diagnosen zum Überprüfen des Systemstatus
Wenn Sie das Einrichten und das Wiederherstellen des Zustands Ihrer Host-Überwachungsdienst-Knotens abgeschlossen haben, sollten Sie die Host-Überwachungsdienst-Diagnosetool zum Überprüfen des Zustands des Systems ausführen.
Zu diesem Zweck führen Sie den folgenden Befehl auf dem Host-Überwachungsdienst-Knoten, in dem Sie die Konfiguration wiederhergestellt:

```powershell
Get-HgsTrace -RunDiagnostics
```

Wenn das Ergebnis"insgesamt" ist nicht "erfolgreich", sind zusätzliche Schritte erforderlich, um die Konfiguration des Systems abzuschließen.
Überprüfen Sie die Meldungen in die Subtest(s), die nicht für Weitere Informationen.

## <a name="patching-hgs"></a>Patchen von Host-Überwachungsdienst
Es ist wichtig, die Host-Überwachungsdienst-Knoten, auf dem neuesten Stand halten, indem Sie das neueste kumulative Update zu installieren, wenn es darum geht. Wenn Sie einen neuen Host-Überwachungsdienst-Knoten festlegen, wird dringend empfohlen, bevor Sie die Host-Überwachungsdienst-Rolle installieren oder Konfigurieren von allen verfügbaren Updates zu installieren.
Dies sorgt eine neue oder geänderte Funktionalität wird sofort wirksam.

Wenn Ihr geschützte Fabric zu patchen, es wird dringend empfohlen, dass Sie zunächst ein upgrade *alle* Hyper-V-Hosts **vor dem Upgrade von Host-Überwachungsdienst**.
Dadurch wird sichergestellt, dass alle an den Nachweis-Richtlinien auf Host-Überwachungsdienst Änderungen *nach* Hyper-V-Hosts wurden aktualisiert, um die für sie erforderlichen Informationen bereitstellen.
Wenn ein Update zum Ändern des Verhaltens von Richtlinien geht, werden sie nicht automatisch aktiviert werden, zu vermeiden, dass Ihr Fabric.
Solche Updates erfordern, dass Sie die Anweisungen in den folgenden Abschnitt aktivieren Sie die neue oder geänderte Nachweis Richtlinien befolgen.
Wir empfehlen Ihnen, lesen die Anmerkungen zu dieser Version für Windows Server und sämtliche kumulativen Updates, die Sie installieren, um festzustellen, ob die Richtlinie für Updates erforderlich sind.

### <a name="updates-requiring-policy-activation"></a>Updates, die eine Richtlinie Aktivierung erfordern
Wenn ein Update für die Host-Überwachungsdienst führt oder merklich das Verhalten einer Richtlinie Nachweis ändert, ist ein zusätzlicher Schritt erforderlich, um die geänderte Richtlinie zu aktivieren.
Richtlinienänderungen werden nur durchgeführt, nach dem Exportieren und importieren den Host-Überwachungsdienst-Zustand.
Sie sollten nur die neuen oder geänderten Richtlinien aktivieren, nachdem Sie das kumulative Update für alle Hosts und alle HGS-Knoten in Ihrer Umgebung angewendet haben.
Nachdem alle Computer aktualisiert wurde, führen Sie die folgenden Befehle auf einem Host-Überwachungsdienst-Knoten zum Auslösen des Upgradevorgangs ein:

```powershell
$password = Read-Host -AsSecureString -Prompt "Enter a temporary password"
Export-HgsServerState -Path .\temporaryExport.xml -Password $password
Import-HgsServerState -Path .\temporaryExport.xml -Password $password
```

Wenn eine neue Richtlinie eingeführt wurde, wird es standardmäßig deaktiviert.
Um die neue Richtlinie zu aktivieren, finden Sie ihn zuerst in der Liste der Microsoft-Richtlinien (mit dem Präfix "HGS_"), und aktivieren Sie sie mit den folgenden Befehlen:

```powershell
Get-HgsAttestationPolicy

Enable-HgsAttestationPolicy -Name <Hgs_NewPolicyName>
```

## <a name="managing-attestation-policies"></a>Verwalten von Attestation-Richtlinien
Host-Überwachungsdienst verwaltet mehrere Attestation-Richtlinien, die den minimalen Satz von Anforderungen zu definieren, die ein Host erfüllen muss, um als "fehlerfrei" erachtet und abgeschirmte VMs ausgeführt werden.
Einige dieser Richtlinien von Microsoft definiert sind, werden andere von Ihnen definieren Sie die zulässige anwendungssteuerungscode-Integritätsrichtlinien, TPM-Baselines und Hosts in Ihrer Umgebung hinzugefügt.
Regelmäßige Wartung dieser Richtlinien ist erforderlich, um sicherzustellen, dass die Hosts bestätigen ordnungsgemäß fortfahren können, zu aktualisieren und zu ersetzen, und um sicherzustellen, dass alle nicht vertrauenswürdigen Hosts oder -Konfigurationen werden blockiert erfolgreich bestätigen.

Für Admin-vertrauenswürdigem Nachweis ist nur eine Richtlinie, das bestimmt, ob ein Host fehlerfrei ist: Mitgliedschaft in einer bekannten, vertrauenswürdigen Sicherheitsgruppe.
TPM-Nachweis ist komplizierter, und umfasst verschiedene Richtlinien zum Messen der den Code und Konfiguration eines Systems, bevor Sie bestimmen, ob sie fehlerfrei ist.

Eine einzelne Host-Überwachungsdienst kann gleichzeitig mit Active Directory und TPM-Richtlinien konfiguriert werden, aber der Dienst überprüft nur die Richtlinien für den aktuellen Modus, die sie für konfiguriert ist, wenn ein Host bestätigen versucht.
Führen Sie zum Überprüfen Ihrer Host-Überwachungsdienst-Servermodus `Get-HgsServer`.

### <a name="default-policies"></a>Standardrichtlinien
Für TPM-vertrauenswürdiger Nachweis es gibt mehrere integrierte Richtlinien, die auf dem Host-Überwachungsdienst konfiguriert.
Einige dieser Richtlinien sind "gesperrt" bedeutet, dass sie aus Sicherheitsgründen nicht deaktiviert werden können –.
In der folgenden Tabelle erläutert den Zweck der einzelnen Standardrichtlinie.

Richtlinienname                    | Zweck
-------------------------------|-----------------------------------------------------
Hgs_SecureBootEnabled          | Erfordert die Hosts in der sichere Start aktiviert. Dies ist erforderlich, die Start-Binärdateien und andere UEFI-locked-Einstellungen zu messen.
Hgs_UefiDebugDisabled          | Stellt sicher, dass die Hosts keinen Kerneldebugger aktiviert haben. Benutzermodus-Debugger werden mit anwendungssteuerungscode-Integritätsrichtlinien blockiert.
Hgs_SecureBootSettings         | Negative Richtlinie, um sicherzustellen, dass die Hosts über mindestens eine TPM-Baseline (vom Administrator definiert) übereinstimmen.
Hgs_CiPolicy                   | Negative Richtlinie, um sicherzustellen, dass die Hosts, die eine der vom Administrator definierte CI-Richtlinien verwendet werden.
Hgs_HypervisorEnforcedCiPolicy | Erfordert die codeintegritätsrichtlinie vom Hypervisor erzwungen werden. Bei Deaktivierung dieser Richtlinie Verringerung Ihrer Schutzmaßnahmen gegen Angriffe von Kernelmodus-Code Integrity Richtlinie.
Hgs_FullBoot                   | Stellt sicher, dass der Host nicht aus dem Energiesparmodus oder Ruhezustand fortgesetzt. Hosts müssen ordnungsgemäß neu gestartet oder heruntergefahren, die diese Richtlinie übergeben werden.
Hgs_VsmIdkPresent              | Erfordert die virtualisierungssicherheit, die basierend auf dem Host ausgeführt werden. Die IDK stellt dar, den Schlüssel zum Verschlüsseln der Informationen, die an sicheren Speicherbereich des Hosts gesendet werden.
Hgs_PageFileEncryptionEnabled  | Erfordert die Auslagerungsdateien auf dem Host verschlüsselt werden. Bei Deaktivierung dieser Richtlinie konnte in Offenlegung von Informationen führen, wenn eine unverschlüsselte Auslagerungsdatei für Mandanten geheime Schlüssel überprüft wird.
Hgs_BitLockerEnabled           | Erfordert BitLocker auf dem Hyper-V-Host aktiviert sein. Diese Richtlinie ist standardmäßig deaktiviert, zur Verbesserung der Leistung und wird nicht empfohlen, die aktiviert werden. Diese Richtlinie hat keinen Einfluss auf die Verschlüsselung von die abgeschirmten VMs selbst.
Hgs_IommuEnabled               | Erfordert, dass der Host ein IOMMU-Gerät verwendet, um direct Memory Access Angriffe zu verhindern. Bei Deaktivierung dieser Richtlinie, und Verwenden von Hosts ohne eine IOMMU aktiviert, können Mandanten vertrauliche Informationen zur Weiterleitung einer Speicher-Angriffe verfügbar machen.
Hgs_NoHibernation              | Erfordert den Ruhezustand auf dem Hyper-V-Host deaktiviert werden soll. Bei Deaktivierung dieser Richtlinie können Hosts abgeschirmte VM-Speicher in einer unverschlüsselten Ruhezustanddatei zu speichern.
Hgs_NoDumps                    | Erfordert, dass Arbeitsspeicher Abbilder auf dem Hyper-V-Host deaktiviert werden soll. Wenn Sie diese Richtlinie deaktivieren, empfiehlt es sich, dass Sie die speicherabbildverschlüsselung, um zu verhindern, dass die abgeschirmte VM-Speicher gespeichert wird, um unverschlüsselte Absturzabbilddateien konfigurieren.
Hgs_DumpEncryption             | Speicherabbilder, erfordert, wenn auf dem Hyper-V-Host aktiviert werden soll, eine Verschlüsselung mit einem Verschlüsselungsschlüssel, die vom Host-Überwachungsdienst als vertrauenswürdig eingestuft. Diese Richtlinie gilt nicht, wenn Absturzabbilder auf dem Host nicht aktiviert sind. Wenn diese Richtlinie und *Host-Überwachungsdienst\_NoDumps* beide deaktiviert ist, werden geschützte VM-Speicher konnte in einer unverschlüsselten Dumpdatei gespeichert werden.
Hgs_DumpEncryptionKey          | Negative Richtlinie um sicherzustellen, dass Hosts, die so konfiguriert, dass der Speicher, dass Speicherabbilder einen Dump vom Administrator definierte Datei bekannten, dass der Host-Überwachungsdienst Verschlüsselungsschlüssel verwenden. Diese Richtlinie gilt nicht beim *Host-Überwachungsdienst\_DumpEncryption* ist deaktiviert.

### <a name="authorizing-new-guarded-hosts"></a>Autorisieren von neuen überwachten hosts
Autorisieren Sie einen neuen Host zu einem bewachten Host (z. B. bestätigen erfolgreich), Host-Überwachungsdienst muss den Host als vertrauenswürdig einstufen und (Wenn für die Verwendung von TPM-vertrauenswürdiger Nachweis konfiguriert) die Software ausgeführt wird.
Die Schritte zum Autorisieren eines neuen Hosts davon ab, den nachweismodus, die für den Host-Überwachungsdienst derzeit konfiguriert ist.
Führen Sie zum Überprüfen der nachweismodus für Ihr geschütztes Fabric `Get-HgsServer` auf einem Host-Überwachungsdienst-Knoten.

#### <a name="software-configuration"></a>Software-Konfiguration
Stellen Sie sicher, dass dieser Windows Server 2016 Datacenter-Edition installiert ist, auf dem neuen Hyper-V-Host.
Windows Server 2016 Standard kann nicht abgeschirmte virtuelle Computer in einem geschützten Fabric ausgeführt.
Der Host kann es sich um Desktopdarstellung oder Server Core installiert sein.

Auf dem Server mit desktopdarstellung und Server Core müssen Sie die Hyper-V und Hyper-V-Unterstützung für Host-Überwachungsdiensts Serverrollen zu installieren:

```powershell
Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
```

#### <a name="admin-trusted-attestation"></a>Admin-vertrauenswürdiger Nachweis
Um einen neuen Host im Host-Überwachungsdienst zu registrieren, wenn Admin-vertrauenswürdiger Nachweis verwenden, müssen Sie zunächst den Host zu einer Sicherheitsgruppe in der Domäne hinzufügen, mit denen sie verknüpft ist.
In der Regel haben jede Domäne eine Sicherheitsgruppe für geschützte Hosts.
Wenn Sie die Gruppe bereits bei HGS registriert haben, ist die einzige Aktion, die Sie ergreifen müssen, zum Neustart des Servers aus, um die Gruppenmitgliedschaft zu aktualisieren.

Sie können überprüfen, welche Sicherheitsgruppen von Host-Überwachungsdienst als vertrauenswürdig eingestuft werden mithilfe des folgenden Befehls:

```powershell
Get-HgsAttestationHostGroup
```

Um eine neue Sicherheitsgruppe für Host-Überwachungsdiensts zu registrieren, erfassen Sie die Sicherheits-ID (SID) der Gruppe in der Domäne und registrieren Sie zunächst die SID mit Host-Überwachungsdienst.

```powershell
Add-HgsAttestationHostGroup -Name "Contoso Guarded Hosts" -Identifier "S-1-5-21-3623811015-3361044348-30300820-1013"
```

Anweisungen zum Einrichten der Vertrauensstellung zwischen der Hostdomäne und der Host-Überwachungsdienst stehen im Bereitstellungshandbuch.

#### <a name="tpm-trusted-attestation"></a>TPM-vertrauenswürdiger Nachweis
Wenn Host-Überwachungsdienst in der TPM-Modus konfiguriert ist, müssen die Hosts alle gesperrt und "enabled" Richtlinien, die mit dem Präfix "Hgs_", als auch mindestens eine TPM-Basislinie, TPM-Bezeichner und codeintegritätsrichtlinie übergeben.
Bei jedem eines neues Hosts hinzufügen, müssen Sie den neuen TPM-Bezeichner bei HGS registriert.
Solange der Host die gleiche Software ausgeführt wird (und die gleichen codeintegritätsrichtlinie angewendet werden wurde) und TPM-Baseline als einen anderen Host in Ihrer Umgebung, Sie müssen keine neue CI-Richtlinien oder Baselines hinzufügen.

**Hinzufügen der TPM-ID für einen neuen Host** auf dem neuen Host, führen Sie den folgenden Befehl aus, um die TPM-ID zu erfassen.
Achten Sie darauf, dass Sie einen eindeutigen Namen für den Host angeben, die Sie auf den Host-Überwachungsdienst nachschlagen können.
Sie benötigen diese Informationen, wenn Sie außer Betrieb den Host setzen oder ausgeführten abgeschirmte VMs im Host-Überwachungsdienst verhindern möchten.

```powershell
(Get-PlatformIdentifier -Name "Host01").InnerXml | Out-File C:\temp\host01.xml -Encoding UTF8
```

Kopieren Sie diese Datei auf Ihrem Host-Überwachungsdienst-Server, führen Sie dann den folgenden Befehl auf den Host bei HGS registriert.

```powershell
Add-HgsAttestationTpmHost -Name 'Host01' -Path C:\temp\host01.xml
```

**Hinzufügen einer neuen TPM-Baselines** , wenn der neue Host eine neue Hardware oder die Firmwarekonfiguration für Ihre Umgebung ausgeführt wird, müssen Sie möglicherweise eine neue TPM-Baseline zu nutzen.
Zu diesem Zweck führen Sie den folgenden Befehl auf dem Host.

```powershell
Get-HgsAttestationBaselinePolicy -Path 'C:\temp\hardwareConfig01.tcglog'
```

> [!NOTE]
> Wenn Sie eine Fehlermeldung mit dem Host Fehler bei der Überprüfung und wird nicht erfolgreich bestätigen erhalten, aber keine Sorge.
> Dies ist, dass eine voraussetzungsprüfung, um sicherzustellen, dass es sich bei dem Host ausgeführt werden kann abgeschirmte VMs und bedeutet, dass Sie eine codeintegritätsrichtlinie oder andere erforderliche Einstellung noch nicht installiert haben.
> Lesen Sie die Fehlermeldung, Änderungen vorgeschlagen werden, und versuchen Sie es erneut.
> Alternativ können Sie die Überprüfung zu diesem Zeitpunkt überspringen, durch das Hinzufügen der `-SkipValidation` Flag an den Befehl.

Kopieren Sie die TPM-Baseline auf Ihren Host-Überwachungsdienst-Server, und registrieren Sie sie mit dem folgenden Befehl aus.
Wir empfehlen Ihnen, eine Benennungskonvention zu verwenden, die Sie die Hardware und Firmware Konfiguration von dieser Klasse des Hyper-V-Hosts unterstützt.

```powershell
Add-HgsAttestationTpmPolicy -Name 'HardwareConfig01' -Path 'C:\temp\hardwareConfig01.tcglog'
```

**Hinzufügen einer neuen codeintegritätsrichtlinie** , wenn Sie die codeintegritätsrichtlinie auf Hyper-V-Hosts geändert haben, müssen Sie die neue Richtlinie mit Host-Überwachungsdienst registrieren, bevor diese Hosts, erfolgreich nachweisen können.
Auf einem Host Verweis, der als master-Image für die vertrauenswürdige Hyper-V-Computer in Ihrer Umgebung dient, erfassen eine neue CI-Richtlinie, mit der `New-CIPolicy` Befehl.
Wir empfehlen Ihnen die Verwendung der **FilePublisher** Ebene und **Hash** für Richtlinien für Hyper-V-Host CI fallback.
Sie sollten zuerst eine CI-Richtlinie erstellen, im Überwachungsmodus, um sicherzustellen, dass alles wie erwartet funktioniert.
Nach der Überprüfung einer beispielworkload eine auf dem System, können Sie erzwingt die Richtlinie, und kopieren Sie die erzwungene Version auf Host-Überwachungsdienst.
Eine vollständige Liste der Konfigurationsoptionen für Code Integrity-Richtlinie, wenden Sie sich an den [Dokumentation zu Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies).

```powershell
# Capture a new CI policy with the FilePublisher primary level and Hash fallback and enable user mode code integrity protections
New-CIPolicy -FilePath 'C:\temp\ws2016-hardware01-ci.xml' -Level FilePublisher -Fallback Hash -UserPEs

# Apply the CI policy to the system
ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\ws2016-hardware01-ci.xml' -BinaryFilePath 'C:\temp\ws2016-hardware01-ci.p7b'
Copy-Item 'C:\temp\ws2016-hardware01-ci.p7b' 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'
Restart-Computer

# Check the event log for any untrusted binaries and update the policy if necessary
# Consult the Device Guard documentation for more details

# Change the policy to be in enforced mode
Set-RuleOption -FilePath 'C:\temp\ws2016-hardare01-ci.xml' -Option 3 -Delete

# Apply the enforced CI policy on the system
ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\ws2016-hardware01-ci.xml' -BinaryFilePath 'C:\temp\ws2016-hardware01-ci.p7b'
Copy-Item 'C:\temp\ws2016-hardware01-ci.p7b' 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'
Restart-Computer
```

Nachdem Sie die Richtlinie erstellt haben, getestet und erzwungen, kopieren Sie die Binärdatei (. p7b) auf Ihren Host-Überwachungsdienst-Server und registrieren Sie die Richtlinie.

```powershell
Add-HgsAttestationCiPolicy -Name 'WS2016-Hardware01' -Path 'C:\temp\ws2016-hardware01-ci.p7b'
```

**Hinzufügen von einen Verschlüsselungsschlüssel für die Arbeitsspeicher-Dumps**

Wenn die *Host-Überwachungsdienst\_NoDumps* Richtlinie ist deaktiviert und *Host-Überwachungsdienst\_DumpEncryption* Richtlinie aktiviert ist, geschützte Hosts zulässig sind (einschließlich von Absturzabbildern) Speicherabbilder sein aktiviert, solange diese Speicherabbilder verschlüsselt werden. Überwachte Hosts werden nur einen Nachweis erbringen, wenn sie deaktiviert Speicherabbilder oder haben sie mit einem Schlüssel bekannt, dass der Host-Überwachungsdienst verschlüsselt werden. Standardmäßig werden keine Verschlüsselungsschlüssel sichern auf Host-Überwachungsdienst konfiguriert.

Um einen Verschlüsselungsschlüssel für die Abbild-Host-Überwachungsdienst hinzuzufügen, verwenden Sie die `Add-HgsAttestationDumpPolicy` -Cmdlet zum Bereitstellen von Host-Überwachungsdienst mit dem Hashwert der Ihr Verschlüsselungsschlüssel sichern.
Wenn Sie eine TPM-Baseline auf einem Hyper-V-Host mit speicherabbildverschlüsselung konfiguriert erfassen, wird der Hash ist in der Tcglog enthalten und bereitgestellt werden können die `Add-HgsAttestationDumpPolicy` Cmdlet.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey01' -Path 'C:\temp\TpmBaselineWithDumpEncryptionKey.tcglog'
```

Alternativ können Sie direkt eine Zeichenfolgendarstellung des Hashs an das Cmdlet bereitstellen.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey02' -PublicKeyHash '<paste your hash here>'
```

Achten Sie darauf, dass Sie Host-Überwachungsdienst jedes eindeutige Abbild-Verschlüsselungsschlüssel hinzugefügt wird, wenn Sie unterschiedliche Schlüssel für Ihre geschützten Fabrics verwenden möchten.
Hosts, die mit einem Schlüssel, der Host-Überwachungsdienst nicht bekannt Speicherabbilder verschlüsselt werden, werden nicht einen Nachweis erbringen.

In der Hyper-V-Dokumentation für Weitere Informationen zu [Konfigurieren der Verschlüsselung auf Hosts Sichern](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption).

#### <a name="check-if-the-system-passed-attestation"></a>Überprüfen Sie, ob das System der Nachweis bestanden
Nachdem die erforderlichen Informationen bei HGS registriert haben, sollten Sie überprüfen, ob der Host den Nachweis besteht.
Führen Sie auf dem neu hinzugefügten Hyper-V-Host `Set-HgsClientConfiguration` , und geben Sie die richtigen URLs für den Host-Überwachungsdienst-Cluster.
Diese URLs erhalten Sie, indem Sie Ausführung `Get-HgsServer` auf einem Host-Überwachungsdienst-Knoten.

```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'http://hgs.bastion.local/KeyProtection' -AttestationServerUrl 'http://hgs.bastion.local/Attestation'
```

Wenn Sie der resultierende Status nicht angeben, dass "IsHostGuarded: "True""müssen Sie zur Problembehandlung der Konfiguration.
Führen Sie den folgenden Befehl aus, um einen detaillierten Bericht zu Problemen zu erhalten, mit denen Sie den Nachweis der Fehler beheben kann, auf dem Host, der Fehler beim Nachweis.

```powershell
Get-HgsTrace -RunDiagnostics -Detailed
```

> [!IMPORTANT]
> Wenn Sie Windows Server-2019 oder Windows 10, Version 1809 verwenden und die anwendungssteuerungscode-Integritätsrichtlinien, verwenden `Get-HgsTrace` möglicherweise einen Fehler für zurück der **Code Integrity Richtlinie aktiv** Diagnose.
> Sie können dieses Ergebnis gefahrlos ignorieren, bei dem nur fehlgeschlagene Diagnose.

### <a name="review-attestation-policies"></a>Überprüfen Sie Richtlinien zum Nachweis
Um den aktuellen Zustand der auf Host-Überwachungsdienst konfigurierten Richtlinien zu überprüfen, führen Sie die folgenden Befehle auf einem Host-Überwachungsdienst-Knoten:

```powershell
# List all trusted security groups for admin-trusted attestation
Get-HgsAttestationHostGroup

# List all policies configured for TPM-trusted attestation
Get-HgsAttestationPolicy
```

Wenn Sie eine Richtlinie aktiviert finden, die nicht mehr erfüllt die sicherheitsanforderung Ihrer (z. B. eine alte codeintegritätsrichtlinie der jetzt als unsicher angesehen wird), können Sie es deaktivieren, durch, und Ersetzen Sie dabei den Namen der Richtlinie in den folgenden Befehl aus:

```powershell
Disable-HgsAttestationPolicy -Name 'PolicyName'
```

Auf ähnliche Weise können Sie `Enable-HgsAttestationPolicy` um eine Richtlinie erneut zu aktivieren.

Wenn Sie eine Richtlinie und möchten es von allen Knoten der Host-Überwachungsdienst entfernen nicht mehr benötigen, führen Sie `Remove-HgsAttestationPolicy -Name 'PolicyName'` um die Richtlinie dauerhaft zu löschen.

## <a name="changing-attestation-modes"></a>Nachweismodi ändern
Wenn Sie Ihr geschützte Fabric mit Admin-vertrauenswürdiger Nachweis begonnen haben, möchten Sie wahrscheinlich, die wesentlich stärker TPM-nachweismodus zu aktualisieren, sobald Sie genügend TPM 2.0-kompatiblen Hosts in Ihrer Umgebung haben.
Bei der Sie wechseln möchten, können Sie alle Elemente der Nachweis (CI-Richtlinien, TPM-Baselines und TPM-Bezeichner) in Host-Überwachungsdienst vorab laden, und weiterhin die Host-Überwachungsdienst mit Admin-vertrauenswürdiger Nachweis auszuführen.
Zu diesem Zweck führen Sie einfach die Anweisungen in der [Autorisieren eines neuen überwachten Hosts](#authorizing-new-guarded-hosts) Abschnitt.

Nachdem Sie alle Ihre Richtlinien zum Host-Überwachungsdienst hinzugefügt haben, besteht der nächste Schritt, der Versuch einer synthetischen Nachweis auf den Hosts, um festzustellen, ob sie einen Nachweis, im TPM-Modus erbringen sollen ausgeführt.
Dies wirkt sich nicht auf den aktuellen Betriebszustand des Host-Überwachungsdienst.
Die folgenden Befehle, müssen auf einem Computer ausgeführt werden, die Zugriff auf alle Hosts in der Umgebung mindestens einen Host-Überwachungsdienst-Knoten hat.
Wenn Ihre Firewall oder andere Sicherheitsrichtlinien dies verhindern, können Sie diesen Schritt überspringen.
Wenn möglich, wird empfohlen, den Nachweis der synthetischen können nützliche Informationen, ob "ein" in den TPM-Modus für Ihre virtuellen Computer Ausfallzeiten kommt ausgeführt. 

```powershell
# Get information for each host in your environment
$hostNames = 'host01.contoso.com', 'host02.contoso.com', 'host03.contoso.com'
$credential = Get-Credential -Message 'Enter a credential with admin privileges on each host'
$targets = @()
$hostNames | ForEach-Object { $targets += New-HgsTraceTarget -Credential $credential -Role GuardedHost -HostName $_ }

$hgsCredential = Get-Credential -Message 'Enter an admin credential for HGS'
$targets += New-HgsTraceTarget -Credential $hgsCredential -Role HostGuardianService -HostName 'HGS01.bastion.local'

# Initiate the synthetic attestation attempt
Get-HgsTrace -RunDiagnostics -Target $targets -Diagnostic GuardedFabricTpmMode 
```

Überprüfen Sie nachdem die Diagnose abgeschlossen ist die ausgegebene Informationen, um festzustellen, ob alle Hosts Nachweis im TPM-Modus fehlgeschlagen wären.
Führen Sie die Diagnose erneut aus, bis Sie von jedem Host zu einen "Pass" erhalten, fahren Sie mit Host-Überwachungsdienst in den TPM-Modus zu wechseln.

**Ändern in den TPM-Modus** dauert nur ein paar Sekunden abgeschlossen.
Führen Sie den folgenden Befehl auf einem Host-Überwachungsdienst-Knoten den nachweismodus zu aktualisieren.

```powershell
Set-HgsServer -TrustTpm
```

Wenn Sie Probleme auftreten und wieder in den Active Directory-Modus wechseln zu müssen ausführen, erreichen Sie dies mit `Set-HgsServer -TrustActiveDirectory`.

Nachdem Sie, dass alles bestätigt haben wie erwartet funktioniert, sollten alle vertrauenswürdigen Active Directory-Hostgruppen vom Host-Überwachungsdienst entfernen und die Vertrauensstellung zwischen den Domänen-Host-Überwachungsdienst und der Fabric entfernen.
Wenn Sie die Active Directory-Vertrauensstellung vorhanden lassen, riskieren Sie jemand die Vertrauensstellung erneut aktiviert, und wechseln Host-Überwachungsdienst in den Active Directory-Modus, der nicht vertrauenswürdigen Code deaktiviert ausführen, auf die überwachten Hosts verwendet werden können.

## <a name="key-management"></a>Schlüsselverwaltung
Die geschützte Fabric-Lösung verwendet mehrere öffentlichen/privaten Schlüsselpaaren überprüfen die Integrität der verschiedenen Komponenten in der Projektmappe, und Verschlüsseln von Geheimnissen für Mandanten.
Host-Überwachungsdienst ist mit mindestens zwei Zertifikate (mit öffentlichen und privaten Schlüssel) konfiguriert, die verwendet werden, zum Signieren und verschlüsseln den Schlüssel für abgeschirmte virtuelle Computer zu starten.
Dieser Schlüssel müssen sorgfältig verwaltet werden.
Wenn der private Schlüssel von einem Angreifer abgerufen wird, werden sie Lage unshield alle virtuellen Computer, auf Ihr Fabric ausgeführt wird, oder richten Sie einen stünden HGS-Cluster, der weniger strikten Richtlinien der Nachweis verwendet, um die Schutzmechanismen zu umgehen, die Sie platziert.
Sie verlieren die privaten Schlüssel während eines Notfalls und diese in eine Sicherung nicht gefunden, müssen Sie ein neues Schlüsselpaar einrichten und jeden virtuellen Computer erneut verschlüsselt, um die neuen Zertifikate zu autorisieren.

Dieser Abschnitt enthält allgemeine schlüsselverwaltung Themen, mit denen Sie Ihre Schlüssel zu konfigurieren, damit sie funktionsfähig und sicher sind.

### <a name="adding-new-keys"></a>Hinzufügen neuer Schlüssel
Während der Host-Überwachungsdienst mit einem einzelnen Satz von Schlüsseln initialisiert werden muss, können Sie mehr als eine einzelne Verschlüsselung und den Signaturschlüssel zum Host-Überwachungsdienst hinzufügen.
Die zwei häufigsten Gründe, warum Sie Host-Überwachungsdienst neue Schlüssel hinzufügen würden, sind:
1. "Bring your own Key"-Szenarien unterstützt, in denen Mandanten kopieren Sie ihre privaten Schlüssel in Ihr Hardwaresicherheitsmodul und autorisieren nur ihre Schlüssel, um geschützten virtuelle Maschinen zu starten.
2. Um die vorhandenen Schlüssel für die Host-Überwachungsdienst durch zuerst Hinzufügen der neuen Schlüssel, und beide Sätze von Schlüsseln beibehalten, bis die einzelnen virtuellen Computer zu ersetzen wurde Konfiguration aktualisiert, um die Verwendung der neuen Schlüssel.

Der Prozess zum Hinzufügen der neuen Schlüssel, unterscheidet sich basierend auf dem Typ von Zertifikat, das Sie verwenden.

**Option 1: Hinzufügen eines Zertifikats in einem HSM gespeicherten**

Unsere empfohlene Vorgehensweise zum Sichern von Host-Überwachungsdienst-Schlüssel ist zum Verwenden von Zertifikaten, die in einem Hardwaresicherheitsmodul (HSM) erstellt.
HSMs stellen Sie sicher, dass die Verwendung der Schlüssel mit physischen Zugriff auf eine sicherheitsrelevante Gerät in Ihrem Datencenter verknüpft ist.
Jeder HSM ist anders, und verfügt über eine eindeutige Prozess zum Erstellen von Zertifikaten und registrieren Sie ihn beim Host-Überwachungsdienst.
Die folgenden Schritte dienen zur Verfügung zu stellen Ungefährer für die Verwendung von HSM mit Zertifikaten gesichert.
Funktionen und die genauen Schritte finden Sie in den HSM-Anbieter-Dokumentation.

1. Installieren Sie die HSM-Software auf jedem Host-Überwachungsdienst-Knoten im Cluster. Je nachdem, ob Sie ein Netzwerk oder lokalen HSM-Gerät haben müssen Sie möglicherweise so konfigurieren Sie das HSM, um Ihren Computerzugriff auf die Schlüsselspeicher zu gewähren.
2. Erstellen Sie 2 Zertifikate in das HSM mit **2048-Bit-RSA-Schlüssel** für Verschlüsselung und Signatur
    1. Erstellen Sie ein Verschlüsselungszertifikat mit dem **Data Encipherment** key Usage-Eigenschaft in Ihrem HSM
    2. Erstellen Sie ein Signaturzertifikat mit dem **digitale Signatur** key Usage-Eigenschaft in Ihrem HSM
3. Installieren Sie die Zertifikate in jedem Knoten des Host-Überwachungsdienst lokalen Zertifikatspeicher gemäß Anleitung für den HSM-Anbieter.
4. Wenn Ihr HSM differenzierte Berechtigungen gewähren bestimmten Anwendungen oder Benutzern die Berechtigung zur Verwendung des privaten Schlüssels verwendet wird, müssen Sie Ihr HGS gruppenverwalteten Dienstkontenzugriff auf das Zertifikat zu gewähren. Sie finden den Namen des Host-Überwachungsdienst gMSA-Kontos mit `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
5. Hinzufügen der Zertifikate für Signierung und Verschlüsselung auf dem Host-Überwachungsdienst und Ersetzen Sie dabei die Fingerabdrücke mit denen Ihre Zertifikate in den folgenden Befehlen:

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA"
    ```

**Option 2: Hinzufügen von softwarezertifikaten für nicht exportierbare**

Wenn Sie über ein Software-gesicherten Zertifikat von Ihrem Unternehmen oder einer öffentlichen Zertifizierungsstelle, die einen nicht exportierbaren privaten Schlüssel aufweist, Sie das Zertifikat auf dem Host-Überwachungsdienst mit seinen Fingerabdruck hinzufügen müssen.
1. Installieren Sie das Zertifikat auf Ihrem Computer entsprechend der Zertifizierungsstelle Anweisungen ein.
2. Erteilen Sie die Host-Überwachungsdienst gruppenverwalteten Dienstkonto Lese--Zugriff auf den privaten Schlüssel des Zertifikats. Sie finden den Namen des Host-Überwachungsdienst gMSA-Kontos mit `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
3. Registrieren des Zertifikats mit Host-Überwachungsdiensts mithilfe des folgenden Befehls, und Ersetzen in den Fingerabdruck des Zertifikats (ändern Sie *Verschlüsselung* zu *Signierung* für das Signieren von Zertifikaten):

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    ```

> [!IMPORTANT]
> Sie müssen manuell installieren Sie den privaten Schlüssel, und gewähren von Lesezugriff auf das gMSA-Konto auf jedem Host-Überwachungsdienst-Knoten.
> Host-Überwachungsdienst können nicht automatisch repliziert werden private Schlüssel für *alle* durch seinen Fingerabdruck registrierte Zertifikat.

**Option 3: Hinzufügen von Zertifikaten im PFX-Dateien gespeichert**

Wenn Sie über ein Software-Backup-Zertifikat mit einem exportierbaren privaten Schlüssel, die in das PFX-Dateiformat gespeichert und mit einem Kennwort geschützt werden können verfügen, kann Host-Überwachungsdienst Ihre Zertifikate automatisch für Sie verwalten.
Zertifikate, die mit der PFX-Dateien hinzugefügt werden automatisch auf jedem Knoten des Clusters Host-Überwachungsdienst repliziert und Host-Überwachungsdienst sichert den Zugriff auf die privaten Schlüssel.
Um ein neues Zertifikat mit einer PFX-Datei hinzuzufügen, führen Sie die folgenden Befehle auf einem Host-Überwachungsdienst-Knoten (ändern Sie *Verschlüsselung* zu *Signierung* für das Signieren von Zertifikaten):

```powershell
$certPassword = Read-Host -AsSecureString -Prompt "Provide the PFX file password"
Add-HgsKeyProtectionCertificate -CertificateType Encryption -CertificatePath "C:\temp\encryptionCert.pfx" -CertificatePassword $certPassword
```

**Identifizieren und ändern die primäre Zertifikate** während der Host-Überwachungsdienst mehrere Zertifikate für Signierung und Verschlüsselung unterstützen kann, wird ein Paar als ihre "primary" Zertifikate verwendet.
Hierbei handelt es sich um die Zertifikate, die verwendet werden, wenn ein Benutzer der überwachungsmetadaten für diesen Host-Überwachungsdienst-Cluster heruntergeladen.
Um zu überprüfen, welche Zertifikate als Ihre primäre Zertifikate derzeit markiert sind, führen Sie den folgenden Befehl aus:

```powershell
Get-HgsKeyProtectionCertificate -IsPrimary $true
```

Um einen neuen primären Verschlüsselung oder Signaturzertifikat festlegen, den Fingerabdruck des das gewünschte Zertifikat aus, und markieren Sie ihn als primäre mit den folgenden Befehlen:

```powershell
Get-HgsKeyProtectionCertificate
Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899" -IsPrimary
Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA" -IsPrimary
```

### <a name="renewing-or-replacing-keys"></a>Erneuern oder Ersetzen von Schlüsseln
Beim Erstellen der Zertifikate, die von Host-Überwachungsdienst verwendet werden die Zertifikate ein Ablaufdatum gemäß der Richtlinie für das Zertifikat der Zertifizierungsstelle und Ihre Anforderung zugewiesen werden.
In Szenarien, in denen die Gültigkeit des Zertifikats wie z. B. das Sichern von HTTP-Kommunikation wichtig ist, müssen normalerweise Zertifikate erneuert werden, bevor sie ablaufen, um eine dienstunterbrechung oder schlecht Fehlermeldung zu vermeiden.
Host-Überwachungsdienst verwendet Zertifikate nicht in dieser Hinsicht.
Host-Überwachungsdienst ist einfach mithilfe von Zertifikaten auf einfache Weise erstellen und speichern ein asymmetrisches Schlüsselpaar.
Ein abgelaufener Verschlüsselung oder Signaturzertifikat auf dem Host-Überwachungsdienst gibt eine Schwachstelle oder Verlust des Schutzes für abgeschirmte VMs nicht an.
Darüber hinaus werden die zertifikatsperrüberprüfungen nicht vom Host-Überwachungsdienst ausgeführt.
Wenn ein Host-Überwachungsdienst-Zertifikat oder der ausstellenden Zertifizierungsstelle widerrufen wurde, hat es keine Auswirkung auf HGS Verwendung des Zertifikats.

Nur dann müssen Sie ein Zertifikat für die Host-Überwachungsdienst kümmern wird gestohlen wurde, wenn Sie Grund zu glauben, dass seinen privaten Schlüssel hat verfügen.
In diesem Fall ist die Integrität Ihrer geschützten virtuellen Computer gefährdet, da besitzt die private Hälfte des der HGS-Verschlüsselung und Unterzeichnung von Schlüsselpaar ausreichend ist, um die geschützten Schutzmaßnahmen auf einem virtuellen Computer zu entfernen oder einen gefälschten HGS-Server, der schwächere Nachweis Richtlinien ist, einsatzbereit.

Wenn Sie in dieser Situation geraten oder Compliance-Standards Zertifikatsschlüssel regelmäßig aktualisieren erforderlich sind, beschreiben die folgenden Schritte den Prozess, um die Schlüssel auf einem Host-Überwachungsdienst-Server zu ändern.
Beachten Sie, dass die folgende Anleitung kein leichtes Unterfangen darstellt, das für jeden virtuellen Computer vom Host-Überwachungsdienst-Cluster verarbeitet zu einer Unterbrechung des Diensts führen.
Richtiger Planung für das Ändern von Host-Überwachungsdienst-Schlüssels ist erforderlich, um dienstunterbrechungen zu minimieren und Gewährleistung der Sicherheit der Mandanten-VMs.

Führen Sie auf einem Host-Überwachungsdienst-Knoten die folgenden Schritte aus, um ein neues Paar von Verschlüsselung und Signaturzertifikate zu registrieren.
Finden Sie im Abschnitt [Hinzufügen neuer Schlüssel](#adding-new-keys) für detaillierte Informationen für die verschiedenen Möglichkeiten zum Host-Überwachungsdienst neuer Schlüssel hinzugefügt.
1. Erstellen Sie ein neues Paar der Verschlüsselung und Signaturzertifikate für den Host-Überwachungsdienst-Server. Im Idealfall werden diese in einem Hardwaresicherheitsmodul erstellt werden.
2. Registrieren die neue Verschlüsselung und Signaturzertifikate mit **hinzufügen-HgsKeyProtectionCertificate**

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>
    ```
3. Wenn Sie die Fingerabdrücke verwendet, müssen Sie zu jedem Knoten im Cluster installieren Sie den privaten Schlüssel und die Host-Überwachungsdienst gMSA Zugriff auf den Schlüssel zu gewähren.
4. Stellen Sie die neuen Zertifikate der Standardzertifikate im Host-Überwachungsdienst

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsPrimary
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsPrimary
    ```

An diesem Punkt geschützten Daten, die mit Metadaten abgerufen, die über den Host-Überwachungsdienst-Knoten erstellt die neuen Zertifikate verwenden, aber die vorhandene virtuelle Computer weiterhin funktionsfähig, da ältere Zertifikate immer noch vorhanden sind.
Um sicherzustellen, dass alle vorhandenen virtuellen Computer mit der neuen Schlüssel verwendet werden kann, müssen Sie die Schlüsselschutzvorrichtung auf jedem virtuellen Computer zu aktualisieren.
Dies ist eine Aktion, die den VM-Besitzer (Person oder Entität im Besitz der Überwachungsdienst "Besitzer") muss der beteiligt sein.
Führen Sie für jeden geschützten virtuellen Computer die folgenden Schritte aus:
5. Fahren Sie den virtuellen Computer herunter. Der virtuelle Computer kann nicht wieder aktiviert werden, bis die übrigen Schritte abgeschlossen sind, ansonsten müssen Sie zum Starten des Prozesses wieder ganz von vorn.
6. Speichern Sie die aktuelle Schlüsselschutzvorrichtung in einer Datei: `Get-VMKeyProtector -VMName 'VM001' | Out-File '.\VM001.kp'`
7. Übertragen Sie die KP auf der VM-Besitzer
8. Haben Sie den Download der Besitzer die aktualisierte Überwachungsdienst Informationen von Host-Überwachungsdienst und importieren Sie es auf ihrem lokalen system
9. Gelesen Sie die aktuelle KP in den Arbeitsspeicher, die KP gewähren Sie den neuen Überwachungsdienst Zugriff und speichern Sie sie in eine neue Datei, indem Sie die folgenden Befehle ausführen:

    ```powershell
    $kpraw = Get-Content -Path .\VM001.kp
    $kp = ConvertTo-HgsKeyProtector -Bytes $kpraw
    $newGuardian = Get-HgsGuardian -Name 'UpdatedHgsGuardian'
    $updatedKP = Grant-HgsKeyProtectorAccess -KeyProtector $kp -Guardian $newGuardian
    $updatedKP.RawData | Out-File .\updatedVM001.kp
    ```
10. Kopieren Sie die aktualisierte KP zurück zum Host-fabric
11. Der ursprüngliche virtuelle Computer gelten Sie der-KP:

   ```powershell
   $updatedKP = Get-Content -Path .\updatedVM001.kp
   Set-VMKeyProtector -VMName VM001 -KeyProtector $updatedKP
   ```
12. Abschließend starten Sie den virtuellen Computer aus, und stellen Sie sicher, dass es erfolgreich ausgeführt wird.

> [!NOTE]
> Wenn der Besitzer der virtuellen Computer eine falschen Schlüsselschutzvorrichtung auf dem virtuellen Computer und Ihr Fabric für die VM ist nicht autorisiert, werden Sie nicht die abgeschirmte VM starten.
> Um auf die letzten bekannten guten Schlüsselschutzvorrichtung zurückzugeben, führen `Set-VMKeyProtector -RestoreLastKnownGoodKeyProtector`

Nachdem alle virtuellen Computer zum Autorisieren der neuen Schlüssel für den Überwachungsdienst aktualisiert wurden, können Sie deaktivieren und die alten Schlüssel entfernen.

13. Die Fingerabdrücke für die alte Zertifikate aus abrufen `Get-HgsKeyProtectionCertificate -IsPrimary $false`

14. Deaktivieren Sie jedes Zertifikat, indem Sie die folgenden Befehle ausführen:  

   ```powershell
   Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsEnabled $false
   Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsEnabled $false
   ```

15. Nachdem Sie sichergestellt haben, dass die virtuellen Computer weiterhin für den Einstieg können entfernen die Zertifikate, die deaktiviert ist, Sie die Zertifikate von Host-Überwachungsdienst durch die folgenden Befehle ausführen:

   ```powershell
   Remove-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>`
   Remove-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>`
   ```

> [!IMPORTANT]
> VM-Sicherungen enthalten alte Kennwortschlüssel-Schutzvorrichtung, mit denen die alte Zertifikate verwendet werden, um den virtuellen Computer zu starten.
> Wenn Sie wissen, dass Ihr private Schlüssel gefährdet ist, sollten Sie davon ausgehen, dass die VM-Sicherungen ebenfalls gefährdet werden können und entsprechende Maßnahmen ergreifen.
> Zerstören die VM-Konfiguration aus den Sicherungen (vmcx) entfernt die Schlüsselschutzvorrichtungen auf Kosten der BitLocker-Wiederherstellungskennwort zu verwenden, den virtuellen Computer das nächste Mal starten.

### <a name="key-replication-between-nodes"></a>Replikation zwischen Knoten
Jeder Knoten im Cluster-Host-Überwachungsdienst muss konfiguriert werden, mit der gleichen Verschlüsselung, "Signierung", und (Wenn konfiguriert) SSL-Zertifikate.
Dies ist erforderlich, um sicherzustellen, dass Hyper-V-Hosts, die auf einen beliebigen Knoten im Cluster mit unseren Lesern ihrer Anforderungen, die erfolgreich verarbeitet werden können.

**Wenn Sie HGS-Server mit der PFX-Zertifikate initialisiert** und Host-Überwachungsdienst die öffentlichen und privaten Schlüssel dieser Zertifikate automatisch auf jedem Knoten im Cluster repliziert werden.
Sie müssen nur die Schlüssel auf einem Knoten hinzufügen.

**Wenn Sie HGS-Server mit Zertifikat verweisen initialisiert** oder Fingerabdrücke, und klicken Sie dann auf Host-Überwachungsdienst nur repliziert wird die *öffentliche* Schlüssel im Zertifikat für jeden Knoten.
Darüber hinaus Host-Überwachungsdienst können nicht gewährt selbst den Zugriff auf den privaten Schlüssel auf einem beliebigen Knoten in diesem Szenario.
Aus diesem Grund ist es Ihre Aufgabe, aus:
1. Installieren Sie den privaten Schlüssel auf jedem Host-Überwachungsdienst-Knoten
2. Erteilen Sie die Host-Überwachungsdienst gruppenverwalteten Dienstkonto (gMSA) Zugriff auf den privaten Schlüssel auf jedem Knoten, dass dazu zusätzliche operative Last hinzufügen, jedoch sie für den HSM-gesicherten Schlüssel und Zertifikate mit nicht exportierbaren privaten Schlüssel erforderlich sind.

**SSL-Zertifikate** werden nie in irgendeiner Form repliziert.
Es ist Ihre Aufgabe, initialisieren jeden Host-Überwachungsdienst-Server mit dasselbe SSL-Zertifikat, und aktualisieren jeden Server aus, wenn Sie angeben, erneuern oder Ersetzen Sie das SSL-Zertifikat.
Wenn das SSL-Zertifikat ersetzt wird, wird empfohlen, die Sie dazu die [Set-HgsServer](https://technet.microsoft.com/library/mt652180.aspx) Cmdlet.

## <a name="unconfiguring-hgs"></a>Aufheben der Konfiguration des Host-Überwachungsdienst

Wenn Sie außer Betrieb nehmen oder neu erheblich einen HGS-Server konfigurieren möchten, erreichen Sie dies über die [Clear-HgsServer](https://technet.microsoft.com/library/mt652176.aspx) oder [deinstallieren-HgsServer](https://technet.microsoft.com/library/mt652182.aspx) Cmdlets.

### <a name="clearing-the-hgs-configuration"></a>Löschen die Konfiguration des Host-Überwachungsdienst

Verwenden Sie zum Entfernen eines Knotens aus dem Cluster-Host-Überwachungsdienst die [Clear-HgsServer](https://technet.microsoft.com/library/mt652176.aspx) Cmdlet.
Mit diesem Cmdlet wird auf dem Server die folgenden Änderungen vornehmen, in dem er ausgeführt wird:

- Hebt die Registrierung für die Nachweis- und Datenschutzdienste
- Entfernt den "microsoft.windows.hgs" JEA-verwaltungsendpunkt
- Entfernt den lokalen Computer aus dem Failovercluster-Host-Überwachungsdienst

Wenn der Server den letzten HGS-Knoten im Cluster ist, werden der Cluster und die entsprechende Distributed Network Name Ressource auch zerstört werden.

```powershell
# Removes the local computer from the HGS cluster
Clear-HgsServer
```

Nachdem der Löschvorgang abgeschlossen ist, kann der HGS-Server mit erneut initialisiert werden [Initialize-HgsServer](https://technet.microsoft.com/library/mt652185.aspx).
Wenn Sie verwendet [Install-HgsServer](https://technet.microsoft.com/library/mt652169.aspx) zum Einrichten einer Active Directory Domain Services-Domäne dieser Domäne bleibt konfiguriert ist und funktioniert nach dem Löschvorgang.

### <a name="uninstalling-hgs"></a>Deinstallieren von Host-Überwachungsdienst

Wenn Sie zum Entfernen eines Knotens aus dem Cluster-Host-Überwachungsdienst möchten **und** tiefer stufen der Active Directory-Domänencontroller ausgeführt wird, verwenden Sie die [deinstallieren-HgsServer](https://technet.microsoft.com/library/mt652182.aspx) Cmdlet.
Mit diesem Cmdlet wird auf dem Server die folgenden Änderungen vornehmen, in dem er ausgeführt wird:

- Hebt die Registrierung für die Nachweis- und Datenschutzdienste
- Entfernt den "microsoft.windows.hgs" JEA-verwaltungsendpunkt
- Entfernt den lokalen Computer aus dem Failovercluster-Host-Überwachungsdienst
- Die Active Directory-Domänencontroller tiefer gestuft, wenn konfiguriert

Wenn der Server den letzten HGS-Knoten im Cluster ist, werden die Domäne, Failovercluster und des Clusters verteilt Vnn-Ressource auch zerstört werden.

```powershell
# Removes the local computer from the HGS cluster and demotes the ADDC (restart required)
$newLocalAdminPassword = Read-Host -AsSecureString -Prompt "Enter a new password for the local administrator account"
Uninstall-HgsServer -LocalAdministratorPassword $newLocalAdminPassword -Restart
```

Nachdem der Deinstallationsvorgang abgeschlossen ist, und der Computer neu gestartet wurde, können Sie neu installieren ADDC und Host-Überwachungsdienst mit [Install-HgsServer](https://technet.microsoft.com/library/mt652169.aspx) oder fügen Sie den Computer einer Domäne, und initialisieren Sie den Server-Host-Überwachungsdiensts in der Domäne mit [ Initialize-HgsServer](https://technet.microsoft.com/library/mt652185.aspx).

Wenn Sie nicht mehr den Computer als ein Knoten für die Host-Überwachungsdienst verwenden möchten, können Sie die Rolle aus Windows entfernen.

```powershell
Uninstall-WindowsFeature HostGuardianServiceRole
```
