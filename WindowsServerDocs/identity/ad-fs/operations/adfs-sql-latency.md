---
title: In Ordnung ist, werden Optimierung von SQL und Behandlung von Latenzproblemen mit AD FS
description: In diesem Dokument wird erläutert, wie zur Feinabstimmung von SQL mit AD FS wird.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 06/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb699a1f92013f5657d2fbb48b203f96a5e5a5ba
ms.sourcegitcommit: 6b6c3601fb7493ab145ccff02db26d7123df9a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/21/2019
ms.locfileid: "67322857"
---
# <a name="fine-tuning-sql-and-addressing-latency-issues-with-ad-fs"></a>In Ordnung ist, werden Optimierung von SQL und Behandlung von latenzproblemen mit AD FS
In einem Update für [AD FS 2016](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) vorgestellt, die folgenden Verbesserungen an plattformübergreifende Datenbank Latenz zu verringern. Eine zukünftigen Update für AD FS-2019 wird diese Verbesserungen umfassen.

## <a name="in-memory-cache-update-in-background-thread"></a>In-Memory-Cache-Update im Hintergrund-thread 
In früheren Always on-Verfügbarkeitsgruppen (AoA)-Bereitstellungen, Latenz vorhanden waren, für alle "Lesen" Vorgang wie der Masterknoten in einem separaten Rechenzentrum gefunden werden konnte. Der Aufruf zwischen zwei Rechenzentren führte zu Wartezeit.  

Das neueste Update für AD FS ist eine Verringerung der Latenz durch Hinzufügen von einem Hintergrundthread zum Aktualisieren der AD FS-Konfiguration-Cache und eine zum Festlegen die Aktualisierung der Zeitraum vorgesehen. Die für eine Datenbanksuche aufgewendete Zeit wird in den Anforderungsthread, erheblich reduziert, wie die Datenbank-Cache-Updates in der Hintergrundthread verschoben werden.  

Bei der `backgroundCacheRefreshEnabled` nastaven NA hodnotu True gibt an, AD FS kann vom Hintergrundthread Cacheupdates ausführen. Die Häufigkeit der Abrufen von Daten aus dem Cache kann in einen Uhrzeitwert angepasst werden, durch Festlegen von `cacheRefreshIntervalSecs`. Der Standardwert ist 300 Sekunden festgelegt. wenn `backgroundCacheRefreshEnabled` wird festgelegt auf "true". Nach dem festgelegtem Wert Dauer, AD FS beginnt, dessen Cache aktualisiert, und während des Updates ausgeführt wird, weiterhin die alten Cachedaten verwendet werden.  

>[!NOTE]
> Der Cache Daten werden außerhalb von aktualisiert die `cacheRefreshIntervalSecs` -Wert, wenn AD FS empfängt eine Benachrichtigung SQL gibt an, dass eine Änderung in der Datenbank aufgetreten ist. Diese Benachrichtigung wird ausgelöst, den Cache aktualisiert werden. 

### <a name="recommendations-for-setting-the-cache-refresh"></a>Empfehlungen für das die cacheaktualisierung 
Der Standardwert für die Aktualisierung des Cache wird **fünf Minuten**. Es wird empfohlen, die festgelegt ist, dass **1 Stunde** um eine Aktualisierung nicht benötigte Daten von AD FS zu reduzieren, da die Daten im Cache aktualisiert werden werden, wenn alle SQL-Änderungen auftreten.  

AD FS registriert einen Rückruf für SQL-Änderungen, und auf eine Änderung der AD FS, die eine Benachrichtigung erhält. Durch diese Methode empfängt AD FS jedes neue Änderung von SQL, sobald es tritt ein. 

Im Falle einer netzwerkstörung Dies führt zu AD FS fehlt die SQL-Benachrichtigung, AD FS vom Cache angegebenen Intervall aktualisiert Wert aktualisiert wird. Wenn Sie alle Verbindungsprobleme zwischen AD FS und SQL vermutet werden, wird empfohlen, den Cache Aktualisierungswert senken als eine Stunde festzulegen.  

### <a name="configuration-instructions"></a>Konfigurationsanweisungen 
Die Konfigurationsdatei unterstützt mehrere Cacheeinträge. Die unten aufgeführten folgende können alle konfiguriert werden je nach den Anforderungen Ihrer Organisation. 

