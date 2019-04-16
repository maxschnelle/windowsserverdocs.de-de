---
title: Vorbereiten der Cluster-Computer-Objekte in Active Directory-Domänendienste
description: Informationen zum Vorabbereitstellen von Cluster-Computer-Objekte in Active Directory-Domänendienste.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 111969b074b33764dbbf72bfb24ad606f8314e41
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082166"
---
# <a name="prestage-cluster-computer-objects-in-active-directory-domain-services"></a>Vorbereiten der Cluster-Computer-Objekte in Active Directory-Domänendienste

>Betrifft: Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2016

In diesem Thema wird die Vorgehensweise Cluster Computer-Objekte in Active Directory-Domänendienste (AD DS) vorbereiten. Dieses Verfahren können Sie um einen Benutzer oder eine Gruppe zu einen Failovercluster erstellen, wenn sie nicht über Berechtigungen zum Erstellen von Computerobjekten in AD DS verfügen zu aktivieren.

Wenn Sie einen Failovercluster mithilfe des Assistenten zum Erstellen von Cluster oder mithilfe von Windows PowerShell erstellen, müssen Sie einen Namen für den Cluster angeben. Wenn Sie beim Erstellen des Clusters über ausreichende Berechtigungen verfügen, wird der Prozess zum Erstellen eines Clusters automatisch ein Computerobjekt in AD DS, die den Namen des Clusters entspricht erstellt. Dieses Objekt wird der *clusternamensobjekt* oder CNO bezeichnet. Virtuelle Computer-Objekte (virtuellen Computerobjekte) werden über das Clusternetzwerkobjekt automatisch erstellt, beim Konfigurieren von gruppierter Rollen, die Clientzugriffspunkte verwenden. Beispielsweise, wenn Sie einen hochverfügbare Dateiserver mit einem Client Access Point mit dem Namen *FileServer1*erstellen, wird das Clusternetzwerkobjekt entsprechende VCO in AD DS erstellen.

>[!NOTE]
>In Windows Server 2012 R2 besteht die Möglichkeit, einen Cluster getrennt von Active Directory erstellen möchten, auf dem keine CNO oder virtuellen Computerobjekte in AD DS erstellt werden. Dies ist für bestimmte Arten von Cluster-Bereitstellungen geplant. Weitere Informationen finden Sie unter [Bereitstellen eines Clusters Active Directory-Detached](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v%3dws.11)>).

Um das Clusternetzwerkobjekt automatisch zu erstellen, muss der Benutzer, der den Failovercluster erstellt, die Berechtigung **Computerobjekte erstellen** auf die Organisationseinheit (OU) oder auf den Container, in denen die Server, die den Cluster bilden befinden. Um einen Benutzer oder eine Gruppe zum Erstellen eines Clusters ohne diese Berechtigung zu aktivieren, kann Benutzer mit entsprechenden Berechtigungen in AD DS (in der Regel ein Domänenadministrator) das Clusternetzwerkobjekt in AD DS vorbereiten. Dadurch wird auch als Domänenadministrator mehr Kontrolle über die Namenskonvention, die für den Cluster verwendet wird, und Kontrolle über die, denen ORGANISATIONSEINHEIT in der Clusterobjekte erstellt werden.

## <a name="step-1-prestage-the-cno-in-ad-ds"></a>Schritt 1: Vorbereiten des Clusternetzwerkobjekts in AD DS

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes beachten:

- Der Name, den Sie den Cluster zuweisen möchten
- Der Name des Benutzerkontos oder der Gruppe, dem Sie die Rechte zum Erstellen des Clusters gewähren möchten

Als bewährte Methode wird empfohlen, eine Organisationseinheit für die Clusterobjekte zu erstellen. Wenn eine Organisationseinheit bereits vorhanden ist, dass Sie verwenden möchten, ist die Mitgliedschaft in der Gruppe **Konten-Operatoren** mindestens erforderlich, um diesen Schritt abzuschließen. Wenn Sie eine Organisationseinheit für die Clusterobjekte erstellen müssen, ist Mitglied der Gruppe **Domänen-Admins** oder einer ähnlichen mindestens erforderlich, um diesen Schritt abzuschließen.

