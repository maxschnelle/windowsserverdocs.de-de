---
title: Vorgänge für Updates
description: 'Windows Server Update Service (WSUS)-Thema: Verwalten von Updates, einschließlich des Genehmigungsprozesses'
ms.topic: article
ms.assetid: 4cb7ff54-3014-4e91-842a-a7b831ea59ff
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f4ce19a8cfcfdb427cb332daf95b43feb157abba
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624319"
---
# <a name="updates-operations"></a>Vorgänge für Updates

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Updates mit dem WSUS-Server synchronisiert wurden, werden Sie automatisch auf die für die Client Computer des Servers relevanten Kriterien überprüft. Sie müssen jedoch die Updates genehmigen, bevor Sie auf den Computern in Ihrem Netzwerk bereitgestellt werden. Wenn Sie ein Update genehmigen, weisen Sie WSUS im Grunde zu, was damit zu tun ist (Ihre Auswahl ist für ein neues Update " **install** " oder " **ablehnen** "). Sie können Updates für die Gruppe **alle Computer** oder für Untergruppen genehmigen. Wenn Sie ein Update nicht genehmigen, wird der Genehmigungs Status **nicht genehmigt**angezeigt, und der WSUS-Server ermöglicht Clients, zu prüfen, ob das Update benötigt wird.

Wenn Ihr WSUS-Server im Replikat Modus ausgeführt wird, können Sie keine Updates auf dem WSUS-Server genehmigen. Weitere Informationen zum Replikat Modus finden Sie unter [Ausführen des WSUS-Replikat Modus](running-wsus-replica-mode.md).

## <a name="approving-updates"></a>Genehmigen von Updates
Sie können die Installation von Updates für alle Computer in Ihrem WSUS-Netzwerk oder für verschiedene Computer Gruppen genehmigen. Nach der Genehmigung eines Updates können Sie eine oder mehrere der folgenden Aktionen ausführen:

-   Wenden Sie diese Genehmigung ggf. auf untergeordnete Gruppen an.

-   Legen Sie einen Stichtag für die automatische Installation fest. Wenn Sie diese Option auswählen, legen Sie bestimmte Uhrzeiten und Datumsangaben fest, um Updates zu installieren, und überschreiben alle Einstellungen auf den Client Computern. Außerdem können Sie ein letztes Datum für den Stichtag angeben, wenn Sie ein Update sofort genehmigen möchten (das installiert werden soll, wenn Client Computer das nächste Mal mit dem WSUS-Server in Verbindung treten).

-   Entfernt ein installiertes Update, wenn dieses Update das Entfernen unterstützt.

Es gibt zwei wichtige Überlegungen, die Sie beachten sollten:

-   Erstens können Sie keinen Stichtag für die automatische Installation eines Updates festlegen, wenn eine Benutzereingabe erforderlich ist (z. b. die Angabe einer für das Update relevanten Einstellung). Um zu ermitteln, ob ein Update Benutzereingaben erfordert, sehen Sie sich das Feld **möglicherweise Benutzereingabe anfordern** in den Update Eigenschaften für ein Update an, das auf der Seite **Updates** angezeigt wird. Überprüfen Sie im Feld **Updates genehmigen** auch, ob für **das ausgewählte Update Benutzereingaben erforderlich sind und ein Installations Stichtag nicht unterstützt**wird.

-   Wenn Updates für die WSUS-Serverkomponente vorliegen, können Sie andere Updates für Client Systeme erst genehmigen, wenn das WSUS-Update genehmigt wurde. Diese Warnmeldung wird im Dialogfeld "Updates genehmigen" angezeigt: Es sind WSUS-Updates vorhanden, die nicht genehmigt wurden. Sie sollten die WSUS-Updates genehmigen, bevor Sie dieses Update genehmigen. In diesem Fall sollten Sie auf den Knoten WSUS-Updates klicken und sicherstellen, dass alle Updates in dieser Ansicht vor der Rückkehr zu den allgemeinen Updates genehmigt wurden.

