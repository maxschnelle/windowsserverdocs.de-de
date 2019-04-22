---
title: Vorgänge für Updates
description: Windows Server Update Service (WSUS)-Thema - So verwalten Sie Updates, einschließlich des Genehmigungsprozess
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cb7ff54-3014-4e91-842a-a7b831ea59ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d99e006a03e12d7201390748aec8671236cf297
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822551"
---
# <a name="updates-operations"></a>Vorgänge für Updates

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Nachdem die Updates auf dem WSUS-Server synchronisiert wurden, werden sie automatisch Relevanz für das Serverzertifikat-Clientcomputern überprüft werden. Allerdings müssen Sie die Updates genehmigen, bevor sie auf den Computern in Ihrem Netzwerk bereitgestellt werden. Wenn Sie ein Update genehmigen, veranlassen Sie im Wesentlichen, dass WSUS was damit zu tun haben (die Optionen lauten **installieren** oder **ablehnen** für ein neues Update). Sie können Updates für Genehmigen der **alle Computer** Gruppe oder für Untergruppen. Wenn Sie ein Update nicht genehmigt sind, bleibt der Genehmigungsstatus **nicht genehmigt**, und dem WSUS-Server ermöglicht den Clients ausgewertet, und zwar unabhängig davon, ob sie das Update benötigen.

Wenn Ihr WSUS-Server im Replikatmodus ausgeführt wird, werden Sie nicht so genehmigen Sie Updates auf dem WSUS-Server sein. Weitere Informationen zum Replikatmodus finden Sie unter [ausgeführten WSUS Replikatmodus](running-wsus-replica-mode.md).

## <a name="approving-updates"></a>Genehmigen von Updates
Sie können die Installation von Updates für alle Computer in Ihrem WSUS-Netzwerk oder für verschiedene Computergruppen genehmigen. Nach der Genehmigung eines Updates können Sie (mindestens) die folgenden ausführen:

-   Gelten Sie diese Genehmigung für untergeordnete Gruppen, sofern vorhanden.

-   Festlegen Sie Stichtag für die automatische Installation. Wenn Sie diese Option auswählen, legen Sie bestimmte Uhrzeiten und Datumsangaben zum Installieren von Updates, überschreiben alle Einstellungen auf den Clientcomputern. Darüber hinaus können Sie ein Datum in der Vergangenheit für den Stichtag angeben, wenn Sie ein Update sofort (für das nächste Mal erhalten Sie Clientcomputer, auf den WSUS-Server installiert werden) genehmigen möchten.

-   Entfernen eines installierten Updates, wenn dieses Update entfernen unterstützt.

Es gibt zwei wichtige Überlegungen, die Sie bedenken sollten:

-   Sie können nicht zuerst einen Stichtag für die automatische Installation für ein Update festlegen, wenn Benutzereingaben (z. B. die Angabe einer anderen Einstellung für das Update) erforderlich ist. Um zu bestimmen, ob ein Update Benutzereingaben erforderlich ist, sehen Sie sich die **Benutzereingabe anfordern kann** Feld in den Updateeigenschaften für ein Update angezeigt, auf die **aktualisiert** Seite. Überprüfen Sie auch für eine Nachricht in die **Updates genehmigen** Feld, "**das ausgewählte Update erfordert und unterstützt kein Installationszeitlimit**."

-   Wenn Updates der WSUS-Server-Komponente vorhanden sind, können nicht Sie andere Updates an Clientsysteme genehmigen, bis die WSUS-Updates genehmigt wird. Diese Warnmeldung wird im Dialogfeld Updates genehmigen wird angezeigt: "Es gibt WSUS-Updates, die nicht genehmigt wurden. Sie sollten die WSUS-Updates vor genehmigen dieser Updates genehmigen." In diesem Fall sollten Sie auf den WSUS-Updates-Knoten, und stellen Sie sicher, dass alle Updates in dieser Ansicht vor der Rückgabe auf die allgemeine Updates genehmigt wurden.

#### <a name="to-approve-updates"></a>So genehmigen Sie updates

