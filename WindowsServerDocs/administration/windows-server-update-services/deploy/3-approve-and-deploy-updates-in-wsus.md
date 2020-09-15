---
title: 'Schritt 3: Genehmigen und Bereitstellen von Updates in WSUS'
description: 'WSUS-Thema (Windows Server Update Services): Genehmigen und Bereitstellen von Updates in WSUS – Dritter Schritt eines Prozesses mit vier Schritten für die Bereitstellung von WSUS'
ms.topic: article
ms.assetid: 8d728ff9-170f-47e6-aefe-52be93315a75
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9dbeebf6add9bcd81d8aa6066fb166a35937a692
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637567"
---
# <a name="step-3-approve-and-deploy-updates-in-wsus"></a>Schritt 3: Genehmigen und Bereitstellen von Updates in WSUS

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Computer in einer Computergruppe kontaktieren innerhalb der nächsten 24 Stunden automatisch den WSUS-Server, um Updates abzurufen. Mithilfe des WSUS-Berichtsfeatures können Sie feststellen, ob diese Updates auf den Testcomputern bereitgestellt wurden. Nach dem erfolgreichen Abschließen der Tests können Sie die Updates für die entsprechenden Computergruppen in Ihrer Organisation genehmigen. In der folgenden Prüfliste sind die Schritte zum Genehmigen und Bereitstellen von Updates mithilfe der WSUS-Verwaltungskonsole beschrieben.

