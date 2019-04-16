---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: Erweiterte Active Directory-Replikation und Topologieverwaltung mithilfe von WindowsPowerShell (Stufe 200)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1e05616b4b594ae54fcaa3ec6496c0917ecde38b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>Erweiterte Active Directory-Replikation und Topologieverwaltung mithilfe von WindowsPowerShell (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden die neuen AD DS-Replikation und topologieverwaltungs-Cmdlets ausführlicher erläutert und liefert zusätzliche Beispiele. Eine Einführung finden Sie unter [Introduction to Active Directory-Replikation und Topologieverwaltung mithilfe von Windows PowerShell & #40; Stufe 100 & #41; ](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md).  
  
1.  [Einführung in](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)  
  
2.  [Replikation und Metadaten](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)  
  
3.  [Get-ADReplicationAttributeMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)  
  
4.  [Get-ADReplicationPartnerMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)  
  
5.  [Get-ADReplicationFailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)  
  
6.  [Get-ADReplicationQueueOperation und Get-ADReplicationUpToDatenessVectorTable](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)  
  
7.  [Sync-ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)  
  
8.  [Topologie](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)  
  
## <a name="BKMK_Intro"></a>Einführung in  
Windows Server 2012 wird die Active Directory-Modul für Windows PowerShell mit 25 neue Cmdlets zum Verwalten von Replikation und gesamtstrukturtopologie erweitert. Zuvor mussten Sie die generischen **\*-AdObject** Substantive oder .NET-Funktionen aufrufen.  
  
Wie alle Active Directory Windows PowerShell-Cmdlets, diese neue Funktion erfordert die Installation der [Active Directory-Verwaltungsgatewaydienst](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852) auf mindestens einem Domänencontroller (und bevorzugt, alle Domänencontroller).  
  
Die folgende Tabelle enthält die neuen Replikations- und Topologie-Cmdlets für das Active Directory Windows PowerShell-Modul hinzugefügt.  
  
|||  
|-|-|  
|Cmdlet|Erläuterung|  
|Get-ADReplicationAttributeMetadata|Gibt die Attributreplikation für ein Objekt|  
|Get-ADReplicationConnection|Es werden domänencontrollerverbindung Objektdetails zurückgegeben.|  
|Get-ADReplicationFailure|Gibt den neuesten Replikationsfehler für einen Domänencontroller zurück|  
|Get-ADReplicationPartnerMetadata|Gibt die Replikationskonfiguration von einem Domänencontroller|  
|Get-ADReplicationQueueOperation|Gibt den aktuellen Replikations-Rückstandsprotokoll Warteschlange|  
|Get-ADReplicationSite|Gibt Standortinformationen zurück|  
|Get-ADReplicationSiteLink|Gibt Standortverknüpfungsinformationen zurück|  
|Get-ADReplicationSiteLinkBridge|Gibt standortverknüpfungsbrückeninformationen zurück|  
|Get-ADReplicationSubnet|Gibt die AD-Subnetzinformationen zurück|  
|Get-ADReplicationUpToDatenessVectorTable|Gibt den Aktualitätsvektor für einen Domänencontroller|  
|Get-ADTrust|Gibt Informationen über eine Domänen- oder gesamtstrukturübergreifende Vertrauensstellung zurück|  
|New-ADReplicationSite|Erstellt einen neuen Standort|  
|Neue ADReplicationSiteLink|Erstellt eine neue standortverknüpfung|  
|Neue ADReplicationSiteLinkBridge|Erstellt eine neue Standortverknüpfungsbrücke|  
|Neue ADReplicationSubnet|Erstellt ein neues AD-Subnetz|  
|Remove-ADReplicationSite|Löscht einen Standort|  
|Remove-ADReplicationSiteLink|Löscht eine standortverknüpfung|  
|Remove-ADReplicationSiteLinkBridge|Löscht eine Standortverknüpfungsbrücke|  
|Remove-ADReplicationSubnet|Löscht ein AD-Subnetz|  
|Set-ADReplicationConnection|Bearbeitet eine Verbindung|  
|Set-ADReplicationSite|Bearbeitet einen Standort|  
|Set-ADReplicationSiteLink|Bearbeitet eine standortverknüpfung|  
|Set-ADReplicationSiteLinkBridge|Bearbeitet eine Standortverknüpfungsbrücke|  
|Set-ADReplicationSubnet|Ändert ein AD-Subnetz|  
|Sync-ADObject|Erzwingt die Replikation eines einzelnen Objekts|  
  
Die meisten dieser Cmdlets müssen die Basis Repadmin.exe. Andere (nicht aufgelistete) Cmdlets verwalten Features wie die dynamische Zugriffssteuerung und Gruppenverwaltete Dienstkonten.  
  
Für eine vollständige Liste aller Active Directory Windows PowerShell-Cmdlets ausführen:  
  
```  
Get-command -module ActiveDirectory  
```  
  
Verweisen Sie eine vollständige Liste aller Active Directory Windows PowerShell-Cmdlet-Argumente die Hilfe. Zum Beispiel:  
  
```  
Get-help New-ADReplicationSite  
  
```  
  
Verwenden der `Update-Help` -Cmdlet zum Herunterladen und Installieren von Hilfedateien  
  
### <a name="BKMK_Repl"></a>Replikation und Metadaten  
Repadmin.exe prüft Integrität und Konsistenz der Active Directory-Replikation. Repadmin.exe bietet einfache Optionen – einige Argumente unterstützen CSV-Ausgaben, z. B. - Automatisierung müssen jedoch normalerweise Ausgaben analysieren. Active Directory-Modul für Windows PowerShell ist der erste Versuch zu bieten, die echte Kontrolle über die zurückgegebenen Daten ermöglicht. zuvor mussten Sie zum Erstellen von Skripts oder Tools von Drittanbietern verwenden.  
  
Die folgenden Cmdlets implementieren Sie zusätzlich einen neuer Parametersatz **Ziel**, **Bereich**, und **EnumerationServer**:  
  
-   **Get-ADReplicationFailure**  
  
-   **Get-ADReplicationPartnerMetadata**  
  
-   **Get-ADReplicationUpToDatenessVectorTable**  
  
Die **Ziel** -Argument akzeptiert eine durch Trennzeichen getrennte Liste von Zeichenfolgen, die den Zielserver, Standorte, Domänen oder Gesamtstrukturen, die vom angegebenen Identifizieren der **Bereich** Argument. Ein Sternchen (\ *) ist auch zulässig und bezeichnet alle Server innerhalb des angegebenen Bereichs. Wenn kein Bereich angegeben ist, bedeutet es alle Server in der aktuellen Gesamtstruktur des Benutzers. Die **Bereich** Argument gibt die Breite der Suche. Zulässige Werte sind **Server**, **Website**, **Domäne**, und **Gesamtstruktur**. Die **EnumerationServer** gibt den Server an, die die Liste der Domänencontroller im angegebenen listet **Ziel** und **Bereich**. Es verläuft genauso wie die **Server** Argument und der angegebene Server Active Directory-Webdienst ausführen muss.  
  
Um die neuen Cmdlets sind hier einige Szenarien mit Funktionen Repadmin.exe nicht möglich. folgen, werden die administrativen Möglichkeiten offensichtlich. Überprüfen Sie die Cmdlet-Hilfe zur spezifischen Syntax.  
  
### <a name="BKMK_ReplAttrMD"></a>Get-ADReplicationAttributeMetadata  
Dieses Cmdlet ähnelt **repadmin.exe/showobjmeta**. Sie können die gibt Replikationsmetadaten zurück, z. B. Änderungszeitpunkt eines Attributs, den Ursprungs-Domänencontroller, die Version und USN-Informationen und Attributdaten. Dieses Cmdlet ist hilfreich, müssen, wo und wann eine Änderung durchgeführt wurde.  
  
Im Gegensatz zu Repadmin steuern Windows PowerShell bietet flexible Suche und Ausgabe. Beispielsweise können Sie die Metadaten des Domänen-Admins-Objekts sortiert als lesbare Liste ausgeben:  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list  
  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)  
  
Alternativ können Sie die Daten wie Repadmin, in einer Tabelle anordnen:  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap  
  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)  
  
