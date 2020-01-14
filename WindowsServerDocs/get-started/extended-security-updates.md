---
title: Erweiterte Sicherheitsupdates für Windows Server 2008 und 2008 R2
description: Erfahre, wie du erweiterte Sicherheitsupdates (Extended Security Updates, ESU) für Windows Server 2008 und 2008 R2 nach dem Ende des Supportlebenszyklus verwenden kannst.
ms.prod: windows-server
ms.technology: server-general
ms.mktglfcycl: manage
author: iainfoulds
ms.author: iainfou
ms.topic: get-started-article
ms.localizationpriority: high
ms.date: 12/16/2019
ms.openlocfilehash: a5af1ad5a730f1dc90111734a9b8b1aacc91201b
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75466343"
---
# <a name="how-to-use-windows-server-2008-and-2008-r2-extended-security-updates-esu"></a>Verwenden der erweiterten Sicherheitsupdates (ESU) für Windows Server 2008 und 2008 R2

>Gilt für: Windows Server 2008/2008 R2

Windows Server 2008 und Windows Server 2008 R2 erreichen am 14. Januar 2020 das Ende des Supportlebenszyklus. Windows Server Long-Term Servicing Channel (LTSC) bietet mindestens zehn Jahre lang Support – fünf Jahre grundlegenden Support und fünf Jahre erweiterten Support. Dieser Support umfasst regelmäßige Sicherheitsupdates.

Das Ende des Supports bedeutet auch das Ende der Sicherheitsupdates. Dieses Szenario kann Sicherheits- oder Complianceprobleme mit sich bringen und eine Gefahr für Geschäftsanwendungen darstellen. Microsoft empfiehlt, dass du [ein Upgrade auf die aktuelle Version von Windows Server](modernize-windows-server-2008.md) durchführst, um von der aktuellen Sicherheit, Leistung und Innovation zu profitieren.

Wenn du nicht alle Server bis zum Stichtag für das Ende des Supportlebenszyklus aktualisieren kannst, helfen dir die folgenden Optionen während der Übergangszeit beim Schutz von Anwendungen und Daten:

* Migriere vorhandene Windows Server 2008- und 2008 R2-Workloads unverändert zu Azure Virtual Machines (VMs).
    * Diese Migration zu Azure ermöglicht es dir, automatisch weitere drei Jahre lang erweiterte Sicherheitsupdates (ESU) zu erhalten. Neben den Kosten für die Azure-VM fallen keine zusätzlichen Gebühren für erweiterte Sicherheitsupdates an, und es ist keine weitere Konfiguration erforderlich.
* Erwirb ein erweitertes Sicherheitsupdateabonnement für deine Server, und bleib geschützt, bis du bereit bist, ein Upgrade auf eine neuere Version von Windows Server auszuführen.
    * Diese Updates werden bis zu drei Jahre nach dem Ende des Lebenszyklus des Supports bereitgestellt.

Wenn die drei Jahre mit erweiterten Updates abgelaufen sind, gibt es keine Möglichkeit mehr, dass Computer zusätzliche Updates erhalten.

## <a name="what-are-extended-security-updates-for-windows-server"></a>Was sind erweiterte Sicherheitsupdates für Windows Server?

Erweiterte Sicherheitsupdates (ESU) für Windows Server umfassen Sicherheitsupdates und Bulletins, die als *kritisch* und *wichtig* bewertet sind. Du erhältst diese nach dem 14. Januar 2020 für einen Zeitraum von maximal drei Jahren. Folgendes ist in den erweiterten Sicherheitsupdates nicht enthalten:

* Neue Funktionen
* Vom Kunden angeforderte nicht sicherheitsrelevante Hotfixes
* Anforderungen zu Entwurfsänderungen

