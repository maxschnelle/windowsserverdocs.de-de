---
title: Exportieren Sie einen NPS-Serverkonfiguration für den Import auf einem anderen Server
description: In diesem Thema können Sie Informationen zum Exportieren einer Netzwerkrichtlinienserver-Konfiguration in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 141a99e930672d8403315cb6804290d184ef3007
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="export-an-nps-server-configuration-for-import-on-another-server"></a>Exportieren Sie einen NPS-Serverkonfiguration für den Import auf einem anderen Server

Gilt für: Windows Server 2016

Sie können die gesamte NPS-Konfiguration exportieren – einschließlich RADIUS-Clients und Servern, Netzwerkrichtlinien, Verbindungsanforderungsrichtlinie, Registrierung und Konfiguration der Protokollierung – von einem NPS-Server für den Import auf einen anderen NPS-Server. 

Verwenden Sie eines der folgenden Tools, um die NPS-Konfiguration zu exportieren:

- In Windows Server2016, Windows Server2012 R2 und Windows Server2012 mithilfe von Netsh können, oder Sie können mithilfe von Windows PowerShell.
- Verwenden Sie in Windows Server2008 R2 und Windows Server2008 Netsh.

>[!IMPORTANT]
>Verwenden Sie dieses Verfahren nicht, wenn die NPS-Quelldatenbank eine höhere Versionsnummer als die Versionsnummer der NPS-Zieldatenbank hat. Sie können die Versionsnummer der NPS-Datenbank aus der Anzeige des Anzeigen der **Netsh Nps anzeigen Config** Befehl.

Da NPS-Konfigurationen nicht verschlüsselt werden, in der exportierten XML-Datei, und senden sie über ein Netzwerk ein Sicherheitsrisiko darstellen kann daher Vorsichtsmaßnahmen Sie bei die XML-Datei vom Quellserver auf den Zielserver verschieben. Beispielsweise können fügen Sie die Datei auf einer verschlüsselten, kennwortgeschützten Archivdatei vor dem Verschieben der Datei hinzu. Speichern Sie die Datei außerdem an einem sicheren Ort, um zu verhindern, dass böswillige Benutzer darauf zugreifen kann.

>[!NOTE]
>Wenn SQL Server-Protokollierung auf dem NPS-Quellserver konfiguriert ist, werden die Einstellungen für SQL Server-Protokollierung nicht der XML-Datei exportiert. Nachdem Sie die Datei auf einem anderen NPS-Server importieren, müssen Sie SQL Server-Protokollierung manuell konfigurieren.

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Exportieren Sie und importieren Sie die NPS-Konfiguration mithilfe von Windows PowerShell

Für Windows Server2012 und höheren Versionen des Betriebssystems können Sie die NPS-Konfiguration mithilfe von Windows PowerShell exportieren.

Die Befehlssyntax zum Exportieren der NPS-Konfiguration lautet wie folgt. 

    Export-NpsConfiguration -Path <filename>

In der folgende Tabelle sind die Parameter für die **Export-NpsConfiguration** Windows PowerShell-Cmdlets. Parameter fett formatiert sind erforderlich.

|Parameter|Beschreibung|
|---------|-----------|
|Pfad|Gibt den Namen und Speicherort der XML-Datei, die Sie die NPS-Serverkonfiguration zu exportieren möchten.|

**Administrative Anmeldeinformationen**

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="export-example"></a>Export-Beispiel 

Im folgenden Beispiel wird die NPS-Konfiguration in eine XML-Datei auf dem lokalen Laufwerk exportiert. Zum Ausführen dieses Befehls führen Sie Windows PowerShell auf dem NPS-Quellserver als Administrator aus, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE.

`Export-NpsConfiguration –Path c:\config.xml` 

Weitere Informationen finden Sie unter [Export-NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx).

Nachdem Sie die NPS-Konfiguration exportiert haben, kopieren Sie die XML-Datei auf den Zielserver.

Die Befehlssyntax zum Importieren der NPS-Konfigurations auf dem Zielserver lautet wie folgt.

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>Importbeispiel

Der folgende Befehl importiert die Einstellungen aus der Datei mit dem Namen C:\Npsconfig.xml an den NPS. Zum Ausführen dieses Befehls führen Sie Windows PowerShell als Administrator aus, auf dem NPS-Zielserver, geben Sie den folgenden Befehl, und drücken Sie die EINGABETASTE.

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

Weitere Informationen finden Sie unter [Import-NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx).

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Exportieren Sie und importieren Sie die NPS-Konfiguration mithilfe von Netsh

Sie können Network Shell-\(Netsh\) mithilfe die NPS-Serverkonfiguration zu exportieren der **Netsh Nps exportieren** Befehl.

Wenn die **Netsh Nps importieren** Befehl ausgeführt wird, wird NPS mit den aktualisierten Konfigurationseinstellungen automatisch aktualisiert. Sie müssen keine NPS auf dem Zielcomputer auszuführende Beenden der **Netsh Nps importieren** Befehl, jedoch ist der NPS-Konsole oder NPS-MMC-Snap-In öffnen während des Imports Konfiguration, Änderungen an der Serverkonfiguration nicht sichtbar sind, bis Sie die Ansicht zu aktualisieren. 

>[!NOTE]
>Bei Verwendung der **Netsh Nps exportieren** Befehl ist erforderlich, den Command-Parameter bereitstellen **ExportPSK** mit dem Wert **Ja**. Dieser Parameter und Wert Zustand ausdrücklich, dass Sie wissen, dass Sie beim Exportieren der NPS-Serverkonfiguration und die exportierte XML-Datei enthält gemeinsame geheime Schlüssel für RADIUS-Clients und Mitglieder von RADIUS-Remoteservergruppen unverschlüsselt.

**Administrative Anmeldeinformationen**

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-copy-an-nps-server-configuration-to-another-nps-server-using-netsh-commands"></a>Kopieren Sie einen NPS-Serverkonfiguration auf einen anderen NPS-Server mithilfe von Netsh-Befehle

1. Öffnen Sie auf dem NPS-Quellserver **Eingabeaufforderung**, Typ **Netsh**, und drücken Sie dann die EINGABETASTE.

2. Bei der **Netsh** dazu aufgefordert werden, geben Sie **Nps**, und drücken Sie dann die EINGABETASTE. 

3. Bei der **Netsh Nps** dazu aufgefordert werden, geben Sie **Name der Exportdatei =**"*path\file.xml*" **ExportPSK = YES**, wobei *Pfad* ist der Speicherort des Ordners, in der Sie den NPS-Server Konfigurationsdatei speichern möchten, und *Datei* ist der Name der XML-Datei, die Sie speichern möchten. Drücken Sie EINGABETASTE. 

Hiermit werden die Einstellungen für die Konfiguration \(including registry settings\) in eine XML-Datei. Der Pfad kann relativ oder absolut sein, oder es kann es sich um eine \(UNC\) Universal Naming Convention-Pfad. Nachdem Sie die EINGABETASTE, wird eine Meldung angibt, ob der Export in die Datei erfolgreich war.

4. Kopieren Sie die Datei, die Sie erstellt haben, auf den NPS-Zielserver.

5. Geben Sie an einer Eingabeaufforderung auf dem NPS-Zielserver **Netsh Nps import Dateiname =**"*path\file.xml*", und drücken Sie dann die EINGABETASTE. Eine Meldung wird angezeigt, ob der Import aus der XML-Datei erfolgreich war.

Weitere Informationen zu Netsh finden Sie unter [Netzwerkshell (Netsh)](../netsh/netsh.md).

