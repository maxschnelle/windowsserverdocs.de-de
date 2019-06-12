---
title: Exportieren Sie eine NPS-Konfiguration für den Import auf einem anderen Server
description: Sie können in diesem Thema verwenden, erfahren, wie eine Konfiguration des Netzwerkrichtlinienservers unter Windows Server 2016 zu exportieren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b95e39af63e284d0147335faabfb740c0dd175bc
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812300"
---
# <a name="export-an-nps-configuration-for-import-on-another-server"></a>Exportieren Sie eine NPS-Konfiguration für den Import auf einem anderen Server

Gilt für: Windows Server 2016

Sie können die gesamte NPS-Konfiguration exportieren – einschließlich der RADIUS-Clients und Servern, Netzwerkrichtlinie, Verbindungsanforderungsrichtlinie, Registrierung und Konfiguration der Protokollierung – von einem NPS für den Import auf einer anderen NPS. 

Verwenden Sie eine der folgenden Tools, um die NPS-Konfiguration zu exportieren:

- In Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 können Sie Netsh, oder Sie können Windows PowerShell verwenden.
- In Windows Server 2008 R2 und Windows Server 2008 können mithilfe von Netsh.

> [!IMPORTANT]
> Verwenden Sie dieses Verfahren nicht, wenn die NPS-Quelldatenbank eine höhere Versionsnummer als die Versionsnummer der Zieldatenbank NPS hat. Sehen Sie die Versionsnummer der Datenbank aus der Anzeige des NPS die **Netsh Nps anzeigen Config** Befehl.

Da die NPS-Konfigurationen nicht verschlüsselt sind, in der exportierten XML-Datei, und senden, dass sie über ein Netzwerk ein Sicherheitsrisiko darstellen könnte also Vorsichtsmaßnahmen Sie beim Verschieben von XML-Datei vom Quellserver auf dem Zielserver. Beispielsweise können fügen Sie die Datei auf einer verschlüsselten, kennwortgeschützten Archivdatei vor dem Verschieben der Datei hinzu. Speichern Sie außerdem die Datei an einem sicheren Ort, um zu verhindern, dass böswillige Benutzer darauf zugreifen.

> [!NOTE]
> Wenn SQL Server-Protokollierung auf dem Quellcomputer NPS konfiguriert ist, werden die Einstellungen für SQL Server-Protokollierung nicht der XML-Datei exportiert. Nachdem Sie die Datei auf einer anderen NPS importiert haben, müssen Sie SQL Server-Protokollierung manuell konfigurieren.

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Exportieren Sie und importieren Sie die NPS-Konfiguration mithilfe von Windows PowerShell

Für Windows Server 2012 und höheren Betriebssystemversionen können Sie die NPS-Konfiguration mithilfe von Windows PowerShell exportieren.

Die Befehlssyntax zum Exportieren der NPS-Konfiguration lautet wie folgt. 

    Export-NpsConfiguration -Path <filename>

Die folgende Tabelle enthält die Parameter für die **Export-NpsConfiguration** Windows PowerShell-Cmdlet. Parameter in Fettschrift angezeigt, die erforderlich sind.

|Parameter|Beschreibung|
|---------|-----------|
|Pfad|Gibt den Namen und Speicherort der XML-Datei zu der Sie die NPS-Konfiguration exportieren möchten.|

**Administratoranmeldeinformationen**

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="export-example"></a>Beispiel zum Exportieren 

Im folgenden Beispiel wird die NPS-Konfiguration in eine XML-Datei befindet sich auf dem lokalen Laufwerk exportiert. Zum Ausführen dieses Befehls, führen Sie Windows PowerShell als Administrator aus, auf dem Quellcomputer NPS, geben Sie den folgenden Befehl aus, und drücken Sie EINGABETASTE.

`Export-NpsConfiguration –Path c:\config.xml` 

Weitere Informationen finden Sie unter [Export-NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx).

Nachdem Sie die NPS-Konfiguration exportiert haben, kopieren Sie die XML-Datei auf den Zielserver.

Die Befehlssyntax zum Importieren der NPS-Konfiguration auf dem Zielserver ist wie folgt aus.

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>Importbeispiel

Der folgende Befehl importiert die Einstellungen aus der Datei mit dem Namen C:\Npsconfig.xml an NPS. Zum Ausführen dieses Befehls, führen Sie Windows PowerShell als Administrator aus, auf dem NPS-Zielserver, geben Sie den folgenden Befehl aus, und drücken Sie die EINGABETASTE.

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

Weitere Informationen finden Sie unter [Import-NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx).

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Exportieren Sie und importieren Sie die NPS-Konfiguration mithilfe von Netsh

Können Sie Netzwerkshell \(Netsh\) So exportieren Sie die NPS-Konfiguration mithilfe der **Netsh Nps export** Befehl.

Wenn die **Netsh Nps import** ausgeführt wird, NPS wird automatisch mit den aktualisierten Konfigurationseinstellungen aktualisiert. Sie müssen nicht zum Beenden von NPS auf dem Zielcomputer zum Ausführen der **Netsh Nps import** Befehl jedoch, wenn die NPS-Konsole oder NPS-MMC-Snap-in während des Imports Konfiguration geöffnet ist, Änderungen an der Serverkonfiguration nicht erst sichtbar sind Sie können die Ansicht aktualisieren. 

> [!NOTE]
> Bei Verwendung der **Netsh Nps export** Befehls müssen Sie die Befehlsparameter bieten **ExportPSK** mit dem Wert **Ja**. Dieser Parameter und Wert Zustand explizit, dass Sie wissen, dass Sie die NPS-Konfiguration exportieren und die exportierte XML-Datei enthält nicht gemeinsame geheime Schlüssel für RADIUS-Clients und Mitglieder von RADIUS-Remoteservergruppen verschlüsselte.

**Administratoranmeldeinformationen**

Um dieses Verfahren ausführen zu können, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-copy-an-nps-configuration-to-another-nps-using-netsh-commands"></a>Kopieren Sie eine NPS-Konfiguration an einer anderen NPS mithilfe von Netsh-Befehle

1. Öffnen Sie auf der Quelle NPS **Eingabeaufforderung**, Typ **Netsh**, und drücken Sie dann die EINGABETASTE.

2. Auf der **Netsh** dazu aufgefordert werden, geben Sie **Nps**, und drücken Sie dann die EINGABETASTE. 

3. Auf der **Netsh Nps** dazu aufgefordert werden, geben Sie **exportieren Filename =** "*path\file.xml*" **ExportPSK = YES**, wobei *Pfad* ist der Speicherort des Ordners, in dem die NPS-XML-Konfigurationsdatei gespeichert werden soll, und *Datei* ist der Name der XML-Datei, die Sie speichern möchten. Drücken Sie die EINGABETASTE. 

Speichert Konfigurationseinstellungen \(einschließlich registrierungseinstellungen\) in eine XML-Datei. Der Pfad kann relativ oder absolut sein, oder es kann ein Universal Naming Convention \(UNC\) Pfad. Nachdem Sie die EINGABETASTE drücken, wird eine Meldung, der angibt,, ob der Export in Datei erfolgreich war.

4. Kopieren Sie die Datei, die Sie erstellt haben, an das Ziel NPS.

5. Geben Sie an einer Eingabeaufforderung auf dem NPS-Zielserver **Netsh Nps import Dateiname =** "*path\file.xml*", und drücken Sie dann die EINGABETASTE. Es erscheint eine Meldung angibt, ob der Import aus der XML-Datei erfolgreich war.

Weitere Informationen zu Netsh finden Sie unter [Netzwerkshell (Netsh)](../netsh/netsh.md).

