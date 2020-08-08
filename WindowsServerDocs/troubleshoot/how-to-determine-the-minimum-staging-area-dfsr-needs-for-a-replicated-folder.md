---
title: Ermitteln der Mindestanforderungen an den DFSR-Stagingbereich für einen replizierten Ordner
description: Dieser Artikel ist eine Kurzanleitung zum Berechnen des minimalen Stagingbereichs, der für die ordnungsgemäße Funktionsweise von DFSR benötigt wird.
ms.date: 06/10/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 581b485f219e960ecd467baa1f7dff7742c3acf8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965787"
---
# <a name="how-to-determine-the-minimum-staging-area-dfsr-needs-for-a-replicated-folder"></a>Ermitteln der Mindestanforderungen an den DFSR-Stagingbereich für einen replizierten Ordner

Dieser Artikel ist eine Kurzanleitung zum Berechnen des minimalen Stagingbereichs, der für die ordnungsgemäße Funktionsweise von DFSR benötigt wird. Werte, die niedriger als solche sind, können dazu führen, dass die Replikation langsam ist

Beachten Sie, dass es sich hierbei *nur um Mindestgebühren*handelt. Wenn Sie die Größe des Stagingbereichs berücksichtigen, desto größer ist der Stagingbereich, bis zur Größe des replizierten Ordners. Weitere Informationen dazu, warum es wichtig ist, einen Stagingbereich mit ordnungsgemäßer Skalierungs Umfang zu haben, finden Sie im Abschnitt "bestimmen, ob Probleme mit dem Stagingbereich vorliegen" und in den Blogbeiträgen, die am Ende dieses Artikels verknüpft sind.

