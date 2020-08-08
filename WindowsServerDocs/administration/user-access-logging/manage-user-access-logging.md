---
title: Verwalten der Benutzerzugriffsprotokollierung
description: Beschreibt das Verwalten der Benutzer Zugriffs Protokollierung
ms.topic: article
ms.assetid: 4f039017-4152-47eb-838e-bb6ef730b638
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 75f0395afbcbefcdc4ac3a9fc4dc4de3bf962428
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991744"
---
# <a name="manage-user-access-logging"></a>Verwalten der Benutzerzugriffsprotokollierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Dokument wird beschrieben, wie Sie die Benutzerzugriffsprotokollierung verwalten.

Die Benutzerzugriffsprotokollierung ist ein Feature, mit dessen Hilfe Serveradministratoren die Anzahl eindeutiger Clientanforderungen von Rollen und Diensten auf einem lokalen Server messen können.

Die Benutzerzugriffsprotokollierung wird standardmäßig installiert und aktiviert und erfasst Daten nahezu in Echtzeit. Für die Benutzerzugriffsprotokollierung sind nur wenige Konfigurationsoptionen verfügbar. Diese Optionen und ihr Verwendungszweck werden in diesem Dokument beschrieben.

Weitere Informationen zu den Vorteilen der [Benutzer Zugriffs Protokollierung finden Sie unter Einstieg in die Benutzer Zugriffs Protokollierung](get-started-with-user-access-logging.md).

**Inhalt dieses Dokuments**

In diesem Dokument werden folgende Konfigurationsoptionen behandelt:

-   Deaktivieren und Aktivieren des Diensts für die Benutzerzugriffsprotokollierung

-   Sammeln und Entfernen von Daten

-   Löschen der von der Benutzerzugriffsprotokollierung protokollierten Daten

-   Verwalten der Benutzerzugriffsprotokollierung in Umgebungen mit hohem Aufkommen an Clientanforderungen

-   Wiederherstellen nach einer Beschädigung

-   Aktivieren der Nachverfolgung der Arbeitsordner-Nutzungslizenz

## <a name="disabling-and-enabling-the-ual-service"></a><a name="BKMK_Step1"></a>Deaktivieren und Aktivieren des Diensts für die Benutzerzugriffsprotokollierung
Die Benutzer Zugriffs Protokollierung ist standardmäßig aktiviert und wird ausgeführt, wenn ein Computer unter Windows Server 2012 oder höher installiert und zum ersten Mal gestartet wird. Mitunter müssen Administratoren die Benutzerzugriffsprotokollierung deaktivieren, um Datenschutzanforderungen oder andere betriebliche Anforderungen zu erfüllen. Sie können die Benutzer Zugriffs Protokollierung mithilfe der Dienste-Konsole, über die Befehlszeile oder mithilfe von PowerShell-Cmdlets deaktivieren. Um sicherzustellen, dass die Benutzer Zugriffs Protokollierung beim nächsten Start des Computers nicht wieder ausgeführt wird, müssen Sie auch den Dienst deaktivieren. Die folgenden Prozeduren beschreiben, wie Sie die Benutzer Zugriffs Protokollierung deaktivieren und deaktivieren.

> [!NOTE]
> Sie können das PowerShell-Cmdlet `Get-Service UALSVC` verwenden, um Informationen zum Dienst für die Benutzerzugriffsprotokollierung abzurufen, z. B. ob er ausgeführt wird oder beendet wurde und ob er aktiviert oder deaktiviert ist.

#### <a name="to-stop-and-disable-the-ual-service-by-using-the-services-console"></a>So beenden und deaktivieren Sie den Dienst für die Benutzerzugriffsprotokollierung mithilfe der Konsole %%amp;quot;Dienste%%amp;quot;

1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.

2.  Zeigen Sie in Server-Manager auf **Tools**, und klicken Sie anschließend auf **Dienste**.

3.  Führen Sie einen Bildlauf nach unten durch, und wählen Sie **Dienst für die Benutzerzugriffsprotokollierung** aus. Klicken Sie auf **Dienst beenden**.

4.  \-Klicken Sie mit der rechten Maustaste auf den Dienstnamen und wählen Sie **Eigenschaften** Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Deaktiviert**, und klicken Sie dann auf **OK**.

#### <a name="to-stop-and-disable-ual-from-the-command-line"></a>So beenden und deaktivieren Sie die Benutzerzugriffsprotokollierung über die Befehlszeile

1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.