#### <a name="to-approve-updates"></a>So genehmigen Sie Updates

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates das Update aus, das Sie genehmigen möchten, und klicken Sie mit der rechten Maustaste (oder wechseln Sie zum Bereich Aktionen). Wählen Sie dann im Dialogfeld Updates genehmigen die Computergruppe aus, für die Sie das Update genehmigen möchten, und klicken Sie auf den Pfeil daneben.

3.  Wählen Sie **für die Installation genehmigt aus**, und klicken Sie dann auf **genehmigen**.

4.  Im Fenster **Genehmigungs** Status wird der Fortschritt im Hinblick auf das Abschließen der Genehmigung angezeigt. Wenn der Prozess abgeschlossen ist, wird die Schaltfläche **Schließen** angezeigt. Klicken Sie auf **Schließen**.

5.  Wenn Sie einen Stichtag auswählen, klicken Sie mit der rechten Maustaste auf das Update, wählen Sie die entsprechende Computergruppe aus, klicken Sie auf den Pfeil daneben, und klicken Sie dann auf **Stichtag**.

    -   Sie können einen der Standard Termine (eine Woche, zwei Wochen, einen Monat) auswählen, oder Sie können auf **Benutzer** definiert klicken, um ein Datum und eine Uhrzeit anzugeben.

    -   Wenn Sie ein Update installieren möchten, sobald die Client Computer mit dem Server in Kontakt treten, klicken Sie auf **Benutzer**definiert, und legen Sie dann ein Datum und eine Uhrzeit auf das aktuelle Datum und die Uhrzeit bzw. auf das aktuelle Datum fest.

#### <a name="to-approve-multiple-updates"></a>So genehmigen Sie mehrere Updates

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Zum Auswählen mehrerer zusammenhängender Updates drücken Sie während der Auswahl von Updates die **UMSCHALT** Taste. Zum Auswählen mehrerer nicht zusammenhängender Updates halten Sie die **STRG** -Taste gedrückt, während Sie Updates auswählen.

3.  Klicken Sie mit der rechten Maustaste auf die Auswahl und dann auf **genehmigen**. Das Dialogfeld **Updates genehmigen** wird geöffnet, und der **Genehmigungs Status** ist auf **vorhandene Genehmigungen beibehalten** und die Schaltfläche **OK** deaktiviert.

4.  Sie können die Genehmigungen für die einzelnen Gruppen ändern, dies wirkt sich jedoch nicht auf die untergeordneten Genehmigungen aus. Wählen Sie die Gruppe aus, für die Sie die Genehmigung ändern möchten, und klicken Sie auf den Pfeil auf der linken Seite. Klicken Sie im Kontextmenü auf **für die Installation genehmigt**.

5.  Die Genehmigung für die ausgewählte Gruppe wird in **install**geändert. Wenn untergeordnete Gruppen vorhanden sind, bleibt die Genehmigung weiterhin **bestehen**. Um die Genehmigung für die untergeordneten Gruppen zu ändern, klicken Sie auf die Gruppe, und klicken Sie auf den Pfeil auf der linken Seite. Klicken Sie im Kontextmenü **auf auf auf unter**geordnete Elemente anwenden.

6.  Klicken Sie auf das untergeordnete Element, und klicken Sie auf den Pfeil auf der linken Seite, um ein bestimmtes untergeordnetes Element festzulegen Klicken Sie im Kontextmenü auf **identisch als übergeordnetes**Element. Wenn Sie ein untergeordnetes Element für das Erben von Genehmigungen festlegen, aber die übergeordneten Genehmigungen nicht ändern, erbt das untergeordnete Objekt die vorhandenen Genehmigungen des übergeordneten Elements.

7.  Wenn Sie das Genehmigungs Verhalten für alle untergeordneten Elemente ändern möchten, genehmigen Sie **alle Computer**, und wählen Sie dann **auf unter**geordnete Elemente anwenden aus.

8.  Klicken Sie auf **OK** , nachdem Sie alle Genehmigungen eingerichtet haben. Im Fenster **Genehmigungs** Status wird der Fortschritt im Hinblick auf das Abschließen der Genehmigung angezeigt. Wenn der Prozess abgeschlossen ist, ist die Schaltfläche **Schließen** verfügbar. Klicken Sie auf **Schließen**.

