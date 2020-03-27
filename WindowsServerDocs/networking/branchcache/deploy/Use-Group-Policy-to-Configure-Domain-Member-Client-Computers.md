---
title: Verwenden von Gruppenrichtlinie zum Konfigurieren von Domänen Mitglieds-Client Computern
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: lizross
author: eross-msft
ms.date: 06/02/2018
ms.openlocfilehash: c6ca1ff8fabb559628afd2dd1abafc56a908909a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319196"
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>Verwenden von Gruppenrichtlinie zum Konfigurieren von Domänen Mitglieds-Client Computern

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Abschnitt erstellen Sie ein Gruppenrichtlinie Objekt für alle Computer in Ihrer Organisation, konfigurieren Domänen Mitglieds Client-Computer mit dem Modus "verteilter Cache" oder "gehosteter Cache" und konfigurieren die Windows-Firewall mit erweiterter Sicherheit, um BranchCache zuzulassen. verkehrssicher.  
  
Dieser Abschnitt enthält die folgenden Prozeduren.  
  
1.  [So erstellen Sie ein Gruppenrichtlinie Objekt und konfigurieren die BranchCache-Modi](#bkmk_gp)  
  
2.  [So konfigurieren Sie die Windows-Firewall mit Regeln für eingehenden Datenverkehr](#bkmk_inbound)  
  
3.  [So konfigurieren Sie Regeln für ausgehenden Datenverkehr für die Windows-Firewall](#bkmk_outbound)  
  
> [!TIP]  
> Im folgenden Verfahren werden Sie angewiesen, ein Gruppenrichtlinie Objekt in der Standard Domänen Richtlinie zu erstellen. Sie können das Objekt jedoch in einer Organisationseinheit oder einem anderen Container erstellen, der für Ihre Bereitstellung geeignet ist.  
  
Sie müssen Mitglied der Gruppe **Domänen-Admins**oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.  
  
## <a name="to-create-a-group-policy-object-and-configure-branchcache-modes"></a><a name="bkmk_gp"></a>So erstellen Sie ein Gruppenrichtlinie Objekt und konfigurieren die BranchCache-Modi  
  
1.  Klicken Sie auf einem **Computer, auf**dem die Active Directory Domain Services Server-Rolle installiert ist, in Server-Manager auf Extras, und klicken Sie dann auf **Gruppenrichtlinie Verwaltung**. Die Gruppenrichtlinie-Verwaltungskonsole wird geöffnet.  
  
2.  Erweitern Sie in der Gruppenrichtlinie-Verwaltungskonsole den folgenden Pfad: Gesamtstruktur **:** *example.com*, **Domänen**, *example.com*, **Gruppenrichtlinie Objekte**, wobei *example.com* der Name der Domäne ist, in der sich die zu konfigurierenden BranchCache-Client Computer Konten befinden.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienobjekte**, und klicken Sie dann auf **Neu**. Das Dialogfeld **Neues Gruppenrichtlinienobjekt** wird geöffnet. Geben Sie unter **Name**einen Namen für das neue Gruppenrichtlinie Objekt (GPO) ein. Wenn Sie das Objekt z. B. BranchCache-Clientcomputer nennen möchten, geben Sie **BranchCache-Clientcomputer** ein. Klicken Sie auf **OK**.  
  
4.  Stellen Sie in der Gruppenrichtlinien-Verwaltungskonsole sicher, dass **Gruppenrichtlinienobjekte** ausgewählt ist, und klicken Sie im Detailbereich mit der rechten Maustaste auf das soeben erstellte Gruppenrichtlinienobjekt. Wenn Sie das Gruppenrichtlinienobjekt z. B. „BranchCache-Clientcomputer“ genannt haben, klicken Sie mit der rechten Maustaste auf **BranchCache-Clientcomputer**. Klicken Sie auf **Bearbeiten**. Die Gruppenrichtlinienverwaltungs-Editor-Konsole wird geöffnet.  
  
5.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole den folgenden Pfad: **Computer Konfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtlinien Definitionen (ADMX-Dateien), die vom lokalen Computer abgerufen**werden, **Netzwerk**, **BranchCache**.  
  
6.  Klicken Sie auf **BranchCache** und doppelklicken Sie dann im Detailbereich auf **BranchCache aktivieren**. Das Dialogfeld für die Richtlinien Einstellung wird geöffnet.  
  
7.  Klicken Sie im Dialogfeld **BranchCache aktivieren** auf **Aktiviert** und dann auf **OK**.  
  
8.  Um den Modus für den verteilten BranchCache-Cache zu aktivieren, doppelklicken Sie im Detailbereich auf **BranchCache-Modus "verteilter Cache" festlegen**. Das Dialogfeld für die Richtlinien Einstellung wird geöffnet.  
  
9. Klicken Sie im Dialogfeld **BranchCache-Modus „Verteilter Cache“ festlegen** auf **Aktiviert** und dann auf **OK**.  
  
10. Wenn Sie über eine oder mehrere Zweigstellen verfügen, in denen Sie BranchCache im Modus "gehosteter Cache" bereitstellen und gehostete Cache Server in diesen Niederlassungen bereitgestellt haben, doppelklicken Sie auf **Automatische gehostete Cache Ermittlung durch Dienst Verbindungspunkt aktivieren**. Das Dialogfeld für die Richtlinien Einstellung wird geöffnet.  
  
11. Klicken Sie im Dialogfeld **Automatische Ermittlung von gehosteten Caches nach Dienst Verbindungspunkt aktivieren** auf **aktiviert**, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Wenn Sie die Richtlinien Einstellungen " **BranchCache-verteilter Cache** " und " **Automatische gehostete Cache Ermittlung durch Dienst Verbindungspunkt** " aktivieren, werden die Client Computer im verteilten BranchCache-Cache Modus ausgeführt, es sei denn, Sie finden einen gehosteten Cache Server in der Filiale. an diesem Punkt arbeiten Sie im Modus "gehosteter Cache".  
  
12. Verwenden Sie die folgenden Verfahren, um Firewalleinstellungen auf Client Computern mithilfe von Gruppenrichtlinie zu konfigurieren.  
  
## <a name="to-configure-windows-firewall-with-advanced-security-inbound-traffic-rules"></a><a name="bkmk_inbound"></a>So konfigurieren Sie die Windows-Firewall mit Regeln für eingehenden Datenverkehr  
  
1.  Erweitern Sie in der Gruppenrichtlinie-Verwaltungskonsole den folgenden Pfad: Gesamtstruktur **:** *example.com*, **Domänen**, *example.com*, **Gruppenrichtlinie Objekte**, wobei *example.com* der Name der Domäne ist, in der sich die zu konfigurierenden BranchCache-Client Computer Konten befinden.  
  
2.  Stellen Sie in der Gruppenrichtlinien-Verwaltungskonsole sicher, dass **Gruppenrichtlinienobjekte** ausgewählt ist, und klicken Sie im Detailbereich mit der rechten Maustaste auf das zuvor erstellte Gruppenrichtlinienobjekt der BranchCache-Clientcomputer. Wenn Sie das Gruppenrichtlinienobjekt z. B. „BranchCache-Clientcomputer“ genannt haben, klicken Sie mit der rechten Maustaste auf **BranchCache-Clientcomputer**. Klicken Sie auf **Bearbeiten**. Die Gruppenrichtlinienverwaltungs-Editor-Konsole wird geöffnet.  
  
3.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-Editor Konsole den folgenden Pfad: **Computer Konfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, **Windows-Firewall mit**erweiterter Sicherheit, **Windows-Firewall mit erweiterter Sicherheit-LDAP**, **Eingehende Regeln**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie dann auf **Neue Regel**. Der Assistent für neue eingehende Regeln wird geöffnet.  
  
5.  Klicken Sie unter **Regeltyp**auf **vordefiniert**, erweitern Sie die Auswahlliste, und klicken Sie dann auf **BranchCache-Inhalts Abruf (verwendet http)** . Klicken Sie auf **Weiter**.  
  
6.  Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
7.  Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr empfangen kann.  
  
8.  Um die WS-Discovery-Firewallausnahme zu erstellen, klicken Sie erneut mit der rechten Maustaste auf **Eingehende Regeln**, und klicken Sie dann auf **Neue Regel**. Der Assistent für neue eingehende Regeln wird geöffnet.  
  
9. Klicken Sie unter **Regeltyp**auf **vordefiniert**, erweitern Sie die Auswahlliste, und klicken Sie dann auf **BranchCache-Peer Ermittlung (verwendet WSD)** . Klicken Sie auf **Weiter**.  
  
10. Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
11. Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr empfangen kann.  
  
## <a name="to-configure-windows-firewall-with-advanced-security-outbound-traffic-rules"></a><a name="bkmk_outbound"></a>So konfigurieren Sie Regeln für ausgehenden Datenverkehr für die Windows-Firewall  
  
1.  Klicken Sie in der Konsole des Gruppenrichtlinienverwaltungs-Editors mit der rechten Maustaste auf **Ausgehende Regeln**, und klicken Sie dann auf **Neue Regel**. Der Assistent für neue ausgehende Regeln wird geöffnet.  
  
2.  Klicken Sie unter **Regeltyp**auf **vordefiniert**, erweitern Sie die Auswahlliste, und klicken Sie dann auf **BranchCache-Inhalts Abruf (verwendet http)** . Klicken Sie auf **Weiter**.  
  
3.  Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
4.  Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr senden kann.  
  
5.  Um die WS-Discovery-Firewallausnahme zu erstellen, klicken Sie erneut mit der rechten Maustaste auf **Ausgehende Regeln**, und klicken Sie dann auf **Neue Regel**. Der Assistent für neue ausgehende Regeln wird geöffnet.  
  
6.  Klicken Sie unter **Regeltyp**auf **vordefiniert**, erweitern Sie die Auswahlliste, und klicken Sie dann auf **BranchCache-Peer Ermittlung (verwendet WSD)** . Klicken Sie auf **Weiter**.  
  
7.  Klicken Sie unter **Vordefinierte Regeln** auf **Weiter**.  
  
8.  Vergewissern Sie sich, dass für **Aktion** die Option **Verbindung zulassen** ausgewählt ist, und klicken Sie  dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen **Verbindung zulassen** auswählen, damit der BranchCache-Client auf diesem Port Datenverkehr senden kann.  
  


