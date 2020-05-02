---
title: Vorabbereitstellen von Clustercomputerobjekten in Active Directory Domain Services
description: Vorab Bereitstellen von Cluster Computer Objekten in Active Directory Domain Services.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: eb9077f40c33d615c0bbe18f1c02b29ce27165a2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720523"
---
# <a name="prestage-cluster-computer-objects-in-active-directory-domain-services"></a>Vorabbereitstellen von Clustercomputerobjekten in Active Directory Domain Services

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird gezeigt, wie Sie Clustercomputerobjekte in den Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) vorab bereitstellen. Sie können mit diesem Verfahren Benutzern oder Gruppen, die nicht über Berechtigungen zum Erstellen von Computerobjekten in AD DS verfügen, das Erstellen eines Failoverclusters ermöglichen.

Beim Erstellen eines Failoverclusters mit dem Clustererstellungs-Assistenten oder mit Windows PowerShell müssen Sie einen Namen für den Cluster angeben. Wenn Sie beim Erstellen des Clusters über ausreichende Berechtigungen verfügen, wird automatisch in AD DS ein Computerobjekt erstellt, das den gleichen Namen hat wie der Cluster. Dieses Objekt wird als *Clusternamenobjekt* oder CNO bezeichnet. Über das CNO werden automatisch virtuelle Computerobjekte (VCOs) erstellt, wenn Sie Clusterrollen konfigurieren, von denen Clientzugriffspunkte verwendet werden. Wenn Sie beispielsweise einen hoch verfügbaren Dateiserver mit einem Clientzugriffspunkt mit dem Namen *Dateiserver1*erstellen, wird vom CNO ein entsprechendes VCO in AD DS erstellt.

>[!NOTE]
>Es gibt die Option, einen Active Directory getrennten Cluster zu erstellen, bei dem in AD DS keine CNO oder VCOs erstellt werden. Diese Möglichkeit ist für bestimmte Typen von Clusterbereitstellungen gedacht. Weitere Informationen finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v%3dws.11)>).

Für die automatische Erstellung des CNOs benötigt der Benutzer, der den Failovercluster erstellt, die Berechtigung **Computerobjekte erstellen** für die Organisationseinheit (Organizational Unit, OU) oder den Container, in dem sich die Server befinden, aus denen der Cluster gebildet werden soll. Ein Benutzer mit entsprechenden Berechtigungen in AD DS (normalerweise ein Domänenadministrator) kann das CNO vorab in AD DS bereitstellen, damit ein Benutzer oder eine Gruppe ohne diese Berechtigung einen Cluster erstellen kann. Dadurch hat der Domänenadministrator außerdem mehr Kontrolle über die für den Cluster verwendete Benennungskonvention sowie darüber, in welcher Organisationseinheit die Clusterobjekte erstellt werden.

## <a name="step-1-prestage-the-cno-in-ad-ds"></a>Schritt 1: Vorabbereitstellen des CNOs in AD DS

Bevor Sie beginnen, sollten Sie sicherstellen, dass folgende Informationen vorhanden sind:

- Der Name, den Sie dem Cluster zuweisen möchten
- Der Name des Benutzerkontos oder der Gruppe, dem bzw. der Sie Rechte zum Erstellen des Clusters erteilen möchten.

Als bewährte Methode wird empfohlen, eine Organisationseinheit für die Clusterobjekte zu erstellen. Wenn bereits eine Organisationseinheit vorhanden ist, die Sie verwenden möchten, ist zum Ausführen dieses Schritts mindestens die Mitgliedschaft in der Gruppe **Konten-Operatoren** erforderlich. Wenn Sie eine Organisationseinheit für die Clusterobjekte erstellen, müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um diesen Schritt auszuführen.

>[!NOTE]
>Wenn Sie das CNO im Standardcontainer %%amp;quot;Computer%%amp;quot; anstatt in einer Organisationseinheit erstellen, müssen Sie Schritt 3 dieses Themas nicht ausführen. In diesem Szenario kann ein Clusteradministrator bis zu zehn VCOs ohne zusätzliche Konfiguration erstellen.

