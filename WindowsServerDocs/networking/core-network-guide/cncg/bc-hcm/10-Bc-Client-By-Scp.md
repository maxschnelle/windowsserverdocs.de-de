---
title: Konfigurieren der Ermittlung von Clients automatisch nach gehosteten Cacheservern nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: ea1c34fd-5a33-4228-9437-9bb3d44230eb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b12fa6f9e11c8816d74c9013dd80b3fa38d0a478
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
#  <a name="configure-client-automatic-hosted-cache-discovery-by-service-connection-point"></a>Konfigurieren der Ermittlung von Clients automatisch nach gehosteten Cacheservern nach Dienstverbindungspunkt

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Mit diesem Verfahren können Sie Gruppenrichtlinien verwenden, aktivieren und Konfigurieren von BranchCache-gehosteten Cachemodus auf Domäne\ verbundene Computer, die den folgenden BranchCache\-fähigen Windows-Betriebssystemen ausgeführt werden.

- Windows 10 Enterprise
- Windows 10 Education
- Windows 8.1 Enterprise
- Windows 8 Enterprise

> [!NOTE]  
> Um die Domäne eingebundene Computer konfigurieren, auf denen Windows Server 2008 R2 oder Windows 7 ausgeführt werden, finden Sie unter der Windows Server 2008 R2 [BranchCache-Bereitstellungshandbuchs](https://technet.microsoft.com/library/ee649232.aspx).

Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.

### <a name="to-use-group-policy-to-configure-clients-for-hosted-cache-mode"></a>Verwendung von Gruppenrichtlinien zum Konfigurieren von Clients für den gehosteten Cachemodus

1. Auf einem Computer, auf dem die Active Directory-Domänendienste-Serverrolle installiert ist, öffnen Sie Server-Manager, wählen Sie den lokalen Server, klicken Sie auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.

2. In der Gruppenrichtlinien-Verwaltungskonsole, erweitern Sie den folgenden Pfad: **Gesamtstruktur:** *corp.contoso.com*, **Domänen**, *corp.contoso.com*, **Group Policy Objects**, wobei *corp.contoso.com* ist der Name der Domäne, in dem zu konfigurierenden BranchCache-Clientcomputerkonten befinden.

3. Klicken Sie auf **Group Policy Objects**, und klicken Sie dann auf **neu**. Die **Gruppenrichtlinienobjekt** Dialogfeld wird geöffnet. In **Namen**, geben Sie einen Namen für die neue Gruppenrichtlinie \(GPO\) Objekt. Geben Sie beispielsweise, wenn Sie das BranchCache-Clientcomputer-Objekt zu benennen möchten, **BranchCache-Clientcomputern**. Klicken Sie auf **OK**.

4. In der Gruppenrichtlinien-Verwaltungskonsole, stellen Sie sicher, dass **Group Policy Objects** wird ausgewählt und in den Details im Bereich mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, das Sie gerade erstellt. Wenn Sie Ihre Gruppenrichtlinienobjekt BranchCache-Clientcomputer mit dem Namen z. B. mit der rechten Maustaste auf **BranchCache-Clientcomputern**. Klicken Sie auf **bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.

5. Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtlinie Definitionen \(ADMX files\) aus dem lokalen Computer abgerufen**, **Netzwerk**, **BranchCache**.

6. Klicken Sie auf **BranchCache**, und klicken Sie dann im Detailbereich auf Variablenname **BranchCache aktivieren**. Die **BranchCache aktivieren** Dialogfeld wird geöffnet.
  
7.  In der **BranchCache aktivieren** Dialogfeld, klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.

8. In der Konsole Gruppenrichtlinienverwaltungs-Editor sicher, dass **BranchCache** immer noch ausgewählt ist, und klicken Sie dann im Detailbereich Fenster Variablenname- **aktivieren automatische gehosteten Cache der Ermittlung von Service Connection Point**. Im Dialogfeld für die Einstellung der Richtlinie wird geöffnet.

9. In der **aktivieren automatische gehosteten Cache der Ermittlung von Service Connection Point** Dialogfeld, klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.

10. Zum Aktivieren von Clientcomputern zum Herunterladen und Zwischenspeichern Datei Inhalte vom BranchCache Server\-basierte Inhaltsserver: In der Konsole Gruppenrichtlinienverwaltungs-Editor sicher, dass **BranchCache** immer noch ausgewählt ist, und klicken Sie dann im Detailbereich Fenster Variablenname- **BranchCache für Netzwerkdateien**. Die **BranchCache für Netzwerkdateien konfigurieren** Dialogfeld wird geöffnet. 
11. In der **BranchCache für Netzwerkdateien konfigurieren** Dialogfeld, klicken Sie auf **aktiviert**. In **Optionen**, geben Sie einen numerischen Wert in Millisekunden an, für die maximale Roundtrip-netzwerkwartezeitzeit, und klicken Sie dann auf **OK**.
  
    > [!NOTE]
    > In der Standardeinstellung cache Clientcomputer Inhalt von Dateiservern, bei der Roundtrip-Netzwerklatenz mehr als 80 Millisekunden.
  
12. So konfigurieren Sie die Menge an Festplattenspeicher, die auf jedem Clientcomputer für den BranchCache-Cache zugewiesen: In der Konsole Gruppenrichtlinienverwaltungs-Editor sicher, dass **BranchCache** immer noch ausgewählt ist, und klicken Sie dann im Detailbereich Fenster Variablenname- **prozentuale speicherplatzbelegung durch clientcomputercache festlegen**. Die **prozentuale speicherplatzbelegung durch clientcomputercache festlegen** Dialogfeld wird geöffnet. Klicken Sie auf **aktiviert**, und klicken Sie dann im **Optionen** Geben Sie einen numerischen Wert, der den Prozentsatz der benötigte Speicherplatz auf jedem Clientcomputer für den BranchCache-Cache darstellt. Klicken Sie auf **OK**.

13. Das standardalter in Tagen angeben, für die Segmente gültig in der BranchCache-Datencache auf Clientcomputern sind: In der Konsole Gruppenrichtlinienverwaltungs-Editor sicher, dass **BranchCache** immer noch ausgewählt ist, und klicken Sie dann im Detailbereich Fenster Variablenname- **Festlegen des Alters für Segmente im Datencache**. Die **Festlegen des Alters für Segmente im Datencache** Dialogfeld wird geöffnet. Klicken Sie auf **aktiviert**, und geben Sie dann im Detailbereich die Anzahl der Tage, in der Sie arbeiten. Klicken Sie auf **OK**.

14. Konfigurieren Sie zusätzliche BranchCache-Richtlinien für Clientcomputer als für die Bereitstellung sinnvoll.

15. Aktualisieren der Gruppenrichtlinie auf Clientcomputern für Branch Office durch Ausführen des Befehls **Gpupdate/force**, oder durch einen Neustart der Clientcomputer.

Die Bereitstellung des BranchCache-gehosteten Cache-Modus ist nun abgeschlossen.

Weitere Informationen zu den Technologien in diesem Handbuch finden Sie unter [zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md).