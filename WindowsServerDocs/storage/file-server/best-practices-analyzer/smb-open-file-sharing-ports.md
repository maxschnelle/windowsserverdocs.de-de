---
Title: 'SMB: Datei- und Druckerfreigabe Ports sollte geöffnet sein.'
TOCTitle: 'SMB: File and printer sharing ports should be open'
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: b6ad1f1f8573fc380e999e5ec2091cea8ebb8aa1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820361"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB: Datei- und Druckerfreigabe Ports sollte geöffnet sein.


Aktualisiert: 2 Februar 2011

Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2 und WindowsServer 2012, Windows Server 2008 R2

*Dieses Thema soll ein spezifisches, durch eine Best Practices Analyzer-Überprüfung ermitteltes Problem behandelt. Sie sollten die Informationen in diesem Thema nur auf Computer anwenden, die der Datei Services Best Practices Analyzer ausführen mussten und stoßen auf das Problem behoben, indem in diesem Thema. Weitere Informationen zu best Practices und Überprüfungen finden Sie unter* [Best Practices Analyzer](http://go.microsoft.com/fwlink/?linkid=122786%0d%0a).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Betriebssystem</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>Produkt /-Funktion</strong></p></td>
<td><p>Dateidienste</p></td>
</tr>
<tr class="odd">
<td><p><strong>Schweregrad</strong></p></td>
<td><p>Fehler</p></td>
</tr>
<tr class="even">
<td><p><strong>Kategorie</strong></p></td>
<td><p>Konfiguration</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>Problem

> *Nicht öffnen der Firewallports werden muss, damit die Datei- und Druckerfreigabe (Ports 445 und 139).*

## <a name="impact"></a>Auswirkungen

> *Computer werden nicht auf freigegebene Ordner und andere Server Message Block SMB-basierten Netzwerkdienste auf diesem Server zugreifen können.*

## <a name="resolution"></a>Auflösung

> *Aktivieren Sie Datei- und Druckerfreigabe, für die Kommunikation durch Firewall des Computers.*

Zum Ausführen dieser Prozedur müssen Sie Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein.

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>Zum Öffnen der Firewallports zum Aktivieren der Datei- und Druckerfreigabe

1.  Öffnen Sie die Systemsteuerung, klicken Sie auf **System und Sicherheit**, und klicken Sie dann auf **Windows-Firewall**.

2.  Klicken Sie im linken Bereich auf **Erweiterte Einstellungen**, und klicken Sie in der Konsolenstruktur auf **Eingangsregeln**.

3.  Klicken Sie unter **Eingangsregeln**, suchen Sie die Regeln **Datei- und Druckerfreigabe (NB-Sitzung eingehend)** und **Datei- und Druckerfreigabe (SMB eingehend)**.

4.  Für jede Regel, mit der rechten Maustaste in der Regelsatzes aus, und klicken Sie dann auf **Regel aktivieren**.

## <a name="additional-references"></a>Weitere Verweise

[Grundlegendes zu freigegebenen Ordnern und die Windows-Firewall](http://technet.microsoft.com/en-us/library/cc731402.aspx)()http://technet.microsoft.com/en-us/library/cc731402.aspx)

