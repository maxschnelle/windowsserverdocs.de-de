---
title: Exportieren einer NPS-Konfiguration für den Import auf einem anderen Server
description: In diesem Thema erfahren Sie, wie Sie eine Netzwerk Richtlinien Server-Konfiguration in Windows Server 2016 exportieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cbebd0388ccd5dd2540a20f5d325d7f97c7e2bb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405436"
---
# <a name="export-an-nps-configuration-for-import-on-another-server"></a>Exportieren einer NPS-Konfiguration für den Import auf einem anderen Server

Gilt für: Windows Server 2016

Sie können die gesamte NPS-Konfiguration – einschließlich RADIUS-Clients und-Server, Netzwerk Richtlinien, Verbindungs Anforderungs Richtlinie, Registrierung und Protokollierungs Konfiguration – von einem NPS für den Import auf einem anderen NPS exportieren. 

Verwenden Sie eines der folgenden Tools, um die NPS-Konfiguration zu exportieren:

- In Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 können Sie Netsh verwenden, oder Sie können Windows PowerShell verwenden.
- Verwenden Sie in Windows Server 2008 R2 und Windows Server 2008 Netsh.

> [!IMPORTANT]
> Verwenden Sie dieses Verfahren nicht, wenn die NPS-Quelldatenbank eine höhere Versionsnummer als die Versionsnummer der Ziel-NPS-Datenbank aufweist. Sie können die Versionsnummer der NPS-Datenbank in der Anzeige des Befehls **netsh nps show config** anzeigen.

Da NPS-Konfigurationen in der exportierten XML-Datei nicht verschlüsselt werden, kann das Senden über ein Netzwerk ein Sicherheitsrisiko darstellen. Achten Sie daher darauf, beim Verschieben der XML-Datei vom Quell Server auf die Zielserver Vorsichtsmaßnahmen zu treffen. Fügen Sie die Datei z. b. einer verschlüsselten, Kenn Wort geschützten Archivdatei hinzu, bevor Sie die Datei verschieben. Speichern Sie die Datei außerdem an einem sicheren Speicherort, um zu verhindern, dass böswillige Benutzer darauf zugreifen.

> [!NOTE]
> Wenn SQL Server Protokollierung für den NPS der Quelle konfiguriert ist, werden SQL Server Protokollierungs Einstellungen nicht in die XML-Datei exportiert. Nachdem Sie die Datei auf einem anderen NPS importiert haben, müssen Sie SQL Server Protokollierung manuell konfigurieren.

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Exportieren und Importieren der NPS-Konfiguration mithilfe von Windows PowerShell

Für Windows Server 2012 und spätere Betriebssystemversionen können Sie die NPS-Konfiguration mithilfe von Windows PowerShell exportieren.

Die Befehlssyntax zum Exportieren der NPS-Konfiguration lautet wie folgt. 

    Export-NpsConfiguration -Path <filename>

In der folgenden Tabelle sind die Parameter für das Cmdlet **Export-npsconfiguration** in Windows PowerShell aufgeführt. Die fett formatierten Parameter sind erforderlich.

|Parameter|Beschreibung|
|---------|-----------|
|Pfad|Gibt den Namen und den Speicherort der XML-Datei an, in die Sie die NPS-Konfiguration exportieren möchten.|

**Administrator Anmelde Informationen**

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="export-example"></a>Beispiel für den Export 

Im folgenden Beispiel wird die NPS-Konfiguration in eine XML-Datei exportiert, die sich auf dem lokalen Laufwerk befindet. Führen Sie zum Ausführen dieses Befehls Windows PowerShell als Administrator auf dem NPS-Quelldatei aus, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

`Export-NpsConfiguration –Path c:\config.xml` 

Weitere Informationen finden Sie unter [Export-npsconfiguration](https://technet.microsoft.com/library/jj872749.aspx).

Nachdem Sie die NPS-Konfiguration exportiert haben, kopieren Sie die XML-Datei auf den Zielserver.

Die Befehlssyntax zum Importieren der NPS-Konfiguration auf dem Zielserver lautet wie folgt.

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>Beispiel importieren

Mit dem folgenden Befehl werden die Einstellungen aus der Datei "c:\npsconfig.xml" in "NPS" importiert. Führen Sie zum Ausführen dieses Befehls Windows PowerShell als Administrator auf dem Ziel-NPS aus, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE.

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

Weitere Informationen finden Sie unter [Import-npsconfiguration](https://technet.microsoft.com/library/jj872750.aspx).

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Exportieren und Importieren der NPS-Konfiguration mithilfe von Netsh

Mithilfe des Netzwerkshell-\(Netsh\) können Sie die NPS-Konfiguration mit dem Befehl **netsh NPS Export** exportieren.

Wenn der Befehl " **netsh NPS Import** " ausgeführt wird, wird NPS automatisch mit den aktualisierten Konfigurationseinstellungen aktualisiert. Es ist nicht erforderlich, NPS auf dem Zielcomputer zu starten, um den Befehl **netsh NPS Import** auszuführen. wenn die NPS-Konsole oder das NPS-MMC-Snap-in während des Konfigurations Imports geöffnet ist, werden die Änderungen an der Serverkonfiguration erst angezeigt, wenn Sie die Ansicht aktualisieren. 

> [!NOTE]
> Wenn Sie den Befehl " **netsh NPS Export** " verwenden, müssen Sie den Befehlsparameter " **exportpsk** " mit dem Wert " **Yes**" angeben. Dieser Parameter und Wert geben explizit an, dass Sie die NPS-Konfiguration exportieren und dass die exportierte XML-Datei unverschlüsselte gemeinsame geheime Schlüssel für RADIUS-Clients und Mitglieder von RADIUS-Remote Server Gruppen enthält.

**Administrator Anmelde Informationen**

Um dieses Verfahren abzuschließen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

### <a name="to-copy-an-nps-configuration-to-another-nps-using-netsh-commands"></a>So kopieren Sie eine NPS-Konfiguration mithilfe von Netsh-Befehlen in ein anderes NPS

1. Öffnen Sie in der NPS-Quelle die **Eingabeaufforderung**, geben Sie **netsh**ein, und drücken Sie dann die EINGABETASTE.

2. Geben Sie an der **netsh** -Eingabeaufforderung **NPS**ein, und drücken Sie dann die EINGABETASTE. 

3. Geben Sie an der **netsh NPS** -Eingabeaufforderung **Export filename =** "*path\file.XML*" **exportpsk = Yes**ein, wobei *path* der Speicherort des Ordners ist, in dem Sie die NPS-Konfigurationsdatei speichern möchten, und *File* der Name der XML-Datei ist, die Sie speichern möchten. Drücken Sie die EINGABETASTE. 

Dies speichert Konfigurationseinstellungen \(einschließlich der in einer XML-Datei\) Registrierungs Einstellungen. Der Pfad kann relativ oder absolut sein, oder es kann sich um einen Universal Naming Convention \(UNC-\) Pfad handeln. Nachdem Sie die EINGABETASTE gedrückt haben, wird eine Meldung angezeigt, die angibt, ob der Export in die Datei erfolgreich war

4. Kopieren Sie die erstellte Datei in das Ziel-NPS.

5. Geben Sie an einer Eingabeaufforderung auf dem Ziel-NPS **netsh NPS Import filename =** "*path\file.XML*" ein, und drücken Sie dann die EINGABETASTE. Es wird eine Meldung angezeigt, die angibt, ob der Import aus der XML-Datei erfolgreich war.

Weitere Informationen zu Netsh finden Sie unter [Network Shell (Netsh)](../netsh/netsh.md).