Sie können auch Metadaten für eine gesamte Objektklasse, abrufen, indem pipelining der **Get-Adobject** mit einem Filter, z. B. alle Gruppen - Cmdlet kombinieren, die dann mit einem bestimmten Datum. Pipelines sind Kanäle zur Datenübergabe zwischen mehreren Cmdlets zum Übergeben von Daten. Um alle Gruppen, die in irgendeiner Weise geändert werden, am 13. Januar 2012 finden Sie unter:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)  
  
Weitere Informationen zu Windows PowerShell-Operationen mit Pipelines finden Sie unter [Piping und die Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).  
  
Alternativ hat, erfahren Sie, jede Gruppe, die Tony Wang Mitglied und die Gruppe zuletzt geändert wurde:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto  
  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)  
  
Alternativ wiederhergestellt finden Sie alle Objekte autorisierend mit eine Sicherung des Systemstatus in der Domäne anhand ihrer künstlich hohen Versionsnummer:  
  
```  
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)  
  
Sie können auch senden Sie aller in eine CSV-Datei zur späteren Prüfung in Microsoft Excel:  
  
```  
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv  
```  
  
### <a name="BKMK_PartnerMD"></a>Get-ADReplicationPartnerMetadata  
Dieses Cmdlet gibt Informationen über die Konfiguration und den Status der Replikation für einen Domänencontroller, sodass Sie überwachen, Inventur und Problembehandlung. Im Gegensatz zu Repadmin.exe bedeutet das, dass Windows PowerShell, dass Sie nur die Daten angezeigt, die wichtig sind, im Format ist, werden sollen.  
  
Beispiel: der lesbare Replikationsstatus eines einzelnen Domänencontrollers:  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)  
  
Alternativ der Zeitpunkt der letzten eines Domänencontrollers Replikation eingehende und seinen Partnern in einer Tabelle formatieren:  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)  
  
Sie können auch wenden Sie sich an alle Domänencontroller in der Gesamtstruktur und diejenigen zeigen Sie, deren letzter Replikationsversuch aus irgendeinem Grund ein Fehler aufgetreten ist an:  
  
```  
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto  
  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)  
  
