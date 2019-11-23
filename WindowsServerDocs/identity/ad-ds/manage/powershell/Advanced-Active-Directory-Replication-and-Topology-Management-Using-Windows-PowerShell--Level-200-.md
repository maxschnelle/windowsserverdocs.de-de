---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: Erweiterte Active Directory-Replikation und Topologieverwaltung mithilfe von Windows PowerShell (Level 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: eeac84fb4e875ffe31b560bc72190895cd0527bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402675"
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>Erweiterte Active Directory-Replikation und Topologieverwaltung mithilfe von Windows PowerShell (Level 200)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Artikel enthält Details zu den neuen AD DS-Replikations- und Topologieverwaltungs-Cmdlets und liefert zusätzliche Beispiele. Eine Einführung finden Sie unter [Einführung in Active Directory Replikation und Topologieverwaltung mit &#40;Windows PowerShell Level&#41;100](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md).  
  
1.  [Einführung](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)  
  
2.  [Replikation und Metadaten](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)  
  
3.  [Get-adreplicationattributemetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)  
  
4.  [Get-adreplicationpartnermetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)  
  
5.  [Get-adreplicationfailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)  
  
6.  ["Get-adreplicationqueueoperation" und "Get-adreplicationupdedateness Vector Table"](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)  
  
7.  [Sync-ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)  
  
8.  [Topologie](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)  
  
## <a name="BKMK_Intro"></a>Einführung  
Mit Windows Server 2012 wurde das Active Directory-Modul für Windows PowerShell um 25 neue Cmdlets zur Verwaltung von Replikation und Gesamtstrukturtopologie erweitert. Zuvor mussten Sie die generischen **\*-ADObject-** Nomen verwenden oder .NET-Funktionen aufzurufen.  
  
Wie auch für alle anderen Active Directory Windows PowerShell-Cmdlets müssen Sie für diese neuen Funktionen den [Active Directory-Verwaltungsgatewaydienst](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852) auf mindestens einem Domänencontroller (bevorzugt auf allen Domänencontrollern) installieren.  
  
Die folgende Tabelle enthält die neuen Replikations- und Topologie-Cmdlets, die zum Active Directory Windows PowerShell-Modul hinzugefügt wurden.  
  
|||  
|-|-|  
|Cmdlet|Erläuterung|  
|Get-ADReplicationAttributeMetadata|Gibt Metadaten zur Attributreplikation für ein Objekt zurück|  
|Get-ADReplicationConnection|Gibt Objektdetails zur Domänencontrollerverbindung zurück|  
|Get-ADReplicationFailure|Gibt den neuesten Replikationsfehler für einen Domänencontroller zurück|  
|Get-ADReplicationPartnerMetadata|Gibt die Replikationskonfiguration für einen Domänencontroller zurück|  
|Get-ADReplicationQueueOperation|Gibt das Backlog der aktuellen Replikations-Warteschlange zurück|  
|Get-ADReplicationSite|Gibt Standortinformationen zurück|  
|Get-ADReplicationSiteLink|Gibt Standortverknüpfungsinformationen zurück|  
|Get-ADReplicationSiteLinkBridge|Gibt Standortverknüpfungsbrückeninformationen zurück|  
|Get-ADReplicationSubnet|Gibt AD-Subnetzinformationen zurück|  
|Get-ADReplicationUpToDatenessVectorTable|Gibt den Aktualitätsvektor für einen Domänencontroller zurück|  
|Get-ADTrust|Gibt Informationen über eine domänen- oder gesamtstrukturübergreifende Vertrauensstellung zurück|  
|New-ADReplicationSite|Erstellt einen neuen Standort|  
|New-ADReplicationSiteLink|Erstellt eine neue Standortverknüpfung|  
|New-ADReplicationSiteLinkBridge|Erstellt eine neue Standortverknüpfungsbrücke|  
|New-ADReplicationSubnet|Erstellt ein neues AD-Subnetz|  
|Remove-ADReplicationSite|Löscht einen Standort|  
|Remove-ADReplicationSiteLink|Löscht eine Standortverknüpfung|  
|Remove-ADReplicationSiteLinkBridge|Löscht eine Standortverknüpfungsbrücke|  
|Remove-ADReplicationSubnet|Löscht ein AD-Subnetz|  
|Set-ADReplicationConnection|Bearbeitet eine Verbindung|  
|Set-ADReplicationSite|Bearbeitet einen Standort|  
|Set-ADReplicationSiteLink|Bearbeitet eine Standortverknüpfung|  
|Set-ADReplicationSiteLinkBridge|Bearbeitet eine Standortverknüpfungsbrücke|  
|Set-ADReplicationSubnet|Bearbeitet ein AD-Subnetz|  
|Sync-ADObject|Erzwingt die Replikation eines einzelnen Objekts|  
  
Die Basis der meisten dieser Cmdlets ist Repadmin.exe. Andere (nicht aufgelistete) Cmdlets verwalten Features wie die dynamische Zugriffssteuerung und gruppenverwaltete Dienstkonten.  
  
Eine vollständige Liste aller Active Directory Windows PowerShell-Cmdlets erhalten Sie mit dem folgenden Befehl:  
  
```  
Get-command -module ActiveDirectory  
```  
  
Eine vollständige Liste der Argumente aller Active Directory Windows PowerShell-Cmdlets finden Sie im jeweiligen Hilfeartikel. Zum Beispiel:  
  
```  
Get-help New-ADReplicationSite  
  
```  
  
Mit dem Cmdlet `Update-Help` können Sie die Hilfedateien herunterladen und installieren.  
  
### <a name="BKMK_Repl"></a>Replikation und Metadaten  
Repadmin.exe prüft Integrität und Konsistenz der Active Directory-Replikation. Repadmin.exe bietet einfache Optionen zur Datenbearbeitung, wie z. B. einige Argumente für CSV-Ausgabe, für die Automatisierung müssen jedoch normalerweise Ausgaben in Form von Textdateien analysiert werden. Das Active Directory-Modul für Windows PowerShell ist der erste Versuch, echte Kontrolle über die zurückgegebenen Daten zu bieten. Bislang mussten Sie dafür Skripts ausführen oder externe Tools verwenden.  
  
Außerdem haben die folgenden Cmdlets die neuen Parameter **Ziel**, **Bereich** und **EnumerationServer**:  
  
-   **Get-adreplicationfailure**  
  
-   **Get-adreplicationpartnermetadata**  
  
-   **Get-adreplicationupdedateness Vector Table**  
  
Das **Ziel** -Argument akzeptiert eine durch Trennzeichen getrennte Liste von Zeichenfolge, mit denen die im Argument **Bereich** angegebenen Zielserver, Standorte, Domänen oder Gesamtstrukturen identifiziert werden. Ein Sternchen (\*) ist ebenfalls zulässig und bezeichnet alle Server innerhalb des angegebenen Bereichs. Wenn kein Bereich angegeben ist, sind alle Server in der Gesamtstruktur des aktuellen Benutzers gemeint. Das Argument **Bereich** gibt die Breite der Suche an. Akzeptiert werden die Werte **Server**, **Site**, **Domain** und **Forest**. **EnumerationServer** gibt den Server an, der die Aufzählung der in **Ziel** und **Bereich**angegebenen Liste von Domänencontrollern enthält. Dieses Argument funktioniert analog zu **Server** , und der angegebene Server muss den Active Directory-Webdienst ausführen.  
  
Es folgen nun einige Beispielszenarien, die mit repadmin.exe nicht möglich waren, um die Verwaltungsmöglichkeiten der neuen Cmdlets aufzuzeigen. Genauere Informationen zur Syntax finden Sie in den Hilfedateien der einzelnen Cmdlets.  
  
### <a name="BKMK_ReplAttrMD"></a>Get-adreplicationattributemetadata  
Dieses Cmdlet funktioniert gleich wie **repadmin.exe /showobjmeta**. Es gibt Replikationsmetadaten zurück, z. B. den Änderungszeitpunkt eines Attributs, den Ursprungs-Domänencontroller, Versions- und USN-Informationen und Attributdaten. Dieses Cmdlet ist hilfreich, wenn Sie feststellen müssen, wo und wann eine Änderung durchgeführt wurde.  
  
Im Gegensatz zu Repadmin bietet Windows PowerShell flexible Kontrolle über Suche und Ausgabe. Sie können z. B. die Metadaten des Domänen-Admin-Objekts sortiert als lesbare Liste ausgeben:  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list  
  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)  
  
Alternativ können Sie die Daten wie bei Repadmin in einer Tabelle ausgeben:  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap  
  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)  
  
