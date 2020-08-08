---
title: Aktivieren des Banner zum Ermitteln der Erweiterung
description: Aktivieren des Banner zum Ermitteln der Erweiterung
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: ef08eec08b43f83121bc94abc46a5f657556db65
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945022"
---
# <a name="enabling-the-extension-discovery-banner"></a>Aktivieren des Banner zum Ermitteln der Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Das Erweiterungs Ermittlungs Banner-Feature wurde in der Version Windows Admin Center Preview 1903 eingeführt. Diese Funktion ermöglicht einer Erweiterung das Deklarieren des Server Hardwareherstellers und der von ihr unterstützten Modelle. Wenn ein Benutzer eine Verbindung mit einem Server oder Cluster herstellt, für den eine Erweiterung verfügbar ist, wird ein Benachrichtigungs Banner angezeigt, um die Erweiterung zu installieren. Erweiterungs Entwickler können eine höhere Sichtbarkeit für Ihre Erweiterungen erzielen, und Benutzer können auf einfache Weise weitere Verwaltungsfunktionen für Ihre Server ermitteln.

![Banner für die Erweiterungs Ermittlung](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>Funktionsweise des Banner zur Erweiterungs Ermittlung

Wenn das Windows Admin Center gestartet wird, stellt es eine Verbindung mit den registrierten Erweiterungs Feeds her und ruft die Metadaten für die verfügbaren Erweiterungs Pakete ab. Wenn ein Benutzer dann im Windows Admin Center eine Verbindung mit einem Server oder Cluster herstellt, lesen wir den Hersteller und das Modell der Server Hardware, die im Übersichts Tool angezeigt werden. Wenn wir eine Erweiterung finden, die deklariert, dass Sie den Hersteller und das Modell des aktuellen Servers unterstützt, wird ein Banner angezeigt, das den Benutzern mitzuteilen. Wenn Sie auf den Link "jetzt einrichten" klicken, wird der Benutzer in den Erweiterungs-Manager übernommen, wo er die Erweiterung installieren kann.

## <a name="how-to-implement-the-extension-discovery-banner"></a>So implementieren Sie das Banner für die Erweiterungs Ermittlung

Die "Tags"-Metadaten in der nuspec-Datei werden verwendet, um die von der Erweiterung unterstützten Hardwarehersteller und/oder Modelle zu deklarieren. Tags werden durch Leerzeichen getrennt, und Sie können entweder einen Hersteller oder ein modelltag oder beides hinzufügen, um den unterstützten Hersteller und/oder die unterstützten Modelle zu deklarieren. Das Tagformat ist ``"[value type]_[value condition]"`` , wobei [Werttyp] entweder ' Hersteller ' oder ' Model ' (Groß-/Kleinschreibung beachten) und [value Condition] ein [regulärer JavaScript-Ausdruck](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Regular_Expressions) ist, der den Hersteller oder die Modell Zeichenfolge definiert, und [Werttyp] und [value Condition] durch einen Unterstrich voneinander getrennt sind. Diese Zeichenfolge wird dann mithilfe der URI-Codierung codiert und zur nuspec-Metadatenzeichenfolge "Tags" hinzugefügt.

### <a name="example"></a>Beispiel

Nehmen wir an, ich habe eine Erweiterung entwickelt, die Server von einem Unternehmen mit dem Namen "Configuration Manager" mit dem Modellnamen "R3xx" und "R4xx" unterstützt.

1. Das Tag für den Hersteller wäre ``"Manufacturer_/Contoso Inc./"`` . Das-Tag für die Modelle kann sein ``"Model_/^R[34][0-9]{2}$/"`` . Abhängig davon, wie genau die Übereinstimmungs Bedingung definiert werden soll, gibt es verschiedene Möglichkeiten zum Definieren des regulären Ausdrucks. Sie können auch die Hersteller-oder Modell Tags in mehrere Tags aufteilen, beispielsweise könnte auch das modelltag lauten ``"Model_/R3../ Model_/R4../"`` .
2. Sie können den regulären Ausdruck mit der devtools-Konsole Ihres Webbrowsers testen. Drücken Sie in Edge oder Chrome F12, um das devtools-Fenster zu öffnen, und geben Sie auf der Registerkarte Konsole Folgendes ein, und drücken Sie die EINGABETASTE:

   ```javascript
   var regex = /^R[34][0-9]{2}$/
   ```

   Wenn Sie Folgendes eingeben und ausführen, wird "true" zurückgegeben.

   ```javascript
   regex.test('R300')
   ```

   Wenn Sie Folgendes ausführen, wird "false" zurückgegeben.

   ```javascript
   regex.test('R500')
   ```

3. Nachdem Sie den regulären Ausdruck überprüft haben, können Sie ihn auch in der devtools-Konsole codieren, indem Sie die folgende JavaScript-Methode verwenden:

   ```javascript
   encodeURI(/^R[34][0-9]{2}$/)
   ```

   Das endgültige Format der Tagzeichenfolge, die der nuspec-Datei hinzugefügt werden soll, lautet wie folgt:

   ```
   <tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
   ```

> [!Tip]
> Wir wissen, dass ein Hardwarehersteller vielfältige Modellnamen aufweisen kann, von denen einige möglicherweise nicht unterstützt werden. Beachten Sie, dass dieses Feature **bei der Ermittlung** ihrer Erweiterung helfen soll, aber es muss sich nicht um eine vollständig aktuellste Inventur aller Modelle handeln. Sie können den regulären Ausdruck als einfacheren Ausdruck definieren, der mit einer Teilmenge der Modelle übereinstimmt. Ein Benutzer sieht das Discovery-Banner möglicherweise nicht, wenn er zum ersten Mal eine Verbindung mit einem Server Modell herstellt, das nicht mit der Bedingung identisch ist, aber früher oder später eine Verbindung mit einem anderen Server herstellt, von dem die Erweiterung erkannt und installiert wird. Sie können auch einen einfachen regulären Ausdruck definieren, der nur mit dem Herstellernamen übereinstimmt. In einigen Fällen unterstützt Ihre Erweiterung möglicherweise nicht ein bestimmtes Modell, Sie können jedoch mit dem [Feature "dynamische Tool Anzeige](./dynamic-tool-display.md) " ein benutzerdefiniertes PowerShell-Skript zum Überprüfen der Modell Unterstützung definieren und ihre Erweiterung bei Bedarf nur anzeigen. Sie können auch für Modelle, die nicht alle Funktionen unterstützen, eingeschränkte Funktionen in ihrer Erweiterung bereitstellen.