### <a name="BKMK_ReplFail"></a>Get-ADReplicationFailure  
Dieses Cmdlet kann gibt Informationen über aktuelle Fehler bei der Replikation verwendet werden. Es entspricht **Repadmin.exe showreplsum**, aber in diesem Fall mit wesentlich mehr Kontrolle Dank Windows PowerShell.  
  
Beispielsweise können Sie zurückkehren, die aktuellsten Fehler eines Domänencontrollers und er konnte wenden Sie sich an Partner:  
  
```  
Get-ADReplicationFailure dc1.corp.contoso.com  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)  
  
Geben Sie alternativ eine Tabellenansicht für alle Server in einem logischen AD-Standort, sortiert zur leichteren Analyse und enthält nur die wichtigsten Daten zurück:  
  
```  
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto  
  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)  
  
### <a name="BKMK_ReplQueue"></a>Get-ADReplicationQueueOperation und Get-ADReplicationUpToDatenessVectorTable  
Beide Cmdlets gibt weitere Aspekte des Domänencontrollers "Versionsvektoren", die ausstehender Replikationen und Informationen enthält.  
  
### <a name="BKMK_Sync"></a>Sync-ADObject  
Dieses Cmdlet entspricht der Ausführung **Repadmin.exe/replsingleobject**. Es ist sehr nützlich, wenn Sie Änderungen, für die Out-Band-Replikation erforderlich vornehmen, insbesondere, um ein Problem zu beheben.  
  
