---
title: Verwenden von Gruppenrichtlinien zum Konfigurieren von Domänenmitglieds-Clientcomputern
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 911c1538-f79d-42e9-ba38-f4618f87b008
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 96bf84df14eac8016a898e92eb96f90435c53c98
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="use-group-policy-to-configure-domain-member-client-computers"></a>Verwenden von Gruppenrichtlinien zum Konfigurieren von Domänenmitglieds-Clientcomputern

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Diese Verfahren können Sie um ein Gruppenrichtlinienobjekt für alle Computer in Ihrer Organisation konfigurieren von Domänenmitglieds-Clientcomputern mit verteilten Cachemodus oder im Modus für gehostete Caches und zum Konfigurieren der Windows-Firewall mit erweiterter Sicherheit zum Zulassen von BranchCache-Datenverkehr zu erstellen.  
  
Dieser Abschnitt enthält die folgenden Verfahren.  
  
1.  [Ein Gruppenrichtlinienobjekt erstellen und Konfigurieren von BranchCache-Modi](#bkmk_gp)  
  
2.  [Zum Konfigurieren der Windows-Firewall mit erweiterter Sicherheit eingehende Datenverkehrsregeln](#bkmk_inbound)  
  
3.  [Zum Konfigurieren der Windows-Firewall mit erweiterter Sicherheit ausgehenden Datenverkehrsregeln](#bkmk_outbound)  
  
> [!TIP]  
> Im folgenden Verfahren Sie werden gebeten, erstellen ein Gruppenrichtlinienobjekt in der Standarddomänenrichtlinie, für die Bereitstellung sinnvoll ist jedoch Sie das Objekt in einer Organisationseinheit (OU) oder einem anderen Container erstellen können.  
  
Sie müssen ein Mitglied sein **Domänen-Admins**, oder eine gleichwertige Durchführung dieser Verfahren.  
  
## <a name="bkmk_gp"></a>Ein Gruppenrichtlinienobjekt erstellen und Konfigurieren von BranchCache-Modi  
  
1.  Klicken Sie auf einem Computer, auf denen die Active Directory-Domänendienste-Serverrolle, im Server-Manager installiert ist, auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird geöffnet.  
  
2.  In der Gruppenrichtlinien-Verwaltungskonsole, erweitern Sie den folgenden Pfad: **Gesamtstruktur:** *"Beispiel.com"*, **Domänen**, *"Beispiel.com"*, **Group Policy Objects**, wobei *"Beispiel.com"* ist der Name der Domäne, in dem zu konfigurierenden BranchCache-Clientcomputerkonten befinden.  
  
3.  Mit der rechten Maustaste **Group Policy Objects**, und klicken Sie dann auf **neu**. Die **Gruppenrichtlinienobjekt** Dialogfeld wird geöffnet. In **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt (GPO). Geben Sie beispielsweise, wenn Sie das BranchCache-Clientcomputer-Objekt zu benennen möchten, **BranchCache-Clientcomputern**. Klicken Sie auf **OK**.  
  
4.  In der Gruppenrichtlinien-Verwaltungskonsole, stellen Sie sicher, dass **Group Policy Objects** ausgewählt ist, und klicken Sie im Detailbereich mit der Maustaste des Gruppenrichtlinienobjekts, das Sie gerade erstellt haben. Wenn Sie Ihre Gruppenrichtlinienobjekt BranchCache-Clientcomputer mit dem Namen, z. B. Maustaste **BranchCache-Clientcomputern**. Klicken Sie auf **bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.  
  
5.  Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen: Richtliniendefinitionen (ADMX-Dateien) aus dem lokalen Computer abgerufen**, **Netzwerk**, **BranchCache**.  
  
6.  Klicken Sie auf **BranchCache**, und doppelklicken Sie dann im Detailbereich auf **BranchCache aktivieren**. Im Dialogfeld für die Einstellung der Richtlinie wird geöffnet.  
  
7.  In der **BranchCache aktivieren** Dialogfeld, klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.  
  
8.  So aktivieren Sie den verteilten Cachemodus BranchCache, klicken Sie im Detailbereich, doppelklicken Sie auf **festlegen BranchCache verteilten Cachemodus**. Im Dialogfeld für die Einstellung der Richtlinie wird geöffnet.  
  
9. In der **festlegen BranchCache verteilten Cachemodus** Dialogfeld, klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.  
  
10. Besitzen Sie eine oder mehrere Filialen, in dem Bereitstellen von BranchCache im Modus für gehostete Caches und Sie bereitgestellt haben gehosteten Cacheserver in diesen Zweigstellen, doppelklicken Sie auf **aktivieren automatische gehosteten Cache der Ermittlung von Service Connection Point**. Im Dialogfeld für die Einstellung der Richtlinie wird geöffnet.  
  
11. In der **aktivieren automatische gehosteten Cache der Ermittlung von Service Connection Point** Dialogfeld, klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Wenn Sie beide Aktivieren der **festlegen BranchCache verteilten Cachemodus** und die **aktivieren automatische gehosteten Cache der Ermittlung von Service Connection Point** Richtlinieneinstellungen, Client-Computern ausgeführt werden im verteilten Cachemodus BranchCache, wenn sie einen gehosteten Cacheserver in der Filiale gefunden, an welcher Stelle sie im Modus für gehostete Caches funktionieren.  
  
12. Verwenden Sie die folgenden Verfahren, um Firewall-Einstellungen auf Clientcomputern mithilfe von Gruppenrichtlinien zu konfigurieren.  
  
## <a name="bkmk_inbound"></a>Zum Konfigurieren der Windows-Firewall mit erweiterter Sicherheit eingehende Datenverkehrsregeln  
  
1.  In der Gruppenrichtlinien-Verwaltungskonsole, erweitern Sie den folgenden Pfad: **Gesamtstruktur:** *"Beispiel.com"*, **Domänen**, *"Beispiel.com"*, **Group Policy Objects**, wobei *"Beispiel.com"* ist der Name der Domäne, in dem zu konfigurierenden BranchCache-Clientcomputerkonten befinden.  
  
2.  In der Gruppenrichtlinien-Verwaltungskonsole, stellen Sie sicher, dass **Group Policy Objects** ausgewählt ist, und klicken Sie im Detailbereich mit der Maustaste die BranchCache-Clientcomputer Gruppenrichtlinienobjekt, das Sie zuvor erstellt haben. Wenn Sie Ihre Gruppenrichtlinienobjekt BranchCache-Clientcomputer mit dem Namen, z. B. Maustaste **BranchCache-Clientcomputern**. Klicken Sie auf **bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.  
  
3.  Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad: **Computerkonfiguration**, **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, **Windows-Firewall mit erweiterter Sicherheit**, **Windows-Firewall mit erweiterter Sicherheit - LDAP**, **eingehende Regeln**.  
  
4.  Mit der rechten Maustaste **eingehende Regeln**, und klicken Sie dann auf **neue Regel**. Der neue eingehende Regel-Assistent wird geöffnet.  
  
5.  In **Regeltyp**, klicken Sie auf **vordefiniert**, erweitern Sie die Liste der Optionen, und klicken Sie dann auf **BranchCache – Inhaltsabruf (verwendet HTTP)**. Klicken Sie auf **Weiter**.  
  
6.  In **vordefinierte Regeln**, klicken Sie auf **Weiter**.  
  
7.  In **Aktion**, stellen Sie sicher, dass **Verbindung zulassen,** ausgewählt ist, und klicken Sie dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen auswählen, **Verbindung zulassen,** für den BranchCache-Client auf diesem Port Datenverkehr empfangen kann.  
  
8.  Um die WS-Discovery-Firewallausnahme zu erstellen, erneut Maustaste **eingehende Regeln**, und klicken Sie dann auf **neue Regel**. Der neue eingehende Regel-Assistent wird geöffnet.  
  
9. In **Regeltyp**, klicken Sie auf **vordefiniert**, erweitern Sie die Liste der Optionen, und klicken Sie dann auf **BranchCache – Peerermittlung (verwendet WSD)**. Klicken Sie auf **Weiter**.  
  
10. In **vordefinierte Regeln**, klicken Sie auf **Weiter**.  
  
11. In **Aktion**, stellen Sie sicher, dass **Verbindung zulassen,** ausgewählt ist, und klicken Sie dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen auswählen, **Verbindung zulassen,** für den BranchCache-Client auf diesem Port Datenverkehr empfangen kann.  
  
## <a name="bkmk_outbound"></a>Zum Konfigurieren der Windows-Firewall mit erweiterter Sicherheit ausgehenden Datenverkehrsregeln  
  
1.  In der Gruppenrichtlinienverwaltungs-Editor-Konsole mit der rechten Maustaste **ausgehende Regeln**, und klicken Sie dann auf **neue Regel**. Der neue ausgehende Regel-Assistent wird geöffnet.  
  
2.  In **Regeltyp**, klicken Sie auf **vordefiniert**, erweitern Sie die Liste der Optionen, und klicken Sie dann auf **BranchCache – Inhaltsabruf (verwendet HTTP)**. Klicken Sie auf **Weiter**.  
  
3.  In **vordefinierte Regeln**, klicken Sie auf **Weiter**.  
  
4.  In **Aktion**, stellen Sie sicher, dass **Verbindung zulassen,** ausgewählt ist, und klicken Sie dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen auswählen, **Verbindung zulassen,** für den BranchCache-Client auf diesem Port Datenverkehr senden kann.  
  
5.  Um die WS-Discovery-Firewallausnahme zu erstellen, erneut Maustaste **ausgehende Regeln**, und klicken Sie dann auf **neue Regel**. Der neue ausgehende Regel-Assistent wird geöffnet.  
  
6.  In **Regeltyp**, klicken Sie auf **vordefiniert**, erweitern Sie die Liste der Optionen, und klicken Sie dann auf **BranchCache – Peerermittlung (verwendet WSD)**. Klicken Sie auf **Weiter**.  
  
7.  In **vordefinierte Regeln**, klicken Sie auf **Weiter**.  
  
8.  In **Aktion**, stellen Sie sicher, dass **Verbindung zulassen,** ausgewählt ist, und klicken Sie dann auf **Fertig stellen**.  
  
    > [!IMPORTANT]  
    > Sie müssen auswählen, **Verbindung zulassen,** für den BranchCache-Client auf diesem Port Datenverkehr senden kann.  
  


