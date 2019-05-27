---
title: Erstellen einer Klassifizierungseigenschaft
description: Dieser Artikel beschreibt die verwendeten Klassifizierungseigenschaften, um Dateien im angegebenen Ordner oder Volumes Werte zuzuweisen.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: aa1f1a2ab4422f4bb36a737e47894b22b60160e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880651"
---
# <a name="create-a-classification-property"></a>Erstellen einer Klassifizierungseigenschaft

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Klassifizierungseigenschaften werden verwendet, um Dateien im angegebenen Ordner oder Volumes Werte zuzuweisen. Es gibt viele Eigenschaftstypen, die Sie je nach Bedarf auswählen können. In der folgenden Tabelle werden die verfügbaren Eigenschaftstypen beschrieben:

|Eigenschaft | Beschreibung |
| --- | --- |
| Ja/Nein | Eine boolesche Eigenschaft kann **Ja** oder **Nein** sein. Wenn Sie mehrere Werte während der Klassifizierung oder von Dateiinhalten kombinieren, wird ein **Nein**-Wert wird von einem **Ja**‑Wert überschrieben. |
| Datum und Uhrzeit | Eine einfache Datum/Uhrzeit-Eigenschaft. Wenn Sie mehrere Werte während der Klassifizierung oder aus Dateiinhalten kombinieren, verhindern die in Konflikt stehenden Werte eine erneute Klassifizierung. |
| Number | Eigenschaft einer einfachen Zahl. Wenn Sie mehrere Werte während der Klassifizierung oder aus Dateiinhalten kombinieren, verhindern die in Konflikt stehenden Werte eine erneute Klassifizierung. |
| Sortierte Liste | Eine Liste der festen Werte. Einer Eigenschaft kann jeweils nur ein Wert zugewiesen werden. Wenn Sie mehrere Werte während der Klassifizierung oder von Dateiinhalten kombinieren, wird der höchste Wert der Liste verwendet. |
| Zeichenfolge | Eigenschaft einer einfachen Zeichenfolge. Wenn Sie mehrere Werte während der Klassifizierung oder aus Dateiinhalten kombinieren, verhindern die in Konflikt stehenden Werte eine erneute Klassifizierung. |
| Mehrfachauswahl | Eine Liste der Werte, die einer Eigenschaft zugewiesen werden können. Einer Eigenschaft können mehrere Werte zugewiesen werden. Wenn Sie mehrere Werte während der Klassifizierung oder von Dateiinhalten kombinieren, wird jeder Wert der Liste verwendet. |
| Mehrteilige Zeichenfolge | Eine Liste der Zeichenfolgen, die einer Eigenschaft zugewiesen werden können. Einer Eigenschaft können mehrere Werte zugewiesen werden. Wenn Sie mehrere Werte während der Klassifizierung oder von Dateiinhalten kombinieren, wird jeder Wert der Liste verwendet. |

<br />

Die folgende Anweisung führt Sie durch den Prozess zum Erstellen einer Klassifizierungseigenschaft.

## <a name="to-create-a-classification-property"></a>So erstellen Sie eine Klassifizierungseigenschaft

1.  Klicken Sie in der **Klassifizierungsverwaltung** auf den Knoten **Klassifizierungseigenschaft**.

2.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungseigenschaften** und dann auf **Neue Eigenschaft erstellen** (oder klicken Sie auf **Neue Eigenschaft erstellen** im Bereich **Aktionen** aus). Daraufhin wird das Dialogfeld **Definitionen für Klassifizierungseigenschaften** geöffnet.

3.  Geben Sie im Textfeld **Eigenschaftenname** einen Namen für die Eigenschaft ein.

4.  Geben Sie in das Textfeld **Beschreibung** eine optionale Beschreibung für die Eigenschaft ein.

5.  Wählen Sie im Dropdownmenü **Eigenschaftentyp** einen Eigenschaftentyp aus der Liste aus.

6.  Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Erstellen Sie eine Regel für die automatische Klassifizierung](create-automatic-classification-rule.md)
-   [Klassifizierungsverwaltung](classification-management.md)