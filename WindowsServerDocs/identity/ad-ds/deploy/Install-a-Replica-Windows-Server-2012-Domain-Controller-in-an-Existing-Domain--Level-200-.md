---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: Installieren eines Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne (Stufe 200)
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a7a9b59d9676484ea39262fb023b56374533e6ec
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88940880"
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>Installieren eines Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne (Stufe 200)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel beschreibt die erforderlichen Schritte für die Aktualisierung bestehender Gesamtstrukturen oder Domänen auf Windows Server 2012, entweder via Server-Manager oder Windows PowerShell. Sie erfahren, wie Sie die Domänencontroller, auf denen Windows Server 2012 ausgeführt wird, zu einer Domäne hinzufügen können.

-   [Upgrade- und Replikat-Workflow](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)

-   [Upgrade und Replikat mit Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)

-   [Bereitstellung](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)

## <a name="upgrade-and-replica-workflow"></a><a name="BKMK_Workflow"></a>Upgrade- und Replikat-Workflow
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory-Domänendienste, wenn Sie die AD DS-Rolle zuvor installiert haben und den Konfigurations-Assistenten für die Active Directory-Domänendienste über den Server-Manager gestartet haben, um einen neuen Domänencontroller in einer existierenden Domäne zu erstellen.

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)

## <a name="upgrade-and-replica-windows-powershell"></a><a name="BKMK_PS"></a>Upgrade und Replikat mit Windows PowerShell

| Cmdlet "ADDSDeployment" | Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.) |
|--|--|
| Install-AddsDomainController | -SkipPreChecks<p>***-Domain Name***<p>*-SafeModeAdministratorPassword*<p>*-Sitename*<p>*-ADPrepCredential*<p>-ApplicationPartitionsToReplicate<p>*-Allowdomaincontrollerreinstall*<p>-Confirm<p>*-"-Kreatednsdelegation"*<p>***-Credential***<p>-CriticalReplicationOnly<p>*-DatabasePath*<p>*-DNSDelegationCredential*<p>-Force<p>*-Installationmediapath*<p>*-InstallDNS*<p>*-LogPath*<p>-MoveInfrastructureOperationMasterRoleIfNecessary<p>-NoDnsOnNetwork<p>*-Noglobalcatalog*<p>-Norebootoncompletion<p>*-ReplicationSourceDC*<p>-SkipAutoConfigureDNS<p>-SiteName<p>*-System Key*<p>*-Sysvolpath*<p>*-UseExistingAccount*<p>*-WhatIf* |

> [!NOTE]
> Das Argument **-credential** wird nur benötigt, wenn Sie nicht bereits als Mitglied der Gruppen Organisations-Admins und Schema-Admins (für Upgrades der Gesamtstruktur) oder der Gruppe Domänen-Admins (beim Hinzufügen eines neuen Domänencontrollers zu einer existierenden Domäne) angemeldet sind.

## <a name="deployment"></a><a name="BKMK_Dep"></a>Nutzung

### <a name="deployment-configuration"></a>Bereitstellungskonfiguration
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)

In Server-Manager beginnt jede Heraufstufung eines Domänencontrollers auf der Seite **Bereitstellungskonfiguration**. Die restlichen Optionen und erforderlichen Felder auf dieser Seite und den folgenden Seiten variieren in Abhängigkeit von dem von Ihnen ausgewählten Bereitstellungsvorgang.

Um eine existierende Gesamtstruktur zu aktualisieren oder einen beschreibbaren Domänencontroller zu einer existierenden Domäne hinzuzufügen, klicken Sie auf **Domänencontroller vorhandener Domäne hinzufügen** und auf **Auswählen**, um **die Domäneninformationen für diese Domäne anzugeben**. Server-Manager fordert Sie ggf. zur Eingabe gültiger Anmeldeinformationen auf.

