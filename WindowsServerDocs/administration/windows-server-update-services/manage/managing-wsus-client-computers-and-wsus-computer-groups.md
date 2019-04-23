---
title: Verwalten von WSUS-Clientcomputern und WSUS-Computergruppen
description: Thema mit Windows Server Update Service (WSUS) - Clientcomputer und Gruppen verwalten
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e63aa5d53f01fbff3029c6896556d92c9c99aa50
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857681"
---
# <a name="managing-wsus-client-computers-and-wsus-computer-groups"></a>Verwalten von WSUS-Clientcomputern und WSUS-Computergruppen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Der Knoten "Computer" ist in der WSUS-Verwaltungskonsole zum Verwalten von WSUS-Clientcomputer und Geräte zentraler Zugriffspunkt. Unter diesem Knoten finden Sie die verschiedenen Gruppen, die Sie eingerichtet haben (und die Standardgruppe, nicht zugewiesene Computer).

## <a name="managing-client-computers"></a>Verwalten von Clientcomputern
Auswählen einer der Computergruppen in der **Computer** Knoten unter **Optionen** bewirkt, dass die Computer in der Gruppe, die im Detailbereich angezeigt werden. Wenn ein Computer mehreren Gruppen zugewiesen ist, wird es in den Codebeispielen beider Gruppen angezeigt. Wenn Sie einen Computer in der Liste auswählen, sehen Sie seine Eigenschaften, die allgemeine Informationen zu dem Computer und der Status von Updates für sie, wie z. B. die Installation oder die Erkennung Status eines Updates für einen bestimmten Computer enthalten. Sie können die Liste der Computer unter einer bestimmten Computergruppe nach Status filtern. Der Standardwert zeigt nur Computer, für welche Updates erforderlich sind, oder der Fehler bei der Installation haben; Allerdings können Sie die Anzeige von einem beliebigen Status filtern. Klicken Sie auf **aktualisieren** nach dem Ändern des Status-Filters.