|Aufgabe|Beschreibung|
|----|--------|
|[3.1. Genehmigen und Bereitstellen von WSUS-Updates](3-approve-and-deploy-updates-in-wsus.md#BKM_3.1.)|Verwenden Sie die WSUS-Verwaltungskonsole zum Genehmigen und Bereitstellen von WSUS-Updates.|
|[3.2. Konfigurieren von Regeln für die automatische Genehmigung](3-approve-and-deploy-updates-in-wsus.md#BKM_3.2.a.)|Konfigurieren Sie WSUS für die automatische Genehmigung der Installation von Updates für ausgewählte Gruppen sowie die Art der Genehmigung von Revisionen für vorhandene Updates.|
|[3.3. Überprüfen von installierten Updates anhand von WSUS-Berichten](3-approve-and-deploy-updates-in-wsus.md#BKM_3.3.)|Verwenden Sie das WSUS-Berichtsfeature zum Überprüfen von installierten Updates, der Computer auf denen sie installiert wurden sowie weiterer Details.|

## <a name="31-approve-and-deploy-wsus-updates"></a><a name=BKM_3.1.></a>3.1. Genehmigen und Bereitstellen von WSUS-Updates
Verwenden Sie das folgende Verfahren, um Updates zu genehmigen und bereitzustellen.

#### <a name="to-approve-and-deploy-wsus-updates"></a>So genehmigen Sie WSUS-Updates und stellen sie bereit

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates**. Im rechten Bereich wird eine Zusammenfassung der Updatestatus für **Alle Updates**, **Wichtige Updates**, **Sicherheitsupdates**und **WSUS-Updates**angezeigt.

2.  Klicken Sie im Bereich **Alle Updates** auf **Für Computer erforderliche Updates**.

3.  Wählen Sie in der Liste mit Updates jene aus, die Sie für die Installation in Ihrer Testcomputergruppe genehmigen möchten. Informationen zu einem ausgewählten Update sind unten im Bereich **Updates** verfügbar. Zum Auswählen mehrerer zusammenhängender Updates hältst du die **UMSCHALTTASTE** gedrückt, während du auf den Updatenamen klickst. Zum Auswählen mehrerer nicht zusammenhängender Updates halten Sie die **STRG** -Taste gedrückt, während Sie auf die Updatenamen klicken.

4.  Klicken Sie mit der rechten Maustaste auf das die ausgewählten Updates, und klicken Sie anschließend auf **Genehmigen**.

5.  Wählen Sie im Dialogfeld **Updates genehmigen** Ihre Testgruppe aus, und klicken Sie dann auf den Pfeil nach unten.

6.  Klicken Sie auf **Für die Installation genehmigt**und anschließend auf **OK**.

7.  Das Fenster **Status der Genehmigung** wird angezeigt. Darin wird der Fortschritt der Aufgaben angezeigt, die sich auf die Updategenehmigung auswirken. Klicken Sie nach Abschluss des Genehmigungsprozesses auf **Schließen**.

## <a name="32-configure-auto-approval-rules"></a><a name=BKM_3.2.a.></a>3.2. Konfigurieren von Regeln für die automatische Genehmigung
Mit automatischen Genehmigungen können Sie angeben, wie die automatische Genehmigung der Installation von Updates für ausgewählte Gruppen erfolgen soll und wie vorhandene Updates genehmigt werden sollen.

#### <a name="to-configure-automatic-approvals"></a>So konfigurieren Sie die automatische Genehmigung

1.  Erweitern Sie in der WSUS-Verwaltungskonsole unter **Update Services**den WSUS-Server, und klicken Sie dann auf **Optionen**. Das Fenster **Optionen** wird geöffnet.

2.  Klicken Sie in **Optionen**auf **Automatische Genehmigungen**. Das Dialogfeld „Automatische Genehmigungen“ wird geöffnet.

3.  Klicken Sie in **Updateregeln**auf **Neue Regel**. Das Dialogfeld **Regel hinzufügen** wird geöffnet.

4.  Wähle unter **Regel hinzufügen** in **Schritt 1: Eigenschaften auswählen** jede einzelne Option oder eine Kombination von Optionen aus den folgenden Möglichkeiten aus:

    -   **Wenn ein Update in einer bestimmten Klassifizierung enthalten ist**

    -   **Wenn ein Update in einem bestimmten Produkt enthalten ist**

    -   **Stichtag für die Genehmigung festlegen**

5.  Klicke in **Schritt 2: Eigenschaften bearbeiten** auf jede der aufgeführten Optionen, und wähle dann jeweils die gewünschten Optionen aus.

6.  Gib in **Schritt 3: Namen angeben** einen Namen für die Regel ein, und klicke dann auf **OK**.

7.  Klicken Sie auf **OK** , um das Dialogfeld „Automatische Genehmigungen“ zu schließen.

## <a name="33-review-installed-updates-with-wsus-reports"></a><a name=BKM_3.3.></a>3.3. Überprüfen von installierten Updates anhand von WSUS-Berichten
24 Stunden nach dem Genehmigen der Updates können Sie mithilfe des WSUS-Berichtsfeatures feststellen, ob die Updates auf den Testgruppencomputern bereitgestellt wurden. Verwenden Sie das WSUS-Berichtsfeature folgendermaßen, um den Status eines Updates zu überprüfen.

#### <a name="to-review-updates"></a>So überprüfen Sie Updates

1.  Klicken Sie im Navigationsbereich der WSUS-Verwaltungskonsole auf **Berichte**.

2.  Klicken Sie auf der Seite mit den **Berichten** auf den Bericht **Updatestatus-Zusammenfassung** . Das Fenster **Updatebericht** wird geöffnet.

3.  Wenn Sie die Updateliste filtern möchten, wählen Sie die zu verwendenden Kriterien aus, z. B. **Updates in folgenden Klassifizierungen einbeziehen**, und klicken Sie anschließend auf **Bericht ausführen**.

4.  Der Bereich **Updatebericht** wird angezeigt. Sie können den Status einzelner Updates überprüfen, indem Sie im linken Abschnitt des Bereichs das gewünschte Update auswählen. Im letzten Abschnitt des Berichtsbereichs wird die Statuszusammenfassung des Updates angezeigt.

5.  Sie können diesen Bericht speichern oder drucken, indem Sie auf der Symbolleiste auf das entsprechende Symbol klicken.

6.  Nach dem Prüfen der Updates können Sie diese für die Installation in den entsprechenden Computergruppen in Ihrer Organisation genehmigen.
