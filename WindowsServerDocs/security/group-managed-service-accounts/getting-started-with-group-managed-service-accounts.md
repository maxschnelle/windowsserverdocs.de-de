---
title: Erste Schritte mit gruppenverwalteten Dienstkonten
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
ms.openlocfilehash: 6da212185eb47d3f30f81ca6f1eb322bc232e229
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881451"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>Erste Schritte mit gruppenverwalteten Dienstkonten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


Dieses Handbuch enthält detaillierte Anweisungen und Hintergrundinformationen für die Aktivierung und Verwendung von gruppenverwalteten Dienstkonten in Windows Server 2012.

**In diesem Dokument**

-   [Erforderliche Komponenten](#BKMK_Prereqs)

-   [Einführung](#BKMK_Intro)

-   [Bereitstellen einer neuen Serverfarm](#BKMK_DeployNewFarm)

-   [Hinzufügen von mitgliedshosts zu einer vorhandenen Serverfarm](#BKMK_AddMemberHosts)

-   [Aktualisieren Sie die Eigenschaften des Gruppenverwalteten Dienstkontos](#BKMK_Update_gMSA)

-   [Außerbetriebsetzung von mitgliedshosts in einer vorhandenen Serverfarm](#BKMK_DecommMemberHosts)


> [!NOTE]
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="BKMK_Prereqs"></a>Erforderliche Komponenten
Informationen hierzu finden Sie in diesem Thema im Abschnitt [Anforderungen für gruppenverwaltete Dienstkonten](#BKMK_gMSA_Req).

## <a name="BKMK_Intro"></a>Einführung in
Wenn sich ein Clientcomputer mit einem auf einer Serverfarm gehosteten Dienst mithilfe des Netzwerklastenausgleichs (Network Load Balancing, NLB) oder einer anderen Methode verbindet, in der der Client alle Server als gleichen Dienst interpretiert, dann können die gegenseitige Authentifizierung unterstützende Authentifizierungsprotokolle wie Kerberos nicht verwendet werden, es sei denn, alle Instanzen der Dienste verwenden denselben Prinzipal. Das heißt, dass jeder Dienst dieselben Kennwörter/Schlüssel zum Beweisen der entsprechenden Identität verwenden muss.

> [!NOTE]
> Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt werden, können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe oder gMSA oder sMSA systemeigen unterstützen.

Dienste verfügen über die folgenden Prinzipale, aus denen ausgewählt werden kann, und jeder hat bestimmte Begrenzungen.

|Prinzipale|Bereich|Unterstützte Dienste|Kennwortverwaltung|
|-------|-----|-----------|------------|
|Computerkonto von Windows-System|Domäne|Auf einen mit einer Domäne verbundenen Server|Vom Computer verwaltet|
|Computerkonto ohne Windows-System|Domäne|Jeder mit einer Domäne verbundene Server|Keine|
|Virtuelles Konto|Lokal|Auf einen Server begrenzt|Vom Computer verwaltet|
|Eigenständig verwaltetes Windows 7-Dienstkonto|Domäne|Auf einen mit einer Domäne verbundenen Server|Vom Computer verwaltet|
|Benutzerkonto|Domäne|Jeder mit einer Domäne verbundene Server|Keine|
|Gruppenverwaltetes Dienstkonto|Domäne|Eine beliebige Domäne eingebundenen Windows Server 2012-server|Der Domänencontroller verwaltet, und der Host ruft ab|

Ein Windows-Computerkonto oder ein eigenständiges verwaltetes Windows 7-Dienstkonto (standalone Managed Service Account, sMSA) oder virtuelle Konten können nicht über mehrere Systeme hinweg freigegeben werden. Wenn Sie ein Konto für Dienste auf freizugebenden Serverfarmen konfigurieren, müssten Sie getrennt vom Windows-System ein Benutzer- oder Computerkonto auswählen. So oder so verfügen diese Konten nicht über die Fähigkeit der Kennwortverwaltung über einen einzigen Steuerungspunkt. Dies führt zu einem Problem, wobei jede Organisation eine teure Lösung erstellen muss, um die Schlüssel für den Dienst in Active Directory zu aktualisieren und anschließend die Schlüssel in allen Instanzen dieser Dienste bereitzustellen.

In Windows Server 2012 müssen Dienste oder Dienstadministratoren nicht zum Verwalten der kennwortsynchronisierung zwischen Dienstinstanzen, die bei Verwendung von gruppenverwalteten Dienstkonten (gMSA). Sie stellen die gruppenverwalteten Dienstkonten in Active Directory bereit und konfigurieren anschließend den Dienst, der verwaltete Dienstkonten unterstützt. Sie können ein gruppenverwaltetes Dienstkonto mithilfe der Cmdlets „*-ADServiceAccount“ bereitstellen, die Bestandteil des Active Directory-Moduls sind. Die Dienstidentitätskonfiguration auf dem Host wird unterstützt durch:

-   Dieselben APIs wie sMSA, sodass Produkte, die sMSA unterstützen, auch gMSA unterstützen

-   Dienste, die den Dienststeuerungs-Manager zum Konfigurieren der Anmeldeidentität verwenden

-   Dienste, die den IIS-Manager für Anwendungspools zwecks Konfiguration der Identität verwenden

-   Aufgaben mithilfe der Aufgabenplanung.

### <a name="BKMK_gMSA_Req"></a>Anforderungen für Gruppenverwaltete Dienstkonten: Übersicht
Die folgende Tabelle führt die Betriebssystemanforderungen auf, damit die Kerberos-Authentifizierung mit Diensten mithilfe von gMSA funktioniert. Die Active Directory-Anforderungen sind im Anschluss an die Tabelle aufgeführt.

Zum Ausführen der Windows PowerShell-Befehle ist eine 64-Bit-Architektur erforderlich, die zum Verwalten von gruppenverwalteten Dienstkonten (group Managed Service Accounts, gMSA) verwendet werden.

**Betriebssystemanforderungen**

|Element|Anforderung|Betriebssystem|
|------|--------|----------|
|Host der Clientanwendung|RFC-konformer Kerberos-Client|Mindestens Windows XP|
|Domänencontroller für Domäne des Benutzerkontos|RFC-konformer KDC|Mindestens Windows Server 2003|
|Mitgliederhosts für freigegebene Dienste|| Windows Server 2012 |
|Domänencontroller für Domäne des mitgliedhosts|RFC-konformer KDC|Mindestens Windows Server 2003|
|Domänencontroller für Domäne des gMSA-Kontos| Windows Server 2012-Domänencontroller für den Host zum Abrufen des Kennworts verfügbare|Domäne mit Windows Server 2012, die einige Systeme früher als Windows Server 2012 haben kann |
|Back-End-Diensthost|RFC-konformer Kerberos-Anwendungsserver|Mindestens Windows Server 2003|
|Domänencontroller für Domäne des Back-End-Dienstkonto|RFC-konformer KDC|Mindestens Windows Server 2003|
|Windows PowerShell für Active Directory|Die lokal auf einem Computer oder auf Ihrem Remoteverwaltungscomputer (beispielsweise mithilfe des Remoteserver-Verwaltungstoolkits) installierte Windows PowerShell für Active Directory, die eine 64-Bit-Architektur unterstützt.| Windows Server 2012 |

**Anforderungen für Active Directory Domain Services**

-   Active Directory-Schema in einer Gesamtstruktur der gMSA-Domäne muss auf Windows Server 2012, erstellen Sie ein gMSA aktualisiert werden.

    Installieren eines Domänencontrollers, das Windows Server 2012 ausgeführt wird oder durch die Version von adprep.exe auf einem Computer unter Windows Server 2012 ausführen, können Sie das Schema aktualisieren. Das Objektversionsattribut für das Objekt „CN=Schema,CN=Configuration,DC=Contoso,DC=Com“ muss „52“ sein.

-   Neues gruppenverwaltetes Dienstkonto

-   Wenn Sie die Diensthostberechtigung verwalten, um das gMSA nach Gruppe zu verwenden, dann neue oder vorhandene Sicherheitsgruppe

-   Beim Verwalten der Dienstzugriffssteuerung nach Gruppe dann neue oder vorhandene Sicherheitsgruppe

-   Wenn erste Hauptstammschlüssel für Active Directory nicht in der Domäne bereitgestellt wird oder nicht erstellt wurde, dann erstellen Sie ihn. Die Ergebnisse seiner Erstellung können im KdsSvc-Betriebsprotokoll unter Ereignis-ID 4004 nachvollzogen werden.

Anweisungen zum Erstellen des Schlüssels finden Sie unter [erstellen Sie den Schlüssel Verteilung KDS-Stammschlüssels](create-the-key-distribution-services-kds-root-key.md). Der Microsoft-Schlüsselverteilungsdienst („kdssvc.dll“) ist der Stammschlüssel für Active Directory.

**Lifecycle**

Der Lebenszyklus einer Serverfarm, die das gMSA-Feature verwendet, umfasst für gewöhnlich folgende Aufgaben:

-   Bereitstellen einer neuen Serverfarm

-   Hinzufügen von Mitgliedshosts zu einer vorhandenen Serverfarm

-   Außerbetriebsetzung von Mitgliedshosts in einer vorhandenen Serverfarm

-   Außerbetriebsetzung einer vorhandenen Serverfarm

-   Entfernen eines gefährdeten Mitgliedhosts aus einer Serverfarm, sofern erforderlich.

## <a name="BKMK_DeployNewFarm"></a>Bereitstellen einer neuen Serverfarm
Beim Bereitstellen einer neuen Serverfarm muss der Dienstadministrator Folgendes bestimmen:

-   Ob der Dienst mithilfe von gMSAs unterstützt wird

-   Ob für den Dienst eingehende oder ausgehende authentifizierte Verbindungen erforderlich sind

-   Die Computerkontennamen für die Mitgliedhosts für den Dienst mithilfe des gMSAs

-   Den NetBIOS-Namen für den Dienst

-   Den DNS-Hostnamen für den Dienst

-   Die Dienstprinzipalnamen für den Dienst

-   Das Kennwortänderungsintervall (Standard liegt bei 30 Tagen)

### <a name="BKMK_Step1"></a>Schritt 1: Bereitstellen gruppenverwalteter Dienstkonten
Sie können ein gruppenverwaltetes Dienstkonto erstellen, nur dann, wenn das Gesamtstrukturschema wurde auf Windows Server 2012 aktualisiert, der hauptstammschlüssel für Active Directory bereitgestellt wurde und mindestens einen Windows Server 2012-Domänencontroller besteht, in der Domäne, in der das gMSA erstellt wird.

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Erstellen von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um die folgenden Verfahren abzuschließen.

#### <a name="BKMK_CreateGMSA"></a>So erstellen Sie ein gMSA mithilfe des Cmdlets New-ADServiceAccount

1.  Führen Sie Windows PowerShell über die Taskleiste, auf dem Windows Server 2012-Domänencontroller.

2.  Geben Sie an der Befehlszeile für die Windows PowerShell die folgenden Befehle ein, und drücken Sie die EINGABETASTE: (Das Active Directory-Modul wird automatisch geladen.)

    **New-ADServiceAccount [-Name] <string> - DNSHostName <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal] >] - SamAccountName <string> - ServicePrincipalNames < Zeichenfolge [] >**

    |Parameter|Zeichenfolge|Beispiel|
    |-------|-----|------|
    |Name|Name des Kontos|ITFarm1|
    |DNSHostName|DNS-Hostname des Diensts|ITFarm1.contoso.com|
    |KerberosEncryptionType|Jeder durch die Hostserver unterstützte Verschlüsselungstyp|RC4, AES128, AES256|
    |ManagedPasswordIntervalInDays|Kennwortänderungsintervall in Tagen (Standard liegt bei 30, wenn keine Angabe erfolgt)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|ITFarmHosts|
    |SamAccountName|NetBIOS-Name für den Dienst, sofern dies nicht „Name“ entspricht|ITFarm1|
    |ServicePrincipalNames|Die Dienstprinzipalnamen für den Dienst|http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso|

    > [!IMPORTANT]
    > Das Kennwortänderungsintervall kann nur während der Erstellung festgelegt werden. Wenn Sie das Intervall ändern möchten, müssen Sie ein neues gMSA erstellen und es zur Erstellungszeit festlegen.

    **Beispiel**

    Geben Sie jeden Befehl in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Erstellen von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um dieses Verfahren abzuschließen. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter [Lokale und Domänenstandardgruppen](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>So erstellen Sie ein gMSA ausschließlich für die ausgehende Authentifizierung mithilfe des Cmdlets „New-ADServiceAccount“

1.  Führen Sie Windows PowerShell über die Taskleiste, auf dem Windows Server 2012-Domänencontroller.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **New-ADServiceAccount [-Name] <string> - RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays < Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >]**

    |Parameter|Zeichenfolge|Beispiel|
    |-------|-----|------|
    |Name|Benennen Sie das Konto|ITFarm1|
    |ManagedPasswordIntervalInDays|Kennwortänderungsintervall in Tagen (Standard liegt bei 30, wenn keine Angabe erfolgt)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|ITFarmHosts|

    > [!IMPORTANT]
    > Das Kennwortänderungsintervall kann nur während der Erstellung festgelegt werden. Wenn Sie das Intervall ändern möchten, müssen Sie ein neues gMSA erstellen und es zur Erstellungszeit festlegen.

**Beispiel**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>Schritt 2: Konfigurieren des Dienstidentitäts-Anwendungsdiensts
Um die Dienste in Windows Server 2012 konfigurieren zu können, finden Sie in der folgenden featuredokumenation:

-   IIS-Anwendungspool

    Weitere Informationen finden Sie unter [Angeben einer Identität für einen Anwendungspool (IIS 7)](https://technet.microsoft.com/library/cc771170(WS.10).aspx).

-   Windows-Dienste

    Weitere Informationen finden Sie unter [Dienste](https://technet.microsoft.com/library/cc772408.aspx).

-   Richtlinienübersicht

    Weitere Informationen finden Sie unter [Aufgabenplanung (Übersicht)](https://technet.microsoft.com/library/cc721871.aspx).

Andere Dienste könnten gMSA unterstützen. Konsultieren Sie die entsprechende Produktdokumentation, um Details darüber zu erhalten, wie diese Dienste zu konfigurieren sind.

## <a name="BKMK_AddMemberHosts"></a>Hinzufügen von mitgliedshosts zu einer vorhandenen Serverfarm
Wenn Sicherheitsgruppen für die Verwaltung von mitgliedshosts zu verwenden, fügen Sie das Computerkonto für den neuen mitgliedhosts der Sicherheitsgruppe (der die mitgliedhosts des Mitglied sind) mit einer der folgenden Methoden.

Die Mitgliedschaft in **Domänen-Admins**oder die Fähigkeit, Mitglieder zum Sicherheitsgruppenobjekt hinzuzufügen, ist die Mindestvoraussetzung zum Abschließen dieser Verfahren.

-   Methode 1: Active Directory-Benutzer und-Computer

    Verfahren zum Verwenden dieser Methode mithilfe der Windows-Benutzeroberfläche finden Sie unter [Hinzufügen eines Computerkontos zu einer Gruppe](https://technet.microsoft.com/library/cc733097.aspx) und [Verwalten unterschiedlicher Domänen im Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

-   Methode 2: „dsmod“

    Verfahren zum Verwenden dieser Methode mithilfe der Befehlszeile finden Sie unter [Hinzufügen eines Computerkontos zu einer Gruppe](https://technet.microsoft.com/library/cc733097.aspx) .

-   Methode 3: Windows PowerShell Active Directory-Cmdlet „Add-ADPrincipalGroupMembership“

    Verfahren zum Verwenden dieser Methode finden Sie unter [Add-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx).

Suchen Sie bei der Verwendung von Benutzerkonten nach vorhandenen Konten, und fügen Sie dann das neue Benutzerkonto hinzu.

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**oder Fähigkeit zum Verwalten von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um dieses Verfahren abzuschließen. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter „Lokale und Domänenstandardgruppen“.

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>So fügen Sie Hosts mithilfe des Cmdlets „Set-ADServiceAccount“ hinzu

1.  Führen Sie Windows PowerShell über die Taskleiste, auf dem Windows Server 2012-Domänencontroller.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **Get-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **Set-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|Parameter|Zeichenfolge|Beispiel|
|-------|-----|------|
|Name|Benennen Sie das Konto|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|Host1, Host2, Host3|

**Beispiel**

Geben Sie beispielsweise zum Hinzufügen von Mitgliedhosts die folgenden Befehle ein, und drücken Sie dann die EINGABETASTE.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1,Host2,Host3

```

## <a name="BKMK_Update_gMSA"></a>Aktualisieren der Group-Managed Service Account,-Eigenschaften
Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**oder Fähigkeit zum Schreiben in „msDS-GroupManagedServiceAccount“-Objekte ist die Mindestvoraussetzung, um diese Verfahren abzuschließen.

Öffnen Sie das Active Directory-Modul für die Windows PowerShell, und legen Sie eine beliebige Eigenschaft mithilfe des Cmdlets „Set-ADServiceAccount“ fest.

Detaillierte Informationen für das Festlegen dieser Eigenschaften finden Sie unter [Set-ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) in der TechNet-Bibliothek, oder indem Sie an der Eingabeaufforderung für das Active Directory-Modul für Windows PowerShell **Get-Help Set-ADServiceAccount** eingeben und die EINGABETASTE drücken.

## <a name="BKMK_DecommMemberHosts"></a>Außerbetriebsetzung von mitgliedshosts in einer vorhandenen Serverfarm
Die Mitgliedschaft in **Domänen-Admins** oder die Fähigkeit, Mitglieder aus dem Sicherheitsgruppenobjekt zu entfernen, ist die Mindestvoraussetzung zum Abschließen dieser Verfahren.

### <a name="step-1-remove-member-host-from-gmsa"></a>Schritt 1: Entfernen von Mitgliedhosts vom gMSA
Wenn Sicherheitsgruppen für die Verwaltung von mitgliedshosts zu verwenden, entfernen Sie das Computerkonto für den deaktivierten mitgliedhost aus der Sicherheitsgruppe an, dass die mitgliedhosts des Mitglied mit einem der folgenden Methoden sind.

-   Methode 1: Active Directory-Benutzer und-Computer

    Verfahren zum Verwenden dieser Methode mithilfe der Windows-Benutzeroberfläche finden Sie unter [Löschen eines Computerkontos](https://technet.microsoft.com/library/cc754624.aspx) und [Verwalten unterschiedlicher Domänen im Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

-   Methode 2: „drsm“

    Verfahren zum Verwenden dieser Methode mithilfe der Befehlszeile finden Sie unter [Löschen eines Computerkontos](https://technet.microsoft.com/library/cc754624.aspx) .

-   Methode 3: Windows PowerShell Active Directory-Cmdlet „Remove-ADPrincipalGroupMembership“

    Detaillierte Informationen dazu, wie Sie dies vornehmen können, finden Sie unter  [Remove-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) in der TechNet-Bibliothek, oder indem Sie an der Eingabeaufforderung für das Active Directory-Modul für Windows PowerShell **Get-Help Remove-ADPrincipalGroupMembership** eingeben und die EINGABETASTE drücken.

Wenn Sie Computerkonten auflisten, rufen Sie die vorhandenen Konten ab, und fügen Sie dann alle mit Ausnahme des entfernten Computerkontos hinzu.

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren**oder Fähigkeit zum Verwalten von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um dieses Verfahren abzuschließen. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter „Lokale und Domänenstandardgruppen“.

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>So entfernen Sie Hosts mithilfe des Cmdlets „Set-ADServiceAccount“

1.  Führen Sie Windows PowerShell über die Taskleiste, auf dem Windows Server 2012-Domänencontroller.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **Get-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **Set-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|Parameter|Zeichenfolge|Beispiel|
|-------|-----|------|
|Name|Benennen Sie das Konto|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|Host1, Host3|

**Beispiel**

Geben Sie beispielsweise zum Entfernen von Mitgliedhosts die folgenden Befehle ein, und drücken Sie dann auf die EINGABETASTE.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1,Host3

```

### <a name="BKMK_RemoveGMSA"></a>Schritt 2: Entfernen eines gruppenverwalteten Dienstkontos aus dem System
Entfernen Sie die zwischengespeicherten gruppenverwalteten Dienstkonto-Anmeldeinformationen aus dem Mitgliedhost unter Verwendung der „Uninstall-ADServiceAccount“- oder der „NetRemoveServiceAccount“ auf dem Hostsystem.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren abschließen zu können.

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>So entfernen Sie ein gruppenverwaltetes Dienstkonto mithilfe des Cmdlets „Uninstall-ADServiceAccount“

1.  Führen Sie Windows PowerShell über die Taskleiste, auf dem Windows Server 2012-Domänencontroller.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **< ADServiceAccount > "Uninstall-ADServiceAccount"**

    **Beispiel**

    Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um beispielsweise die zwischengespeicherten Anmeldeinformationen für ein gruppenverwaltetes Dienstkonto namens „ITFarm1“ zu entfernen:

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

Geben Sie für weitere Informationen über das Cmdlet Uninstall-ADServiceAccount an der Eingabeaufforderung für das Active Directory-Modul für Windows PowerShell **Get-Help Uninstall-ADServiceAccount**ein, und drücken Sie dann die EINGABETASTE, oder konsultieren Sie die Informationen auf der TechNet-Website unter [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx).



## <a name="BKMK_Links"></a>Siehe auch

-   [Gruppe verwaltete Dienstkonten: Übersicht](group-managed-service-accounts-overview.md)