Für das Upgrade einer Gesamtstruktur sind Anmeldeinformationen erforderlich, die Gruppenmitgliedschaften in den beiden Gruppen "Organisations-Admins" und "Schema-Admins" in Windows Server 2012 umfassen. Wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften aufweisen, wird später vom Konfigurations-Assistenten für die Active Directory-Domänendienste eine Eingabeaufforderung ausgegeben.

Der automatische Adprep-Prozess ist der einzige operative Unterschied zwischen dem Hinzufügen eines Domänencontrollers zu einer existierenden Windows Server 2012-Domäne oder zu einer Domäne, deren Controller unter einer früheren Windows Server-Version laufen.

ADDSDeployment-Cmdlet und Argumente für die Konfiguration der Bereitstellung sind:

```
Install-AddsDomainController
-domainname <string>
-credential <pscredential>
```

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)

Bestimmte Tests werden auf jeder Seite ausgeführt, von denen einige später als eigenständige Voraussetzungstests wiederholt werden. Falls die ausgewählte Domäne z. B. die Mindest-Funktionsebenen erfüllt, müssen Sie nicht den gesamten Weg von der Heraufstufung bis zum Voraussetzungstest durchlaufen, um dies zu erfahren:

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)

### <a name="domain-controller-options"></a>Domänencontrolleroptionen
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)

Die Seite **Domänencontrolleroptionen** enthält die Domänencontrollerfunktionen für den neuen Domänencontroller. Die konfigurierbaren Domänencontrollerfunktionen lauten **DNS-Server**, **Globaler Katalog** und **Schreibgeschützter Domänencontroller**. Für eine hohe Verfügbarkeit in verteilten Umgebungen empfiehlt Microsoft, dass alle Domänencontroller DNS und globale Katalogdienste bereitstellen. GC ist standardmäßig immer ausgewählt, und DNS-Server ist standardmäßig ausgewählt, wenn die aktuelle Domäne bereits DNS auf deren DCs auf Basis der Autoritätsursprungs-Abfrage hostet. Auf der Seite **Domänencontrolleroptionen** können Sie unter **Standortname** den entsprechenden logischen Standortnamen für Active Directory in der Gesamtstrukturkonfiguration auswählen. Standardmäßig ist der Standortname mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, wird dieser automatisch ausgewählt.

> [!NOTE]
> Wenn der Server zu keinem Active Directory-Subnetz gehört und mehrere Active Directory-Standorte vorhanden sind, wird keine Auswahl getroffen, und die Schaltfläche **Weiter** ist erst wieder verfügbar, nachdem Sie in der Liste einen Standort ausgewählt haben.

Das angegebene **Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus** muss die Kennwortrichtlinie für den Server erfüllen. Wählen Sie stets ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase aus.

Die ADDSDeployment-Argumente für **Domänencontrolleroptionen** sind:

```
-InstallDNS <{$false | $true}>
-NoGlobalCatalog <{$false | $true}>
-sitename <string>
-SafeModeAdministratorPassword <secure string>
```

> [!IMPORTANT]
> Der Standortname muss bei der Angabe als Argument für **-sitename** bereits vorhanden sein. Das **install-AddsDomainController**-Cmdlet erstellt keine Standorte. Mit dem Cmdlet **new-adreplicationsite** können Sie neue Standorte erstellen.

Das Argument **SafeModeAdministratorPassword** funktioniert etwas anders:

-   wenn als Argument *nicht angegeben*, fordert das Cmdlet Sie auf, ein maskiertes Kennwort einzugeben und zu bestätigen. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.

    Um z. B. einen zusätzlichen Domänencontroller in der Domäne treyresearch.net zu erstellen und zur Eingabe eines maskierten Kennworts aufgefordert zu werden:

    ```
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)
    ```

-   wenn *mit einem Wert* angegeben, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.

Mithilfe des Cmdlets **Read-Host** können Sie beispielsweise manuell nach einem Kennwort fragen, um den Benutzer zur Eingabe einer sicheren Zeichenfolge aufzufordern:

```
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)
```