Alternativ können Sie die Metadaten für eine gesamte Objektklasse abrufen, indem Sie das **Get-Adobject** -Cmdlet mit einem Filter verknüpfen, wie z. B. alle Gruppen, und die Ausgabe mit einem bestimmten Datum kombinieren. Pipelines sind Kanäle zur Datenübergabe zwischen mehreren Cmdlets. Anzeigen aller Gruppen, die am 13. Januar 2012 auf irgendeine Art verändert wurden:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)  
  
Weitere Informationen zu Windows PowerShell-Vorgängen mit Pipelines finden Sie unter [Piping und die Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).  
  
Anzeigen aller Gruppen, in denen Tony Wang Mitglied ist, und Anzeigen des letzten Änderungsdatums der Gruppen:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto  
  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)  
  
Anzeigen aller Objekte, die mit einer Systemstatussicherung in der Domäne autoritativ wiederhergestellt wurden, anhand ihrer künstlich hohen Versionsnummer:  
  
```  
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)  
  
Senden aller Benutzermetadaten in eine CSV-Datei zur späteren Analyse in Microsoft Excel:  
  
```  
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv  
```  
  
### <a name="BKMK_PartnerMD"></a>Get-adreplicationpartnermetadata  
Dieses Cmdlet gibt Informationen über Konfiguration und Status der Replikation für einen Domänencontroller zurück und ermöglicht Überwachung, Inventur und Problembehandlung. Im Gegensatz zu Repadmin.exe werden bei Windows PowerShell nur die wirklich relevanten Daten im jeweils optimalen Format angezeigt.  
  
Der lesbare Replikationsstatus eines einzelnen Domänencontrollers:  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)  
  
Der Zeitpunkt der letzten Replikation eines Domänencontrollers in eingehender Richtung und dessen Partner, im Tabellenformat:  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)  
  
Alle Domänencontroller in der Gesamtstruktur kontaktieren und diejenigen anzeigen, deren letzter Replikationsversuch aus irgendeinem Grund fehlgeschlagen ist:  
  
```  
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto  
  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)  
  
