---
ms.assetid: e3d55565-ad45-4504-ad73-8103d1a92170
title: Installieren einer neuen untergeordneten oder Active Directory-Gesamtstrukturdomäne in Windows Server 2012 (Stufe 200)
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b6ffd6fe586e4a9db937814eefbb49477189e58f
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069232"
---
# <a name="install-a-new-windows-server-2012-active-directory-child-or-tree-domain-level-200"></a>Installieren einer neuen untergeordneten oder Active Directory-Gesamtstrukturdomäne in Windows Server 2012 (Stufe 200)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel beschreibt, wie Sie untergeordnete und Strukturdomänen mithilfe von Server-Manager oder Windows PowerShell zu einer existierenden Windows Server 2012-Gesamtstruktur hinzufügen können.

-   [Workflow für untergeordnete und Strukturdomänen](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Workflow)

-   [Untergeordnete und Strukturdomänen in Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)

-   [Bereitstellung](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Deployment)

## <a name="child-and-tree-domain-workflow"></a><a name="BKMK_Workflow"></a>Workflow für untergeordnete und Strukturdomänen
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory-Domänendienste, wenn Sie die AD DS-Rolle zuvor installiert haben und den Konfigurations-Assistenten für die Active Directory-Domänendienste über den Server-Manager gestartet haben, um eine neue Domäne in einer existierenden Gesamtstruktur zu erstellen.

![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/adds_childtreedeploy_beta1.png)

## <a name="child-and-tree-domain-windows-powershell"></a><a name="BKMK_PS"></a>Untergeordnete und Strukturdomänen in Windows PowerShell

| ADDSDeployment-Cmdlet | Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.) |
|--|--|
| **Install-AddsDomain** | -SkipPreChecks<p>**_-Newdomainname_ *_<p>_* _-Element Domainname_ *_<p>_* _-SafeModeAdministratorPassword_*_<p>_ -adprepcredential* <p> -allowdomainreinstall <p> -Confirm <p> *-anatednsdelegation* <p> * * *-Credential** _<p>_ -DatabasePath *<p>* -dnsdelegationcredential *<p> -nodnsonnetwork <p>* -DomainMode *<p> * **-Domain Type**_<p> -Force <p>_ -InstallDNS*<p>*-LogPath*<p>*-NewDomainNetBIOSName*<p>*-Noglobalcatalog*<p>-NoNorebootoncompletion<p>*-ReplicationSourceDC*<p>*-Sitename*<p>-SkipAutoConfigureDNS<p>*-Sysvolpath*<p>*-WhatIf* |  |

> [!NOTE]
> Das Argument **-credential** ist nur erforderlich, wenn Sie derzeit nicht als Mitglied der Gruppe "Organisations-Admins" angemeldet sind. Das Argument **-NewDomainNetBIOSName** ist erforderlich, wenn Sie den automatisch generierten 15-stelligen Namen, der auf dem DNS-Domänennamenspräfix basiert, ändern möchten oder wenn der Name mehr als 15 Zeichen enthält.

## <a name="deployment"></a><a name="BKMK_Deployment"></a>Bereitstellung

### <a name="deployment-configuration"></a>Bereitstellungskonfiguration
Der folgende Screenshot zeigt die Optionen beim Hinzufügen einer untergeordneten Domäne:

![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDeployConfig.png)

Der folgende Screenshot zeigt die Optionen beim Hinzufügen einer Strukturdomäne:

![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_TreeDeployConfig.png)

In Server-Manager beginnt jede Heraufstufung eines Domänencontrollers auf der Seite **Bereitstellungskonfiguration** . Die restlichen Optionen und erforderlichen Felder auf dieser Seite und den folgenden Seiten variieren in Abhängigkeit von dem von Ihnen ausgewählten Bereitstellungsvorgang.

Dieser Artikel verbindet zwei separate Operationen: Heraufstufung von untergeordneten Domänen und Heraufstufung von Strukturdomänen. Der einzige Unterschied zwischen diesen beiden Operation ist der bei der Erstellung ausgewählte Domänentyp. Alle weiteren Schritte der beiden Operationen sind identisch.

