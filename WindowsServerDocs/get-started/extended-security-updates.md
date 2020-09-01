---
title: Erweiterte Sicherheitsupdates für Windows Server 2008 und 2008 R2
description: Erfahre, wie du erweiterte Sicherheitsupdates (Extended Security Updates, ESU) für Windows Server 2008 und 2008 R2 nach dem Ende des Supportlebenszyklus verwenden kannst.
ms.mktglfcycl: manage
author: iainfoulds
ms.author: iainfou
ms.topic: get-started-article
ms.localizationpriority: high
ms.date: 02/21/2020
ms.openlocfilehash: f405486c5ea34b26f23a16552c24527939ca1fd4
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024564"
---
# <a name="how-to-use-windows-server-2008-and-2008-r2-extended-security-updates-esu"></a>Verwenden der erweiterten Sicherheitsupdates (ESU) für Windows Server 2008 und 2008 R2

>Gilt für: Windows Server 2008 und Windows Server 2008 R2

Windows Server 2008 und Windows Server 2008 R2 haben am 14. Januar 2020 das Ende des Supportlebenszyklus erreicht. Der Windows Server Long-Term Servicing Channel (LTSC) bietet mindestens zehn Jahre lang Support – fünf Jahre allgemeinen Support und fünf Jahre erweiterten Support. Dieser Support umfasst regelmäßige Sicherheitsupdates.

Das Ende des Supports bedeutet auch das Ende der Sicherheitsupdates. Dieses Szenario kann Sicherheits- oder Complianceprobleme mit sich bringen und eine Gefahr für Geschäftsanwendungen darstellen. Microsoft empfiehlt, dass du [ein Upgrade auf die aktuelle Version von Windows Server](modernize-windows-server-2008.md) durchführst, um von der aktuellen Sicherheit, Leistung und Innovation zu profitieren.

Wenn Sie noch kein Upgrade Ihrer Server durchgeführt haben, helfen Ihnen die folgenden Optionen, Ihre Apps und Daten während des Übergangs zu schützen:

* Migriere vorhandene Windows Server 2008- und 2008 R2-Workloads unverändert zu Azure Virtual Machines (VMs).
  * Diese Migration zu Azure ermöglicht es dir, automatisch weitere drei Jahre lang erweiterte Sicherheitsupdates (ESU) zu erhalten. Neben den Kosten für die Azure-VM fallen keine zusätzlichen Gebühren für erweiterte Sicherheitsupdates an, und es ist keine weitere Konfiguration erforderlich.
* Erwirb ein erweitertes Sicherheitsupdateabonnement für deine Server, und bleib geschützt, bis du bereit bist, ein Upgrade auf eine neuere Version von Windows Server auszuführen.
  * Diese Updates werden bis zu drei Jahre nach dem Ende des Lebenszyklus des Supports bereitgestellt.

Nach dem dreijährigen erweiterten Updatezeitraum stellen wir die Updates für Windows Server 2008 und 2008 R2 ein. Es empfiehlt sich, Ihre Version von Windows Server so bald wie möglich auf eine neuere Version zu aktualisieren.

## <a name="what-are-extended-security-updates-for-windows-server"></a>Was sind erweiterte Sicherheitsupdates für Windows Server?

Erweiterte Sicherheitsupdates (ESU) für Windows Server umfassen Sicherheitsupdates und Bulletins, die als *kritisch* und *wichtig* bewertet sind. Du erhältst diese nach dem 14. Januar 2020 für einen Zeitraum von maximal drei Jahren. Folgendes ist in den erweiterten Sicherheitsupdates nicht enthalten:

* Neue Funktionen
* Vom Kunden angeforderte nicht sicherheitsrelevante Hotfixes
* Anforderungen zu Entwurfsänderungen

