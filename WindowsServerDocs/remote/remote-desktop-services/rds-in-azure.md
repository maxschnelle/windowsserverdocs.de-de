---
title: Nahtloses Bereitstellen von RDS mit ARM und Azure Marketplace
description: Erfahren Sie, wie eine kleine RDS-Bereitstellung in Azure mithilfe von ARM-Vorlagen und dem Azure Marketplace erstellen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f72ceb6-6f90-48f6-bfc3-bdad63984ce7
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 02/10/2017
ms.openlocfilehash: e4de3d4ac14a0dbc5500fd7ab8bd8f1568f3da53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823081"
---
# <a name="seamlessly-deploy-rds-with-arm-and-azure-marketplace"></a>Nahtloses Bereitstellen von RDS mit ARM und Azure Marketplace

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2

Remote Desktop Services (RDS) ist eine Plattform Ihrer Wahl, um Windows-Desktops und Anwendungen kostengünstig zu hosten. Können Sie eine [Azure Marketplace-Angebot](#basic-rds-through-the-azure-marketplace) oder [schnellstartvorlage](#Customized-RDS-using-Quickstart-templates) , schnell ein RDS auf Azure IaaS-Bereitstellung zu erstellen. Azure Marketplace wird eine Testdomäne für Sie somit einen einfache Mechanismus für Tests und Proof of Concept-erstellt. Die schnellstartvorlagen, auf der anderen Seite können Sie eine vorhandene Domäne, sodass sie ein hervorragendes Tool zum Erstellen einer produktionsumgebung verwenden. Nach der Einrichtung können Sie auf die veröffentlichten Desktops und Anwendungen von verschiedenen Plattformen und Geräten verbinden verwenden die Microsoft Remote Desktop-apps für Windows, Mac, iOS und Android.

## <a name="basic-rds-through-the-azure-marketplace"></a>Grundlegendes RDS über den Azure Marketplace

Erstellen Ihre Bereitstellung über den Azure Marketplace ist die schnellste Möglichkeit zum Einrichten und ausführen. Wenn alles erledigt ist, sieht Ihre Umgebung wie der [grundlegenden RDS-Architektur](desktop-hosting-logical-architecture.md#basic-deployment). Das Angebot erstellt alle RDS-Komponenten, die Sie benötigen – müssen Sie lediglich einige Informationen angeben. 

Sie müssen die folgenden Informationen angeben, wenn Sie das Marketplace-Angebot bereitstellen:
- Benutzername des Administrators und das Kennwort. Dies ist ein neuer Benutzer, der die Bereitstellung verwalten.
- DNS-Namen und AD-Domänenname. Hierbei handelt es sich um neue Ressourcen, die erstellt werden. Stellen Sie sicher, dass die Namen von Bedeutung sind.
- Größe des virtuellen Computers. Sie können die Größe der VMs, für die RDSH-Endpunkte verwenden auswählen. Sie können die Größe auch manuell ändern, nach der ersten Bereitstellung können Sie die virtuellen Computer für Ihre Workloads und Kosten optimieren.

Verwenden Sie diese Schritte, um Ihre RDS-Bereitstellung mit geringem Speicherverbrauch aus dem Azure Marketplace zu erstellen: 

1. Starten Sie den Azure Marketplace RDS-Bereitstellung:
   1. Melden Sie sich bei der [Azure-Portal](https://portal.azure.com).
   2. Klicken Sie auf **neu** Ihrer Bereitstellung hinzufügen.
   3. Geben Sie "RDS" in das Suchfeld ein, und drücken Sie die EINGABETASTE.
   4. Klicken Sie auf **Remote Desktop Services (RDS) – Basic - Dev/Test**, und klicken Sie dann auf **erstellen**.
   5. Führen Sie die Schritte im Portal zum Erstellen und Bereitstellen von RDS. Fügen Sie wichtige Konfigurationsdetails wie die oben aufgeführten Informationen ein. 
2. Verbinden Sie mit Ihrer Bereitstellung. Wenn die Bereitstellung abgeschlossen ist, überprüfen Sie den Abschnitt "Outputs" abschließenden Schritte abgeschlossen und eine Verbindung mit Ihrer Bereitstellung.
   1. Herunterladen und ausführen [dieses PowerShell-Skript](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328) auf Ihrem Testgerät keine Verbindung mit der RDS-Bereitstellung erforderlichen Zertifikate zu installieren. 
   
      Dieser Schritt ist nur erforderlich, während der Testphase. Wenn Sie in der Produktion von RDS in Azure bereitstellen, stellen Sie darauf, befolgen bewährte Methoden wie z.B. erwerben und nutzen ein öffentlich vertrauenswürdiges SSL-Zertifikat auf Ihren Webservern.

   2. Wenn Sie aufgefordert werden, melden Sie sich bei Ihrem Azure-Konto. Wählen Sie die Azure-Abonnement, Ressourcengruppe und öffentliche IP-Adresse, die für diese neue Bereitstellung erstellt wurde.
   3. Wenn das Skript abgeschlossen ist, wird die RD-Webseite im Standardbrowser gestartet. Sie können die RD-Webseite Vergewissern Sie sich durch Vergleichen die URL für die Seite, um die DNS-Adresse, die Sie während der Bereitstellung angegeben haben. 
   
      Melden Sie sich die Administratoranmeldeinformationen, die Sie während der Bereitstellung, finden in den Standarddesktop veröffentlicht, die für Sie erstellt haben. Sie können die Benutzer auch die Remotedesktop-Website so testen Sie ihre Desktops und Anwendungen senden.

      > [!TIP]
      > Vergessen Sie den Domänenbenutzer Name oder Administrator? Sie gelangen zurück auf die neue Ressourcengruppe im Portal, klicken Sie auf **Bereitstellungen**, und zeigen Sie dann die Parameter, die Sie eingegeben haben.

Nachdem Sie eine RDS-Bereitstellung verfügen, können Sie [hinzufügen und Verwalten von Benutzern](rds-user-management.md).

## <a name="customized-rds-using-quickstart-templates"></a>Benutzerdefinierte RDS mit schnellstartvorlagen

Sie können Azure Resource Manager-Vorlagen verwenden, von RDS in Azure bereitstellen. Dies ist besonders nützlich, wenn Sie möchten von einer grundlegenden RDS-Bereitstellung verfügen, aber vorhandene Komponenten (z. B. AD), die Sie verwenden möchten. Im Gegensatz zu den Marketplace bieten können Sie weitere Anpassungen wie die Verwendung eines vorhandenen AD auf einem virtuellen Netzwerk vornehmen, verwenden ein benutzerdefiniertes Betriebssystemabbild für die RDSH-VMs, und klicken Sie auf die Schichten auf hohe Verfügbarkeit für RDS-Komponenten. Nach dem Hinzufügen zur hochverfügbarkeit von jeder Komponente, Ihrer Umgebung sieht die [hoch verfügbar RDS-Architektur](desktop-hosting-logical-architecture.md#highly-available-deployment).

Verwenden Sie diese Schritte, um Ihre RDS-Bereitstellung mit geringem Speicherverbrauch mit einer Azure-RDS-Vorlage zu erstellen: 

1. Wählen Sie Ihre Azure-schnellstartvorlage:
   1. Wechseln Sie zu der [RDS-Azure-Quickstart-Templates](https://aka.ms/rdautomation) Standort.
   2. Wählen Sie die Vorlage, die mit übereinstimmt, was Sie tun möchten. Stellen Sie sicher, dass alle Voraussetzungen für diese bestimmte Vorlage erfüllt. (Z. B. Wenn Sie möchten ein benutzerdefiniertes Image für Ihre virtuellen Computer verwenden, stellen Sie sicher, dass Sie bereits dieses Image in Azure Storage-Konto hochgeladen haben.)
   3. Klicken Sie auf **Bereitstellen in Azure**.
   4. Sie müssen einige Details (z.B. Benutzername des Administrators, AD-Domänenname) Geben Sie im Azure-Portal. Dies hängt von der ausgewählten Vorlage.
   5. Klicken Sie auf **Kauf**.
2. Verbinden Sie mit Ihrer Bereitstellung. 
   1. Herunterladen und ausführen [dieses PowerShell-Skript](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328) auf Ihrem Testgerät keine Verbindung mit der RDS-Bereitstellung erforderlichen Zertifikate zu installieren. 
   
      Dieser Schritt ist nur erforderlich, während der Testphase. Wenn Sie in der Produktion von RDS in Azure bereitstellen, stellen Sie darauf, befolgen bewährte Methoden wie z.B. erwerben und nutzen ein öffentlich vertrauenswürdiges SSL-Zertifikat auf Ihren Webservern.

   2. Wenn Sie aufgefordert werden, melden Sie sich bei Ihrem Azure-Konto. Wählen Sie die Azure-Abonnement, Ressourcengruppe und öffentliche IP-Adresse, die für diese neue Bereitstellung erstellt wurde.
   3. Wenn das Skript abgeschlossen ist, wird die RD-Webseite im Standardbrowser gestartet. Sie können die RD-Webseite Vergewissern Sie sich durch Vergleichen die URL für die Seite, um die DNS-Adresse, die Sie während der Bereitstellung angegeben haben. 
   
      Melden Sie sich die Administratoranmeldeinformationen, die Sie während der Bereitstellung, finden in den Standarddesktop veröffentlicht, die für Sie erstellt haben. Sie können die Benutzer auch die Remotedesktop-Website so testen Sie ihre Desktops und Anwendungen senden.

      > [!TIP]
      > Vergessen Sie den Domänenbenutzer Name oder Administrator? Sie gelangen zurück auf die neue Ressourcengruppe im Portal, klicken Sie auf **Bereitstellungen**, und zeigen Sie dann die Parameter, die Sie eingegeben haben.

Nachdem Sie eine RDS-Bereitstellung verfügen, können Sie [hinzufügen und Verwalten von Benutzern](rds-user-management.md).