### <a name="prestage-the-cno-in-ad-ds"></a>CNO in AD DS vorab bereitstellen

1. Öffnen Sie auf einem Computer, auf dem die AD DS-Tools aus den Remoteserver-Verwaltungstools installiert sind, oder auf einem Domänencontroller das Snap-In **Active Directory-Benutzer und -Computer**. Um dies auf einem Server zu erreichen, starten Sie Server-Manager, und wählen Sie dann **im Menü Extras** die Option **Active Directory Benutzer und Computer**aus.
2. Zum Erstellen einer Organisationseinheit für die Cluster Computer Objekte klicken Sie mit der rechten Maustaste auf den Domänen Namen oder eine vorhandene Organisationseinheit, zeigen Sie auf **neu**, und wählen Sie dann **Organisationseinheit**aus. Geben Sie im Feld **Name** den Namen der Organisationseinheit ein, und klicken Sie dann auf **OK**.
3. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die Organisationseinheit, in der Sie das CNO erstellen möchten, zeigen Sie auf **neu**, und wählen Sie dann **Computer**aus.
4. Geben Sie im Feld **Computer Name** den Namen ein, der für den Failovercluster verwendet werden soll, und klicken Sie dann auf **OK**.

   >[!NOTE]
   >Diesen Clusternamen gibt der Benutzer, der den Cluster erstellt, auf der Seite **Zugriffspunkt für die Clusterverwaltung** im Clustererstellungs-Assistenten oder als Wert des *–Name* -Parameters für das Windows PowerShell-Cmdlet **New-Cluster** an.

5. Klicken Sie als bewährte Vorgehensweise mit der rechten Maustaste auf das gerade erstellte Computer Konto, wählen Sie **Eigenschaften**aus, und klicken Sie dann auf die Registerkarte **Objekt** . Aktivieren Sie auf der Registerkarte **Objekt** das Kontrollkästchen **Objekt vor zufälligem Löschen schützen** , und klicken Sie dann auf **OK**.
6. Klicken Sie mit der rechten Maustaste auf das gerade erstellte Computer Konto, und wählen Sie dann **Konto deaktivieren**aus. Wählen Sie zur Bestätigung **Ja** aus, und klicken Sie dann auf **OK**.

   >[!NOTE]
   >Sie müssen das Konto deaktivieren, damit bei der Clustererstellung überprüft werden kann, ob das Konto zurzeit von einem vorhandenen Computer oder Cluster in der Domäne verwendet wird.

![Deaktiviertes CNO in der Beispielorganisationseinheit %%amp;quot;Cluster%%amp;quot;](media/prestage-cluster-adds/disabled-cno-in-the-example-clusters-ou.png)

**Abbildung 1. Deaktiviertes CNO in der Organisationseinheit für Beispiel Cluster**

## <a name="step-2-grant-the-user-permissions-to-create-the-cluster"></a>Schritt 2: Erteilen der Benutzerberechtigungen zum Erstellen des Clusters

Sie müssen Berechtigungen konfigurieren, damit das Benutzerkonto, das zum Erstellen des Failoverclusters verwendet wird, über Vollzugriff auf das gerade erstellte CNO verfügt:

Sie müssen mindestens Mitglied der Gruppe **Konten-Operatoren** sein, um diesen Schritt ausführen zu können.

So erteilen Sie dem Benutzerberechtigungen zum Erstellen des Clusters:

1. Stellen Sie in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; sicher, dass im Menü **Ansicht** die Option **Erweiterte Features** ausgewählt ist.
2. Suchen Sie das CNO, klicken Sie mit der rechten Maustaste darauf, und wählen Sie dann **Eigenschaften**aus.
3. Wählen Sie auf der Registerkarte **Sicherheit** die Option **Hinzufügen** aus.
4. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das Benutzerkonto oder die Gruppe an, dem bzw. der Sie Berechtigungen erteilen möchten, und klicken Sie dann auf **OK**.
5. Wählen Sie das gerade hinzugefügte Benutzerkonto bzw. die gerade hinzugefügte Gruppe aus, und aktivieren Sie dann neben **Vollzugriff** das Kontrollkästchen **Zulassen**.
  
   ![Erteilen der Benutzer- oder Gruppenberechtigungen zum Erstellen des Clusters](media/prestage-cluster-adds/granting-full-control-to-the-user-create-the-cluster.png)
  
   **Abbildung 2. Gewähren der vollständigen Kontrolle für den Benutzer oder die Gruppe, der den Cluster erstellt**
