---
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: Einführung in die Active Directory-Replikation und Topologieverwaltung mithilfe von Windows PowerShell (Stufe 100)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: c8a5863865d465d55f1d5865fdcbdeeb942ce194
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71409082"
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Einführung in die Active Directory-Replikation und Topologieverwaltung mithilfe von Windows PowerShell (Stufe 100)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows PowerShell für Active Directory bietet die Möglichkeit zum Verwalten von Replikationen, Standorten, Domänen und Gesamtstrukturen, Domänencontrollern und Partitionen. Benutzer älterer Verwaltungstools, wie des Active Directory-Standorte und -Dienste-Snap-Ins und „repadmin.exe“, werden bemerken, dass eine ähnliche Funktionalität jetzt innerhalb des Windows PowerShell für Active Directory-Kontextes verfügbar ist. Außerdem sind diese Cmdlets kompatibel mit den vorhandenen Windows PowerShell für Active Directory-Cmdlets und sorgen so für eine optimale Erfahrung. Außerdem können Kunden problemlos Automatisierungsskripts erstellen.

> [!NOTE]
> Die Windows PowerShell für Active Directory-Replikations- und -Topologie-Cmdlets sind in folgenden Umgebungen verfügbar:
> 
> -    Windows Server 2012-Domänen Controller
> -    Windows Server 2012 mit der Remoteserver-Verwaltungstools für AD DS und AD LDS installiert.
> -   Windows&reg; 8 mit der Remoteserver-Verwaltungstools für AD DS und AD LDS installiert.

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Installieren des Active Directory-Moduls für Windows PowerShell
Das Active Directory-Modul für Windows PowerShell wird standardmäßig installiert, wenn die AD DS Server Rolle auf einem Server installiert ist, auf dem Windows Server 2012 ausgeführt wird. Es sind keine weiteren Schritte neben dem Hinzufügen der Serverrolle erforderlich. Sie können auch das Active Directory Modul auf einem Server installieren, auf dem Windows Server 2012 ausgeführt wird, indem Sie die Remoteserver-Verwaltungstools installieren. Sie können das Modul Active Directory auf einem Computer installieren, auf dem Windows 8 ausgeführt wird, indem Sie die [Remote Server-Verwaltungs Tools (RSAT)](https://www.microsoft.com/download/details.aspx?id=28972)herunterladen und installieren. Die Installationsschritte finden Sie unter [Instructions](https://www.microsoft.com/download/details.aspx?id=28972).

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Szenarios zum Testen der Windows PowerShell für Active Directory-Replikations- und -Topologieverwaltungs-Cmdlets
Die folgenden Szenarios wurden für Administratoren entwickelt, um sich mit den neuen Verwaltungs-Cmdlets vertraut zu machen:

-   Abrufen einer Liste aller Domänencontroller und ihrer entsprechenden Standorte

-   Verwalten der Replikationstopologie

-   Anzeigen von Replikationsstatus und -informationen

## <a name="lab-requirements"></a>Testumgebungsanforderungen

-   Zwei Windows Server 2012-Domänen Controller: **DC1** und **DC2** , die Teil der contoso.com-Domäne sind und sich auf der Unternehmenswebsite innerhalb dieser Domäne befinden.

## <a name="view-domain-controllers-and-their-sites"></a>Anzeigen der Domänencontroller und ihrer Standorte
In diesem Schritt verwenden Sie das Active Directory-Modul für Windows PowerShell zum Anzeigen der vorhandenen Domänencontroller und der Replikationstopologie für die Domäne.

Damit Sie die Schritte in den folgenden Verfahren ausführen können, müssen Sie ein Mitglied der Gruppe der Domänenadministratoren sein oder über vergleichbare Berechtigungen verfügen.

#### <a name="to-view-all-active-directory-sites"></a>So zeigen Sie alle Active Directory-Standorte an

1.  Klicken Sie auf **DC1** auf der Taskleiste auf **Windows PowerShell**.

2.  Geben Sie den folgenden Befehl ein:

    `Get-ADReplicationSite -Filter *`

    Dieser Befehl gibt detaillierte Informationen zu den einzelnen Standorten zurück. Der `Filter` -Parameter wird in PowerShell-Cmdlets für Active Directory verwendet, um die Anzahl der zurückgegebenen Objekte einzuschränken. In diesem Fall zeigt das Sternchen (*) alle Standortobjekte an.

    > [!TIP]
    > Sie können die Tab-Taste verwenden, um Befehle in Windows PowerShell automatisch zu vervollständigen.
    > 
    > Beispiel: Geben Sie `Get-ADRep` ein, und blättern Sie durch mehrmaliges Drücken der TAB-TASTE durch die passenden Befehle, bis Sie `Get-ADReplicationSite`erreichen. AutoVervollständigen kann auch für Parameternamen wie `Filter` verwendet werden.

    Wenn Sie die Ausgabe des Befehls `Get-ADReplicationSite` als Tabelle formatieren und die Anzeige auf bestimmte Felder beschränken möchten, können Sie die Ausgabe an den `Format-Table`-Befehl übergeben (oder kurz "`ft`"):

    `Get-ADReplicationSite -Filter * | ft Name`

    Dadurch wird eine kürzere Version der Zeitliste zurückgegeben, die nur das Namensfeld umfasst.

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>So erzeugen sie eine Tabelle aller Domänencontroller

-   Geben Sie an der Eingabeaufforderung des **Active Directory-Moduls für Windows PowerShell** den folgenden Befehl ein:

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    Dieser Befehl gibt die Hostnamen der Domänencontroller sowie ihre Standortzuordnungen zurück.

## <a name="manage-replication-topology"></a>Verwalten der Replikationstopologie
Im vorherigen Schritt wurde `Get-ADDomainController -Filter * | ft Hostname,Site`DC2 **nach dem Ausführen des Befehls** als Teil des Standorts **CORPORATE** aufgeführt. In den folgenden Prozeduren erstellen Sie den neuen Filialstandort **BRANCH1** sowie eine neue Standortverknüpfung, legen die Kosten und die Replikationsfrequenz für die Standortverknüpfung fest und verschieben **DC2** anschließend nach **BRANCH1**.

Damit Sie die Schritte in den folgenden Verfahren ausführen können, müssen Sie ein Mitglied der Gruppe der Domänenadministratoren sein oder über vergleichbare Berechtigungen verfügen.

#### <a name="to-create-a-new-site"></a>So erstellen Sie einen neuen Standort

-   Geben Sie an der Eingabeaufforderung des **Active Directory-Moduls für Windows PowerShell** den folgenden Befehl ein:

    `New-ADReplicationSite BRANCH1`

    Dieser Befehl erstellt den neuen Filialstandort, %%amp;quot;branch1%%amp;quot;.

#### <a name="to-create-a-new-site-link"></a>So erstellen Sie eine neue Standortverknüpfung

-   Geben Sie an der Eingabeaufforderung des **Active Directory-Moduls für Windows PowerShell** den folgenden Befehl ein:

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    Mit diesem Befehl wird die Standortverknüpfung mit **BRANCH1** erstellt und der Änderungsbenachrichtigungsprozess aktiviert.

    > [!TIP]
    > Drücken Sie TAB, um Parameternamen wie `-SitesIncluded` und `-OtherAttributes` per AutoVervollständigen (und nicht mittels manueller Eingabe) anzugeben.

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>So legen Sie die Kosten und die Replikationsfrequenz für die Standortverknüpfung fest

-   Geben Sie an der Eingabeaufforderung des **Active Directory-Moduls für Windows PowerShell** den folgenden Befehl ein:

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    Mit diesem Befehl werden die Standortverknüpfungskosten für **BRANCH1** auf **100** und die Replikationsfrequenz für den Standort wird auf **15 Minuten**festgelegt.

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>So verschieben sie einen Domänencontroller an einen anderen Standort

-   Geben Sie an der Eingabeaufforderung des **Active Directory-Moduls für Windows PowerShell** den folgenden Befehl ein:

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    Mit diesem Befehl wird der Domänencontroller **DC2** an den Standort **BRANCH1** verschoben.

### <a name="verification"></a>Überprüfung

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>So überprüfen Sie die Standorterstellung, die neue Standortverknüpfung sowie die Kosten und die Replikationsfrequenz

-   Klicken Sie auf **Server-Manager**, klicken Sie auf **Extras**, klicken Sie auf **Active Directory-Standorte und -Dienste**, und überprüfen Sie Folgendes:

    Vergewissern Sie sich, dass der Standort **BRANCH1** über alle korrekten Werte aus den Windows PowerShell-Befehlen verfügt.

    Vergewissern Sie sich, dass die Standortverknüpfung **CORPORATE-BRANCH1** erstellt wird und eine Verbindung zwischen den Standorten **BRANCH1** und **CORPORATE** herstellt.

    Vergewissern Sie sich, dass sich **DC2** jetzt am Standort **BRANCH1** befindet. Alternativ können Sie auch das **Active Directory-Modul für Windows PowerShell** öffnen und folgenden Befehl eingeben, um sich zu vergewissern, dass sich **DC2** jetzt am Standort **BRANCH1** befindet: `Get-ADDomainController -Filter * | ft Hostname,Site`.

## <a name="view-replication-status-information"></a>Anzeigen von Replikationsstatusinformationen
In den folgenden Prozeduren erstellen Sie mithilfe von `Get-ADReplicationUpToDatenessVectorTable DC1` – einem Replikations- und Verwaltungs-Cmdlet von Windows PowerShell für Active Directory – einen einfachen Replikationsbericht unter Verwendung der Aktualitätsvektortabelle, die von den einzelnen Domänencontrollern verwaltet wird. Diese Aktualitätsvektortabelle überwacht den höchsten ausgehenden Schreib-USN, der von den einzelnen Domänencontrollern in der Gesamtstruktur erfasst wird.

Damit Sie die Schritte in den folgenden Verfahren ausführen können, müssen Sie ein Mitglied der Gruppe der Domänenadministratoren sein oder über vergleichbare Berechtigungen verfügen.

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>So zeigen sie die Aktualitätsvektortabelle für einen einzelnen Domänencontroller an

1.  Geben Sie an der Eingabeaufforderung des **Active Directory-Moduls für Windows PowerShell** den folgenden Befehl ein:

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    Dadurch wird eine Liste mit den höchsten von **DC1** ermittelten USNs für jeden Domänencontroller in der Gesamtstruktur angezeigt. Der Wert **Server** bezieht sich auf den Server, von dem die Tabelle verwaltet wird (in diesem Fall **DC1**). Der Wert **Partner** bezieht sich auf den Replikationspartner (direkt oder indirekt), auf dem Änderungen vorgenommen wurden. Der Wert %%amp;quot;UsnFilter%%amp;quot; ist der höchste von **DC1** ermittelte USN des Partners. Wenn der Gesamtstruktur ein neuer Domänen Controller hinzugefügt wird, wird er erst in der **DC1**-Tabelle angezeigt, wenn **DC1** eine Änderung empfängt, die von der neuen Domäne stammt.

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>So zeigen sie die Aktualitätsvektortabelle für alle Domänencontroller in einer Domäne an

1.  Geben Sie an der Eingabeaufforderung des Active Directory-Moduls für Windows PowerShell den folgenden Befehl ein:

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    Bei diesem Befehl wird **DC1** durch `*`ersetzt. Dadurch werden die Daten der Aktualitätsvektortabelle von allen Domänencontrollern gesammelt. Die Daten werden nach **Partner** und **Server** sortiert und anschließend in Tabellenform angezeigt.

    Durch die Sortierung können Sie den letzten USN, der von den einzelnen Domänencontrollern für einen angegebenen Replikationspartner erfasst wurde, einfach vergleichen. Dies ist eine schnelle Möglichkeit, um zu überprüfen, ob die Replikation in der gesamten Umgebung stattfindet. Wenn die Replikation ordnungsgemäß funktioniert, sollten die %%amp;quot;UsnFilter%%amp;quot;- Werte, die für einen angegebenen Replikationspartner gemeldet werden, auf allen Domänencontrollern ähnlich sein.

## <a name="see-also"></a>Weitere Informationen
[Erweiterte Active Directory Replikation und Topologieverwaltung mithilfe &#40;der Windows PowerShell-Ebene 200&#41;](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