-   Um eine neue untergeordnete Domäne zu erstellen, klicken Sie auf **Neue Domäne einer vorhandenen Gesamtstruktur hinzufügen** und wählen **Untergeordnete Domäne** aus. Unter **Übergeordnete Domäne** geben Sie den Namen der übergeordneten Domäne ein bzw. wählen diesen aus. Geben Sie anschließend den Namen der neuen Domäne in das Feld **Neuer Domänenname** ein. Geben Sie einen gültigen Namen für die untergeordnete Domäne an, der aus einer einzelnen Bezeichnung besteht; der Name muss die Anforderungen an den DNS-Domänennamen erfüllen.

-   Um eine neue Strukturdomäne innerhalb einer vorhandenen Gesamtstruktur zu erstellen, klicken Sie auf **Neue Domäne einer vorhandenen Gesamtstruktur hinzufügen** und wählen **Strukturdomäne** aus. Geben Sie den Namen der Gesamtstruktur-Stammdomäne und anschließend den Namen der neuen Domäne ein. Geben Sie einen gültigen, vollqualifizierten Stammdomänennamen an; der Name darf nicht aus einer einzelnen Bezeichnung bestehen und muss die Anforderungen an den DNS-Domänennamen erfüllen.

Weitere Informationen zu DNS-Namen finden Sie unter [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](https://support.microsoft.com/kb/909264).

Der Konfigurations-Assistent für die Active Directory-Domänendienste im Server-Manager fordert Sie zur Eingabe der Domänenanmeldeinformationen auf, wenn Ihre aktuellen Anmeldeinformationen nicht zu der Domäne gehören. Klicken Sie auf **Ändern** , um Domänenanmeldeinformationen für die Heraufstufung anzugeben.

ADDSDeployment-Cmdlet und Argumente für die Konfiguration der Bereitstellung sind:

```
Install-AddsDomain
-domaintype <{childdomain | treedomain}>
-parentdomainname <string>
-newdomainname <string>
-credential <pscredential>
```

### <a name="domain-controller-options"></a>Domänencontrolleroptionen
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_DCOptions_Child.gif)

Auf der Seite **Domänencontrolleroptionen** können Sie die Domänencontrolleroptionen für den neuen Domänencontroller eingeben. Die konfigurierbaren Domänencontrolleroptionen lauten **DNS-Server** und **Globaler Katalog** . Das Konfigurieren eines schreibgeschützten Domänencontrollers als ersten Domänencontroller in einer neuen Domäne ist nicht möglich.

Für eine hohe Verfügbarkeit in verteilten Umgebungen empfiehlt Microsoft, dass alle Domänencontroller DNS und globale Katalogdienste bereitstellen. GC ist standardmäßig immer ausgewählt, und DNS ist standardmäßig ausgewählt, wenn die aktuelle Domäne bereits DNS auf deren GCs hostet, basierend auf einer Autoritätsursprungs-Abfrage. Außerdem müssen Sie eine **Domänenfunktionsebene** angeben. Die Standard-Funktionsebene ist Windows Server 2012, und Sie können einen beliebigen Wert gleich oder größer der aktuellen Gesamtstrukturfunktionsebene auswählen.

Auf der Seite **Domänencontrolleroptionen** können Sie unter **Standortname** den entsprechenden logischen Standortnamen für Active Directory in der Gesamtstrukturkonfiguration auswählen. Standardmäßig wird der Standortname mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, wird dieser automatisch ausgewählt.

> [!IMPORTANT]
> Wenn der Server zu keinem Active Directory-Subnetz gehört und mehrere Active Directory-Standorte vorhanden sind, wird keine Auswahl getroffen, und die Schaltfläche **Weiter** ist erst wieder verfügbar, nachdem Sie in der Liste einen Standort ausgewählt haben.

Das angegebene **Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus** muss die Kennwortrichtlinie für den Server erfüllen. Wählen Sie stets ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase aus.

Die Argumente des Cmdlets "ADDSDeployment" für **Domänencontrolleroptionen** sind:

```
-InstallDNS <{$false | $true}>
-NoGlobalCatalog <{$false | $true}>
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>
-Sitename <string>
-SafeModeAdministratorPassword <secure string>
-Credential <pscredential>
```

