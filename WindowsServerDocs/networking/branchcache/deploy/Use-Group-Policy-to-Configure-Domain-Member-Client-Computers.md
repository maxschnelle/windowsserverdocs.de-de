---
title: Verwenden von Gruppenrichtlinien zum Konfigurieren von Domänenmitglieds-Clientcomputern
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: pashort
author: shortpatti
ms.date: 06/02/2018
ms.openlocfilehash: 8e82d3e0ee7a84fbd6e2916d0f22472a8c117688
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855081"
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>Verwenden von Gruppenrichtlinien zum Konfigurieren von Domänenmitglieds-Clientcomputern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Abschnitt Sie ein Gruppenrichtlinienobjekt für alle Computer in Ihrer Organisation erstellen, Konfigurieren von Domänenmitglieds-Clientcomputern mit Modus "verteilter Cache" oder Modus für gehostete Caches und Konfigurieren von Windows-Firewall mit erweiterter Sicherheit, um BranchCache zu ermöglichen. Datenverkehr wird:  
  
Dieser Abschnitt enthält die folgenden Verfahren.  
  
1.  [Erstellen ein Gruppenrichtlinienobjekt, und Konfigurieren von BranchCache-Modi](#bkmk_gp)  
  
2.  [So konfigurieren Sie Windows-Firewall mit erweiterter Sicherheit eingehende Regeln für den Netzwerkdatenverkehr](#bkmk_inbound)  
  
3.  [So konfigurieren Sie Windows-Firewall mit erweiterter Sicherheit ausgehende Datenverkehrsregeln](#bkmk_outbound)  
  
> [!TIP]  
> Klicken Sie in der folgenden Prozedur werden Sie angewiesen, erstellen ein Gruppenrichtlinienobjekt in der Standarddomänenrichtlinie, allerdings können Sie das Objekt erstellen, in einer Organisationseinheit (OU) oder einem anderen Container, die für Ihre Bereitstellung geeignet ist.  
  
Sie müssen ein Mitglied sein **Domänen-Admins**, oder einer entsprechenden Variablen, um diese Verfahren ausführen.  
  
## <a name="bkmk_gp"></a>Erstellen ein Gruppenrichtlinienobjekt, und Konfigurieren von BranchCache-Modi  
  
1.  Klicken Sie auf einem Computer, auf denen die Active Directory-Domänendienste-Serverrolle, im Server-Manager installiert ist, auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.  
  
2.  Erweitern Sie folgenden Pfad in der Gruppenrichtlinien-Verwaltungskonsole: **Gesamtstruktur:** *"example.com"*, **Domänen**, *"example.com"*, **Gruppenrichtlinienobjekte**, wobei  *"example.com"* ist der Name der Domäne, in denen, die zu konfigurierenden BranchCache-Clientcomputerkonten befinden.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienobjekte**, und klicken Sie dann auf **Neu**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. In **Namen**, geben Sie einen Namen für die neue Gruppe Gruppenrichtlinienobjekt (GPO). Wenn Sie das Objekt z. B. BranchCache-Clientcomputer nennen möchten, geben Sie **BranchCache-Clientcomputer** ein. Klicken Sie auf **OK**.  
  
4.  Stellen Sie in der Gruppenrichtlinien-Verwaltungskonsole sicher, dass **Gruppenrichtlinienobjekte** ausgewählt ist, und klicken Sie im Detailbereich mit der rechten Maustaste auf das soeben erstellte Gruppenrichtlinienobjekt. Wenn Sie das Gruppenrichtlinienobjekt z. B. „BranchCache-Clientcomputer“ genannt haben, klicken Sie mit der rechten Maustaste auf **BranchCache-Clientcomputer**. Klicken Sie auf **Bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.  
  
5.  Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad ein: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtliniendefinitionen (ADMX-Dateien) auf dem lokalen Computer abgerufen**, **Netzwerk**, **BranchCache**.  
  
6.  Klicken Sie auf **BranchCache** und doppelklicken Sie dann im Detailbereich auf **BranchCache aktivieren**. Das Dialogfeld für die Richtlinie wird geöffnet.  
  
7.  Klicken Sie im Dialogfeld **BranchCache aktivieren** auf **Aktiviert** und dann auf **OK**.  
  
8.  Doppelklicken Sie zum Aktivieren von BranchCache verteilten Cachemodus, klicken Sie im Detailbereich auf **festgelegt BranchCache verteilten Cachemodus**. Das Dialogfeld für die Richtlinie wird geöffnet.  
  
9. Klicken Sie im Dialogfeld **BranchCache-Modus „Verteilter Cache“ festlegen** auf **Aktiviert** und dann auf **OK**.  
  
10. Wenn Sie eine oder mehrere Filialen haben, in denen Sie BranchCache im Modus "gehosteter Cache" bereitstellen und Sie die bereitgestellten gehosteten Cacheservern in Unterhalt der Büros gesenkt, doppelklicken Sie auf **aktivieren automatisch gehosteten Cache der Suche nach Dienstverbindungspunkt**. Das Dialogfeld für die Richtlinie wird geöffnet.  
  
11. In der **aktivieren automatisch gehosteten Cache der Suche nach Dienstverbindungspunkt** Dialogfeld klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Wenn Sie beide aktivieren die **festgelegt BranchCache verteilten Cachemodus** und die **aktivieren automatisch gehosteten Cache der Suche nach Dienstverbindungspunkt** Richtlinieneinstellungen, Client-Computern ausgeführt werden, in BranchCache Cachemodus verteilt, es sei denn, sie einen gehosteten Cacheserver in der Zweigstelle, finden Sie an diesem, die Punkt, die sie im gehosteten Cachemodus betrieben werden.  
  
12. Verwenden Sie die folgenden Verfahren, um die Firewall-Einstellungen mithilfe der Gruppenrichtlinie auf Clientcomputern zu konfigurieren.  
  
## <a name="bkmk_inbound"></a>So konfigurieren Sie Windows-Firewall mit erweiterter Sicherheit eingehende Regeln für den Netzwerkdatenverkehr  
  
1.  Erweitern Sie folgenden Pfad in der Gruppenrichtlinien-Verwaltungskonsole: **Gesamtstruktur:** *"example.com"*, **Domänen**, *"example.com"*, **Gruppenrichtlinienobjekte**, wobei  *"example.com"* ist der Name der Domäne, in denen, die zu konfigurierenden BranchCache-Clientcomputerkonten befinden.  
  
2.  Stellen Sie in der Gruppenrichtlinien-Verwaltungskonsole sicher, dass **Gruppenrichtlinienobjekte** ausgewählt ist, und klicken Sie im Detailbereich mit der rechten Maustaste auf das zuvor erstellte Gruppenrichtlinienobjekt der BranchCache-Clientcomputer. Wenn Sie das Gruppenrichtlinienobjekt z. B. „BranchCache-Clientcomputer“ genannt haben, klicken Sie mit der rechten Maustaste auf **BranchCache-Clientcomputer**. Klicken Sie auf **Bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.  
  
3.  Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad ein: **Computerkonfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, **Windows-Firewall mit erweiterter Sicherheit**, **Windows-Firewall mit erweiterter Sicherheit - LDAP**, **Eingangsregeln**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie dann auf **Neue Regel**. Der neue eingehende Regel-Assistent wird geöffnet.  
  
5.  In **Regeltyp**, klicken Sie auf **vordefinierte**, erweitern Sie die Liste der Optionen aus, und klicken Sie dann auf **BranchCache – Inhaltsabruf (verwendet HTTP)**. Klicken Sie auf **Weiter**.  
  
6.  Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
7.  Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr empfangen kann.  
  
8.  Um die WS-Discovery-Firewallausnahme zu erstellen, klicken Sie erneut mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie dann auf **Neue Regel**. Der neue eingehende Regel-Assistent wird geöffnet.  
  
9. In **Regeltyp**, klicken Sie auf **vordefinierte**, erweitern Sie die Liste der Optionen aus, und klicken Sie dann auf **BranchCache – Peerermittlung (verwendet WSD)**. Klicken Sie auf **Weiter**.  
  
10. Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
11. Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr empfangen kann.  
  
## <a name="bkmk_outbound"></a>So konfigurieren Sie Windows-Firewall mit erweiterter Sicherheit ausgehende Datenverkehrsregeln  
  
1.  Klicken Sie in der Konsole des Gruppenrichtlinienverwaltungs-Editors mit der rechten Maustaste auf **Ausgehende Regeln**, und klicken Sie dann auf **Neue Regel**. Die Assistenten für neue ausgehende Regeln wird geöffnet.  
  
2.  In **Regeltyp**, klicken Sie auf **vordefinierte**, erweitern Sie die Liste der Optionen aus, und klicken Sie dann auf **BranchCache – Inhaltsabruf (verwendet HTTP)**. Klicken Sie auf **Weiter**.  
  
3.  Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
4.  Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr senden kann.  
  
5.  Um die WS-Discovery-Firewallausnahme zu erstellen, klicken Sie erneut mit der rechten Maustaste auf **Ausgehende Regeln**, und klicken Sie dann auf **Neue Regel**. Die Assistenten für neue ausgehende Regeln wird geöffnet.  
  
6.  In **Regeltyp**, klicken Sie auf **vordefinierte**, erweitern Sie die Liste der Optionen aus, und klicken Sie dann auf **BranchCache – Peerermittlung (verwendet WSD)**. Klicken Sie auf **Weiter**.  
  
7.  Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
8.  Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr senden kann.  
  


