---
title: Konfigurieren der automatischen Clientermittlung für den gehosteten Cache nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: ea1c34fd-5a33-4228-9437-9bb3d44230eb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 60ccc8b80537da0d0b689f6c508c75ef15a339c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406400"
---
#  <a name="configure-client-automatic-hosted-cache-discovery-by-service-connection-point"></a>Konfigurieren der automatischen Clientermittlung für den gehosteten Cache nach Dienstverbindungspunkt

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit diesem Verfahren können Sie Gruppenrichtlinie zum Aktivieren und Konfigurieren des BranchCache-Modus für gehostete Caches auf Domänen @ no__t-Computern verwenden, auf denen die folgenden BranchCache @ no__t-1fähigen Windows-Betriebssysteme ausgeführt werden.

- Windows 10 Enterprise
- Windows 10 Education
- Windows 8.1 Enterprise
- Windows 8 Enterprise

> [!NOTE]  
> Informationen zum Konfigurieren von in die Domäne eingebundenen Computern, auf denen Windows Server 2008 R2 oder Windows 7 ausgeführt wird, finden Sie im Windows Server 2008 R2 [BranchCache-Bereitstellungs Handbuch](https://technet.microsoft.com/library/ee649232.aspx).

Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.

### <a name="to-use-group-policy-to-configure-clients-for-hosted-cache-mode"></a>So verwenden Sie Gruppenrichtlinie, um Clients für den gehosteten Cache Modus zu konfigurieren

1. Öffnen Sie auf einem Computer, auf dem die Active Directory Domain Services Server-Rolle installiert ist, Server-Manager, wählen Sie den lokalen Server aus **, klicken Sie**auf Extras, und klicken Sie dann auf **Gruppenrichtlinie Verwaltung**. Die Gruppenrichtlinie-Verwaltungskonsole wird geöffnet.

2. Erweitern Sie folgenden Pfad in der Gruppenrichtlinien-Verwaltungskonsole: Gesamtstruktur **:** *Corp.contoso.com*, **Domänen**, *Corp.contoso.com*, **Gruppenrichtlinie Objekte**, wobei *Corp.contoso.com* der Name der Domäne ist, in der die BranchCache-Client Computer Konten, die Sie Konfigurieren von.

3. Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. Geben Sie unter **Name**einen Namen für das neue Gruppenrichtlinie Objekt \(gpo @ no__t-2 ein. Wenn Sie das Objekt z. B. BranchCache-Clientcomputer nennen möchten, geben Sie **BranchCache-Clientcomputer** ein. Klicken Sie auf **OK**.

4. Stellen Sie in der Gruppenrichtlinie-Verwaltungskonsole sicher, dass **Gruppenrichtlinie Objekte** ausgewählt ist, und klicken Sie im Detailbereich mit der rechten Maustaste auf das soeben erstellte Gruppenrichtlinien Objekt. Wenn Sie z. b. Ihre GPO-BranchCache-Client Computer benannt haben, klicken Sie mit der rechten Maustaste auf **BranchCache-Client Computer**. Klicken Sie auf **Bearbeiten**. Die Gruppenrichtlinienverwaltungs-Editor-Konsole wird geöffnet.

5. Erweitern Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole den folgenden Pfad: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtlinien Definitionen \(admx-Dateien @ no__t-1, abgerufen von dem lokalen Computer @ no__t-2, **Network**, **BranchCache**.

6. Klicken Sie auf **BranchCache**, und Doppel @ no__t-1Klicken Sie dann im Detail **Bereich auf BranchCache einschalten**. Das Dialogfeld **BranchCache aktivieren** wird geöffnet.
  
7.  Klicken Sie im Dialogfeld **BranchCache aktivieren** auf **Aktiviert** und dann auf **OK**.

8. Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf die Option **Automatische Ermittlung von gehosteten Caches durch Dienst Verbindungspunkt aktivieren**. Das Dialogfeld für die Richtlinien Einstellung wird geöffnet.

9. Klicken Sie im Dialogfeld **Automatische Ermittlung von gehosteten Caches nach Dienst Verbindungspunkt aktivieren** auf **aktiviert**, und klicken Sie dann auf **OK**.

10. So aktivieren Sie den Client Computern das herunterladen und Zwischenspeichern von Inhalten von einem BranchCache-Dateiserver @ no__t-0based Content Servers: Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf die Option **BranchCache für Netzwerkdateien**. Das Dialogfeld **BranchCache für Netzwerkdateien konfigurieren** wird geöffnet. 
11. Klicken Sie im Dialogfeld **BranchCache für Netzwerkdateien konfigurieren** auf **Aktiviert**. Geben Sie unter **Optionen** einen numerischen Wert für die maximale Roundtrip-Netzwerkwartezeitzeit (in Millisekunden) ein, und klicken Sie dann auf **OK**.
  
    > [!NOTE]
    > Standardmäßig werden von Client Computern Inhalt von Dateiservern zwischengespeichert, wenn die Roundtrip-Netzwerk Latenz länger als 80 Millisekunden ist.
  
12. So konfigurieren Sie den verfügbaren Festplattenspeicher, der dem BranchCache-Cache auf jedem Clientcomputer zugeordnet ist: Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf die Option **Prozentsatz des Speicherplatzes, der für den Cache des Client Computers verwendet**wird. Das Dialogfeld **Prozentuale Speicherplatzbelegung durch Clientcomputercache festlegen** wird geöffnet. Klicken Sie auf **Aktiviert**, und geben Sie dann im Feld **Optionen** einen numerischen Wert ein, der den Prozentsatz des Festplattenspeicherplatzes darstellt, der auf jedem Clientcomputer für den BranchCache-Cache verwendet werden soll. Klicken Sie auf **OK**.

13. So geben Sie das Standard Alter (in Tagen) an, für das Segmente im BranchCache-Daten Cache auf Client Computern gültig sind: Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf **Alter für Segmente im Daten Cache festlegen**. Das Dialogfeld **Alter für Segmente im Daten Cache festlegen** wird geöffnet. Klicken Sie auf **aktiviert**, und geben Sie dann im Detailbereich die gewünschte Anzahl von Tagen ein. Klicken Sie auf **OK**.

14. Konfigurieren Sie zusätzliche Einstellungen für die BranchCache-Richtlinie für Client Computer entsprechend Ihrer Bereitstellung.

15. Aktualisieren Sie Gruppenrichtlinie auf den Client Computern der Zweigstelle, indem Sie den Befehl **gpupdate/force**ausführen oder die Client Computer neu starten.

Die Bereitstellung des BranchCache-gehosteten Cache Modus ist nun fertiggestellt.

Weitere Informationen zu den Technologien in dieser Anleitung finden Sie unter [zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md).