> [!WARNING]
> Da mit der vorherigen Option das Kennwort nicht bestätigt wird, gehen Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.

Sie können eine sichere Zeichenfolge auch als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird.

```
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)

```

Zuletzt sollten Sie das verborgene Kennwort in einer Datei speichern und später wiederverwenden, ohne dass jemals das Klartextkennwort erscheint. Beispiel:

```
$file = "c:\pw.txt"
$pw = read-host -prompt "Password:" -assecurestring
$pw | ConvertFrom-SecureString | Set-Content $file

-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)

```

> [!WARNING]
> Das Bereitstellen oder Speichern eines Klartext- oder abgeblendeten Kennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen zusehen, kennen dann das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort extrahieren. Mit diesem Wissen können sie sich bei einem Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden, einen Identitätswechsel für den Domänencontroller selbst ausführen und ihre Rechte in einer Active Directory-Gesamtstruktur auf die höchste Stufe heraufstufen. Zusätzliche Schritte mit **System.Security.Cryptography** zur Verschlüsselung der Textdatei werden empfohlen, sind jedoch nicht Teil dieser Anleitung. Generell sollten Sie es vermeiden, Kennwörter zu speichern.

Das ADDSDeployment-Cmdlet bietet eine zusätzliche Option zum Überspringen der automatischen Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Sie können diese Konfiguration nicht überspringen, wenn Sie Server-Manager verwenden. Dieses Argument ist nur relevant, wenn Sie die DNS-Serverrolle vor der Konfiguration des Domänencontrollers installiert haben:

```
-SkipAutoConfigureDNS
```

Auf der Seite **Domänencontrolleroptionen** erhalten Sie eine Warnung, dass Sie keine schreibgeschützten Domänencontroller erstellen können, wenn Ihre existierenden Domänencontroller unter Windows Server 2003 laufen. Diese Warnung ist zu erwarten und kann verworfen werden.

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)

### <a name="dns-options-and-dns-delegation-credentials"></a>DNS-Optionen und DNS-Delegierungs-Anmeldeinformationen
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)

Auf der Seite **DNS-Optionen** können Sie die DNS-Delegierung konfigurieren, wenn Sie die Option **DNS-Server** auf der Seite *Domänencontrolleroptionen* ausgewählt haben und auf eine Zone verweisen, in der DNS-Delegierungen erlaubt sind. Möglicherweise müssen Sie Anmeldeinformationen eines Benutzers angeben, der Mitglied der Gruppe **DNS-Admins** ist.

ADDSDeployment-Cmdlet und Argumente für die **DNS-Optionen** sind:

```
-creatednsdelegation
-dnsdelegationcredential <pscredential>
```

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)

Weitere Informationen dazu, ob Sie die DNS-Delegierung aktualisieren müssen, finden Sie unter [Grundlegendes zur Zonendelegierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771640(v=ws.11)).

### <a name="additional-options"></a>Zusätzliche Optionen
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)

Die Seite **Zusätzliche Optionen** enthält eine Konfigurationsoption, mit der Sie einen Domänencontroller als Replikationsquelle angeben oder einen beliebigen Domänencontroller als Replikationsquelle verwenden können.

Sie können auch festlegen, dass der Domänencontroller mithilfe gesicherter Medien und der Option %%amp;quot;Installieren von Medium%%amp;quot; (Install from Media, IFM) installiert wird. Wenn Sie das Kontrollkästchen **Installieren von Medium** markieren, wird eine Option zum Durchsuchen angezeigt, und Sie müssen auf **Überprüfen** klicken, um sicherzustellen, dass sich am angegebenen Pfad ein gültiges Medium befindet. Von der IFM-Option verwendete Medien dürfen nur mit der Windows Server-Sicherung oder mit Ntdsutil.exe auf einem anderen vorhandenen Windows Server 2012-Computer erstellt werden. Die Verwendung von Windows Server 2008 R2 oder eines vorherigen Betriebssystems zum Erstellen von Medien für einen Windows Server 2012-Domänencontroller ist nicht möglich. Weitere Informationen zu Änderungen in IFM finden Sie unter [Anhang für vereinfachte Verwaltung](../../ad-ds/deploy/Simplified-Administration-Appendix.md). Wenn die Medien mit einem Systemschlüssel (SYSKEY) geschützt sind, werden Sie während der Überprüfung von Server-Manager zur Eingabe des Kennworts für das Abbild aufgefordert.

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)