## <a name="declining-updates"></a>Abnehmende Updates
Wenn Sie diese Option auswählen, wird das Update aus der Standardliste der verfügbaren Updates entfernt, und der WSUS-Server bietet das Update für Clients weder für die Evaluierung noch für die Installation. Sie können diese Option erreichen, indem Sie ein Update oder eine Gruppe von Updates auswählen und mit der rechten Maustaste klicken oder zum Bereich Aktionen wechseln. Abgelehnte Updates werden nur dann in der Liste Updates angezeigt, wenn Sie in der Liste Genehmigung die Option **abgelehnt** ausgewählt haben, wenn Sie den Filter für die Update Liste unter **Ansicht**angeben.

#### <a name="to-decline-updates"></a>Ablehnen von Updates

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates mindestens ein Update aus, das Sie ablehnen möchten.

3.  Wählen Sie **ablehnen**aus, und klicken Sie dann in der Bestätigungsmeldung auf **Ja** .

## <a name="cleaning-up-declined-updates"></a>Bereinigen abgelehnter Updates
Abgelehnte Updates verbrauchen weiterhin einige WSUS-Server Ressourcen. Sie sollten den Server Bereinigungs-Assistenten ausführen, um Abgelehnte Updates aus der WSUS-Datenbank zu entfernen. Weitere Informationen finden Sie [unter dem Server Bereinigungs-Assistenten](the-server-cleanup-wizard.md).

## <a name="reinstating-declined-updates"></a>Abgelehnte Updates werden erneut eingefügt.
Nachdem ein Update abgelehnt wurde, können Sie es weiterhin wiederherstellen.

#### <a name="to-reinstate-declined-updates"></a>So setzen Sie Abgelehnte Updates wieder

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Ändern Sie **Genehmigung** in **abgelehnt** , und klicken Sie auf **Aktualisieren**. Die Liste der abgelehnten Updates wird geladen.

3.  Wählen Sie in der Liste der Updates mindestens ein abgelehnten Update aus, das Sie wiederherstellen möchten.

4.  Klicken Sie zum Wiederherstellen eines bestimmten Updates mit der rechten Maustaste auf das Update, und wählen Sie **genehmigen**aus. Klicken Sie im Dialogfeld **Updates genehmigen** auf **OK** , um den Standardstatus nicht genehmigte Genehmigung erneut anzuwenden. Das Update wird in der Liste als **nicht genehmigt** , sondern nicht als abgelehnt angezeigt.

Nachdem ein abgelehntes Update mit dem WSUS-Server Bereinigungs-Assistenten bereinigt wurde, wird es auf dem WSUS-Server gelöscht und in der Ansicht alle Updates nicht mehr angezeigt. Sie können abgelehnte, bereinigte Updates aus dem Microsoft Update Katalog neu importieren. Weitere Informationen finden Sie unter [WSUS und die-Katalog Website](wsus-and-the-catalog-site.md).

## <a name="change-an-approved-update-to-not-approved"></a>Ändern eines genehmigten Updates in "nicht genehmigt"
Wenn ein Update genehmigt wurde und Sie es nicht zu diesem Zeitpunkt installieren möchten, sondern es für einen späteren Zeitpunkt speichern möchten, können Sie das Update in den Status nicht genehmigt ändern. Dies bedeutet, dass das Update in der Standardliste der verfügbaren Updates verbleibt und die Client Konformität meldet, aber nicht auf Clients installiert wird.

#### <a name="to-change-an-update-from-approved-to-not-approved"></a>So ändern Sie ein Update von "genehmigt" in "nicht genehmigt"

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates mindestens ein genehmigtes Update aus, das Sie in nicht genehmigt ändern möchten.

3.  Wählen Sie im Kontextmenü oder im Bereich **Aktionen** die Option **nicht genehmigt**aus, und klicken Sie dann in der Bestätigungsmeldung auf **Ja** .