Weitere Informationen findest du unter [Häufig gestellte Fragen zu erweiterten Sicherheitsupdates](https://www.microsoft.com/cloud-platform/extended-security-updates).

## <a name="register-for-extended-security-updates"></a>Für erweiterte Sicherheitsupdates registrieren

Damit du erweiterte Sicherheitsupdates verwenden kannst, musst du einen Mehrfachaktivierungsschlüssel (Multiple Activation Key, MAK) erstellen und auf Windows Server 2008- und 2008 R2-Computer anwenden. Mit diesem Schlüssel teilst du den Windows Update-Servern mit, dass du weiterhin Sicherheitsupdates empfangen kannst. Du registrierst dich für erweiterte Sicherheitsupdates und verwaltest diese Schlüssel mithilfe des Azure-Portals, auch wenn du nur lokale Computer verwendest.

> [!NOTE]
> Wenn du Windows Server 2008/2008 R2-VMs in Azure ausführst, sind die folgenden Schritte nicht erforderlich. Azure-VMs werden automatisch für erweiterte Sicherheitsupdates aktiviert. Du musst keine Ressource und keinen Schlüssel für erweiterte Sicherheitsupdates erstellen, und es fallen keine zusätzlichen Kosten für die Verwendung erweiterter Sicherheitsupdates mit Azure-VMs an.

Führe die folgenden Schritte im Azure-Portal aus, um andere VMs als Azure-VMs für erweiterte Sicherheitsupdates zu registrieren und einen Schlüssel zu erstellen:

1. Melde dich beim [Azure-Portal](https://portal.azure.com/) an.
1. Suche im Suchfeld oben im Azure-Portal nach **Erweiterte Sicherheitsupdates**, und wähle diese aus.

    ![Suchen nach erweiterten Sicherheitsupdates im Azure-Portal](media/extended-security-updates/esu-portal-search.png)

    Wenn du bisher noch keine erweiterten Sicherheitsupdates verwendet hast, wähle zunächst die Option **+Erstellen** einer Ressource für erweiterte Sicherheitsupdates aus. Wähle andernfalls deine Ressource aus der Liste aus.

1. Wähle unter **Register for Extended Service Updates** (Für erweiterte Serviceupdates registrieren) die Option **Erste Schritte** aus.

    ![Erste Schritte mit erweiterten Sicherheitsupdates im Azure-Portal](media/extended-security-updates/get-started-with-esu.png)

1. Damit du deinen ersten Schlüssel erstellen kannst, wähle **Schlüssel abrufen** aus.

    ![Auswählen, einen Schlüssel im Azure-Portal zu erstellen](media/extended-security-updates/get-key.png)

    > [!NOTE]
    > Du benötigst ein Azure-Abonnement, das deinem Konto zugeordnet ist, um die Ressource und den Schlüssel für erweiterte Sicherheitsupdates zu erstellen. Wenn du über kein Azure-Abonnement verfügst, das deinem Konto zugeordnet ist, melde dich mit einem anderen Benutzerkonto an, oder erstelle ein Azure-Abonnement, indem du die im Portal angezeigten Schritte ausführst.

1. Wähle unter **Azure-Details** dein Azure-Abonnement, eine Ressourcengruppe und einen Speicherort für deinen Schlüssel aus.

    Gib unter **Registrierungsdetails** die folgenden Informationen ein:

    | Einstellung             | Value |
    |---------------------|-------|
    | Schlüsselname            | Einen Anzeigenamen für deinen Schlüssel, z. B. *Vertrag01* |
    | Vertragsnummer    | Die vom Volumenlizenzierungs-Vertragsverwaltungssystem oder vom MSLicense for Enterprise Agreement-Programm generierte Vertragsnummer |
    | Anzahl von Computern | Wähle die Anzahl der Computer aus, auf denen du erweiterte Sicherheitsupdates mit diesem Schlüssel installieren möchtest. |
    | Betriebssystem    | Wähle das Betriebssystem aus, mit dem dieser Schlüssel verwendet werden soll, z. B. Windows Server 2008 oder Windows Server 2008 R2. |

    Wenn du fertig bist, wähle **Review + register** (Überprüfen und Registrieren) aus.

1. Nach erfolgreicher Überprüfung wird eine Zusammenfassung der Optionen für die neue Registrierungsressource angezeigt. Korrigiere ggf. Validierungsfehler, oder aktualisiere deine Konfigurationsoptionen. Die [Rechtlichen Hinweise](https://azure.microsoft.com/support/legal/) und die [Datenschutzbestimmungen](https://privacy.microsoft.com/privacystatement) für Azure gelten.

    Aktiviere das Kontrollkästchen, um zu bestätigen, dass du über berechtigte Computer verfügst und der Schlüssel nur in deiner Organisation verwendet wird:

    ![Bestätigen, dass der Schlüssel nur von deiner Organisation verwendet wird](media/extended-security-updates/confirm-key-usage.png)

    Wenn du fertig bist, wähle **Erstellen** aus, um den MAK zu generieren.

Die Registrierung für erweiterte Sicherheitsupdates ist jetzt für die Verwendung mit deinen Computern verfügbar. Wende den erstellten Schlüssel auf Windows Server 2008- und 2008 R2-Computer an, für die du weiterhin Sicherheitsupdates erhalten möchtest.

## <a name="download-and-apply-extended-security-updates"></a>Herunterladen und Anwenden erweiterter Sicherheitsupdates

Das Bereitstellen, Herunterladen und Anwenden erweiterter Sicherheitsupdates für Windows Server unterscheidet sich nicht von den vorhandenen Bereitstellungsprozessen. Die Updates, die über erweiterte Sicherheitsupdates bereitgestellt werden, dienen ausschließlich der *Sicherheit*und werden an jedem Patch-Dienstag veröffentlicht.

Du kannst die Updates mithilfe der Tools und Prozesse installieren, über die du bereits verfügst. Der einzige Unterschied besteht darin, dass das System mit dem im vorherigen Abschnitt generierten Schlüssel registriert werden muss, damit die Updates heruntergeladen und installiert werden können.

Bei Azure-VMs wird der Vorgang zum Aktivieren des Computers für erweiterte Sicherheitsupdates automatisch abgeschlossen. Updates werden ohne eine zusätzliche Konfiguration heruntergeladen und installiert.