> [!IMPORTANT]
> Der Standortname muss bei der Angabe als Wert für das **sitename** -Argument bereits vorhanden sein. Das Cmdlet **install-AddsDomainController** erstellt keine Standortnamen. Sie können das Cmdlet **new-adreplicationsite** zum Erstellen neuer Standorte verwenden.

Die Argumente des Cmdlets **Install-ADDSDomainController** verwenden dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben sind.

Das Argument **SafeModeAdministratorPassword** funktioniert etwas anders:

-   wenn als Argument *nicht angegeben* , fordert das Cmdlet Sie auf, ein maskiertes Kennwort einzugeben und zu bestätigen. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.

    Um z. B. eine neue untergeordnete Domäne namens NorthAmerica in der Contoso.com-Gesamtstruktur zu erstellen und zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert zu werden:

    ```
    Install-ADDSDomain "NewDomainName NorthAmerica "ParentDomainName Contoso.com "DomainType Child
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
> Das Bereitstellen oder Speichern eines Klartext- oder abgeblendeten Kennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen zusehen, kennen dann das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort extrahieren. Mit diesem Wissen können sich diese an einem Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden, einen Identitätswechsel für den Domänencontroller selbst ausführen und ihre Rechte in einer AD-Gesamtstruktur auf die höchste Stufe heraufstufen. Zusätzliche Schritte mit **System.Security.Cryptography** zur Verschlüsselung der Textdatei werden empfohlen, sind jedoch nicht Teil dieser Anleitung. Generell sollten Sie es vermeiden, Kennwörter zu speichern.

Das ADDSDeployment-Modul bietet eine zusätzliche Option zum Überspringen der automatischen Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Dies ist im Server-Manager nicht konfigurierbar. Dieses Argument ist nur relevant, wenn Sie den DNS-Server vor der Konfiguration des Domänencontrollers bereits installiert haben:

```
-SkipAutoConfigureDNS