1.  In der WSUS-Verwaltungskonsole, klicken Sie auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates das Update aus, dem Sie verwenden möchten, genehmigen und mit der rechten Maustaste (oder wechseln zu dem Bereich "Aktionen"), und wählen Sie die Computergruppe, für die Sie das Update genehmigen möchten, klicken Sie im Dialogfeld Updates genehmigen, und klicken Sie auf den Pfeil daneben.

3.  Wählen Sie **für die Installation genehmigt**, und klicken Sie dann auf **genehmigen**.

4.  Die **Status der Genehmigung** Fenster wird der Fortschritt beim Abschluss der Genehmigung angezeigt. Wenn der Prozess abgeschlossen ist, ist die **schließen** Schaltfläche angezeigt wird. Klicken Sie auf **Schließen**.

5.  Sie können einen Stichtag auswählen, indem Sie mit der rechten Maustaste in des Updates die entsprechenden Computergruppe auswählen, auf den Pfeil daneben und klicken Sie dann auf **Stichtag**.

    -   Wählen Sie eine von der standard-Terminen (eine Woche, alle zwei Wochen, einen Monat), oder klicken Sie auf **benutzerdefinierte** Datum und Uhrzeit angeben.

    -   Wenn Sie ein Update so schnell wie die Computer Client Verbindung mit dem Server installiert werden soll, klicken Sie auf **benutzerdefinierte**, und legen Sie dann Datum und Uhrzeit für das aktuelle Datum und die Uhrzeit oder eine in der Vergangenheit.

#### <a name="to-approve-multiple-updates"></a>So genehmigen Sie mehrere updates

1.  In der WSUS-Verwaltungskonsole, klicken Sie auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Drücken Sie zum Auswählen mehrerer zusammenhängender Updates **UMSCHALT** beim Auswählen von Updates. Zum Auswählen mehrerer nicht zusammenhängender Updates halten Sie **STRG** beim Auswählen von Updates.

3.  Mit der rechten Maustaste in der Auswahl, und klicken Sie auf **genehmigen**. Die **Updates genehmigen** Dialogfeld wird geöffnet, und die **Genehmigungsstatus** festgelegt **vorhandene Genehmigungen beibehalten** und **OK** Schaltfläche deaktiviert.

4.  Sie können die Genehmigungen für die einzelnen Gruppen ändern, aber dies also keine Auswirkung auf untergeordnete Genehmigungen. Wählen Sie die Gruppe, die für die Sie die Genehmigung ändern möchten, und klicken Sie auf den Pfeil auf der linken Seite. Klicken Sie im Kontextmenü die Option, die auf **für die Installation genehmigt**.

5.  Die Genehmigung für die ausgewählte Gruppe wird nun **installieren**. Wenn alle untergeordneten Gruppen vorhanden sind, bleibt die Genehmigung **vorhandene Genehmigungen beibehalten**. Um die Genehmigung für den untergeordneten Gruppen zu ändern, klicken Sie auf die Gruppe aus, und klicken Sie auf den Pfeil auf der linken Seite. Klicken Sie im Kontextmenü die Option, die auf **anwenden, um untergeordnete Elemente**.

6.  Um einem bestimmten untergeordneten Objekt alle seine Genehmigung vom übergeordneten Element erben festzulegen, klicken Sie auf das untergeordnete Element, und klicken Sie auf den Pfeil auf der linken Seite. Klicken Sie im Kontextmenü die Option, die auf **Auflösungskategorie für übergeordneten**. Wenn Sie Genehmigungen geerbt untergeordnetes Element festgelegt, aber die übergeordneten-Genehmigungen nicht ändern, wird das untergeordnete Element der vorhandenen Genehmigungen des übergeordneten Elements erben.

7.  Wenn Sie das Verhalten der Genehmigung für alle untergeordneten Elemente ändern möchten, zu genehmigen **alle Computer**, und wählen Sie dann **anwenden, um untergeordnete Elemente**.

8.  Klicken Sie auf **OK** nach dem Festlegen aller Ihrer Genehmigungen. Die **Status der Genehmigung** Fenster wird der Fortschritt beim Abschluss der Genehmigung angezeigt. Wenn der Prozess abgeschlossen ist, ist die **schließen** Schaltfläche werden zur Verfügung stehen. Klicken Sie auf **Schließen**.

