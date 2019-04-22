---
title: Erstellen lokaler Benutzerkonten
description: Erfahren Sie Suchen des maßgeblichen drei Arten von Benutzerkonten in MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33321932-4266-4961-9924-2cb4620bfcb4
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: e2e5a6c79e6dcd603d19ca868df1d11fce2bf746
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823671"
---
# <a name="create-local-user-accounts"></a>Erstellen lokaler Benutzerkonten
Drei Ebenen von lokalen Benutzerkonten können erstellt werden, sich mit dem MultiPoint-Manager: Standardbenutzerkonten; MultiPoint-Dashboardbenutzer, die mit Administratorrechten eingeschränkter; und vollständige Administratorkonten.  
  
Verwenden Sie das folgende Verfahren, um ein lokales Benutzerkonto auf einem MultiPoint Server zu erstellen. Wenn Ihre Umgebung mehrere MultiPoint-Server umfasst und der Benutzer jede Station auf jedem Server anmelden können soll, müssen Sie ein lokales Benutzerkonto auf jedem Ihrer Server zu erstellen. Das Setup gelten einige Einschränkungen. In einer domänenumgebung können Sie auch Benutzer, die die Domänenkonten verwenden lassen. Eine Übersicht über die Optionen, finden Sie unter [Planen von Benutzerkonten für Ihre Windows MultiPoint Services-Umgebung](Plan-user-accounts-for-your-MultiPoint-services-environment.md).  
   
1.  Melden Sie sich an den Server als Administrator, und öffnen Sie MultiPoint-Manager.  
  
2.  Klicken Sie auf die **Benutzer** Registerkarte, und klicken Sie dann auf **Benutzerkonto hinzufügen**.  
  
    Den Assistenten zum Hinzufügen von Benutzer-Konto wird geöffnet.  
  
3.  Geben Sie einen Kontonamen und das Kennwort für das neue Benutzerkonto ein, und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie das Benutzerkonto, das Sie erstellen möchten:  
  
    -   **Standardbenutzer** : an eine Station anmelden und Benutzeraufgaben ausführen, können aber hat keinen Zugriff auf den MultiPoint-Manager oder das MultiPoint Server-Dashboard, und kann nicht das System heruntergefahren.  
  
    -   **MultiPoint-Dashboardbenutzer** -verfügt über eingeschränkte Administratorrechte. Ein Dashboardbenutzer das Dashboard öffnen und Ausführen von Aufgaben wie das Protokollieren von Benutzern aus dem System oder Herunterfahren des MultiPoint Server-Computers kann, aber der Benutzer verfügt nicht über Zugriff auf den MultiPoint-Manager.  
  
    -   **Administrator** verfügt über vollständige Administratorrechte in MultiPoint-Server. Beispielsweise kann ein Administrator MultiPoint-Manager ausführen, hinzufügen und Löschen von Benutzern, Systemeinstellungen ändern und Treiber aktualisieren.  
  
5.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen** um das Benutzerkonto zu erstellen.