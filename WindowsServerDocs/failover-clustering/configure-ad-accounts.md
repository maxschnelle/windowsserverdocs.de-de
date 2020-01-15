---
title: Konfigurieren von Clusterkonten in Active Directory
ms.date: 11/12/2012
ms.prod: windows-server
ms.technology: storage-failover-clustering
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 47f3a515379eb79f628a0ee97ef2c7965c4d8d50
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948154"
---
# <a name="configuring-cluster-accounts-in-active-directory"></a>Konfigurieren von Clusterkonten in Active Directory

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008

Wenn Sie in Windows Server einen Failovercluster erstellen und geclusterte Dienste oder Anwendungen konfigurieren, erstellen die Failovercluster-Assistenten die erforderlichen Active Directory Computer Konten (auch Computer Objekte genannt) und stellen Ihnen bestimmte Berechtigungen zur Verfügung. Die Assistenten erstellen ein Computerkonto für den Cluster (dieses Konto wird auch als das Clusternamenobjekt oder CNO bezeichnet) und ein Computerkonto für die meisten Typen von geclusterten Diensten und Anwendungen, mit Ausnahme des virtuellen Hyper-V-Computers. Die Berechtigungen für diese Konten werden von den Failovercluster-Assistenten automatisch festgelegt. Wenn die Berechtigungen geändert wurden, müssen sie wieder zurückgesetzt werden, damit sie den Clusteranforderungen entsprechen. In dieser Anleitung werden diese Active Directory-Konten und -Berechtigungen beschrieben, Hintergrundinformationen dazu bereitgestellt, warum sie wichtig sind, und Schritte zum Konfigurieren und Verwalten der Konten beschrieben.
      

## <a name="overview-of-active-directory-accounts-needed-by-a-failover-cluster"></a>Übersicht über Active Directory-Konten, die von einem Failovercluster benötigt werden

In diesem Abschnitt werden die Active Directory-Computerkonten (auch als Active Directory-Computerobjekte bezeichnet) beschrieben, die für einen Failovercluster wichtig sind. Dabei handelt es sich um die folgenden Konten:

  - **Das Benutzerkonto, das zum Erstellen des Clusters verwendet wird.** Dies ist das Benutzerkonto, das verwendet wird, um den Clustererstellungs-Assistenten zu starten. Das Konto ist wichtig, da es die Grundlage bereitstellt, auf der ein Computerkonto für den Cluster erstellt wird.  
      
  - **Das Cluster Namen Konto.** (das Computer Konto des Clusters selbst, auch als Cluster Namen Objekt oder CNO bezeichnet). Dieses Konto wird automatisch vom Clustererstellungs-Assistenten erstellt und hat den gleichen Namen wie der Cluster. Das Clusternamenkonto ist sehr wichtig, da über dieses Konto andere Konten automatisch erstellt werden, wenn Sie neue Dienste und Anwendungen auf dem Cluster konfigurieren. Wenn das Clusternamenkonto gelöscht wird oder dem Konto Berechtigungen entzogen werden, können erst dann wieder andere für den Cluster erforderliche Konten erstellt werden, wenn das Clusternamenkonto wiederhergestellt bzw. die entsprechenden Berechtigungen wieder erteilt wurden.  
      
    Wenn Sie beispielsweise einen Cluster mit dem Namen Cluster1 erstellen und dann versuchen, in dem Cluster einen Clusterdruckerserver mit dem Namen PrintServer1 zu konfigurieren, muss das Konto Cluster1 in Active Directory die erforderlichen Berechtigungen beibehalten, damit es verwendet werden kann, um ein Computerkonto mit dem Namen PrintServer1 zu erstellen.  
      
    Das Clusternamenkonto wird im Standardcontainer für Computerkonten in Active Directory erstellt. Standardmäßig ist dies der Container "Computer", der Domänenadministrator kann es jedoch zu einem anderen Container oder einer Organisationseinheit umleiten.  
      
  - **Das Computer Konto (Computer Objekt) eines geclusterten Dienstanbieter oder einer geclusterten Anwendung.** Diese Konten werden automatisch vom Assistenten für hohe Verfügbarkeit im Rahmen der Erstellung der meisten Typen von geclusterten Diensten und Anwendungen erstellt, mit Ausnahme von virtuellen Hyper-V-Computern. Dem Cluster Namen Konto werden die erforderlichen Berechtigungen zum Steuern dieser Konten gewährt.  
      
    Wenn Sie beispielsweise über einen Cluster mit dem Namen Cluster1 verfügen und dann einen Clusterdateiserver mit dem Namen FileServer1 erstellen, erstellt der Assistent für hohe Verfügbarkeit ein Active Directory-Computerkonto mit dem Namen FileServer1. Der Assistent für hohe Verfügbarkeit erteilt dem Konto Cluster1 außerdem die erforderlichen Berechtigungen zum Steuern des FileServer1-Kontos.  
      

