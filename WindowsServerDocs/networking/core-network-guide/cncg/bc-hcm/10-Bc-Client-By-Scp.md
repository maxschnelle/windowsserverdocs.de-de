---
title: Konfigurieren der automatischen Clientermittlung für den gehosteten Cache nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: ea1c34fd-5a33-4228-9437-9bb3d44230eb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd77fc76a999517cb8372aec8dfad25b4dd5be3b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829721"
---
#  <a name="configure-client-automatic-hosted-cache-discovery-by-service-connection-point"></a>Konfigurieren der automatischen Clientermittlung für den gehosteten Cache nach Dienstverbindungspunkt

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Mit diesem Verfahren können Sie Gruppenrichtlinien verwenden, aktivieren und konfigurieren gehosteten BranchCache-Cachemodus in Domäne\-eingebundenen Computern unter den folgenden BranchCache\-fähigen Windows-Betriebssysteme.

- Windows 10 Enterprise
- Windows 10 Education
- Windows 8.1 Enterprise
- Windows 8 Enterprise

> [!NOTE]  
> Um die Domäne eingebundenen Computern konfigurieren, die Windows Server 2008 R2 oder Windows 7 ausgeführt werden, finden Sie unter Windows Server 2008 R2 [BranchCache-Bereitstellungshandbuch](https://technet.microsoft.com/library/ee649232.aspx).

Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.

### <a name="to-use-group-policy-to-configure-clients-for-hosted-cache-mode"></a>Verwendung von Gruppenrichtlinien zum Konfigurieren von Clients für den Modus "gehosteter Cache"

1. Auf einem Computer, auf dem die Active Directory-Domänendienste-Serverrolle installiert ist, öffnen Sie Server-Manager, wählen Sie den lokalen Server, klicken Sie auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.

2. Erweitern Sie folgenden Pfad in der Gruppenrichtlinien-Verwaltungskonsole: **Gesamtstruktur:** *"corp.contoso.com"*, **Domänen**, *"corp.contoso.com"*, **Gruppenrichtlinienobjekte**, wobei *"corp.contoso.com"* ist der Name der Domäne, in denen, die zu konfigurierenden BranchCache-Clientcomputerkonten befinden.

3. Rechts\-klicken Sie auf **Group Policy Objects**, und klicken Sie dann auf **neu**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. In **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt \(GPO\). Wenn Sie das Objekt z. B. BranchCache-Clientcomputer nennen möchten, geben Sie **BranchCache-Clientcomputer** ein. Klicken Sie auf **OK**.

4. In der Gruppenrichtlinien-Verwaltungskonsole, stellen Sie sicher, dass **Group Policy Objects** aktiviert ist, und im rechten Bereich Details\-klicken Sie auf das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben. Wenn Sie Ihre Gruppenrichtlinienobjekt BranchCache-Clientcomputer mit dem Namen, z. B. rechten\-klicken Sie auf **BranchCache-Clientcomputern**. Klicken Sie auf **Bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.

5. Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad ein: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtliniendefinitionen \(ADMX-Dateien\) aus dem lokalen Computer abgerufen**, **Netzwerk**, **BranchCache**.

6. Klicken Sie auf **BranchCache**, und doppelklicken Sie dann im Detailbereich,\-klicken Sie auf **BranchCache aktivieren**. Das Dialogfeld **BranchCache aktivieren** wird geöffnet.
  
7.  Klicken Sie im Dialogfeld **BranchCache aktivieren** auf **Aktiviert** und dann auf **OK**.

8. In der Konsole des Gruppenrichtlinienverwaltungs-Editor, stellen Sie sicher, dass **BranchCache** weiterhin aktiviert ist, und klicken Sie dann in die Details im Bereich doppelte\-klicken Sie auf **aktivieren gehosteten Cache AutoErmittlung von Dienst-Verbindung Punkt**. Das Dialogfeld für die Richtlinie wird geöffnet.

9. In der **aktivieren automatisch gehosteten Cache der Suche nach Dienstverbindungspunkt** Dialogfeld klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.

10. Aktivieren von Clientcomputern zum Herunterladen und Zwischenspeichern von Inhalten von BranchCache-Dateiserver\-basierte Inhaltsserver: In der Konsole des Gruppenrichtlinienverwaltungs-Editor, stellen Sie sicher, dass **BranchCache** weiterhin aktiviert ist, und klicken Sie dann in die Details im Bereich doppelte\-klicken Sie auf **BranchCache für Netzwerkdateien**. Das Dialogfeld **BranchCache für Netzwerkdateien konfigurieren** wird geöffnet. 
11. Klicken Sie im Dialogfeld **BranchCache für Netzwerkdateien konfigurieren** auf **Aktiviert**. Geben Sie unter **Optionen** einen numerischen Wert für die maximale Roundtrip-Netzwerkwartezeitzeit (in Millisekunden) ein, und klicken Sie dann auf **OK**.
  
    > [!NOTE]
    > In der Standardeinstellung Zwischenspeichern Clientcomputer Inhalt von Dateiservern, liegt die Roundtrip-Netzwerklatenz länger als 80 Millisekunden.
  
12. So konfigurieren Sie den verfügbaren Festplattenspeicher, der dem BranchCache-Cache auf jedem Clientcomputer zugeordnet ist: In der Konsole des Gruppenrichtlinienverwaltungs-Editor, stellen Sie sicher, dass **BranchCache** weiterhin aktiviert ist, und klicken Sie dann in die Details im Bereich doppelte\-klicken Sie auf **Prozentsatz des Speicherplatzes für Cache Clientcomputersverwendetfestlegen**. Das Dialogfeld **Prozentuale Speicherplatzbelegung durch Clientcomputercache festlegen** wird geöffnet. Klicken Sie auf **Aktiviert**, und geben Sie dann im Feld **Optionen** einen numerischen Wert ein, der den Prozentsatz des Festplattenspeicherplatzes darstellt, der auf jedem Clientcomputer für den BranchCache-Cache verwendet werden soll. Klicken Sie auf **OK**.

13. An das standardalter in Tagen, für die Segmente in der BranchCache-Datencache auf Clientcomputern gültig sind: In der Konsole des Gruppenrichtlinienverwaltungs-Editor, stellen Sie sicher, dass **BranchCache** weiterhin aktiviert ist, und klicken Sie dann in die Details im Bereich doppelte\-klicken Sie auf **Festlegen des Alters für Segmente im Datencache**. Die **Festlegen des Alters für Segmente im Datencache** Dialogfeld wird geöffnet. Klicken Sie auf **aktiviert**, und geben Sie dann im Detailbereich die Anzahl der Tage, die Sie bevorzugen. Klicken Sie auf **OK**.

14. Konfigurieren Sie zusätzliche BranchCache-gruppenrichtlinieneinstellungen für Clientcomputer nach Bedarf für Ihre Bereitstellung ein.

15. Aktualisieren der Gruppenrichtlinie auf Clientcomputern für Branch Office mithilfe des Befehls **Gpupdate/force**, oder durch einen Neustart des Computer.

Die BranchCache-gehosteten Cache-Modus-Bereitstellung ist nun abgeschlossen.

Weitere Informationen zu den Technologien in diesem Handbuch finden Sie unter [Zusatzressourcen](11-Bc-Hcm-additional-resources.md).