---
title: Aktivieren die Erweiterung Discovery-banner
description: Aktivieren die Erweiterung Discovery-banner
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fafc16d6acae3c5a7a58a379d2f88998b8e98c3d
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811880"
---
# <a name="enabling-the-extension-discovery-banner"></a>Aktivieren die Erweiterung Discovery-banner

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Ein neues Feature in Windows Admin Center Preview 1903 ist das Extension-Discovery-Banner. Mit diesem Feature können eine Erweiterung, deklarieren die Hardware-Hersteller und die Modelle, die es unterstützt, und wenn ein Benutzer eine Verbindung, auf einem Server oder Cluster, die für die eine Erweiterung verfügbar ist herstellt, ein benachrichtigungsbanner angezeigt wird, um die Erweiterung zu installieren. Entwickler von Erweiterungen werden in der Lage, mehr Transparenz für ihre Erweiterungen zu erhalten, und Benutzer werden in der Lage, weitere Funktionen für ihre Server leicht zu erkennen.

![Erweiterung Discovery-banner](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>Wie funktioniert das Extension-Discovery-banner

Wenn Windows Admin Center gestartet wird, wird eine Verbindung herstellen, die registrierte Extension-Feeds und Abrufen der Metadaten für die verfügbare Erweiterungspakete. Wenn ein Benutzer mit einem Server oder Cluster in Windows Admin Center verbunden ist, lesen wir klicken Sie dann die Hardware-Hersteller und Modell, in der Übersicht über die Tools angezeigt. Wenn es sich um eine Erweiterung, die deklariert gefunden, dass sie Hersteller und/oder ein Modell für des aktuellen Servers unterstützt, zeigen wir ein Banner aus, um den Benutzer informieren. Auf den Link "Jetzt einrichten" wird der Benutzer ausführen auf Erweiterungs-Manager, in dem sie die Erweiterung installieren können.

## <a name="how-to-implement-the-extension-discovery-banner"></a>Gewusst wie: Implementieren Sie die Erweiterung Discovery-banner

Die "Tags"-Metadaten in der NuSpec-Datei wird verwendet, um die Hardware-Hersteller deklarieren und/oder modelliert die Erweiterung unterstützt. Tags durch Leerzeichen getrennt sind, und Sie können entweder einen Hersteller oder Modell Tag oder beides zum Deklarieren der unterstützten Hersteller und/oder Modelle hinzufügen. Das Tagformat ist ``"[value type]_[value condition]"`` wobei [Typ] "Manufacturer" oder "Model" (Groß-/ Kleinschreibung) und [Wert] beachtet werden muss eine [reguläre Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) definieren, Hersteller oder Modellzeichenfolge ein, und [Typ] und [ die wertbedingung] durch einen Unterstrich voneinander getrennt sind. Diese Zeichenfolge wird dann codiert und URI-Codierung und die Metadatenzeichenfolge für den "NuSpec"Tags"hinzugefügt.

### <a name="example"></a>Beispiel

Angenommen, ich habe eine Erweiterung, die von einem Unternehmen namens Contoso Inc., mit dem Modell unterstützt entwickelt benennen R3xx und R4xx.

1. Das Tag für den Hersteller wäre ``"Manufacturer_/Contoso Inc./"``. Das Tag für die Modelle möglicherweise ``"Model_/^R[34][0-9]{2}$/"``. Je nachdem wie streng Sie die entsprechende Bedingung definieren möchten stehen verschiedene Möglichkeiten, den regulären Ausdruck zu definieren. Sie können auch die Hersteller oder Modell-Tags in mehreren Tags trennen, z. B. modelltag kann auch sein ``"Model_/R3../ Model_/R4../"``.
2. Sie können den regulären Ausdruck mit Ihrem Webbrowser DevTools-Konsole testen. Klicken Sie in Edge oder Chrome drücken Sie F12, um das DevTools-Fenster zu öffnen, und geben Sie in der Registerkarte "Konsole" den folgende, und klicken Sie auf die EINGABETASTE:

   ```javascript
   var regex = /^R[34][0-9]{2}$/
   ```

   Wenn Sie eingeben, und führen Sie den folgenden Befehl, wird zurückgegeben 'true'.

   ```javascript
   regex.test('R300')
   ```

   Und wenn Sie Folgendes ausführen, wird "false" zurückgegeben.

   ```javascript
   regex.test('R500')
   ```

3. Nachdem Sie den regulären Ausdruck überprüft haben, können Sie es in der DevTools-Konsole, codieren mit dem folgenden Javascript-Verfahren:

   ```javascript
   encodeURI(/^R[34][0-9]{2}$/)
   ```

   Es wäre das endgültige Format der Zeichenfolge Tag Ihrer NuSpec-Datei hinzu:

   ```
   <tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
   ```

> [!Tip]
> Uns ist bewusst, dass Hardware-Hersteller eine große Bandbreite von Modellnamen möglicherweise von denen einige möglicherweise unterstützt werden, während einige nicht sind. Denken Sie daran, die diese Funktion sich zur Unterstützung eignet der **Ermittlung** Ihrer Erweiterung, aber es muss keine perfekt aktuelle Inventarliste aller Modelle werden. Sie können definieren, dass den regulären Ausdruck, um ein einfacher Ausdruck sein, der eine Teilmenge Ihrer Modelle entspricht. Ein Benutzer möglicherweise nicht das Discovery-Banner angezeigt, wenn zuerst ein Server-Modell herstellen, die mit die Bedingung übereinstimmt, aber früher oder später sie eine Verbindung mit einem anderen Server, der ist und zu ermitteln und installieren die Erweiterung. Sie können auch erwägen, definieren einen einfachen regulären Ausdruck, der nur den Namen des Herstellers entspricht. In einigen Fällen die Erweiterung unterstützt möglicherweise kein bestimmtes Modell, aber Sie können die [dynamisches Tool Anzeige Feature](./dynamic-tool-display.md) definieren Sie ein benutzerdefiniertes Powershellskript zum Überprüfen der Unterstützung und zeigt nur die Erweiterung, falls zutreffend, oder Geben Sie eingeschränkten Funktionalität in Ihrer Erweiterung, für die Modelle, die nicht alle Funktionen unterstützen.