## <a name="declining-updates"></a>Ablehnen von updates
Wenn Sie diese Option auswählen, das Update wird aus der Standardliste der verfügbaren Updates entfernt, und der WSUS-Server das Update nicht an Clients, die entweder für die Auswertung oder Installation bietet. Sie können diese Option erreichen, wählen Sie ein Update oder eine Gruppe von Updates und mit der rechten Maustaste oder die den Bereich "Aktionen". Abgelehnte Updates werden in der Updateliste angezeigt, nur wenn Sie **abgelehnt** in der Liste Genehmigung, wenn Sie den Filter für die Updateliste unter angeben **Ansicht**.

#### <a name="to-decline-updates"></a>Ablehnen von updates

1.  In der WSUS-Verwaltungskonsole, klicken Sie auf **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates eine oder mehrere Updates, die Sie ablehnen möchten.

3.  Wählen Sie **ablehnen**, und klicken Sie dann auf **Ja** in der bestätigungsmeldung.

## <a name="cleaning-up-declined-updates"></a>Bereinigen von abgelehnten Aktualisierungen
Abgelehnte Updates weiterhin einige WSUS-Server-Ressourcen beanspruchen. Sie sollten die Server-Cleanup-Assistenten zum Entfernen von abgelehnter Aktualisierungen aus der WSUS-Datenbank ausführen. Thema [Die Bereinigung der Server Assistenten](the-server-cleanup-wizard.md), weitere Details.

## <a name="reinstating-declined-updates"></a>Abgelehnte Updates reaktiviert
Nachdem ein Update abgelehnt wurde, können Sie es reaktivieren.

#### <a name="to-reinstate-declined-updates"></a>So reaktivieren Sie abgelehnte Aktualisierungen an

1.  In der WSUS-Verwaltungskonsole, klicken Sie auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Ändern Sie **Genehmigung** zu **abgelehnt** , und klicken Sie auf **aktualisieren**. Die Liste der abgelehnten Updates werden geladen.

3.  Wählen Sie in der Liste der Updates eine oder mehrere abgelehnten Updates, die Sie reaktivieren möchten.

4.  Um ein bestimmtes Update wieder zu aktivieren, mit der rechten Maustaste auf das Update, und wählen **genehmigen**. In der **Updates genehmigen** Dialogfeld klicken Sie auf **OK** den Standardwert "Nicht genehmigt" Genehmigungsstatus erneut anwenden. Das Update wird angezeigt, in der Liste als **nicht genehmigt** statt abgelehnt.

Nach einem abgelehnten Updates bereinigt wurde mit dem WSUS-Server-Cleanup-Assistent, vom WSUS-Server gelöscht werden und wird nicht mehr in der Ansicht alle Updates angezeigt. Sie können abgelehnt, Cleanup-Updates von Microsoft Update-Katalog erneut importieren. Weitere Informationen finden Sie unter [WSUS und Katalog-Website](wsus-and-the-catalog-site.md).

## <a name="change-an-approved-update-to-not-approved"></a>Ändern Sie ein Update genehmigt, die nicht genehmigt
Wenn ein Update genehmigt wurde, und Sie möchten nicht zu diesem Zeitpunkt zu installieren, und stattdessen für einen späteren Zeitpunkt gespeichert werden soll, können Sie das Update auf den Status nicht genehmigt ändern. Dies bedeutet, dass das Update in der Liste der verfügbaren Updates bleibt und -Clientkompatibilität meldet, aber nicht auf Clients installiert.

#### <a name="to-change-an-update-from-approved-to-not-approved"></a>Zum Ändern der ein Update genehmigt ist, nicht genehmigt

1.  In der WSUS-Verwaltungskonsole, klicken Sie auf **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates mindestens eine genehmigte Updates, die nicht genehmigt ändern möchten.

3.  Im Kontextmenü oder die **Aktionen** wählen Sie im Bereich **nicht genehmigt**, und klicken Sie dann auf **Ja** in der bestätigungsmeldung.

