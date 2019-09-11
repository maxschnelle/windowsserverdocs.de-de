---
title: Optimieren von SQL und Beheben von Latenzproblemen mit AD FS
description: In diesem Dokument wird erläutert, wie Sie SQL mit AD FS optimieren.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 06/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 29c8e8ba52f62a335ab136756e759b6114ecfb20
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865610"
---
# <a name="fine-tuning-sql-and-addressing-latency-issues-with-ad-fs"></a>Optimieren von SQL und Beheben von Latenzproblemen mit AD FS
In einem Update für [AD FS 2016](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) haben wir die folgenden Verbesserungen eingeführt, um die datenbankübergreifende Latenz zu verringern. Ein demnächst erbendes Update für AD FS 2019 umfasst diese Verbesserungen.

## <a name="in-memory-cache-update-in-background-thread"></a>In-Memory-Cache Update im Hintergrund Thread 
In früheren bereit Stellungen von AlwaysOn-Verfügbarkeit (AOA) gab es für jeden Lesevorgang eine Latenz, da sich der Master Knoten in einem separaten Rechenzentrum befinden konnte. Der-Rückruf zwischen zwei unterschiedlichen Daten Centern führte zu einer Latenz.  

Beim neuesten Update für AD FS wird eine Verringerung der Latenz durch das Hinzufügen eines Hintergrundthreads zum Aktualisieren des AD FS Konfigurations Caches und eine Einstellung zum Festlegen des Aktualisierungs Zeitraums angestrebt. Die für eine Datenbanksuche aufgewendeten Zeit wird im Anforderungs Thread erheblich reduziert, da die Daten Bank Cache Updates in den Hintergrund Thread verschoben werden.  

Wenn auf true festgelegt ist,ermöglichtADFSdemHintergrundThreaddasAusführenvonCacheUpdates.`backgroundCacheRefreshEnabled` Die Häufigkeit, mit der Daten aus dem Cache abgerufen werden können, kann durch Festlegen `cacheRefreshIntervalSecs`von auf einen Zeitwert angepasst werden. Der Standardwert ist auf 300 Sekunden festgelegt `backgroundCacheRefreshEnabled` , wenn auf true festgelegt ist. Nach der festgelegten Wert Dauer beginnt AD FS mit der Aktualisierung des Caches, und während das Update ausgeführt wird, werden die alten Cache Daten weiterhin verwendet.  

>[!NOTE]
> Die Daten des Caches werden außerhalb des `cacheRefreshIntervalSecs` Werts aktualisiert, wenn von ADFS eine Benachrichtigung von SQL empfangen wird, was bedeutet, dass in der Datenbank eine Änderung aufgetreten ist. Diese Benachrichtigung löst die Aktualisierung des Caches aus. 

### <a name="recommendations-for-setting-the-cache-refresh"></a>Empfehlungen zum Festlegen der Cache Aktualisierung 
Der Standardwert für die Cache Aktualisierung ist **fünf Minuten**. Es wird empfohlen, den Wert auf **1 Stunde** festzulegen, um eine unnötige Datenaktualisierung durch AD FS zu vermeiden, da die Cache Daten aktualisiert werden, wenn SQL-Änderungen auftreten.  

AD FS registriert einen Rückruf für SQL-Änderungen, und bei einer Änderung erhält ADFS eine Benachrichtigung. Mit dieser Methode empfängt ADFS jede neue Änderung von SQL, sobald Sie auftritt. 

Bei einem netzwerkglitch, bei dem die SQL-Benachrichtigung AD FS fehlt, wird AD FS in dem durch den Cache Aktualisierungs Wert angegebenen Intervall aktualisiert. Wenn Konnektivitätsprobleme zwischen AD FS und SQL vermutet werden, empfiehlt es sich, den Cache Aktualisierungs Wert auf weniger als eine Stunde festzulegen.  

### <a name="configuration-instructions"></a>Konfigurations Anweisungen 
Die Konfigurationsdatei unterstützt mehrere Cache Einträge. Die unten aufgeführten Angaben können je nach den Anforderungen Ihrer Organisation konfiguriert werden. 