Die ADDSDeployment Windows PowerShell-Argumente für **Zusätzliche Optionen** sind:

```
-replicationsourcedc <string>
-installationmediapath <string>
-syskey <secure string>
```

### <a name="paths"></a>Pfade
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)

Auf der Seite **Pfade** können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von %systemroot%.

ADDSDeployment-Cmdlet und Argumente für Active Directory-Pfade sind:

```
-databasepath <string>
-logpath <string>
-sysvolpath <string>
```

### <a name="preparation-options"></a>Vorbereitungsoptionen
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)

Die Seite **Vorbereitungsoptionen** weist Sie darauf hin, dass die AD DS-Konfiguration eine Erweiterung des Schemas (forestprep) und eine Aktualisierung der Domäne umfasst (domainprep).  Diese Seite wird nur angezeigt, wenn Gesamtstruktur und Domäne nicht durch eine vorherige Installation eines Windows Server 2012 Domänencontrollers oder durch manuelles Ausführen von Adprep.exe vorbereitet wurden. Der Konfigurations-Assistent für Active Directory-Domänendienste unterdrückt diese Seite beispielsweise, wenn Sie einen neuen Domänencontroller zu einer existierenden Windows Server 2012-Gesamtstruktur-Stammdomäne hinzufügen.

Erweiterung des Schemas und Aktualisierung der Domäne erfolgen noch nicht, wenn Sie auf **Weiter** klicken. Diese Schritte werden erst während der Installationsphase ausgeführt. Diese Seite weist Sie lediglich auf die Schritte hin, die später bei der Installation ausgeführt werden.

Die Seite prüft außerdem, ob die aktuellen Anmeldeinformationen Mitglieder der Gruppen Schema-Admins und Organisations-Admins sind. Sie müssen Mitglied dieser beiden Gruppen sein, um ein Schema zu erweitern oder eine Domäne vorzubereiten. Klicken Sie auf **Ändern**, um die entsprechenden Benutzeranmeldeinformationen einzugeben, falls Sie einen Hinweis erhalten, dass die aktuellen Daten keine ausreichenden Berechtigungen haben.

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)

Das Argument für das Cmdlet "ADDSDeployment" für "Zusätzliche Optionen" ist:

```
-adprepcredential <pscredential>
```

> [!IMPORTANT]
> Wie bei früheren Windows Server-Versionen wird GPPREP bei der automatischen Domänenvorbereitung für Domänencontroller unter Windows Server 2012 nicht ausgeführt. Führen Sie **adprep.exe /gpprep** manuell für alle Domänen aus, die nicht zuvor für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Sie sollten GPPrep nur einmal während der Lebensdauer einer Domäne ausführen, und nicht bei jedem Upgrade. Adprep.exe führe /gpprep nicht automatisch aus, da dieser Vorgang dazu führen kann, dass alle Dateien und Ordner im SYSVOL-Ordner erneut auf allen Domänencontrollern repliziert werden.
>
> Der automatische RODCPrep-Vorgang wird ausgeführt, wenn Sie den ersten nicht gestaffelten RODC in einer Domäne heraufstufen. Der Vorgang wird nicht ausgeführt, wenn Sie den ersten beschreibbaren Windows Server 2012-Domänencontroller heraufstufen. Sie können **adprep.exe /rodcprep** dennoch manuell ausführen, wenn Sie schreibgeschützte Domänencontroller bereitstellen möchten.

### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)

