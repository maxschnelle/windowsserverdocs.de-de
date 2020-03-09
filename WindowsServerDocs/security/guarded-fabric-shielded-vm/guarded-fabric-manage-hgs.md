---
title: Verwalten des Host-Überwachungs Diensts
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: eecb002e-6ae5-4075-9a83-2bbcee2a891c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 41912c90beacbb0c0c285ea4da8305c1afdf2a51
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78370644"
---
# <a name="managing-the-host-guardian-service"></a>Verwalten des Host-Überwachungs Diensts

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Der Host-Überwachungsdienst (Host Guardian Service, HGS) ist das Kernstück der geschützten Fabric-Lösung.
Er ist dafür verantwortlich, sicherzustellen, dass Hyper-V-Hosts im Fabric dem hostet oder Unternehmen bekannt sind und vertrauenswürdige Software ausführen und die Schlüssel verwalten, die zum Starten von abgeschirmten VMS verwendet werden.
Wenn ein Mandant beschließt, Sie zu hosten, um die geschützten VMS zu hosten, platziert er seine Vertrauensstellung in Ihrer Konfiguration und Verwaltung des Host-Überwachungs Diensts.
Daher ist es sehr wichtig, die bewährten Methoden bei der Verwaltung des Host-Überwachungs Diensts zu befolgen, um die Sicherheit, Verfügbarkeit und Zuverlässigkeit Ihres geschützten Fabrics sicherzustellen.
In den Anweisungen in den folgenden Abschnitten werden die häufigsten Betriebsprobleme behandelt, die Administratoren von HGS begegnen.

## <a name="limiting-admin-access-to-hgs"></a>Einschränken des Administrator Zugriffs auf HGS
Aufgrund der sicherheitssensiblen Natur von HGS ist es wichtig sicherzustellen, dass seine Administratoren sehr vertrauenswürdige Mitglieder Ihrer Organisation sind und im Idealfall von den Administratoren Ihrer Fabric-Ressourcen getrennt werden.
Außerdem wird empfohlen, dass Sie nur HGS von sicheren Arbeitsstationen mithilfe von sicheren Kommunikationsprotokollen verwalten, wie z. b. WinRM über HTTPS.

### <a name="separation-of-duties"></a>Trennung von Aufgaben
Beim Einrichten von HGS haben Sie die Möglichkeit, eine isolierte Active Directory Gesamtstruktur nur für HGS zu erstellen oder HGS mit einer vorhandenen vertrauenswürdigen Domäne zu verknüpfen.
Diese Entscheidung und die Rollen, die Sie den Administratoren in Ihrer Organisation zuweisen, bestimmen die Vertrauensstellungs Grenze für HGS.
Wer Zugriff auf HGS hat, egal ob direkt als Administrator oder indirekt als Administrator von etwas anderem (z. b. Active Directory), das die HGS beeinflussen kann, hat Kontrolle über das geschützte Fabric.
HGS-Administratoren wählen, welche Hyper-V-Hosts autorisiert sind, abgeschirmte VMS auszuführen und die Zertifikate zu verwalten, die zum Starten von abgeschirmten VMS erforderlich sind.
Angreifer oder böswillige Administratoren, die Zugriff auf HGS haben, können mit dieser Leistungsfähigkeit kompromittierte Hosts autorisieren, geschützte VMS auszuführen, einen Denial-of-Service-Angriff durch Entfernen wichtiger Materialien und vieles mehr zu initiieren.

Um dieses Risiko zu vermeiden, wird *dringend* empfohlen, die Überschneidung zwischen den Administratoren Ihrer HGS (einschließlich der Domäne, mit der HGS verknüpft ist) und Hyper-V-Umgebungen einzuschränken.
Wenn Sie sicherstellen, dass kein Administrator auf beide Systeme zugreifen kann, müsste ein Angreifer zwei verschiedene Konten von 2 Personen kompromittieren, um seine Aufgabe zum Ändern der HGS-Richtlinien abzuschließen.
Dies bedeutet auch, dass die Domänen-und Organisations-Administratoren für die beiden Active Directory Umgebungen nicht dieselbe Person sein sollten und dass HGS dieselbe Active Directory Gesamtstruktur wie Ihre Hyper-V-Hosts verwenden.
Jeder Benutzer, der sich selbst Zugriff auf Weitere Ressourcen gewähren kann, stellt ein Sicherheitsrisiko dar.