6. Klicken Sie auf **OK**.

Nach Abschluss dieses Schritts kann der Benutzer, dem Sie Berechtigungen erteilt haben, den Failovercluster erstellen. Wenn sich das CNO jedoch in einer Organisationseinheit befindet, kann der Benutzer erst dann Clusterrollen erstellen, für die ein Clientzugriffspunkt erforderlich ist, wenn Sie Schritt 3 abgeschlossen haben.

>[!NOTE]
>Wenn sich das CNO im Standardcontainer %%amp;quot;Computer%%amp;quot; befindet, kann ein Clusteradministrator bis zu zehn VCOs ohne zusätzliche Konfiguration erstellen. Zum Hinzufügen von mehr als zehn VCOs müssen Sie explizit die Berechtigung **Computerobjekte erstellen** für das CNO für den Container %%amp;quot;Computer%%amp;quot; erteilen.

## <a name="step-3-grant-the-cno-permissions-to-the-ou-or-prestage-vcos-for-clustered-roles"></a>Schritt 3: Erteilen der CNO-Berechtigungen für die Organisationseinheit oder Vorabbereitstellen von VCOs für Clusterrollen

Wenn Sie eine Clusterrolle mit einem Clientzugriffspunkt erstellen, wird vom Cluster ein VCO in der gleichen Organisationseinheit erstellt, in der sich das CNO befindet. Damit dies automatisch geschieht, muss das CNO über Berechtigungen zum Erstellen von Computerobjekten in der Organisationseinheit verfügen.

Wenn Sie das CNO vorab in AD DS bereitgestellt haben, können Sie eine der folgenden Aktionen ausführen, um VCOs zu erstellen:

- Option 1: [Erteilen der CNO-Berechtigungen für die Organisationseinheit](#grant-the-cno-permissions-to-the-ou). Wenn Sie diese Option verwenden, können vom Cluster automatisch VCOs in AD DS erstellt werden. Daher kann ein Administrator für den Failovercluster Clusterrollen erstellen und muss Sie dazu nicht bitten, VCOs vorab in AD DS bereitstellen.

>[!NOTE]
>Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um die Schritte für diese Option ausführen zu können.

- Option 2: [vorab Bereitstellen eines VCO für eine Cluster Rolle](#prestage-a-vco-for-a-clustered-role). Verwenden Sie diese Option, wenn aufgrund von Anforderungen in der Organisation Konten für Clusterrollen vorab bereitgestellt werden müssen. Beispielsweise kann es sein, dass Sie die Benennungskonvention steuern möchten, oder steuern möchten, welche Clusterrollen erstellt werden.

>[!NOTE]
>Sie müssen mindestens Mitglied der Gruppe **Konten-Operatoren** oder einer entsprechenden Gruppe sein, um die Schritte für diese Option ausführen zu können.

### <a name="grant-the-cno-permissions-to-the-ou"></a>Erteilen der CNO-Berechtigungen für die Organisationseinheit

1. Stellen Sie in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; sicher, dass im Menü **Ansicht** die Option **Erweiterte Features** ausgewählt ist.
2. Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, in der Sie das CNO in [Schritt 1: vorab Bereitstellen des CNO in AD DS](#step-1-prestage-the-cno-in-ad-ds)erstellt haben, und wählen Sie dann **Eigenschaften**.
3. Wählen Sie auf der Registerkarte **Sicherheit** die Option **erweitert**aus.
4. Wählen Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen** die Option **Hinzufügen**aus.
5. Klicken Sie neben **Prinzipal**auf **Prinzipal auswählen**.
6. Wählen Sie im Dialogfeld **Benutzer, Computer, Dienst Konto oder Gruppen auswählen** die **Objekttypen**aus, aktivieren Sie das Kontrollkästchen **Computer** , und klicken Sie dann auf **OK**.
7. Geben Sie unter **Geben Sie die zu ausgewäfenden Objektnamen**ein den Namen des CNO ein, wählen Sie **Namen überprüfen**aus, und klicken Sie dann auf **OK**. Wählen Sie als Antwort auf die Warnmeldung, die besagt, dass Sie im Begriff sind, ein deaktiviertes Objekt hinzuzufügen, **OK**aus.
8. Stellen Sie im Dialogfeld **Berechtigungseintrag** sicher, dass die Liste **Typ** auf **Zulassen** und die Liste **Anwenden auf** auf **Dieses und alle untergeordneten Objekte** festgelegt ist.
9. Aktivieren Sie unter **Berechtigungen** das Kontrollkästchen **Computerobjekte erstellen**.

   ![Erteilen der Berechtigung zum Erstellen von Computerobjekten für das CNO](media/prestage-cluster-adds/granting-create-computer-objects-permission-to-the-cno.png)

   **Abbildung 3. Erteilen der Berechtigung zum Erstellen von Computer Objekten für das CNO**
10. Wählen Sie **OK** , bis Sie zum Active Directory Benutzer-und Computer-Snap-in zurückkehren.

Ein Administrator des Failoverclusters kann jetzt Clusterrollen mit Clientzugriffspunkten erstellen und die Ressourcen online schalten.

### <a name="prestage-a-vco-for-a-clustered-role"></a>Vorab Bereitstellen eines VCO für eine Cluster Rolle

1. Stellen Sie, bevor Sie beginnen, sicher, dass Sie den Namen des Clusters und den Namen, den die Clusterrolle erhalten wird, kennen.
2. Stellen Sie in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; sicher, dass im Menü **Ansicht** die Option **Erweiterte Features** ausgewählt ist.
3. Klicken Sie unter Active Directory Benutzer und Computer mit der rechten Maustaste auf die Organisationseinheit, in der sich das CNO für den Cluster befindet, zeigen Sie auf **neu**, und wählen Sie dann **Computer**aus.
4. Geben Sie im Feld **Computer Name** den Namen ein, der für die Cluster Rolle verwendet werden soll, und klicken Sie dann auf **OK**.
5. Klicken Sie als bewährte Vorgehensweise mit der rechten Maustaste auf das gerade erstellte Computer Konto, wählen Sie **Eigenschaften**aus, und klicken Sie dann auf die Registerkarte **Objekt** . Aktivieren Sie auf der Registerkarte **Objekt** das Kontrollkästchen **Objekt vor zufälligem Löschen schützen** , und klicken Sie dann auf **OK**.
6. Klicken Sie mit der rechten Maustaste auf das gerade erstellte Computer Konto, und wählen Sie dann **Eigenschaften**aus.
7. Wählen Sie auf der Registerkarte **Sicherheit** die Option **Hinzufügen** aus.
8. Wählen Sie im Dialogfeld **Benutzer, Computer, Dienst Konto oder Gruppen auswählen** die **Objekttypen**aus, aktivieren Sie das Kontrollkästchen **Computer** , und klicken Sie dann auf **OK**.
9. Geben Sie unter **Geben Sie die zu ausgewäfenden Objektnamen**ein den Namen des CNO ein, wählen Sie **Namen überprüfen**aus, und klicken Sie dann auf **OK**. Wenn Sie eine Warnmeldung erhalten, die besagt, dass Sie im Begriff sind, ein deaktiviertes Objekt hinzuzufügen, klicken Sie auf **OK**.
10. Stellen Sie sicher, dass das CNO ausgewählt ist, und aktivieren Sie dann neben **Vollzugriff** das Kontrollkästchen **Zulassen**.
11. Klicken Sie auf **OK**.

Ein Administrator des Failoverclusters kann jetzt die Clusterrolle mit einem Clientzugriffspunkt erstellen, die dem vorab bereitgestellten VCO-Namen entspricht, und die Ressource online schalten.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclustering](failover-clustering.md)
- [Konfigurieren von Clusterkonten in Active Directory](configure-ad-accounts.md)