Beispielsweise, wenn jemand Benutzerkonto des Geschäftsführers gelöscht, und klicken Sie dann mit der Active Directory-Papierkorb wiederhergestellt, möchten Sie wahrscheinlich, dass er sofort auf alle Domänencontroller repliziert. Sie möchten wahrscheinlich auch ohne Erzwingen der Replikation alle anderen Objekt Änderungen; Schließlich ist daher stehen Ihnen einen Replikationszeitplan -, damit nicht überlastet WAN-Links.  
  
```  
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}  
  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)  
  
### <a name="BKMK_Topo"></a>Topologie  
Repadmin.exe ist, zwar gut Daten über Replikationstopologien wie z. B. Standorten, standortverknüpfungen, Standortverknüpfungsbrücken und Verbindungen verfügt es nicht über einen umfassenden Satz von Argumenten Änderungen vornehmen. In der Tat nie wurde Skriptgesteuertes, integriertes Windows-Hilfsprogramm speziell für Administratoren, die AD DS-Topologien zu erstellen. Wie Active Directory in Millionen von kundenumgebungen gereift, ändern die Notwendigkeit, stapelweises Active Directory wird deutlich, logische Informationen.  
  
Z. B. möglicherweise nach einer schnellen Erweiterung neuer Filialen, und der Konsolidierung anderer, standortänderungen Sie basierend auf physischen Standorten, netzwerkänderungen und neuen kapazitätsanforderungen haben. Anstatt Dssites.msc und Adsiedit.msc Änderungen vornehmen, können Sie automatisieren. Dies ist besonders überzeugend, wenn Sie eine Tabelle mit den Daten von Ihrem Netzwerk- und einrichtungsteams erhalten starten.  
  
Die **abrufen-Adreplication\ *** Cmdlets geben Informationen über die Replikationstopologie zurück und sind hilfreich in Verbindung mit der **festlegen-Adreplication\ *** Cmdlets zusammen. **Abrufen** Cmdlets ändern keine Daten, sie zeigt nur Daten oder zum Erstellen von Windows PowerShell-Sitzung Objekte, aufgenommen werden können, um **festlegen-Adreplication\ *** Cmdlets. Die **neu** und **entfernen** Cmdlets sind hilfreich zum Erstellen oder Entfernen von Active Directory-Topologie-Objekte.  
  
Sie können z. B. neue Standorte mit einer CSV-Datei erstellen:  
  
```  
import-csv -path C:\newsites.csv | new-adreplicationsite  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)  
  
Alternativ erstellen Sie eine neue standortverknüpfung zwischen zwei existierenden Standorten mit benutzerdefiniertem Replikationsintervall und Kosten:  
  
```  
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)  
  
Sie können auch jeder Standort in der Gesamtstruktur suchen und ersetzen die **Optionen** ändern Attribute durch eine Kennzeichnung zum Aktivieren der standortübergreifenden Benachrichtigung, um mit maximaler Geschwindigkeit mit Komprimierung zu replizieren:  
  
```  
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)  
  
> [!IMPORTANT]  
> Legen Sie **--Bor 5** Komprimierung für diese standortverknüpfungen ebenfalls deaktivieren.  
  
Oder Sie suchen nach allen Standorten mit fehlenden Subnetz-Zuweisungen, um die Liste mit den tatsächlichen Subnetzen dieser Standorte abzustimmen:  
  
```  
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name  
```  
  
![Erweiterte Verwaltung mit powershell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)  
  
## <a name="see-also"></a>Siehe auch  
[Einführung in die Active Directory-Replikation und Topologieverwaltung mithilfe von WindowsPowerShell & #40; Stufe 100 & #41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)  
  

