---
title: Schritt 11 Konfigurieren der Bereitstellung für mehrere Standorte
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cbdeb1d-5f7c-4360-bcc1-ab40d3cd8040
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3a80697665eeb67c2dda0d4d25201c7d02ed0c7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404806"
---
# <a name="step-11-configure-the-multisite-deployment"></a>Schritt 11 Konfigurieren der Bereitstellung für mehrere Standorte

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Um eine Bereitstellung für mehrere Standorte zu konfigurieren, nehmen Sie Änderungen am Assistenten für die Remote Zugriffs Konfiguration auf Edge1 vor, aktivieren Sie die Funktion für mehrere Standorte, und fügen Sie dann 2-Edge1 als zweiten Einstiegspunkt hinzu.  
  
- Konfigurieren des Remote Zugriffs auf Edge1  
  
- Aktivieren der Konfiguration für mehrere Standorte auf Edge1  
  
- 2-Edge1 als zweiten Einstiegspunkt hinzufügen  
  
## <a name="configDA"></a>Konfigurieren des Remote Zugriffs auf Edge1  
  
1.  Geben Sie auf dem **Start** Bildschirm**ramgmtui. exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole auf **Konfiguration**.  
  
3.  Klicken Sie im mittleren Bereich der Konsole im Bereich **Schritt 2** RAS-Server auf **Bearbeiten**.  
  
4.  Klicken Sie auf **Präfix Konfiguration**. Geben Sie auf der Seite **Präfix Konfiguration** in **interne Netzwerk-IPv6-Präfixe** **2001: db8:1::/64; 2001: db8:2::/64**ein. Geben Sie im **IPv6-Präfix, das DirectAccess-Client Computern zugewiesen**ist, **2001: db8:1: 1000::/64**ein, klicken Sie auf **weiter**und dann auf **Fertig**stellen.  
  
5.  Klicken Sie im mittleren Bereich der Konsole im Bereich **Schritt 3 Infrastruktur Server** auf **Bearbeiten**.  
  
6.  Klicken Sie auf **DNS-Suffixsuchliste**. Vergewissern Sie sich auf der Seite **DNS-Suffixsuchliste** , dass das Kontrollkästchen **DirectAccess-Clients mit DNS-clientsuffixsuchliste konfigurieren** aktiviert ist, und dass die Domänen Suffixe **Corp.contoso.com** und **corp2.Corp.contoso.com** aktiviert sind. in der Liste **zu verwendende Domänen Suffixe** angezeigt werden, klicken Sie auf **weiter**und dann auf Fertigstellen.  
  
7.  Klicken Sie im mittleren Bereich der Konsole auf **Fertig**stellen.  
  
8.  Überprüfen Sie im Dialogfeld **Remote Zugriffs Überprüfung** die Konfigurationseinstellungen, und klicken Sie **dann auf über**nehmen. Klicken Sie im Dialogfeld **Anwenden der Einstellungen zum Einrichten des Remotezugriffs** auf **Schließen**.  
  
9. Klicken Sie im Bereich **Tasks** auf **Verwaltungs Server aktualisieren**, und klicken Sie dann auf **Schließen** , wenn Sie fertig sind.  
  
## <a name="EnabledMultisite"></a>Aktivieren der Konfiguration für mehrere Standorte auf Edge1  
  
1.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole im Bereich **Tasks** auf **Multisite aktivieren**.  
  
2.  Klicken Sie im Assistenten zum Aktivieren der Bereitstellung für mehrere Standorte auf der Seite **Vorbemerkungen** auf **weiter**.  
  
3.  Geben Sie auf der Seite **Bereitstellungs Name** unter **Name der Bereitstellung für mehrere Standorte**den Wert " **Edge1-Site**" **ein, und**klicken Sie **dann auf** **weiter**.  
  
4.  Klicken Sie auf der Seite **Einstiegspunkt Auswahl** auf **Einstiegspunkte automatisch zuweisen, und aktivieren Sie die Option Clients manuell auswählen**, und klicken Sie dann auf **weiter**.  
  
