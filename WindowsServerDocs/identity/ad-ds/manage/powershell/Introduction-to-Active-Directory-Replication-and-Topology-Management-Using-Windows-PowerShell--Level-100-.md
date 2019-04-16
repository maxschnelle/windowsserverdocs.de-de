---
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: "Einführung in die Active Directory-Replikation und Topologieverwaltung mithilfe von WindowsPowerShell (Stufe 100)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 006179bb3220f7bccfc7510e1b8ef69678321074
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Einführung in die Active Directory-Replikation und Topologieverwaltung mithilfe von WindowsPowerShell (Stufe 100)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Windows PowerShell für Active Directory bietet die Möglichkeit zum Verwalten der Replikation, Standorten, Domänen und Gesamtstrukturen, Domänencontrollern und Partitionen. Benutzer älterer Verwaltungstools wie die Active Directory-Standorte und -Dienste-Snap-in und repadmin.exe werden bemerken, dass ähnliche Funktionalität jetzt innerhalb des Windows PowerShell für Active Directory-Kontextes verfügbar ist. Darüber hinaus sind diese Cmdlets kompatibel mit den vorhandenen Windows PowerShell für Active Directory-Cmdlets und somit eine optimale Erfahrung und können Kunden problemlos Automatisierungsskripts erstellen.