>[!NOTE]
>Wenn Sie das Clusternetzwerkobjekt im Container Standardcomputers anstelle einer Organisationseinheit erstellen, müssen Sie keinen Schritt 3 dieses Themas ausführen. In diesem Szenario kann Clusteradministrator bis zu 10 virtuellen Computerobjekte ohne zusätzliche Konfiguration erstellen.

### <a name="prestage-the-cno-in-ad-ds"></a>Vorbereiten des Clusternetzwerkobjekts in AD DS

1. Öffnen Sie auf einem Computer, der AD DS-Tools aus der Remoteserver-Verwaltungstools installiert sind, oder auf einem Domänencontroller **Active Directory-Benutzer und -Computer**. Klicken Sie hierzu auf einem Server starten Sie den Server Manager, und wählen Sie dann im Menü **Extras** aus **Active Directory-Benutzer und-Computer**.
2. Zum Erstellen einer Organisationseinheit für den Cluster Computer-Objekte, mit der rechten Maustaste den Domänennamen oder eine vorhandene Organisationseinheit, zeigen Sie auf **neu**, und wählen Sie dann auf **Organisationseinheit**. Geben Sie im Feld **Name** den Namen der Organisationseinheit, und wählen Sie dann auf **OK**.
3. In der Konsolenstruktur mit der rechten Maustaste der Organisationseinheit, in dem das Clusternetzwerkobjekt erstellen, zeigen Sie auf **neu**, und wählen Sie dann auf **Computer**werden soll.
4. Geben Sie im Feld **Name des Computers** den Namen, der für den Failovercluster verwendet werden, und wählen Sie dann auf **OK**.

  >[!NOTE]
  >Dies ist der Clustername, die der Benutzer, der den Cluster erstellt auf der Seite **Zum Verwalten des Clusters Zugriffspunkt** im Cluster erstellen-Assistenten oder als Wert des angeben, wird die *– Name* -Parameter für das **New-Cluster** Windows PowerShell Cmdlet.

5. Es empfiehlt sich mit der rechten Maustaste in des Computerkontos an, dem Sie gerade erstellt haben, wählen Sie **Eigenschaften**aus, und wählen Sie dann auf der Registerkarte **Objekt** . Klicken Sie auf der Registerkarte **Objekt** aktivieren Sie das Kontrollkästchen **Protect-Objekt vor versehentlichem Löschen** , und wählen Sie dann auf **OK**.
6. Maustaste auf das Computerkonto, das Sie gerade erstellt haben, und wählen Sie dann auf **Konto deaktivieren**. Wählen Sie **Ja,** um zu bestätigen, und wählen Sie dann auf **OK**.

  >[!NOTE]
  >Deaktivieren Sie das Konto, so dass während der Erstellung des Clusters, der Prozess zum Erstellen eines Clusters bestätigen kann, dass das Konto nicht von einem vorhandenen Computer oder Cluster in der Domäne verwendet wird.

![Deaktivierte CNO im Beispiel-OU-Clustern](media/prestage-cluster-adds/disabled-cno-in-the-example-clusters-ou.png)

**Abbildung1. Deaktivierte CNO im Beispiel-OU-Clustern**

## <a name="step-2-grant-the-user-permissions-to-create-the-cluster"></a>Schritt 2: Erteilen Sie die Berechtigungen eines Benutzers Erstellen des Clusters

Sie müssen Berechtigungen konfigurieren, so dass das Benutzerkonto, das zum Erstellen des Failoverclusters verwendet wird Vollzugriff auf das Clusternetzwerkobjekt verfügt.

Mitgliedschaft in der Gruppe **Konten-Operatoren** ist die Mindestanforderung zum Ausführen dieses Schritts.

So erteilen Sie die Berechtigungen eines Benutzers Erstellen des Clusters funktioniert:

1. Active Directory-Benutzer und-Computer im Menü **Ansicht** stellen Sie sicher, dass **Erweiterte Funktionen** aktiviert ist.
2. Suchen und anschließend mit der Maustaste das CNO, und wählen Sie dann **Eigenschaften**aus.
3. Wählen Sie auf der Registerkarte **Sicherheit** **Hinzufügen**aus.
4. Klicken Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das Benutzerkonto oder die Gruppe an, die Sie Berechtigungen erteilen möchten, und wählen Sie dann auf **OK**.
5. Wählen Sie das Benutzerkonto oder die Gruppe, die Sie soeben hinzugefügt haben, und wählen Sie dann das Kontrollkästchen **Zulassen** neben **Vollzugriff**.
  
  ![Erteilen von Vollzugriff an den Benutzer oder die Gruppe, die den Cluster erstellen](media/prestage-cluster-adds/granting-full-control-to-the-user-create-the-cluster.png)
  
  **Abbildung2. Erteilen von Vollzugriff an den Benutzer oder die Gruppe, die den Cluster erstellen**