## <a name="approving-updates-for-removal"></a>Genehmigen von Updates zum Entfernen
Sie können ein Update zum Entfernen genehmigen (d. h., ein bereits installiertes Update zu deinstallieren). Diese Option ist nur verfügbar, wenn das Update bereits installiert ist und das Entfernen unterstützt. Sie können einen Stichtag für die Installation des Updates angeben, oder Sie können ein letztes Datum für den Stichtag angeben, wenn Sie das Update sofort entfernen möchten (wenn Client Computer das nächste Mal mit dem WSUS-Server in Verbindung treten).

Es ist wichtig zu erwähnen, dass nicht alle Updates entfernt werden. Sie können sehen, ob ein Update das Entfernen unterstützt, indem Sie ein einzelnes Update auswählen und sich im **Detail** Bereich ansehen. Unter **Weitere Details** **wird die Wechsel** Kategorie angezeigt. Wenn das Update nicht durch WSUS entfernt werden kann, kann es in einigen Fällen **mithilfe der Option** Software in der **Systemsteuerung**entfernt werden.

#### <a name="to-approve-updates-for-removal"></a>So genehmigen Sie Updates zum Entfernen

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates** , und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie in der Liste der Updates mindestens ein Update aus, das Sie zum Entfernen genehmigen möchten, und klicken Sie mit der rechten Maustaste darauf (oder wechseln Sie zum **Aktions** Bereich).

3.  Wählen Sie im Dialogfeld **Updates genehmigen** die Computergruppe aus, von der Sie das Update entfernen möchten, und klicken Sie auf den Pfeil daneben.

4.  Wählen Sie **genehmigte zum Entfernen aus**, und klicken Sie dann auf die Schaltfläche **Entfernen** .

5.  Nachdem die Genehmigung entfernen abgeschlossen ist, können Sie einen Stichtag auswählen, indem Sie mit der rechten Maustaste auf das Update klicken, die entsprechende Computergruppe auswählen und dann auf den Pfeil daneben klicken. Wählen Sie dann **Stichtag**aus. Sie können einen der Standard Termine (eine Woche, zwei Wochen, einen Monat) auswählen, oder Sie können auf **Benutzer** definiert klicken, um ein bestimmtes Datum und eine bestimmte Uhrzeit auszuwählen.

6.  Wenn Sie ein Update entfernen möchten, sobald die Client Computer den Server kontaktieren, klicken Sie auf **Benutzer**definiert, und legen Sie ein Datum in der Vergangenheit fest.

## <a name="approving-updates-automatically"></a>Automatisches genehmigen von Updates
Sie können den WSUS-Server für die automatische Genehmigung bestimmter Updates konfigurieren. Sie können auch die automatische Genehmigung von Revisionen vorhandener Updates angeben, sobald diese verfügbar sind. Diese Option ist standardmäßig ausgewählt. Eine Revision ist eine Version eines Updates, bei der Änderungen vorgenommen wurden (z. b. Wenn Sie abgelaufen ist oder die anwendbarkeits Regeln geändert wurden). Wenn Sie die überarbeitete Version eines Updates nicht automatisch genehmigen, wird die ältere Version von WSUS verwendet, und Sie müssen die Update Revision manuell genehmigen.

Sie können Regeln erstellen, die auf dem WSUS-Server automatisch während der Synchronisierung angewendet werden. Sie geben an, welche Updates Sie automatisch für die Installation genehmigen möchten, indem Sie die Update Klassifizierung, das Produkt und die Computergruppe durchsuchen. Dies gilt nur für neue Updates und nicht für überarbeitete Updates. Sie können auch einen Stichtag für die Genehmigung von Updates angeben, mit dem eine Anzahl von Tagen und eine bestimmte Zeitspanne festgelegt wird, bevor das genehmigte Update Stichtag installiert wird. Diese Einstellungen sind im Bereich **Optionen** unter **Automatische Genehmigungen**verfügbar.

#### <a name="to-automatically-approve-updates"></a>So genehmigen Sie Updates automatisch

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**und dann auf **Automatische Genehmigungen**.

2.  Klicken Sie in **Updateregeln**auf **Neue Regel**.

3.  Wählen Sie im Dialogfeld **Regel hinzufügen** unter **Schritt 1: Eigenschaften auswählen**aus, ob verwendet werden soll, **Wenn ein Update in einer bestimmten Klassifizierung** oder ein **Update in einem bestimmten Produkt** (oder beiden) als Kriterium verwendet wird. Wählen Sie optional aus, ob Sie **einen Stichtag** für die Genehmigung festlegen möchten.

