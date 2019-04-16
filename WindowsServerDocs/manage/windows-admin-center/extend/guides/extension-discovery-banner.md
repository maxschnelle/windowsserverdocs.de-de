---
title: Aktivieren die Erweiterung-Discovery-banner
description: Aktivieren die Erweiterung-Discovery-banner
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/08/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 389acba6d1fe6f65320bd780c9fde6469b387e0b
ms.sourcegitcommit: e558dda2774345e9ad17ff04b759f68c59d88139
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "9262967"
---
# Aktivieren die Erweiterung-Discovery-banner #

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Ein neues Feature in Windows Admin Center Vorschau 1903 verfügbar ist, die Erweiterung-Discovery-Banner. Dieses Feature ermöglicht eine Erweiterung Server Hardwarehersteller und Modelle, die er unterstützt deklariert, und wenn ein Benutzer eine mit einem Server oder Cluster für die Erweiterung verfügbar ist Verbindung, wird eine Benachrichtigung Banner angezeigt werden, um einfach die Erweiterung zu installieren. Erweiterung-Entwickler sind in der Lage, mehr Sichtbarkeit für ihre Erweiterungen zu erhalten, und Benutzer werden in der Lage, weitere Verwaltungsfunktionen für die Server leicht zu erkennen.

![Erweiterung Discovery banner](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## Wie funktioniert die Erweiterung-Discovery-banner ##

Wenn Windows Admin Center gestartet wird, wird es für die registrierten Extension-Feeds verbinden und die Metadaten für die verfügbaren Erweiterung Pakete abrufen. Wenn ein Benutzer mit einem Server oder Cluster in Windows Admin Center verbunden ist, lesen Sie dann wir Server-Hardware-Hersteller und Modell in der Übersicht über die Tools angezeigt. Wenn wir eine Erweiterung, die deklariert suchen, dass er des aktuellen Servers Hersteller bzw. Modell unterstützt, wird ein Banner, um dem Benutzer mitzuteilen, lassen angezeigt. Klicken Sie auf den Link "Jetzt einrichten" wird der Benutzer ausführen auf Erweiterungs-Managers, in denen sie die Erweiterung installieren können.

## Wie Sie die Erweiterung-Discovery-Banner implementieren ##

Die Metadaten "Tags" in der Datei .nuspec wird verwendet, um welche Hardwarehersteller deklarieren und/oder Modelle Ihre Erweiterung unterstützt. Tags werden durch Leerzeichen getrennt, und Sie können entweder ein Hersteller Modell Tag oder beides um Deklarieren der unterstützten Hersteller bzw. Modelle hinzufügen. Das Tag-Format ist ``"[value type]_[value condition]"`` dabei [Werttyp] "Hersteller" oder "Modell" (Groß-/Kleinschreibung beachten) und [Wert Bedingung] ist eine [regulärer Javascript-Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) definieren die Hersteller oder Modellzeichenfolge und [Werttyp] und [Wert Bedingung] sind durch einen Unterstrich getrennt. Diese Zeichenfolge wird dann codiert mit URI-Codierung und die Metadaten-Zeichenfolge .nuspec "Tags" hinzugefügt.

### Beispiel ###

Nehmen wir an ich eine Erweiterung, die Server von einem Unternehmen namens Contoso Inc. mit Modell unterstützt haben entwickelt, benennen Sie R3xx und R4xx.

1. Das Tag für den Hersteller wäre ``"Manufacturer_/Contoso Inc./"``. Das Tag für die Modelle wäre ``"Model_/^R[34][0-9]{2}$/"``. Je nachdem, wie streng die Bedingung definiert werden soll werden verschiedene Möglichkeiten, Ihre regulären Ausdruck zu definieren. Sie können auch die Hersteller oder das Modell Tags in mehrere Tags trennen, z. B. das Modell Tag kann auch ``"Model_/R3../ Model_/R4../"``.
2. Sie können den regulären Ausdruck in Ihrem Webbrowser DevTools-Konsole testen. Klicken Sie in Edge oder Chrome F12, um das DevTools-Fenster öffnen erreicht, und geben Sie in der Registerkarte "Konsole" die folgenden und Treffertests EINGABETASTE:

```javascript
var regex = /^R[34][0-9]{2}$/
```

Wenn Sie eingeben, und führen Sie Folgendes aus, es zurück "" true ",".

```javascript
regex.test('R300')
```

Und wenn Sie Folgendes ausführen, wird "false" zurückgegeben.

```javascript
regex.test('R500')
```

3. Nachdem Sie den regulären Ausdruck überprüft haben, können Sie es in der DevTools-Konsole auch Codieren mithilfe der folgenden Javascript-Methode:

```javascript
encodeURI(/^R[34][0-9]{2}$/)
```

Es wäre das endgültige Format der Zeichenfolge Tag Ihrer .nuspec-Datei hinzu:

```
<tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
```

> [!Tip]
> Wir sind uns bewusst, dass eine Hardwarehersteller eine sehr breite Palette von Modellnamen möglicherweise von denen einige unterstützt, werden möglicherweise während einige nicht sind. Denken Sie daran, die dieses Feature dient dazu, bei der **Ermittlung** der Erweiterung helfen, aber es muss nicht unbedingt eine perfekt auf dem neuesten Stand Inventur aller Ihrer Modelle werden. Sie können Ihre regulären Ausdruck zum ein einfacher Ausdruck sein, der einen Teil Ihrer Modelle entspricht definieren. Ein Benutzer möglicherweise nicht das Discovery-Banner angezeigt, wenn sie zuerst ein Server-Modell herstellen, die die Bedingung übereinstimmt, aber früher oder später Benutzer werden die Verbindung mit einem anderen Server verfügt und erkennen und installieren Sie die Erweiterung. Sie können auch überlegen, definieren einen einfachen regulären Ausdruck, der nur den Namen des Herstellers entspricht. In einigen Fällen können unterstützt die Erweiterung eines bestimmten Modells möglicherweise nicht, Sie jedoch die [Dynamisches Tool anzeigen Feature](./dynamic-tool-display.md) verwenden, definieren Sie ein benutzerdefiniertes Powershellskript zum Suchen von Modell Unterstützung und zeigen nur die Erweiterung, wenn zutreffend, oder bieten begrenzte Funktionen in der Erweiterung für Modelle, die alle Funktionen nicht unterstützen.