In der folgenden Tabelle werden die erforderlichen Berechtigungen für diese Konten beschrieben.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>„Konto“</th>
<th>Details zu Berechtigungen</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Konto zum Erstellen des Clusters</p></td>
<td><p>Erfordert Administratorberechtigungen für die Server, die Clusterknoten werden. Benötigt außerdem die Berechtigung zum Erstellen von Computerobjektenund die Berechtigung zum Lesen aller Eigenschaftenin dem Container, der in der Domäne für Computerkonten verwendet wird.</p></td>
</tr>
<tr class="even">
<td><p>Clusternamenkonto (Computerkonto des Clusters)</p></td>
<td><p>Wenn der Clustererstellungs-Assistent ausgeführt wird, erstellt er das Clusternamenkonto in dem Standardcontainer, der in der Domäne für Computerkonten verwendet wird. Standardmäßig kann das Clusternamenkonto (wie andere Computerkonten) bis zu zehn Computerkonten in der Domäne erstellen.</p>
<p>Wenn Sie das Clusternamenkonto (Clusternamenobjekt) erstellen, bevor Sie den Cluster erstellen, das Konto also vorab bereitstellen, müssen Sie diesem die Berechtigungen zum Erstellen von Computerobjektenund zum Lesen aller Eigenschaftenin dem Container erteilen, der in der Domäne für Computerkonten verwendet wird. Sie müssen das Konto außerdem deaktivieren und dem Konto <strong>Vollzugriff</strong> erteilen, das von dem Administrator verwendet wird, der den Cluster installiert. Weitere Informationen finden Sie weiter unten in dieser Anleitung unter <a href="#steps-for-prestaging-the-cluster-name-account" data-raw-source="[Steps for prestaging the cluster name account](#steps-for-prestaging-the-cluster-name-account)">Schritte für die Vorabbereitstellung des Clusternamenkontos</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Computerkonto eines geclusterten Diensts oder einer geclusterten Anwendung</p></td>
<td><p>Wenn der Assistent für hohe Verfügbarkeit ausgeführt wird (um einen neuen geclusterten Dienst oder eine neue Anwendung zu erstellen), wird in den meisten Fällen ein Computer Konto für den geclusterten Dienst oder die Anwendung in Active Directory erstellt. Dem Cluster Namen Konto werden die erforderlichen Berechtigungen zum Steuern dieses Kontos erteilt. Die Ausnahme ist ein geclusterter virtueller Hyper-V-Computer, für den kein Computer Konto erstellt wurde.</p>
<p>Wenn Sie das Computer Konto für einen geclusterten Dienst oder eine geclusterte Anwendung vorab bereitstellen, müssen Sie es mit den erforderlichen Berechtigungen konfigurieren. Weitere Informationen finden Sie weiter unten in dieser Anleitung unter <a href="#steps-for-prestaging-an-account-for-a-clustered-service-or-application" data-raw-source="[Steps for prestaging an account for a clustered service or application](#steps-for-prestaging-an-account-for-a-clustered-service-or-application)">Schritte für die Vorabbereitstellung eines Kontos für einen geclusterten Dienst oder eine geclusterte Anwendung</a>.</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> In früheren Versionen von Windows Server gab es ein Konto für die Clusterdienst. Seit Windows Server 2008 wird der Clusterdienst jedoch automatisch in einem besonderen Kontext ausgeführt, der die spezifischen Berechtigungen und Berechtigungen bereitstellt, die für den Dienst erforderlich sind (ähnlich dem lokalen Systemkontext, jedoch mit eingeschränkten Berechtigungen). Andere Konten werden jedoch wie in dieser Anleitung beschrieben benötigt. 
<br>


### <a name="how-accounts-are-created-through-wizards-in-failover-clustering"></a>Erstellen von Konten für die Failover-Clusterunterstützung mithilfe von Assistenten

Im folgenden Diagramm werden die Verwendung und die Erstellung von Computerkonten (Active Directory-Objekte) veranschaulicht, die im vorherigen Unterabschnitt beschrieben werden. Diese Konten sind von Bedeutung, wenn ein Administrator den Clustererstellungs-Assistenten ausführt und anschließend den Assistenten für hohe Verfügbarkeit ausführt (um einen geclusterten Dienst oder eine geclusterte Anwendung zu konfigurieren).

![](media/configure-ad-accounts/Cc731002.e8a7686c-9ba8-4ddf-87b1-175b7b51f65d(WS.10).gif)

Beachten Sie, dass im oben dargestellten Diagramm ein einzelner Administrator sowohl den Clustererstellungs-Assistenten als auch den Assistenten für hohe Verfügbarkeit ausführt. Dies können jedoch auch zwei verschiedene Administratoren sein, die zwei verschiedene Benutzerkonten verwenden, sofern beide Konten über ausreichende Berechtigungen verfügen. Die Berechtigungen werden weiter unten in dieser Anleitung unter Anforderungen für Failovercluster, Active Directory-Domänen und Konten ausführlicher beschrieben.

### <a name="how-problems-can-result-if-accounts-needed-by-the-cluster-are-changed"></a>Probleme, die sich durch Änderungen an den vom Cluster benötigten Konten ergeben können

Im folgenden Diagramm wird veranschaulicht, wie sich Probleme ergeben können, wenn das Clusternamenkonto (eines der für den Cluster erforderlichen Konten) geändert wird, nachdem es automatisch vom Clustererstellungs-Assistenten erstellt wurde.

![](media/configure-ad-accounts/Cc731002.beecc4f7-049c-4945-8fad-2cceafd6a4a5(WS.10).gif)

