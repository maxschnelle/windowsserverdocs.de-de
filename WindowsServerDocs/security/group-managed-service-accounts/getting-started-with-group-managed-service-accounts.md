---
title: Getting Started with Group Managed Service Accounts
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 979a6cf1e0b5e2d68c05f6285a9d745eabe41fa4
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991521"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>Getting Started with Group Managed Service Accounts

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016


Diese Anleitung enthält Schritt-für-Schritt-Anleitungen und Hintergrundinformationen zum Aktivieren und Verwenden von Gruppen verwalteten Dienst Konten in Windows Server 2012.

**Inhalt dieses Dokuments**

-   [Voraussetzungen](#BKMK_Prereqs)

-   [Einführung](#BKMK_Intro)

-   [Bereitstellen einer neuen Serverfarm](#BKMK_DeployNewFarm)

-   [Hinzufügen von Mitgliedshosts zu einer vorhandenen Serverfarm](#BKMK_AddMemberHosts)

-   [Aktualisieren der Eigenschaften für Gruppen verwaltete Dienst Konten](#BKMK_Update_gMSA)

-   [Außerbetriebsetzung von Mitgliedshosts in einer vorhandenen Serverfarm](#BKMK_DecommMemberHosts)


> [!NOTE]
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="prerequisites"></a><a name="BKMK_Prereqs"></a>Voraussetzungen
Informationen finden Sie im Abschnitt dieses Themas unter [Anforderungen für gruppenverwaltete Dienstkonten](#BKMK_gMSA_Req).

## <a name="introduction"></a><a name="BKMK_Intro"></a>Einführung
Wenn sich ein Clientcomputer mit einem auf einer Serverfarm gehosteten Dienst mithilfe des Netzwerklastenausgleichs (Network Load Balancing, NLB) oder einer anderen Methode verbindet, in der der Client alle Server als gleichen Dienst interpretiert, dann können die gegenseitige Authentifizierung unterstützende Authentifizierungsprotokolle wie Kerberos nicht verwendet werden, es sei denn, alle Instanzen der Dienste verwenden denselben Prinzipal. Das heißt, dass jeder Dienst dieselben Kennwörter/Schlüssel zum Beweisen der entsprechenden Identität verwenden muss.

> [!NOTE]
> Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt werden, können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe oder gMSA oder sMSA systemeigen unterstützen.

Dienste verfügen über die folgenden Prinzipale, aus denen ausgewählt werden kann, und jeder hat bestimmte Begrenzungen.

|Principals|`Scope`|Unterstützte Dienste|Kennwortverwaltung|
|-------|-----|-----------|------------|
|Computerkonto von Windows-System|Domain|Auf einen mit einer Domäne verbundenen Server|Vom Computer verwaltet|
|Computerkonto ohne Windows-System|Domain|Jeder mit einer Domäne verbundene Server|Keine|
|Virtuelles Konto|Lokal|Auf einen Server begrenzt|Vom Computer verwaltet|
|Eigenständig verwaltetes Windows 7-Dienstkonto|Domain|Auf einen mit einer Domäne verbundenen Server|Vom Computer verwaltet|
|Benutzerkonto|Domain|Jeder mit einer Domäne verbundene Server|Keine|
|Gruppenverwaltetes Dienstkonto|Domain|Alle in die Domäne eingebundenen Windows Server 2012-Server|Der Domänencontroller verwaltet, und der Host ruft ab|

Ein Windows-Computerkonto oder ein eigenständiges verwaltetes Windows 7-Dienstkonto (standalone Managed Service Account, sMSA) oder virtuelle Konten können nicht über mehrere Systeme hinweg freigegeben werden. Wenn Sie ein Konto für Dienste auf freizugebenden Serverfarmen konfigurieren, müssten Sie getrennt vom Windows-System ein Benutzer- oder Computerkonto auswählen. So oder so verfügen diese Konten nicht über die Fähigkeit der Kennwortverwaltung über einen einzigen Steuerungspunkt. Dies führt zu einem Problem, wobei jede Organisation eine teure Lösung erstellen muss, um die Schlüssel für den Dienst in Active Directory zu aktualisieren und anschließend die Schlüssel in allen Instanzen dieser Dienste bereitzustellen.

Mit Windows Server 2012 müssen Dienste oder Dienst Administratoren die Kenn Wort Synchronisierung zwischen Dienst Instanzen nicht verwalten, wenn Sie Gruppen verwaltete Dienst Konten (Group Managed Service Accounts, GMSA) verwenden. Sie stellen die gruppenverwalteten Dienstkonten in Active Directory bereit und konfigurieren anschließend den Dienst, der verwaltete Dienstkonten unterstützt. Sie können ein gruppenverwaltetes Dienstkonto mithilfe der Cmdlets „*-ADServiceAccount“ bereitstellen, die Bestandteil des Active Directory-Moduls sind. Die Dienstidentitätskonfiguration auf dem Host wird unterstützt durch:

-   Dieselben APIs wie sMSA, sodass Produkte, die sMSA unterstützen, auch gMSA unterstützen

-   Dienste, die den Dienststeuerungs-Manager zum Konfigurieren der Anmeldeidentität verwenden

-   Dienste, die den IIS-Manager für Anwendungspools zwecks Konfiguration der Identität verwenden

-   Aufgaben mithilfe der Aufgabenplanung.

### <a name="requirements-for-group-managed-service-accounts"></a><a name="BKMK_gMSA_Req"></a>Anforderungen für gruppenverwaltete Dienstkonten
Die folgende Tabelle führt die Betriebssystemanforderungen auf, damit die Kerberos-Authentifizierung mit Diensten mithilfe von gMSA funktioniert. Die Active Directory-Anforderungen sind im Anschluss an die Tabelle aufgeführt.

Zum Ausführen der Windows PowerShell-Befehle ist eine 64-Bit-Architektur erforderlich, die zum Verwalten von gruppenverwalteten Dienstkonten (group Managed Service Accounts, gMSA) verwendet werden.

**Betriebssystemanforderungen**

|Element|Anforderung|Betriebssystem|
|------|--------|----------|
|Host der Clientanwendung|RFC-konformer Kerberos-Client|Mindestens Windows XP|
|Domänen Controller der Domäne des Benutzerkontos|RFC-konformer KDC|Mindestens Windows Server 2003|
|Mitgliederhosts für freigegebene Dienste|| Windows Server 2012 |
|Domänen DCS des Mitglieds Hosts|RFC-konformer KDC|Mindestens Windows Server 2003|
|Domänen DCS des GMSA-Kontos| Windows Server 2012 DCS verfügbar für den Host zum Abrufen des Kennworts|Domäne mit Windows Server 2012, die einige Systeme vor Windows Server 2012 haben kann |
|Back-End-Diensthost|RFC-konformer Kerberos-Anwendungsserver|Mindestens Windows Server 2003|
|Domänen Controller des Back-End-Dienst Kontos|RFC-konformer KDC|Mindestens Windows Server 2003|
|Windows PowerShell für Active Directory|Die lokal auf einem Computer oder auf Ihrem Remoteverwaltungscomputer (beispielsweise mithilfe des Remoteserver-Verwaltungstoolkits) installierte Windows PowerShell für Active Directory, die eine 64-Bit-Architektur unterstützt.| Windows Server 2012 |

**Anforderungen für Active Directory-Domänendienste**

-   Das Active Directory Schema in der Gesamtstruktur der GMSA-Domäne muss auf Windows Server 2012 aktualisiert werden, um ein GMSA zu erstellen.

    Sie können das Schema aktualisieren, indem Sie einen Domänen Controller installieren, auf dem Windows Server 2012 ausgeführt wird, oder indem Sie die Version von adprep.exe von einem Computer mit Windows Server 2012 ausführen. Das Objektversionsattribut für das Objekt „CN=Schema,CN=Configuration,DC=Contoso,DC=Com“ muss „52“ sein.

-   Neues gruppenverwaltetes Dienstkonto

-   Wenn Sie die Diensthostberechtigung verwalten, um das gMSA nach Gruppe zu verwenden, dann neue oder vorhandene Sicherheitsgruppe

-   Beim Verwalten der Dienstzugriffssteuerung nach Gruppe dann neue oder vorhandene Sicherheitsgruppe

-   Wenn erste Hauptstammschlüssel für Active Directory nicht in der Domäne bereitgestellt wird oder nicht erstellt wurde, dann erstellen Sie ihn. Die Ergebnisse seiner Erstellung können im KdsSvc-Betriebsprotokoll unter Ereignis-ID 4004 nachvollzogen werden.

Anweisungen zum Erstellen des Schlüssels finden Sie unter [Erstellen des Schlüssel Verteilungs Dienste-KDS](create-the-key-distribution-services-kds-root-key.md)-Stamm Schlüssels. Der Microsoft-Schlüsselverteilungsdienst („kdssvc.dll“) ist der Stammschlüssel für Active Directory.

**Lebenszyklus**

Der Lebenszyklus einer Serverfarm, die das gMSA-Feature verwendet, umfasst für gewöhnlich folgende Aufgaben:

-   Bereitstellen einer neuen Serverfarm

-   Hinzufügen von Mitgliedshosts zu einer vorhandenen Serverfarm

-   Außerbetriebsetzung von Mitgliedshosts in einer vorhandenen Serverfarm

-   Außerbetriebsetzung einer vorhandenen Serverfarm

-   Entfernen eines gefährdeten Mitgliedhosts aus einer Serverfarm, sofern erforderlich.

## <a name="deploying-a-new-server-farm"></a><a name="BKMK_DeployNewFarm"></a>Bereitstellen einer neuen Serverfarm
Beim Bereitstellen einer neuen Serverfarm muss der Dienstadministrator Folgendes bestimmen:

-   Ob der Dienst mithilfe von gMSAs unterstützt wird

-   Ob für den Dienst eingehende oder ausgehende authentifizierte Verbindungen erforderlich sind

-   Die Computerkontennamen für die Mitgliedhosts für den Dienst mithilfe des gMSAs

-   Den NetBIOS-Namen für den Dienst

-   Den DNS-Hostnamen für den Dienst

-   Die Dienstprinzipalnamen für den Dienst

-   Das Kennwortänderungsintervall (Standard liegt bei 30 Tagen)

### <a name="step-1-provisioning-group-managed-service-accounts"></a><a name="BKMK_Step1"></a>Schritt 1: Bereitstellen gruppenverwalteter Dienstkonten
Sie können ein GMSA nur erstellen, wenn das Gesamtstruktur Schema auf Windows Server 2012 aktualisiert wurde, der Hauptstamm Schlüssel für Active Directory bereitgestellt wurde und mindestens ein Windows Server 2012 DC in der Domäne vorhanden ist, in der das GMSA erstellt wird.

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Erstellen von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um die folgenden Verfahren abzuschließen.

> [!NOTE]
> Ein Wert für den Parameter "-Name" ist immer erforderlich (unabhängig davon, ob Sie "-Name" angeben), mit "-dNSHostName", "-restricttosinglecomputer" und "-restricttooutboundauthentication" sind sekundäre Anforderungen für die drei Bereitstellungs Szenarien.


#### <a name="to-create-a-gmsa-using-the-new-adserviceaccount-cmdlet"></a><a name="BKMK_CreateGMSA"></a>So erstellen Sie ein gMSA mithilfe des Cmdlets „New-ADServiceAccount“

1.  Führen Sie auf dem Windows Server 2012-Domänen Controller Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für die Windows PowerShell die folgenden Befehle ein, und drücken Sie die EINGABETASTE: (Das Active Directory-Modul wird automatisch geladen.)

    **New-ADServiceAccount [-Name] &lt; String &gt; -dNSHostName &lt; String &gt; [-kerberosencryptiontype &lt; adkerberosencryptiontype &gt; ] [-managedpasswordintervalindays <NULL-Werte zulassen [Int32] >] [-principalsallowedtoretrievemanagedpassword <ADPrincipal [] >] [-sAMAccountName &lt; String &gt; ] [-ServicePrincipalNames <String [] >]**

    |Parameter|String|Beispiel|
    |-------|-----|------|
    |Name|Name des Kontos|ITFarm1|
    |DNSHostName|DNS-Hostname des Diensts|ITFarm1.contoso.com|
    |KerberosEncryptionType|Jeder durch die Hostserver unterstützte Verschlüsselungstyp|None, RC4, AES128, AES256|
    |ManagedPasswordIntervalInDays|Kennwortänderungsintervall in Tagen (Standard liegt bei 30, wenn keine Angabe erfolgt)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|ITFarmHosts|
    |SamAccountName|NetBIOS-Name für den Dienst, sofern dies nicht „Name“ entspricht|ITFarm1|
    |ServicePrincipalNames|Die Dienstprinzipalnamen für den Dienst|http/"itfarm1". "c#", "c", "" itfarm1 "....... com", "http/. c", "MSSQLSvc/" itfarm1 ".", "MSSQLSvc/" itfarm1 ".... com", "MSSQLSvc/INST01. Configuration. com:"|

    > [!IMPORTANT]
    > Das Kennwortänderungsintervall kann nur während der Erstellung festgelegt werden. Wenn Sie das Intervall ändern möchten, müssen Sie ein neues gMSA erstellen und es zur Erstellungszeit festlegen.

    **Beispiel**

    Geben Sie jeden Befehl in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

    ```Powershell
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts$ -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso
    ```

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Erstellen von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um dieses Verfahren abzuschließen. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter [Lokale und Domänenstandardgruppen](/previous-versions/orphan-topics/ws.10/dd728026(v=ws.10)).

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>So erstellen Sie ein gMSA ausschließlich für die ausgehende Authentifizierung mithilfe des Cmdlets „New-ADServiceAccount“

1.  Führen Sie auf dem Windows Server 2012-Domänen Controller Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie auf die EINGABETASTE:

    **New-ADServiceAccount [-Name] &lt; String &gt; -restricttooutboundauthenticationonly [-managedpasswordintervalindays <Nullable [Int32] >] [-principalsallowedtoretrievemanagedpassword <ADPrincipal [] >]**

    |Parameter|String|Beispiel|
    |-------|-----|------|
    |Name|Benennen Sie das Konto|ITFarm1|
    |ManagedPasswordIntervalInDays|Kennwortänderungsintervall in Tagen (Standard liegt bei 30, wenn keine Angabe erfolgt)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|ITFarmHosts|

    > [!IMPORTANT]
    > Das Kennwortänderungsintervall kann nur während der Erstellung festgelegt werden. Wenn Sie das Intervall ändern möchten, müssen Sie ein neues gMSA erstellen und es zur Erstellungszeit festlegen.

  **Beispiel**

```PowerShell
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts$
```

### <a name="step-2-configuring-service-identity-application-service"></a><a name="BKMK_ConfigureServiceIdentity"></a>Schritt 2: Konfigurieren des Dienstidentitäts-Anwendungsdiensts
Informationen zum Konfigurieren der Dienste in Windows Server 2012 finden Sie in der folgenden Featuredokumentation:

-   IIS-Anwendungspool

    Weitere Informationen finden Sie unter [Angeben einer Identität für einen Anwendungspool (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771170(v=ws.10)).

-   Windows-Dienste

    Weitere Informationen finden Sie unter [Dienste](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772408(v=ws.11)).

-   Tasks

    Weitere Informationen finden Sie unter [Aufgabenplanung (Übersicht)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc721871(v=ws.11)).

Andere Dienste könnten gMSA unterstützen. Konsultieren Sie die entsprechende Produktdokumentation, um Details darüber zu erhalten, wie diese Dienste zu konfigurieren sind.

## <a name="adding-member-hosts-to-an-existing-server-farm"></a><a name="BKMK_AddMemberHosts"></a>Hinzufügen von Mitgliedshosts zu einer vorhandenen Serverfarm
Wenn Sie Sicherheitsgruppen für die Verwaltung von Mitglied Hosts verwenden, fügen Sie das Computer Konto für den neuen Mitglieds Host der Sicherheitsgruppe (die Mitglieder Hosts des GMSA angehören) mithilfe einer der folgenden Methoden hinzu.

Die Mitgliedschaft in **Domänen-Admins** oder die Fähigkeit, Mitglieder zum Sicherheitsgruppenobjekt hinzuzufügen, ist die Mindestvoraussetzung zum Abschließen dieser Verfahren.

-   Methode 1: Active Directory-Benutzer und-Computer

    Verfahren zum Verwenden dieser Methode mithilfe der Windows-Benutzeroberfläche finden Sie unter [Hinzufügen eines Computerkontos zu einer Gruppe](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc733097(v=ws.11)) und [Verwalten unterschiedlicher Domänen im Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

-   Methode 2: „dsmod“

    Verfahren zum Verwenden dieser Methode mithilfe der Befehlszeile finden Sie unter [Hinzufügen eines Computerkontos zu einer Gruppe](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc733097(v=ws.11)) .

-   Methode 3: Windows PowerShell Active Directory-Cmdlet „Add-ADPrincipalGroupMembership“

    Verfahren zum Verwenden dieser Methode finden Sie unter [Add-ADPrincipalGroupMembership](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617203(v=technet.10)).

Suchen Sie bei der Verwendung von Benutzerkonten nach vorhandenen Konten, und fügen Sie dann das neue Benutzerkonto hinzu.

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Verwalten von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um dieses Verfahren abzuschließen. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter „Lokale und Domänenstandardgruppen“.

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>So fügen Sie Hosts mithilfe des Cmdlets „Set-ADServiceAccount“ hinzu

1.  Führen Sie auf dem Windows Server 2012-Domänen Controller Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie auf die EINGABETASTE:

    **Get-ADServiceAccount [-Identity] &lt; String &gt; -Properties principalsallowedtoretestevemanagedpassword**

3.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie auf die EINGABETASTE:

    **Set-ADServiceAccount [-Identity] &lt; String &gt; -principalsallowedtoretrievemanagedpassword <ADPrincipal [] >**

|Parameter|String|Beispiel|
|-------|-----|------|
|Name|Benennen Sie das Konto|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|Host1, Host2, Host3|

**Beispiel**

Geben Sie beispielsweise zum Hinzufügen von Mitgliedhosts die folgenden Befehle ein, und drücken Sie dann die EINGABETASTE.

```PowerShell
Get-ADServiceAccount [-Identity] ITFarm1 -Properties PrincipalsAllowedToRetrieveManagedPassword
```

```PowerShell
Set-ADServiceAccount [-Identity] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1$,Host2$,Host3$
```

## <a name="updating-the-group-managed-service-account-properties"></a><a name="BKMK_Update_gMSA"></a>Aktualisieren der Eigenschaften für gruppenverwaltete Dienstkonten
Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Schreiben in „msDS-GroupManagedServiceAccount“-Objekte ist die Mindestvoraussetzung, um diese Verfahren abzuschließen.

Öffnen Sie das Active Directory-Modul für die Windows PowerShell, und legen Sie eine beliebige Eigenschaft mithilfe des Cmdlets „Set-ADServiceAccount“ fest.

Detaillierte Informationen für das Festlegen dieser Eigenschaften finden Sie unter [Set-ADServiceAccount](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617252(v=technet.10)) in der TechNet-Bibliothek, oder indem Sie an der Eingabeaufforderung für das Active Directory-Modul für Windows PowerShell **Get-Help Set-ADServiceAccount** eingeben und die EINGABETASTE drücken.

## <a name="decommissioning-member-hosts-from-an-existing-server-farm"></a><a name="BKMK_DecommMemberHosts"></a>Außerbetriebsetzung von Mitgliedshosts in einer vorhandenen Serverfarm
Die Mitgliedschaft in **Domänen-Admins** oder die Fähigkeit, Mitglieder aus dem Sicherheitsgruppenobjekt zu entfernen, ist die Mindestvoraussetzung zum Abschließen dieser Verfahren.

### <a name="step-1-remove-member-host-from-gmsa"></a>Schritt 1: Entfernen von Mitgliedhosts vom gMSA
Wenn Sie Sicherheitsgruppen für die Verwaltung von Mitglieds Hosts verwenden, entfernen Sie das Computer Konto für den außer Betrieb gesetzten Mitglieds Host aus der Sicherheitsgruppe, der die Mitglieder Hosts des GMSA angehören. verwenden Sie dazu eine der folgenden Methoden.

-   Methode 1: Active Directory-Benutzer und-Computer

    Verfahren zum Verwenden dieser Methode mithilfe der Windows-Benutzeroberfläche finden Sie unter [Löschen eines Computerkontos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754624(v=ws.11)) und [Verwalten unterschiedlicher Domänen im Active Directory-Verwaltungscenter](manage-different-domains-in-active-directory-administrative-center.md).

-   Methode 2: „drsm“

    Verfahren zum Verwenden dieser Methode mithilfe der Befehlszeile finden Sie unter [Löschen eines Computerkontos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754624(v=ws.11)) .

-   Methode 3: Windows PowerShell Active Directory-Cmdlet „Remove-ADPrincipalGroupMembership“

    Detaillierte Informationen dazu, wie Sie dies vornehmen können, finden Sie unter  [Remove-ADPrincipalGroupMembership](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617243(v=technet.10)) in der TechNet-Bibliothek, oder indem Sie an der Eingabeaufforderung für das Active Directory-Modul für Windows PowerShell **Get-Help Remove-ADPrincipalGroupMembership** eingeben und die EINGABETASTE drücken.

Wenn Sie Computerkonten auflisten, rufen Sie die vorhandenen Konten ab, und fügen Sie dann alle mit Ausnahme des entfernten Computerkontos hinzu.

Die Mitgliedschaft in **Domänen-Admins**, **Konten-Operatoren** oder Fähigkeit zum Verwalten von „msDS-GroupManagedServiceAccount“-Objekten ist die Mindestvoraussetzung, um dieses Verfahren abzuschließen. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter „Lokale und Domänenstandardgruppen“.

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>So entfernen Sie Hosts mithilfe des Cmdlets „Set-ADServiceAccount“

1.  Führen Sie auf dem Windows Server 2012-Domänen Controller Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie auf die EINGABETASTE:

    **Get-ADServiceAccount [-Identity] &lt; String &gt; -Properties principalsallowedtoretestevemanagedpassword**

3.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie auf die EINGABETASTE:

    **Set-ADServiceAccount [-Identity] &lt; String &gt; -principalsallowedtoretrievemanagedpassword <ADPrincipal [] >**

|Parameter|String|Beispiel|
|-------|-----|------|
|Name|Benennen Sie das Konto|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|Die Computerkonten des Mitgliedhosts oder der Sicherheitsgruppe, die das Mitglied hostet, sind Mitglied von|Host1, Host3|

**Beispiel**

Geben Sie beispielsweise zum Entfernen von Mitgliedhosts die folgenden Befehle ein, und drücken Sie dann die EINGABETASTE.

```PowerShell
Get-ADServiceAccount [-Identity] ITFarm1 -Properties PrincipalsAllowedToRetrieveManagedPassword
```

```PowerShell
Set-ADServiceAccount [-Identity] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1$,Host3$
```

### <a name="step-2-removing-a-group-managed-service-account-from-the-system"></a><a name="BKMK_RemoveGMSA"></a>Schritt 2: Entfernen eines gruppenverwalteten Dienstkontos aus dem System
Entfernen Sie die zwischengespeicherten gruppenverwalteten Dienstkonto-Anmeldeinformationen aus dem Mitgliedhost unter Verwendung der „Uninstall-ADServiceAccount“- oder der „NetRemoveServiceAccount“ auf dem Hostsystem.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren abschließen zu können.

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>So entfernen Sie ein gruppenverwaltetes Dienstkonto mithilfe des Cmdlets „Uninstall-ADServiceAccount“

1.  Führen Sie auf dem Windows Server 2012-Domänen Controller Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie auf die EINGABETASTE:

    **Deinstallation: ADServiceAccount &lt; ADServiceAccount&gt;**

    **Beispiel**

    Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um beispielsweise die zwischengespeicherten Anmeldeinformationen für ein gruppenverwaltetes Dienstkonto namens „ITFarm1“ zu entfernen:

    ```PowerShell
    Uninstall-ADServiceAccount ITFarm1
    ```

Geben Sie für weitere Informationen über das Cmdlet Uninstall-ADServiceAccount an der Eingabeaufforderung für das Active Directory-Modul für Windows PowerShell **Get-Help Uninstall-ADServiceAccount**ein, und drücken Sie dann die EINGABETASTE, oder konsultieren Sie die Informationen auf der TechNet-Website unter [Uninstall-ADServiceAccount](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617202(v=technet.10)).



## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch

-   [Übersicht über Gruppen verwaltete Dienst Konten](group-managed-service-accounts-overview.md)