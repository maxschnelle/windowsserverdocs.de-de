---
ms.assetid: 2e748187-6a10-4bb0-aed5-34f886a250d2
title: Fsutil
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: a12647908811066293772ab1e9354a0d67874d88
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720047"
---
# <a name="fsutil"></a>Fsutil

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Führt Aufgaben im Zusammenhang mit Datei Zuordnungs Tabellen-und NTFS-Dateisystemen aus, z. b. das Verwalten von Analyse Punkten, das Verwalten von sparsesdateien oder das Aufheben der Bereitstellung eines Volumes. Wenn Sie ohne Parameter verwendet wird, zeigt " **f** " eine Liste der unterstützten Unterbefehle an. 

> [!NOTE] 
> Sie müssen als Administrator oder Mitglied der Gruppe "Administratoren" angemeldet sein, damit Sie fsutil verwenden können. Der Befehl "f" ist sehr leistungsstark und sollte nur von fortgeschrittenen Benutzern verwendet werden, die über umfassende Kenntnisse der Windows-Betriebssysteme verfügen.
>
>Sie müssen das Windows-Subsystem für Linux aktivieren, bevor Sie **fsutil**ausführen können. Führen Sie den folgenden Befehl als Administrator in PowerShell aus, um dieses optionale Feature zu aktivieren:
>
>```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
>```
> Sie werden aufgefordert, den Computer nach der Installation neu zu starten. Nachdem der Computer neu gestartet wurde, können Sie **fsutil** als Administrator ausführen.

### <a name="parameters"></a>Parameter