## <a name="approving-updates-for-removal"></a>Genehmigen von Updates für die Entfernung
Genehmigen eines Updates für die Entfernung können (d. h. So deinstallieren Sie ein Update bereits installiert). Diese Option steht nur dann, wenn das Update bereits installiert ist, und Entfernen unterstützt. Sie können Geben Sie einen Stichtag für das Update deinstalliert werden, oder geben Sie ein Datum für die Frist in der Vergangenheit aus, wenn das Update sofort (das nächste Mal Clientcomputer, auf den WSUS-Server kontaktieren) entfernt werden soll.

Es ist wichtig zu erwähnen, dass nicht alle Updates entfernen unterstützt. Sehen Sie, ob ein Update zum Entfernen unterstützt, indem ein individuelles Update auswählen, und betrachten die **Details** Bereich. Unter **Detailinformationen**, sehen Sie die **Wechselmedien** Kategorie. Wenn das Update über WSUS nicht entfernt werden kann, in einigen Fällen können Sie es entfernen mit **hinzufügen oder Entfernen von Programmen** aus **Systemsteuerung**.

#### <a name="to-approve-updates-for-removal"></a>So genehmigen Sie Updates für die Entfernung

1.  In der WSUS-Verwaltungskonsole, klicken Sie auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates, die ein oder mehrere Updates, die Sie verwenden möchten, für die Deinstallation genehmigen, und mit der rechten Maustaste sie (oder wechseln Sie zu der **Aktionen** Bereich).

3.  In der **Updates genehmigen** Dialogfeld Wählen Sie die Computergruppe, die von dem das Update entfernt werden sollen, und klicken Sie auf den Pfeil daneben.

4.  Wählen Sie **genehmigt, die zu entfernende**, und klicken Sie dann auf die **entfernen** Schaltfläche.

5.  Nach Abschluss die entfernungsgenehmigung können Sie einen Stichtag auswählen, indem mit der rechten Maustaste erneut auf des Updates, auswählen von der entsprechenden Computergruppe, und klicken Sie dann auf den Pfeil neben. Wählen Sie dann **Stichtag**. Sie können keines der standardmäßigen Termine (eine Woche, alle zwei Wochen, einen Monat) auswählen, oder klicken Sie auf **benutzerdefinierte** um ein bestimmtes Datum und eine Uhrzeit auszuwählen.

6.  Wenn Sie ein Update so schnell wie die Client-Computern wenden Sie sich an den Server entfernt werden möchten, klicken Sie auf **benutzerdefinierte**, und legen Sie ein Datum in der Vergangenheit.

## <a name="approving-updates-automatically"></a>Automatisch genehmigen von Updates
Sie können für die automatische Genehmigung von bestimmte Updates auf dem WSUS-Server konfigurieren. Sie können automatischen Genehmigung von Revisionen für vorhandene Updates auch angeben, sobald diese verfügbar werden. Diese Option ist standardmäßig ausgewählt. Eine Revision ist eine Version eines Updates, die Änderungen vorgenommen wurden (z. B. möglicherweise abgelaufen oder die Anwendbarkeitsregeln möglicherweise geändert haben). Wenn Sie nicht auswählen, die überarbeitete Version eines Updates automatisch zu genehmigen, WSUS wird die ältere Version verwenden und müssen Sie die updaterevision manuell genehmigen.

Sie können Regeln erstellen, die dem WSUS-Server automatisch während der Synchronisierung angewendet werden. Sie angeben, welche Updates, die Sie für die Installation nach updateklassifizierung, nach Produkt und von Computergruppe automatisch genehmigen möchten. Dies gilt nur für neue Updates, im Gegensatz zu überarbeiteten Updates. Sie können auch einen Stichtag für Update-Genehmigung angeben, der festlegt, einer Anzahl von Tagen und eine bestimmte Uhrzeit anbieten, bevor die Genehmigung von Updates Stichtag installiert ist. Diese Einstellungen sind verfügbar, in der **Optionen** Bereich unter **automatische Genehmigungen**.

#### <a name="to-automatically-approve-updates"></a>So genehmigen Sie Aktualisierungen automatisch

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **automatische Genehmigungen**.

2.  Klicken Sie in **Updateregeln** auf **Neue Regel**.