### <a name="BKMK_ReplFail"></a>Get-adreplicationfailure  
Dieses Cmdlet gibt Informationen über aktuelle Fehler bei der Replikation zurück. Es funktioniert gleich wie **Repadmin.exe /showreplsum**, jedoch ebenfalls mit wesentlich mehr Kontrolle dank Windows PowerShell.  
  
Sie können z. B. die aktuellsten Fehler eines Domänencontrollers und die Partner anzeigen, deren Kontaktierung fehlgeschlagen ist:  
  
```  
Get-ADReplicationFailure dc1.corp.contoso.com  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)  
  
Anzeigen einer Tabellenansicht für alle Server in einem logischen AD-Standort, sortiert zur leichteren Analyse und nur mit den wichtigsten Daten:  
  
```  
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto  
  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)  
  
### <a name="BKMK_ReplQueue"></a>"Get-adreplicationqueueoperation" und "Get-adreplicationupdedateness Vector Table"  
Diese beiden Cmdlets geben weitere Aspekte der "Aktualität" von Domänencontrollern zurück, inklusive ausstehender Replikationen und Versionsvektoren.  
  
### <a name="BKMK_Sync"></a>Sync-ADObject  
Dieses Cmdlet funktioniert gleich wie **Repadmin.exe /replsingleobject**. Diese Funktion ist hilfreich, wenn Sie irgendwelche Änderungen außerplanmäßig replizieren möchten, insbesondere bei der Korrektur von Problemen.  
  