6. Wählen Sie **OK** aus.

Nachdem Sie diesen Schritt abgeschlossen haben, kann der Benutzer, die Sie die Berechtigungen erteilt Failovercluster erstellen. Jedoch das Clusternetzwerkobjekt in einer Organisationseinheit befindet, kann nicht der Benutzer erstellen gruppierte Rollen, die einen Client Access Point erfordern erst nach Abschluss von Schritt 3.

>[!NOTE]
>Wenn das Clusternetzwerkobjekt im Container Standardcomputers ist, kann Clusteradministrator bis zu 10 virtuellen Computerobjekte ohne zusätzliche Konfiguration erstellen. Wenn mehr als 10 virtuellen Computerobjekte hinzufügen möchten, müssen Sie die Berechtigung **Erstellen von Computerobjekten** explizit auf dem Clusternamensobjekt für den Container Computer gewähren.

## <a name="step-3-grant-the-cno-permissions-to-the-ou-or-prestage-vcos-for-clustered-roles"></a>Schritt 3: Erteilen von Berechtigungen für das CNO für der Organisationseinheit oder Vorabbereitstellen virtuellen Computerobjekte für gruppierte Rollen

Beim Erstellen einer gruppierten Rolle mit einem Client Access Point erstellt Cluster VCO in derselben Organisationseinheit wie das Clusternetzwerkobjekt. Für diese Funktion automatisch ausgeführt wird muss das Clusternetzwerkobjekt Berechtigungen zum Erstellen von Computerobjekten in der Organisationseinheit verfügen.

Wenn Sie das Clusternetzwerkobjekt in AD DS vorbereitet haben, können Sie zum virtuellen Computerobjekte erstellen die folgenden Möglichkeiten:

- Option 1: [Erteilen von Berechtigungen für das CNO für die Organisationseinheit](#grant-the-cno-permissions-to-the-ou). Wenn Sie diese Option verwenden, kann der Cluster virtuellen Computerobjekte in AD DS automatisch erstellt. Aus diesem Grund kann ein Administrator für den Failovercluster ohne anfordern, dass Sie die virtuellen Computerobjekte in AD DS Vorabbereitstellen gruppierte Rollen erstellen.

>[!NOTE]
>Mitgliedschaft in der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe ist mindestens erforderlich, um die Schritte für diese Option ausführen.

- Option 2: [Prestage VCO für eine gruppierte Rolle](#prestage-a-vco-for-the-clustered-role). Verwenden Sie diese Option aus, wenn es zum Vorbereiten von Benutzerkonten für gruppierte Rollen aufgrund von Anforderungen in Ihrer Organisation erforderlich ist. Beispiel: Sie möchten Steuern der Namenskonvention oder Steuerelement die gruppierten Rollen erstellt werden.

>[!NOTE]
>Mitgliedschaft in der Gruppe **Konten-Operatoren** ist mindestens erforderlich, um die Schritte für diese Option ausführen.

### <a name="grant-the-cno-permissions-to-the-ou"></a>Erteilen von Berechtigungen für das CNO für der Organisationseinheit

1. Active Directory-Benutzer und-Computer im Menü **Ansicht** stellen Sie sicher, dass **Erweiterte Funktionen** aktiviert ist.
2. Mit der rechten Maustaste in der Organisationseinheit, die Sie erstellt, in dem das Clusternetzwerkobjekt in haben [Schritt 1: Vorbereiten des Clusternetzwerkobjekts in AD DS](#step-1:-prestage-the-CNO-in-ad-ds), und wählen Sie dann **Eigenschaften**aus.
3. Wählen Sie auf der Registerkarte **Sicherheit** **Erweitert**.
4. Wählen Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen** **Hinzufügen**aus.
5. Wählen Sie neben **Prinzipal** **Wählen Sie aus einem Prinzipal**.
6. Klicken Sie im Dialogfeld **Benutzer, Computer, Dienstkonto oder Gruppen** wählen Sie **Objekttypen**, aktivieren Sie das Kontrollkästchen **Computer** und wählen Sie dann auf **OK**.
7. Klicken Sie unter **Geben Sie die zu verwendenden Objektnamen ein**Geben Sie den Namen des Clusternetzwerkobjekts, wählen Sie **Namen überprüfen**und wählen Sie dann auf **OK**. Als Antwort auf die Warnung, die besagt, die sind Sie dabei, ein deaktiviertes Objekt hinzufügen, wählen Sie **OK**aus.
8. Klicken Sie im Dialogfeld **Berechtigungseintrag** stellen Sie sicher, dass die Liste **Typ** auf **Zulassen**festgelegt ist, und die Liste **betrifft** auf **dieses Objekt und alle untergeordneten Objekte**festgelegt ist.
9. Aktivieren Sie unter **Berechtigungen**das Kontrollkästchen **Computerobjekte erstellen** .

  ![Erteilen von dem Computer erstellen Objekte Berechtigungen für dem Clusternetzwerkobjekt](media/prestage-cluster-adds/granting-create-computer-objects-permission-to-the-cno.png)

  **Abbildung3. Erteilen von dem Computer erstellen Objekte Berechtigungen für dem Clusternetzwerkobjekt**
10. Wählen Sie **OK** aus, bis Sie Active Directory-Benutzer und Computer-Snap-in.

Ein Administrator auf dem Failovercluster kann jetzt gruppierte Rollen mit Client Zugriffspunkte erstellen und die Ressourcen online schalten.

### <a name="prestage-a-vco-for-a-clustered-role"></a>Vorabbereitstellen Sie VCO für eine gruppierte Rolle

1. Bevor Sie beginnen, stellen Sie sicher, dass Sie den Namen des Clusters und den Namen, die die Rolle gruppierte kennen.
2. Active Directory-Benutzer und-Computer im Menü **Ansicht** stellen Sie sicher, dass **Erweiterte Funktionen** aktiviert ist.
3. In Active Directory-Benutzer und-Computer mit der rechten Maustaste in der Organisationseinheit, in dem Clusternamensobjekt für den Cluster gespeichert ist, zeigen Sie auf **neu**, und wählen Sie dann auf **Computer**.
4. Geben Sie im Feld **Name des Computers** den Namen, den Sie für die gruppierten Rolle verwenden, und wählen Sie dann auf **OK**.
5. Es empfiehlt sich mit der rechten Maustaste in des Computerkontos an, dem Sie gerade erstellt haben, wählen Sie **Eigenschaften**aus, und wählen Sie dann auf der Registerkarte **Objekt** . Klicken Sie auf der Registerkarte **Objekt** aktivieren Sie das Kontrollkästchen **Protect-Objekt vor versehentlichem Löschen** , und wählen Sie dann auf **OK**.
6. Maustaste auf das Computerkonto, das Sie gerade erstellt haben, und wählen Sie dann **Eigenschaften**aus.
7. Wählen Sie auf der Registerkarte **Sicherheit** **Hinzufügen**aus.
8. Klicken Sie im Dialogfeld **Benutzer, Computer, Dienstkonto oder Gruppen** wählen Sie **Objekttypen**, aktivieren Sie das Kontrollkästchen **Computer** und wählen Sie dann auf **OK**.
9. Klicken Sie unter **Geben Sie die zu verwendenden Objektnamen ein**Geben Sie den Namen des Clusternetzwerkobjekts, wählen Sie **Namen überprüfen**und wählen Sie dann auf **OK**. Wenn Sie eine Warnung, die besagt erhalten, dass Sie haben ein deaktiviertes Objekt hinzuzufügen, wählen Sie **OK**aus.
10. Stellen Sie sicher, dass das Clusternetzwerkobjekt ausgewählt ist, und wählen Sie dann das Kontrollkästchen **Zulassen** neben **Vollzugriff**.
11. Wählen Sie **OK** aus.

Ein Administrator auf dem Failovercluster kann jetzt erstellen Sie die gruppierte Rolle mit einem Client Access Point, der den Namen der Vorstufe VCO entspricht und schalten Sie die Ressource online.

## <a name="more-information"></a>Weitere Informationen

- [Failoverclustering](failover-clustering.md)