Im folgenden Beispiel wird die Aktualisierung im Hintergrund Cache aktiviert und wird der Cache-Aktualisierungszeitraum auf 1800 Sekunden und 30 Minuten. Dies muss erfolgen auf jedem AD FS-Knoten, und der AD FS-Dienst muss anschließend neu gestartet werden. Die Änderungen keine Auswirkungen auf andere Knoten, und testen den ersten Knoten vor der Änderung in allen Knoten. 

  1. Navigieren Sie zu der AD FS-Config-Datei und im Abschnitt "Microsoft.IdentityServer.Service", fügen Sie den folgenden Eintrag:  
  
  - `backgroundCacheRefreshEnabled`  – Gibt an, ob das Feature für den Hintergrund-Cache aktiviert ist. Werte für "True/False".
  - `cacheRefreshIntervalSecs` -Wert in Sekunden, die an denen AD FS der Cache aktualisiert wird. AD FS wird den Cache aktualisiert, wenn eine in der SQL Änderung. AD FS wird eine SQL-Benachrichtigung erhalten und den Cache aktualisieren.  
 
 >[!NOTE]
 > Alle Einträge in der Konfigurationsdatei sind die Groß-/Kleinschreibung beachtet.  
 &lt;cache cacheRefreshIntervalSecs="1800" backgroundCacheRefreshEnabled="true" /&gt; 
 
Zusätzliche unterstützte konfigurierbaren Werte: 

   - **MaxRelyingPartyEntries** : maximale Anzahl von der vertrauenden Seite Partei-Einträge, die AD FS im Arbeitsspeicher beibehalten werden sollen. Dieser Wert wird auch von der oAuth-Anwendungscache Berechtigung verwendet. Wenn es weitere Berechtigungen der Anwendung als vertrauende Seiten und sind Wenn alle im Arbeitsspeicher gespeichert werden, sollte dieser Wert die Anzahl der Anwendungsberechtigungen sein. Der Standardwert ist 1000.
   - **MaxIdentityProviderEntries** : Dieses ist die maximale Anzahl der Ansprüche Anbieter-Einträge, die AD FS im Arbeitsspeicher beibehalten wird. Der Standardwert ist 200. 
   - **MaxClientEntries** – Dies ist die maximale Anzahl der Einträge des OAuth-Clients, AD FS im Arbeitsspeicher beibehalten wird. Der Standardwert ist 500. 
   - **MaxClaimDescriptorEntries** : maximale Anzahl von Anspruchs-Deskriptor-Einträge, die AD FS im Arbeitsspeicher beibehalten wird. Der Standardwert ist 500. 
   - **MaxNullEntries** – Dies wird als negative Cache verwendet. Wenn AD FS nach einem Eintrag in der Datenbank sucht, und sie nicht gefunden wird, können Sie AD FS in negativen Cache hinzugefügt. Dies ist die maximale Größe dieses Caches. Negativer Cache für jeden Typ von Objekten vorhanden ist, es ist nicht für alle Objekte eines einzelnen Caches. Der Standardwert ist 50,0000. 

## <a name="multiple-artifact-db-support-across-datacenters"></a>Mehrere Artefakt DB in mehreren Rechenzentren zu unterstützen. 
Bei vorherigen Konfigurationen von mehreren Rechenzentren hat AD FS nur eine einzelne Datenbank Artefakt unterstützt verursacht Cross Center Datacenter-Latenz bei Datenabruf aufrufen.  

Um übergreifende Datacenter Latenz zu verringern, kann ein AD FS-Administratoren nun mehrere Instanzen der Artefakt-DB bereitstellen und ändern Sie eine AD FS-Knoten-Konfigurationsdatei auf verschiedenen Elementinstanzen DB verweisen. Die Artefakt-Datenbankverbindungszeichenfolge kann in der Konfigurationsdatei können eine knotenbasierte Artefakt-Datenbank bereitgestellt werden. Wenn die Verbindungszeichenfolge nicht in der Konfigurationsdatei vorhanden ist, wird der Knoten zurückgreifen auf die vorherige die Artefakt-Datenbank verwenden, die in der Konfiguration der Datenbank vorhanden ist.  
Hybrid-Umgebungen werden bei dieser Konfiguration ebenfalls unterstützt.  