Weitere Informationen findest du unter [Häufig gestellte Fragen zu erweiterten Sicherheitsupdates](https://www.microsoft.com/cloud-platform/extended-security-updates).

## <a name="how-to-use-extended-security-updates"></a>Verwenden erweiterter Sicherheitsupdates

Wenn Sie VMs mit Windows Server 2008 oder 2008 R2 in Azure ausführen, sind für diese automatisch erweiterte Sicherheitsupdates aktiviert. Sie brauchen nichts zu konfigurieren, und es fallen keine zusätzlichen Kosten für die Verwendung erweiterter Sicherheitsupdates mit Azure-VMs an. Erweiterte Sicherheitsupdates werden automatisch an Azure-VMs übermittelt, wenn diese für den Empfang von Updates konfiguriert sind.

> [!NOTE]
> Microsoft.ClassicCompute-VMs erfordern eine zusätzliche Konfiguration für die Bereitstellung erweiterter Sicherheitsupdates, da sie keinen Zugriff auf [Azure Instance Metadata Service](https://docs.microsoft.com/azure/virtual-machines/windows/instance-metadata-service) haben, der die Berechtigung für erweiterte Sicherheitsupdates bestimmt. Wenden Sie sich an den [Microsoft-Support](https://support.microsoft.com/contactus?PID=17336), um weitere Hilfe zu erhalten.

Für andere Umgebungen, wie z. B. lokale VMs oder physische Server, müssen Sie erweiterte Sicherheitsupdates manuell anfordern und konfigurieren. Sie können erweiterte Sicherheitsupdates über Volumenlizenzierungsprogramme erwerben, wie etwa Enterprise Agreement (EA), Enterprise Agreement Subscription (EAS), Enrollment for Education Solutions (EES) oder Server and Cloud Enrollment (SCE).

Wenn Sie erweiterte Sicherheitsupdates erworben haben, können Sie eine der folgenden Methoden verwenden, um Ihre Schlüssel zu erhalten:

* Wenn Sie erweiterte Sicherheitsupdates über das Azure-Portal beziehen möchten, können Sie sich [für erweiterte Sicherheitsupdates im Azure-Portal registrieren](#register-for-extended-security-updates-on-azure-portal).
* Sie können sich auch beim [Microsoft Volume Licensing Service Center anmelden](#sign-in-to-the-microsoft-volume-licensing-service-center), um Ihre Schlüssel abzurufen, ohne das Azure-Portal zu verwenden.

### <a name="register-for-extended-security-updates-on-azure-portal"></a>Registrieren für erweiterte Sicherheitsupdates im Azure-Portal

Um erweiterte Sicherheitsupdates zu verwenden, müssen Sie einen Mehrfachaktivierungsschlüssel (Multiple Activation Key, MAK) erstellen und auf Windows Server 2008- und 2008 R2-Computer anwenden. Mit dem MAK teilen Sie den Windows Update-Servern mit, dass Sie weiterhin Sicherheitsupdates empfangen können. Sie registrieren sich für erweiterte Sicherheitsupdates und verwalten diese Schlüssel mithilfe des Azure-Portals, auch wenn Sie nur lokale Computer verwenden.

> [!NOTE]
> Wenn Sie Windows Server 2008 und 2008 R2 in Azure VMs ausführen, brauchen Sie sich nicht für erweiterte Sicherheitsupdates zu registrieren. Für andere Umgebungen, wie z. B. lokale VMs oder physische Server, müssen Sie [erweiterte Sicherheitsupdates kaufen](https://www.microsoft.com/licensing/how-to-buy/how-to-buy), bevor Sie diese registrieren und verwenden können.

Um Ihre VM für erweiterte Sicherheitsupdates zu registrieren und einen Schlüssel zu erstellen, öffnen Sie das Azure-Portal, und befolgen Sie diese Anweisungen:

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.
2. Suchen Sie im Suchfeld oben im Azure-Portal nach **Erweiterte Sicherheitsupdates**, und wählen Sie diese aus.

    ![Suchen nach erweiterten Sicherheitsupdates im Azure-Portal](media/extended-security-updates/esu-portal-search.png)

    Wenn Sie bisher noch keine erweiterten Sicherheitsupdates verwendet haben, wählen Sie zunächst die Option **+Erstellen** aus, um eine Ressource für erweiterte Sicherheitsupdates zu erstellen. Wähle andernfalls deine Ressource aus der Liste aus.

3. Wähle unter **Register for Extended Service Updates** (Für erweiterte Serviceupdates registrieren) die Option **Erste Schritte** aus.

    ![Erste Schritte mit erweiterten Sicherheitsupdates im Azure-Portal](media/extended-security-updates/get-started-with-esu.png)

4. Damit du deinen ersten Schlüssel erstellen kannst, wähle **Schlüssel abrufen** aus.

    ![Auswählen der Option zum Erstellen eines Schlüssels im Azure-Portal](media/extended-security-updates/get-key.png)

    Sie benötigen ein Azure-Abonnement, das Ihrem Konto zugeordnet ist, um die Ressource und den Schlüssel für erweiterte Sicherheitsupdates zu erstellen. Wenn Sie nicht über ein Azure-Abonnement verfügen, das Ihrem Konto zugeordnet ist, melden Sie sich mit einem anderen Benutzerkonto an, oder erstellen Sie im Azure-Portal ein Azure-Abonnement.

    Ihrem Azure-Abonnement muss außerdem die Rolle „Mitwirkender“ zugeordnet sein, damit das Sicherheitsupdate funktioniert. Um Ihre Rolle zu überprüfen, geben Sie „Abonnements“ im Suchfeld ein. Sie sehen eine Tabelle, die Ihre Rolle neben Ihrer Abonnement-ID und Ihrem Namen anzeigt.

    Wenn Sie kein Mitwirkender sind, können Sie den Besitzer des Abonnements bitten, Ihre Rolle zu ändern. Um herauszufinden, wer Ihr Abonnement besitzt, navigieren Sie zur Rollentabelle, die im vorherigen Absatz beschrieben ist, und wählen Sie den Namen Ihres Abonnements aus. Navigieren Sie dann zum Menü auf der linken Seite, wählen Sie **Zugriffssteuerung (IAM)**  > **Rollenzuweisungen** aus, und suchen Sie nach dem Abschnitt „Besitzer“ in der Tabelle.

5. Wenn eine Seite angezeigt wird, die besagt „Registrieren Sie sich, um einen Mehrfachaktivierungsschlüssel zu erhalten“, bedeutet dies, dass Sie Zugriff auf die private Vorschau anfordern müssen, bevor Sie die erweiterten Sicherheitsupdates verwenden können. Wenn diese Seite nicht angezeigt wird, fahren Sie mit Schritt 6 fort.

   Um Zugriff anzufordern, wählen Sie **An der privaten Vorschau teilnehmen** aus. Ein E-Mail-Benachrichtigungsfenster wird geöffnet. Diese E-Mail stellt Ihre Zugriffsanforderung an das Produktteam dar.

    Geben Sie in Ihrer Anforderung die folgenden Informationen ein.

    * Kundenname
    * Azure-Abonnement-ID
    * Vertragsnummer (für ESU)
    * Anzahl der ESU-Server

    Wenn Sie fertig sind, senden Sie die E-Mail.

    Das Team überprüft die Informationen, die Sie in Ihrer Anforderungs-E-Mail angegeben haben. Wenn alles in Ordnung zu sein scheint, werden Sie der Liste der genehmigten Anforderungen hinzugefügt.

    Wenn das Team Ihre Anforderung nicht genehmigt, wird der folgende Fehler angezeigt:

    [Der Ressourcentyp konnte nicht im Namespace "Microsoft.WindowsESU" gefunden werden]()

6. Wähle unter **Azure-Details** dein Azure-Abonnement, eine Ressourcengruppe und einen Speicherort für deinen Schlüssel aus.

    Gib unter **Registrierungsdetails** die folgenden Informationen ein:

    | Einstellung             | Value |
    |---------------------|-------|
    | Schlüsselname            | Einen Anzeigenamen für deinen Schlüssel, z. B. *Vertrag01* |
    | Vertragsnummer    | Die vom Volumenlizenzierungs-Vertragsverwaltungssystem oder vom MSLicense for Enterprise Agreement-Programm generierte Vertragsnummer |
    | Anzahl von Computern | Wähle die Anzahl der Computer aus, auf denen du erweiterte Sicherheitsupdates mit diesem Schlüssel installieren möchtest. |
    | Betriebssystem    | Wähle das Betriebssystem aus, mit dem dieser Schlüssel verwendet werden soll, z. B. Windows Server 2008 oder Windows Server 2008 R2. |

    Wenn du fertig bist, wähle **Review + register** (Überprüfen und Registrieren) aus.

    >[!NOTE]
    >Achten Sie darauf, in Ihrem globalen Filter das Azure-Abonnement auszuwählen, an dessen privater Vorschau Sie teilgenommen haben. Wählen Sie die **Filter**-Schaltfläche auf dem Azure-Portal-Menüband aus, um Ihren globalen Abonnementfilter zu überprüfen.
    >
    > ![Abbildung des Azure-Portal-Menübands mit ausgewählter Schaltfläche „Filter“](media/azure-ribbon-filter.png)

7. Nach erfolgreicher Überprüfung wird eine Zusammenfassung der Optionen für die neue Registrierungsressource angezeigt. Korrigiere ggf. Validierungsfehler, oder aktualisiere deine Konfigurationsoptionen. Die [Rechtlichen Hinweise](https://azure.microsoft.com/support/legal/) und die [Datenschutzbestimmungen](https://privacy.microsoft.com/privacystatement) für Azure gelten.

    Aktiviere das Kontrollkästchen, um zu bestätigen, dass du über berechtigte Computer verfügst und der Schlüssel nur in deiner Organisation verwendet wird:

    ![Bestätigen, dass der Schlüssel nur von deiner Organisation verwendet wird](media/extended-security-updates/confirm-key-usage.png)

    Wenn du fertig bist, wähle **Erstellen** aus, um den MAK zu generieren.

Die Registrierung für erweiterte Sicherheitsupdates ist jetzt für die Verwendung mit Ihren Computern verfügbar. Wende den erstellten Schlüssel auf Windows Server 2008- und 2008 R2-Computer an, für die du weiterhin Sicherheitsupdates erhalten möchtest.

### <a name="sign-in-to-the-microsoft-volume-licensing-service-center"></a>Melden Sie sich beim Microsoft Volume Licensing Service Center an.

Wenn Sie keinen Zugriff auf das Azure-Portal besitzen, können Sie den Volumenlizenzierungsserver verwenden, um Ihre Aktivierungsschlüssel anzuzeigen und herunterzuladen.

So rufen Sie Ihre Schlüssel beim Volume Licensing Service Center ab:

1. Navigieren Sie zur [Volume Licensing Service Center-Seite](https://www.microsoft.com/vlsc), und melden Sie sich mit Ihren Azure-Anmeldeinformationen an.

2. Wählen Sie **Lizenzen** > **Beziehungszusammenfassung** > **Lizenzierungs-ID** > **Product Keys** aus.

Weitere Informationen zum Erhalten von erweiterten Sicherheitsupdates für berechtigte Windows-Geräte finden Sie in [unseren Tech Community-Beiträgen](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/obtaining-extended-security-updates-for-eligible-windows-devices/ba-p/1167091#).

## <a name="download-and-apply-extended-security-updates"></a>Herunterladen und Anwenden erweiterter Sicherheitsupdates

Das Bereitstellen, Herunterladen und Anwenden erweiterter Sicherheitsupdates für Windows Server unterscheidet sich nicht von den vorhandenen Bereitstellungsprozessen. Die Updates, die über erweiterte Sicherheitsupdates bereitgestellt werden, dienen ausschließlich der *Sicherheit*und werden an jedem Patch-Dienstag veröffentlicht.

Du kannst die Updates mithilfe der Tools und Prozesse installieren, über die du bereits verfügst. Der einzige Unterschied besteht darin, dass das System mit dem im vorherigen Abschnitt generierten Schlüssel registriert werden muss, damit die Updates heruntergeladen und installiert werden können.

Bei Azure-VMs wird der Vorgang zum Aktivieren des Computers für erweiterte Sicherheitsupdates automatisch abgeschlossen. Updates werden ohne eine zusätzliche Konfiguration heruntergeladen und installiert.