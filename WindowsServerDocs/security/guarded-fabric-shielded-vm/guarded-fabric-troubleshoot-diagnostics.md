---
title: Problembehandlung mithilfe der geschützten Fabric-Diagnosetool
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 07691d5b-046c-45ea-8570-a0a85c3f2d22
manager: dongill
author: huu
ms.technology: security-guarded-fabric
ms.openlocfilehash: 0fb257f693cc27c0bc6dd18fc89e8dc6328ee638
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447340"
---
# <a name="troubleshooting-using-the-guarded-fabric-diagnostic-tool"></a>Problembehandlung mithilfe der geschützten Fabric-Diagnosetool

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt die Verwendung des überwachten Fabric Diagnostic Tools zum Bestimmen und Beheben von häufig auftretenden Fehler in der Bereitstellung, Konfiguration und laufenden Betrieb der geschützten Fabric-Infrastruktur. Dies schließt die (Host Guardian Service, HGS), alle überwachten Hosts und unterstützende Dienste wie DNS und Active Directory. Das Diagnosetool kann verwendet werden, ein erster-Schritt bei der Selektierung einer fehlerhaften überwachten Fabric, die Administratoren einen Ausgangspunkt zum Auflösen von Ausfällen, und identifizieren falsch konfigurierte Ressourcen ausführen. Das Tool ist kein Ersatz für einen sound verstehen des Betriebs eines geschützten Fabrics, und nur dazu dient, die am häufigsten auftretenden Probleme, die während der täglichen Vorgänge schnell zu überprüfen.