Im folgenden Beispiel wird die Aktualisierung des Hintergrund Caches aktiviert und der Cache Aktualisierungs Zeitraum auf 1800 Sekunden oder 30 Minuten festgelegt. Dies muss auf jedem AD FS-Knoten erfolgen, und der ADFS-Dienst muss danach neu gestartet werden. Die Änderungen wirken sich nicht auf andere Knoten aus und testen den ersten Knoten, bevor Sie die Änderung in allen Knoten vornehmen. 

  1. Navigieren Sie zur AD FS config-Datei, und fügen Sie im Abschnitt "Microsoft. identityserver. Service" den folgenden Eintrag hinzu:  
  
  - `backgroundCacheRefreshEnabled`: Gibt an, ob die Hintergrund Cache Funktion aktiviert ist. true/false-Werte.
  - `cacheRefreshIntervalSecs`-Wert in Sekunden, bei dem der Cache von ADFS aktualisiert wird. AD FS aktualisiert den Cache, wenn SQL geändert wird. AD FS wird eine SQL-Benachrichtigung empfangen und den Cache aktualisieren.  
 
 >[!NOTE]
 > Bei allen Einträgen in der Konfigurationsdatei wird die Groß-/Kleinschreibung beachtet.  
 &lt;Cache cacherefreshintervalabcs = "1800" backgroundcacherefreshaktivierte = "true"/&gt; 
 
Weitere konfigurierbare Werte werden unterstützt: 

   - **maxrelyingpartyentries** : maximale Anzahl von Einträgen der vertrauenden Seite, die AD FS im Arbeitsspeicher beibehalten werden. Dieser Wert wird auch vom OAuth-Anwendungs Berechtigungs Cache verwendet. Wenn mehr Anwendungs Berechtigungen als RPS vorhanden sind und alle im Arbeitsspeicher gespeichert werden, sollte dieser Wert der Anzahl von Anwendungs Berechtigungen entsprechen. Der Standardwert ist 1000.
   - **maxidentityproviderentries** : Dies ist die maximale Anzahl von Anspruchs Anbieter Einträgen, AD FS im Arbeitsspeicher beibehalten werden. Der Standardwert ist 200. 
   - **maxcliententries** : Dies ist die maximale Anzahl von OAuth-Client Einträgen, AD FS im Arbeitsspeicher beibehalten werden. Der Standardwert ist 500. 
   - **maxclaimdescriptorentries** : maximale Anzahl von Anspruchs Deskriptoreinträgen AD FS die im Arbeitsspeicher beibehalten werden. Der Standardwert ist 500. 
   - **maxnullentries** : wird als negativer Cache verwendet. Wenn AD FS nach einem Eintrag in der Datenbank sucht und nicht gefunden wird, fügt AD FS einen negativen Cache hinzu. Dies ist die maximale Größe des Caches. Für jeden Objekttyp gibt es einen negativen Cache, es handelt sich jedoch nicht um einen einzelnen Cache für alle Objekte. Der Standardwert ist 50, 0000. 

## <a name="multiple-artifact-db-support-across-datacenters"></a>Unterstützung mehrerer artefaktdb über Rechenzentren hinweg 
Bei früheren Konfigurationen mehrerer Daten Center hat AD FS nur eine einzelne artefaktdatenbank unterstützt, die während Abruf aufrufen eine Rechenzentrums übergreifende Latenz verursacht hat.  

Um die Latenz zwischen Rechenzentren zu reduzieren, kann ein AD FS Administrator nun mehrere artefaktdb-Instanzen bereitstellen und dann die Konfigurationsdatei eines AD FS Knotens ändern, sodass Sie auf verschiedene artefaktdb-Instanzen verweist. Die artefaktdatenbank-Verbindungs Zeichenfolge kann in der Konfigurationsdatei bereitgestellt werden, die eine Knoten übergreifende artefaktdatenbank zulässt. Wenn die Verbindungs Zeichenfolge in der Konfigurationsdatei nicht vorhanden ist, greift der Knoten auf den vorherigen Entwurf zurück, um die artefaktdatenbank zu verwenden, die in der Konfigurations Datenbank vorhanden ist.  
Hybrid Umgebungen werden auch mit dieser Konfiguration unterstützt.  