4.  Klicken Sie in **Schritt 2: Bearbeiten der Eigenschaften** auf die unterstrichenen Eigenschaften, um die Klassifizierungen, Produkte und Computer Gruppen auszuwählen, für die Sie ggf. automatische Genehmigungen benötigen. Wählen Sie optional den Tag und die Uhrzeit der Update Genehmigung aus.

5.  Geben Sie in **Schritt 3: Geben Sie einen Namen**ein den eindeutigen Namen für die Regel ein.

6.  Klicken Sie auf **OK**.

Regeln für automatische Genehmigungen gelten nicht für Updates, für die ein Endbenutzer-Lizenzvertrag (EULA) erforderlich ist, der auf dem Server noch nicht akzeptiert wurde. Wenn Sie feststellen, dass das Anwenden einer automatischen Genehmigungs Regel nicht dazu führt, dass alle relevanten Updates genehmigt werden, sollten Sie diese Updates manuell genehmigen.

## <a name="automatically-approving-revisions-to-updates-and-declining-expired-updates"></a>Automatisches genehmigen von Revisionen von Updates und abnehmenden abgelaufenen Updates
Der Abschnitt Automatische Genehmigungen des Bereichs Optionen enthält eine Standardoption zum automatischen genehmigen von Revisionen genehmigter Updates. Sie können auch festlegen, dass der WSUS-Server abgelaufene Updates automatisch ablehnen soll. Wenn Sie die überarbeitete Version eines Updates nicht automatisch genehmigen möchten, wird auf dem WSUS-Server die ältere Revision verwendet, und Sie müssen die Update Revision manuell genehmigen.

> [!NOTE]
> Eine Revision ist eine Version eines Updates, die geändert wurde (z. b. ob Sie abgelaufen ist oder über aktualisierte anwendbarkeits Regeln verfügt).

#### <a name="to-automatically-approve-revisions-to-updates-and-decline-expired-updates"></a>So genehmigen Sie Aktualisierungen von Updates automatisch und lehnen abgelaufene Updates ab

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**und dann auf **Automatische Genehmigungen**.

2.  Vergewissern Sie sich, dass auf der Registerkarte **erweitert** sowohl **neue Revisionen genehmigter Updates automatisch genehmigen** als auch **Updates automatisch ablehnen, wenn eine neue Revision das ablaufen** der Änderungen bewirkt.

3.  Klicken Sie auf OK.

    > [!NOTE]
    > Wenn Sie die Standardwerte für diese Optionen behalten, können Sie eine gute Leistung in Ihrem WSUS-Netzwerk gewährleisten. Wenn Sie nicht möchten, dass abgelaufene Updates automatisch abgelehnt werden, sollten Sie Sie in regelmäßigen Abständen manuell ablehnen.

## <a name="automatically-declining-superseded-updates"></a>Automatisch abnehmende abgelösten Updates
Wenn Sie ein neues Update genehmigen, das ein vorhandenes Update ersetzt, das automatisch genehmigt wird, gilt das ersetzte Update nicht mehr für einen Computer oder ein Gerät, sobald das neuere Update installiert wurde. Sie können in der WSUS-Konsole überprüfen, ob ein Update für alle Computer nicht anwendbar ist. Wenn dies der Fall ist, kann das Update sicher abgelehnt werden. Außerdem wird das Update möglicherweise automatisch abgelehnt, wenn Sie den WSUS-Server Bereinigungs-Assistenten ausführen.

Wenn Sie nach abgelösten Updates suchen möchten, können Sie die Spalte "abgelösten Flag" in der Ansicht "alle Updates" auswählen und nach dieser Spalte sortieren. Es gibt vier Gruppen:

-   Updates, die noch nie abgelöst wurden (ein leeres Symbol).

-   Updates, die abgelöst wurden, aber noch nie ein anderes Update abgelöst haben (ein Symbol mit einem blauen Quadrat unten).

-   Updates, die abgelöst wurden und ein anderes Update abgelöst haben (ein Symbol mit einem blauen Quadrat in der Mitte).

