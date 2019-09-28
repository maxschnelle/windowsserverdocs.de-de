---
title: Erstellen lokaler Benutzerkonten
description: Erfahren Sie mehr über die drei Arten von Benutzerkonten in Multipoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33321932-4266-4961-9924-2cb4620bfcb4
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: 874d9cbdb56c59693cb5843a898b9ebd6893d674
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405111"
---
# <a name="create-local-user-accounts"></a>Erstellen lokaler Benutzerkonten
Drei Ebenen lokaler Benutzerkonten können in mithilfe des Multipoint-Managers erstellt werden: Standard Benutzerkonten; Multipoint-Dashboardbenutzer mit eingeschränkten Administratorrechten und vollständige Administrator Benutzerkonten.  
  
Verwenden Sie das folgende Verfahren, um ein lokales Benutzerkonto auf einem Multipoint-Server zu erstellen. Wenn Ihre Umgebung mehrere Multipoint-Server umfasst und Sie möchten, dass sich der Benutzer in einer beliebigen Station auf einem beliebigen Server anmelden kann, müssen Sie auf jedem Server ein lokales Benutzerkonto erstellen. Das Setup weist einige Einschränkungen auf. In einer Domänen Umgebung können Sie Benutzern auch die Verwendung ihrer Domänen Konten erlauben. Eine Übersicht über die Optionen finden Sie unter [Planen von Benutzerkonten für Ihre Windows-MultiPoint Services-Umgebung](Plan-user-accounts-for-your-MultiPoint-services-environment.md).  
   
1.  Melden Sie sich als Administrator beim Server an, und öffnen Sie den Multipoint-Manager.  
  
2.  Klicken Sie auf die Registerkarte **Benutzer** , und klicken Sie dann auf **Benutzerkonto hinzufügen**.  
  
    Der Assistent zum Hinzufügen eines Benutzerkontos wird geöffnet.  
  
3.  Geben Sie einen Kontonamen und ein Kennwort für das neue Benutzerkonto ein, und klicken Sie dann auf **weiter**.  
  
4.  Wählen Sie den Typ des Benutzerkontos aus, das Sie erstellen möchten:  
  
    -   **Standard Benutzer** : kann sich bei einer Station anmelden und Benutzer Aufgaben durchführen, aber keinen Zugriff auf Multipoint Manager oder das Multipoint Server-Dashboard haben. das System kann nicht heruntergefahren werden.  
  
    -   **Multipoint-Dashboardbenutzer** : verfügt über eingeschränkte Administratorrechte. Ein Dashboardbenutzer kann das Dashboard öffnen und Aufgaben ausführen, wie z. b. das Anmelden von Benutzern vom System oder das Herunterfahren des Multipoint-Server Computers, aber der Benutzer hat keinen Zugriff auf den Multipoint-Manager.  
  
    -   Administrator Verfügt über vollständige Administratorrechte in Multipoint Server. Beispielsweise kann ein Administrator den Multipoint-Manager ausführen, Benutzer hinzufügen und löschen, Systemeinstellungen ändern und Treiber aktualisieren.  
  
5.  Klicken Sie auf **weiter**und dann auf **Fertig** stellen, um das Benutzerkonto zu erstellen.