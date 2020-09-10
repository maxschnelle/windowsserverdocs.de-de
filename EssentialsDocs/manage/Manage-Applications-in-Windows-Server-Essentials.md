---
title: Verwalten von Anwendungen in Windows Server 2012 Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: ae89c46a-0afd-4858-9150-ec97650f45a4
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 30b8dfa2087e76cc80011eb359715c95564ec1b6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623276"
---
# <a name="manage-applications-in-windows-server-essentials"></a>Verwalten von Anwendungen in Windows Server 2012 Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Das Server-Dashboard in Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle ermöglicht das Ausführen allgemeiner administrativer Aufgaben. Weitere Informationen zum Durchführen dieser Aufgaben finden Sie unter:

-   [Anwendungsverwaltungsaufgaben im Dashboard](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_1)

-   [Installieren und Entfernen von Add-Ins mithilfe des Dashboards](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_2)

##  <a name="application-management-tasks-in-the-dashboard"></a><a name="BKMK_1"></a> Anwendungs Verwaltungsaufgaben im Dashboard
 Die Verwaltungsseite **Anwendungen** im Dashboard bietet Folgendes:

- Eine Liste der installierten Add-Ins, wobei Folgendes angezeigt wird:

  -   Der Name des Onlinedienstes oder des Add-Ins

  -   Der Aktualisierungsstatus des Add-Ins

  -   Der Abonnementstatus des Add-Ins

  -   Der Name des Unternehmens oder des Herausgebers, der das Add-In zur Verfügung stellt

- Ein Aufgabenbereich, der eine Reihe von Aufgaben für die Verwaltung eines ausgewählten Add-Ins enthält

- Eine Liste von Add-Ins, die zum Herunterladen und Installieren von Microsoft Pinpoint verfügbar sind

  Die folgende Tabelle beschreibt die verschiedenen Add-In-Verwaltungsaufgaben, die im Server-Dashboard verfügbar sind. Einige Aufgaben sind Add-In-spezifisch, sodass sie nur angezeigt werden, wenn Sie ein Add-In in der Liste auswählen.

|Aufgabenname|BESCHREIBUNG|
|---------------|-----------------|
|Add-In entfernen|Entfernt das ausgewählte Add-In vom Server und von allen anderen Computern im Netzwerk.|
|Add-In auf Netzwerkcomputern installieren|Hilft Ihnen bei der Planung der Installation der ausgewählten Add-Ins auf allen anderen Computern im Netzwerk.|
|Hilfe zum Add-In abrufen|Öffnet eine Website im Internetbrowser, auf der Sie nach Lösungen für Probleme suchen können und die weitere Informationen zu einem ausgewählten Add-In enthält.|
|Add-In aktualisieren|Hilft Ihnen dabei, Updates für die Add-Ins, die auf dem Server und den Computern im Netzwerk installiert sind, herunterzuladen und zu installieren.|
|Abonnement für das Add-In verlängern|Öffnet eine Website im Internetbrowser, über die Sie das Add-In-Abonnement erneuern können.|
|Datenschutzbestimmungen für das Add-In lesen|Öffnet eine Website im Internetbrowser, auf der Sie die Datenschutzbestimmungen anzeigen können.|
|Wie werden Add-Ins installiert oder entfernt?|Öffnet eine Website im Internetbrowser mit Hilfethemen.|

##  <a name="install-or-remove-add-ins-using-the-dashboard"></a><a name="BKMK_2"></a> Installieren oder Entfernen von Add-Ins mithilfe des Dashboards
 Ein Add-In ist eine Softwareanwendung, die zusätzliche Funktionen für den Server bereitstellt. Eine wachsende Zahl von Add-Ins wird von Microsoft und anderen unabhängigen Softwareanbietern (ISVs) zur Verfügung gestellt.

 Bevor Sie die erweiterten Funktionen nutzen können, die ein Add-In Ihnen bietet, müssen Sie zuerst das Add-In auf dem Server installieren.

#### <a name="to-install-an-add-in-from-microsoft-pinpoint"></a>So installieren Sie ein Add-In von Microsoft Pinpoint

1.  Klicken Sie im Server Dashboard auf **Anwendungen**, und klicken Sie dann auf die Registerkarte **Microsoft PinPoint** .  Eine Liste der verfügbaren Add-Ins wird angezeigt.

2.  Klicken Sie auf das Add-In, das Sie installieren möchten. Die Seite mit Add-In-Informationen wird angezeigt.

3.  Klicken Sie auf der Add-In-Informationsseite auf "Herunterladen", und befolgen Sie die Anweisungen auf dem Bildschirm zum Herunterladen und Installieren des Add-Ins.

4.  Befolgen Sie die Anweisungen im Assistenten, um das Add-In zu installieren.

5.  Wenn die Installation abgeschlossen ist, starten Sie das Dashboard neu, öffnen Sie die Seite **Anwendungen** im Server-Dashboard, und stellen Sie sicher, dass das Add-In in der Liste angezeigt wird.

#### <a name="to-install-an-add-in-from-another-provider"></a>So installieren Sie ein Add-In von einem anderen Anbieter

1.  Öffnen Sie den Windows Explorer, und navigieren Sie zum Speicherort der Add-In-Installationsdatei.

2.  Doppelklicken Sie auf die Datei, um den Installationsassistenten auszuführen.

3.  Befolgen Sie die Anweisungen im Assistenten, um das Add-In zu installieren.

4.  Wenn die Installation abgeschlossen ist, starten Sie das Dashboard neu, öffnen Sie die Seite **Anwendungen**, und stellen Sie sicher, dass das Add-In in der Liste angezeigt wird.

#### <a name="to-remove-an-add-in"></a>So entfernen Sie ein Add-In

1.  Öffnen Sie das Server-Dashboard.

2.  Klicken Sie auf die Registerkarte **Anwendungen**.

3.  Wählen Sie auf der Registerkarte **Add-Ins** das Add-In aus, das Sie entfernen möchten, und klicken Sie dann auf **Add-In entfernen**.

4.  Klicken Sie im Fenster **Add-In entfernen** auf **Entfernen**.

    > [!NOTE]
    >  Möglicherweise müssen Sie das Dashboard neu starten, um das Add-In vollständig zu entfernen.

## <a name="additional-references"></a>Weitere Verweise

-   [Übersicht über das Dashboard](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
