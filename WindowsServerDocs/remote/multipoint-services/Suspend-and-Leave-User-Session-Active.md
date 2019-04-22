---
title: Anhalten von Benutzersitzungen im aktiven Zustand
description: Erfahren Sie, wie einen Benutzer aus einer MultiPoint-Sitzung angehalten wird, ohne die getrennt werden
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5263bce3-fe92-4398-8393-2e3a4e05d530
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: cc4310e6f7609464cf037b750bec6e5e805e0b26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815221"
---
# <a name="suspend-and-leave-user-session-active"></a>Anhalten von Benutzersitzungen im aktiven Zustand
Sie können trennen oder die Benutzer im MultiPoint Services-System anhalten, wenn Sie nicht, um benutzersitzungen zu beenden möchten. Ein Benutzer kann eine Sitzung auch selbst trennen. Während eine Benutzersitzung angehalten ist, bleibt die Sitzung im Arbeitsspeicher des MultiPoint Services-Systems aktiv, bis der Computer heruntergefahren oder neu gestartet wird. Zu diesem Zeitpunkt werden alle angehaltenen Sitzungen beendet, und sämtliche nicht gespeicherte Arbeit geht verloren.  
  
1.  Öffnen Sie MultiPoint-Manager im stationsmodus, und klicken Sie dann auf die **Stationen** Registerkarte.  
  
2.  Klicken Sie in der Spalte **Computer** auf den Namen des Computers, dessen Sitzungen Sie anhalten möchten.  
  
3.  Klicken Sie unter **Stationsaufgaben** auf **Alle Stationen anhalten**.  
  
Nachdem eine Benutzersitzung angehalten wurde, kann sich der Benutzer an derselben oder einer anderen Station anmelden und seine Arbeit in der ursprünglichen Sitzung fortsetzen.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Benutzerdesktops](manage-user-desktops-using-multipoint-dashboard.md)  
[Abmelden oder Trennen von Benutzersitzungen](Log-off-or-Disconnect-User-Sessions.md)