### <a name="requirements"></a>Anforderungen: 
Vor dem Einrichten mehrerer artefaktdatenbankunterstützung führen Sie ein Update auf allen Knoten aus, und aktualisieren Sie die Binärdateien, da die Aufrufe mehrerer Knoten über dieses Feature erfolgen. 
  1. Generieren eines Bereitstellungs Skripts zum Erstellen der artefaktdatenbank: Zum Bereitstellen mehrerer artefaktdb-Instanzen muss ein Administrator das SQL-Bereitstellungs Skript für die artefaktdatenbank generieren. Als Teil dieses Updates wurde das vorhandene `Export-AdfsDeploymentSQLScript`Cmdlet aktualisiert und gibt optional einen Parameter an, der angibt, für welche AD FS Datenbank ein SQL-Bereitstellungs Skript generiert werden soll. 
 
 Um z. b. das Bereitstellungs Skript nur für die artefaktdatenbank zu `-DatabaseType` generieren, geben Sie den Parameter an, und übergeben Sie den Wert "artefaktname". Der optionale `-DatabaseType` -Parameter gibt den Datenbanktyp AD FS an und kann auf festgelegt werden: Alle (Standard), artefaktdatei oder Konfiguration. Wenn kein `-DatabaseType` Parameter angegeben wird, konfiguriert das Skript sowohl das artefaktkonfigurations-als auch das Konfigurationsskript.  

   ```PowerShell
   PS C:\> Export-AdfsDeploymentSQLScript -DestinationFolder <script folder where scripts will be created> -ServiceAccountName <domain\serviceaccount> -DatabaseType "Artifact" 
   ```
Das generierte Skript sollte auf dem SQL-Computer ausgeführt werden, um die erforderlichen Datenbanken zu erstellen und dem AD FS Dienst Konto, SQL SA-Berechtigungen für diese Datenbanken zu geben.

 2. Erstellen Sie die artefaktdatenbank mithilfe des Bereitstellungs Skripts. Kopieren Sie die neu generierten Bereitstellungs Skripts "mpatedb. SQL" und "setberechtigungs-SQL" auf den SQL Server-Computer, und führen Sie Sie aus, um die lokale artefaktdatenbank 
 
 3. Ändern Sie die Konfigurationsdatei, um die artefaktdb-Verbindung hinzuzufügen. 
 Navigieren Sie zur Konfigurationsdatei des AD FS Knotens, und fügen Sie im Abschnitt "Microsoft. identityserver. Service" der neu konfigurierten artifactdb einen Einstiegspunkt hinzu. 

 >[!NOTE] 
 > bei artifactstore und ConnectionString werden die Groß-/Kleinschreibung beachtet. Stellen Sie sicher, dass Sie richtig konfiguriert sind. &lt;artifactstore ConnectionString = "Data Source = .\SQLinstance; Integrated Security = true; Initial Catalog = adfsartifactstore"/&gt; 
>
>Verwenden Sie einen Datenquellen Wert, der mit Ihrer SQL-Verbindung übereinstimmt.



 4. Starten Sie den AD FS-Dienst neu, damit die Änderungen wirksam werden. 
 
 >[!NOTE] 
 > Es wird nicht empfohlen, die SQL-Replikation oder die Synchronisierung zwischen den artefaktdatenbanken zu verwenden. Es wird empfohlen, eine artefaktdatenbank pro Rechenzentrum einzurichten. 
 