Auf der Seite **Optionen prüfen** können Sie vor dem Starten der Installation Ihre Einstellungen validieren und sicherstellen, dass Ihre Anforderungen erfüllt werden. Dies ist jedoch nicht die letzte Möglichkeit, um die Installation mit Server-Manager zu stoppen. Diese Seite ermöglicht Ihnen lediglich das Überprüfen und Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetzen.

Die Seite **Optionen prüfen** im Server-Manager bietet zudem die optionale Schaltfläche **Skript anzeigen** zum Erstellen einer Unicode-Textdatei, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dies ermöglicht Ihnen die Verwendung der grafischen Oberfläche von Server-Manager als Windows PowerShell-Bereitstellungsstudio. Mithilfe des Konfigurations-Assistenten für die Active Directory-Domänendienste können Sie Optionen konfigurieren, die Konfiguration exportieren und den Assistenten abbrechen.  Bei diesem Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt.

Beispiel:

```
#
# Windows PowerShell Script for AD DS Deployment
#
Import-Module ADDSDeployment
Install-ADDSDomainController `
-CreateDNSDelegation `
-Credential (Get-Credential) `
-CriticalReplicationOnly:$false `
-DatabasePath "C:\Windows\NTDS" `
-DomainName "root.fabrikam.com" `
-InstallDNS:$true `
-LogPath "C:\Windows\NTDS" `
-SiteName "Default-First-Site-Name" `
-SYSVOLPath "C:\Windows\SYSVOL"
-Force:$true

```

> [!NOTE]
> Server-Manager füllt bei der Heraufstufung normalerweise alle Argumente mit Werten aus und verlässt sich nicht auf Standardwerte (da sich diese in zukünftigen Windows-Versionen oder Service Packs ändern können). Die einzige Ausnahme hierbei ist das Argument **-safemodeadministratorpassword**. Lassen Sie dieses Argument bei der interaktiven Ausführung des Cmdlets aus, um eine Bestätigungsaufforderung zu erzwingen
>
> Verwenden Sie das optionale **Whatif**-Argument für das **Install-ADDSDomainController**-Cmdlet, um die Konfigurationsinformationen zu überprüfen. Auf diese Weise können Sie die impliziten und expliziten Argumentwerte für ein Cmdlet anzeigen.

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)

### <a name="prerequisites-check"></a>Voraussetzungsüberprüfung
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)

Die **Voraussetzungsüberprüfung** ist ein neues Feature in der AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob Domäne und Gesamtstruktur in der Lage sind, einen neuen Windows Server 2012-Domänencontroller zu unterstützen.

Bei der Installation eines neuen Domänencontrollers führt der Konfigurations-Assistent des Server-Managers für Active Directory-Domänendienste eine Reihe serialisierter modularer Tests durch. Diese Tests geben anschließend Empfehlungen für Reparaturoptionen aus. Sie können die Tests beliebig oft ausführen. Der Prozess für den Domänencontroller kann erst fortgesetzt werden, wenn alle Voraussetzungstests positiv abgeschlossen wurden.

Bei der **Voraussetzungsüberprüfung** werden außerdem relevante Informationen wie z. B. Sicherheitsänderungen angezeigt, die ältere Betriebssysteme betreffen.

Weitere Informationen zu den Voraussetzungsprüfungen finden Sie unter [Voraussetzungsüberprüfung](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).

Bei Verwendung des Server-Managers können Sie die **Voraussetzungsüberprüfung** nicht überspringen. Sie können diese jedoch mit dem folgenden Argument überspringen, wenn Sie das Cmdlet "ADDSDeployment" verwenden:

```
-skipprechecks

