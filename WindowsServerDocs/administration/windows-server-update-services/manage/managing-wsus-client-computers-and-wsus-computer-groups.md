---
title: Verwalten von WSUS-Clientcomputern und WSUS-Computergruppen
description: 'Thema zu Windows Server Update Service (WSUS): Verwalten von Client Computern und-Gruppen'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b1ea915-0f9f-4f0e-8913-a1dd460d07ab
author: coreyp-at-msft
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 454fa385dc9fb91218ad836d4ad34e92e9644dac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361631"
---
# <a name="managing-wsus-client-computers-and-wsus-computer-groups"></a>Verwalten von WSUS-Clientcomputern und WSUS-Computergruppen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Knoten Computer ist der zentrale Zugriffspunkt in der WSUS-Verwaltungskonsole zum Verwalten von WSUS-Client Computern und-Geräten. Unter diesem Knoten finden Sie die verschiedenen Gruppen, die Sie eingerichtet haben (zuzüglich der Standardgruppe "nicht zugewiesene Computer").

## <a name="managing-client-computers"></a>Verwalten von Client Computern
Wenn Sie eine der Computer Gruppen im Knoten **Computer** unter **Optionen** auswählen, werden die Computer in dieser Gruppe im Detailbereich angezeigt. Wenn ein Computer mehreren Gruppen zugewiesen ist, wird er in den Listen beider Gruppen angezeigt. Wenn Sie einen Computer in der Liste auswählen, werden die zugehörigen Eigenschaften angezeigt. Hierzu gehören allgemeine Details zum Computer und der Status der Updates, wie z. b. die Installation oder der Erkennungs Status eines Updates für einen bestimmten Computer. Sie können die Liste der Computer unter einer bestimmten Computergruppe nach dem Status filtern. In der Standardeinstellung werden nur Computer angezeigt, für die Updates erforderlich sind oder bei denen Installationsfehler aufgetreten sind. Allerdings können Sie die Anzeige nach beliebigen Status filtern. Klicken Sie nach dem Ändern des Status Filters auf **Aktualisieren** .

