---
title: Schritt 11 konfigurieren Sie die Bereitstellung für mehrere Standorte
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cbdeb1d-5f7c-4360-bcc1-ab40d3cd8040
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c95fb641c0d0fa3161caadfa2eb769e12b47672d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283226"
---
# <a name="step-11-configure-the-multisite-deployment"></a>Schritt 11 konfigurieren Sie die Bereitstellung für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Um eine Bereitstellung für mehrere Standorte zu konfigurieren, nehmen Sie Änderungen an den aktuellen RAS-Konfigurationsassistenten auf EDGE1, aktivieren Sie das Feature für mehrere Standorte und dann fügen Sie 2-EDGE1 als zweite Einstiegspunkt hinzu.  
  
- Konfigurieren des Remotezugriffs auf EDGE1  
  
- Aktivieren Sie die Konfiguration für mehrere Standorte auf EDGE1  
  
- 2-EDGE1 als zweite-Einstiegspunkt hinzufügen  
  
## <a name="configDA"></a>Konfigurieren des Remotezugriffs auf EDGE1  
  
1.  Auf der **starten** geben**RAMgmtUI.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**.  
  
3.  Im mittleren Bereich der Konsole in der **Schritt 2 RAS-Server** Bereich, klicken Sie auf **bearbeiten**.  
  
4.  Klicken Sie auf **Präfixkonfiguration**. Auf der **Präfixkonfiguration** auf der Seite **Präfixe des internen Netzwerks IPv6**, geben Sie **2001:db8:1:: / 64; 2001:db8:2:: / 64**. In **IPv6-Präfix, die DirectAccess-Clientcomputer zugewiesen**, geben Sie **2001:db8:1:1000:: / 64**, klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen** .  
  
5.  Im mittleren Bereich der Konsole in der **Schritt 3 Infrastrukturserver** Bereich, klicken Sie auf **bearbeiten**.  
  
6.  Klicken Sie auf **DNS-Suffix-Suchliste**. Auf der **DNS-Suffixsuchliste** Seite, stellen Sie sicher, dass die **Konfigurieren von DirectAccess-Clients mit dem Suffix-Suchliste für DNS-Client** das Kontrollkästchen aktiviert ist und dass die **"corp.contoso.com"** und **corp2.corp.contoso.com** Domänensuffixe angezeigt, der **zu verwendende Domänensuffixe** auf **Weiter**, und klicken Sie dann auf "Fertig stellen".  
  
7.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig stellen**.  
  
8.  Auf der **Remote Zugriffsüberprüfung** (Dialogfeld), überprüfen Sie die Konfigurationseinstellungen, und klicken Sie dann auf **übernehmen**. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
9. In der **Aufgaben** Bereich, klicken Sie auf **Verwaltungsserver aktualisieren**, und klicken Sie auf **schließen** Abschluss.  
  
## <a name="EnabledMultisite"></a>Aktivieren Sie die Konfiguration für mehrere Standorte auf EDGE1  
  
1.  In der Remotezugriffs-Verwaltungskonsole in der **Aufgaben** Bereich, klicken Sie auf **aktivieren mehrere Standorte**.  
  
2.  Assistenten zum Aktivieren der Bereitstellung für mehrere Standorte auf die **Vorbemerkungen** auf **Weiter**.  
  
3.  Auf der **Bereitstellungsname** auf der Seite **Namen der Bereitstellung für mehrere Standorte**, Typ **Contoso**im **erster Einstiegspunkt Namen**, Typ **Edge1-Site**, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Eintrag Punktauswahl** auf **Einstiegspunkte automatisch zuweisen, und ermöglichen Sie Clients manuell auswählen**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **globalen Lastenausgleich** auf **Nein, verwenden Sie keine globalen Lastenausgleich**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Clientunterstützung** auf **können Client-Computern mit Windows 7 ausführen, um Zugriff auf diesen Einstiegspunkt**, und klicken Sie auf **hinzufügen**.  
  
7.  Auf der **Gruppen auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen**, Typ **Win7_Clients_Site1**, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Client-GPO-Einstellungen** auf **Weiter**.  
  
9. Auf der **Zusammenfassung** auf **Commit**.  
  
10. Auf der **Multisite-Bereitstellung aktivieren** Dialogfeld klicken Sie auf **schließen** und Aktivieren von Multisite-Bereitstellungs-Assistenten klicken Sie dann auf **schließen**.  
  
## <a name="AddEP"></a>2-EDGE1 als zweite-Einstiegspunkt hinzufügen  
  
1.  In der Remotezugriffs-Verwaltungskonsole in der **Aufgaben** Bereich, klicken Sie auf **fügen einen Einstiegspunkt**.  
  
2.  Hinzufügen einen Einstiegspunkt-Assistenten auf der **Punkt Eingabedetails** auf der Seite **RAS-Server**, Typ **2-edge1.corp2.corp.contoso.com**im **Eintrag Zeigen Sie Namen**, Typ **2-Edge1-Site**, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **Netzwerktopologie** auf **Edge**, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Netzwerkname oder IP-Adresse** auf der Seite **Geben Sie den öffentlichen Namen oder IP-Adresse, die von Clients zum Verbinden mit dem RAS-Server verwendet**, Typ **2-edge1.contoso.com**, und Klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Netzwerkadapter** Seite, stellen Sie sicher, dass die **externen Adapter** ist **Internet**, **des internen Adapters** ist **2 -"Corpnet"** , das Zertifikat ist **CN = 2-edge1.contoso.com**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Präfixkonfiguration** auf der Seite **IPv6-Präfix, die DirectAccess-Clientcomputer zugewiesen**, Typ **2001:db8:2:2000:: / 64**, und klicken Sie dann auf **weiter** .  
  
7.  Auf der **Clientunterstützung** auf **können Client-Computern mit Windows 7 ausführen, um Zugriff auf diesen Einstiegspunkt**, und klicken Sie auf **hinzufügen**.  
  
8.  Auf der **Gruppen auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen**, Typ **Win7_Clients_Site2**, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Client-GPO-Einstellungen** auf **Weiter**.  
  
10. Auf der **Server-GPO-Einstellungen** auf **Weiter**.  
  
11. Auf der **Zusammenfassung** auf **Commit**.  
  
12. Auf der **Einstiegspunkt hinzufügen** Dialogfeld klicken Sie auf **schließen** , und klicken Sie auf den Einstiegspunkt des Assistenten zum Hinzufügen von, **schließen**.  
  