### <a name="requirements"></a>Anforderungen: 
Vor dem Einrichten der Datenbank-Unterstützung für mehrere Artefakt, führen Sie ein Update auf allen Knoten, und die Binärdateien aktualisiert werden, weil mit mehreren Knoten-Aufrufe mittels dieser Funktion auftreten. 
  1. Generieren Sie Bereitstellungsskripts, um die Artefakt-Datenbank zu erstellen: Um mehrere Instanzen der Artefakt-DB bereitstellen zu können, müssen ein Administrator das SQL-Bereitstellungsskript für die Artefakt-Datenbank zu generieren. Im Rahmen des Updates, die vorhandene `Export-AdfsDeploymentSQLScript`Cmdlet wurde aktualisiert, um optional in einem Parameter, der angibt, welche die zum Generieren einer SQL-Bereitstellungsskripts für AD FS-Datenbank nutzen. 
 
 Um das Bereitstellungsskript für die Artefakt-Datenbank zu generieren, geben Sie z. B. die `-DatabaseType` Parameter, und übergeben den Wert "Element". Der optionale `-DatabaseType` Parameter gibt den Typ der AD FS-Datenbank und kann so festgelegt werden: Alle (Standard), Elements oder der Konfiguration. Wenn kein `-DatabaseType` -Parameter angegeben wird, das Skript wird sowohl die Konfiguration der Artefakt-Skripts konfigurieren.  

   ```PowerShell
   PS C:\> Export-AdfsDeploymentSQLScript -DestinationFolder <script folder where scripts will be created> -ServiceAccountName <domain\serviceaccount> -DatabaseType "Artifact" 
   ```
Das generierte Skript sollte auf dem SQL-Computer, die erforderlichen Datenbanken zu erstellen, und geben Sie die AD FS-Dienstkonto, das SQL-SA-Berechtigungen für diese Datenbanken ausgeführt werden.

 2. Erstellen Sie die Artefakt-Datenbank, die das Bereitstellungsskript verwenden. Kopieren Sie den neu generierten CreateDB.sql und SetPermissions.sql Bereitstellungsskripts mit dem SQL Server-Computer und führen Sie aus, um die local DB Artefakt erstellen. 
 
 3. Ändern Sie die Konfigurationsdatei, um die Artefakt-DB-Verbindung hinzuzufügen. 
 Navigieren Sie zur Konfigurationsdatei für die AD FS-Knoten, und klicken Sie im Abschnitt "Microsoft.IdentityServer.Service", die neu konfigurierte ArtifactDB Einstiegspunkt hinzugefügt. 

 >[!NOTE] 
 > ArtifactStore ' und ' ConnectionString Werte Groß-/Kleinschreibung beachtet. Stellen Sie sicher, dass sie ordnungsgemäß konfiguriert sind. &lt;ArtifactStore ConnectionString = "Data Source =. \SQLInstance; Integrated Security = True; Initial Catalog = AdfsArtifactStore" /&gt; 
>
>Verwenden Sie einen Datenquelle-Wert, der die Sql-Verbindung entspricht.



 4. Starten Sie den AD FS-Dienst für die Änderungen wirksam werden. 
 
 >[!NOTE] 
 > Es wird nicht empfohlen, SQL-Replikation oder die Synchronisierung zwischen den Artefakt-Datenbanken zu verwenden. Es wird empfohlen, um ein Element pro Datencenter einzurichten. 
 