5.  Klicken Sie auf der Seite **Globaler Lastenausgleich** auf **Nein, verwenden Sie keinen globalen Lastenausgleich**, und klicken Sie dann auf **weiter**.  
  
6.  Klicken Sie auf der Seite **Client Unterstützung** auf **Client Computern, auf denen Windows 7 ausgeführt wird, auf diesen Einstiegspunkt zugreifen**, und klicken Sie auf **Hinzufügen**.  
  
7.  Geben Sie im Dialogfeld **Gruppen auswählen** unter **Geben Sie die zu ausgewäfnenden Objektnamen ein den Namen** **Win7_Clients_Site1**ein, klicken Sie auf **OK**, und klicken Sie dann auf **weiter**.  
  
8.  Klicken Sie auf der Seite **Einstellungen des Client** -Gruppenrichtlinien Objekts auf **weiter**.  
  
9. Klicken Sie auf der Seite **Zusammenfassung** auf **Commit**.  
  
10. Klicken Sie im Dialogfeld **Bereitstellung für mehrere Standorte** aktivieren auf **Schließen** , und klicken Sie dann im Assistenten zum Aktivieren der Bereitstellung für mehrere Standorte auf **Schließen**.  
  
## <a name="AddEP"></a>2-Edge1 als zweiten Einstiegspunkt hinzufügen  
  
1.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole im Bereich **Tasks** auf **Einstiegspunkt hinzufügen**.  
  
2.  Geben Sie im Assistenten zum Hinzufügen von Einstiegspunkten auf der Seite **Details zum Einstiegspunkt** unter RAS- **Server**den Namen **2-Edge1.corp2.Corp.contoso.com**ein, geben Sie unter **Einstiegspunkt Name den Namen** **2-Edge1-Site**ein, und klicken Sie dann auf **weiter**.  
  
3.  Klicken Sie auf der Seite **Netzwerktopologie** auf **Edge**und dann auf **weiter**.  
  
4.  Geben Sie auf der Seite **Netzwerkname oder IP-Adresse** unter **Geben Sie den öffentlichen Namen oder die IP-Adresse ein, die von Clients zum Herstellen einer Verbindung mit dem Remote Zugriffs Server verwendet**wird, **2-Edge1.contoso.com**ein, und klicken Sie dann auf **weiter**.  
  
5.  Vergewissern Sie sich auf der Seite **Netzwerkadapter** , dass der **externe Adapter** **Internet**, der **interne Adapter** **2-Corpnet**, das Zertifikat **CN = 2-Edge1.contoso.com**ist, und klicken Sie dann auf **weiter**.  
  
6.  Geben Sie auf der Seite **Präfix Konfiguration** unter **IPv6-Präfix, das DirectAccess-Client Computern zugewiesen**ist Folgendes ein **: 2001: db8:2: 2000::/64**, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie auf der Seite **Client Unterstützung** auf **Client Computern, auf denen Windows 7 ausgeführt wird, auf diesen Einstiegspunkt zugreifen**, und klicken Sie auf **Hinzufügen**.  
  
8.  Geben Sie im Dialogfeld **Gruppen auswählen** unter **Geben Sie die zu ausgewäfnenden Objektnamen ein den Namen** **Win7_Clients_Site2**ein, klicken Sie auf **OK**, und klicken Sie dann auf **weiter**.  
  
9. Klicken Sie auf der Seite **Einstellungen des Client** -Gruppenrichtlinien Objekts auf **weiter**.  
  
10. Klicken Sie auf der Seite **Server-GPO-Einstellungen** auf **weiter**.  
  
11. Klicken Sie auf der Seite **Zusammenfassung** auf **Commit**.  
  
12. Klicken Sie im Dialogfeld **Einstiegspunkt hinzufügen** auf **Schließen** , und klicken Sie dann im Assistenten zum Hinzufügen von Einstiegspunkten auf **Schließen**.  
  


