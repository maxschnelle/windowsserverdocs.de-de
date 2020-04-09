---
title: Installieren von MultiPoint Services
description: Erfahren Sie, wie Sie Multipoint Services in Windows Server 2016 installieren und konfigurieren.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: ab82782f4ac1ffa8532dc23ad9340329a65765de
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859213"
---
# <a name="install-multipoint-services"></a>Installieren von MultiPoint Services
Wenn Sie einen Server von Grund auf neu installieren, befolgen Sie diese Anweisungen, um Multipoint Services zu installieren.  

Nachdem Sie Windows Server 2016 installiert haben, melden Sie sich erfolgreich als Administrator an. Verwenden Sie die Server-Manager, in der Sie Multipoint Services aktivieren können. Der Server-Manager wird beim Start automatisch geöffnet. Wählen Sie auf dem Dashboard **Rollen und Features hinzufügen** aus, um Multipoint Services zu aktivieren, und befolgen Sie die Anweisungen im Assistenten.

Im Abschnitt für den Installationstyp können Sie entweder mit dem 
- Rollenbasierte oder featurebasierte Installation oder
- Installation von Remotedesktopdiensten

Für Standard Bereitstellungen von Multipoint Services empfiehlt es sich, die Remotedesktopdienste Installation auszuwählen, mit der Sie die Multipoint Services-Rolle unter Bereitstellungstyp bequem auswählen können. Bei der rollenbasierten Installation müssen Sie in der Liste der Rollen **Multipoint Services** auswählen. Der Server wird nach der erfolgreichen Installation neu gestartet.  
  
## <a name="configure-your-primary-station"></a>Konfigurieren der primären Station  
  
1.  Geben Sie auf der Seite **Multipoint-Server Station erstellen** den angegebenen Buchstaben von der Tastatur für diesen Monitor ein. Mit dem richtigen Schlüssel Eintrag werden die Tastatur und die Maus für diese Station verknüpft.  
2.  Melden Sie sich als Administrator an.  