Wenn die im Diagramm gezeigte Art von Problem auftritt, wird ein bestimmtes Ereignis (1193, 1194, 1206 oder 1207) in der Ereignisanzeige protokolliert. Weitere Informationen zu diesen Ereignissen finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=118271](https://go.microsoft.com/fwlink/?linkid=118271).

Beachten Sie, dass ein ähnliches Problem mit dem Erstellen eines Kontos für einen geclusterten Dienst oder eine geclusterte Anwendung auftreten kann, wenn das domänenweite Kontingent für das Erstellen von Computerobjekten (standardmäßig 10) erreicht wurde. Wenn dies der Fall ist, könnte es sinnvoll sein, sich an den Domänenadministrator zu wenden, damit dieser das Kontingent erhöht, obwohl dies eine domänenweite Einstellung ist und nur nach gründlicher Überlegung geändert werden sollte. Außerdem sollten Sie sich erst vergewissern, dass im vorstehenden Diagramm nicht Ihre Situation beschrieben wird. Weitere Informationen finden Sie weiter unten in dieser Anleitung unter [Schritte zum Beheben von Problemen, die durch Änderungen an clusterbezogenen Active Directory-Konten verursacht wurden](#steps-for-troubleshooting-problems-caused-by-changes-in-cluster-related-active-directory-accounts).

## <a name="requirements-related-to-failover-clusters-active-directory-domains-and-accounts"></a>Anforderungen für Failovercluster, Active Directory-Domänen und Konten

Wie in den vorausgehenden drei Abschnitten beschrieben, müssen bestimmte Anforderungen erfüllt sein, bevor geclusterte Dienste und Anwendungen auf einem Failovercluster erfolgreich konfiguriert werden können. Die grundlegendsten Anforderungen betreffen den Speicherort von Clusterknoten (innerhalb einer einzigen Domäne) und die Berechtigungsstufe des Kontos für die Person, die den Cluster installiert. Wenn diese Anforderungen erfüllt sind, können die anderen vom Cluster benötigten Konten von den Failovercluster-Assistenten automatisch erstellt werden. In der folgenden Liste werden Details zu diesen grundlegenden Anforderungen aufgeführt.

  - **Knoten:** Alle Knoten müssen sich in der gleichen Active Directory Domäne befinden. (Die Domäne kann nicht auf Windows NT 4.0 basieren, das kein Active Directory einschließt.)  
      
  - **Konto der Person, die den Cluster installiert:** Die Person, die den Cluster installiert, muss ein Konto mit den folgenden Eigenschaften verwenden:  
      
      - Das Konto muss ein Domänenkonto sein. Es muss kein Domänenadministratorkonto sein. Es kann ein Domänenbenutzerkonto sein, wenn es die anderen Anforderungen in dieser Liste erfüllt.  
          
      - Das Konto muss über Administratorberechtigungen für die Server verfügen, die Clusterknoten werden sollen. Die einfachste Möglichkeit, diese Bedingung zu erfüllen, besteht darin, ein Domänenbenutzerkonto zu erstellen und dieses Konto anschließend der lokalen Gruppe Administratoren auf jedem Server hinzuzufügen, der ein Clusterknoten werden soll. Weitere Informationen finden Sie weiter unten in dieser Anleitung unter [Schritte zum Konfigurieren des Kontos für die Person, die den Cluster installiert](#steps-for-configuring-the-account-for-the-person-who-installs-the-cluster).  
          
      - Dem Konto (oder der Gruppe, deren Mitglied das Konto ist) müssen die Berechtigungen zum Erstellen von Computerobjektenund zum Lesen aller Eigenschaftenin dem Container erteilt werden, der in der Domäne für Computerkonten verwendet wird. Weitere Informationen finden Sie weiter unten in dieser Anleitung unter [Schritte zum Konfigurieren des Kontos für die Person, die den Cluster installiert](#steps-for-configuring-the-account-for-the-person-who-installs-the-cluster).  
          
      - Wenn die Organisation sich dafür entscheidet, das Clusternamenkonto (ein Computerkonto mit dem gleichen Namen wie der Cluster) vorab bereitzustellen, muss das vorab bereitgestellte Clusternamenkonto dem Konto der Person, die den Cluster installiert, die Berechtigung "Vollzugriff" erteilen. Weitere wichtige Details zur Vorabbereitstellung des Clusternamenkontos finden Sie weiter unten in dieser Anleitung unter [Schritte für die Vorabbereitstellung des Clusternamenkontos](#steps-for-prestaging-the-cluster-name-account).  
          

### <a name="planning-ahead-for-password-resets-and-other-account-maintenance"></a>Vorausplanung für Kennwortzurücksetzungen und andere Kontowartungsmaßnahmen

Die Administratoren von Failoverclustern müssen möglicherweise manchmal das Kennwort des Clusternamenkontos zurücksetzen. Für diese Aktion ist eine spezielle Berechtigung erforderlich, die Berechtigung **Kennwort zurücksetzen**. Daher hat es sich bewährt, die Berechtigungen des Clusternamenkontos zu bearbeiten (mithilfe des Snap-Ins "Active Directory-Benutzer und -Computer"), um den Administratoren des Clusters die Berechtigung **Kennwort zurücksetzen** für das Clusternamenkonto zu erteilen. Weitere Informationen finden Sie weiter unten in dieser Anleitung unter [Schritte zum Beheben von Kennwortproblemen mit dem Clusternamenkonto](#steps-for-troubleshooting-password-problems-with-the-cluster-name-account).

## <a name="steps-for-configuring-the-account-for-the-person-who-installs-the-cluster"></a>Schritte zum Konfigurieren des Kontos für die Person, die den Cluster installiert

Das Konto der Person, die den Cluster installiert, ist wichtig, da es die Grundlage bereitstellt, auf der ein Computerkonto für den Cluster erstellt wird.

Die zum Ausführen des folgenden Verfahrens minimal erforderliche Gruppenmitgliedschaft ist davon abhängig, ob Sie das Domänenkonto erstellen und ihm die erforderlichen Berechtigungen in der Domäne zuweisen oder ob Sie das (von jemand anderem erstellte) Konto lediglich der lokalen Gruppe **Administratoren** auf den Servern hinzufügen, die Knoten im Failovercluster werden sollen. Wenn die erste, die Mitgliedschaft in **Konto Operatoren** oder einer entsprechenden Gruppe, mindestens erforderlich ist, um dieses Verfahren abzuschließen. Im zweiten Fall ist lediglich die Mitgliedschaft in der lokalen Gruppe **Administratoren** auf den Servern, die Knoten im Failovercluster werden sollen, oder eine gleichwertige Mitgliedschaft erforderlich. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=83477](https://go.microsoft.com/fwlink/?linkid=83477).

#### <a name="to-configure-the-account-for-the-person-who-installs-the-cluster"></a>So konfigurieren Sie das Konto für die Person, die den Cluster installiert

1.  Erstellen Sie ein Domänenkonto für die Person, die den Cluster installiert, oder rufen Sie es ab. Bei diesem Konto kann es sich um ein Domänen Benutzerkonto oder um ein **Konto Operator** Konto handeln. Wenn Sie ein Standardbenutzer Konto verwenden, müssen Sie diesem später in diesem Verfahren einige zusätzliche Berechtigungen einräumen.

2.  Wenn das in Schritt 1 erstellte oder abgerufene Konto nicht automatisch in der lokalen Gruppe **Administratoren** auf den Computern in der Domäne enthalten ist, fügen Sie das Konto der lokalen Gruppe **Administratoren** auf den Servern hinzu, die als Knoten im Failovercluster verwendet werden sollen:
    
    1.  Klicken Sie auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Server-Manager**.  
          
    2.  Erweitern Sie in der Konsolenstruktur nacheinander **Konfiguration**, **Lokale Benutzer und Gruppen** und **Gruppen**.  
          
    3.  Klicken Sie im mittleren Bereich mit der rechten Maustaste auf **Administratoren**, klicken Sie auf **Zur Gruppe hinzufügen** und dann auf **Hinzufügen**.  
          
    4.  Geben **Sie unter Geben Sie die zu**erstellenden Objektnamen ein den Namen des Benutzerkontos ein, das in Schritt 1 erstellt oder abgerufen wurde. Wenn Sie dazu aufgefordert werden, geben Sie einen Kontonamen und ein Kennwort mit ausreichenden Berechtigungen für diese Aktion ein. Klicken Sie dann auf **OK**.  
          
    5.  Wiederholen Sie diese Schritte für jeden Server, der ein Knoten im Failovercluster werden soll.  

> [!IMPORTANT]
> Diese Schritte müssen für alle Server wiederholt werden, die Knoten im Cluster werden sollen. 
<br>


3. Wenn das in Schritt 1 erstellte oder abgerufene Konto ein Domänenadministratorkonto ist, überspringen Sie den Rest dieses Verfahrens. Erteilen Sie andernfalls dem Konto die Berechtigungen zum Erstellen von Computerobjektenund zum Lesen aller Eigenschaftenin dem Container, der in der Domäne für Computerkonten verwendet wird:
    
   1.  Klicken Sie auf einem Domänencontroller auf **Start**, auf **Verwaltung** und dann auf **Active Directory-Benutzer und -Computer**. Wenn das Dialogfeld **Benutzerkontensteuerung** eingeblendet wird, bestätigen Sie die angegebene Aktion und klicken dann auf **Weiter**.  
          
   2.  Stellen Sie sicher, dass im Menü **Ansicht** die Option **Erweiterte Funktionen** ausgewählt ist.  
          
       Wenn **Erweiterte Funktionen** ausgewählt ist, wird die Registerkarte **Sicherheit** in den Eigenschaften der Konten (Objekte) in **Active Directory-Benutzer und -Computer** angezeigt.  
          
   3.  Klicken Sie mit der rechten Maustaste auf den Standardcontainer **Computer** oder den Standardcontainer, in dem Computerkonten in der Domäne erstellt werden, und klicken Sie dann auf **Eigenschaften**. **Computer** befinden sich unter <b>Active Directory Benutzer und Computer/</b><i>Domäne-Knoten</i><b>/Computers</b>.  
          
   4.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Erweitert**.  
          
   5.  Klicken Sie auf **Hinzufügen**, geben Sie den Namen des in Schritt 1 erstellten oder abgerufenen Kontos ein, und klicken Sie dann auf **OK**.  
          
   6.  Suchen Sie im Dialogfeld **Berechtigungs Eintrag für * * * Container* die Berechtigungen zum **Erstellen von Computer Objekten** und zum **Lesen aller Eigenschaften** , und stellen Sie sicher, dass das Kontrollkästchen **zulassen** für jeden Container aktiviert ist.  
          
       ![](media/configure-ad-accounts/Cc731002.0a863ac5-2024-4f9f-8a4d-a419aff32fa0(WS.10).gif)

## <a name="steps-for-prestaging-the-cluster-name-account"></a>Schritte für die Vorabbereitstellung des Clusternamenkontos

Es ist normalerweise einfacher, wenn Sie das Clusternamenkonto nicht vorab bereitstellen, sondern das Konto beim Ausführen des Clustererstellungs-Assistenten automatisch erstellen und konfigurieren lassen. Wenn es jedoch aufgrund der Anforderungen in Ihrer Organisation notwendig ist, das Clusternamenkonto vorab bereitzustellen, verwenden Sie das folgende Verfahren.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=83477](https://go.microsoft.com/fwlink/?linkid=83477). Beachten Sie, dass Sie das gleiche Konto wie beim Erstellen des Clusters für dieses Verfahren verwenden können.

#### <a name="to-prestage-a-cluster-name-account"></a>So stellen Sie ein Clusternamenkonto vorab bereit

1.  Stellen Sie sicher, dass Sie den Namen, den der Cluster erhalten wird, und den Namen des Benutzerkontos, das von der Person verwendet wird, die den Cluster erstellt, kennen. (Beachten Sie, dass Sie dieses Konto verwenden können, um dieses Verfahren auszuführen.)

2.  Klicken Sie auf einem Domänencontroller auf **Start**, auf **Verwaltung** und dann auf **Active Directory-Benutzer und -Computer**. Wenn das Dialogfeld **Benutzerkontensteuerung** eingeblendet wird, bestätigen Sie die angegebene Aktion und klicken dann auf **Weiter**.

3.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf **Computer** oder den Standardcontainer, in dem Computerkonten in der Domäne erstellt werden. **Computer** befinden sich unter <b>Active Directory Benutzer und Computer/</b><i>Domäne-Knoten</i><b>/Computers</b>.

4.  Klicken Sie auf **Neu** und anschließend auf **Computer**.

5.  Geben Sie den Namen, der für den Failovercluster verwendet wird, oder anders gesagt, den Clusternamen, der im Clustererstellungs-Assistenten angegeben wird, ein. Klicken Sie dann auf **OK**.

6.  Klicken Sie mit der rechten Maustaste auf das Konto, das Sie gerade erstellt haben, und klicken Sie dann auf **Konto deaktivieren**. Wenn Sie zur Bestätigung Ihrer Auswahl aufgefordert werden, klicken Sie auf **Ja**.
    
    Das Konto muss deaktiviert werden, damit beim Ausführen des Clustererstellungs-Assistenten sichergestellt ist, dass das für den Cluster verwendete Konto nicht gerade von einem vorhandenen Computer oder Cluster in der Domäne verwendet wird.

7.  Stellen Sie sicher, dass im Menü **Ansicht** die Option **Erweiterte Funktionen** ausgewählt ist.
    
    Wenn **Erweiterte Funktionen** ausgewählt ist, wird die Registerkarte **Sicherheit** in den Eigenschaften der Konten (Objekte) in **Active Directory-Benutzer und -Computer** angezeigt.

8.  Klicken Sie mit der rechten Maustaste auf den Ordner, auf den Sie in Schritt 3 geklickt haben, und klicken Sie dann auf **Eigenschaften**.

9.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Erweitert**.

10. Klicken Sie auf **Hinzufügen** und dann auf **Objekttypen**, und stellen Sie sicher, dass **Computer** ausgewählt ist. Klicken Sie anschließend auf **OK**. Geben Sie anschließend unter **Geben Sie die zu verwendenden Objektnamen ein** den Namen des gerade erstellten Computerkontos ein, und klicken Sie dann auf **OK**. Wenn eine Nachricht angezeigt wird, die besagt, dass Sie im Begriff sind, ein deaktiviertes Objekt hinzuzufügen, klicken Sie auf **OK**.

11. Suchen Sie im Dialogfeld **Berechtigungs Eintrag** die Berechtigungen zum **Erstellen von Computer Objekten** und zum **Lesen aller Eigenschaften** , und stellen Sie sicher, dass das Kontrollkästchen **zulassen** für jede dieser Berechtigungen aktiviert ist.
    
    ![](media/configure-ad-accounts/Cc731002.f5977c4d-a62e-4b17-81e3-8c19ddca2078(WS.10).gif)

12. Klicken Sie auf **OK**, bis Sie zum Snap-In **Active Directory-Benutzer und -Computer** zurückgekehrt sind.

13. Wenn Sie für dieses Verfahren dasselbe Konto verwenden, das zum Erstellen des Clusters verwendet werden soll, überspringen Sie die verbleibenden Schritte. Andernfalls müssen Sie Berechtigungen konfigurieren, damit das Benutzerkonto, das zum Erstellen des Clusters verwendet wird, über Vollzugriff auf das gerade erstellte Computerkonto verfügt:
    
    1.  Stellen Sie sicher, dass im Menü **Ansicht** die Option **Erweiterte Funktionen** ausgewählt ist.  
          
    2.  Klicken Sie mit der rechten Maustaste auf das gerade erstellte Konto, und klicken Sie dann auf **Eigenschaften**.  
          
    3.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Hinzufügen**. Wenn das Dialogfeld **Benutzerkontensteuerung** eingeblendet wird, bestätigen Sie die angegebene Aktion und klicken dann auf **Weiter**.  
          
    4.  Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppen auswählen** das Benutzerkonto an, das zum Erstellen des Clusters verwendet werden soll. Klicken Sie dann auf **OK**.  
          
    5.  Stellen Sie sicher, dass das gerade hinzugefügte Benutzerkonto ausgewählt ist, und aktivieren Sie dann neben **Vollzugriff** das Kontrollkästchen **Zulassen**.  
          
        ![](media/configure-ad-accounts/Cc731002.fffaafe2-a494-498b-974c-8f9d70f7103b(WS.10).gif)

## <a name="steps-for-prestaging-an-account-for-a-clustered-service-or-application"></a>Schritte für die Vorabbereitstellung eines Kontos für einen geclusterten Dienst oder eine geclusterte Anwendung

Es ist normalerweise einfacher, wenn Sie das Computerkonto für einen geclusterten Dienst oder eine geclusterte Anwendung nicht vorab bereitstellen, sondern das Konto beim Ausführen des Assistenten für hohe Verfügbarkeit automatisch erstellen und konfigurieren lassen. Wenn es jedoch aufgrund der Anforderungen in Ihrer Organisation notwendig ist, Konten vorab bereitzustellen, verwenden Sie das folgende Verfahren.

Sie müssen mindestens Mitglied der Gruppe **Konten-Operatoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=83477](https://go.microsoft.com/fwlink/?linkid=83477).

#### <a name="to-prestage-an-account-for-a-clustered-service-or-application"></a>So stellen Sie ein Konto für einen geclusterten Dienst oder eine geclusterte Anwendung vorab bereit

1.  Stellen Sie sicher, dass Sie den Namen des Clusters und den Namen, den der geclusterte Dienst oder die geclusterte Anwendung erhalten wird, kennen.

2.  Klicken Sie auf einem Domänencontroller auf **Start**, auf **Verwaltung** und dann auf **Active Directory-Benutzer und -Computer**. Wenn das Dialogfeld **Benutzerkontensteuerung** eingeblendet wird, bestätigen Sie die angegebene Aktion und klicken dann auf **Weiter**.

3.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf **Computer** oder den Standardcontainer, in dem Computerkonten in der Domäne erstellt werden. **Computer** befinden sich unter <b>Active Directory Benutzer und Computer/</b><i>Domäne-Knoten</i><b>/Computers</b>.

4.  Klicken Sie auf **Neu** und anschließend auf **Computer**.

5.  Geben Sie den Namen ein, den Sie für den geclusterten Dienst oder die geclusterte Anwendung verwenden werden, und klicken Sie dann auf **OK**.

6.  Stellen Sie sicher, dass im Menü **Ansicht** die Option **Erweiterte Funktionen** ausgewählt ist.
    
    Wenn **Erweiterte Funktionen** ausgewählt ist, wird die Registerkarte **Sicherheit** in den Eigenschaften der Konten (Objekte) in **Active Directory-Benutzer und -Computer** angezeigt.

7.  Klicken Sie mit der rechten Maustaste auf das gerade erstellte Konto, und klicken Sie dann auf **Eigenschaften**.

8.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Hinzufügen**.

9.  Klicken Sie auf **Objekttypen**, und stellen Sie sicher, dass **Computer** ausgewählt ist. Klicken Sie anschließend auf **OK**. Geben Sie dann unter **Geben Sie die zu verwendenden Objektnamen ein** das Clusternamenkonto ein, und klicken Sie anschließend auf **OK**. Wenn eine Nachricht angezeigt wird, die besagt, dass Sie im Begriff sind, ein deaktiviertes Objekt hinzuzufügen, klicken Sie auf **OK**.

10. Stellen Sie sicher, dass das Clusternamenkonto ausgewählt ist, und aktivieren Sie dann neben **Vollzugriff** das Kontrollkästchen **Zulassen**.
    
    ![](media/configure-ad-accounts/Cc731002.2e614376-87a6-453a-81ba-90ff7ebc3fa2(WS.10).gif)

## <a name="steps-for-troubleshooting-problems-related-to-accounts-used-by-the-cluster"></a>Schritte zum Beheben von Problemen mit vom Cluster verwendeten Konten

Wenn Sie einen Failovercluster erstellen und geclusterte Dienste oder Anwendungen konfigurieren, erstellen die Failovercluster-Assistenten, wie weiter oben in dieser Anleitung beschrieben, die erforderlichen Active Directory-Konten und erteilen ihnen die passenden Berechtigungen. Wenn ein benötigtes Konto gelöscht wird oder notwendige Berechtigungen geändert werden, können sich Probleme ergeben. Die folgenden Unterabschnitte enthalten Schritte zum Beheben dieser Probleme.

  - [Schritte zur Problembehandlung von Kenn Wort Problemen mit dem Cluster Namen Konto](#steps-for-troubleshooting-password-problems-with-the-cluster-name-account)
      
  - [Schritte zur Behebung von Problemen, die durch Änderungen an Cluster bezogenen Active Directory Konten verursacht wurden](#steps-for-troubleshooting-problems-caused-by-changes-in-cluster-related-active-directory-accounts)
      

### <a name="steps-for-troubleshooting-password-problems-with-the-cluster-name-account"></a>Schritte zum Beheben von Kennwortproblemen mit dem Clusternamenkonto

Verwenden Sie dieses Verfahren, wenn eine Ereignismeldung zu Computerobjekten oder der Clusteridentität angezeigt wird, die den folgenden Text enthält. Beachten Sie, dass dieser Text in der Ereignismeldung steht, nicht am Anfang der Ereignismeldung:

`Logon failure: unknown user name or bad password.`

Ereignismeldungen, die der vorstehenden Beschreibung entsprechen, geben an, dass das Kennwort für das Clusternamenkonto und das entsprechende von der Clustersoftware gespeicherte Kennwort nicht mehr übereinstimmen.

Informationen zum Sicherstellen, dass Clusteradministratoren die erforderlichen Berechtigungen haben, das folgende Verfahren ordnungsgemäß auszuführen, finden Sie weiter oben in dieser Anleitung unter Vorausplanung für Kennwortzurücksetzungen und andere Kontowartungsmaßnahmen.

Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft. Außerdem muss Ihr Konto über die Berechtigung **Kennwort zurücksetzen** für das Clusternamenkonto verfügen (es sei denn, das Konto ist ein **Domänen-Admins**-Konto oder Ersteller-Besitzer des Clusternamenkontos). Das Konto, das von der Person verwendet wurde, die den Cluster installiert hat, kann für dieses Verfahren verwendet werden. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=83477](https://go.microsoft.com/fwlink/?linkid=83477).

#### <a name="to-troubleshoot-password-problems-with-the-cluster-name-account"></a>So beheben Sie Kennwortprobleme mit dem Clusternamenkonto

1.  Klicken Sie zum Öffnen des Failovercluster-Snap-Ins auf **Start**, auf **Verwaltung** und dann auf **Failover-Clusterverwaltung**. (Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, vergewissern Sie sich, dass die gewünschte Aktion angezeigt wird, und klicken Sie dann auf **weiter**.)

2.  Wenn im Snap-In Failover-Clusterverwaltung der zu konfigurierende Cluster nicht angezeigt wird, klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf **Failover-Clusterverwaltung**, klicken Sie auf **Cluster verwalten**, und wählen Sie den gewünschten Cluster aus, oder geben Sie diesen an.

3.  Erweitern Sie im mittleren Bereich **Hauptressourcen des Clusters**.

4.  Klicken Sie unter **Clustername** mit der rechten Maustaste auf das Element **Name**, zeigen Sie auf **Weitere Aktionen**, und klicken Sie dann auf **Active Directory-Objekt reparieren**.

### <a name="steps-for-troubleshooting-problems-caused-by-changes-in-cluster-related-active-directory-accounts"></a>Schritte zum Beheben von Problemen, die durch Änderungen an clusterbezogenen Active Directory-Konten verursacht wurden

Wenn das Clusternamenkonto gelöscht wird oder dem Konto Berechtigungen entzogen werden, treten Probleme auf, wenn Sie einen neuen geclusterten Dienst oder eine neue geclusterte Anwendung konfigurieren. Sie können ein Problem, das möglicherweise auf diese Ursache zurückzuführen ist, beheben, indem Sie mithilfe des Snap-Ins "Active Directory-Benutzer und -Computer" das Clusternamenkonto und andere zugehörige Konten anzeigen bzw. ändern. Informationen zu den Ereignissen, die protokolliert werden, wenn diese Art von Problem auftritt (Ereignis 1193, 1194, 1206 oder 1207), finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=118271](https://go.microsoft.com/fwlink/?linkid=118271).

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=83477](https://go.microsoft.com/fwlink/?linkid=83477).

#### <a name="to-troubleshoot-problems-caused-by-changes-in-cluster-related-active-directory-accounts"></a>So beheben Sie Probleme, die durch Änderungen an clusterbezogenen Active Directory-Konten verursacht wurden

1.  Klicken Sie auf einem Domänencontroller auf **Start**, auf **Verwaltung** und dann auf **Active Directory-Benutzer und -Computer**. Wenn das Dialogfeld **Benutzerkontensteuerung** eingeblendet wird, bestätigen Sie die angegebene Aktion und klicken dann auf **Weiter**.

2.  Erweitern Sie den Standardcontainer **Computer** bzw. den Ordner, in dem sich das Clusternamenkonto (das Computerkonto für den Cluster) befindet. **Computer** befinden sich unter <b>Active Directory Benutzer und Computer/</b><i>Domäne-Knoten</i><b>/Computers</b>.

3.  Beachten Sie das Symbol für das Clusternamenkonto. Es darf keinen abwärts zeigenden Pfeil aufweisen, das heißt, das Konto darf nicht deaktiviert sein. Wenn es als deaktiviert angezeigt wird, klicken Sie mit der rechten Maustaste darauf, und suchen Sie nach dem Befehl **Konto aktivieren**. Wenn Sie den Befehl sehen, klicken Sie darauf.

4.  Stellen Sie sicher, dass im Menü **Ansicht** die Option **Erweiterte Funktionen** ausgewählt ist.
    
    Wenn **Erweiterte Funktionen** ausgewählt ist, wird die Registerkarte **Sicherheit** in den Eigenschaften der Konten (Objekte) in **Active Directory-Benutzer und -Computer** angezeigt.

5.  Klicken Sie mit der rechten Maustaste auf den Standardcontainer **Computer** bzw. den Ordner, in dem sich das Clusternamenkonto befindet.

6.  Klicken Sie auf **Eigenschaften**.

7.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Erweitert**.

8.  Klicken Sie in der Liste der Konten mit Berechtigungen auf das Clusternamenkonto und dann auf **Bearbeiten**.
    

> [!NOTE]
> Wenn das Clusternamenkonto nicht aufgeführt ist, klicken Sie auf <STRONG>Hinzufügen</STRONG>, und fügen Sie es der Liste hinzu. 
<br>


9. Vergewissern Sie sich, dass für das Cluster Namen Konto (auch als Cluster Namen Objekt oder CNO bezeichnet) die Option **zulassen** für die Berechtigungen zum **Erstellen von Computer Objekten** und zum **Lesen aller Eigenschaften** ausgewählt ist.
    
   ![](media/configure-ad-accounts/Cc731002.f5977c4d-a62e-4b17-81e3-8c19ddca2078(WS.10).gif)

10. Klicken Sie auf **OK**, bis Sie zum Snap-In **Active Directory-Benutzer und -Computer** zurückgekehrt sind.

11. Überprüfen Sie die Domänenrichtlinien, die sich auf die Erstellung von Computerkonten (Objekten) beziehen (gegebenenfalls, indem Sie sich an einen Domänenadministrator wenden). Stellen Sie sicher, dass das Clusternamenkonto ein Computerkonto erstellen kann, immer wenn Sie einen geclusterten Dienst oder eine geclusterte Anwendung konfigurieren. Wenn der Domänenadministrator beispielsweise Einstellungen konfiguriert hat, die dazu führen, dass alle neuen Computerkonten in einem spezialisierten Container statt im Standardcontainer **Computer** erstellt werden, müssen Sie sicherstellen, dass diese Einstellungen es dem Clusternamenkonto ermöglichen, ebenfalls neue Computerkonten in diesem Container zu erstellen.

12. Erweitern Sie den Standardcontainer **Computer** oder den Container, in dem sich das Computerkonto für einen geclusterten Dienst oder eine geclusterte Anwendung befindet.

13. Klicken Sie mit der rechten Maustaste auf das Computerkonto für einen geclusterten Dienst oder eine geclusterte Anwendung, und klicken Sie dann auf **Eigenschaften**.

14. Vergewissern Sie sich, dass auf der Registerkarte **Sicherheit** das Clusternamenkonto unter den Konten aufgeführt wird, die über Berechtigungen verfügen, und wählen Sie es aus. Vergewissern Sie sich, dass das Clusternamenkonto über die Berechtigung **Vollzugriff** verfügt (das Kontrollkästchen **Zulassen** ist aktiviert). Wenn dies nicht der Fall ist, fügen Sie der Liste das Clusternamenkonto hinzu, und erteilen Sie dem Konto die Berechtigung **Vollzugriff**.
    
   ![](media/configure-ad-accounts/Cc731002.2e614376-87a6-453a-81ba-90ff7ebc3fa2(WS.10).gif)

15. Wiederholen Sie die Schritte 13 und 14 für jeden geclusterten Dienst und jede geclusterte Anwendung, die im Cluster konfiguriert sind.

16. Überprüfen Sie, ob das domänenweite Kontingent für das Erstellen von Computerobjekten (standardmäßig 10) erreicht wurde (gegebenenfalls, indem Sie sich an einen Domänenadministrator wenden). Wenn alle vorstehenden Elemente in diesem Verfahren überprüft und korrigiert wurden und das Kontingent ausgeschöpft wurde, erwägen Sie, das Kontingent zu vergrößern. So ändern Sie das Kontingent
    
   1.  Öffnen Sie eine Eingabeaufforderung als Administrator, und führen Sie **ADSIEdit.msc** aus.  
          
   2.  Klicken Sie mit der rechten Maustaste auf **ADSI-Editor**, klicken Sie auf **Verbinden mit** und dann auf **OK**. Der Knoten **Standardmäßiger Namenskontext** wird der Konsolenstruktur hinzugefügt.  
          
   3.  Doppelklicken Sie auf **Standardmäßiger Namenskontext**, klicken Sie mit der rechten Maustaste auf das Domänenobjekt darunter, und klicken Sie dann auf **Eigenschaften**.  
          
   4.  Führen Sie einen Bildlauf zu **ms-DS-MachineAccountQuota** durch und wählen Sie das Element aus. Klicken Sie auf **Bearbeiten**, ändern Sie den Wert, und klicken Sie dann auf **OK**.