3.  In der **Regel hinzufügen** Dialogfeld unter **Schritt 1: Wählen Sie Eigenschaften**, auswählen, ob der verwenden **Wenn ein Update ist in einer bestimmten Klassifizierung** oder **Wenn ein Update ist in einem bestimmten Produkt** (oder beides) als Kriterium. Wählen Sie optional an, ob **eine Frist setzen** für die Genehmigung.

4.  In **Schritt2: Bearbeiten Sie die Eigenschaften** klicken Sie auf die unterstrichenen Eigenschaften zum Auswählen von Klassifizierungen, Produkte und Computergruppen, die für die automatische Genehmigungen, gegebenenfalls werden sollen. Wählen Sie optional die updategenehmigung am Stichtag, Tag und Uhrzeit.

5.  In **Schritt 3: Geben Sie ein Namensfeld**, geben Sie einen eindeutigen Namen für die Regel.

6.  Klicken Sie auf **OK**.

Regeln für automatische Genehmigungen gelten nicht für Updates erfordern ein End User License Lizenzvertrag (EULA), die noch nicht auf dem Server akzeptiert wurden. Wenn Sie feststellen, dass die Anwendung einer automatische genehmigungsregel nicht alle entsprechenden Updates genehmigt werden kann, sollten Sie diese Updates manuell genehmigen.

## <a name="automatically-approving-revisions-to-updates-and-declining-expired-updates"></a>Änderungen an Updates automatisch zu genehmigen und Ablehnen von abgelaufene Updates
Abschnitt automatische Genehmigungen ein, der den Bereich "Optionen" enthält eine Standardoption, mit der Änderungen an der genehmigten Updates automatisch genehmigt. Sie können auch die abgelaufenen Updates automatisch ablehnen WSUS-Server festlegen. Wenn Sie nicht die überarbeitete Version eines Updates automatisch genehmigt, Ihr WSUS-Server wird die ältere Version verwenden, und müssen Sie die updaterevision manuell genehmigen.

> [!NOTE]
> Eine Revision ist eine Version eines Updates, die geändert wurde (z. B. es möglicherweise abgelaufen oder wurden aktualisiert, Anwendbarkeitsregeln).

#### <a name="to-automatically-approve-revisions-to-updates-and-decline-expired-updates"></a>Automatisch Änderungen an Updates genehmigen und Ablehnen abgelaufene updates

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **automatische Genehmigungen**.

2.  Auf der **erweitert** Registerkarte, stellen Sie sicher, dass beide **automatisch neue Revisionen genehmigter Updates genehmigen** und **automatisch ablehnen von Updates, wenn eine neue Revision bewirkt, dass sieabläuft** ausgewählt sind.

3.  Klicken Sie auf „OK“.

    > [!NOTE]
    > Halten die Standardwerte für diese Optionen können, dass Sie eine guten Leistung auf Ihrem WSUS-Netzwerks beibehalten. Wenn Sie nicht möchten, dass abgelaufene Updates automatisch abgelehnt wird, sollten Sie sicherstellen, um sie manuell in regelmäßigen Abständen abzulehnen.

## <a name="automatically-declining-superseded-updates"></a>Automatisch ablehnen Ersetzte Updates
Wenn Sie ein neues Update, das ein vorhandenes Update ersetzt, die automatisch genehmigt wird genehmigen, wird das ersetzte Update "Nicht zutreffend" auf einem Computer oder Gerät nach der Installation des neueren Updates. Sie können in der WSUS-Konsole überprüfen, ob ein Update für alle Computer nicht verfügbar ist. Wenn dies der Fall ist, kann das Update problemlos abgelehnt werden. Darüber hinaus kann das Update automatisch abgelehnt werden, beim Ausführen des Assistenten für der WSUS-Server-Bereinigung.

Um nach ersetzten Updates zu suchen, können Sie die Spalte "Abgelöst" zur Kennzeichnung in der Ansicht alle Updates, und die Sortierreihenfolge für die betreffende Spalte auswählen. Es werden vier Gruppen:

-   Updates, die nie wurden ersetzt (ein leeres Symbol).

-   Updates der ersetzt, sondern können unter keinen Umständen ersetzt ein anderes Update (ein Symbol mit einem blauen Quadrat im unteren Bereich).

-   Updates, die ersetzt und haben ein anderes Update (ein Symbol mit einem blauen Quadrat in der Mitte) ersetzt.

