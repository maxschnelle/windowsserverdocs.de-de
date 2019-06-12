---
title: Vorabbereitstellen von clustercomputerobjekten in Active Directory Domain Services
description: Informationen zum Vorabbereitstellen von clustercomputerobjekten in Active Directory Domain Services.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.manager: daveba
ms.technology: storage-failover-clustering
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: fa240ba5fedd98f16639dd19fb8f22c10bfdd9ac
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442460"
---
# <a name="prestage-cluster-computer-objects-in-active-directory-domain-services"></a>Vorabbereitstellen von clustercomputerobjekten in Active Directory Domain Services

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird gezeigt, wie Sie Clustercomputerobjekte in den Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) vorab bereitstellen. Sie können mit diesem Verfahren Benutzern oder Gruppen, die nicht über Berechtigungen zum Erstellen von Computerobjekten in AD DS verfügen, das Erstellen eines Failoverclusters ermöglichen.

Beim Erstellen eines Failoverclusters mit dem Clustererstellungs-Assistenten oder mit Windows PowerShell müssen Sie einen Namen für den Cluster angeben. Wenn Sie beim Erstellen des Clusters über ausreichende Berechtigungen verfügen, wird automatisch in AD DS ein Computerobjekt erstellt, das den gleichen Namen hat wie der Cluster. Dieses Objekt wird als *Clusternamenobjekt* oder CNO bezeichnet. Über das CNO werden automatisch virtuelle Computerobjekte (VCOs) erstellt, wenn Sie Clusterrollen konfigurieren, von denen Clientzugriffspunkte verwendet werden. Wenn Sie beispielsweise einen hoch verfügbaren Dateiserver mit einem Clientzugriffspunkt mit dem Namen *Dateiserver1*erstellen, wird vom CNO ein entsprechendes VCO in AD DS erstellt.

>[!NOTE]
>Es ist die Möglichkeit, einen Active Directory getrennten Cluster erstellen, in denen keine CNOS oder VCOs in AD DS erstellt werden. Diese Möglichkeit ist für bestimmte Typen von Clusterbereitstellungen gedacht. Weitere Informationen finden Sie unter [Bereitstellen eines von Active Directory getrennten Clusters](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v%3dws.11)>).

Für die automatische Erstellung des CNOs benötigt der Benutzer, der den Failovercluster erstellt, die Berechtigung **Computerobjekte erstellen** für die Organisationseinheit (Organizational Unit, OU) oder den Container, in dem sich die Server befinden, aus denen der Cluster gebildet werden soll. Ein Benutzer mit entsprechenden Berechtigungen in AD DS (normalerweise ein Domänenadministrator) kann das CNO vorab in AD DS bereitstellen, damit ein Benutzer oder eine Gruppe ohne diese Berechtigung einen Cluster erstellen kann. Dadurch hat der Domänenadministrator außerdem mehr Kontrolle über die für den Cluster verwendete Benennungskonvention sowie darüber, in welcher Organisationseinheit die Clusterobjekte erstellt werden.

## <a name="step-1-prestage-the-cno-in-ad-ds"></a>Schritt 1: Vorabbereitstellen des CNOS in AD DS

Bevor Sie beginnen, sollten Sie sicherstellen, dass folgende Informationen vorhanden sind:

- Der Name, der dem Cluster zuweisen möchten.
- Der Name des Benutzerkontos oder der Gruppe, die Sie Rechte zum Erstellen des Clusters erteilen möchten

Als bewährte Methode wird empfohlen, eine Organisationseinheit für die Clusterobjekte zu erstellen. Wenn bereits eine Organisationseinheit vorhanden ist, die Sie verwenden möchten, ist zum Ausführen dieses Schritts mindestens die Mitgliedschaft in der Gruppe **Konten-Operatoren** erforderlich. Wenn Sie eine Organisationseinheit für die Clusterobjekte erstellen, müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um diesen Schritt auszuführen.