> [!Note]
> Außerdem verfügen wir über einen Hotfix, der Sie bei der Berechnung der staginggrößen unterstützt. [Das Update für die DFS-Replikation-Verwaltungsschnittstelle (DFSR) ist verfügbar.](https://support.microsoft.com/kb/2607047)

## <a name="rules-of-thumb"></a>Faustregeln

**Windows Server 2003 R2** – das Kontingent für den Stagingbereich muss so groß wie die neun größten Dateien im replizierten Ordner sein.

**Windows Server 2008 und 2008 R2** – das Kontingent für den Stagingbereich muss so groß sein wie die größten 32 Dateien im replizierten Ordner.

Durch die erste Replikation wird der Stagingbereich wesentlich stärker genutzt als die tägliche Replikation. Das Festlegen des Stagingbereichs über den minimalen Wert während der ersten Replikation wird dringend empfohlen, wenn der Laufwerks Speicherplatz verfügbar ist.

## <a name="where-do-i-get-powershell"></a>Wo erhalte ich PowerShell?

PowerShell ist unter Windows 2008 und höher enthalten. Sie müssen PowerShell unter Windows Server 2003 installieren. Sie können PowerShell für Windows 2003 [hier](https://support.microsoft.com/kb/968930)herunterladen.

## <a name="how-do-you-find-these-x-largest-files"></a>Wie finden Sie diese X größten Dateien?

Verwenden Sie ein PowerShell-Skript, um die größten Dateien (32 oder 9) zu suchen und zu bestimmen, wie viele Gigabyte Sie addieren (aufgrund von Ned Pyle für die PowerShell-Befehle). Ich werde Ihnen tatsächlich drei PowerShell-Skripts vorstellen. Jede ist selbst nützlich. Allerdings ist Number 3 die nützlichste.

1. Führen Sie den folgenden Befehl aus:
   ```Powershell
   Get-ChildItem c:\\temp -recurse | Sort-Object length -descending | select-object -first 32 | ft name,length -wrap –auto
   ```

   Mit diesem Befehl werden die Dateinamen und die Größe der Dateien in Bytes zurückgegeben. Nützlich, wenn Sie wissen möchten, welche 32-Dateien im replizierten Ordner am größten sind, damit Sie Ihre Besitzer "besuchen" können.

2. Führen Sie den folgenden Befehl aus:
   ```Poswershell
   Get-ChildItem c:\\temp -recurse | Sort-Object length -descending | select-object -first 32 | measure-object -property length –sum
   ```
   Mit diesem Befehl wird die Gesamtzahl der Bytes der 32 größten Dateien im Ordner zurückgegeben, ohne dass die Dateinamen aufgelistet werden.

3. Führen Sie den folgenden Befehl aus:
   ```Poswershell
   $big32 = Get-ChildItem c:\\temp -recurse | Sort-Object length -descending | select-object -first 32 | measure-object -property length –sum

   $big32.sum /1gb
   ```
   Mit diesem Befehl wird die Gesamtzahl der Bytes von 32 größten Dateien im Ordner angezeigt, und Sie können die Berechnungen durchführen, um Bytes für Sie in Gigabyte zu konvertieren. Dieser Befehl ist zwei separate Zeilen. Sie können beide Elemente gleichzeitig in die PowerShell-Befehlsshell einfügen oder Sie wieder zurückführen.

## <a name="manual-walkthrough"></a>Manuelle Exemplarische Vorgehensweise

Um den Prozess zu veranschaulichen und hoffentlich das Verständnis der Vorgehensweise zu verbessern, werde ich die einzelnen Komponenten manuell schrittweise durchlaufen.

Durch Ausführen von Befehl 1 werden ähnliche Ergebnisse wie in der folgenden Ausgabe zurückgegeben. In diesem Beispiel werden nur 16 Dateien aus Gründen der Kürze verwendet. Verwenden Sie immer 32 für Windows 2008 und spätere Betriebssysteme und 9 für Windows 2003 R2.

### <a name="example-data-returned-by-powershell"></a>Von PowerShell zurückgegebene Beispiel Daten

<table>
<tbody>
<tr class="odd">
<td>Name</td>
<td>Länge</td>
</tr>
<tr class="even">
<td><strong>File5.zip</strong></td>
<td>10286089216</td>
</tr>
<tr class="odd">
<td><strong>archive.zip</strong></td>
<td>6029853696</td>
</tr>
<tr class="even">
<td><strong>BACKUP.zip</strong></td>
<td>5751522304</td>
</tr>
<tr class="odd">
<td> <strong>file9.zip</strong></td>
<td>5472683008</td>
</tr>
<tr class="even">
<td><strong>MENTOS.zip</strong></td>
<td>5241586688</td>
</tr>
<tr class="odd">
<td><strong>File7.zip</strong></td>
<td>4321264640</td>
</tr>
<tr class="even">
<td><strong>file2.zip</strong></td>
<td>4176765952</td>
</tr>
<tr class="odd">
<td><strong>frd2.zip</strong></td>
<td>4176765952</td>
</tr>
<tr class="even">
<td><strong>BACKUP.zip</strong></td>
<td>4078994432</td>
</tr>
<tr class="odd">
<td><strong>File44.zip</strong></td>
<td>4058424320</td>
</tr>
<tr class="even">
<td><strong>file11.zip</strong></td>
<td>3858056192</td>
</tr>
<tr class="odd">
<td><strong>Backup2.zip</strong></td>
<td>3815138304</td>
</tr>
<tr class="even">
<td><strong>BACKUP3.zip</strong></td>
<td>3815138304</td>
</tr>
<tr class="odd">
<td><strong>Current.zip</strong></td>
<td>3576931328</td>
</tr>
<tr class="even">
<td><strong>Backup8.zip</strong></td>
<td>3307488256</td>
</tr>
<tr class="odd">
<td><strong>File999.zip</strong></td>
<td>3274982400</td>
</tr>
</tbody>
</table>

### <a name="how-to-use-this-data-to-determine-the-minimum-staging-area-size"></a>Verwenden dieser Daten, um die minimale Größe des Stagingbereichs zu ermitteln:

  - Name = Name der Datei.
  - Länge = bytes
  - Ein Gigabyte = 1073741824 bytes

Zuerst müssen Sie die Gesamtzahl der Bytes summieren. Teilen Sie als nächstes die Summe um 1073741824. Ich schlage vor, Excel oder das gewünschte Arbeitsblatt für die mathematische Verwendung zu verwenden.

### <a name="example"></a>Beispiel

Im obigen Beispiel wird die Gesamtzahl der Bytes = 75241684992. Um das minimale Kontingent für das staginggebiet zu erhalten, muss ich 75241684992 durch 1073741824 dividieren.

> 75241684992/1073741824 = 70,07 GB

Basierend auf diesen Daten würde ich den Stagingbereich auf 71 GB festlegen, wenn ich auf die nächste ganze Zahl aufgerundet.

### <a name="real-world-scenario"></a>Szenario in der Praxis:

Während eine manuelle Exemplarische Vorgehensweise interessant ist, ist es wahrscheinlich nicht die beste Verwendung ihrer Zeit, um die Mathematik selbst durchzuführen. Um den Prozess zu automatisieren, verwenden Sie Befehl 3 aus den Beispielen oben. Die Ergebnisse sehen wie folgt aus.

> [![Klang](https://msdnshared.blob.core.windows.net/media/TNBlogsFS/prod.evol.blogs.technet.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/58/02/metablogapi/8204.image_thumb_02CB3914.png "image")](https://msdnshared.blob.core.windows.net/media/TNBlogsFS/prod.evol.blogs.technet.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/58/02/metablogapi/0876.image_03A39EFE.png)

Mit dem Beispiel Befehl 3 ohne zusätzlichen Aufwand, außer bei der Rundung auf die nächste ganze Zahl, kann ich feststellen, dass ich ein 6 GB großes stagingbereichkontingent für d: docs benötige \\ .

## <a name="do-i-need-to-reboot-or-restart-the-service-for-the-changes-to-be-picked-up"></a>Muss der Dienst neu gestartet oder neu gestartet werden, damit die Änderungen übernommen werden?

Für Änderungen am Kontingent des Stagingbereichs ist es nicht erforderlich, dass der Dienst neu gestartet oder neu gestartet wird. Sie müssen auf die AD-Replikation und den AD-Abruf Zeitraum von DFSR warten, damit die Änderungen angewendet werden.

## <a name="how-to-determine-if-you-have-a-staging-area-problem"></a>Ermitteln, ob Probleme mit dem Stagingbereich auftreten

Sie erkennen Probleme mit dem Stagingbereich, indem Sie bestimmte Ereignisse-IDs auf Ihren DFSR-Servern überwachen. Die Liste der Ereignisse lautet 4202, 4204, 4206, 4208 und 4212. Die Texte dieser Ereignisse sind unten aufgeführt. Es ist wichtig, zwischen 4202 und 4204 und den anderen Ereignissen zu unterscheiden. Es ist möglich, eine große Anzahl von 4202-und 4204-Ereignissen unter normalen Betriebsbedingungen zu protokollieren. Stellen Sie sich vor, dass sich 4202-und 4204-Ereignisse analog zu den Puls nehmen, während 4206, 4208 und 4212 wie die brustprobleme sind. Im folgenden wird erläutert, wie die 4202-und 4204-Ereignisse interpretiert werden.

### <a name="staging-area-events"></a>Ereignisse im Stagingbereich

> Ereignis-ID: **4202** Schweregrad: **Warnung**
>
> Der DFS-Replikation Dienst hat festgestellt, dass der Stagingbereich, der für den replizierten Ordner im lokalen Pfad (Pfad) verwendet wird, über dem oberen Grenzwert liegt. Der Dienst versucht, die ältesten Stagingdateien zu löschen. Die Leistung kann beeinträchtigt werden.
>
> Ereignis-ID: **4204** Schweregrad: **Information**
>
> Der DFS-Replikation Dienst hat alte Stagingdateien für den replizierten Ordner unter dem lokalen Pfad (Pfad) erfolgreich gelöscht. Der Stagingbereich liegt nun unter dem hohen Grenzwert.
>
> Ereignis-ID: **4206** Schweregrad: **Warnung**
>
> Der DFS-Replikation-Dienst konnte die alten Stagingdateien für den replizierten Ordner unter dem lokalen Pfad (Pfad) nicht bereinigen. Der Dienst kann möglicherweise einige große Dateien nicht replizieren, und der replizierte Ordner ist möglicherweise nicht mehr synchron. Der Dienst versucht automatisch, den stagingbereinigungs-Bereinigung in (x) Minuten zu wiederholen. Der Dienst startet die Bereinigung möglicherweise früher, wenn er erkennt, dass einige Stagingdateien entsperrt wurden.
>
> Ereignis-ID: **4208** Schweregrad: **Warnung**
>
> Der DFS-Replikation Dienst hat festgestellt, dass die Speicherplatz Auslastung über dem Stagingkontingent für den replizierten Ordner unter lokaler Pfad (Pfad) liegt. Der Dienst kann möglicherweise einige große Dateien nicht replizieren, und der replizierte Ordner ist möglicherweise nicht mehr synchron. Der Dienst versucht automatisch, den Stagingbereich zu bereinigen.
>
> Ereignis-ID: **4212** Schweregrad: **Fehler**
>
> Der DFS-Replikation Dienst konnte den replizierten Ordner nicht unter dem lokalen Pfad (Pfad) replizieren, da der Stagingpfad ungültig oder nicht verfügbar ist.

## <a name="what-is-the-difference-between-4202-and-4208"></a>Worin besteht der Unterschied zwischen 4202 und 4208?

Die Ereignisse 4202 und 4208 weisen einen ähnlichen Text auf. DFSR hat festgestellt, dass die Nutzung des Stagingbereichs den hohen Grenzwert überschreitet. Der Unterschied besteht darin, dass 4208 protokolliert wird, nachdem die Bereinigung des Stagingbereichs ausgeführt und das Stagingkontingent weiterhin überschritten wurde. 4202 ist ein normales und erwartetes Ereignis, während 4208 nicht normal ist und Eingreifen erfordert.

## <a name="how-many-4202-4204-events-are-too-many"></a>Wie viele 4202-und 4204-Ereignisse sind zu lang?

Es gibt keine einzelne Antwort auf diese Frage. Im Gegensatz zu 4206-, 4208-oder 4212-Ereignissen, die immer schlecht sind und angeben, dass eine Aktion erforderlich ist, werden die Ereignisse 4202 und 4204 unter normalen Betriebsbedingungen ausgeführt. Viele 4202-und 4204-Ereignisse *können* auf ein Problem hinweisen. Ziehen Sie Folgendes in Betracht:

1.  Führt der replizierte Ordner (RF) 4202 die anfängliche Replikation aus? Wenn dies der Fall ist, ist es normal, die Ereignisse 4202 und 4204 zu protokollieren. Sie sollten diese bei der ersten Replikation so wenig wie möglich halten, indem Sie so viel Stagingbereich wie möglich bereitstellen.
2.  Die einfache Überprüfung der Gesamtanzahl von 4202-Ereignissen ist nicht ausreichend. Sie müssen wissen, wie viele pro RF protokolliert wurden. Wenn Sie 20 4202-Ereignisse für eine RF in einem Zeitraum von 24 Stunden protokollieren, der hoch ist. Wenn Sie jedoch über 20 replizierte Ordner verfügen und ein Ereignis pro Ordner vorhanden ist, sind Sie gut.
3.  Sie sollten mehrere Tage Daten überprüfen, um Trends zu ermitteln.

Ich gebe Kunden in der Regel an, dass unter normalen Betriebsbedingungen nicht mehr als 1 4202 Ereignis pro repliziertem Ordner pro Tag zulässig ist. "Normal" bedeutet, dass keine anfängliche Replikation stattfindet. Ich basiere auf der Begründung:

1.  Die Zeit, die für das Bereinigen des Stagingbereichs aufgewendet wurde, ist die Zeit, die für das Die Replikation wird angehalten, während der Stagingbereich gelöscht wird.
2.  DFSR profitiert von einem vollständigen Stagingbereich, der für die RDC-und Datei übergreifende RDC-Datei oder das Replizieren derselben Dateien auf andere Mitglieder verwendet wird.
3.  Die mehr 4202-und 4204-Ereignisse, die Sie protokollieren, treten in der Situation auf, in der DFSR den Stagingbereich nicht bereinigen kann oder Dateien vorzeitig aus dem Stagingbereich löschen muss.
4.  4206-, 4208-und 4212-Ereignisse sind in meiner Ober Arbeit immer einer hohen Anzahl von 4202-und 4204-Ereignissen vorangestellt.

Obwohl das Zulassen von nur 1 4202-Ereignis pro RF pro Tag konservativ ist, verringert es die Wahrscheinlichkeit, dass Probleme im Stagingbereich auftreten, und nutzt die Ressourcen Ihres DFSR-Servers für den vorgesehenen Zweck der Replikation von Dateien.