### <a name="using-just-enough-administration"></a>Verwendung von Just Enough Administration
HGS verfügt über [Just](https://aka.ms/JEAdocs) -in-Management-Rollen (Jea), die Sie bei der sicheren Verwaltung unterstützen.
Jea unterstützt Sie bei der Delegierung von Administrator Aufgaben an Benutzer ohne Administratorrechte, was bedeutet, dass die Personen, die HGS-Richtlinien verwalten, eigentlich nicht Administratoren des gesamten Computers oder der Domäne sein müssen.
Jea schränkt die Befehle ein, die ein Benutzer in einer PowerShell-Sitzung ausführen kann, und verwendet ein temporäres lokales Konto im Hintergrund (eindeutig für jede Benutzersitzung), um die Befehle auszuführen, die normalerweise eine Erhöhung erfordern.

In HGS werden zwei vorkonfigurierte Jea-Rollen bereitgestellt:
- **HGS-Administratoren** , die es Benutzern ermöglichen, alle HGS-Richtlinien zu verwalten, einschließlich der Autorisierungs Autorisierungs neuer Hosts zum Ausführen geschützter VMS.
- **HGS-Prüfer** , die nur Benutzern das Recht zum Überwachen vorhandener Richtlinien erlauben. Sie können keine Änderungen an der HGS-Konfiguration vornehmen.

Um Jea verwenden zu können, müssen Sie zunächst einen neuen Standardbenutzer erstellen und Sie zu einem Mitglied der Gruppe "HGS-Administratoren" oder "HGS-Prüfer" machen.
Wenn Sie `Install-HgsServer` verwendet haben, um eine neue Gesamtstruktur für HGS einzurichten, werden diese Gruppen "*Service Name*Administrators" und "*Service Name*Reviewer" genannt, wobei " *Service* Name" der Netzwerkname des HGS-Clusters ist.
Wenn Sie HGS zu einer vorhandenen Domäne hinzugefügt haben, sollten Sie auf die Gruppennamen verweisen, die Sie in `Initialize-HgsServer`angegeben haben.

**Erstellen von Standard Benutzern für die Rollen "HGS-Administrator" und "Reviewer"**

```powershell
$hgsServiceName = (Get-ClusterResource HgsClusterResource | Get-ClusterParameter DnsName).Value
$adminGroup = $hgsServiceName + "Administrators"
$reviewerGroup = $hgsServiceName + "Reviewers"

New-ADUser -Name 'hgsadmin01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Admin Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $adminGroup -Members 'hgsadmin01'

New-ADUser -Name 'hgsreviewer01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Reviewer Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $reviewerGroup -Members 'hgsreviewer01'
```

**Überwachen von Richtlinien mit der Reviewer-Rolle**

Führen Sie auf einem Remote Computer mit Netzwerk Konnektivität mit HGS die folgenden Befehle in PowerShell aus, um die Jea-Sitzung mit den Reviewer-Anmelde Informationen einzugeben.
Beachten Sie Folgendes: da das Reviewer-Konto nur ein Standardbenutzer ist, kann es nicht für reguläre Windows PowerShell-Remoting, Remotedesktop Zugriff auf HGS usw. verwendet werden.

```powershell
Enter-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsreviewer01' -ConfigurationName 'microsoft.windows.hgs'
```

Sie können dann überprüfen, welche Befehle in der Sitzung mit `Get-Command` zulässig sind, und alle zulässigen Befehle zum Überwachen der Konfiguration ausführen.
Im folgenden Beispiel überprüfen wir, welche Richtlinien auf HGS aktiviert sind.

```powershell
Get-Command

Get-HgsAttestationPolicy
```

Geben Sie den Befehl `Exit-PSSession` oder den zugehörigen Alias ein, `exit`, wenn Sie mit der Jea-Sitzung gearbeitet haben. 

**Hinzufügen einer neuen Richtlinie zu HGS mithilfe der Administrator Rolle**

Um eine Richtlinie tatsächlich zu ändern, müssen Sie eine Verbindung mit dem Jea-Endpunkt mit einer Identität herstellen, die zur Gruppe "hgsadministrators" gehört.
Im folgenden Beispiel wird gezeigt, wie Sie eine neue Code Integritätsrichtlinie in HGS kopieren und mit Jea registrieren können.
Die Syntax unterscheidet sich möglicherweise von ihrer Verwendung.
Dies dient dazu, einige der Einschränkungen in Jea zu erfüllen, wie z. b. keinen Zugriff auf das vollständige Dateisystem.

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

## <a name="monitoring-hgs"></a>Überwachen von HGS
### <a name="event-sources-and-forwarding"></a>Ereignis Quellen und Weiterleitung
Ereignisse von HGS werden im Windows-Ereignisprotokoll unter 2 Quellen angezeigt:
- **Hostguardianservice-Nachweis**
- **Hostguardianservice-keyprotection**

Sie können diese Ereignisse anzeigen, indem Sie Ereignisanzeige öffnen und zu "Microsoft-Windows-hostguardianservice-Attestation" und "Microsoft-Windows-hostguardianservice-keyprotection" navigieren.

In einer großen Umgebung ist es häufig vorzuziehen, Ereignisse an einen zentralen Windows-Ereignis Sammler weiterzuleiten, um die Analyse der Ereignisse zu vereinfachen.
Weitere Informationen finden Sie in der [Dokumentation zur Windows-Ereignis Weiterleitung](https://msdn.microsoft.com/library/windows/desktop/bb427443.aspx).

### <a name="using-system-center-operations-manager"></a>Verwenden von System Center Operations Manager
Sie können auch System Center 2016-Operations Manager verwenden, um HGS und die überwachten Hosts zu überwachen.
Der geschützte Fabric-Management Pack verfügt über Ereignis Monitore, die auf häufige Fehlkonfigurationen überprüfen können, die zu Ausfallzeiten von Rechenzentren führen können, einschließlich Hosts, die keine Nachrichten übergeben, und HGS-Server, die Fehler melden

[Installieren und konfigurieren Sie zunächst SCOM 2016](https://technet.microsoft.com/system-center-docs/om/welcome-to-operations-manager) , und [Laden Sie die geschützte Fabric-Management Pack herunter](https://www.microsoft.com/download/details.aspx?id=52764).
Das enthaltene Management Pack Handbuch erläutert, wie Sie die Management Pack konfigurieren und den Bereich Ihrer Monitore verstehen.

## <a name="backing-up-and-restoring-hgs"></a>Sichern und Wiederherstellen von HGS
### <a name="disaster-recovery-planning"></a>Planen der Notfall Wiederherstellung
Beim Entwerfen Ihrer Notfall Wiederherstellungs Pläne ist es wichtig, die besonderen Anforderungen des Host-Überwachungs Diensts in Ihrem geschützten Fabric zu beachten.
Wenn Sie einige oder alle ihrer HGS-Knoten verlieren, treten möglicherweise unmittelbare Verfügbarkeits Probleme auf, die verhindern, dass Benutzer ihre abgeschirmten VMs starten.
In einem Szenario, in dem Sie den gesamten HGS-Cluster verlieren, benötigen Sie vollständige Sicherungen der HGS-Konfiguration, um den HGS-Cluster wiederherstellen und den normalen Betrieb fortsetzen zu können.
In diesem Abschnitt werden die erforderlichen Schritte für die Vorbereitung eines solchen Szenarios beschrieben.

Zuerst ist es wichtig zu verstehen, welche Informationen zu HGS für die Sicherungskopie wichtig sind.
HGS behält verschiedene Informationen bei, mit denen ermittelt werden kann, welche Hosts zum Ausführen geschützter VMS autorisiert sind.
Dazu zählen:
1. Active Directory Sicherheits-IDs für die Gruppen mit vertrauenswürdigen Hosts (bei Verwendung Active Directory Attestation);
2. Eindeutige TPM-IDs für jeden Host in Ihrer Umgebung
3. TPM-Richtlinien für jede eindeutige Konfiguration des Hosts immer
4. Code Integritäts Richtlinien, die bestimmen, welche Software auf den Hosts ausgeführt werden darf.

Diese Nachweis Artefakte müssen mit den Administratoren Ihres hostingfabrics koordiniert werden, um diese Informationen nach einem Notfall wiederholen zu können.

Außerdem erfordert HGS Zugriff auf zwei oder mehr Zertifikate, die zum Verschlüsseln und Signieren der zum Starten einer abgeschirmten VM erforderlichen Informationen (die Schlüssel Schutzvorrichtung) benötigt werden.
Diese Zertifikate sind bekannt (von den Besitzern von abgeschirmten VMS verwendet, um Ihr Fabric zum Ausführen Ihrer virtuellen Computer zu autorisieren) und müssen nach einem Notfall wieder hergestellt werden, um eine nahtlose Wiederherstellung zu ermöglichen.
Wenn Sie HGS nicht mit denselben Zertifikaten nach einem Notfall wiederherstellen, muss jeder virtuelle Computer aktualisiert werden, um die neuen Schlüssel zum Entschlüsseln Ihrer Informationen zu autorisieren.
Aus Sicherheitsgründen kann nur der Besitzer des virtuellen Computers die VM-Konfiguration aktualisieren, um diese neuen Schlüssel zu autorisieren. Dies bedeutet, dass die Wiederherstellung Ihrer Schlüssel nach einem Notfall dazu führt, dass jeder VM-Besitzer Maßnahmen ergreifen muss, damit die virtuellen Computer erneut ausgeführt werden.

#### <a name="preparing-for-the-worst"></a>Vorbereitung auf die schlechteste
Um einen kompletten Verlust von HGS vorzubereiten, müssen Sie zwei Schritte ausführen:
1. Sichern der HGS-Nachweis Richtlinien
2. Sichern der HGS-Schlüssel

Anweisungen zum Ausführen dieser beiden Schritte finden Sie im Abschnitt [Sichern von HGS](#backing-up-hgs) .

Außerdem wird empfohlen, aber nicht erforderlich, dass Sie die Liste der Benutzer sichern, die zum Verwalten von HGS in der Active Directory Domäne oder Active Directory selbst autorisiert sind.

Sicherungen sollten regelmäßig ausgeführt werden, um sicherzustellen, dass die Informationen auf dem neuesten Stand sind und sicher gespeichert werden, um Manipulationen oder Diebstähle zu vermeiden.

Es wird **nicht empfohlen** , ein gesamtes System Abbild eines HGS-Knotens zu sichern oder wiederherzustellen.
Wenn Sie den gesamten Cluster verloren haben, besteht die bewährte Methode darin, einen neuen HGS-Knoten einzurichten und nur den HGS-Status und nicht das gesamte Server Betriebssystem wiederherzustellen.

#### <a name="recovering-from-the-loss-of-one-node"></a>Wiederherstellung nach dem Verlust eines Knotens
Wenn Sie einen oder mehrere Knoten (aber nicht jeden Knoten) in Ihrem HGS-Cluster verlieren, können Sie dem [Cluster einfach Knoten hinzufügen](guarded-fabric-configure-additional-hgs-nodes.md) , indem Sie die Anleitungen im Bereitstellungs Handbuch befolgen.
Die Nachweis Richtlinien werden automatisch synchronisiert, ebenso wie alle Zertifikate, die HGS als PFX-Dateien mit begleitenden Kenn Wörtern bereitgestellt wurden.
Für Zertifikate, die zu HGS mithilfe eines Fingerabdrucks (nicht exportierbar und Hardware gestützte Zertifikate, häufig) hinzugefügt werden, müssen Sie sicherstellen, dass jeder neue Knoten Zugriff auf den privaten Schlüssel jedes Zertifikats hat.

#### <a name="recovering-from-the-loss-of-the-entire-cluster"></a>Wiederherstellung nach dem Verlust des gesamten Clusters
Wenn der gesamte HGS-Cluster ausfällt und Sie nicht wieder online geschaltet werden können, müssen Sie HGS aus einer Sicherung wiederherstellen.
Das Wiederherstellen von HGS aus einer Sicherung umfasst zunächst das Einrichten eines neuen HGS-Clusters gemäß der [Anleitung im Bereitstellungs Handbuch](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).
Es wird dringend empfohlen, den gleichen Cluster Namen zu verwenden, wenn die Recovery-HGS-Umgebung eingerichtet wird, um die Namensauflösung von Hosts zu unterstützen.
Wenn Sie denselben Namen verwenden, müssen Sie die Hosts mit neuen Nachweis-und Schlüsselschutz-URLs nicht neu konfigurieren.
Wenn Sie Objekte in den Active Directory Domänen Sicherungs-HGS wieder hergestellt haben, wird empfohlen, vor dem Initialisieren des HGS-Servers die Objekte zu entfernen, die den HGS-Cluster, die Computer, das Dienst Konto und die Jea-Gruppen darstellen.

Nachdem Sie den ersten HGS-Knoten eingerichtet haben (z. b. installiert und initialisiert), befolgen Sie die Verfahren unter Wiederherstellen [von HGS aus einer Sicherung](#restoring-hgs-from-a-backup) , um die Nachweis Richtlinien und die öffentliche Hälfte der Schlüsselschutz Zertifikate wiederherzustellen.
Die privaten Schlüssel für Ihre Zertifikate müssen manuell gemäß der Anleitung Ihres Zertifikat Anbieters wieder hergestellt werden (z. b. Importieren des Zertifikats in Windows oder Konfigurieren des Zugriffs auf HSM-gestützte Zertifikate).
Nachdem Sie den ersten Knoten eingerichtet haben, können Sie weiterhin [zusätzliche Knoten auf dem Cluster installieren](guarded-fabric-configure-additional-hgs-nodes.md) , bis Sie die gewünschte Kapazität und Resilienz erreicht haben.

### <a name="backing-up-hgs"></a>Sichern von HGS
Der HGS-Administrator sollte in regelmäßigen Abständen für die Sicherung von HGS verantwortlich sein.
Eine komplette Sicherung enthält vertrauliche Schlüsselmaterial, die entsprechend gesichert werden müssen.
Sollte eine nicht vertrauenswürdige Entität Zugriff auf diese Schlüssel erhalten, können Sie diese Informationen verwenden, um eine bösartige HGS-Umgebung zum Zweck der Gefährdung von abgeschirmten VMS einzurichten.

**Sichern der Nachweis Richtlinien** Um die Richtlinien für den HGS-Nachweis zu sichern, führen Sie den folgenden Befehl auf einem beliebigen funktionierenden HGS-Server Knoten aus.
Sie werden aufgefordert, ein Kennwort anzugeben.
Dieses Kennwort wird zum Verschlüsseln aller Zertifikate verwendet, die zu HGS hinzugefügt werden, indem eine PFX-Datei (anstelle eines Zertifikat Fingerabdrucks) verwendet wird.

```powershell
Export-HgsServerState -Path C:\temp\HGSBackup.xml
```

> [!NOTE]
> Wenn Sie einen vom Administrator vertrauenswürdigen Nachweis verwenden, müssen Sie die Mitgliedschaft in den Sicherheitsgruppen, die von HGS zum Autorisieren von überwachten Hosts verwendet werden, separat sichern.
> HGS sichert nur die SID der Sicherheitsgruppen, nicht die darin enthaltenen Mitgliedschaften.
> Wenn diese Gruppen während eines Notfalls verloren gehen, müssen Sie die Gruppe (n) neu erstellen und jeden überwachten Host erneut hinzufügen.

**Sichern von Zertifikaten**

Der `Export-HgsServerState`-Befehl sichert alle PFX-basierten Zertifikate, die zu dem Zeitpunkt, zu dem der Befehl ausgeführt wird, den HGS hinzugefügt werden.
Wenn Sie HGS Zertifikate mithilfe eines Fingerabdrucks (typisch für nicht exportierbare und Hardware gestützte Zertifikate) hinzugefügt haben, müssen Sie die privaten Schlüssel für Ihre Zertifikate manuell sichern.
Um zu ermitteln, welche Zertifikate bei HGS registriert sind und manuell gesichert werden müssen, führen Sie den folgenden PowerShell-Befehl auf einem beliebigen funktionierenden HGS-Server Knoten aus.

```powershell
Get-HgsKeyProtectionCertificate | Where-Object { $_.CertificateData.GetType().Name -eq 'CertificateReference' } | Format-Table Thumbprint, @{ Label = 'Subject'; Expression = { $_.CertificateData.Certificate.Subject } }
```

Für jedes der aufgeführten Zertifikate müssen Sie den privaten Schlüssel manuell sichern.
Wenn Sie ein softwarebasiertes Zertifikat verwenden, das nicht exportierbar ist, wenden Sie sich an die Zertifizierungsstelle, um sicherzustellen, dass Sie über eine Sicherung Ihres Zertifikats verfügen, und/oder können Sie bei Bedarf neu ausstellen.
Bei Zertifikaten, die in Hardware Sicherheits Modulen erstellt und gespeichert werden, sollten Sie sich in der Dokumentation zu Ihrem Gerät über die Planung der Notfall Wiederherstellung informieren.

Sie sollten die Zertifikat Sicherungen zusammen mit den Nachweis Richtlinien Sicherungen an einem sicheren Ort speichern, damit beide Teile zusammen wieder hergestellt werden können.

**Zusätzliche Konfiguration für die Sicherungskopie**

Der gesicherte HGS-Serverstatus enthält nicht den Namen Ihres HGS-Clusters, Informationen aus Active Directory oder SSL-Zertifikate, die zum Sichern der Kommunikation mit den HGS-APIs verwendet werden.
Diese Einstellungen sind wichtig, um Konsistenz zu gewährleisten, aber nicht wichtig, um Ihren HGS-Cluster nach einem Notfall wieder online zu schalten.

Um den Namen des HGS-dienstanweises aufzuzeichnen, führen Sie `Get-HgsServer` aus, und notieren Sie sich den flachen Namen in den URLs für den Nachweis und den Schlüsselschutz.
Wenn die Nachweis-URL z. b. "<http://hgs.contoso.com/Attestation>" lautet, ist "HGS" der Name des HGS-dienstanweises.

Die von HGS verwendete Active Directory Domäne sollte wie jede andere Active Directory Domäne verwaltet werden.
Wenn Sie HGS nach einem Notfall wiederherstellen, müssen Sie nicht unbedingt die exakten Objekte neu erstellen, die in der aktuellen Domäne vorhanden sind.
Allerdings wird die Wiederherstellung vereinfacht, wenn Sie Active Directory sichern und eine Liste der Jea-Benutzer, die zur Verwaltung des Systems autorisiert sind, sowie die Mitgliedschaft von Sicherheitsgruppen, die vom Administrator vertrauenswürdigen Nachweis verwendet werden, zum Autorisieren von überwachten Hosts erhalten.

Führen Sie den folgenden Befehl in PowerShell aus, um den Fingerabdruck der SSL-Zertifikate zu identifizieren, die für HGS konfiguriert sind.
Anschließend können Sie die SSL-Zertifikate gemäß den Anweisungen Ihres Zertifikat Anbieters sichern.

```powershell
Get-WebBinding -Protocol https | Select-Object certificateHash
```

### <a name="restoring-hgs-from-a-backup"></a>Wiederherstellen von HGS aus einer Sicherung
In den folgenden Schritten wird beschrieben, wie Sie die HGS-Einstellungen aus einer Sicherung wiederherstellen.
Die Schritte sind für beide Situationen relevant, in denen Sie versuchen, Änderungen an Ihren bereits vorhandenen HGS-Instanzen rückgängig zu machen, und wenn Sie nach einem vollständigen Verlust der vorherigen Instanz einen neuen HGS-Cluster einrichten.

#### <a name="set-up-a-replacement-hgs-cluster"></a>Einrichten eines Ersetzungs-HGS-Clusters
Bevor Sie HGS wiederherstellen können, benötigen Sie einen initialisierten HGS-Cluster, auf dem Sie die Konfiguration wiederherstellen können.
Wenn Sie einfach Einstellungen importieren, die versehentlich in einen vorhandenen (laufenden) Cluster gelöscht wurden, können Sie diesen Schritt überspringen.
Wenn Sie nach einem kompletten Verlust von HGS wiederherstellen, müssen Sie mindestens einen HGS-Knoten installieren und initialisieren, indem Sie die [Anweisungen im Bereitstellungs Handbuch](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)befolgen.

Insbesondere müssen Sie die folgenden Schritte ausführen:
1. [Einrichten der HGS-Domäne](guarded-fabric-choose-where-to-install-hgs.md) oder einbinden von HGS in eine vorhandene Domäne
2. [Initialisieren Sie den HGS-Server](guarded-fabric-initialize-hgs.md) mit Ihren vorhandenen Schlüsseln *oder* einem Satz von temporären Schlüsseln. Sie können [die temporären Schlüssel](#renewing-or-replacing-keys) nach dem Importieren Ihrer eigentlichen Schlüssel aus den HGS-Sicherungsdateien entfernen.
3. [Importieren Sie die HGS-Einstellungen](#import-settings-from-a-backup) aus der Sicherung, um die vertrauenswürdigen Host Gruppen, Code Integritäts Richtlinien, TPM-Baselines und TPM-IDs wiederherzustellen.

> [!TIP]
> Der neue HGS-Cluster muss nicht die gleichen Zertifikate, den gleichen Dienstnamen oder die gleiche Domäne wie die HGS-Instanz verwenden, von der aus die Sicherungsdatei exportiert wurde.

#### <a name="import-settings-from-a-backup"></a>Importieren von Einstellungen aus einer Sicherung

Führen Sie den folgenden Befehl auf einem initialisierten HGS-Server Knoten aus, um Nachweis Richtlinien, PFX-basierte Zertifikate und die öffentlichen Schlüssel von nicht-PFX-Zertifikaten auf Ihrem HGS-Knoten aus einer Sicherungsdatei wiederherzustellen.
Sie werden aufgefordert, das Kennwort einzugeben, das Sie beim Erstellen der Sicherung angegeben haben.

```powershell
Import-HgsServerState -Path C:\Temp\HGSBackup.xml
```

Wenn Sie nur admin-Trusted Nachweis-Richtlinien oder TPM-vertrauenswürdige Nachweis Richtlinien importieren möchten, können Sie dazu die `-ImportActiveDirectoryModeState` oder `-ImportTpmModeState` Flags für [Import-hgsserverstate](https://technet.microsoft.com/library/mt652168.aspx)angeben.

Stellen Sie sicher, dass das neueste kumulative Update für Windows Server 2016 installiert ist, bevor Sie `Import-HgsServerState`ausführen.
Wenn dies nicht der Fall ist, kann ein Import Fehler auftreten.

> [!NOTE]
> Wenn Sie Richtlinien auf einem vorhandenen HGS-Knoten wiederherstellen, auf dem bereits eine oder mehrere dieser Richtlinien installiert sind, wird im Import Befehl ein Fehler für jede doppelte Richtlinie angezeigt.
> Dies ist ein erwartetes Verhalten und kann in den meisten Fällen problemlos ignoriert werden.

#### <a name="reinstall-private-keys-for-certificates"></a>Neuinstallation privater Schlüssel für Zertifikate
Wenn eines der Zertifikate, die auf dem HGS verwendet werden, von dem die Sicherung erstellt wurde, mithilfe von Fingerabdrücken hinzugefügt wurde, wird nur der öffentliche Schlüssel dieser Zertifikate in die Sicherungsdatei eingeschlossen.
Dies bedeutet, dass Sie für jedes dieser Zertifikate manuell installieren und/oder Zugriff auf die privaten Schlüssel gewähren müssen, bevor HGS Anforderungen von Hyper-V-Hosts bedienen kann.
Welche Aktionen zum Durchführen dieses Schritts erforderlich sind, hängt davon ab, wie das Zertifikat ursprünglich ausgestellt wurde.
Bei softwaregestützten Zertifikaten, die von einer Zertifizierungsstelle ausgestellt werden, müssen Sie sich an Ihre Zertifizierungsstelle wenden, um den privaten Schlüssel zu erhalten und auf **jedem** HGS-Knoten gemäß Ihren Anweisungen zu installieren.
Wenn Ihre Zertifikate auf Hardware basieren, müssen Sie auch die Dokumentation Ihres Hardware Sicherheitsmodul-Herstellers aufrufen, um die erforderlichen Treiber auf den einzelnen HGS-Knoten zu installieren, um eine Verbindung mit dem HSM herzustellen und jedem Computer Zugriff auf den privaten Schlüssel zu gewähren.

Zur Erinnerung: Zertifikate, die HGS mithilfe von Fingerabdrücken hinzugefügt werden, erfordern eine manuelle Replikation der privaten Schlüssel für jeden Knoten.
Sie müssen diesen Schritt auf jedem zusätzlichen Knoten wiederholen, den Sie dem wiederhergestellten HGS-Cluster hinzufügen.

#### <a name="review-imported-attestation-policies"></a>Überprüfen der importierten Nachweis Richtlinien
Nachdem Sie die Einstellungen aus einer Sicherung importiert haben, wird empfohlen, alle importierten Richtlinien mithilfe von `Get-HgsAttestationPolicy` genau zu überprüfen, um sicherzustellen, dass nur die Hosts, denen Sie Vertrauen, dass Sie abgeschirmte VMS ausführen, erfolgreich bestätigt werden können.
Wenn Sie Richtlinien finden, die nicht mehr dem Sicherheitsstatus entsprechen, können Sie [diese deaktivieren oder entfernen](#review-attestation-policies).

#### <a name="run-diagnostics-to-check-system-state"></a>Ausführen der Diagnose zum Überprüfen des Systemstatus
Nachdem Sie die Einrichtung und Wiederherstellung des Status des HGS-Knotens abgeschlossen haben, sollten Sie das HGS-Diagnosetool ausführen, um den Status des Systems zu überprüfen.
Führen Sie hierzu den folgenden Befehl auf dem HGS-Knoten aus, auf dem Sie die Konfiguration wieder hergestellt haben:

```powershell
Get-HgsTrace -RunDiagnostics
```

Wenn das "Gesamtergebnis" nicht "Pass" ist, sind zusätzliche Schritte erforderlich, um die Konfiguration des Systems abzuschließen.
Überprüfen Sie die in den untertests gemeldeten Meldungen, bei denen weitere Informationen aufgetreten sind.

## <a name="patching-hgs"></a>Patching von HGS
Es ist wichtig, die Knoten des Host-Überwachungs Diensts auf dem neuesten Stand zu halten, indem Sie das aktuellste kumulative Update installieren. Wenn Sie einen neuen HGS-Knoten einrichten, wird dringend empfohlen, dass Sie alle verfügbaren Updates installieren, bevor Sie die HGS-Rolle installieren oder konfigurieren.
Dadurch wird sichergestellt, dass neue oder geänderte Funktionen sofort wirksam werden.

Beim Patchen ihres geschützten Fabrics wird dringend empfohlen, zuerst *alle* Hyper-V-Hosts **vor dem Upgrade von HGS**zu aktualisieren.
Dadurch wird sichergestellt, dass alle Änderungen an den Nachweis Richtlinien auf den HGS vorgenommen werden, *nachdem* die Hyper-V-Hosts aktualisiert wurden, um die für Sie erforderlichen Informationen bereitzustellen.
Wenn das Verhalten von Richtlinien durch ein Update geändert wird, werden Sie nicht automatisch aktiviert, um die Unterbrechung Ihres Fabrics zu vermeiden.
Diese Updates erfordern, dass Sie die Anweisungen im folgenden Abschnitt befolgen, um die neuen oder geänderten Nachweis Richtlinien zu aktivieren.
Wir empfehlen Ihnen, die Anmerkungen zu dieser Version für Windows Server und alle kumulativen Updates zu lesen, die Sie installieren, um zu prüfen, ob die Richtlinien Updates erforderlich sind.

### <a name="updates-requiring-policy-activation"></a>Updates, die die Richtlinien Aktivierung erfordern
Wenn ein Update für HGS das Verhalten einer Nachweis Richtlinie einführt oder erheblich ändert, ist ein zusätzlicher Schritt erforderlich, um die geänderte Richtlinie zu aktivieren.
Richtlinien Änderungen werden nur nach dem Exportieren und Importieren des HGS-Zustands festgesetzt.
Sie sollten nur die neuen oder geänderten Richtlinien aktivieren, nachdem Sie das kumulative Update auf alle Hosts und alle HGS-Knoten in Ihrer Umgebung angewendet haben.
Nachdem jeder Computer aktualisiert wurde, führen Sie die folgenden Befehle auf einem beliebigen HGS-Knoten aus, um den Upgradevorgang zu initiieren:

```powershell
$password = Read-Host -AsSecureString -Prompt "Enter a temporary password"
Export-HgsServerState -Path .\temporaryExport.xml -Password $password
Import-HgsServerState -Path .\temporaryExport.xml -Password $password
```

Wenn eine neue Richtlinie eingeführt wurde, wird Sie standardmäßig deaktiviert.
Um die neue Richtlinie zu aktivieren, suchen Sie Sie zuerst in der Liste der Microsoft-Richtlinien (mit dem Präfix "HGS_"), und aktivieren Sie Sie dann mit den folgenden Befehlen:

```powershell
Get-HgsAttestationPolicy

Enable-HgsAttestationPolicy -Name <Hgs_NewPolicyName>
```

## <a name="managing-attestation-policies"></a>Verwalten von Nachweis Richtlinien
HGS verwaltet mehrere Nachweis Richtlinien, die die Mindestanzahl von Anforderungen definieren, die ein Host erfüllen muss, um als "fehlerfrei" eingestuft zu werden, und für die das Ausführen von abgeschirmten VMS zugelassen ist.
Einige dieser Richtlinien werden von Microsoft definiert, andere werden von Ihnen hinzugefügt, um die zulässigen Code Integritäts Richtlinien, TPM-Baselines und Hosts in Ihrer Umgebung zu definieren.
Eine regelmäßige Wartung dieser Richtlinien ist erforderlich, um sicherzustellen, dass Hosts beim Aktualisieren und ersetzen weiterhin ordnungsgemäß getestet werden können, und um sicherzustellen, dass nicht vertrauenswürdige Hosts oder Konfigurationen nicht erfolgreich getestet werden können.

Für den Administrator vertrauenswürdigen Nachweis gibt es nur eine Richtlinie, die bestimmt, ob ein Host fehlerfrei ist: Mitgliedschaft in einer bekannten, vertrauenswürdigen Sicherheitsgruppe.
Der TPM-Nachweis ist komplizierter und umfasst verschiedene Richtlinien, mit denen der Code und die Konfiguration eines Systems gemessen werden können, bevor festgestellt wird, ob es fehlerfrei ist.

Ein einzelner HGS kann gleichzeitig mit Active Directory-und TPM-Richtlinien konfiguriert werden, aber der Dienst überprüft nur die Richtlinien für den aktuellen Modus, für den er konfiguriert ist, wenn ein Host versucht, die Tests zu testen.
Führen Sie `Get-HgsServer`aus, um den Modus des HGS-Servers zu überprüfen.

### <a name="default-policies"></a>Standardrichtlinien
Für den TPM-vertrauenswürdigen Nachweis gibt es mehrere integrierte Richtlinien, die auf HGS konfiguriert sind.
Einige dieser Richtlinien sind "gesperrt", was bedeutet, dass Sie aus Sicherheitsgründen nicht deaktiviert werden können.
In der folgenden Tabelle wird der Zweck jeder Standard Richtlinie erläutert.

Richtlinienname                    | Zweck
-------------------------------|-----------------------------------------------------
Hgs_SecureBootEnabled          | Erfordert, dass für Hosts der sichere Start aktiviert ist. Dies ist erforderlich, um die Start Binärdateien und andere UEFI-Locked-Einstellungen zu messen.
Hgs_UefiDebugDisabled          | Stellt sicher, dass für Hosts kein Kernel Debugger aktiviert ist. Benutzermodus-debuggger werden mit Code Integritäts Richtlinien blockiert.
Hgs_SecureBootSettings         | Negative Richtlinie, um sicherzustellen, dass die Hosts mindestens einer (vom Administrator definierten) TPM-Baseline entsprechen.
Hgs_CiPolicy                   | Negative Richtlinie, um sicherzustellen, dass die Hosts eine der Administrator definierten CI-Richtlinien verwenden.
Hgs_HypervisorEnforcedCiPolicy | Erfordert, dass die Code Integritätsrichtlinie vom Hypervisor erzwungen wird. Wenn Sie diese Richtlinie deaktivieren, wird der Schutz vor kernelmodusintegritäts-Richtlinien Angriffen geschwächt.
Hgs_FullBoot                   | Sicherstellen, dass der Host nicht aus dem Standbymodus oder Ruhezustand fortgesetzt wurde Hosts müssen ordnungsgemäß neu gestartet oder heruntergefahren werden, um diese Richtlinie zu übergeben.
Hgs_VsmIdkPresent              | Erfordert, dass virtualisierungsbasierte Sicherheit auf dem Host ausgeführt wird. Das idk stellt den Schlüssel dar, der zum Verschlüsseln von Informationen erforderlich ist, die zurück an den sicheren Speicherbereich des Hosts gesendet werden.
Hgs_PageFileEncryptionEnabled  | Erfordert, dass Auslagerungs Dateien auf dem Host verschlüsselt wird. Wenn Sie diese Richtlinie deaktivieren, kann es zu Informations Informationen kommen, wenn eine unverschlüsselte ausseitendatei auf Mandanten Geheimnisse überprüft wird.
Hgs_BitLockerEnabled           | Erfordert, dass BitLocker auf dem Hyper-V-Host aktiviert ist. Diese Richtlinie ist aus Leistungsgründen standardmäßig deaktiviert und wird nicht empfohlen, Sie zu aktivieren. Diese Richtlinie hat keine Auswirkungen auf die Verschlüsselung der abgeschirmten VMs selbst.
Hgs_IommuEnabled               | Erfordert, dass der Host über ein IOMMU-Gerät verfügt, das verwendet wird, um Angriffe durch direkten Speicherzugriff zu verhindern. Wenn Sie diese Richtlinie deaktivieren und Hosts ohne IOMMU-Aktivierung verwenden, können Sie Mandanten-VM-Schlüssel für direkte Speicher Angriffe verfügbar machen.
Hgs_NoHibernation              | Erfordert, dass der Ruhezustand auf dem Hyper-V-Host deaktiviert wird. Durch die Deaktivierung dieser Richtlinie können Hosts den geschützten VM-Speicher in einer unverschlüsselten Ruhe Zustands Datei speichern.
Hgs_NoDumps                    | Erfordert, dass Speicher Abbilder auf dem Hyper-V-Host deaktiviert werden. Wenn Sie diese Richtlinie deaktivieren, empfiehlt es sich, die dumpverschlüsselung zu konfigurieren, um zu verhindern, dass geschützter VM-Speicher in unverschlüsselten Absturz Abbild Dateien gespeichert wird.
Hgs_DumpEncryption             | Erfordert, dass Speicher Abbilder, die auf dem Hyper-V-Host aktiviert sind, mit einem Verschlüsselungsschlüssel verschlüsselt werden, der von HGS als vertrauenswürdig eingestuft wird. Diese Richtlinie gilt nicht, wenn Abbilder auf dem Host nicht aktiviert sind. Wenn diese Richtlinie und *HGS\_nodumps* deaktiviert sind, kann der geschützte VM-Speicher in einer unverschlüsselten Dumpdatei gespeichert werden.
Hgs_DumpEncryptionKey          | Eine negative Richtlinie zum sicherstellen, dass Hosts, die für das Zulassen von Speicher Abbildern konfiguriert sind, einen vom Administrator definierten Verschlüsselungsschlüssel für die Dumpdatei verwendet Diese Richtlinie gilt nicht, wenn *HGS\_dumpencryption* deaktiviert ist.

### <a name="authorizing-new-guarded-hosts"></a>Autorialisieren von neuen überwachten Hosts
Um einen neuen Host zu einem überwachten Host zu autorisieren (z. b. erfolgreich), müssen die HGS dem Host Vertrauen und (bei Konfiguration für die Verwendung des TPM-vertrauenswürdigen Attestation) die darauf laufende Software als vertrauenswürdig einstufen.
Die Schritte zum Autorisieren eines neuen Hosts unterscheiden sich je nach Nachweis Modus, für den HGS derzeit konfiguriert ist.
Führen Sie `Get-HgsServer` auf einem beliebigen HGS-Knoten aus, um den Nachweis Modus für Ihr überwachtes Fabric zu überprüfen.

#### <a name="software-configuration"></a>Softwarekonfiguration
Stellen Sie auf dem neuen Hyper-V-Host sicher, dass Windows Server 2016 Datacenter Edition installiert ist.
Windows Server 2016 Standard kann keine abgeschirmten VMs in einem geschützten Fabric ausführen.
Auf dem Host ist möglicherweise Desktop Darstellung oder Server Core installiert.

Auf dem Server mit Desktop Darstellung und Server Core müssen Sie die Hyper-v-und Host-Überwachungs Server-Hyper-v-Unterstützungs Server Rollen installieren:

```powershell
Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
```

#### <a name="admin-trusted-attestation"></a>Admin-vertrauenswürdiger Nachweis
Wenn Sie einen neuen Host bei der Verwendung von Administrator vertrauenswürdigem Nachweis in HGS registrieren möchten, müssen Sie ihn zunächst zu einer Sicherheitsgruppe in der Domäne hinzufügen, mit der er verknüpft ist.
In der Regel verfügt jede Domäne über eine Sicherheitsgruppe für geschützte Hosts.
Wenn Sie diese Gruppe bereits bei HGS registriert haben, müssen Sie nur den Host neu starten, um die Gruppenmitgliedschaft zu aktualisieren.

Sie können überprüfen, welche Sicherheitsgruppen von HGS als vertrauenswürdig eingestuft werden, indem Sie den folgenden Befehl ausführen:

```powershell
Get-HgsAttestationHostGroup
```

Zum Registrieren einer neuen Sicherheitsgruppe bei HGS erfassen Sie zuerst die Sicherheits-ID (SID) der Gruppe in der Host Domäne und registrieren die SID bei HGS.

```powershell
Add-HgsAttestationHostGroup -Name "Contoso Guarded Hosts" -Identifier "S-1-5-21-3623811015-3361044348-30300820-1013"
```

Anweisungen zum Einrichten der Vertrauensstellung zwischen der Host Domäne und den HGS finden Sie im Bereitstellungs Handbuch.

#### <a name="tpm-trusted-attestation"></a>TPM-vertrauenswürdiger Nachweis
Wenn HGS im TPM-Modus konfiguriert ist, müssen Hosts alle gesperrten Richtlinien und aktivierten Richtlinien, die mit dem Präfix "Hgs_" als Präfix versehen sind, sowie mindestens eine TPM-Baseline, TPM-ID und Code Integritätsrichtlinie übergeben.
Jedes Mal, wenn Sie einen neuen Host hinzufügen, müssen Sie die neue TPM-ID bei HGS registrieren.
Solange der Host dieselbe Software (und die gleiche Code Integritätsrichtlinie angewendet) und die TPM-Baseline als einen anderen Host in Ihrer Umgebung ausführen, müssen Sie keine neuen CI-Richtlinien oder Basis Linien hinzufügen.

**Hinzufügen des TPM-Bezeichners für einen neuen Host** Führen Sie auf dem neuen Host den folgenden Befehl aus, um den TPM-Bezeichner zu erfassen.
Stellen Sie sicher, dass Sie einen eindeutigen Namen für den Host angeben, der Sie bei der Suche nach HGS unterstützt.
Sie benötigen diese Informationen, wenn Sie den Host außer Betrieb nehmen oder verhindern möchten, dass abgeschirmte VMs in HGS ausgeführt werden.

```powershell
(Get-PlatformIdentifier -Name "Host01").InnerXml | Out-File C:\temp\host01.xml -Encoding UTF8
```

Kopieren Sie diese Datei auf Ihren HGS-Server, und führen Sie dann den folgenden Befehl aus, um den Host bei HGS zu registrieren.

```powershell
Add-HgsAttestationTpmHost -Name 'Host01' -Path C:\temp\host01.xml
```

**Hinzufügen einer neuen TPM-Baseline** Wenn auf dem neuen Host eine neue Hardware-oder Firmwarekonfiguration für Ihre Umgebung ausgeführt wird, müssen Sie möglicherweise eine neue TPM-Baseline erstellen.
Führen Sie hierzu den folgenden Befehl auf dem Host aus.

```powershell
Get-HgsAttestationBaselinePolicy -Path 'C:\temp\hardwareConfig01.tcglog'
```

> [!NOTE]
> Wenn Sie eine Fehlermeldung erhalten, die besagt, dass der Host die Überprüfung nicht erfolgreich war
> Dies ist eine Voraussetzungs Prüfung, um sicherzustellen, dass der Host abgeschirmte VMS ausführen kann. Dies bedeutet wahrscheinlich, dass Sie noch keine Code Integritätsrichtlinie oder andere erforderliche Einstellungen angewendet haben.
> Lesen Sie die Fehlermeldung, nehmen Sie die von ihr vorgeschlagenen Änderungen vor, und wiederholen Sie dann den Vorgang.
> Alternativ können Sie die Überprüfung zu diesem Zeitpunkt überspringen, indem Sie dem Befehl das `-SkipValidation`-Flag hinzufügen.

Kopieren Sie die TPM-Baseline auf Ihren HGS-Server, und registrieren Sie Sie mit dem folgenden Befehl.
Wir empfehlen Ihnen, eine Benennungs Konvention zu verwenden, die Ihnen hilft, die Hardware-und Firmwarekonfiguration dieser Klasse von Hyper-V-Hosts zu verstehen.

```powershell
Add-HgsAttestationTpmPolicy -Name 'HardwareConfig01' -Path 'C:\temp\hardwareConfig01.tcglog'
```

**Hinzufügen einer neuen Code Integritätsrichtlinie** Wenn Sie die Code Integritätsrichtlinie geändert haben, die auf Ihren Hyper-V-Hosts ausgeführt wird, müssen Sie die neue Richtlinie mit HGS registrieren, damit diese Hosts erfolgreich bestätigen können.
Erfassen Sie auf einem Referenz Host, der als Master Abbild für die vertrauenswürdigen Hyper-V-Computer in Ihrer Umgebung fungiert, mithilfe des Befehls `New-CIPolicy` eine neue CI-Richtlinie.
Wir empfehlen Ihnen, die **filepublisher** -Ebene und den **hashback** für Hyper-V-Host-CI-Richtlinien zu verwenden.
Erstellen Sie zunächst eine CI-Richtlinie im Überwachungsmodus, um sicherzustellen, dass alles wie erwartet funktioniert.
Nachdem Sie eine Beispiel Arbeitsauslastung im System überprüft haben, können Sie die Richtlinie erzwingen und die erzwungene Version in HGS kopieren.
Eine umfassende Liste der Konfigurationsoptionen für die Code Integritätsrichtlinie finden Sie in der [Device Guard-Dokumentation](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies).

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

Nachdem Sie die Richtlinie erstellt, getestet und erzwungen haben, kopieren Sie die Binärdatei (. p7b) auf Ihren HGS-Server, und registrieren Sie die Richtlinie.

```powershell
Add-HgsAttestationCiPolicy -Name 'WS2016-Hardware01' -Path 'C:\temp\ws2016-hardware01-ci.p7b'
```

**Hinzufügen eines Verschlüsselungsschlüssels für den Speicher Abbild**

Wenn die *HGS\_nodumps* -Richtlinie deaktiviert ist und *HGS\_dumpencryption* -Richtlinie aktiviert ist, dürfen geschützte Hosts Speicher Abbilder (einschließlich Absturz Abbilder) aktivieren, damit Sie aktiviert werden, solange diese Abbilder verschlüsselt werden. Geschützte Hosts bestehen nur dann, wenn Sie entweder Speicher Abbilder deaktiviert haben oder Sie mit einem Schlüssel verschlüsseln, der HGS bekannt ist. Standardmäßig werden keine dumpverschlüsselungs Schlüssel auf HGS konfiguriert.

Verwenden Sie das Cmdlet "`Add-HgsAttestationDumpPolicy`", um HGS den Hashwert Ihres dumpverschlüsselungs Schlüssels hinzuzufügen.
Wenn Sie eine TPM-Baseline auf einem Hyper-V-Host erfassen, der mit der dumpverschlüsselung konfiguriert ist, wird der Hash in tcglog eingeschlossen und kann für das Cmdlet "`Add-HgsAttestationDumpPolicy`" bereitgestellt werden.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey01' -Path 'C:\temp\TpmBaselineWithDumpEncryptionKey.tcglog'
```

Alternativ können Sie die Zeichen folgen Darstellung des Hashs direkt für das Cmdlet bereitstellen.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey02' -PublicKeyHash '<paste your hash here>'
```

Stellen Sie sicher, dass Sie jeden eindeutigen Verschlüsselungsschlüssel für die Verschlüsselung zu HGS hinzufügen, wenn Sie sich für die Verwendung verschiedener Schlüssel in Ihrem geschützten Fabric entscheiden.
Hosts, die Speicher Abbilder mit einem Schlüssel verschlüsseln, der HGS nicht bekannt ist, erhalten keinen Nachweis.

Weitere Informationen zum [Konfigurieren der dumpverschlüsselung auf Hosts finden Sie in](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)der Hyper-V-Dokumentation.

#### <a name="check-if-the-system-passed-attestation"></a>Überprüfen, ob das System den Nachweis überschritten hat
Nachdem Sie die erforderlichen Informationen bei HGS registriert haben, sollten Sie überprüfen, ob der Host den Nachweis übergibt.
Führen Sie auf dem neu hinzugefügten Hyper-V-Host `Set-HgsClientConfiguration` aus, und geben Sie die richtigen URLs für Ihren HGS-Cluster an.
Diese URLs können abgerufen werden, indem `Get-HgsServer` auf einem beliebigen HGS-Knoten ausgeführt wird.

```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'http://hgs.bastion.local/KeyProtection' -AttestationServerUrl 'http://hgs.bastion.local/Attestation'
```

Wenn der resultierende Status nicht "ishostbewacht: true" angibt, müssen Sie die Problembehandlung für die Konfiguration durchführen.
Führen Sie auf dem Host, bei dem ein Fehler aufgetreten ist, den folgenden Befehl aus, um einen ausführlichen Bericht zu Problemen zu erhalten, die Ihnen helfen können, den fehlgeschlagenen Nachweis zu beheben.

```powershell
Get-HgsTrace -RunDiagnostics -Detailed
```

> [!IMPORTANT]
> Wenn Sie Windows Server 2019 oder Windows 10, Version 1809, verwenden und Code Integritäts Richtlinien verwenden, wird `Get-HgsTrace` möglicherweise einen Fehler für die aktive Diagnose der **Code Integritätsrichtlinie** zurückgeben.
> Sie können dieses Ergebnis gefahrlos ignorieren, wenn es die einzige Fehlerdiagnose ist.

### <a name="review-attestation-policies"></a>Nachweis Richtlinien prüfen
Um den aktuellen Status der auf HGS konfigurierten Richtlinien zu überprüfen, führen Sie die folgenden Befehle auf einem beliebigen HGS-Knoten aus:

```powershell
# List all trusted security groups for admin-trusted attestation
Get-HgsAttestationHostGroup

# List all policies configured for TPM-trusted attestation
Get-HgsAttestationPolicy
```

Wenn Sie feststellen, dass eine aktivierte Richtlinie nicht mehr Ihren Sicherheitsanforderungen entspricht (z. b. eine alte Code Integritätsrichtlinie, die jetzt als unsicher eingestuft wird), können Sie diese deaktivieren, indem Sie den Namen der Richtlinie im folgenden Befehl ersetzen:

```powershell
Disable-HgsAttestationPolicy -Name 'PolicyName'
```

Auf ähnliche Weise können Sie `Enable-HgsAttestationPolicy` verwenden, um eine Richtlinie erneut zu aktivieren.

Wenn Sie eine Richtlinie nicht mehr benötigen und Sie von allen HGS-Knoten entfernen möchten, führen Sie `Remove-HgsAttestationPolicy -Name 'PolicyName'` aus, um die Richtlinie dauerhaft zu löschen.

## <a name="changing-attestation-modes"></a>Ändern der Nachweis Modi
Wenn Sie Ihr überwachtes Fabric mit einem vom Administrator vertrauenswürdigen Nachweis gestartet haben, möchten Sie wahrscheinlich ein Upgrade auf den weitaus stärkeren TPM-Nachweis Modus durchführen, sobald Sie über genügend TPM 2,0-kompatible Hosts in Ihrer Umgebung verfügen.
Wenn Sie bereit sind, zu wechseln, können Sie alle Nachweis Artefakte (CI-Richtlinien, TPM-Basis Linien und TPM-IDs) in HGS vorab laden, während Sie weiterhin HGS mit dem Administrator vertrauenswürdigen Nachweis ausführen.
Befolgen Sie hierzu einfach die Anweisungen im Abschnitt [autorisierender neuer](#authorizing-new-guarded-hosts) überwachter Hosts.

Nachdem Sie alle Ihre Richtlinien zu HGS hinzugefügt haben, besteht der nächste Schritt darin, einen synthetischen Nachweis Versuch auf Ihren Hosts auszuführen, um zu überprüfen, ob Sie den Nachweis im TPM-Modus bestanden haben.
Dies wirkt sich nicht auf den aktuellen Betriebsstatus von HGS aus.
Die folgenden Befehle müssen auf einem Computer ausgeführt werden, der Zugriff auf alle Hosts in der Umgebung und mindestens einen HGS-Knoten hat.
Wenn die Firewall oder andere Sicherheitsrichtlinien dies verhindern, können Sie diesen Schritt überspringen.
Nach Möglichkeit empfiehlt es sich, den synthetischen Nachweis durchführen, um einen guten Hinweis darauf zu erhalten, ob das "Kippen" in den TPM-Modus Ausfallzeiten für Ihre virtuellen Computer verursacht. 

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

Überprüfen Sie nach Abschluss der Diagnose die ausgegebenen Informationen, um zu ermitteln, ob bei einem der Hosts im TPM-Modus ein Fehler aufgetreten ist.
Führen Sie die Diagnose erneut aus, bis Sie von jedem Host einen "Pass" erhalten, und wechseln Sie dann zum Ändern von HGS in den TPM-Modus.

Das **Ändern in den TPM-Modus** dauert nur eine Sekunde.
Führen Sie den folgenden Befehl auf einem beliebigen HGS-Knoten aus, um den Nachweis Modus zu aktualisieren.

```powershell
Set-HgsServer -TrustTpm
```

Wenn Probleme auftreten und Sie zurück in den Active Directory-Modus wechseln müssen, können Sie dazu `Set-HgsServer -TrustActiveDirectory`ausführen.

Nachdem Sie bestätigt haben, dass alles wie erwartet funktioniert, sollten Sie alle vertrauenswürdigen Active Directory Host Gruppen aus HGS entfernen und die Vertrauensstellung zwischen den HGS-und Fabric-Domänen entfernen.
Wenn Sie die Active Directory Vertrauensstellung aktiviert haben, riskieren Sie, dass jemand die Vertrauensstellung erneut aktiviert und die HGS in Active Directory Modus wechselt. Dadurch kann nicht vertrauenswürdiger Code auf den überwachten Hosts deaktiviert werden.

## <a name="key-management"></a>Schlüsselverwaltung
Die geschützte Fabric-Lösung verwendet mehrere öffentliche/private Schlüsselpaare zum Überprüfen der Integrität der verschiedenen Komponenten in der Lösung und zum Verschlüsseln von Mandanten Geheimnissen.
Der Host-Überwachungsdienst ist mit mindestens zwei Zertifikaten (mit öffentlichen und privaten Schlüsseln) konfiguriert, die zum Signieren und Verschlüsseln der Schlüssel verwendet werden, die zum Starten von abgeschirmten VMS verwendet werden.
Diese Schlüssel müssen sorgfältig verwaltet werden.
Wenn der private Schlüssel von einem Angreifer abgerufen wird, kann er alle virtuellen Computer, die in Ihrem Fabric ausgeführt werden, aufheben oder einen dort stünden-HGS-Cluster einrichten, der schwächere Nachweis Richtlinien verwendet, um die von Ihnen eingerichteten Schutzmaßnahmen zu umgehen.
Wenn Sie die privaten Schlüssel während eines Notfalls verlieren und nicht in einer Sicherung finden, müssen Sie ein neues Schlüsselpaar einrichten und jeden virtuellen Computer neu anordnen, um die neuen Zertifikate zu autorisieren.

In diesem Abschnitt werden die allgemeinen Schlüssel Verwaltungs Themen behandelt, mit denen Sie Ihre Schlüssel so konfigurieren können, dass Sie funktionsfähig und sicher sind.

### <a name="adding-new-keys"></a>Neue Schlüssel werden hinzugefügt
Obwohl HGS mit einem Satz von Schlüsseln initialisiert werden müssen, können Sie den HGS mehrere Verschlüsselungs-und Signatur Schlüssel hinzufügen.
Die zwei häufigsten Gründe dafür, dass Sie HGS neue Schlüssel hinzufügen würden:
1. Zur Unterstützung von "Bring-your-own-Key"-Szenarien, in denen Mandanten Ihre privaten Schlüssel in das Hardware Sicherheitsmodul kopieren und nur Ihre Schlüssel zum Starten Ihrer abgeschirmten VMS autorisieren.
2. Um die vorhandenen Schlüssel für HGS zu ersetzen, indem Sie zuerst die neuen Schlüssel hinzufügen und beide Sätze von Schlüsseln aufbewahren, bis jede VM-Konfiguration aktualisiert wurde, um die neuen Schlüssel zu verwenden.

Der Vorgang zum Hinzufügen der neuen Schlüssel unterscheidet sich je nach Art des verwendeten Zertifikats.

**Option 1: Hinzufügen eines in einem HSM gespeicherten Zertifikats**

Die empfohlene Vorgehensweise zum Sichern von HGS-Schlüsseln ist die Verwendung von Zertifikaten, die in einem Hardware Sicherheitsmodul (HSM) erstellt werden.
Mithilfe von HSMs wird sichergestellt, dass die Verwendung Ihrer Schlüssel an den physischen Zugriff auf ein Sicherheits sensibles Gerät in Ihrem Daten Center gebunden ist.
Jedes HSM ist unterschiedlich und verfügt über einen eindeutigen Prozess zum Erstellen von Zertifikaten und Registrieren der Zertifikate bei HGS.
Die folgenden Schritte sind für eine grobe Anleitung zur Verwendung von HSM-gestützten Zertifikaten vorgesehen.
Die genauen Schritte und Funktionen finden Sie in der Dokumentation des HSM-Herstellers.

1. Installieren Sie die HSM-Software auf jedem HGS-Knoten in Ihrem Cluster. Abhängig davon, ob Sie über ein Netzwerk oder ein lokales HSM-Gerät verfügen, müssen Sie möglicherweise das HSM so konfigurieren, dass Ihr Computer Zugriff auf den Schlüsselspeicher erhält.
2. Erstellen von 2 Zertifikaten im HSM mit **2048-Bit-RSA-Schlüsseln** für die Verschlüsselung und Signierung
    1. Erstellen Sie ein Verschlüsselungs Zertifikat mit der Schlüssel Verwendungs Eigenschaft " **Data Encipherment** " in Ihrem HSM.
    2. Erstellen eines Signatur Zertifikats mit der Eigenschaft "Nutzung **digitaler Signatur** Schlüssel" in Ihrem HSM
3. Installieren Sie die Zertifikate im lokalen Zertifikat Speicher der einzelnen HGS-Knoten gemäß der Anleitung Ihres HSM-Herstellers.
4. Wenn Ihr HSM differenzierte Berechtigungen verwendet, um bestimmten Anwendungen oder Benutzern die Berechtigung zum Verwenden des privaten Schlüssels zu erteilen, müssen Sie Ihrem HGS-Gruppen verwalteten Dienst Konto Zugriff auf das Zertifikat gewähren. Sie können den Namen des HGS-GMSA-Kontos ermitteln, indem Sie ausführen `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
5. Fügen Sie die Signatur-und Verschlüsselungs Zertifikate zu HGS hinzu, indem Sie die Fingerabdrücke durch die der Zertifikate "in den folgenden Befehlen ersetzen:

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA"
    ```

**Option 2: Hinzufügen nicht exportier barer Software Zertifikate**

Wenn Sie über ein Software gestütztes Zertifikat verfügen, das von Ihrem Unternehmen oder von einer öffentlichen Zertifizierungsstelle ausgestellt wurde, die über einen nicht exportierbaren privaten Schlüssel verfügt, müssen Sie das Zertifikat mithilfe des Fingerabdrucks zu HGS hinzufügen.
1. Installieren Sie das Zertifikat auf Ihrem Computer gemäß den Anweisungen Ihrer Zertifizierungsstelle.
2. Erteilen Sie dem verwalteten Dienst Konto der HGS-Gruppe Lesezugriff auf den privaten Schlüssel des Zertifikats. Sie können den Namen des HGS-GMSA-Kontos ermitteln, indem Sie ausführen `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
3. Registrieren Sie das Zertifikat mit dem folgenden Befehl bei HGS, und ersetzen Sie dabei den Fingerabdruck Ihres Zertifikats (Ändern der *Verschlüsselung* in *Signieren* für Signatur Zertifikate):

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    ```

> [!IMPORTANT]
> Sie müssen den privaten Schlüssel manuell installieren und auf jedem HGS-Knoten Lesezugriff auf das GMSA-Konto gewähren.
> HGS können private Schlüssel für *ein* Zertifikat, das durch seinen Fingerabdruck registriert wird, nicht automatisch replizieren.

**Option 3: Hinzufügen von in PFX-Dateien gespeicherten Zertifikaten**

Wenn Sie über ein Software gestütztes Zertifikat mit einem exportierbaren privaten Schlüssel verfügen, der im PFX-Dateiformat gespeichert und mit einem Kennwort gesichert werden kann, können die Zertifikate von HGS automatisch für Sie verwaltet werden.
Zertifikate, die mit PFX-Dateien hinzugefügt werden, werden automatisch an jeden Knoten Ihres HGS-Clusters repliziert, und HGS sichert den Zugriff auf die privaten Schlüssel.
Wenn Sie ein neues Zertifikat mit einer PFX-Datei hinzufügen möchten, führen Sie die folgenden Befehle auf einem beliebigen HGS-Knoten aus (ändern Sie die *Verschlüsselung* in *Signatur* für Signatur Zertifikate):

```powershell
$certPassword = Read-Host -AsSecureString -Prompt "Provide the PFX file password"
Add-HgsKeyProtectionCertificate -CertificateType Encryption -CertificatePath "C:\temp\encryptionCert.pfx" -CertificatePassword $certPassword
```

**Identifizieren und Ändern der primären Zertifikate** Obwohl HGS mehrere Signatur-und Verschlüsselungs Zertifikate unterstützen kann, wird ein paar als "primäre" Zertifikate verwendet.
Dabei handelt es sich um die Zertifikate, die verwendet werden, wenn jemand die Wächter Metadaten für diesen HGS-Cluster herunterlädt.
Führen Sie den folgenden Befehl aus, um zu überprüfen, welche Zertifikate derzeit als primäre Zertifikate gekennzeichnet sind:

```powershell
Get-HgsKeyProtectionCertificate -IsPrimary $true
```

Um ein neues primäres Verschlüsselungs-oder Signaturzertifikat festzulegen, suchen Sie den Fingerabdruck des gewünschten Zertifikats, und markieren Sie ihn mit den folgenden Befehlen als Primärschlüssel:

```powershell
Get-HgsKeyProtectionCertificate
Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899" -IsPrimary
Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA" -IsPrimary
```

### <a name="renewing-or-replacing-keys"></a>Erneuern oder Ersetzen von Schlüsseln
Wenn Sie die von HGS verwendeten Zertifikate erstellen, wird den Zertifikaten gemäß der Richtlinie Ihrer Zertifizierungsstelle und Ihren Anforderungs Informationen ein Ablaufdatum zugewiesen.
Normalerweise müssen Zertifikate in Szenarien, in denen die Gültigkeit des Zertifikats wichtig ist, z. b. das Sichern von http-Kommunikationen, erneuert werden, bevor Sie ablaufen, um eine Dienst Unterbrechung oder eine Fehlermeldung zu vermeiden.
HGS verwendet in diesem Sinne keine Zertifikate.
HGS verwendet Zertifikate einfach als bequeme Möglichkeit zum Erstellen und Speichern eines asymmetrischen Schlüssel Paars.
Ein abgelaufenes Verschlüsselungs-oder Signaturzertifikat auf HGS weist nicht auf eine Schwachstelle oder den Schutz von geschützten VMS hin.
Außerdem werden Zertifikat Sperr Überprüfungen nicht von HGS ausgeführt.
Wenn ein HGS-Zertifikat oder das Zertifikat der ausstellenden Zertifizierungsstelle widerrufen wird, hat dies keine Auswirkung auf die Verwendung des Zertifikats durch die HGS.

Sie müssen sich nur über ein HGS-Zertifikat Gedanken machen, wenn Sie der Meinung sind, dass der private Schlüssel gestohlen wurde.
In diesem Fall besteht die Gefahr, dass die Integrität ihrer abgeschirmten VMS gefährdet ist, weil der Besitz der privaten Hälfte des HGS-Verschlüsselungs-und Signatur Schlüssel Paars ausreicht, um den Schutz Schutz auf einem virtuellen Computer zu entfernen oder einen gefälschten HGS-Server zu erhalten, der schwächere Nachweis Richtlinien aufweist.

Wenn Sie sich in dieser Situation befinden oder von Kompatibilitäts Standards zum regelmäßigen Aktualisieren von Zertifikat Schlüsseln benötigt werden, wird in den folgenden Schritten der Prozess zum Ändern der Schlüssel auf einem HGS-Server beschrieben.
Beachten Sie, dass die folgende Anleitung ein bedeutendes Unternehmen darstellt, das zu einer Dienst Unterbrechung für jede VM führt, die vom HGS-Cluster bedient wird.
Die richtige Planung für das Ändern von HGS-Schlüsseln ist erforderlich, um die Dienst Unterbrechung zu minimieren und die Sicherheit von Mandanten-VMS

Führen Sie auf einem HGS-Knoten die folgenden Schritte aus, um ein neues Paar von Verschlüsselungs-und Signatur Zertifikaten zu registrieren.
Ausführliche Informationen zu den verschiedenen Möglichkeiten zum Hinzufügen neuer Schlüssel zu HGS finden Sie im Abschnitt zum Hinzufügen [neuer Schlüssel](#adding-new-keys) .
1. Erstellen Sie ein neues Paar von Verschlüsselungs-und Signatur Zertifikaten für Ihren HGS-Server. Im Idealfall werden diese in einem Hardware Sicherheitsmodul erstellt.
2. Registrieren der neuen Verschlüsselungs-und Signatur Zertifikate mit **Add-hgskeyschutzcertificate**

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>
    ```
3. Wenn Sie Fingerabdrücke verwendet haben, müssen Sie zu jedem Knoten im Cluster wechseln, um den privaten Schlüssel zu installieren und dem HGS-GMSA Zugriff auf den Schlüssel zu gewähren.
4. Erstellen der neuen Zertifikate als Standardzertifikate in HGS

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsPrimary
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsPrimary
    ```

An diesem Punkt werden geschützte Daten, die mit Metadaten aus dem HGS-Knoten erstellt werden, die neuen Zertifikate verwenden, vorhandene virtuelle Computer funktionieren jedoch weiterhin, da die älteren Zertifikate weiterhin vorhanden sind.
Um sicherzustellen, dass alle vorhandenen VMS mit den neuen Schlüsseln funktionieren, müssen Sie die Schlüssel Schutzvorrichtung auf den einzelnen virtuellen Computern aktualisieren.
Dabei handelt es sich um eine Aktion, die erfordert, dass der Besitzer des virtuellen Computers (Person oder Entität, die den "Owner"-Wächter besitzt) beteiligt ist.
Führen Sie für jede abgeschirmte VM die folgenden Schritte aus:
5. Fahren Sie den virtuellen Computer herunter. Der virtuelle Computer kann erst wieder eingeschaltet werden, wenn die restlichen Schritte ausgeführt wurden. andernfalls müssen Sie den Prozess erneut starten.
6. Aktuelle Schlüssel Schutzvorrichtung in einer Datei speichern: `Get-VMKeyProtector -VMName 'VM001' | Out-File '.\VM001.kp'`
7. Übertragen der KP in den VM-Besitzer
8. Lassen Sie den Besitzer die aktualisierten Überwachungsinformationen von HGS herunterladen und auf Ihrem lokalen System importieren
9. Lesen Sie die aktuelle KP in den Arbeitsspeicher, gewähren Sie dem neuen Erziehungsberechtigten Zugriff auf die KP, und speichern Sie Sie in einer neuen Datei, indem Sie die folgenden Befehle ausführen:

    ```powershell
    $kpraw = Get-Content -Path .\VM001.kp
    $kp = ConvertTo-HgsKeyProtector -Bytes $kpraw
    $newGuardian = Get-HgsGuardian -Name 'UpdatedHgsGuardian'
    $updatedKP = Grant-HgsKeyProtectorAccess -KeyProtector $kp -Guardian $newGuardian
    $updatedKP.RawData | Out-File .\updatedVM001.kp
    ```
10. Kopieren Sie die aktualisierte KP zurück in das hostingfabric.
11. Wenden Sie die KP auf den ursprünglichen virtuellen Computer an:

   ```powershell
   $updatedKP = Get-Content -Path .\updatedVM001.kp
   Set-VMKeyProtector -VMName VM001 -KeyProtector $updatedKP
   ```
12. Starten Sie die VM, und stellen Sie sicher, dass Sie erfolgreich ausgeführt wird.

> [!NOTE]
> Wenn der VM-Besitzer eine falsche Schlüssel Schutzvorrichtung auf dem virtuellen Computer festlegt und Ihr Fabric nicht zum Ausführen des virtuellen Computers autorisiert, können Sie den abgeschirmten virtuellen Computer nicht starten.
> Um zur letzten als funktionierend bekannten Schlüssel Schutzvorrichtung zurückzukehren, führen Sie `Set-VMKeyProtector -RestoreLastKnownGoodKeyProtector`

Nachdem alle VMs aktualisiert wurden, um die neuen Wächter Schlüssel zu autorisieren, können Sie die alten Schlüssel deaktivieren und entfernen.

13. Holen Sie sich die Fingerabdrücke der alten Zertifikate aus `Get-HgsKeyProtectionCertificate -IsPrimary $false`

14. Deaktivieren Sie die einzelnen Zertifikate, indem Sie die folgenden Befehle ausführen:  

   ```powershell
   Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsEnabled $false
   Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsEnabled $false
   ```

15. Nachdem Sie sichergestellt haben, dass die VMs weiterhin mit deaktivierten Zertifikaten gestartet werden können, entfernen Sie die Zertifikate aus HGS, indem Sie die folgenden Befehle ausführen:

   ```powershell
   Remove-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>`
   Remove-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>`
   ```

> [!IMPORTANT]
> VM-Sicherungen enthalten alte schlüsselschutzinformationen, mit denen die alten Zertifikate zum Starten der VM verwendet werden können.
> Wenn Sie wissen, dass Ihr privater Schlüssel kompromittiert wurde, sollten Sie davon ausgehen, dass die VM-Sicherungen ebenfalls kompromittiert werden können, und die entsprechenden Maßnahmen ergreifen.
> Durch das zerstören der VM-Konfiguration aus den Sicherungen (vmcx-Dateien) werden die Schlüssel Schutzvorrichtungen entfernt. Dies führt dazu, dass das BitLocker-Wiederherstellungs Kennwort zum nächsten Mal zum Starten der VM verwendet werden muss.

### <a name="key-replication-between-nodes"></a>Schlüssel Replikation zwischen Knoten
Jeder Knoten im HGS-Cluster muss mit denselben Verschlüsselungs-, Signatur-und (wenn konfigurierten) SSL-Zertifikaten konfiguriert werden.
Dies ist erforderlich, um sicherzustellen, dass die Anforderungen von Hyper-V-Hosts, die zu einem beliebigen Knoten im Cluster gelangen, erfolgreich bedient werden können.

**Wenn Sie den HGS-Server mit PFX-basierten Zertifikaten initialisiert** haben, repliziert HGS automatisch sowohl den öffentlichen als auch den privaten Schlüssel dieser Zertifikate auf allen Knoten im Cluster.
Sie müssen nur die Schlüssel auf einem Knoten hinzufügen.

**Wenn Sie den HGS-Server mit Zertifikat verweisen** oder Fingerabdrücken initialisiert haben, repliziert HGS den *öffentlichen* Schlüssel im Zertifikat nur auf jeden Knoten.
Darüber hinaus kann HGS selbst keinen Zugriff auf den privaten Schlüssel auf einem Knoten in diesem Szenario gewähren.
Daher sind Sie für folgende Aufgaben verantwortlich:
1. Installieren Sie den privaten Schlüssel auf jedem HGS-Knoten.
2. Gewähren Sie dem Gruppen verwalteten Dienst Konto (Managed Service Account, GMSA) der HGS-Gruppe Zugriff auf den privaten Schlüssel auf jedem Knoten, da diese Aufgaben zusätzliche Betriebsbelastung erfordern, sind Sie jedoch für HSM-gestützte Schlüssel und Zertifikate mit nicht exportierbaren privaten Schlüsseln erforderlich.

**SSL-Zertifikate** werden nie in irgendeiner Form repliziert.
Es liegt in ihrer Verantwortung, jeden HGS-Server mit demselben SSL-Zertifikat zu initialisieren und jeden Server zu aktualisieren, wenn Sie das SSL-Zertifikat erneuern oder ersetzen.
Wenn Sie das SSL-Zertifikat ersetzen, empfiehlt es sich, das Cmdlet [Set-hgsserver](https://technet.microsoft.com/library/mt652180.aspx) zu verwenden.

## <a name="unconfiguring-hgs"></a>Aufheben der Konfiguration von HGS

Wenn Sie einen HGS-Server außer Betrieb setzen oder erheblich neu konfigurieren müssen, können Sie dazu die Cmdlets [Clear-hgsserver](https://technet.microsoft.com/library/mt652176.aspx) oder [Uninstall-hgsserver](https://technet.microsoft.com/library/mt652182.aspx) verwenden.

### <a name="clearing-the-hgs-configuration"></a>Löschen der HGS-Konfiguration

Verwenden Sie zum Entfernen eines Knotens aus dem HGS-Cluster das Cmdlet [Clear-hgsserver](https://technet.microsoft.com/library/mt652176.aspx) .
Mit diesem Cmdlet werden auf dem Server, auf dem es ausgeführt wird, die folgenden Änderungen vorgenommen:

- Hebt die Registrierung der Nachweis-und Schlüsselschutz Dienste auf.
- Entfernt den Jea-Verwaltungs Endpunkt "Microsoft. Windows. HGS".
- Entfernt den lokalen Computer aus dem HGS-Failovercluster.

Wenn der Server der letzte HGS-Knoten im Cluster ist, werden auch der Cluster und die zugehörige verteilte Netzwerknamen Ressource zerstört.

```powershell
# Removes the local computer from the HGS cluster
Clear-HgsServer
```

Nachdem der Löschvorgang abgeschlossen ist, kann der HGS-Server mit [Initialize-hgsserver](https://technet.microsoft.com/library/mt652185.aspx)erneut initialisiert werden.
Wenn Sie [install-hgsserver](https://technet.microsoft.com/library/mt652169.aspx) zum Einrichten einer Active Directory Domain Services Domäne verwendet haben, bleibt diese Domäne nach dem Löschvorgang konfiguriert und betriebsbereit.

### <a name="uninstalling-hgs"></a>Deinstallieren von HGS

Wenn Sie einen Knoten aus dem HGS-Cluster entfernen **und** den Active Directory-Domäne Controller herabstufen möchten, auf dem er ausgeführt wird, verwenden Sie das Cmdlet [Uninstall-hgsserver](https://technet.microsoft.com/library/mt652182.aspx) .
Mit diesem Cmdlet werden auf dem Server, auf dem es ausgeführt wird, die folgenden Änderungen vorgenommen:

- Hebt die Registrierung der Nachweis-und Schlüsselschutz Dienste auf.
- Entfernt den Jea-Verwaltungs Endpunkt "Microsoft. Windows. HGS".
- Entfernt den lokalen Computer aus dem HGS-Failovercluster.
- Herabstufen des Active Directory-Domäne Controllers, sofern konfiguriert

Wenn es sich bei dem Server um den letzten HGS-Knoten im Cluster handelt, werden die Domäne, der Failovercluster und die verteilte Netzwerknamen Ressource des Clusters ebenfalls zerstört.

```powershell
# Removes the local computer from the HGS cluster and demotes the ADDC (restart required)
$newLocalAdminPassword = Read-Host -AsSecureString -Prompt "Enter a new password for the local administrator account"
Uninstall-HgsServer -LocalAdministratorPassword $newLocalAdminPassword -Restart
```

Nachdem der Deinstallations Vorgang abgeschlossen und der Computer neu gestartet wurde, können Sie addc und HGS mithilfe von [install-hgsserver](https://technet.microsoft.com/library/mt652169.aspx) neu installieren oder den Computer einer Domäne hinzufügen und den HGS-Server in dieser Domäne mit [initialisieren-hgsserver](https://technet.microsoft.com/library/mt652185.aspx)initialisieren.

Wenn Sie den Computer nicht mehr als HGS-Knoten verwenden möchten, können Sie die Rolle aus Windows entfernen.

```powershell
Uninstall-WindowsFeature HostGuardianServiceRole
```