Dokumentation zu den in diesem Thema verwendeten Cmdlets finden Sie unter [TechNet](https://technet.microsoft.com/library/mt718834.aspx).

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

# <a name="quick-start"></a>Schnellstart

Sie können entweder ein überwachter Host oder einen Host-Überwachungsdienst-Knoten durch Aufrufen von Folgendes von einer Windows PowerShell-Sitzung mit lokalen Administratorrechten diagnostizieren:
```PowerShell
Get-HgsTrace -RunDiagnostics -Detailed
```
Automatisch wird die Rolle des aktuellen Hosts zu erkennen und diagnostizieren alle relevanten Probleme, die nicht automatisch erkannt werden können.  Alle bei diesem Vorgang generierten Ergebnisse werden angezeigt, durch das Vorhandensein der `-Detailed` wechseln.

Im weiteren Verlauf dieses Themas bietet eine ausführliche exemplarische Vorgehensweise für die fortgeschrittene Verwendung der `Get-HgsTrace` für folgende Aufgaben: Diagnostizieren von mehreren Hosts gleichzeitig und komplexe knotenübergreifender Fehlkonfiguration erkannt.

## <a name="diagnostics-overview"></a>Übersicht über die Diagnose
Geschütztes Fabric-Diagnose stehen auf einem Host mit abgeschirmten virtuellen Computer verknüpft, Tools und Features installiert haben, einschließlich Server Core-Hosts.  Derzeit sind die Diagnose mit den folgenden Features/Paketen enthalten:

1. Host-Überwachungsdienst-Dienstrolle
2. Host-Überwachungsunterstützung für Hyper-V
3. VM-Abschirmungstools für Fabric-Verwaltung
4. Remoteserver-Verwaltungstools (RSAT)

Dies bedeutet, dass die Tools für die Diagnose für alle überwachten Hosts, Host-Überwachungsdienst-Knoten, bestimmte Fabric-Management-Server und alle Windows 10-Arbeitsstationen in zur Verfügung stehen [RSAT](https://www.microsoft.com/download/details.aspx?id=45520) installiert.  Diagnosen können von jedem der oben genannten Computer mit der Absicht der Diagnose von Problemen, die überwachten Host bzw. die Host-Überwachungsdienst-Knoten in einem geschützten Fabric aufgerufen werden. verwenden die remote-Trace-Ziele, Diagnose suchen und eine Verbindung herstellen, auf andere Hosts als dem Computer, die Ausführung von Diagnosen.

Jeder Host für die Diagnose wird als ein "Trace-Ziel" bezeichnet  Trace-Ziele werden durch ihre Hostnamen und Rollen identifiziert.  Datenbankrollen beschrieben werden, die Funktion, die ein Ziel für die angegebene Ablaufverfolgung in einem geschützten Fabric ausgeführt wird.  Ablaufverfolgung ist derzeit Support `HostGuardianService` und `GuardedHost` Rollen.  Beachten Sie, dass es für einen Host belegt Sie mehrere Rollen gleichzeitig möglich ist, und dies wird auch von der Diagnose, unterstützt, aber dies sollte nicht in produktionsumgebungen ausgeführt werden.  Die Host-Überwachungsdienst und Hyper-V-Hosts sollten getrennt bleiben und unterschiedliche zu jeder Zeit.

Administratoren können alle Diagnosetasks starten, indem Sie Ausführung `Get-HgsTrace`.  Durch diesen Befehl werden zwei verschiedene Funktionen, die basierend auf den Switches zur Laufzeit bereitgestellt wird: Sammlung und Diagnose zu verfolgen.  Während des gesamten Entwicklungsprozesses des überwachten Fabric Diagnostic Tools machen diese beiden kombiniert.  Obwohl nicht explizit erforderlich ist, erfordern nützlichsten Diagnose ablaufverfolgungen, die nur mit Administratoranmeldeinformationen auf dem Ziel der Ablaufverfolgung erfasst werden können.  Wenn Sie nicht über ausreichende Berechtigungen der Benutzer ausführt, Sammlung von startablaufdaten reserviert sind, schlagen ablaufverfolgungen, die erhöhte Rechte erfordern, während alle anderen übergeben werden.  Dadurch können teilweise Diagnose den Fall, dass ein Operator unterdimensionierte Privileged "Selektierung" ausführt. 

### <a name="trace-collection"></a>Ablaufverfolgungssammlung
In der Standardeinstellung `Get-HgsTrace` wird nur die Ablaufverfolgung erfassen und speichern Sie sie in einen temporären Ordner.  Ablaufverfolgungen werden in der Form von einen Ordner namens nach dem entsprechenden Host gefüllt mit speziell formatierte Dateien, die beschreiben, wie der Host konfiguriert wurde.  Die ablaufverfolgungen enthalten außerdem Metadaten, die beschreiben, wie die Diagnose aufgerufen wurden, um die ablaufverfolgungen zu erfassen.  Diese Daten werden von der Diagnose verwendet, um Informationen über den Host zu aktivieren, wenn manuelle Diagnose ausführen.

Bei Bedarf können ablaufverfolgungen manuell überprüft werden.  Alle Formate sind entweder lesbar (XML) oder kann leicht überprüft werden mithilfe von Standardtools (z. B. X509 Zertifikate und die Windows-Kryptografie-Shell-Erweiterungen).  Beachten Sie jedoch, dass ablaufverfolgungen sind nicht für die manuelle Diagnose ausgelegt, und es immer mehr ist zum Verarbeiten von ablaufverfolgungen mit den Diagnose-Funktionen der effektiven `Get-HgsTrace`.

Die Ergebnisse der Ausführung der Sammlung von startablaufdaten machen sich nicht auf einen Hinweis auf, die Integrität eines bestimmten Hosts aus.  Sie geben einfach an, dass ablaufverfolgungen erfolgreich gesammelt wurden.  Es ist erforderlich, die Funktionen für die Diagnose von verwenden `Get-HgsTrace` zu bestimmen, ob die ablaufverfolgungen fehlerhaften Umgebung anzugeben.

Mithilfe der `-Diagnostic` Parameter, Sie können einschränken, Trace-Auflistung, um nur diese ablaufverfolgungen erforderlich, um die angegebenen Diagnose ausgeführt werden.  Dies reduziert die Menge der Daten sowie die erforderlichen Berechtigungen zum Aufrufen der Diagnose erfasst.

### <a name="diagnosis"></a>Diagnose
Gesammelte ablaufverfolgungen können durch die bereitgestellten diagnostiziert werden `Get-HgsTrace` den Speicherort der ablaufverfolgungen über die `-Path` Parameter und Angeben der `-RunDiagnostics` wechseln.  Darüber hinaus `Get-HgsTrace` Aktualisierungsoption Auflistung und Diagnose in einem einzelnen Durchlauf durch die Bereitstellung der `-RunDiagnostics` wechseln und eine Liste der Ziele der Ablaufverfolgung.  Wenn keine Ziele für die Ablaufverfolgung bereitgestellt werden, der aktuelle Computer als implizite-Ziel, und seine Rolle durch Überprüfen der installierten Windows PowerShell-Module abgeleitet wird.

Diagnose wird Ergebnisse in einem hierarchischen Format angezeigt, der die Ablaufverfolgung-Ziele, die Diagnose legt, und einzelne Diagnose für einen bestimmten Fehler verantwortlich ist.  Fehler bei der enthalten Wiederherstellungsprozess sowie lösungsempfehlungen, wenn eine Identifizierung vorgenommen werden kann, welche Aktion weiter ausgeführt werden soll.  Standardmäßig werden erfolgreiche und irrelevante Ergebnisse ausgeblendet.  Um alles, was getestet werden, von der Diagnose anzuzeigen, geben Sie die `-Detailed` wechseln.  Dadurch werden alle Ergebnisse unabhängig von deren Status angezeigt werden.

Es ist möglich, den Satz von Diagnosedaten zu beschränken, die ausgeführt werden, mithilfe der `-Diagnostic` Parameter.  Dadurch können Sie angeben, welche Klassen der Diagnose für die Ablaufverfolgung ausgerichtet ist, ausgeführt werden soll, und alle anderen unterdrücken.  Beispiele für verfügbare diagnostische Klassen sind, Netzwerk-, best Practices und Client Hardware.  Wenden Sie sich an den [Dokumentation zum Cmdlet](https://technet.microsoft.com/library/mt718831.aspx) finden Sie eine aktuelle Liste der verfügbaren Diagnosen.

> [!WARNING]
> Diagnose ist kein Ersatz für eine starke Überwachung und Reaktion auf Vorfälle-Pipeline.  Ein System Center Operations Manager-Paket steht zur Verfügung, für die Überwachung von geschützten Fabrics sowie verschiedene ereignisprotokollkanäle, die überwacht werden können, um Probleme früh zu erkennen.  Diagnose kann dann verwendet werden, schnell selektieren diese Fehler und Aktion herzustellen.

## <a name="targeting-diagnostics"></a>Für die Zielgruppenadressierung Diagnose

`Get-HgsTrace` funktioniert für Trace-Ziele.  Ein Ziel für die Ablaufverfolgung handelt es sich um ein Objekt, das eine Host-Überwachungsdienst-Knoten oder einem bewachten Host innerhalb eines geschützten Fabrics entspricht.  Es kann als Erweiterung betrachtet werden eine `PSSession` darunter Angaben, die nur von z. B. die Rolle des Hosts im Fabric-Diagnose erforderlich sind.  Ziele können werden generiert implizit (z. B. lokale oder manuelle Diagnose) oder explizit mit der `New-HgsTraceTarget` Befehl.

### <a name="local-diagnosis"></a>Lokale Diagnose

In der Standardeinstellung `Get-HgsTrace` zielt die "localhost" (d. h., in dem das-Cmdlet aufgerufen wird).  Dies wird als implizite lokale Ziel bezeichnet.  Die implizite lokale Ziel wird nur verwendet, wenn keine Ziele, in bereitgestellt werden der `-Target` Parameter und keine bereits vorhandenen ablaufverfolgungen befinden sich die `-Path`.

Die implizite lokale Ziel verwendet Rolle Typrückschluss, um zu bestimmen, welche Rolle der aktuelle Host in der geschützten Fabric spielt.  Dies basiert auf der installierten Windows PowerShell-Module die entsprechen etwa welche Funktionen auf dem System installiert wurden.  Das Vorhandensein der `HgsServer` Modul führt dazu, dass das Ziel der Ablaufverfolgung, die Rolle `HostGuardianService` und das Vorhandensein der `HgsClient` Modul führt dazu, dass das Ziel der Ablaufverfolgung, die Rolle `GuardedHost`.  Es ist möglich, für einen bestimmten Host, damit beide Module in diesem Fall vorhanden, wird es als behandelt, eine `HostGuardianService` und `GuardedHost`.

Aus diesem Grund führt eine Ablaufverfolgung für der Standard-Aufruf der Diagnose zum Sammeln von lokal:
```PowerShell
Get-HgsTrace
```
... ist äquivalent zu folgendem:
```PowerShell
New-HgsTraceTarget -Local | Get-HgsTrace
```
> [!TIP]
> `Get-HgsTrace` lässt die Ziele, die über die Pipeline oder direkt über die `-Target` Parameter.  Es gibt keinen Unterschied zwischen den beiden während des Betriebs.

### <a name="remote-diagnosis-using-trace-targets"></a>Remote-Diagnose mithilfe von Trace-Ziele

Es ist möglich, einen Host eine Remotediagnose für Trace-Ziele mit remoteverbindungsinformationen generieren.  Erforderlich ist lediglich den Hostnamen und einen Satz von Anmeldeinformationen eine Verbindung herstellen über Windows PowerShell-Remoting kann.
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $server
```
In diesem Beispiel wird eine Aufforderung zum Sammeln der Anmeldeinformationen des Remotebenutzers generiert, und klicken Sie dann Diagnose führt mit dem Remotehost an `hgs-01.secure.contoso.com` Ablaufverfolgungssammlung abgeschlossen.  Die resultierenden ablaufverfolgungen sind in den "localhost" heruntergeladen und dann untersucht.  Die Ergebnisse der Diagnose identisch angezeigt werden, bei [lokale Diagnose](#local-diagnosis).  Auf ähnliche Weise ist es nicht erforderlich, eine Rolle an, wie sie basierend auf der Windows PowerShell-Module, die auf dem Remotesystem installiert abgeleitet werden kann.

Remote-Diagnose verwendet Windows PowerShell-Remoting für alle Zugriffe auf den Remotehost.  Daher ist es eine Voraussetzung, dass das Ziel für die Ablaufverfolgung mit Windows PowerShell-Remoting aktiviert haben (finden Sie unter [aktivieren PSRemoting](https://technet.microsoft.com/library/hh849694.aspx)) und dass die "localhost" ordnungsgemäß konfiguriert werden, für den Start von Verbindungen mit dem Ziel.

> [!NOTE]
> In den meisten Fällen ist es nur erforderlich, dass die "localhost" Teil derselben Active Directory-Gesamtstruktur sein und ein gültiger DNS-Hostnamen verwendet wird.  Wenn Ihre Umgebung einen etwas komplizierteren Verbundmodell nutzt oder direkte IP-Adressen für Verbindungen verwenden möchten, müssen Sie möglicherweise zusätzliche Konfigurationsschritte wie das Festlegen der WinRM ausführen [vertrauenswürdige Hosts](https://technet.microsoft.com/library/ff700227.aspx).

Sie können überprüfen, ob ein Ziel für die Ablaufverfolgung ordnungsgemäße Instanziierung und Konfiguration für das Akzeptieren von Verbindungen mit dem `Test-HgsTraceTarget` Cmdlet:
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
$server | Test-HgsTraceTarget
```
Dieser Befehl gibt `$True` nur, wenn `Get-HgsTrace` wäre eine Diagnose Remotesitzung mit dem Trace-Ziel herstellen.  Bei einem Fehler gibt dieses Cmdlet aus, relevante Informationen für die weitere Problembehandlung für die Windows PowerShell-Remoting-Verbindung zurück.

#### <a name="implicit-credentials"></a>Implizite Anmeldeinformationen

Wenn remote-Diagnose von einem Benutzer mit ausreichenden Berechtigungen Herstellen einer Remoteverbindung mit dem Ziel für die Ablaufverfolgung durchführen zu können, ist es nicht erforderlich, geben Sie Anmeldeinformationen für `New-HgsTraceTarget`.  Die `Get-HgsTrace` Cmdlet verwendet die Anmeldeinformationen des Benutzers, der das-Cmdlet beim Öffnen einer Verbindung aufgerufen automatisch erneut.

> [!WARNING]
> Es gelten einige Einschränkungen, die Anmeldeinformationen wiederverwenden, besonders beim Ausführen von sogenannten "zweiten Hop".  Dies tritt auf, bei dem Versuch der Wiederverwendung von Anmeldeinformationen innerhalb einer Remotesitzung mit einem anderen Computer.  Es ist notwendig, [einrichten CredSSP](https://technet.microsoft.com/library/hh849872.aspx) unterstützen dieses Szenario, aber dies ist nicht im Rahmen eines geschützten Fabrics, Verwaltung und Problembehandlung.

#### <a name="using-windows-powershell-just-enough-administration-jea-and-diagnostics"></a>Mithilfe von Windows PowerShell, Just Enough Administration (JEA) und Diagnose

Remote-Diagnose unterstützt die Verwendung von Windows PowerShell eingeschränkten JEA-Endpunkten. Remote-Ablaufverfolgung Ziele werden verbinden sich standardmäßig unter Verwendung der `microsoft.powershell` Endpunkt.  Wenn das Trace-Ziel verfügt die `HostGuardianService` -Rolle wird auch versucht, verwenden Sie die `microsoft.windows.hgs` -Endpunkt konfiguriert ist, bei der Installation von Host-Überwachungsdienst.

Wenn Sie einen benutzerdefinierten Endpunkt verwenden möchten, müssen Sie den Namen der Sitzung angeben, beim Erstellen der Ablaufverfolgung Ziel mithilfe der `-PSSessionConfigurationName` Parameter, wie unten:

```PowerShell
New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential) -PSSessionConfigurationName "microsoft.windows.hgs"
```

#### <a name="diagnosing-multiple-hosts"></a>Diagnostizieren von mehreren Hosts

Sie können mehrere Ablaufverfolgungs-Ziele zu übergeben, `Get-HgsTrace` auf einmal.  Dies schließt eine Mischung aus lokalen und remote-Ziele.  Jedes Ziel in der Ablaufverfolgung erfasst wiederum und klicken Sie dann ablaufverfolgungen aus jedem Ziel werden untersucht werden gleichzeitig.  Das Diagnosetool können die erhöhte Kenntnis Ihrer Bereitstellung komplexere knotenübergreifender Fehlkonfigurationen identifizieren, die ansonsten nicht erkennbare wäre.  Verwenden Sie diese Funktion erfordert für mehrere, beim Aufrufen von Hosts ablaufverfolgungen über mehrere Hosts gleichzeitig (bei manueller Diagnose) oder durch Bereitstellung nur `Get-HgsTrace` (im Fall von remote-Diagnose).

Es folgt ein Beispiel der Verwendung von remote-Diagnose "Selektierung" eine Fabric besteht aus zwei Host-Überwachungsdienst-Knoten und zwei überwachten Hosts, in denen wird einer der überwachten Hosts verwendet, um starten `Get-HgsTrace`.

```PowerShell
$hgs01 = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Credential (Enter-Credential)
$hgs02 = New-HgsTraceTarget -HostName "hgs-02.secure.contoso.com" -Credential (Enter-Credential)
$gh01 = New-HgsTraceTarget -Local
$gh02 = New-HgsTraceTarget -HostName "guardedhost-02.contoso.com"
Get-HgsTrace -Target $hgs01,$hgs02,$gh01,$gh02 -RunDiagnostics
```

> [!NOTE]
> Sie müssen sich nicht um Ihre gesamte geschütztes Fabric zu diagnostizieren, wenn mehrere Knoten zu diagnostizieren.  In vielen Fällen ist es ausreichend, um alle Knoten beteiligt sein können, die in eine bestimmte fehlerbedingung einschließen.  Dies ist in der Regel eine Teilmenge von überwachten Hosts und eine Anzahl von Knoten aus dem Host-Überwachungsdienst-Cluster.

## <a name="manual-diagnosis-using-saved-traces"></a>Manuelle Diagnose unter Verwendung des gespeicherten Ablaufverfolgungen

Manchmal sollten Sie Diagnose erneut ausführen, ohne das Sammeln von ablaufverfolgungen erneut, oder Sie haben nicht die erforderlichen Anmeldeinformationen auf allen Hosts im Fabric gleichzeitig eine Remotediagnose für.  Manuelle Diagnose ist ein Mechanismus, mit dem Sie immer noch mit ausführen können eine ganze-Fabric "Selektierung" `Get-HgsTrace`, aber ohne Verwendung der remote-Ablaufverfolgungssammlung.

Bevor Sie die manuelle Diagnose durchführen, müssen Sie sicherstellen, dass die Administratoren der einzelnen Hosts im Fabric, das selektiert werden wird und zum Ausführen von Befehlen in Ihrem Namen sind.  Diagnoseablaufverfolgung Ausgabe macht keine Informationen, die als vertraulich, in der Regel angezeigt wird verfügbar, aber es dem Benutzer obliegt zu bestimmen, ob diese Informationen an andere Personen verfügbar gemacht werden kann.

> [!NOTE]
> Ablaufverfolgungen werden nicht anonymisiert und Anzeigen der Konfiguration des Netzwerks, PKI-Einstellungen und anderen Konfigurationen, die manchmal auch als privaten Informationen gelten.  Ablaufverfolgungen muss daher nur an vertrauenswürdige Entitäten innerhalb einer Organisation übertragen, und niemals öffentlich gepostet.

Schritte zum Ausführen einer manuellen Diagnose sind wie folgt aus:

1. Anforderung, die jeder hostadministrator ausgeführt `Get-HgsTrace` Angabe einen bekannten `-Path` und die Liste der Diagnose für die resultierenden ablaufverfolgungen ausgeführt werden sollen.  Zum Beispiel:

   ```PowerShell
   Get-HgsTrace -Path C:\Traces -Diagnostic Networking,BestPractices
   ```
2. Fordern Sie an, dass jeder hostadministrator Paket resultierende Traces des Ordners und an Sie senden.  Dieser Prozess kann per E-mail, über Dateifreigaben, oder eine andere Methode, die basierend auf den Betrieb personalsicherheitsrichtlinien und-Verfahren von Ihrer Organisation gesteuert werden.

3. Alle empfangene ablaufverfolgungen in einem einzigen Ordner, ohne andere Inhalte oder Ordner zusammenführen.

    * Nehmen wir beispielsweise an Sie Ihre Administratoren senden, die Sie ablaufverfolgungen von vier Computer, die mit dem Namen erfasst hatten HGS-01, Host-Überwachungsdienst-02, RR1N2608-12 und RR1N2608-13.  Jeder Administrator würden Sie einen Ordner mit demselben Namen gesendet haben.  Sie würden eine Verzeichnisstruktur zusammen, die wie folgt aussieht:

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

4. Führen Sie die Diagnose, die den Pfad zu dem ablaufverfolgungsordner assemblierten zur Bereitstellung der `-Path` Parameter und Angeben der `-RunDiagnostics` sowie die Diagnose, der Sie, Ihre Administratoren zum Sammeln von ablaufverfolgungen aufgefordert, zu wechseln.  Diagnose geht davon aus, es kann nicht zugegriffen werden die Hosts innerhalb des Pfads gefunden und aus diesem Grund versucht, die nur die bereits gesammelten ablaufverfolgungen zu verwenden.  Wenn keine ablaufverfolgungen vorhanden oder beschädigt sind, wird die Diagnose nur die betroffenen Tests fehlschlagen und normal fortgesetzt.  Zum Beispiel:

   ```PowerShell
   Get-HgsTrace -RunDiagnostics -Diagnostic Networking,BestPractices -Path ".\FabricTraces"
   ```

### <a name="mixing-saved-traces-with-additional-targets"></a>Das Kombinieren von Ablaufverfolgungen durch zusätzliche Ziele gespeichert

In einigen Fällen müssen Sie eine Reihe von vorab gesammelte ablaufverfolgungen möglicherweise, die Sie zusammen mit zusätzlichen Host ablaufverfolgungen erweitern möchten.  Es ist möglich, die bereits gesammelte ablaufverfolgungen mit zusätzliche Ziele zu kombinieren, die eine Ablaufverfolgung ausgeführt und in einem einzigen Aufruf der Diagnose diagnostiziert werden.

Rufen Sie den Anweisungen zum Erfassen und Zusammenstellen von einem Trace-Ordner, der oben angegebenen, `Get-HgsTrace` zusätzliche Trace-Ziele, die im Ordner "vorab erfassten Ablaufverfolgung" nicht gefunden:

```PowerShell
$hgs03 = New-HgsTraceTarget -HostName "hgs-03.secure.contoso.com" -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $hgs03 -Path .\FabricTraces
``` 

Die Diagnose-Cmdlet erkennt alle vorab erfassten-Hosts, und die eine zusätzliche, die noch um eine Ablaufverfolgung ausgeführt werden muss und führt die Ablaufverfolgung erforderliche.  Die Summe von alle bereits gesammelten und neu erfasst ablaufverfolgungen wird dann diagnostiziert werden.  Der endgültige Ordnername für die Ablaufverfolgung wird die alten und neuen ablaufverfolgungen enthalten.