-   Updates, bei die ein anderes Update (ein Symbol mit einem blauen Quadrat am oberen) ersetzt haben.

Es ist kein Feature in Windows Server Update Services, dass automatisch ablehnungen Updates nach Genehmigung eines neueren Updates abgelöst. Es wird empfohlen, zuerst die Genehmigung auf "Nicht genehmigt" festgelegt, und klicken Sie dann mithilfe von Server Cleanup Assistenten automatisch das Update ablehnen, wenn alle relevanten Bedingungen erfüllt sind. Weitere Informationen finden Sie in den folgenden Themen: [Die Bereinigung der Server Assistenten](the-server-cleanup-wizard.md).

## <a name="approving-superseding-or-superseded-updates"></a>Ersetzen genehmigen oder Ersetzte Updates
In der Regel führt ein Update, das andere Updates hat Vorrang vor, eine oder mehrere der folgenden:

-   Erweiterung, Verbesserung oder Ergänzung der Korrekturen, die von früher herausgegebenen Updates bereitgestellt wurden

-   Steigerung der Effizienz des Updatedateipakets, das auf Clientcomputern installiert wird, sofern die Installation des Updates genehmigt wird. Beispielsweise könnte das abgelöste Update Dateien enthalten, die für die Korrektur oder die jetzt vom neuen Update unterstützten Betriebssysteme nicht mehr relevant sind. Diese Dateien sind dann im Dateipaket des abgelösten Updates nicht enthalten.

-   Updates für neuere Betriebssysteme. Es ist auch wichtig zu beachten, dass das ersetzende Update möglicherweise nicht mit frühere Versionen von Betriebssystemen unterstützt.

Umgekehrt erfüllt ein Update, das durch ein anderes Update abgelöst wurde Folgendes:

-   Behebt das Problem ähnelt der von dem Update, das vor ihm Vorrang hat. Allerdings kann das Update, das vor ihm Vorrang hat das Update zu verbessern, das das nachrangige Update bereitstellt.

-   Aktualisiert frühere Versionen der Betriebssysteme. In einigen Fällen sind diese Versionen von Betriebssystemen durch das ersetzende Update nicht mehr aktualisiert.

Im Detailbereich für ein individuelles Update anzeigt ein Informationssymbol eine Nachricht am Anfang, dass sie ersetzt oder durch ein anderes Update abgelöst wird. Darüber hinaus können Sie bestimmen, welche Updates abgelöst oder durch das Update ersetzt werden, die anhand der **Updates, die dieses Update ersetzen** und **Updates, die durch dieses Update ersetzt** Einträge in der **Detailinformationen** Teil der **Eigenschaften**. Detailbereich des Updates wird unter der Liste der Updates angezeigt.

WSUS erfasst nicht automatisch lehnt ersetzte Updates, und es wird empfohlen, dass Sie nicht annehmen, dass nachrangige Updates zugunsten eines neuen, vorrangigen Updates abgelehnt werden sollte. Stellen Sie bevor Sie ein nachrangiges Updates ablehnen sicher, dass es von einem Ihrer Clientcomputer nicht mehr benötigt wird. Es folgen Beispiele für Szenarien, in denen Sie möglicherweise ein nachrangiges Update installieren müssen:

-   Wenn ein ersetzendes Update nur neuere Versionen eines Betriebssystems unterstützt aus, und einige Ihrer Clientcomputer frühere Versionen des Betriebssystems ausgeführt werden.

-   Wenn ein vorrangiges Update Anwendbarkeit des Updates ist stärker als eingeschränkt abzulösenden Softwareupdates, die wäre dadurch für einige Clientcomputer ungeeignet.

-   Wenn ein Update aufgrund neuer Änderungen nicht mehr ein vorher veröffentlichtes Update ersetzt. Es ist möglich, dass durch Änderungen mit jeder neuen Version, ein Update nicht mehr ein Update ersetzt, die sie zuvor in einer früheren Version ersetzt. In diesem Szenario noch sehen eine Nachricht zu dem ersetzten Update, Sie auch, wenn das ersetzende Update durch ein Update ersetzt wurde, die nicht der Fall ist.