Sie können Computer Gruppen auch auf der Seite Computer verwalten. dazu gehören das Erstellen der Gruppen und das Zuweisen von Computern. Weitere Informationen zum Verwalten von Computer Gruppen finden Sie im Abschnitt Verwalten von Computer Gruppen im nächsten Abschnitt dieses Handbuchs und im Abschnitt [1,5. Planen der WSUS-Computer Gruppen @ no__t-0 in Schritt 1: Vorbereiten der WSUS-Bereitstellung des WSUS-Bereitstellungs Handbuchs.

> [!NOTE]
> Sie müssen die Client Computer zunächst so konfigurieren, dass Sie den WSUS-Server kontaktieren, bevor Sie Sie von diesem Server aus verwalten können. Bis Sie diese Aufgabe ausführen, erkennt der WSUS-Server Ihre Client Computer nicht und wird nicht in der Liste auf der Seite Computer angezeigt. Weitere Informationen zum Einrichten von Client Computern finden Sie unter [1,5. Planen der WSUS-Computer Gruppen @ no__t-0 von Schritt 1: Vorbereiten der WSUS-Bereitstellung und Schritt 3: Konfigurieren von WSUS im WSUS-Bereitstellungs Handbuch.

## <a name="controlling-when-wsus-client-computers-install-updates"></a>Steuern, wann Updates von WSUS-Client Computern installiert werden
Es gibt zwei Methoden, um zu steuern, wann Updates von WSUS-Client Computern installiert werden:

-   Genehmigung mit Terminen: Fristen, die bei der Installation eines Updates strikt erzwingen

-   WSUS-Gruppenrichtlinien: Gruppenrichtlinien steuern, wann Updates durch den Windows Update-Agent überprüft und installiert werden

    Weitere Informationen finden Sie unter: [Schritt 5: Konfigurieren Sie Gruppenrichtlinie Einstellungen für automatische Updates @ no__t-0 im WSUS-Bereitstellungs Handbuch.

## <a name="managing-computer-groups"></a>Verwalten von Computer Gruppen
WSUS bietet Ihnen die Möglichkeit, Updates gezielt auf Gruppen von Clientcomputern anzuwenden, sodass Sie sicherstellen können, dass bestimmte Computer immer zum geeigneten Zeitpunkt die richtigen Updates erhalten. Wenn z. B. für alle Computer in einer Abteilung (z. B. im Buchhaltungsteam) eine bestimmte Konfiguration verwendet wird, können Sie eine Gruppe für das Team erstellen, entscheiden, welche Updates für die Computer erforderlich sind und wann sie installiert werden sollen, und anschließend mithilfe von WSUS-Berichten die Updates für das Team auswerten.

Computer werden immer der Gruppe **alle Computer** zugewiesen und bleiben der Gruppe **nicht zugewiesene Computer** zugewiesen, bis Sie Sie einer anderen Gruppe zuweisen. Computer können mehreren Gruppen angehören.

Computergruppen können in Hierarchien eingerichtet werden (z. B. %%amp;quot;Gehaltsabrechnung%%amp;quot; und %%amp;quot;Kreditoren%%amp;quot; als untergeordnete Gruppen von %%amp;quot;Buchhaltung%%amp;quot;). Updates, die für eine höhere Gruppe genehmigt werden, werden automatisch für niedrigere Gruppen und für die höhere Gruppe bereitgestellt. Wenn Sie Update1 für die Gruppe "Buchhaltung" genehmigen, wird das Update auf allen Computern in der Gruppe "Buchhaltung", auf allen Computern in der Gehaltsgruppe und auf allen Computern in der Gruppe "Konten ist" bereitgestellt.

Da Computer mehreren Gruppen zugewiesen werden können, kann es passieren, dass ein Update mehrmals für einen Computer genehmigt wird. Das Update wird jedoch nur einmal bereitgestellt, und alle Konflikte werden vom WSUS-Server aufgelöst. Wenn Sie das obige Beispiel fortsetzen möchten, wenn ComputerA sowohl dem Abrechnungs-als auch dem Konto für die kontozuweisung zugewiesen ist und Update1 für beide Gruppen genehmigt wird, wird es nur einmal bereitgestellt.

Für die Zuweisung von Computern zu Computergruppen stehen zwei Methoden zur Verfügung: serverseitige Zielgruppenadressierung und clientseitige Zielgruppenadressierung. Bei der serverseitigen Ausrichtung müssen Sie mindestens einen Client Computer manuell in eine Computergruppe verschieben. Bei der clientseitigen Zielzuordnung richten Sie Clientcomputer mithilfe von Gruppenrichtlinien oder durch entsprechende Bearbeitung der Registrierungseinstellungen so ein, dass sie sich zuvor erstellten Computergruppen selbst hinzufügen können. Bei diesem Prozess kann ein Skript erstellt und auf mehreren Computern gleichzeitig bereitgestellt werden. Sie müssen die Ziel Ziel Methode angeben, die auf dem WSUS-Server verwendet werden soll, indem Sie eine der beiden Optionen im Abschnitt **Computer** der Seite **Optionen** auswählen.

> [!NOTE]
> Auf einem im Replikatmodus ausgeführten WSUS-Server können keine Computergruppen erstellt werden. Alle Computer Gruppen, die für Clients des Replikat Servers erforderlich sind, müssen auf dem WSUS-Server erstellt werden, der das Stammverzeichnis der WSUS-Server Hierarchie ist. Weitere Informationen zum Replikat Modus finden Sie unter [Ausführen des WSUS-Replikat Modus](running-wsus-replica-mode.md) . Weitere Informationen zur serverseitigen und Client seitigen Ziel Einstellungen finden Sie im Abschnitt [1,5. Planen der WSUS-Computer Gruppen @ no__t-0 von Schritt 1: Vorbereiten der WSUS-Bereitstellung im WSUS-Bereitstellungs Handbuch.