|Unterbefehl |BESCHREIBUNG|
|---|---|
|["F", "8dot3name"](fsutil-8dot3name.md) | Abfragen oder Ändern der Einstellungen für das Kurznamen Verhalten im System, z. b. Generieren von Dateinamen mit einer Länge von 8,3 Zeichen. Entfernt Kurznamen für alle Dateien in einem Verzeichnis. Scannt ein Verzeichnis und identifiziert Registrierungsschlüssel, die möglicherweise betroffen sind, wenn Kurznamen aus den Dateien im Verzeichnis entfernt wurden.|
|[Verhalten von "f"](fsutil-behavior.md) |Fragt das Volumen Verhalten ab oder legt es fest.|
|[Nicht geändert](fsutil-dirty.md)| Fragt ab, ob das geänderte Bit des Volumes festgelegt ist, oder legt das geänderte Bit eines Volumes fest. Wenn das geänderte Bit eines Volumes festgelegt ist, überprüft **Autochk** automatisch das Volume auf Fehler, wenn der Computer das nächste Mal neu gestartet wird.|
|[Datei "Datei"](fsutil-file.md)|Sucht eine Datei anhand des Benutzernamens (wenn die Datenträger Kontingente aktiviert sind), fragt zugeordnete Bereiche für eine Datei ab, legt den Kurznamen einer Datei fest, legt die gültige Daten Länge einer Datei fest, legt die Daten für eine Datei fest, erstellt eine neue Datei mit einer angegebenen Größe, sucht eine Datei-ID, wenn der Name angegeben wird, oder sucht einen Datei Verknüpfungs Namen für|
|[F-Datei (f)](fsutil-fsinfo.md)|Listet alle Laufwerke auf und fragt den Laufwerkstyp, die Volumeinformationen, die NTFS-spezifischen Volumeinformationen oder die Statistiken des Dateisystems ab.|
|[Mit hardlink "f"](fsutil-hardlink.md)|Listet feste Links für eine Datei auf oder erstellt einen festen Link (einen Verzeichniseintrag für eine Datei). Jede Datei kann als mindestens eine feste Verknüpfung angesehen werden. Auf NTFS-Volumes kann jede Datei über mehrere feste Links verfügen, sodass eine einzelne Datei in vielen Verzeichnissen (oder sogar im gleichen Verzeichnis mit unterschiedlichen Namen) angezeigt werden kann. Da alle Links auf dieselbe Datei verweisen, können Programme alle Links öffnen und die Datei ändern. Eine Datei wird nur dann aus dem Dateisystem gelöscht, nachdem alle Verknüpfungen damit gelöscht wurden. Nachdem Sie einen festen Link erstellt haben, kann er von Programmen wie jeder andere Dateiname verwendet werden.|
|[' F '-ObjectID](fsutil-objectid.md)|Verwaltet Objekt Bezeichner, die vom Windows-Betriebssystem zum Nachverfolgen von Objekten wie Dateien und Verzeichnissen verwendet werden.|
|[Nicht-Kontingent](fsutil-quota.md)|Verwaltet Datenträger Kontingente auf NTFS-Volumes, um eine präzisere Steuerung des netzwerkbasierten Speichers zu ermöglichen. Datenträger Kontingente werden pro Volume implementiert und ermöglichen die Implementierung von Hard-und Soft-Storage-Limits auf Benutzerbasis.|
|[Nicht reparieren](fsutil-repair.md)|Fragt den selbst reparierenden Zustand des Volumes ab oder legt ihn fest. Die Selbstreparatur von NTFS versucht, die Beschädigungen des NTFS-Dateisystems online zu korrigieren, ohne dass " **Chkdsk. exe** " ausgeführt werden muss. Umfasst das Initiieren der Überprüfung auf dem Datenträger und das warten auf den Abschluss der Reparatur|
|["F"-Analyse Punkt](fsutil-reparsepoint.md)|Fragt Analyse Punkte ab oder löscht sie (NTFS-Dateisystem Objekte, die über ein definierbares Attribut verfügen, das benutzergesteuerte Daten enthält). Analyse Punkte werden verwendet, um die Funktionalität des e/a-Subsystems (Input/Output, e/a) zu erweitern. Sie werden für Verzeichnis Verknüpfungs Punkte und volumeeinstellungspunkte verwendet. Sie werden auch von Dateisystem Filter-Treibern verwendet, um bestimmte Dateien als spezielle Dateien für diesen Treiber zu markieren.|
|[Ressource "f"](fsutil-resource.md)|Erstellt eine sekundäre Transaktions Ressourcen-Manager, startet oder beendet eine transaktionale Ressourcen-Manager, zeigt Informationen zu einem transaktionalen Ressourcen-Manager an oder ändert das Verhalten.|
|[Geringe Dichte](fsutil-sparse.md)|Verwaltet Dateien mit geringer Dichte. Eine sparsedatei ist eine Datei mit einer oder mehreren Regionen nicht zugeordneter Daten. Die nicht zugeordneten Regionen werden von einem Programm als Bytes mit dem Wert 0 (null) angezeigt, es wird jedoch kein Speicherplatz zur Darstellung dieser Nullen verwendet. Alle aussagekräftigen Daten oder Daten, die nicht NULL sind, werden zugeordnet, während alle nicht aussagekräftigen Daten (große Daten Zeichenfolgen aus Nullen) nicht zugeordnet werden. Wenn eine sparsedatei gelesen wird, werden zugeordnete Daten als gespeicherte Daten zurückgegeben, und nicht zugeordnete Daten werden als Nullen zurückgegeben (standardmäßig in Übereinstimmung mit der C2-Sicherheits Anforderungsspezifikation). Unterstützung für die Unterstützung von geringer Dichte ermöglicht die Zuordnung von Daten von jedem beliebigen Speicherort in der Datei|
|[Untergeordnetes Tiering](fsutil-tiering.md)|Ermöglicht die Verwaltung von Funktionen für die Speicher Ebene, z. b. das Festlegen und Deaktivieren von Flags und das Auflisten von Ebenen.|
|[Ssutil-Transaktion](fsutil-transaction.md)|Führt einen Commit für eine angegebene Transaktion aus, führt ein Rollback für eine angegebene Transaktion aus oder zeigt Informationen zur Transaktion an.|
|[Nicht zutreffend](fsutil-usn.md)|Verwaltet das Änderungs Journal der Update Sequenznummer (USN), das ein dauerhaftes Protokoll aller an Dateien auf dem Volume vorgenommenen Änderungen bereitstellt.|
|[Volume "Volume"](fsutil-volume.md)|Verwaltet ein Volume. Hebt die Bereitstellung eines Volumes auf, um zu sehen, wie viel freier Speicherplatz auf einem Datenträger verfügbar ist, oder sucht eine Datei, die einen angegebenen Cluster verwendet.|
|[Wim](fsutil-wim.md)|Stellt Funktionen zum Ermitteln und Verwalten von Wim-gestützten Dateien bereit.|

## <a name="see-also"></a>Weitere Informationen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)