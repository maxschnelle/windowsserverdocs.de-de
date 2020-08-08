---
title: Problembehandlung mithilfe des geschützten Fabric-Diagnosetools
ms.topic: article
ms.assetid: 07691d5b-046c-45ea-8570-a0a85c3f2d22
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 01/14/2020
ms.openlocfilehash: a0537c938b86141f83857f1763fbb18260a23e42
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944193"
---
# <a name="troubleshooting-using-the-guarded-fabric-diagnostic-tool"></a>Problembehandlung mithilfe des geschützten Fabric-Diagnosetools

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie häufige Fehler bei der Bereitstellung, Konfiguration und beim laufenden Betrieb der geschützten Fabric-Infrastruktur mithilfe des geschützten Fabric-Diagnosetools identifizieren und beheben. Dies schließt den Host-Überwachungsdienst (Host Guardian Service, HGS), alle überwachten Hosts und unterstützende Dienste wie DNS und Active Directory ein. Das Diagnosetool kann verwendet werden, um einen ersten Durchlauf bei der Selektierung eines fehlerhaften geschützten Fabrics durchzuführen, sodass Administratoren einen Ausgangspunkt für die Behebung von Ausfällen und die Identifizierung falsch konfigurierter Assets erhalten. Das Tool ist kein Ersatz für einen fundierten Einblick in das Betreiben eines geschützten Fabrics und dient nur der schnellen Überprüfung der häufigsten Probleme, die bei alltäglichen Vorgängen auftreten.

Eine vollständige Dokumentation der in diesem Artikel verwendeten Cmdlets finden Sie in der [Referenz zum hgsdiagnostics-Modul](https://docs.microsoft.com/powershell/module/hgsdiagnostics/?view=win10-ps).

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)]

## <a name="quick-start"></a>Schnellstart

Sie können entweder einen überwachten Host oder einen HGS-Knoten diagnostizieren, indem Sie den folgenden Befehl in einer Windows PowerShell-Sitzung mit lokalen Administratorrechten aufrufen:

```PowerShell
Get-HgsTrace -RunDiagnostics -Detailed
```

Dadurch wird automatisch die Rolle des aktuellen Hosts erkannt und relevante Probleme, die automatisch erkannt werden können, diagnostiziert.  Alle Ergebnisse, die während dieses Vorgangs generiert werden, werden aufgrund des Vorhandenseins des `-Detailed` Schalters angezeigt.

Im restlichen Teil dieses Themas finden Sie eine ausführliche Exemplarische Vorgehensweise für die Erweiterte Verwendung von zum Ausführen von Aufgaben `Get-HgsTrace` wie der gleichzeitigen Diagnose mehrerer Hosts und zum erkennen komplexer Knoten übergreifender Fehlkonfigurationen.

## <a name="diagnostics-overview"></a>Diagnose Übersicht

Die geschützte Fabric-Diagnose ist auf jedem Host verfügbar, auf dem geschützte virtuelle computerbezogene Tools und Features installiert sind, einschließlich Hosts, auf denen Server Core ausgeführt wird.  Derzeit sind die Diagnosen in den folgenden Features/Paketen enthalten:

1. Rolle "Host-Überwachungsdienst"
2. Host-Überwachungsunterstützung für Hyper-V
3. VM-Abschirmungstools für Fabric-Verwaltung
4. Remoteserver-Verwaltungstools (RSAT)

