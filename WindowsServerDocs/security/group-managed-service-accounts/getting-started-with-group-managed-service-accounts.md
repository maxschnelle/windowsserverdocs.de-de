---
title: Erste Schrittemit Gruppe von verwalteten Dienstkonten
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: cd1e92f93701e5b430d1425fcf9a2f3590d1fe5d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="getting-started-with-group-managed-service-accounts"></a>Erste Schrittemit Gruppe von verwalteten Dienstkonten

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016


Dieses Handbuch enthält schrittweise Anweisungen und Hintergrundinformationen zur Aktivierung und Verwendung von Gruppenverwalteten Dienstkonten in Windows Server 2012.

**In diesem Dokument**

-   [Erforderliche Komponenten](#BKMK_Prereqs)

-   [Einführung in](#BKMK_Intro)

-   [Bereitstellen einer neuen Serverfarm](#BKMK_DeployNewFarm)

-   [Hinzufügen von mitgliedshosts zu einer vorhandenen Serverfarm](#BKMK_AddMemberHosts)

-   [Aktualisieren Sie die Group-Managed Service Account-Eigenschaften](#BKMK_Update_gMSA)

-   [Außerbetriebsetzung von mitgliedshosts in einer vorhandenen Serverfarm](#BKMK_DecommMemberHosts)


> [!NOTE]
> Dieses Thema enthält Beispiel für Windows PowerShell-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="BKMK_Prereqs"></a>Erforderliche Komponenten
Finden Sie im Abschnitt in diesem Thema [Anforderungen für Gruppenverwaltete Dienstkonten](#BKMK_gMSA_Req).

## <a name="BKMK_Intro"></a>Einführung in
Wenn ein Clientcomputer mit einem Dienst verbunden die in einer Serverfarm mit Netzwerklastenausgleich (NLB) oder einer anderen Methode gehostet wird wird, in dem alle Server angezeigt werden, um denselben Dienst an den Client werden, können z. B. Kerberos gegenseitigen Authentifizierung unterstützende Authentifizierungsprotokolle verwendet werden, es sei denn, alle Instanzen der Dienste den gleichen Prinzipal verwenden. Dies bedeutet, dass jeder Dienst dieselben Kennwörter/Schlüssel zu nutzen, um ihre Identität zu bestätigen.

> [!NOTE]
> Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe sind oder gMSA oder sMSA systemeigen zu unterstützen.

Dienste verfügen über die folgenden Prinzipale, aus denen auswählen, und jeder hat bestimmte Begrenzungen.

|Sicherheitsprinzipale|Bereich|Dienste, die unterstützt|Kennwortverwaltung|
|-------|-----|-----------|------------|
|Computer-Konto von Windows-system|Domäne|Beschränkt auf einer Domäne beigetreten server|Computer verwaltet|
|Computerkonto ohne Windows-system|Domäne|Alle Server innerhalb der Domäne|Keine|
|Virtuellen Kontos|Lokale|Auf einen Server begrenzt|Computer verwaltet|
|Windows 7 Standalone Managed Service Account|Domäne|Beschränkt auf einer Domäne beigetreten server|Computer verwaltet|
|Benutzerkonto|Domäne|Alle Server innerhalb der Domäne|Keine|
|Gruppenverwaltetes Dienstkonto|Domäne|Server für alle Windows Server 2012-Domäne|Der Domänencontroller verwaltet, und der Host Ruft ab|

Ein Windows-Computerkonto oder ein eigenständiges Windows 7 Managed Service Account (sMSA), oder virtuelle Konten können nicht über mehrere Systeme hinweg freigegeben werden. Wenn Sie ein Konto für Dienste auf freizugebenden Serverfarmen konfigurieren, müssten Sie ein Benutzerkonto oder ein Computerkonto abgesehen von einem Windows-System zu wählen. In beiden Fällen ist für diese Konten nicht die Möglichkeit, Single Point of Control kennwortverwaltung erforderlich. Dies führt zu einem Problem, in denen muss jede Organisation eine teure Lösung, um Schlüssel für den Dienst in Active Directory aktualisieren und verteilen Sie die Schlüssel in allen Instanzen dieser Dienste erstellen.

Mit Windows Server 2012 müssen Dienste oder Dienstadministratoren nicht zum Verwalten von kennwortsynchronisierung zwischen Dienstinstanzen bei Verwendung von Gruppenverwalteten Dienstkonten (gMSA). Sie gMSA in Active Directory bereitstellen und konfigurieren Sie den Dienst, der von verwalteten Dienstkonten unterstützt. Sie können bereitstellen, ein gruppenverwaltetes Dienstkonto mithilfe der *-ADServiceAccount-Cmdlets, die Teil der Active Directory-Modul. Die dienstidentitätskonfiguration auf dem Host wird von unterstützt:

-   Dieselben APIs wie sMSA, sodass Produkte, die sMSA unterstützen, werden gMSA unterstützen.

-   Dienste, die Service Control Manager zum Konfigurieren der anmeldeidentität verwenden

-   Dienste, die den IIS-Manager für Anwendungspools Konfiguration der Identität verwenden

-   Aufgaben, die mithilfe der Aufgabenplanung.

### <a name="BKMK_gMSA_Req"></a>Anforderungen für Gruppenverwaltete Dienstkonten
Die folgende Tabelle enthält die betriebssystemanforderungen für Kerberos-Authentifizierung mit Diensten mithilfe von gMSA funktioniert. Die Active Directory-Anforderungen werden nach der Tabelle aufgeführt.

Eine 64-Bit-Architektur ist erforderlich, zum Ausführen der Windows PowerShell-Befehle zum Verwalten von Gruppenverwalteten Dienstkonten verwendet.

**Betriebssystemanforderungen**

|Element|Anforderung|Betriebssystem|
|------|--------|----------|
|Host der Clientanwendung|RFC-konformer Kerberos-client|Mindestens Windows XP|
|Domänencontroller für Domäne des Benutzerkontos|RFC-konformer KDC|Mindestens WindowsServer 2003|
|Mitgliederhosts für freigegebene Dienste|| Windows Server 2012 |
|Domänencontroller für Domäne des mitgliedhosts|RFC-konformer KDC|Mindestens WindowsServer 2003|
|Domänencontroller für Domäne des gMSA-Kontos| Windows Server 2012-Domänencontroller für den Host zum Abrufen des Kennworts verfügbare|Domäne mit Windows Server 2012 die einige Systeme früher als Windows Server 2012 haben kann |
|Back-End-Diensthost|RFC kompatiblen Kerberos-Anwendungsserver|Mindestens WindowsServer 2003|
|Domänencontroller für Domäne des Back-End-Dienstkonto|RFC-konformer KDC|Mindestens WindowsServer 2003|
|WindowsPowerShell für Active Directory|Windows PowerShell für Active Directory, die lokal auf einem Computer unterstützt eine 64-Bit-Architektur oder auf Ihrem Remoteverwaltungscomputer (beispielsweise mithilfe der Remoteserver-Verwaltungstoolkits) installiert.| Windows Server 2012 |

**Anforderungen für Active Directory-Domänendienste**

-   Active Directory-Schema in einer Gesamtstruktur der gMSA-Domäne muss aktualisiert werden, um Windows Server 2012, um ein gMSA zu erstellen.

    Sie können das Schema aktualisieren, Installieren eines Domänencontrollers, das Windows Server 2012 ausgeführt wird oder durch die Version von adprep.exe auf einem Computer unter Windows Server 2012 ausführen. Der Attributwert Objekt-Version für das Objekt CN = Schema, CN = Configuration, DC = Contoso, DC = Com "52" sein muss.

-   Neues Gruppenverwaltetes Dienstkonto

-   Bei der Verwaltung der Service Host die Berechtigung zum Verwenden von gMSA nach Gruppe dann neue oder vorhandene Sicherheitsgruppe

-   Verwalten der dienstzugriffssteuerung nach Gruppe dann neue oder vorhandene Sicherheitsgruppe

-   Wenn der erste hauptstammschlüssel für Active Directory nicht in der Domäne bereitgestellt wird oder nicht erstellt wurde, erstellen Sie ihn. Die Ergebnisse seiner Erstellung kann im KdsSvc-Betriebsprotokoll, Ereignis-ID 4004 überprüft werden.

Eine Anleitung zum Erstellen des Schlüssels finden Sie unter [erstellen Sie den Schlüssel Verteilung KDS-Stammschlüssels](create-the-key-distribution-services-kds-root-key.md). Microsoft-Schlüsselverteilungsdienst ("kdssvc.dll") der Stammschlüssel für Active Directory.

**Lebenszyklus**

Der Lebenszyklus einer Serverfarm das gMSA-Feature in der Regel umfasst die folgenden Aufgaben:

-   Bereitstellen einer neuen Serverfarm

-   Hinzufügen von mitgliedshosts zu einer vorhandenen Serverfarm

-   Außerbetriebsetzung von mitgliedshosts in einer vorhandenen Serverfarm

-   Außerbetriebsetzung einer vorhandenen Serverfarm

-   Entfernen eines gefährdeten mitgliedhosts aus einer Serverfarm, falls erforderlich.

## <a name="BKMK_DeployNewFarm"></a>Bereitstellen einer neuen Serverfarm
Wenn Sie eine neue Serverfarm bereitstellen, müssen der Dienstadministrator zu bestimmen:

-   Wenn der Dienst mithilfe von gMSAs unterstützt

-   Wenn der Dienst eingehende oder ausgehende authentifizierte Verbindungen erforderlich sind.

-   Die Computerkontennamen für die mitgliedhosts für den Dienst mithilfe des Gmsas

-   Den NetBIOS-Namen für den Dienst

-   Der DNS-Hostnamen für den Dienst

-   Die Dienstprinzipalnamen (SPN) für den Dienst

-   Das Kennwortänderungsintervall (Standard ist 30 Tage).

### <a name="BKMK_Step1"></a>Schritt 1: Bereitstellen Gruppenverwalteter Dienstkonten
Sie können ein gMSA erstellen, nur dann, wenn das Gesamtstrukturschema auf Windows Server 2012 wurde, der hauptstammschlüssel für Active Directory bereitgestellt wurde und es ist mindestens Windows Server 2012-Domänencontroller in der Domäne, in der das gMSA erstellt wird.

Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Erstellen von "MsDS-groupmanagedserviceaccount"-Objekten ist mindestens erforderlich, um die folgenden Verfahren auszuführen.

#### <a name="BKMK_CreateGMSA"></a>So erstellen Sie ein gMSA mithilfe des Cmdlets New-ADServiceAccount

1.  Führen Sie Windows PowerShell auf dem Windows Server 2012-Domänencontroller auf der Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für die Windows PowerShell und drücken Sie dann die EINGABETASTE. (Active Directory-Modul wird automatisch geladen.)

    **New-ADServiceAccount [-Name] <string> DNSHostName - <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >] - SamAccountName <string> - Dienstprinzipalnamen (SPN) < String [] >**

    |Parameter|Zeichenfolge|Beispiel|
    |-------|-----|------|
    |Name|Name des Kontos|"Itfarm1" zu|
    |DNSHostName|DNS-Hostname des Diensts|ITFarm1.contoso.com|
    |KerberosEncryptionType|Alle durch die Hostserver unterstützte Verschlüsselungstyp|RC4, AES128, AES256|
    |ManagedPasswordIntervalInDays|Kennwortänderungsintervall in Tagen (Standard liegt bei 30 Tagen andernfalls bereitgestellt)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des mitgliedhosts oder der Sicherheitsgruppe, der das Mitglied hostet Mitglied sind.|ITFarmHosts|
    |"SAMAccountName"|NetBIOS-name für den Dienst, falls nicht denselben Namen wie|"Itfarm1" zu|
    |Dienstprinzipalnamen (SPN)|Dienstprinzipalnamen (SPN) für den Dienst|http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http / "itfarm1" zu/contoso|

    > [!IMPORTANT]
    > Das Kennwortänderungsintervall kann nur während der Erstellung festgelegt werden. Wenn Sie das Intervall ändern möchten, müssen Sie ein neues gMSA erstellen, und legen sie zum Zeitpunkt der Erstellung.

    **Beispiel**

    Geben Sie den Befehl in einer einzelnen Zeile, auch wenn es über mehrere Zeilen umgebrochen möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**, oder Fähigkeit zum Erstellen von "MsDS-groupmanagedserviceaccount"-Objekten ist mindestens erforderlich, um dieses Verfahren ausführen. Ausführliche Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänenstandardgruppen](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>So erstellen Sie ein gMSA für die ausgehende Authentifizierung nur mit dem Cmdlet "New-ADServiceAccount"

1.  Führen Sie Windows PowerShell auf dem Windows Server 2012-Domänencontroller auf der Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **New-ADServiceAccount [-Name] <string> - RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays < Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >]**

    |Parameter|Zeichenfolge|Beispiel|
    |-------|-----|------|
    |Name|Benennen Sie das Konto|"Itfarm1" zu|
    |ManagedPasswordIntervalInDays|Kennwortänderungsintervall in Tagen (Standard liegt bei 30 Tagen andernfalls bereitgestellt)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des mitgliedhosts oder der Sicherheitsgruppe, der das Mitglied hostet Mitglied sind.|ITFarmHosts|

    > [!IMPORTANT]
    > Das Kennwortänderungsintervall kann nur während der Erstellung festgelegt werden. Wenn Sie das Intervall ändern möchten, müssen Sie ein neues gMSA erstellen, und legen sie zum Zeitpunkt der Erstellung.

**Beispiel**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>Schritt 2: Konfigurieren des Dienstidentitäts-Anwendungsdiensts
Konfigurieren der Dienste in Windows Server 2012 finden Sie in der folgenden Featuredokumentation:

-   IIS-Anwendungspool

    Weitere Informationen finden Sie unter [angeben einer Identität für einen Anwendungspool (IIS 7)](https://technet.microsoft.com/library/cc771170(WS.10).aspx).

-   Windows-Dienste

    Weitere Informationen finden Sie unter [Dienste](https://technet.microsoft.com/library/cc772408.aspx).

-   Aufgaben

    Weitere Informationen finden Sie in der [Übersicht über den Taskplaner](https://technet.microsoft.com/library/cc721871.aspx).

Andere Dienste könnten gMSA unterstützen. Finden Sie die entsprechende Produktdokumentation Details dazu, wie diese Dienste zu konfigurieren.

## <a name="BKMK_AddMemberHosts"></a>Hinzufügen von mitgliedshosts zu einer vorhandenen Serverfarm
Wenn Sicherheitsgruppen für die Verwaltung von mitgliedshosts, fügen Sie das Computerkonto für den neuen mitgliedhosts zur Sicherheitsgruppe (die mitgliedhosts des Mitglied sind) eine der folgenden Methoden verwenden.

Mitgliedschaft in **Domänen-Admins**, oder die Möglichkeit, die Mitglieder der Sicherheitsgruppenobjekt hinzuzufügen ist mindestens erforderlich, um diese Verfahren abzuschließen.

-   Methode 1: Active Directory-Benutzer und-Computer

    Verfahren zum Verwenden dieser Methode finden Sie unter [hinzufügen ein Computerkontos zu einer Gruppe](https://technet.microsoft.com/library/cc733097.aspx) mithilfe der Windows-Benutzeroberfläche und [Verwalten anderer Domänen im Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

-   Methode 2: "dsmod"

    Verfahren zum Verwenden dieser Methode finden Sie unter [hinzufügen ein Computerkontos zu einer Gruppe](https://technet.microsoft.com/library/cc733097.aspx) über die Befehlszeile.

-   Methode 3: Windows PowerShell Active Directory-Cmdlets Add-ADPrincipalGroupMembership

    Verfahren zum Verwenden dieser Methode finden Sie unter [Add-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx).

Wenn Sie Computerkonten zu verwenden, finden Sie die vorhandenen Konten, und fügen Sie das neue Benutzerkonto hinzu.

Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**, oder die Möglichkeit zum Verwalten von "MsDS-groupmanagedserviceaccount"-Objekten ist die mindestvoraussetzung, um dieses Verfahren ausführen. Ausführliche Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften finden Sie unter Lokale und Domänenstandardgruppen.

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Hinzufügen von mitgliedhosts mit dem Cmdlet Set-ADServiceAccount

1.  Führen Sie Windows PowerShell auf dem Windows Server 2012-Domänencontroller auf der Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **Get-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **Set-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|Parameter|Zeichenfolge|Beispiel|
|-------|-----|------|
|Name|Benennen Sie das Konto|"Itfarm1" zu|
|PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des mitgliedhosts oder der Sicherheitsgruppe, der das Mitglied hostet Mitglied sind.|Host1, Host2, Host3|

**Beispiel**

Z. B. Mitglied hinzufügen Hosts Geben Sie die folgenden Befehle, und drücken Sie dann die EINGABETASTE.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1 Host2 Host3

```

## <a name="BKMK_Update_gMSA"></a>Aktualisieren die Eigenschaften der Managed Service Account
Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**, oder die Berechtigung zum Schreiben in "MsDS-groupmanagedserviceaccount"-Objekten ist mindestens erforderlich, um diese Verfahren abzuschließen.

Öffnen Sie das Active Directory-Modul für Windows PowerShell, und legen Sie eine Eigenschaft mit dem Cmdlet Set-ADServiceAccount.

Detaillierte Informationen zum Festlegen dieser Eigenschaften finden Sie unter [Set-ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) in der TechNet-Bibliothek oder durch Eingabe **Get-Help Set-ADServiceAccount** an Active Directory-Modul für Windows PowerShell command Prompt und betätigen Sie.

## <a name="BKMK_DecommMemberHosts"></a>Außerbetriebsetzung von mitgliedshosts in einer vorhandenen Serverfarm
Mitgliedschaft in **Domänen-Admins**, oder die Möglichkeit, Mitglieder aus dem Sicherheitsgruppenobjekt zu entfernen, ist mindestens erforderlich, um diese Verfahren abzuschließen.

### <a name="step-1-remove-member-host-from-gmsa"></a>Schritt 1: Entfernen von mitgliedhosts vom gMSA
Wenn Sicherheitsgruppen für die Verwaltung von mitgliedshosts, entfernen Sie das Computerkonto für den deaktivierten mitgliedhost aus der Sicherheitsgruppe, die mitgliedhosts mithilfe einer der folgenden Methoden gehören.

-   Methode 1: Active Directory-Benutzer und-Computer

    Verfahren zum Verwenden dieser Methode finden Sie unter [Löschen eines Computerkontos](https://technet.microsoft.com/library/cc754624.aspx) mithilfe der Windows-Benutzeroberfläche und [Verwalten anderer Domänen im Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

-   Methode 2: "drsm"

    Verfahren zum Verwenden dieser Methode finden Sie unter [Löschen eines Computerkontos](https://technet.microsoft.com/library/cc754624.aspx) über die Befehlszeile.

-   Methode 3: Windows PowerShell Active Directory-Cmdlet Remove-ADPrincipalGroupMembership

    Detaillierte Informationen hierzu finden Sie unter [Remove-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) in der TechNet-Bibliothek oder durch Eingabe **Get-Help Remove-ADPrincipalGroupMembership** an Active Directory-Modul für Windows PowerShell command Prompt und betätigen Sie.

Wenn Sie Computerkonten auflisten, rufen Sie die vorhandenen Konten ab, und fügen Sie alle mit Ausnahme des entfernten Computerkontos.

Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**, oder die Möglichkeit zum Verwalten von "MsDS-groupmanagedserviceaccount"-Objekten ist die mindestvoraussetzung, um dieses Verfahren ausführen. Ausführliche Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften finden Sie unter Lokale und Domänenstandardgruppen.

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>So entfernen Sie Hosts mithilfe von das Cmdlet "Set-ADServiceAccount"

1.  Führen Sie Windows PowerShell auf dem Windows Server 2012-Domänencontroller auf der Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **Get-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **Set-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|Parameter|Zeichenfolge|Beispiel|
|-------|-----|------|
|Name|Benennen Sie das Konto|"Itfarm1" zu|
|PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des mitgliedhosts oder der Sicherheitsgruppe, der das Mitglied hostet Mitglied sind.|Host1 Host3|

**Beispiel**

Z. B. zum Entfernen Hosts Geben Sie die folgenden Befehle, und drücken Sie dann die EINGABETASTE.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1 Host3

```

### <a name="BKMK_RemoveGMSA"></a>Schritt 2: Entfernen eines Gruppenverwalteten Dienstkontos aus dem system
Entfernen Sie die zwischengespeicherten gruppenverwalteten Dienstkonto-Anmeldeinformationen aus dem mitgliedhost mithilfe des Uninstall-ADServiceAccount oder die NetRemoveServiceAccount-API auf dem Hostsystem.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Verfahren abzuschließen.

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>So entfernen Sie ein gMSA verwenden das Cmdlet "Uninstall-ADServiceAccount"

1.  Führen Sie Windows PowerShell auf dem Windows Server 2012-Domänencontroller auf der Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **< ADServiceAccount > Uninstall-ADServiceAccount**

    **Beispiel**

    Beispielsweise so entfernen Sie die zwischengespeicherten Anmeldeinformationen für ein gruppenverwaltetes Dienstkonto mit dem Namen "itfarm1" zu geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

Weitere Informationen über das Cmdlet Uninstall-ADServiceAccount an der Active Directory-Modul für Windows PowerShell-Eingabeaufforderung, geben Sie **Get-Help Uninstall-ADServiceAccount**, und klicken Sie dann drücken Sie die EINGABETASTE, oder konsultieren Sie die Informationen auf der TechNet-Website unter [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx).



## <a name="BKMK_Links"></a>Siehe auch

-   [Gruppe verwaltete Dienstkonten: Übersicht](group-managed-service-accounts-overview.md)