>[!NOTE]
>Wenn Sie das CNO im Standardcontainer %%amp;quot;Computer%%amp;quot; anstatt in einer Organisationseinheit erstellen, müssen Sie Schritt 3 dieses Themas nicht ausführen. In diesem Szenario kann ein Clusteradministrator bis zu zehn VCOs ohne zusätzliche Konfiguration erstellen.

### <a name="prestage-the-cno-in-ad-ds"></a>Vorabbereitstellen des CNOS in AD DS

1. Öffnen Sie auf einem Computer, auf dem die AD DS-Tools aus den Remoteserver-Verwaltungstools installiert sind, oder auf einem Domänencontroller das Snap-In **Active Directory-Benutzer und -Computer**. Starten Sie dazu auf einem Server, Server-Manager, und klicken Sie dann auf die **Tools** , wählen Sie im Menü **Active Directory-Benutzer und-Computer**.
2. Klicken Sie zum Erstellen einer Organisationseinheit für die clustercomputerobjekte, mit der rechten Maustaste den Domänennamen oder eine vorhandene Organisationseinheit, zeigen Sie auf **neu**, und wählen Sie dann **Organisationseinheit**. In der **Namen** Feld Geben Sie den Namen der Organisationseinheit, und wählen Sie dann **OK**.
3. In der Konsolenstruktur mit der Maustaste der Organisationseinheit, in dem Sie das CNO erstellen möchten zeigen Sie **neu**, und wählen Sie dann **Computer**.
4. In der **Computername** Geben Sie den Namen für den Failovercluster verwendet werden, und wählen Sie dann **OK**.

   >[!NOTE]
   >Diesen Clusternamen gibt der Benutzer, der den Cluster erstellt, auf der Seite **Zugriffspunkt für die Clusterverwaltung** im Clustererstellungs-Assistenten oder als Wert des *–Name* -Parameters für das Windows PowerShell-Cmdlet **New-Cluster** an.

5. Als bewährte Methode, die Maustaste Computerkontos ein, das Sie gerade erstellt haben, wählen **Eigenschaften**, und wählen Sie dann die **Objekt** Registerkarte. Auf der **Objekt** Registerkarte die **schützen Objekt vor zufälligem Löschen** aus, und wählen Sie dann **OK**.
6. Maustaste auf das Computerkonto, die Sie gerade ein erstellt, und wählen Sie dann **Disable Account**. Wählen Sie **Ja** zu bestätigen, und wählen Sie dann **OK**.

   >[!NOTE]
   >Sie müssen das Konto deaktivieren, damit bei der Clustererstellung überprüft werden kann, ob das Konto zurzeit von einem vorhandenen Computer oder Cluster in der Domäne verwendet wird.

![Deaktiviertes CNO in der Beispielorganisationseinheit %%amp;quot;Cluster%%amp;quot;](media/prestage-cluster-adds/disabled-cno-in-the-example-clusters-ou.png)

**Abbildung 1. Deaktiviertes CNO im Beispiel Cluster%**

## <a name="step-2-grant-the-user-permissions-to-create-the-cluster"></a>Schritt 2: Gewähren Sie die Benutzerberechtigungen zum Erstellen des Clusters

Sie müssen Berechtigungen konfigurieren, damit das Benutzerkonto, das zum Erstellen des Failoverclusters verwendet wird, über Vollzugriff auf das gerade erstellte CNO verfügt:

Sie müssen mindestens Mitglied der Gruppe **Konten-Operatoren** sein, um diesen Schritt ausführen zu können.

So wird die Benutzerberechtigungen zum Erstellen des Clusters zu gewähren:

1. Stellen Sie in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; sicher, dass im Menü **Ansicht** die Option **Erweiterte Features** ausgewählt ist.
2. Suchen Sie per Rechtsklick das CNO, und wählen Sie dann **Eigenschaften**.
3. Auf der **Sicherheit** Registerkarte **hinzufügen**.
4. In der **Auswahl von Benutzern, Computern oder Gruppen** Dialogfeld geben die Benutzer- oder Gruppenkonto, das Sie verwenden möchten, Erteilen von Berechtigungen für, und wählen Sie dann **OK**.
5. Wählen Sie das gerade hinzugefügte Benutzerkonto bzw. die gerade hinzugefügte Gruppe aus, und aktivieren Sie dann neben **Vollzugriff**das Kontrollkästchen **Zulassen** .
  
   ![Erteilen der Benutzer- oder Gruppenberechtigungen zum Erstellen des Clusters](media/prestage-cluster-adds/granting-full-control-to-the-user-create-the-cluster.png)
  
   **Abbildung 2. Gewähren Sie volle Kontrolle für den Benutzer oder Gruppe, die den Cluster erstellen**