```

> [!WARNING]
> Microsoft rät davon ab, die Voraussetzungsüberprüfung zu überspringen, da dies zu einer teilweisen Heraufstufung des Domänencontrollers oder zu einer beschädigten AD DS-Gesamtstruktur führen kann.

Klicken Sie auf **Installieren**, um mit der Domänencontroller-Heraufstufung zu beginnen. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Der Heraufstufungsprozess kann während der Ausführung nicht unterbrochen werden. Der Computer wird nach dem Ende der Heraufstufung unabhängig von deren Ergebnis neu gestartet. Die Seite **Voraussetzungsüberprüfung** zeigt alle beim Prozess aufgetretenen Probleme an und enthält Hinweise zu deren Lösung.

### <a name="installation"></a>Installation
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)

Wenn die Seite **Installation** angezeigt wird, beginnt die Konfiguration des Domänencontrollers und kann nicht angehalten oder abgebrochen werden. Detaillierte Informationen werden auf dieser Seite angezeigt und in die Protokolle geschrieben:

-   %systemroot%\debug\dcpromo.log

-   %systemroot%\debug\dcpromoui.log

-   %systemroot%\debug\adprep\logs

-   %systemroot%\debug\netsetup.log (falls der Server zu einer Arbeitsgruppe gehört)

Verwenden Sie das folgende Cmdlet, um eine neue Active Directory-Gesamtstruktur mithilfe des ADDSDeployment-Moduls zu installieren:

```
Install-addsdomaincontroller
```

Unter [Upgrade und Replikat mit Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS) finden Sie eine Liste optionaler und benötigter Argumente.

Das **Install-AddsDomainController**-Cmdlet besteht nur aus zwei Phasen (Voraussetzungsüberprüfung und Installation). Die beiden folgenden Abbildungen zeigen die Installationsphase mit den benötigten Mindestargumenten **-domainname** und **-credential**. Beachten Sie, dass der Adprep-Vorgang automatisch beim Hinzufügen des ersten Windows Server 2012-Domänencontrollers zu einer existierenden Windows Server 2003-Gesamtstruktur erfolgt:

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)

Ebenso wie beim Server-Manager werden Sie von **Install-ADDSDomainController** darauf hingewiesen, dass der Server beim Heraufstufen automatisch neu gestartet wird. Mit dem **-force**-Argument oder dem **-confirm:$false**-Argument können Sie den Neustart in allen Windows PowerShell-Cmdlets vom Typ "ADDSDeployment" automatisch akzeptieren. Verwenden Sie das **-norebootoncompletion**-Argument, um den automatischen Neustart am Ende der Heraufstufung zu verhindern.

> [!WARNING]
> Es wird davon abgeraten, den Neustart zu verhindern. Der Domänencontroller muss neu gestartet werden, um korrekt zu funktionieren.

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)

Um einen Domänen Controller Remote mithilfe von Windows PowerShell zu konfigurieren, müssen Sie das Cmdlet **install-addsdomaincontroller** *innerhalb* des Cmdlets " **Aufruf-Command** " einschließen. Verwenden Sie dazu geschweifte Klammern.

```
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>
```

Beispiel:

![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)

> [!NOTE]
> Weitere Informationen zur Installation und zum Adprep-Prozess finden Sie unter [Problembehandlung der Domänencontrollerbereitstellung](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md).

### <a name="results"></a>Ergebnisse
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)

Auf der Seite **Ergebnisse** werden Erfolg bzw. Misserfolg der Heraufstufung sowie alle wichtigen Administrationsinformationen angezeigt. Im Erfolgsfall wird der Domänencontroller nach 10 Sekunden automatisch neu gestartet.

Wie bei früheren Windows Server-Versionen wird GPPREP bei der automatischen Domänenvorbereitung für Domänencontroller unter Windows Server 2012 nicht ausgeführt. Führen Sie **adprep.exe /gpprep** manuell für alle Domänen aus, die nicht zuvor für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Sie sollten GPPrep nur einmal während der Lebensdauer einer Domäne ausführen, und nicht bei jedem Upgrade. Adprep.exe führe /gpprep nicht automatisch aus, da dieser Vorgang dazu führen kann, dass alle Dateien und Ordner im SYSVOL-Ordner erneut auf allen Domänencontrollern repliziert werden.

