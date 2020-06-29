---
title: Erstellen einer Klassifizierungseigenschaft
description: In diesem Artikel werden die Klassifizierungs Eigenschaften beschrieben, die zum Zuweisen von Werten zu Dateien in einem angegebenen Ordner oder Volume verwendet werden.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f8e0ba45883385a2b2bf161b04f99f8077fdef28
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473757"
---
# <a name="create-a-classification-property"></a>Erstellen einer Klassifizierungseigenschaft

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Klassifizierungs Eigenschaften werden verwendet, um Dateien in einem angegebenen Ordner oder Volume Werte zuzuweisen. Es gibt viele Eigenschafts Typen, aus denen Sie auswählen können, je nach Ihren Anforderungen. In der folgenden Tabelle sind die verfügbaren Eigenschafts Typen definiert.

|Eigenschaft | BESCHREIBUNG |
| --- | --- |
| Ja/Nein | Eine boolesche Eigenschaft, die " **Yes** " oder " **No**" sein kann. Wenn Sie mehrere Werte bei der Klassifizierung oder dem Dateiinhalt kombinieren, wird ein **kein** Wert durch einen **Yes** -Wert überschrieben. |
| Datum/Uhrzeit | Eine einfache Datums-/Uhrzeit-Eigenschaft. Beim Kombinieren mehrerer Werte während der Klassifizierung oder des Datei Inhalts wird durch widersprüchliche Werte die erneute Klassifizierung verhindert. |
| Number | Eine einfache Number-Eigenschaft. Beim Kombinieren mehrerer Werte während der Klassifizierung oder des Datei Inhalts wird durch widersprüchliche Werte die erneute Klassifizierung verhindert. |
| Geordnete Liste | Eine Liste fester Werte. Einer Eigenschaft kann jeweils nur ein Wert zugewiesen werden. Wenn Sie mehrere Werte bei der Klassifizierung oder dem Dateiinhalt kombinieren, wird der Wert, der in der Liste am höchsten ist, verwendet. |
| String | Eine einfache Zeichen folgen Eigenschaft. Beim Kombinieren von mehreren Werten während der Klassifizierung oder bei in Konflikt stehenden Werten von Dateiinhalten wird eine erneute Klassifizierung verhindert. |
| Mehrere Auswahlmöglichkeiten | Eine Liste von Werten, die einer Eigenschaft zugewiesen werden können. Einer Eigenschaft können jeweils mehr als ein Wert zugewiesen werden. Beim Kombinieren mehrerer Werte während der Klassifizierung oder des Datei Inhalts wird jeder Wert in der Liste verwendet. |
| Mehrere Zeichen folgen | Eine Liste von Zeichen folgen, die einer Eigenschaft zugewiesen werden können. Einer Eigenschaft können jeweils mehr als ein Wert zugewiesen werden. Beim Kombinieren mehrerer Werte während der Klassifizierung oder des Datei Inhalts wird jeder Wert in der Liste verwendet. |

<br />

Das folgende Verfahren führt Sie durch den Prozess der Erstellung einer Klassifizierungs Eigenschaft.

## <a name="to-create-a-classification-property"></a>So erstellen Sie eine Klassifizierungs Eigenschaft

1.  Klicken Sie in der **Klassifizierungs Verwaltung**auf den Knoten **Klassifizierungs Eigenschaften** .

2.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungs Eigenschaften**, und klicken Sie dann auf **Eigenschaft erstellen** (oder klicken Sie im **Aktions** Bereich auf **Eigenschaft erstellen** ). Dadurch wird das Dialogfeld **Klassifizierungs Eigenschafts Definitionen** geöffnet.

3.  Geben Sie im Textfeld **Eigenschaftsname** einen Namen für die Eigenschaft ein.

4.  Fügen Sie im Textfeld **Beschreibung** eine optionale Beschreibung für die Eigenschaft hinzu.

5.  Wählen Sie im Dropdownmenü **Eigenschaftentyp** einen Eigenschaftentyp aus der Liste aus.

6.  Klicken Sie auf **OK**.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Erstellen einer automatischen Klassifizierungsregel](create-automatic-classification-rule.md)
-   [Klassifizierungsverwaltung](classification-management.md)