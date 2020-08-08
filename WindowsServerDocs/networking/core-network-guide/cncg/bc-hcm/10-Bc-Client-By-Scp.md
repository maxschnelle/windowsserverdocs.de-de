---
title: Konfigurieren der automatischen Clientermittlung für den gehosteten Cache nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.topic: article
ms.assetid: ea1c34fd-5a33-4228-9437-9bb3d44230eb
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 973e79785d296ddf1a98def3da30fdfbeb8bd044
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997098"
---
#  <a name="configure-client-automatic-hosted-cache-discovery-by-service-connection-point"></a>Konfigurieren der automatischen Clientermittlung für den gehosteten Cache nach Dienstverbindungspunkt

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit diesem Verfahren können Sie Gruppenrichtlinie zum Aktivieren und Konfigurieren des BranchCache-Modus für gehostete Caches auf \- Computern verwenden, auf denen die folgenden BranchCache- \- fähigen Windows-Betriebssysteme ausgeführt werden.

- Windows 10 Enterprise
- Windows 10 Education
- Windows 8.1 Enterprise
- Windows 8 Enterprise

> [!NOTE]
> Informationen zum Konfigurieren von in die Domäne eingebundenen Computern, auf denen Windows Server 2008 R2 oder Windows 7 ausgeführt wird, finden Sie im Windows Server 2008 R2 [BranchCache-Bereitstellungs Handbuch](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649232(v=ws.10)).

Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.

### <a name="to-use-group-policy-to-configure-clients-for-hosted-cache-mode"></a>So verwenden Sie Gruppenrichtlinie, um Clients für den gehosteten Cache Modus zu konfigurieren

1. Öffnen Sie auf einem Computer, auf dem die Active Directory Domain Services Server-Rolle installiert ist, Server-Manager, wählen Sie den lokalen Server aus **, klicken Sie**auf Extras, und klicken Sie dann auf **Gruppenrichtlinie Verwaltung**. Die Gruppenrichtlinie-Verwaltungskonsole wird geöffnet.

2. Erweitern Sie in der Gruppenrichtlinie-Verwaltungskonsole den folgenden Pfad: Gesamtstruktur **:** *Corp.contoso.com*, **Domänen**, *Corp.contoso.com*, **Gruppenrichtlinie Objekte**, wobei *Corp.contoso.com* der Name der Domäne ist, in der sich die zu konfigurierenden BranchCache-Client Computer Konten befinden.

3. Klicken Sie mit der rechten \- Maustaste auf **Gruppenrichtlinie Objekte**und dann auf **neu**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. Geben Sie unter **Name**einen Namen für das neue Gruppenrichtlinie Objekt- \( GPO ein \) . Wenn Sie das Objekt z. B. BranchCache-Clientcomputer nennen möchten, geben Sie **BranchCache-Clientcomputer** ein. Klicken Sie auf **OK**.

4. Stellen Sie in der Gruppenrichtlinie-Verwaltungskonsole sicher, dass **Gruppenrichtlinie Objekte** ausgewählt ist, und klicken Sie im Detailbereich mit \- der rechten Maustaste auf das GPO, das Sie soeben erstellt haben. Wenn Sie beispielsweise Ihre Gruppenrichtlinien Objekt-BranchCache-Client Computer benannt haben, klicken Sie mit der rechten \- Maustaste auf **BranchCache-Client Computer**. Klicken Sie auf **Bearbeiten**. Die Gruppenrichtlinienverwaltungs-Editor-Konsole wird geöffnet.

5. Erweitern Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole den folgenden Pfad: **Computer Konfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtlinien Definitionen \( ADMX-Dateien, \) die vom lokalen Computer abgerufen**werden, **Netzwerk**, **BranchCache**.

6. Klicken Sie auf **BranchCache**, und doppelklicken Sie dann im \- Detail **Bereich auf BranchCache einschalten**. Das Dialogfeld **BranchCache aktivieren** wird geöffnet.

7.  Klicken Sie im Dialogfeld **BranchCache aktivieren** auf **Aktiviert** und dann auf **OK**.

8. Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf \- **Automatische gehostete Cache Ermittlung durch Dienst Verbindungspunkt aktivieren**. Das Dialogfeld für die Richtlinien Einstellung wird geöffnet.

9. Klicken Sie im Dialogfeld **Automatische Ermittlung von gehosteten Caches nach Dienst Verbindungspunkt aktivieren** auf **aktiviert**, und klicken Sie dann auf **OK**.

10. So aktivieren Sie die Client Computer zum herunterladen und Zwischenspeichern von Inhalten von BranchCache-Dateiserver \- basierten Inhalts Servern: Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf \- **BranchCache für Netzwerkdateien**. Das Dialogfeld **BranchCache für Netzwerkdateien konfigurieren** wird geöffnet.
11. Klicken Sie im Dialogfeld **BranchCache für Netzwerkdateien konfigurieren** auf **Aktiviert**. Geben Sie unter **Optionen** einen numerischen Wert für die maximale Roundtrip-Netzwerkwartezeitzeit (in Millisekunden) ein, und klicken Sie dann auf **OK**.

    > [!NOTE]
    > Standardmäßig werden von Client Computern Inhalt von Dateiservern zwischengespeichert, wenn die Roundtrip-Netzwerk Latenz länger als 80 Millisekunden ist.

12. So konfigurieren Sie die Menge an Festplattenspeicher, die jedem Client Computer für den BranchCache-Cache zugeordnet ist: Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf \- **Prozentsatz des Speicherplatzes festlegen, der für den Cache des Client Computers verwendet**wird. Das Dialogfeld **Prozentuale Speicherplatzbelegung durch Clientcomputercache festlegen** wird geöffnet. Klicken Sie auf **Aktiviert**, und geben Sie dann im Feld **Optionen** einen numerischen Wert ein, der den Prozentsatz des Festplattenspeicherplatzes darstellt, der auf jedem Clientcomputer für den BranchCache-Cache verwendet werden soll. Klicken Sie auf **OK**.

13. Um das Standard Alter (in Tagen) anzugeben, für das Segmente im BranchCache-Daten Cache auf Client Computern gültig sind: Stellen Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole sicher, dass **BranchCache** noch ausgewählt ist, und doppelklicken Sie dann im Detailbereich auf \- **Alter für Segmente im Daten Cache festlegen**. Das Dialogfeld **Alter für Segmente im Daten Cache festlegen** wird geöffnet. Klicken Sie auf **aktiviert**, und geben Sie dann im Detailbereich die gewünschte Anzahl von Tagen ein. Klicken Sie auf **OK**.

14. Konfigurieren Sie zusätzliche Einstellungen für die BranchCache-Richtlinie für Client Computer entsprechend Ihrer Bereitstellung.

15. Aktualisieren Sie Gruppenrichtlinie auf den Client Computern der Zweigstelle, indem Sie den Befehl **gpupdate/force**ausführen oder die Client Computer neu starten.

Die Bereitstellung des BranchCache-gehosteten Cache Modus ist nun fertiggestellt.

Weitere Informationen zu den Technologien in dieser Anleitung finden Sie unter [zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md).