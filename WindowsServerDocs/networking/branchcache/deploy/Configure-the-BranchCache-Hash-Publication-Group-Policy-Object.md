---
title: Konfigurieren des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6e9a338dfebfb1dfadb258bcbdfcc8d75bd3ea86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862961"
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>Konfigurieren des Gruppenrichtlinienobjekts für BranchCache-Hashveröffentlichung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, die BranchCache-hashveröffentlichung (Group Policy Object, GPO) so konfigurieren, dass alle Dateiserver, die Sie der Name der Organisationseinheit hinzugefügt haben die gleiche Richtlinie hashveröffentlichungseinstellung angewendet haben.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
> [!NOTE]  
> Vor dem Ausführen dieses Verfahrens müssen Sie die BranchCache Dateiserver-Organisationseinheit, erstellen die Dateiserver in die Organisationseinheit verschieben und die BranchCache-hashveröffentlichung GPO erstellen. Weitere Informationen finden Sie unter [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>So konfigurieren Sie die BranchCache-hashveröffentlichung Group Policy Object  
  
1.  Führen Sie Windows PowerShell als Administrator geben **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Gruppenrichtlinienverwaltung**, und klicken Sie anschließend auf **OK**.  
  
4.  Erweitern Sie in der Gruppenrichtlinienverwaltungs-MMC den Pfad zum Gruppenlinienobjekt BranchCache-Hashveröffentlichung, das Sie zuvor erstellt haben. Wenn der Name der Gesamtstruktur z. B. „beispiel.com“ der der Domäne „beispiel1.com“ und der Name des Gruppenrichtlinienobjekts **BranchCache-Hashveröffentlichung** lautet, erweitern Sie den folgenden Pfad: **Gruppenrichtlinienverwaltung**, **Gesamtstruktur: "example.com"**, **Domänen**, **example1.com**, **Gruppenrichtlinienobjekte**,  **BranchCache-Hashveröffentlichung**.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt **BranchCache-Hashveröffentlichung**, und wählen Sie **Bearbeiten** aus. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.  
  
6.  Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad ein: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **Netzwerk**, **LanMan-Server**.  
  
7.  Klicken Sie in der Konsole des Gruppenrichtlinienverwaltungs-Editors auf **LanMan-Server**. Doppelklicken Sie im Detailbereich auf **Hashveröffentlichung für BranchCache**. Das Dialogfeld **Hashveröffentlichung für BranchCache** wird geöffnet.  
  
8.  Klicken Sie im Dialogfeld **Hashveröffentlichung für BranchCache** auf **Aktiviert**.  
  
9. In **Optionen**, klicken Sie auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**, und klicken Sie dann auf einen der folgenden:  
  
    1.  Um hashveröffentlichung für alle freigegebenen Ordner aktivieren, für alle Dateiserver, die Sie mit der Organisationseinheit hinzugefügt haben, klicken Sie auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**.  
  
    2.  Um Hashveröffentlichung nur für freigegebene Ordner zu aktivieren, für die BranchCache aktiviert ist, klicken Sie auf **Hashveröffentlichung nur für freigegebene Ordner mit aktiviertem BranchCache zulassen.**  
  
    3.  Um keine Hashveröffentlichung für alle freigegebenen Ordner auf dem Computer zuzulassen, auch wenn BranchCache auf den Dateifreigaben aktiviert ist, klicken Sie auf **Hashveröffentlichung für keinen freigegebenen Ordner zulassen**.  
  
10. Klicken Sie auf **OK**.  
  
> [!NOTE]  
> In den meisten Fällen müssen Sie die MMC-Konsole speichern und aktualisieren, um die vorgenommenen Konfigurationsänderungen anzuzeigen.  
  