### <a name="cross-datacenter-failover-and-database-recovery"></a>Rechenzentrums übergreifende Failover und Daten Bank Wiederherstellung  
Es wird empfohlen, failoverartefaktdatenbanken in demselben Rechenzentrum wie die Haupt artefaktdatenbank zu erstellen. Wenn ein Failover auftritt, erfolgt keine Erhöhung der Latenz. Failoverartefaktionsdatenbanken über Rechenzentren hinweg werden nicht empfohlen. Im folgenden wird erläutert, wie Aufrufe von OAuth, SAML, ESL und der tokenwiedergabe-Erkennungsfunktion mit mehreren artefaktdatenbanken durchgesetzt werden. 
 - **OAuth und SAML** 

   Für OAuth-und SAML-artefaktanforderungen erstellt der Knoten das Element in der artefaktdatenbank, das in der Konfigurationsdatei vorhanden ist. Wenn die Konfigurationsdatei keine artefaktdatenbankverbindung enthält, wird die allgemeine artefaktdatenbank verwendet. Wenn die nächste Anforderung zum Abrufen des Artefakts an einen anderen Knoten weitergeleitet wird, macht der andere Knoten die Rest-API für den ersten Knoten aus, um das Element aus der artefaktdatenbank abzurufen. Dies ist erforderlich, da unterschiedliche Knoten möglicherweise unterschiedliche artefaktdatenbanken aufweisen und diese von den Knoten nicht bekannt sind. Wenn der erste Knoten ausfällt, tritt bei der artefaktauflösung ein Fehler auf. Aufgrund dieses Entwurfs ist die Replikation der artefaktdatenbank in verschiedenen Rechenzentren nicht erforderlich. Wenn ein gesamtes Rechenzentrum inkonsistent ist, ist der Knoten, der das Element erstellt hat, ebenfalls inkonsistent, was bedeutet, dass das artefaktelement nicht mehr aufgelöst werden kann.  

 - **Extranetsperre** 

    Die artefaktdatenbank, auf die in der Konfigurationsdatei verwiesen wird, wird für extranetsperrungsdaten verwendet. Für das ESL-Feature wählt AD FS jedoch einen Master aus, der die Daten in die artefaktdatenbank schreibt. Alle Knoten führen einen Rest-API-Rückruf an den Master Knoten aus, um die neuesten Informationen zu den einzelnen Benutzern abzurufen und festzulegen. Wenn mehrere artefaktdb verwendet werden, muss der Administrator einen Master Knoten für jedes artefaktdb-oder Datacenter-Element auswählen. 

    Um einen Knoten als ESL-Master auszuwählen, navigieren Sie zur Konfigurationsdatei des ADFS-Knotens, und fügen Sie im Abschnitt "Microsoft. identityserver. Service" Folgendes hinzu:       
    
    Fügen Sie auf dem Master-Eintrag folgenden Eintrag hinzu. Beachten Sie, dass bei allen drei Schlüsseln zwischen Groß-und Kleinschreibung 

    &lt;useractivityfarmrole masterbqdn = [voll qualifizierter Name der primären Datenbank] IsMaster = "true"/&gt;
    
    Fügen Sie auf den anderen Knoten den folgenden Eintrag hinzu:

   &lt;useractivityfarmrole masterbqdn = [voll qualifizierter Schlüssel der ausgewählten primären Datenbank] IsMaster = "false"/&gt;
 
    >[!NOTE] 
    >Da die Daten von mehreren artefaktdatenbanken nicht synchronisiert werden, werden die ESL-Werte nicht zwischen artefaktdatenbanken synchronisiert.
    Ein Benutzer kann möglicherweise ein anderes Daten Center für eine Anforderung erreichen und somit den extranetlockoutthreshold abhängig von der Anzahl der artefaktdatenbanken, extranetlockoutthreshold * Anzahl der artefaktdatenbanken. 
 
  - **Erkennung von tokenwiedergabe** 
    
    Tokenwiedergabe-Erkennungs Daten werden immer von der zentralen artefaktdatenbank aufgerufen. AD FS speichert das Token von der Anspruchs Anbieter-Vertrauensstellung, um sicherzustellen, dass das gleiche Token nicht wiedergegeben werden kann. Wenn ein Angreifer versucht, dasselbe Token wiederzugeben, AD FS überprüft, ob das Token in der artefaktdatenbank vorhanden ist. Wenn das Token vorhanden ist, wird die Anforderung abgelehnt. Die zentrale artefaktdatenbank wird aus Sicherheitsgründen verwendet, da die artefaktdatenbankdaten nicht repliziert werden, könnte ein Angreifer die Anforderung an ein anderes Rechenzentrum senden und ein Token wiedergeben. Durch das Erstellen zusätzlicher Schreib geschützter Kopien von artifactdb wird in diesem Szenario keine Rechenzentrums übergreifende Latenz verhindert, da nur die zentrale artefaktdatenbank verwendet wird.    
 
 