Sie können auch Computergruppen auf der Seite Computer verwalten, einschließlich der Gruppen erstellen und Zuweisen von Computern zu werden. Weitere Informationen zum Verwalten von Computergruppen finden Sie unter Verwalten von Computergruppen, die im nächsten Abschnitt dieses Handbuchs und im Abschnitt [1.5. Planen der WSUS-Computergruppen](../plan/plan-your-wsus-deployment.md#BKMK_1.5) in Schritt 1: Vorbereiten der WSUS-Bereitstellung im WSUS-Bereitstellungshandbuch.

> [!NOTE]
> Sie müssen zuerst konfigurieren, dass Clientcomputer für die WSUS-Server zu kontaktieren, bevor Sie sie von diesem Server verwalten können. Erst nach dem Ausführen dieser Aufgabe dem WSUS-Server erkennt Ihre Clientcomputer nicht, und sie nicht in der Liste auf der Seite "Computer" angezeigt. Weitere Informationen zum Einrichten von Client-Computern finden Sie unter [1.5. Planen der WSUS-Computergruppen](../plan/plan-your-wsus-deployment.md#BKMK_1.5) von Schritt 1: Vorbereiten der WSUS-Bereitstellung und Schritt 3: Konfigurieren Sie WSUS, in der WSUS-Bereitstellungshandbuch.

## <a name="controlling-when-wsus-client-computers-install-updates"></a>Steuern, wenn der WSUS-Clientcomputer Updates installieren
Es gibt zwei Methoden, um zu steuern, bei der Installation von Updates in WSUS-Clientcomputer:

-   Die Genehmigung mit der Fristen: Stichtage zum Erzwingen genau, wenn ein Update installiert wurde

-   Richtlinien für die WSUS-Gruppe: Gruppenrichtlinien steuern, wann der Windows Update-Agent überprüft und Updates installiert

    Weitere Informationen finden Sie unter: [Schritt 5: Konfigurieren der Gruppenrichtlinieneinstellungen für automatische Updates](../deploy/4-configure-group-policy-settings-for-automatic-updates.md), in der WSUS-Bereitstellungshandbuch.

## <a name="managing-computer-groups"></a>Verwalten von Computergruppen
WSUS bietet Ihnen die Möglichkeit, Updates gezielt auf Gruppen von Clientcomputern anzuwenden, sodass Sie sicherstellen können, dass bestimmte Computer immer zum geeigneten Zeitpunkt die richtigen Updates erhalten. Wenn z. B. für alle Computer in einer Abteilung (z. B. im Buchhaltungsteam) eine bestimmte Konfiguration verwendet wird, können Sie eine Gruppe für das Team erstellen, entscheiden, welche Updates für die Computer erforderlich sind und wann sie installiert werden sollen, und anschließend mithilfe von WSUS-Berichten die Updates für das Team auswerten.

Computer werden immer zugewiesen der **alle Computer** gruppieren und bleiben in der **– nicht zugewiesene Computer** gruppieren, bis Sie sie zu einer anderen Gruppe zuweisen. Computer können mehreren Gruppen angehören.

Computergruppen können in Hierarchien eingerichtet werden (z. B. %%amp;quot;Gehaltsabrechnung%%amp;quot; und %%amp;quot;Kreditoren%%amp;quot; als untergeordnete Gruppen von %%amp;quot;Buchhaltung%%amp;quot;). Für eine übergeordnete Gruppe genehmigte Updates werden automatisch für untergeordnete Gruppen sowie für die höhere Gruppe selbst bereitgestellt. Wenn Sie Update 1 für "Buchhaltung" genehmigen, wird das Update also auf alle Computer in der Gruppe "Buchhaltung", alle Computer in der Gruppe Gehaltsabrechnung und alle Computer in der Gruppe "Accounts Payable" bereitgestellt werden.

Da Computer mehreren Gruppen zugewiesen werden können, kann es passieren, dass ein Update mehrmals für einen Computer genehmigt wird. Das Update wird jedoch nur einmal bereitgestellt, und alle Konflikte werden vom WSUS-Server aufgelöst. Fortsetzen möchten im obigen Beispiel ComputerA der Gehaltsabrechnung und Accounts Payable Gruppen zugewiesen ist und Update1 für beide Gruppen genehmigt wird, wird sie nur einmal bereitgestellt werden.

Für die Zuweisung von Computern zu Computergruppen stehen zwei Methoden zur Verfügung: serverseitige Zielgruppenadressierung und clientseitige Zielgruppenadressierung. Mit der serverseitige Zielgruppenadressierung, verschieben Sie manuell einen oder mehrere Clientcomputer in einer Computergruppe zu einem Zeitpunkt. Bei der clientseitigen Zielzuordnung richten Sie Clientcomputer mithilfe von Gruppenrichtlinien oder durch entsprechende Bearbeitung der Registrierungseinstellungen so ein, dass sie sich zuvor erstellten Computergruppen selbst hinzufügen können. Dieser Prozess kann ein Skript erstellt und gleichzeitig auf mehreren Computern bereitgestellt werden. Sie müssen angeben, die für die Zielgruppenadressierung-Methode Sie auf dem WSUS-Server verwenden dazu eine der beiden Optionen auf der **Computer** im Abschnitt der **Optionen** Seite.

> [!NOTE]
> Auf einem im Replikatmodus ausgeführten WSUS-Server können keine Computergruppen erstellt werden. Alle Computergruppen, die für die Clients des Replikatservers erforderlich sind, müssen auf dem WSUS-Server erstellt werden, das der Stamm der Hierarchie der WSUS-Server. Weitere Informationen zum Replikatmodus finden Sie unter [ausgeführten WSUS Replikatmodus](running-wsus-replica-mode.md) und Weitere Informationen über die serverseitige und clientseitige Zielgruppenadressierung finden Sie im Abschnitt [1.5. Planen der WSUS-Computergruppen](../plan/plan-your-wsus-deployment.md#BKMK_1.5) von Schritt 1: Vorbereiten der WSUS-Bereitstellung im Bereitstellungshandbuch für WSUS.