```

### <a name="dns-options-and-dns-delegation-credentials"></a>DNS-Optionen und DNS-Delegierungs-Anmeldeinformationen
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDNSOptions.png)

Auf der Seite **DNS-Optionen** können Sie alternative DNS-Administratoranmeldeinformationen für die Delegierung einrichten.

Bei der Installation einer neuen Domäne in einer vorhandene Gesamtstruktur – falls Sie DNS-Installation auf der Seite **Domänencontrolleroptionen** ausgewählt haben – können Sie keine Optionen konfigurieren. Die Delegierung erfolgt automatisch und unwiderruflich. Sie können alternative DNS-Administratoranmeldeinformationen eingeben, die Berechtigungen zur Änderung dieser Struktur haben.

Die Argumente des Windows PowerShell-Cmdlets "ADDSDeployment" für die **DNS-Optionen** sind:

```
-creatednsdelegation
-dnsdelegationcredential <pscredential>
```

Weitere Informationen zur DNS-Delegierung finden Sie unter [Grundlegendes zur Zonendelegierung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771640(v=ws.11)).

### <a name="additional-options"></a>Zusätzliche Optionen
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildAdditionalOptions.png)

Auf der Seite **Zusätzliche Optionen** wird der NetBIOS-Name der Domäne angezeigt, und es besteht die Möglichkeit, den Namen zu überschreiben. Standardmäßig stimmt der NetBIOS-Domänenname mit dem linken Teil des vollqualifizierten Domänennamens überein, der auf der Seite **Bereitstellungskonfiguration** eingegeben wurde. Wenn Sie z. B. den vollqualifizierten Domänennamen corp.contoso.com eingegeben haben, dann ist der Standard-NetBIOS-Name CORP.

Wenn der Name maximal 15 Zeichen lang ist und nicht mit anderen NetBIOS-Namen in Konflikt steht, wird er nicht verändert. Falls der Name mit einem anderen NetBIOS-Namen in Konflikt steht, wird eine Nummer an den Namen angefügt. Wenn der Name länger als 15 Zeichen ist, schlägt der Assistent einen eindeutigen, abgeschnittenen Namen vor. In beiden Fällen prüft der Assistent zunächst mit einer WINS-Suche und einem NetBIOS-Broadcast, ob der Name bereits vergeben ist.

Weitere Informationen zu DNS-Namen finden Sie unter [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](https://support.microsoft.com/kb/909264).

Die **Install-AddsDomain** -Argumente verwenden dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben sind. Für die **DomainNetBIOSName** -Operation gelten Sonderregeln:

1.  Wenn das **NewDomainNetBIOSName** -Argument nicht mit einem NetBIOS-Domänennamen angegeben wird und das einteilige Präfix des Domänennamens im **DomainName** -Argument maximal 15 Zeichen lang ist, wird die Heraufstufung mit einem automatisch generierten Namen fortgesetzt.

2.  Wenn das **NewDomainNetBIOSName** -Argument nicht mit einem NetBIOS-Domänennamen angegeben wird und das einteilige Präfix des Domänennamens im **DomainName** -Argument mehr als 16 Zeichen lang ist, missling die Heraufstufung.

3.  Wenn das **NewDomainNetBIOSName** -Argument mit einem NetBIOS-Domänennamen mit maximal 15 Zeichen angegeben ist, wird die Heraufstufung mit diesem angegebenen Namen fortgesetzt.

4.  Wenn das **NewDomainNetBIOSName** -Argument mit einem NetBIOS-Domänennamen mit mehr als 16 Zeichen angegeben ist, misslingt die Heraufstufung.

Das ADDSDeployment Windows PowerShell-Argument für **Zusätzliche Optionen** ist:

```
-newdomainnetbiosname <string>
```

### <a name="paths"></a>Paths
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)

Auf der Seite **Pfade** können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von %systemroot%.

Die ADDSDeployment Windows PowerShell-Argumente für **Pfade** sind:

```
-databasepath <string>
-logpath <string>
-sysvolpath <string>
```

### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildReviewOptions.png)

Auf der Seite **Optionen prüfen** können Sie vor dem Starten der Installation Ihre Einstellungen überprüfen und sicherstellen, dass Ihre Anforderungen erfüllt werden. Dies ist jedoch nicht die letzte Möglichkeit, um die Installation mit Server-Manager zu stoppen. Dies ist lediglich eine Option zum Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetze

Die Seite **Optionen prüfen** im Server-Manager bietet zudem die optionale Schaltfläche **Skript anzeigen** zum Erstellen einer Unicode-Textdatei, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dies ermöglicht Ihnen die Verwendung der grafischen Oberfläche von Server-Manager als Windows PowerShell-Bereitstellungsstudio. Mithilfe des Konfigurations-Assistenten für die Active Directory-Domänendienste können Sie Optionen konfigurieren, die Konfiguration exportieren und den Assistenten abbrechen.  Bei diesem Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Beispiel:

```
#
# Windows PowerShell Script for AD DS Deployment
#

Import-Module ADDSDeployment
Install-ADDSDomain `
-NoGlobalCatalog:$false `
-CreateDNSDelegation `
-Credential (Get-Credential) `
-DatabasePath "C:\Windows\NTDS" `
-DomainMode "Win2012" `
-DomainType "ChildDomain" `
-InstallDNS:$true `
-LogPath "C:\Windows\NTDS" `
-NewDomainName "research" `
-NewDomainNetBIOSName "RESEARCH" `
-ParentDomainName "corp.contoso.com" `
-Norebootoncompletion:$false `
-SiteName "Default-First-Site-Name" `
-SYSVOLPath "C:\Windows\SYSVOL"
-Force:$true

