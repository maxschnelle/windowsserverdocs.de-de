---
title: Aktivieren des Banner zum Ermitteln der Erweiterung
description: Aktivieren des Banner zum Ermitteln der Erweiterung
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: fb549d84f565feeea348d2f50a9188218e7638d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357077"
---
# <a name="enabling-the-extension-discovery-banner"></a>Aktivieren des Banner zum Ermitteln der Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Ein neues Feature, das in der Windows Admin Center Preview 1903 verfügbar ist, ist das Banner zur Ermittlung von Erweiterungen. Diese Funktion ermöglicht einer Erweiterung das Deklarieren des Server Hardwareherstellers und der von ihr unterstützten Modelle. Wenn ein Benutzer eine Verbindung mit einem Server oder Cluster herstellt, für den eine Erweiterung verfügbar ist, wird ein Benachrichtigungs Banner angezeigt, um die Erweiterung zu installieren. Erweiterungs Entwickler können eine höhere Sichtbarkeit für Ihre Erweiterungen erzielen, und Benutzer können auf einfache Weise weitere Verwaltungsfunktionen für Ihre Server ermitteln.

![Banner für die Erweiterungs Ermittlung](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>Funktionsweise des Banner zur Erweiterungs Ermittlung

Wenn das Windows Admin Center gestartet wird, stellt es eine Verbindung mit den registrierten Erweiterungs Feeds her und ruft die Metadaten für die verfügbaren Erweiterungs Pakete ab. Wenn ein Benutzer dann im Windows Admin Center eine Verbindung mit einem Server oder Cluster herstellt, lesen wir den Hersteller und das Modell der Server Hardware, die im Übersichts Tool angezeigt werden. Wenn wir eine Erweiterung finden, die deklariert, dass Sie den Hersteller und das Modell des aktuellen Servers unterstützt, wird ein Banner angezeigt, das den Benutzern mitzuteilen. Wenn Sie auf den Link "jetzt einrichten" klicken, wird der Benutzer in den Erweiterungs-Manager übernommen, wo er die Erweiterung installieren kann.

## <a name="how-to-implement-the-extension-discovery-banner"></a>So implementieren Sie das Banner für die Erweiterungs Ermittlung

Die "Tags"-Metadaten in der nuspec-Datei werden verwendet, um die von der Erweiterung unterstützten Hardwarehersteller und/oder Modelle zu deklarieren. Tags werden durch Leerzeichen getrennt, und Sie können entweder einen Hersteller oder ein modelltag oder beides hinzufügen, um den unterstützten Hersteller und/oder die unterstützten Modelle zu deklarieren. Das Tagformat ist ``"[value type]_[value condition]"``, wobei [Werttyp] entweder "Hersteller" oder "Modell" (Groß-/Kleinschreibung beachten) und [Wert Bedingung] ein [regulärer JavaScript-Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) ist, der den Hersteller oder die Modell Zeichenfolge definiert, und [Werttyp] und [Wert Bedingung] getrennt sind. durch einen Unterstrich. Diese Zeichenfolge wird dann mithilfe der URI-Codierung codiert und zur nuspec-Metadatenzeichenfolge "Tags" hinzugefügt.

### <a name="example"></a>Beispiel

Nehmen wir an, ich habe eine Erweiterung entwickelt, die Server von einem Unternehmen mit dem Namen "Configuration Manager" mit dem Modellnamen "R3xx" und "R4xx" unterstützt.

1. Das Tag für den Hersteller wäre ``"Manufacturer_/Contoso Inc./"``. Das Tag für die Modelle kann ``"Model_/^R[34][0-9]{2}$/"`` sein. Abhängig davon, wie genau die Übereinstimmungs Bedingung definiert werden soll, gibt es verschiedene Möglichkeiten zum Definieren des regulären Ausdrucks. Sie können auch die Hersteller-oder Modell Tags in mehrere Tags aufteilen, beispielsweise könnte das modelltag auch ``"Model_/R3../ Model_/R4../"`` sein.
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
> Wir wissen, dass ein Hardwarehersteller vielfältige Modellnamen aufweisen kann, von denen einige möglicherweise nicht unterstützt werden. Beachten Sie, dass dieses Feature **bei der Ermittlung** ihrer Erweiterung helfen soll, aber es muss sich nicht um eine vollständig aktuellste Inventur aller Modelle handeln. Sie können den regulären Ausdruck als einfacheren Ausdruck definieren, der mit einer Teilmenge der Modelle übereinstimmt. Ein Benutzer sieht das Discovery-Banner möglicherweise nicht, wenn er zum ersten Mal eine Verbindung mit einem Server Modell herstellt, das nicht mit der Bedingung identisch ist, aber früher oder später eine Verbindung mit einem anderen Server herstellt, von dem die Erweiterung erkannt und installiert wird. Sie können auch einen einfachen regulären Ausdruck definieren, der nur mit dem Herstellernamen übereinstimmt. In einigen Fällen unterstützt Ihre Erweiterung möglicherweise ein bestimmtes Modell nicht, aber Sie können das [Feature "Dynamic Tool Display](./dynamic-tool-display.md) " verwenden, um ein benutzerdefiniertes PowerShell-Skript zum Überprüfen der Unterstützung von Modellen zu definieren und ihre Erweiterung bei entsprechender Angabe nur anzuzeigen oder eine begrenzte Funktionen in ihrer Erweiterung für Modelle, die nicht alle Funktionen unterstützen.