### <a name="cross-datacenter-failover-and-database-recovery"></a>Plattformübergreifende Datencenter-Failover und datenbankwiederherstellung  
Es wird empfohlen, Datenbanken der Failover-Element im gleichen Datencenter als Artefakt der master-Datenbank zu erstellen. Wenn ein Failover auftritt, wird keine Anstieg der Wartezeit vorhanden sein. Failover-Artefakt-Datenbanken in mehreren Rechenzentren wird nicht empfohlen. Im folgenden erläutert, wie Aufrufe für OAuth, SAML, zusammenfassender Meldung und Token Funktion mit mehreren Artefakt Datenbanken wiedergeben. 
 - **OAuth und SAML** 

   Für OAuth und SAML-Artefakt-Anforderungen wird der Knoten erstellt das Artefakt im Artefakt DB vorhanden ist, in der Konfigurationsdatei. Wenn die Konfigurationsdatei nicht über eine datenbankverbindung Artefakt enthält, wird das allgemeine Artefakt DB verwendet. Wenn die nächste Anforderung zum Abrufen des Artefakts auf einen anderen Knoten wechselt, veranlasst der andere Knoten Rest-API auf den 1. Knoten aus, um das Element aus das Artefakt DB abzurufen. Dies ist erforderlich, da es sich bei verschiedene Knoten möglicherweise verschiedene Artefakt-Datenbanken und die Knoten nicht wissen, zu. Wenn der 1. Knoten ausgefallen ist, schlägt die artefaktauflösung fehl. Aufgrund dessen ist das Replizieren des Artefakts DB in verschiedenen Datencentern nicht erforderlich. Wenn ein gesamtes Rechenzentrum ausfällt, wird in den meisten Fällen der Knoten, der das Element erstellt auch nach unten, was bedeutet, dass dieses Element nicht mehr aufgelöst werden kann.  

 - **Extranetsperre** 

    Die Artefakt-Datenbank, die auf die verwiesen wird in der Konfigurationsdatei wird für Extranetsperre Daten verwendet werden. Für die Funktion zusammenfassender Meldung wählt AD FS hingegen einem Masterauftrag für den die Daten im Artefakt DB schreibt. Alle Knoten stellen eine REST-API aufrufen, um den Masterknoten abrufen und die neueste Informationen zu jedem Benutzer festlegen. Wenn mehrere Artefakt DB verwendet werden, muss der Administrator ein Masterknoten für jedes Artefakt DB oder Datencenter auswählen. 

    So wählen Sie einen Knoten, der die Master zusammenfassender Meldung sein, navigieren zu den AD FS-Knoten-Config-Datei, und klicken Sie im Abschnitt "Microsoft.IdentityServer.Service", fügen Sie die folgenden aus:       
    
    Fügen Sie folgenden Eintrag hinzu, auf dem masterzielserver. Beachten Sie, dass alle drei Product Keys Groß-/Kleinschreibung beachtet werden. 

    &lt;Useractivityfarmrole MasterFQDN = [FQDN von der ausgewählten primären] IsMaster = "true" /&gt;
    
    Auf den anderen Knoten fügen Sie den folgenden Eintrag:

   &lt;Useractivityfarmrole MasterFQDN = [FQDN von der ausgewählten primären] IsMaster = "false" /&gt;
 
    >[!NOTE] 
    >Da mehrere Artefakt Datenbanken keine Daten synchronisieren, werden zusammenfassender Meldung Werte zwischen Artefakt-Datenbanken nicht synchronisiert.
    Benutzer kann möglicherweise drücken, ein anderen Rechenzentrum für eine Anforderung, sodass die ExtranetLockoutThreshold hängt von der Anzahl der Artefakt-Datenbanken und ExtranetLockoutThreshold * Anzahl der Artefakt-Datenbanken. 
 
  - **Erkennung einer Tokenmehrfachverwendung** 
    
    Erkennungsdaten von Löschvorgängen Token-Replay werden immer über die zentrale Datenbank für das Element aufgerufen werden. AD FS speichert das Token der Anspruchsanbieter-Vertrauensstellung, sicherzustellen, dass das gleiche Token wiedergegeben werden kann. Wenn ein Angreifer versucht, die das gleiche Token wiedergegeben, wird überprüft, AD FS die Token in der Artefakt-Datenbank vorhanden ist. Wenn das Token vorhanden ist, wird die Anforderung zurückgewiesen werden. Die zentrale Datenbank für das Artefakt wird verwendet, aus Sicherheitsgründen, da die Artefakt-DB-Daten nicht repliziert werden, ein Angreifer kann die Anforderung an ein anderes Datencenter senden und ein Token wiedergegeben. Erstellen zusätzliche schreibgeschützte Kopien der ArtifactDB werden Cross Datacenter Latenz in diesem Szenario nicht verhindern, wie nur die zentrale Datenbank Artefakt verwendet wird.    
 
 