```

> [!NOTE]
> Server-Manager füllt bei der Heraufstufung normalerweise alle Argumente mit Werten aus und verlässt sich nicht auf Standardwerte (da sich diese in zukünftigen Windows-Versionen oder Service Packs ändern können). Die einzige Ausnahme hierbei ist das **-safemodeadministratorpassword** -Argument (das im Skript bewusst ausgelassen wird). Lassen Sie dieses Argument bei der interaktiven Ausführung des Cmdlets aus, um eine Bestätigungsaufforderung zu erzwingen.

Verwenden Sie das optionale **Whatif** -Argument für das Cmdlet **Install-ADDSForest** , um die Konfigurationsinformationen zu überprüfen. Auf diese Weise können Sie die impliziten und expliziten Argumentwerte für ein Cmdlet anzeigen.

![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildWhatIf.png)

### <a name="prerequisites-check"></a>Voraussetzungsüberprüfung
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildPrereqCheck.png)

Die **Voraussetzungsüberprüfung** ist ein neues Feature in der AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration in der Lage ist, eine neue AD DS-Domäne zu unterstützen.

Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Konfigurations-Assistent für Active Directory-Domänendienste im Server-Manager eine Reihe serialisierter, modularer Tests auf. Diese Tests geben anschließend Empfehlungen für Reparaturoptionen aus. Sie können die Tests beliebig oft ausführen. Der Prozess für den Domänencontroller kann erst fortgesetzt werden, wenn alle Voraussetzungstests positiv abgeschlossen wurden.

Bei der **Voraussetzungsüberprüfung** werden außerdem relevante Informationen wie z. B. Sicherheitsänderungen angezeigt, die ältere Betriebssysteme betreffen.

Weitere Informationen zu den Voraussetzungsprüfungen finden Sie unter [Voraussetzungsüberprüfung](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).

Bei Verwendung des Server-Managers können Sie die **Voraussetzungsüberprüfung** nicht überspringen. Sie können diese jedoch mit dem folgenden Argument überspringen, wenn Sie das Cmdlet "ADDSDeployment" verwenden:

```
-skipprechecks
```

> [!WARNING]
> Microsoft rät davon ab, die Voraussetzungsüberprüfung zu überspringen, da dies zu einer teilweisen Heraufstufung des Domänencontrollers oder zu einer beschädigten AD DS-Gesamtstruktur führen kann.

Klicken Sie auf **Installieren** , um mit der Domänencontroller-Heraufstufung zu beginnen. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Der Heraufstufungsprozess kann während der Ausführung nicht unterbrochen werden. Der Computer wird nach der Heraufstufung automatisch neu gestartet, unabhängig von deren Ergebnis.

### <a name="installation"></a>Installation
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildInstallation.png)

Wenn die Seite **Installation** angezeigt wird, beginnt die Konfiguration des Domänencontrollers und kann nicht angehalten oder abgebrochen werden. Detaillierte Informationen werden auf dieser Seite angezeigt und in die Protokolle geschrieben:

-   %systemroot%\debug\dcpromo.log

-   %systemroot%\debug\dcpromoui.log

Verwenden Sie das folgenden Cmdlet, um eine neue Active Directory-Domäne mithilfe des ADDSDeployment-Moduls zu installieren:

```
Install-addsdomain
```

Siehe [Untergeordnete und Strukturdomänen in Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS) für benötigte und optionale Argumente. Das **Install-addsdomain** -Cmdlet besteht nur aus zwei Phasen (Voraussetzungsüberprüfung und Installation). Die beiden folgenden Abbildungen zeigen die Installationsphase mit den benötigten Mindestargumenten **-domaintype** , **-newdomainname** , - **parentdomainname** und **-credential** . Ebenso wie beim Server-Manager werden Sie von **Install-ADDSDomain** darauf hingewiesen, dass der Server beim Heraufstufen automatisch neu gestartet wird.

![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomain.png)

![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomainProgress.png)

Mit dem **-force** -Argument oder dem **-confirm:$false** -Argument können Sie den Neustart in allen Windows PowerShell-Cmdlets vom Typ "ADDSDeployment" automatisch akzeptieren. Verwenden Sie das **-norebootoncompletion** -Argument, um den automatischen Neustart am Ende der Heraufstufung zu verhindern.

> [!WARNING]
> Es wird davon abgeraten, den Neustart zu verhindern. Der Domänencontroller muss neu gestartet werden, um korrekt zu funktionieren

### <a name="results"></a>Ergebnisse
![Neues untergeordnetes Ad-Element installieren](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)

Auf der Seite **Ergebnisse** werden Erfolg bzw. Misserfolg der Heraufstufung sowie alle wichtigen Administrationsinformationen angezeigt. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.