2.  Drücken Sie die WINDOWS-TASTE+R, und geben Sie dann **cmd** ein, um ein Eingabeaufforderungsfenster zu öffnen.

    > [!IMPORTANT]
    > Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

3.  Geben Sie **net stop ualsvc** ein, und drücken Sie dann die EINGABETASTE.

4.  Geben Sie **netsh ualsvc set opmode mode=disable** ein, und drücken Sie dann die EINGABETASTE.

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

Sie können die Benutzerzugriffsprotokollierung auch mit den Windows PowerShell-Befehlen %%amp;quot;Stop-service%%amp;quot; und %%amp;quot;Disable-Ual%%amp;quot; beenden und deaktivieren.

```
Stop-service ualsvc
```

```
Disable-ual
```

Wenn Sie zu einem späteren Zeitpunkt einen Neustart durchführen und die Benutzer Zugriffs Protokollierung erneut aktivieren möchten, können Sie dies mit den folgenden Verfahren tun.

#### <a name="to-start-and-enable-the-ual-service-by-using-the-services-console"></a>So starten und aktivieren Sie den Dienst für die Benutzerzugriffsprotokollierung mithilfe der Konsole %%amp;quot;Dienste%%amp;quot;

1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.

2.  Zeigen Sie in Server-Manager auf **Tools**, und klicken Sie anschließend auf **Dienste**.

3.  Führen Sie einen Bildlauf nach unten durch, und wählen Sie **Dienst für die Benutzerzugriffsprotokollierung** aus. Klicken Sie auf **Dienst starten**.

4.  Klicken Sie mit der rechten Maustaste auf den Namen des Diensts, und wählen Sie **Eigenschaften** aus. Ändern Sie auf der Registerkarte **Allgemein** die Einstellung von **Starttyp** in **Automatisch**, und klicken Sie dann auf **OK**.

#### <a name="to-start-and-enable-ual-from-the-command-line"></a>So starten und aktivieren Sie die Benutzerzugriffsprotokollierung über die Befehlszeile

1.  Melden Sie sich mit den Anmeldeinformationen eines lokalen Administrators am Server an.

2.  Drücken Sie die WINDOWS-TASTE+R, und geben Sie dann **cmd** ein, um ein Eingabeaufforderungsfenster zu öffnen.

    > [!IMPORTANT]
    > Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

3.  Geben Sie **net start ualsvc** ein, und drücken Sie dann die EINGABETASTE.

4.  Geben Sie **netsh ualsvc set opmode mode=enable** ein, und drücken Sie dann die EINGABETASTE.

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

Sie können die Benutzerzugriffsprotokollierung auch mit den Windows PowerShell-Befehlen %%amp;quot;Start-service%%amp;quot; und %%amp;quot;Enable-Ual%%amp;quot; starten und aktivieren.

```
Enable-ual
```

```
Start-service ualsvc
```

## <a name="collecting-ual-data"></a><a name="BKMK_Step2"></a>Sammeln von Daten der Benutzerzugriffsprotokollierung
Zusätzlich zu den im vorherigen Abschnitt beschriebenen PowerShell-Cmdlets können 12 weitere Cmdlets verwendet werden, um die Daten der Benutzer Zugriffs Protokollierung zu erfassen:

-   **Get-UalOverview**: Stellt Details im Zusammenhang mit der Benutzerzugriffsprotokollierung und einen Verlauf der installierten Produkte und Rollen bereit.

-   **Get-UalServerUser**: Stellt Daten zu Clientbenutzerzugriffen für den lokalen Server oder Zielserver bereit.

-   **Get-UalServerDevice**: Stellt Daten zu Clientgerätezugriffen für den lokalen Server oder Zielserver bereit.

-   **Get-UalUserAccess**: Stellt Daten zu Clientbenutzerzugriffen für alle Rollen oder Produkte bereit, die auf dem lokalen Server oder Zielserver installiert sind.

-   **Get-UalDeviceAccess**: Stellt Daten zu Clientgerätezugriffen für alle Rollen oder Produkte bereit, die auf dem lokalen Server oder Zielserver installiert sind.

-   **Get-UalDailyUserAccess**: Stellt Daten zu Clientbenutzerzugriffen für jeden Tag des Jahrs bereit.

-   **Get-UalDailyDeviceAccess**: Stellt Daten zu Clientgerätezugriffen für jeden Tag des Jahrs bereit.

-   **Get-UalDailyAccess**: Stellt Daten zu Clientgerätezugriffen und Clientbenutzerzugriffen für jeden Tag des Jahrs bereit.