Dies bedeutet, dass Diagnosetools auf allen überwachten Hosts, HGS-Knoten, bestimmten Fabric-Verwaltungs Servern und allen Windows 10-Arbeitsstationen verfügbar sind, auf denen [rsat](https://www.microsoft.com/download/details.aspx?id=45520) installiert ist.  Die Diagnose kann von einem der oben genannten Computer aus aufgerufen werden, um alle überwachten Hosts oder HGS-Knoten in einem geschützten Fabric zu diagnostizieren. mithilfe von remotelaufverfolgungs-Zielen kann die Diagnose andere Hosts als den Computer mit Diagnose suchen und verbinden.

Jeder Host, der als Ziel der Diagnose dient, wird als "Ablauf Verfolgungs Ziel" bezeichnet.  Ablauf Verfolgungs Ziele werden anhand ihrer Hostnamen und Rollen identifiziert.  Rollen beschreiben die Funktion, die ein bestimmtes Ablauf Verfolgungs Ziel in einem geschützten Fabric ausführt.  Derzeit unterstützen Ablauf Verfolgungs Ziele `HostGuardianService` und `GuardedHost` Rollen.  Beachten Sie, dass es möglich ist, dass ein Host mehrere Rollen gleichzeitig einnimmt und auch von der Diagnose unterstützt wird. Dies sollte jedoch nicht in Produktionsumgebungen erfolgen.  Die HGS-und Hyper-V-Hosts sollten stets getrennt und voneinander getrennt werden.

Administratoren können alle Diagnose Tasks starten, indem Sie Ausführen `Get-HgsTrace` .  Dieser Befehl führt zwei unterschiedliche Funktionen basierend auf den Schaltern aus, die zur Laufzeit bereitgestellt werden: Ablauf Verfolgungs Sammlung und-Diagnose.  Diese beiden kombinierten bilden das gesamte geschützte Fabric-Diagnose Tool.  Obwohl Sie nicht explizit erforderlich sind, erfordern die meisten nützlichen Diagnosen Ablauf Verfolgungen, die nur mit Administrator Anmelde Informationen für das Ziel der Ablauf Verfolgung erfasst werden können.  Wenn der Benutzer, der die Ablauf Verfolgungs Sammlung ausführt, unzureichende Berechtigungen erhält, schlagen Ablauf Verfolgungen fehl, die eine Rechte Erweiterung erfordern, während alle anderen bestanden werden.  Dies ermöglicht eine partielle Diagnose in dem Fall, dass ein unterprivilegierter Operator eine selektiert durchführt.

### <a name="trace-collection"></a>Ablauf Verfolgungs Sammlung

Standardmäßig werden von nur Ablauf Verfolgungen `Get-HgsTrace` erfasst und in einem temporären Ordner gespeichert.  Ablauf Verfolgungen haben das Format eines Ordners, der nach dem Zielhost benannt ist und mit speziell formatierten Dateien gefüllt ist, die beschreiben, wie der Host konfiguriert ist.  Die Ablauf Verfolgungen enthalten außerdem Metadaten, die beschreiben, wie die Diagnose zum Erfassen der Ablauf Verfolgungen aufgerufen wurde.  Diese Daten werden von der Diagnose verwendet, um beim Ausführen der manuellen Diagnoseinformationen über den Host zu reaktivieren.

Bei Bedarf können Ablauf Verfolgungen manuell überprüft werden.  Alle Formate sind entweder von Menschen lesbar (XML) oder können mithilfe von Standard Tools (z. b. x. 509-Zertifikaten und den Windows-Crypto Shell-Erweiterungen) problemlos überprüft werden.  Beachten Sie jedoch, dass Ablauf Verfolgungen nicht für die manuelle Diagnose konzipiert sind und es immer effektiver ist, die Ablauf Verfolgungen mit den Diagnosefunktionen von zu verarbeiten `Get-HgsTrace` .

Die Ergebnisse der Ausführung der Ablauf Verfolgungs Sammlung geben keine Anzeichen für die Integrität eines bestimmten Hosts an.  Sie geben einfach an, dass Ablauf Verfolgungen erfolgreich erfasst wurden.  Die Diagnosefunktionen von `Get-HgsTrace` müssen verwendet werden, um zu bestimmen, ob die Ablauf Verfolgungen auf eine fehlerhafte Umgebung hindeuten.

Mithilfe des- `-Diagnostic` Parameters können Sie die Ablauf Verfolgungs Sammlung auf die Ablauf Verfolgungen beschränken, die für den Betrieb der angegebenen Diagnose erforderlich sind.  Dadurch wird die Menge der erfassten Daten sowie die zum Aufrufen der Diagnose erforderlichen Berechtigungen reduziert.

### <a name="diagnosis"></a>Diagnosis

Erfasste Ablauf Verfolgungen können durch Bereitstellen des Speicher Orts der Ablauf Verfolgungen `Get-HgsTrace` über den `-Path` -Parameter und durch Angeben des- `-RunDiagnostics` Schalters diagnostiziert werden.  Darüber hinaus `Get-HgsTrace` kann die Sammlung und Diagnose in einem einzigen Durchlauf durch Bereitstellen des `-RunDiagnostics` -Schalters und einer Liste von Ablauf Verfolgungs Zielen ausführen.  Wenn keine Ablauf Verfolgungs Ziele bereitgestellt werden, wird der aktuelle Computer als implizites Ziel verwendet, dessen Rolle durch die Überprüfung der installierten Windows PowerShell-Module abgeleitet ist.

Die Diagnose führt zu einem hierarchischen Format, das anzeigt, welche Ablauf Verfolgungs Ziele, Diagnose Sätze und die einzelnen Diagnosen für einen bestimmten Fehler verantwortlich sind.  Zu den Fehlern zählen Empfehlungen zur Wiederherstellung und Behebung, wenn eine Entscheidung getroffen werden kann, welche Aktion als nächstes ausgeführt werden soll.  Standardmäßig werden das übergeben und das irrelevante Ergebnis ausgeblendet.  Geben Sie den-Schalter an, um alle von der Diagnose getesteten Elemente anzuzeigen `-Detailed` .  Dies bewirkt, dass alle Ergebnisse unabhängig von Ihrem Status angezeigt werden.

Es ist möglich, den Satz der Diagnose, die mithilfe des-Parameters ausgeführt werden, einzuschränken `-Diagnostic` .  Dadurch können Sie angeben, welche Klassen der Diagnose für die Ablauf Verfolgungs Ziele ausgeführt werden sollen, und alle anderen unterdrücken.  Beispiele für verfügbare Diagnoseklassen sind Netzwerk, bewährte Methoden und Client Hardware.  In der [Cmdlet-Dokumentation](https://technet.microsoft.com/library/mt718831.aspx) finden Sie eine aktuelle Liste der verfügbaren Diagnosen.

> [!WARNING]
> Die Diagnose ist kein Ersatz für eine sichere Pipeline zur Überwachung und Reaktion auf Vorfälle.  Es gibt ein System Center Operations Manager Paket für die Überwachung überwachter Fabrics sowie verschiedene Ereignisprotokoll Kanäle, die überwacht werden können, um Probleme frühzeitig zu erkennen.  Die Diagnose kann dann verwendet werden, um diese Fehler schnell zu selektiert und eine Vorgehensweise festzulegen.

## <a name="targeting-diagnostics"></a>Ziel Diagnose

`Get-HgsTrace`arbeitet mit Ablauf Verfolgungs Zielen.  Ein Ablauf Verfolgungs Ziel ist ein Objekt, das einem HGS-Knoten oder einem überwachten Host in einem geschützten Fabric entspricht.  Dies kann als Erweiterung von einer betrachtet werden, `PSSession` die nur Informationen enthält, die nur von Diagnose-, z. b. der Rolle des Hosts im Fabric, benötigt werden.  Ziele können implizit (z. b. lokale oder manuelle Diagnose) oder explizit mit dem `New-HgsTraceTarget` Befehl generiert werden.

### <a name="local-diagnosis"></a>Lokale Diagnose

Standardmäßig verwendet `Get-HgsTrace` den localhost (d. h., wo das Cmdlet aufgerufen wird).  Dies wird als implizites lokales Ziel bezeichnet.  Das implizite lokale Ziel wird nur verwendet, wenn im-Parameter keine Ziele bereitgestellt werden `-Target` und keine bereits vorhandenen Ablauf Verfolgungen in der gefunden werden `-Path` .

Das implizite lokale Ziel verwendet einen Rollen Rückschluss, um zu bestimmen, welche Rolle der aktuelle Host im geschützten Fabric spielt.  Dies basiert auf den installierten Windows PowerShell-Modulen, die ungefähr den Funktionen entsprechen, die auf dem System installiert wurden.  Das vorhanden sein des `HgsServer` Moduls bewirkt, dass das Ablauf Verfolgungs Ziel die Rolle übernimmt `HostGuardianService` und das vorhanden sein des Moduls dazu führt, dass das Ablauf `HgsClient` Verfolgungs Ziel die Rolle übernimmt `GuardedHost` .  Es ist möglich, dass für einen bestimmten Host beide Module vorhanden sind. in diesem Fall wird er sowohl als als `HostGuardianService` auch als behandelt `GuardedHost` .

Daher ist der Standard Aufruf der Diagnose für die lokale Erfassung von Ablauf Verfolgungen:

```PowerShell
Get-HgsTrace
```

... entspricht Folgendem:

```PowerShell
New-HgsTraceTarget -Local | Get-HgsTrace
```

> [!TIP]
> `Get-HgsTrace`kann Ziele über die Pipeline oder direkt über den- `-Target` Parameter akzeptieren.  Es gibt keinen Unterschied zwischen den beiden operationalen.

### <a name="remote-diagnosis-using-trace-targets"></a>Remote Diagnose mithilfe von Ablauf Verfolgungs Zielen

Es ist möglich, einen Host Remote zu diagnostizieren, indem er Ablauf Verfolgungs Ziele mit Remote Verbindungsinformationen erzeugt.  Alles, was erforderlich ist, ist der Hostname und ein Satz von Anmelde Informationen, die mithilfe von Windows PowerShell-Remoting eine Verbindung herstellen können.
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $server
```
In diesem Beispiel wird eine Aufforderung zum Erfassen der Anmelde Informationen des Remote Benutzers generiert. Anschließend wird die Diagnose mithilfe des Remote Hosts unter ausgeführt, um die Ablauf `hgs-01.secure.contoso.com` Verfolgungs Sammlung abzuschließen.  Die resultierenden Ablauf Verfolgungen werden auf den localhost heruntergeladen und anschließend diagnostiziert.  Die Diagnoseergebnisse werden genauso wie bei der [lokalen Diagnose](#local-diagnosis)angezeigt.  Ebenso ist es nicht notwendig, eine Rolle anzugeben, da Sie auf Grundlage der auf dem Remote System installierten Windows PowerShell-Module abgeleitet werden kann.

Bei der Remote Diagnose werden Windows PowerShell-Remoting für alle Zugriffe auf den Remote Host verwendet.  Daher ist es eine Voraussetzung dafür, dass für das Ablauf Verfolgungs Ziel Windows PowerShell-Remoting aktiviert ist (siehe [Aktivieren von psremoting](https://technet.microsoft.com/library/hh849694.aspx)) und dass der localhost ordnungsgemäß für das Starten von Verbindungen mit dem Ziel konfiguriert ist.

> [!NOTE]
> In den meisten Fällen ist es lediglich erforderlich, dass "localhost" ein Teil derselben Active Directory Gesamtstruktur ist und dass ein gültiger DNS-Hostname verwendet wird.  Wenn Ihre Umgebung ein komplizierteres Verbund Modell verwendet oder Sie direkte IP-Adressen für die Konnektivität verwenden möchten, müssen Sie möglicherweise eine zusätzliche Konfiguration durchführen, z. b. das Festlegen von WinRM- [vertrauenswürdigen Hosts](https://technet.microsoft.com/library/ff700227.aspx).

Mithilfe des Cmdlets können Sie überprüfen, ob ein Ablauf Verfolgungs Ziel ordnungsgemäß instanziiert und für das akzeptieren von Verbindungen konfiguriert ist `Test-HgsTraceTarget` :
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
$server | Test-HgsTraceTarget
```
Dieser Befehl gibt `$True` nur dann zurück, wenn `Get-HgsTrace` eine Remote Diagnose Sitzung mit dem Ablauf Verfolgungs Ziel einrichten könnte.  Bei einem Fehler gibt dieses Cmdlet relevante Statusinformationen zur weiteren Problembehandlung der Windows PowerShell-Remoting-Verbindung zurück.

#### <a name="implicit-credentials"></a>Implizite Anmelde Informationen

Wenn eine Remote Diagnose von einem Benutzer mit ausreichenden Berechtigungen zum Herstellen einer Remote Verbindung mit dem Ablauf Verfolgungs Ziel durchgeführt wird, ist es nicht erforderlich, Anmelde Informationen für bereitzustellen `New-HgsTraceTarget` .  Das `Get-HgsTrace` Cmdlet verwendet automatisch die Anmelde Informationen des Benutzers, der das Cmdlet aufgerufen hat, wenn er eine Verbindung öffnet.

> [!WARNING]
> Einige Einschränkungen gelten für die Wiederverwendung von Anmelde Informationen, insbesondere bei der Durchführung eines "zweiten Hops".  Dies tritt auf, wenn versucht wird, Anmelde Informationen aus einer Remote Sitzung auf einem anderen Computer wiederzuverwenden.  [CredSSP](https://technet.microsoft.com/library/hh849872.aspx) muss zur Unterstützung dieses Szenarios eingerichtet werden, aber dies liegt außerhalb des Umfangs der Verwaltung und Problembehandlung für geschützte Fabrics.

#### <a name="using-windows-powershell-just-enough-administration-jea-and-diagnostics"></a>Verwenden von Windows PowerShell Just Enough Administration (Jea) und Diagnostics

Die Remote Diagnose unterstützt die Verwendung von mit Jea eingeschränkten Windows PowerShell-Endpunkten. Standardmäßig werden Remote Ablauf Verfolgungs Ziele mithilfe des Standard `microsoft.powershell` Endpunkts verbunden.  Wenn das Ziel der Ablauf Verfolgung über die `HostGuardianService` Rolle verfügt, wird auch versucht, den Endpunkt zu verwenden, `microsoft.windows.hgs` der bei der Installation von HGS konfiguriert ist.

Wenn Sie einen benutzerdefinierten Endpunkt verwenden möchten, müssen Sie den Namen der Sitzungs Konfiguration beim Erstellen des Ablauf Verfolgungs Ziels mithilfe des- `-PSSessionConfigurationName` Parameters angeben, z. b. unten:

```PowerShell
New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential) -PSSessionConfigurationName "microsoft.windows.hgs"
```

#### <a name="diagnosing-multiple-hosts"></a>Diagnostizieren mehrerer Hosts

Sie können mehrere Ablauf Verfolgungs Ziele `Get-HgsTrace` gleichzeitig an übergeben.  Dies schließt eine Mischung aus lokalen und Remote Zielen ein.  Jedes Ziel wird ihrerseits verfolgt, und dann werden die Ablauf Verfolgungen von jedem Ziel gleichzeitig diagnostiziert.  Das Diagnosetool kann die erweiterten Kenntnisse der Bereitstellung nutzen, um komplexe Knoten übergreifende Fehlkonfigurationen zu identifizieren, die sonst nicht erkennbar sind.  Die Verwendung dieser Funktion erfordert nur die gleichzeitige Bereitstellung von Ablauf Verfolgungen mehrerer Hosts (im Fall der manuellen Diagnose) oder das Festlegen mehrerer Hosts beim Aufrufen von `Get-HgsTrace` (bei Remote Diagnose).

Im folgenden finden Sie ein Beispiel für die Verwendung der Remote Diagnose zum selektiert eines Fabrics aus zwei HGS-Knoten und zwei überwachten Hosts, bei denen einer der überwachten Hosts zum Starten verwendet wird `Get-HgsTrace` .

```PowerShell
$hgs01 = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Credential (Enter-Credential)
$hgs02 = New-HgsTraceTarget -HostName "hgs-02.secure.contoso.com" -Credential (Enter-Credential)
$gh01 = New-HgsTraceTarget -Local
$gh02 = New-HgsTraceTarget -HostName "guardedhost-02.contoso.com"
Get-HgsTrace -Target $hgs01,$hgs02,$gh01,$gh02 -RunDiagnostics
```

> [!NOTE]
> Bei der Diagnose mehrerer Knoten ist es nicht erforderlich, das gesamte geschützte Fabric zu diagnostizieren.  In vielen Fällen genügt es, alle Knoten einzuschließen, die möglicherweise an einer bestimmten Fehlerbedingung beteiligt sind.  Dabei handelt es sich normalerweise um eine Teilmenge der überwachten Hosts und eine bestimmte Anzahl von Knoten aus dem HGS-Cluster.

## <a name="manual-diagnosis-using-saved-traces"></a>Manuelle Diagnose mit gespeicherten Ablauf Verfolgungen

Manchmal möchten Sie die Diagnose erneut ausführen, ohne die Ablauf Verfolgungen erneut zu erfassen, oder Sie verfügen möglicherweise nicht über die erforderlichen Anmelde Informationen, um alle Hosts in Ihrem Fabric gleichzeitig Remote zu diagnostizieren.  Bei der manuellen Diagnose handelt es sich um einen Mechanismus, mit dem Sie weiterhin mithilfe von eine gesamte fabricroterlung ausführen können `Get-HgsTrace` , ohne eine Remote Ablauf Verfolgungs Sammlung zu verwenden.

Vor der manuellen Diagnose müssen Sie sicherstellen, dass die Administratoren jedes Hosts im Fabric, das als veraltet gilt, bereit sind und bereit sind, Befehle in Ihrem Namen auszuführen.  Bei der Ausgabe der Diagnose Ablauf Verfolgung werden keine Informationen verfügbar gemacht, die im Allgemeinen als vertraulich angesehen werden. Allerdings ist es für den Benutzer von nutzen, um festzustellen, ob diese Informationen sicher für andere Personen verfügbar gemacht werden können

> [!NOTE]
> Ablauf Verfolgungen werden nicht anonymisiert und zeigen Netzwerkkonfiguration, PKI-Einstellungen und andere Konfigurationen, die manchmal als private Informationen angesehen werden.  Daher sollten Ablauf Verfolgungen nur an vertrauenswürdige Entitäten innerhalb einer Organisation übertragen und nie öffentlich veröffentlicht werden.

Die Schritte zum Ausführen einer manuellen Diagnose lauten wie folgt:

1. Fordern Sie die einzelnen Host Administratoren `Get-HgsTrace` an, eine bekannte `-Path` und die Liste der Diagnoseinformationen anzugeben, die Sie für die resultierenden Ablauf Verfolgungen ausführen möchten.  Zum Beispiel:

   ```PowerShell
   Get-HgsTrace -Path C:\Traces -Diagnostic Networking,BestPractices
   ```

2. Fordern Sie an, dass die einzelnen Host Administratoren den resultierenden Ablauf Verfolgungs Ordner Verpacken und an Sie senden.  Dieser Prozess kann über e-Mail, über Dateifreigaben oder einen anderen Mechanismus gesteuert werden, basierend auf den Betriebsrichtlinien und Verfahren, die von Ihrer Organisation festgelegt wurden.

3. Alle empfangenen Ablauf Verfolgungen ohne anderen Inhalt oder Ordner in einem einzelnen Ordner zusammenführen.

    * Nehmen Sie beispielsweise an, dass Ihre Administratoren Ihnen die von den vier Computern erfassten Ablauf Verfolgungen mit den Namen HGS-01, HGS-02, RR1N2608-12 und RR1N2608-13 senden.  Jeder Administrator hätte Ihnen einen Ordner mit demselben Namen gesendet.  Sie würden eine Verzeichnisstruktur zusammenstellen, die wie folgt aussieht:

      ```
      FabricTraces
      |- HGS-01
      |  |- TargetMetadata.xml
      |  |- Metadata.xml
      |  |- [any other trace files for this host]
      |- HGS-02
      |  |- [...]
      |- RR1N2608-12
      |  |- [...]
      |- RR1N2608-13
         |- [..]
      ```

4. Führen Sie die Diagnose aus, und geben Sie den Pfad zum assemblierten Ablauf Verfolgungs Ordner für den `-Path` -Parameter und den- `-RunDiagnostics` Schalter sowie die Diagnose an, für die Sie Ihre Administratoren aufgefordert haben, Ablauf Verfolgungen zu erfassen.  Die Diagnose geht davon aus, dass Sie nicht auf die im Pfad gefundenen Hosts zugreifen kann und versucht daher, nur die vorab erfassten Ablauf Verfolgungen zu verwenden.  Wenn Ablauf Verfolgungen fehlen oder beschädigt sind, tritt bei der Diagnose nur ein Fehler auf, und der Vorgang wird normal fortgesetzt.  Zum Beispiel:

   ```PowerShell
   Get-HgsTrace -RunDiagnostics -Diagnostic Networking,BestPractices -Path ".\FabricTraces"
   ```

### <a name="mixing-saved-traces-with-additional-targets"></a>Mischung gespeicherter Ablauf Verfolgungen mit zusätzlichen Zielen

In einigen Fällen verfügen Sie möglicherweise über eine Reihe von vorab gesammelten Ablauf Verfolgungen, die Sie mit zusätzlichen Host Überwachungen erweitern möchten.  Es ist möglich, vorab erfasste Ablauf Verfolgungen mit zusätzlichen Zielen zu kombinieren, die in einem einzigen Diagnose-und Diagnose Vorgang verfolgt werden.

Befolgen Sie die Anweisungen zum Erfassen und Zusammenstellen eines oben angegebenen Ablauf Verfolgungs Ordners, `Get-HgsTrace` der im vorab erfassten Ablauf Verfolgungs Ordner nicht gefunden wurde:

```PowerShell
$hgs03 = New-HgsTraceTarget -HostName "hgs-03.secure.contoso.com" -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $hgs03 -Path .\FabricTraces
```

Das Diagnose-Cmdlet identifiziert alle vorab gesammelten Hosts und den einen zusätzlichen Host, der weiterhin verfolgt werden muss und die erforderliche Ablauf Verfolgung ausführt.  Die Summe aller vorab gesammelten und frisch gesammelten Ablauf Verfolgungen wird dann diagnostiziert.  Der resultierende Ablauf Verfolgungs Ordner enthält sowohl die alte als auch die neue Ablauf Verfolgung.

## <a name="known-issues"></a>Bekannte Probleme

Bei der Ausführung unter Windows Server 2019 oder Windows 10, Version 1809 und neueren Betriebssystemversionen hat das Modul für geschützte Fabric-Diagnosen bekannte Einschränkungen.
Die Verwendung der folgenden Funktionen kann zu fehlerhaften Ergebnissen führen:

* Host Schlüssel Nachweis
* Nur Nachweis-HGS-Konfiguration (für SQL Server Always Encrypted Szenarien)
* Verwendung von v1-Richtlinien Artefakten auf einem HGS-Server, bei dem der Standardwert der Nachweis Richtlinie "V2" lautet

Ein Fehler bei `Get-HgsTrace` der Verwendung dieser Features ist nicht notwendigerweise ein Hinweis darauf, dass der HGS-Server oder der geschützte Host falsch konfiguriert ist.
Verwenden Sie andere Diagnosetools wie `Get-HgsClientConfiguration` auf einem überwachten Host, um zu testen, ob ein Host den Nachweis überschritten hat.
