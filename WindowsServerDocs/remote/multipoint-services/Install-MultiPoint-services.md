---
title: Installieren von MultiPoint Services
description: Informationen Sie zum Installieren und Konfigurieren von MultiPoint Services in Windows Server 2016
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 52a824bbca3e9f2e1c7823601f6208ae19ae50ef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866221"
---
# <a name="install-multipoint-services"></a>Installieren von MultiPoint Services
Führen Sie diese Anweisungen zum Installieren von MultiPoint Services, wenn Sie einen Server von Grund auf neu installieren.  

Nachdem Sie Windows Server 2016 wurde erfolgreich installiert haben sich als Administrator anmelden. Verwenden Sie den Server-Manager, in dem Sie MultiPoint Services aktivieren können. Der Server-Manager wird automatisch beim Start geöffnet. Wählen Sie auf der Dashboard **Rollen und Features hinzufügen** MultiPoint-Dienste aktiviert, und befolgen die Anweisungen im Assistenten.

Im Abschnitt für den Installationstyp kann man entweder mit der 
- Rollenbasierte oder featurebasierte Installation oder
- Installation von Remotedesktopdiensten

Für standard MultiPoint Services-Bereitstellungen empfehlen wir, wählen Sie die Remote Desktop Services-Installation dadurch, dass Sie einfach die MultiPoint Services-Rolle unter Bereitstellungstyp auswählen. Für die rollenbasierte Installation müssen Sie auf **MultiPoint Services** in der Liste der Rollen. Der Server wird nach der erfolgreichen Installation neu gestartet.  
  
## <a name="configure-your-primary-station"></a>Konfigurieren Sie Ihre primäre station  
  
1.  Auf der **erstellen Sie eine MultiPoint Server-Station** geben den angegebenen Buchstaben der Tastatur für den Monitor. Der richtige Schlüssel Eintrag ordnet die Tastatur und Maus für diese Station.  
2.  Melden Sie sich als Administrator.  