-   **Get-UalHyperV**: Stellt für den lokalen Server oder Zielserver relevante Daten zu virtuellen Computern bereit.

-   **Get-UalDns**: Stellt spezifische Daten zum DNS-Client des lokalen DNS-Servers oder DNS-Zielservers bereit.

-   **Get-UalSystemId**: Stellt systemspezifische Daten zur eindeutigen Identifizierung des lokalen Servers oder Zielservers bereit.

`Get-UalSystemId` stellt ein eindeutiges Profil eines Servers bereit, mit dem alle anderen Daten dieses Servers korreliert werden.Wenn ein Serveränderungen in der hat, wird in einem der Parameter eines `Get-UalSystemId` neuen Profils erstellt.  `Get-UalOverview` stellt eine Liste der auf dem Server installierten und verwendeten Rollen für den Administrator bereit.

> [!NOTE]
> Grundlegende Funktionen von Druck-und Dokumentdienste und Datei Diensten werden standardmäßig installiert. Administratoren können daher davon ausgehen, dass für diese Dienste immer Informationen für eine vollständige Installation der Rollen angezeigt werden.Aufgrund der eindeutigen Daten, die die Benutzerzugriffsprotokollierung für Hyper-V und DNS erfasst, sind separate Cmdlets für diese Serverrollen verfügbar.

Ein typisches Verwendungsszenario der Cmdlets für die Benutzerzugriffsprotokollierung ist das Abfragen der eindeutigen Clientzugriffe in einem bestimmten Datumsbereich.Administratoren stehen verschiedene Möglichkeiten zum Ausführen dieser Aufgabe zur Auswahl.Das folgende Codebeispiel zeigt die empfohlene Methode zum Abfragen der eindeutigen Gerätezugriffe in einem Datumsbereich.

```
PS C:\Windows\system32>Gwmi -Namespace "root\AccessLogging" -query "SELECT * FROM MsftUal_DeviceAccess WHERE LastSeen >='1/01/2013' and LastSeen <='3/31/2013'"

```

Dieser Befehl gibt eine ausführliche Liste mit den IP-Adressen aller eindeutigen Clientgeräte zurück, die im jeweiligen Datumsbereich Anforderungen an den Server gesendet haben.

"Activitycount" für jeden eindeutigen Client ist auf 65.535 pro Tag beschränkt.Das Aufrufen der WMI in PowerShell ist nur erforderlich, wenn Sie eine Abfrage anhand eines Datums ausführen.Alle anderen Cmdlet-Parameter für die Benutzerzugriffsprotokollierung können wie im folgenden Beispiel gezeigt in PS-Abfragen verwendet werden:

```
PS C:\Windows\system32> Get-UalDeviceAccess -IPAddress "10.36.206.112"

ActivityCount    : 1
FirstSeen        : 6/23/2012 5:06:50 AM
IPAddress        : 10.36.206.112
LastSeen         : 6/23/2012 5:06:50 AM
ProductName      : Windows Server 2012 Datacenter
RoleGuid         : 10a9226f-50ee-49d8-a393-9a501d47ce04
RoleName         : File Server
TenantIdentifier : 00000000-0000-0000-0000-000000000000
PSComputerName

```

Die Benutzer Zugriffs Protokollierung bewahrt den Verlauf von bis zu zwei Jahren auf. Um den Abruf von Daten der Benutzer Zugriffs Protokollierung durch einen Administrator zu ermöglichen, wenn der Dienst ausgeführt wird, erstellt die Benutzer Zugriffs Protokollierung alle 24 Stunden eine Kopie der aktiven Datenbankdatei (Current *. mdb)* für die Verwendung durch den WMI-Anbieter.

Am ersten Tag des Jahrs erstellt die Benutzerzugriffsprotokollierung eine neue Datei *GUID.mdb*. Die alte *GUID. mdb* wird als Archiv für die Verwendung durch den Anbieter aufbewahrt.  Nach zwei Jahren wird die ursprüngliche Datei *GUID.mdb* überschrieben.

> [!IMPORTANT]
> Die folgenden Verfahren sollten nur von einem erfahrenen Benutzer ausgeführt werden. Sie werden üblicherweise von Entwicklern verwendet, um ihre eigene Instrumentation der Anwendungsprogrammierschnittellen für die Benutzerzugriffsprotokollierung zu testen.