6. Wählen Sie **OK**.

Nach Abschluss dieses Schritts kann der Benutzer, dem Sie Berechtigungen erteilt haben, den Failovercluster erstellen. Wenn sich das CNO jedoch in einer Organisationseinheit befindet, kann der Benutzer erst dann Clusterrollen erstellen, für die ein Clientzugriffspunkt erforderlich ist, wenn Sie Schritt 3 abgeschlossen haben.

>[!NOTE]
>Wenn sich das CNO im Standardcontainer %%amp;quot;Computer%%amp;quot; befindet, kann ein Clusteradministrator bis zu zehn VCOs ohne zusätzliche Konfiguration erstellen. Zum Hinzufügen von mehr als zehn VCOs müssen Sie explizit die Berechtigung **Computerobjekte erstellen** für das CNO für den Container %%amp;quot;Computer%%amp;quot; erteilen.

## <a name="step-3-grant-the-cno-permissions-to-the-ou-or-prestage-vcos-for-clustered-roles"></a>Schritt 3: Erteilen der CNO-Berechtigungen für der Organisationseinheit oder Vorabbereitstellen von VCOs für clusterrollen

Wenn Sie eine Clusterrolle mit einem Clientzugriffspunkt erstellen, wird vom Cluster ein VCO in der gleichen Organisationseinheit erstellt, in der sich das CNO befindet. Damit dies automatisch geschieht, muss das CNO über Berechtigungen zum Erstellen von Computerobjekten in der Organisationseinheit verfügen.

Wenn Sie das CNO vorab in AD DS bereitgestellt haben, können Sie eine der folgenden Aktionen ausführen, um VCOs zu erstellen:

- Option 1: [Erteilen die CNO-Berechtigungen für der Organisationseinheit](#grant-the-cno-permissions-to-the-ou). Wenn Sie diese Option verwenden, können vom Cluster automatisch VCOs in AD DS erstellt werden. Daher kann ein Administrator für den Failovercluster Clusterrollen erstellen und muss Sie dazu nicht bitten, VCOs vorab in AD DS bereitstellen.

>[!NOTE]
>Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um die Schritte für diese Option ausführen zu können.

- Option 2: [Ein VCO für eine Clusterrolle vorab bereitstellen,](#prestage-a-vco-for-a-clustered-role). Verwenden Sie diese Option, wenn aufgrund von Anforderungen in der Organisation Konten für Clusterrollen vorab bereitgestellt werden müssen. Beispielsweise kann es sein, dass Sie die Benennungskonvention steuern möchten, oder steuern möchten, welche Clusterrollen erstellt werden.

>[!NOTE]
>Sie müssen mindestens Mitglied der Gruppe **Konten-Operatoren** oder einer entsprechenden Gruppe sein, um die Schritte für diese Option ausführen zu können.

### <a name="grant-the-cno-permissions-to-the-ou"></a>Erteilen der CNO-Berechtigungen für der Organisationseinheit

1. Stellen Sie in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; sicher, dass im Menü **Ansicht** die Option **Erweiterte Features** ausgewählt ist.
2. Mit der rechten Maustaste in der Organisationseinheit, in dem Erstellung des CNOS in [Schritt 1: Vorabbereitstellen des CNOS in AD DS](#step-1-prestage-the-cno-in-ad-ds), und wählen Sie dann **Eigenschaften**.
3. Auf der **Sicherheit** Registerkarte **erweitert**.
4. In der **Advanced Security Settings** wählen Sie im Dialogfeld **hinzufügen**.
5. Neben **Principal**Option **Prinzipal auswählen**.
6. In der **Select User, Computer, Dienstkonto oder Gruppen** wählen Sie im Dialogfeld **Objekttypen**, wählen die **Computer** aus, und wählen Sie dann **OK** .
7. Klicken Sie unter **Geben Sie die zu verwendenden Objektnamen**, geben Sie den Namen des CNOS, wählen Sie **Namen überprüfen**, und wählen Sie dann **OK**. Wählen Sie in der Antwort auf die Warnmeldung, die besagt, dass Sie sind dabei, das ein deaktiviertes Objekt hinzuzufügen, **OK**.
8. Stellen Sie im Dialogfeld **Berechtigungseintrag** sicher, dass die Liste **Typ** auf **Zulassen** und die Liste **Anwenden auf** auf **Dieses und alle untergeordneten Objekte** festgelegt ist.
9. Aktivieren Sie unter **Berechtigungen** das Kontrollkästchen **Computerobjekte erstellen**.

   ![Erteilen der Berechtigung zum Erstellen von Computerobjekten für das CNO](media/prestage-cluster-adds/granting-create-computer-objects-permission-to-the-cno.png)

   **Abbildung 3. Erteilen der Berechtigung zum Erstellen von Computerobjekten, dem Clusternamenobjekt**
10. Wählen Sie **OK** bis Sie die Active Directory-Benutzer und Computer-Snap-in.

Ein Administrator des Failoverclusters kann jetzt Clusterrollen mit Clientzugriffspunkten erstellen und die Ressourcen online schalten.

### <a name="prestage-a-vco-for-a-clustered-role"></a>Bereitstellen Sie ein VCO für eine Clusterrolle vorab

1. Stellen Sie, bevor Sie beginnen, sicher, dass Sie den Namen des Clusters und den Namen, den die Clusterrolle erhalten wird, kennen.
2. Stellen Sie in %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; sicher, dass im Menü **Ansicht** die Option **Erweiterte Features** ausgewählt ist.
3. In Active Directory-Benutzer und Computer, mit der Maustaste der Organisationseinheit, in dem das CNO für den Cluster befindet, zeigen Sie auf **neu**, und wählen Sie dann **Computer**.
4. In der **Computername** Geben Sie den Namen, die Sie für die Clusterrolle, und wählen Sie dann **OK**.
5. Als bewährte Methode, die Maustaste Computerkontos ein, das Sie gerade erstellt haben, wählen **Eigenschaften**, und wählen Sie dann die **Objekt** Registerkarte. Auf der **Objekt** Registerkarte die **schützen Objekt vor zufälligem Löschen** aus, und wählen Sie dann **OK**.
6. Maustaste auf das Computerkonto, die Sie gerade ein erstellt, und wählen Sie dann **Eigenschaften**.
7. Auf der **Sicherheit** Registerkarte **hinzufügen**.
8. In der **Select User, Computer, Dienstkonto oder Gruppen** wählen Sie im Dialogfeld **Objekttypen**, wählen die **Computer** aus, und wählen Sie dann **OK** .
9. Klicken Sie unter **Geben Sie die zu verwendenden Objektnamen**, geben Sie den Namen des CNOS, wählen Sie **Namen überprüfen**, und wählen Sie dann **OK**. Wenn Sie eine Warnung angezeigt, die besagt werden, dass Sie sind im Begriff, ein deaktiviertes Objekt hinzuzufügen, wählen Sie **OK**.
10. Stellen Sie sicher, dass das CNO ausgewählt ist, und aktivieren Sie dann neben **Vollzugriff** das Kontrollkästchen **Zulassen**.
11. Wählen Sie **OK**.

Ein Administrator des Failoverclusters kann jetzt die Clusterrolle mit einem Clientzugriffspunkt erstellen, die dem vorab bereitgestellten VCO-Namen entspricht, und die Ressource online schalten.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclustering](failover-clustering.md)
- [Konfigurieren von Clusterkonten in Active Directory](configure-ad-accounts.md)