Wenn z. B. jemand das Benutzerkonto des Geschäftsführers gelöscht und anschließend mit dem Active Directory-Papierkorb wiederhergestellt hat, möchten Sie dieses Objekt vermutlich sofort auf alle Domänencontroller replizieren. Außerdem möchten Sie es vermeiden, gleichzeitig sämtliche anderen Änderungen zu replizieren. Sie haben schließlich einen Replikationszeitplan, um überlastete WAN-Links zu vermeiden.  
  
```  
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}  
  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)  
  
### <a name="BKMK_Topo"></a>Topologie  
Repadmin.exe ist zwar praktisch zum Abrufen von Daten über Replikationstopologien wie z. B. Standorte, Standortverknüpfungen, Standortverknüpfungsbrücken und Verbindungen, bietet jedoch keine umfassenden Argumente, um Änderungen an den Objekten vorzunehmen. Bislang gibt es kein skriptgesteuertes, integriertes Windows-Hilfsprogramm speziell für Administratoren, um AD DS-Topologien zu erstellen und zu bearbeiten. Active Directory ist in Millionen von Kundenumgebungen gereift, und offensichtlich wird eine Möglichkeit zum massenweisen Bearbeiten logischer Active Directory-Informationen benötigt.  
  
Nach einer schnellen Erweiterung neuer Filialen und der Konsolidierung anderer Filialen kann es passieren, dass Sie Hunderte von Standortänderungen aufgrund von physischen Standorten, Netzwerkänderungen und neuen Kapazitätsanforderungen vornehmen müssen. Anstatt Dssites.msc und Adsiedit.msc für diese Änderungen zu verwenden, können Sie den Vorgang automatisieren. Dies ist besonders überzeugend, wenn Sie mit einer Datentabelle arbeiten, die Sie von Ihren Netzwerk- und Einrichtungsteams erhalten haben.  
  
Die Cmdlets " **Get-adreplication\\** *" geben Informationen über die Replikations Topologie zurück und sind für die Massen Pipeline in die **Set-adreplication\\** *-Cmdlets hilfreich. **Get** -Cmdlets ändern keine Daten, Sie zeigen nur Daten an oder erstellen Windows PowerShell-Sitzungs Objekte, die an **Set-adreplication\\** *-Cmdlets Weiterleitungen gesendet werden können. Die **New**- und **Remove**-Cmdlets sind hilfreich zum Erstellen und Entfernen von Active Directory-Topologieobjekten.  
  
Sie können z. B. neue Standorte mit einer CSV-Datei erstellen:  
  
```  
import-csv -path C:\newsites.csv | new-adreplicationsite  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)  
  
Alternativ können Sie eine Standortverknüpfung zwischen zwei existierenden Standorten mit benutzerdefiniertem Replikationsintervall und Standortkosten einrichten:  
  
```  
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)  
  
Oder Sie können alle Standorte in der Gesamtstruktur suchen und deren **Options**-Attribut durch eine Kennzeichnung zum Aktivieren der standortübergreifenden Benachrichtigung ersetzen, um mit maximaler Geschwindigkeit und mit Komprimierung zu replizieren:  
  
```  
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)  
  
> [!IMPORTANT]  
> Mit **-bor 5** können Sie die Komprimierung für diese Standortverknüpfungen ebenfalls deaktivieren.  
  
Oder Sie suchen nach allen Standorten mit fehlenden Subnetz-Zuweisungen, um die Liste mit den tatsächlichen Subnetzen dieser Standorte abzustimmen:  
  
```  
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name  
```  
  
![Erweiterte Verwaltung mit PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)  
  
## <a name="see-also"></a>Weitere Informationen  
[Einführung in Active Directory Replikation und Topologieverwaltung mithilfe &#40;der Windows PowerShell-Ebene 100&#41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)  
  