#### <a name="to-adjust-the-default-24-hour-interval-to-make-data-visible-to-the-wmi-provider"></a>So passen Sie das Standardintervall von 24 Stunden an, um Daten für den WMI-Anbieter sichtbar zu machen

1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.

2.  Drücken Sie die WINDOWS-TASTE+R, und geben Sie dann **cmd** ein, um ein Eingabeaufforderungsfenster zu öffnen.

3.  Fügen Sie den folgenden Registrierungswert hinzu:  **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\WMI\AutoLogger\Sum\PollingInterval (REG_DWORD)**.

    > [!WARNING]
    > Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Änderungen an der Registrierung vorgenommen werden, sollten Sie eine Sicherungskopie aller wichtigen Daten auf dem Computer erstellen.

    Das folgende Beispiel zeigt, wie Sie ein Intervall von zwei Minuten hinzufügen (nicht empfohlen als langfristigen Ausführungs Status): **reg Add hklm\system\currentcontrolset\control\wmi \\ autologger\sum/v PollingInterval/t reg \_ DWORD/d 120000/F**

    Die Zeitwerte werden in Millisekunden angegeben. Der Mindestwert ist 60 Sekunden, der Höchstwert ist sieben Tage, und der Standardwert ist 24 Stunden.

4.  Verwenden Sie die Konsole %%amp;quot;Dienste%%amp;quot;, um den Dienst für die Benutzerzugriffsprotokollierung zu beenden und neu zu starten.