> [!NOTE]
> Die Windows PowerShell für Active Directory-Replikation und Topologie-Cmdlets sind in den folgenden Umgebungen verfügbar:
> 
> -    Windows Server 2012-Domänencontroller
> -    WindowsServer 2012 mit den Remoteserver-Verwaltungstools für AD DS und AD LDS installiert.
> -   Windows&reg; 8 mit den Remoteserver-Verwaltungstools für AD DS und AD LDS installiert.

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Installieren von Active Directory-Modul für WindowsPowerShell
Die Active Directory-Modul für Windows PowerShell wird standardmäßig installiert, wenn die AD DS-Serverrolle auf einem Server installiert ist, die Windows Server 2012 ausgeführt wird. Es sind keine weiteren Schritte neben dem Hinzufügen der Serverrolle erforderlich. Sie können auch die Active Directory-Modul auf einem Server mit Windows Server 2012 durch die Installation der Remoteserver-Verwaltungstools installieren, und Sie können auf einem Computer unter Windows 8 herunterladen und Installieren der Active Directory-Modul installieren die [Remote Server Administrative Tools (RSAT)](https://www.microsoft.com/download/details.aspx?id=28972). Finden Sie unter [Anweisungen](https://www.microsoft.com/download/details.aspx?id=28972)Installationsschritte.

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Szenarios zum Testen der Windows PowerShell für Active Directory-Replikation und Topologie-Cmdlets für
Die folgenden Szenarien dienen für Administratoren mit neuen Verwaltungs-Cmdlets vertraut machen:

-   Abrufen einer Liste von allen Domänencontrollern und ihrer entsprechenden Standorte

-   Verwalten der Replikationstopologie

-   Anzeigen von Replikationsstatus und Informationen

## <a name="lab-requirements"></a>Lab-Anforderungen

-   Zwei Windows Server 2012-Domänencontroller: **DC1** und **DC2** , die Teil der Domäne "contoso.com" und befinden sich im Standort "CORPORATE" innerhalb der Domäne.

## <a name="view-domain-controllers-and-their-sites"></a>Anzeigen der Domänencontroller und ihrer Standorte
In diesem Schritt verwenden Sie das Active Directory-Modul für Windows PowerShell die existierenden Domänencontroller und der Replikationstopologie für die Domäne an.

Um die Schritte in den folgenden Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe der Domänenadministratoren sein oder über entsprechende Berechtigungen verfügen.

#### <a name="to-view-all-active-directory-sites"></a>So zeigen Sie alle Active Directory-Standorte an

1.  Auf **DC1**, klicken Sie auf **Windows PowerShell** auf der Taskleiste.

2.  Geben Sie den folgenden Befehl ein:

    `Get-ADReplicationSite -Filter *`

    Dies gibt detaillierte Informationen zu den einzelnen Standorten zurück. Die `Filter` Parameter wird in der gesamten Active Directory-PowerShell-Cmdlets verwendet, um die Anzahl der zurückgegebenen Objekte einzuschränken. In diesem Fall zeigt das Sternchen (*) alle Standortobjekte an.

    > [!TIP]
    > Sie können die Tab-Taste AutoVervollständigen-Befehle in Windows PowerShell verwenden.
    > 
    > Beispiel: Geben `Get-ADRep` und drücken Sie mehrmals Tab, um durch die passenden Befehle zu überspringen, bis Sie erreichen `Get-ADReplicationSite`. AutoVervollständigen kann auch für Parameternamen wie z. B. `Filter`.

    Zum Formatieren der Ausgabe von den `Get-ADReplicationSite` Befehls als Tabelle und beschränken Sie die Anzeige auf bestimmte Felder, Sie können über die Pipeline der Ausgabe an die `Format-Table` Befehl (oder "`ft`" kurz):

    `Get-ADReplicationSite -Filter * | ft Name`

    Dadurch wird eine kürzere Version der Websiteliste, z. B. nur das Namensfeld zurückgegeben.

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>Um eine Tabelle aller Domänencontroller zu erstellen.

-   Geben Sie den folgenden Befehl an der **Active Directory-Modul für Windows PowerShell** an:

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    Dieser Befehl gibt den Domänencontrollern Namen sowie ihre standortzuordnungen zurück.

## <a name="manage-replication-topology"></a>Verwalten der Replikationstopologie
Im vorherigen Schritt nach dem Ausführen des Befehls `Get-ADDomainController -Filter * | ft Hostname,Site`, **DC2** als Bestandteil aufgelistet wurde die **Unternehmen** Standort. In den folgenden Prozeduren erstellen Sie einen neuen Filialstandort **BRANCH1**und Erstellen einer neuen standortverknüpfung, legen Sie die Website Link Kosten und die Replikationsfrequenz und dann nach **DC2** auf **BRANCH1**.

Um die Schritte in den folgenden Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe der Domänenadministratoren sein oder über entsprechende Berechtigungen verfügen.

#### <a name="to-create-a-new-site"></a>Zum Erstellen einer neuen Website

-   Geben Sie den folgenden Befehl an der **Active Directory-Modul für Windows PowerShell** an:

    `New-ADReplicationSite BRANCH1`

    Dieser Befehl erstellt den neuen Filialstandort branch1.

#### <a name="to-create-a-new-site-link"></a>Erstellen eine neuen standortverknüpfung

-   Geben Sie den folgenden Befehl an der **Active Directory-Modul für Windows PowerShell** an:

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    Dieser Befehl erstellt die standortverknüpfung mit **BRANCH1** und der änderungsbenachrichtigungsprozess aktiviert.

    > [!TIP]
    > Mit der Registerkarte Automatische Vervollständigung Parameternamen wie z. B. `-SitesIncluded` und `-OtherAttributes` statt sie manuell einzugeben.

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>Festlegen der Website Link Kosten und die Replikationsfrequenz

-   Geben Sie den folgenden Befehl an der **Active Directory-Modul für Windows PowerShell** an:

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    Mit diesem Befehl wird die Standortverknüpfungskosten auf **BRANCH1** am **100** und legen Sie die Häufigkeit der Replikation mit dem Standort um **15 Minuten**.

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>So verschieben Sie einen Domänencontroller an einen anderen Standort

-   Geben Sie den folgenden Befehl an der **Active Directory-Modul für Windows PowerShell** an:

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    Mit diesem Befehl werden die Domänencontroller **DC2** auf die **BRANCH1** Standort.

### <a name="verification"></a>Überprüfung

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>So überprüfen Sie die standorterstellung, neue standortverknüpfung und Kosten und die Replikationsfrequenz

-   Klicken Sie auf **Server-Manager**, klicken Sie auf **Tools** , und klicken Sie dann auf **Active Directory-Standorte und-Dienste** und überprüfen Sie Folgendes:

    Überprüfen Sie, ob die **BRANCH1** Website enthält alle korrekten Werte aus der Windows PowerShell-Befehle.

    Überprüfen der **CORPORATE-BRANCH1** standortverknüpfung wird erstellt und verbindet die **BRANCH1** und **Unternehmen** Websites.

    Vergewissern Sie sich **DC2** ist jetzt der **BRANCH1** Standort. Alternativ können Sie öffnen die **Active Directory-Modul für Windows PowerShell** , und geben Sie den folgenden Befehl überprüfen **DC2** ist jetzt der **BRANCH1** Site: `Get-ADDomainController -Filter * | ft Hostname,Site`.

## <a name="view-replication-status-information"></a>Anzeigen von Replikationsstatusinformationen
In den folgenden Verfahren verwenden Sie eines der Windows PowerShell für Active Directory-Replikation und Verwaltungs-Cmdlet `Get-ADReplicationUpToDatenessVectorTable DC1`, um einen einfachen Replikationsbericht mithilfe der aktualitätsvektortabelle von jedem Domänencontroller verwaltet zu erzeugen. Diese aktualitätsvektortabelle hält den Überblick über den höchsten ausgehenden Schreib-USN, die von allen Domänencontrollern in der Gesamtstruktur angezeigt.

Um die Schritte in den folgenden Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe der Domänenadministratoren sein oder über entsprechende Berechtigungen verfügen.

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>So zeigen Sie die aktualitätsvektortabelle für einen einzelnen Domänencontroller an

1.  Geben Sie den folgenden Befehl an der **Active Directory-Modul für Windows PowerShell** an:

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    Dadurch wird eine Liste der höchsten USNs anzeigen, indem Sie **DC1** für jeden Domänencontroller in der Gesamtstruktur. Die **Server** Wert bezieht sich auf dem Server verwalten die Tabelle, in diesem Fall **DC1**. Die **Partner** Wert bezieht sich auf den Replikationspartner (direkt oder indirekt) auf dem Änderungen vorgenommen wurden. Der Usnfilter%-Wert ist die höchste USN anzeigen, indem Sie **DC1** von Partner. Wenn ein neuer Domänencontroller in der Gesamtstruktur hinzugefügt wird, erscheint er im **DC1**der Tabelle bis **DC1** eine Änderung, die von der neuen Domäne stammen.

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>So zeigen Sie die aktualitätsvektortabelle für alle Domänencontroller in einer Domäne an

1.  Geben Sie den folgenden Befehl an Active Directory-Modul für Windows PowerShell-Eingabeaufforderung ein:

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    Dieser Befehl ersetzt **DC1** mit `*`, daher die Aktualität Daten von allen Domänencontrollern gesammelt. Die Daten sortiert **Partner** und **Server** , und klicken Sie dann in einer Tabelle angezeigt.

    Die Sortierung können Sie einfach die letzte USN anzeigen, indem Sie jeder Domänencontroller für einen angegebenen Replikationspartner vergleichen. Dies ist eine schnelle Möglichkeit, überprüfen Sie, dass die Replikation in Ihrer Umgebung durchgeführt wird. Wenn die Replikation ordnungsgemäß funktioniert, sollte die Usnfilter% Werte für einen angegebenen Replikationspartner gemeldet auf allen Domänencontrollern ähnlich sein.

## <a name="see-also"></a>Siehe auch
[Erweiterte Active Directory-Replikation und Topologieverwaltung mithilfe von WindowsPowerShell & #40; Level 200 & #41;](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