-   Updates, die ein anderes Update abgelöst haben (ein Symbol mit einem blauen Quadrat oben).

Es gibt keine Funktion in Windows Server Update Services, die bei der Genehmigung eines neueren Updates automatisch ersetzte Updates ablehnt. Es wird empfohlen, zuerst die Genehmigung auf "nicht genehmigt" festzulegen und dann mit dem Assistenten für die Server Bereinigung das Update automatisch abzulehnen, wenn alle relevanten Bedingungen erfüllt sind. Weitere Informationen finden Sie unter [dem Server Bereinigungs-Assistenten](the-server-cleanup-wizard.md).

## <a name="approving-superseding-or-superseded-updates"></a>Genehmigen von ersetzenden oder abgelösten Updates
In der Regel führt ein Update, das andere Updates ersetzt, eine oder mehrere der folgenden Aktionen aus:

-   Erweiterung, Verbesserung oder Ergänzung der Korrekturen, die von früher herausgegebenen Updates bereitgestellt wurden

-   Steigerung der Effizienz des Updatedateipakets, das auf Clientcomputern installiert wird, sofern die Installation des Updates genehmigt wird. Beispielsweise könnte das abgelöste Update Dateien enthalten, die für die Korrektur oder die jetzt vom neuen Update unterstützten Betriebssysteme nicht mehr relevant sind. Diese Dateien sind dann im Dateipaket des abgelösten Updates nicht enthalten.

-   Aktualisiert neuere Versionen von Betriebssystemen. Es ist auch wichtig zu beachten, dass das ersetzende Update möglicherweise keine früheren Versionen von Betriebssystemen unterstützt.

Umgekehrt führt ein Update, das durch ein anderes Update abgelöst wird, Folgendes aus:

-   Korrigiert eines Problems ähnlich dem des Updates, das es ersetzt. Das Update, durch das es ersetzt wird, kann jedoch die Behebung verbessern, die das ersetzte Update bereitstellt.

-   Aktualisiert frühere Versionen von Betriebssystemen. In einigen Fällen werden diese Versionen von Betriebssystemen nicht mehr durch das ersetzende Update aktualisiert.

Im Detailbereich eines einzelnen Updates weist ein Informationssymbol und eine Meldung oben darauf hin, dass es entweder ersetzt oder durch ein anderes Update abgelöst wird. Außerdem können Sie ermitteln, welche Updates durch das Update abgelöst oder ersetzt werden, indem Sie sich die Updates, die **dieses Update** ersetzen, und die Updates, die **durch diese Update Einträge ersetzt** wurden, im Abschnitt **zusätzliche Details** der **Eigenschaften**ansehen. Der Detailbereich eines Updates wird unterhalb der Liste der Updates angezeigt.

WSUS lehnt ersetzte Updates nicht automatisch ab, und es wird empfohlen, dass Sie nicht davon ausgehen, dass abgelösten Updates zugunsten des neuen, ersetzenden Updates abgelehnt werden sollen. Stellen Sie vor dem ablehnen eines abgelösten Updates sicher, dass es von keinem Ihrer Client Computer mehr benötigt wird. Im folgenden finden Sie Beispiele für Szenarien, in denen Sie möglicherweise ein erabgelösten Update installieren müssen:

-   Wenn ein ersetzendes Update nur neuere Versionen eines Betriebssystems unterstützt und auf einigen Client Computern frühere Versionen des Betriebssystems ausgeführt werden.

-   Wenn ein ersetzendes Update die Anwendbarkeit stärker einschränkt als das Update, das es ersetzt, ist es für einige Client Computer ungeeignet.

-   Wenn ein Update aufgrund neuer Änderungen nicht mehr von einem zuvor veröffentlichten Update abgelöst wird. Es ist möglich, dass durch Änderungen in jeder Version ein Update nicht mehr ein Update ersetzt, das zuvor in einer früheren Version abgelöst wurde. In diesem Szenario wird weiterhin eine Meldung über das ersetzte Update angezeigt, auch wenn das Update, durch das es ersetzt wird, durch ein Update ersetzt wurde, das dies nicht getan hat.