## <a name="deleting-data-logged-by-ual"></a>Löschen der von der Benutzerzugriffsprotokollierung protokollierten Daten
Die Benutzerzugriffsprotokollierung ist keine unternehmenskritische Komponente. Sie ist so konzipiert, dass ihre Auswirkungen auf lokale Systemvorgänge so gering wie möglich sind und gleichzeitig eine hohe Zuverlässigkeit gewahrt wird. Dadurch kann der Administrator die DatenbankDatenbank und die unterstützenden Dateien (jede Datei im Verzeichnis "\windows\system32\logfilessum\") auch manuell löschen, um betriebliche Anforderungen zu erfüllen.

#### <a name="to-delete-data-logged-by-ual"></a>So löschen Sie von der Benutzerzugriffsprotokollierung protokollierte Daten

1. Beenden Sie den Dienst für die Benutzerzugriffsprotokollierung.

2. Öffnen Sie Windows-Explorer.

3. Wechseln Sie zu **\windows\system32\logfiles\sum \\ **.

4. Löschen Sie alle Dateien im Ordner.

## <a name="managing-ual-in-high-volume-environments"></a>Verwalten der Benutzerzugriffsprotokollierung in Umgebungen mit hohem Aufkommen an Clientanforderungen
In diesem Abschnitt werden die Besonderheiten erläutert, die bei der Verwendung der Benutzerzugriffsprotokollierung auf einem Server mit vielen Clients zu berücksichtigen sind:

Die Benutzerzugriffsprotokollierung kann maximal 65.535 Zugriffe pro Tag aufzeichnen.Für direkt mit dem Internet verbundene Server (z. B. Webserver, die direkt mit dem Internet verbunden sind) oder Szenarien, in denen eine extrem hohe Leistung die primäre Funktion des Servers ist (z. B. in Umgebungen mit HPC-Arbeitsauslastung), wird die Verwendung der Benutzerzugriffsprotokollierung nicht empfohlen. Die Benutzer Zugriffs Protokollierung ist in erster Linie für Intranetszenarios in kleinen, mittelgroßen und großen Unternehmen gedacht, bei denen ein hohes Volumen erwartet wird, aber nicht so hoch wie viele bereit Stellungen, die regelmäßig Internet Datenverkehr verarbeiten.

Benutzer Zugriffs Protokollierung **im Arbeitsspeicher**: da die Benutzer Zugriffs Protokollierung die Extensible Storage Engine (ESE) verwendet, erhöhen sich die Arbeitsspeicher Anforderungen der Benutzer Zugriffs Protokollierung im Laufe der Zeit (oder nach Anzahl von Client Anforderungen) Der Arbeitsspeicher wird jedoch freigegeben, wenn er vom System benötigt wird, um die Auswirkungen auf die Systemleistung zu minimieren.

Benutzer Zugriffs Protokollierung **auf**Datenträger: die Festplatten Anforderungen der Benutzer Zugriffs Protokollierung lauten ungefähr wie unten dargestellt:

-   0 eindeutige Clientdatensätze: 22 MB

-   50.000 eindeutige Clientdatensätze: 80 MB

-   500.000 eindeutige Clientdatensätze: 384 MB

-   1.000.000 eindeutige Clientdatensätze: 729 MB

## <a name="recovering-from-a-corrupt-state"></a>Wiederherstellen nach einer Beschädigung
In diesem Abschnitt wird erläutert, wie die Extensible Storage Engine (ESE) auf hoher Ebene verwendet wird und was ein Administrator tun kann, wenn Daten der Benutzer Zugriffs Protokollierung beschädigt oder nicht wiederherstellbar sind.

Die Benutzerzugriffsprotokollierung verwendet die ESE, um die Verwendung von Systemressourcen und ihre Beständigkeit gegenüber Beschädigungen zu optimieren.  Weitere Informationen zu den Vorteilen der ESE finden Sie unter [Extensible Storage Engine](/windows/win32/extensible-storage-engine/extensible-storage-engine) auf MSDN.

Bei jedem Start des Diensts für die Benutzerzugriffsprotokollierung führt die ESE eine Wiederherstellung aus. Weitere Informationen finden Sie unter [Extensible Storage Engine-Dateien](/windows/win32/extensible-storage-engine/extensible-storage-engine-files) auf MSDN.

Falls bei der Wiederherstellung ein Problem auftritt, führt die ESE eine Wiederherstellung nach Systemabsturz aus. Weitere Informationen finden Sie unter [JetInit-Funktion](/windows/win32/extensible-storage-engine/jetinit-function) auf MSDN.

Kann die Benutzerzugriffsprotokollierung danach noch immer nicht mit den vorhandenen ESE-Dateien gestartet werden, werden alle Dateien im Verzeichnis %%amp;quot;\Windows\System32\LogFiles\SUM\%%amp;quot; gelöscht. Nachdem diese Dateien gelöscht wurden, wird der Dienst für die Benutzerzugriffsprotokollierung neu gestartet, und es werden neue Dateien erstellt. Der Dienst für die Benutzerzugriffsprotokollierung wird dann wie auf einem neu installierten Computer fortgesetzt.

> [!IMPORTANT]
> Die Dateien im Datenbankverzeichnis der Benutzerzugriffsprotokollierung sollten niemals verschoben oder geändert werden. Andernfalls werden die Wiederherstellungsschritte initiiert (einschließlich der in diesem Abschnitt beschriebenen Bereinigungsroutine). Falls Sicherungen des Verzeichnisses \Windows\System32\LogFiles\SUM\ benötigt werden, müssen alle Dateien im Verzeichnis zusammen gesichert werden, damit die Wiederherstellung wie erwartet funktioniert.

## <a name="enable-work-folders-usage-license-tracking"></a>Aktivieren der Nachverfolgung der Arbeitsordner-Nutzungslizenz
Arbeitsordnerserver können die Benutzerzugriffsprotokollierung für Clientnutzungsberichte verwenden. Im Gegensatz zur Benutzerzugriffsprotokollierung ist die Arbeitsordnerprotokollierung nicht standardmäßig aktiviert. Sie können sie mit der folgenden Registrierungsschlüsseländerung aktivieren:

```
Reg add HKLM\Software\Microsoft\Windows\CurrentVersion\SyncShareSrv /v EnableWorkFoldersUAL /t REG_DWORD /d 1
```

Nach dem Hinzufügen des Registrierungsschlüssels müssen Sie den SyncShareSvc-Dienst auf dem Server neu starten, um die Protokollierung zu aktivieren.

Nachdem die Protokollierung aktiviert ist, werden immer dann, wenn sich ein Client mit dem Server verbindet, zwei Informationsereignisse auf dem Kanal "Windowsprotokolle\Anwendung" protokolliert. Für Arbeitsordner kann jeder Benutzer ein oder mehrere Clientgeräte verwenden, die sich alle 10 Minuten mit dem Server verbinden und prüfen, ob Updates vorhanden sind. Wenn sich 1.000 Benutzer mit jeweils zwei Geräten mit dem Server verbinden, werden die Anwendungsprotokolle alle 70 Minuten überschrieben, was die Problembehandlung bei nicht zusammenhängenden Problemen erschwert. Um dies zu vermeiden, können Sie den Dienst für die Benutzer Zugriffs Protokollierung temporär deaktivieren oder die Größe des Windows-logs\anwendungskanals des Servers erhöhen.

## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch

- [Einstieg in die Benutzer Zugriffs Protokollierung](get-started-with-user-access-logging.md)