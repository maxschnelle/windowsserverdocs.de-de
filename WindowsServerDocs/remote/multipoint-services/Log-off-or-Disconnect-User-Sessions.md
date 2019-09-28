---
title: Abmelden oder Trennen von Benutzersitzungen
description: Erfahren Sie, wie Sie einen Benutzer manuell abmelden.
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e9bbcdc-e33b-481e-8b46-787a4f6d58bc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: c636af35a78eab76d69c68b6f506b64dcb555f81
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395265"
---
# <a name="log-off-or-disconnect-user-sessions"></a>Abmelden oder Trennen von Benutzersitzungen
Multipoint Services-Benutzer können sich bei Ihren Desktop Sitzungen anmelden und abmelden, genauso wie bei jeder beliebigen Windows-Sitzung. Benutzer können Ihre Sitzung auch trennen oder aussetzen, sodass die Multipoint Services-Station nicht verwendet wird, aber Ihre Sitzung bleibt im Arbeitsspeicher des Multipoint Services-Systems aktiv.  
  
Darüber hinaus können Administratoren die Sitzung eines Benutzers beenden, wenn der Benutzer von der Multipoint Services-Sitzung entfernt wurde oder vergessen hat, sich vom System abzumelden.  
  
## <a name="logging-off-or-disconnecting-a-session"></a>Abmelden oder Trennen einer Sitzung  
In der folgenden Tabelle werden verschiedene Möglichkeiten beschrieben, mit deren Hilfe Sie bzw. andere Benutzer eine Sitzung abmelden, anhalten oder beenden können.  
  
|||  
|-|-|  
|**Aktion**|**Entsprechende**|  
|Klicken Sie auf **Start**, klicken Sie auf Einstellungen, klicken Sie auf den Benutzernamen (obere rechte Ecke), und klicken Sie dann auf **Abmelden**.|Die Sitzung wird beendet, und die Station steht für alle Benutzer zur Anmeldung zur Verfügung.|  
|Klicken Sie auf **Start**, auf **Einstellungen**, auf „Ein/Aus“ und dann auf **Trennen**.|Ihre Sitzung wird getrennt und bleibt im Arbeitsspeicher des Computers erhalten. Die Station steht für denselben sowie andere Benutzer zur Anmeldung zur Verfügung.|  
|Klicken Sie auf **Start**, klicken Sie auf Einstellungen, klicken Sie auf den Benutzernamen (obere rechte Ecke), und klicken Sie dann auf **Sperren** .|Die Station ist gesperrt, und Ihre Sitzung bleibt im Arbeitsspeicher des Computers erhalten.|  
  
## <a name="suspending-or-ending-a-users-session"></a>Anhalten oder Beenden der Sitzung eines Benutzers  
In der folgenden Tabelle werden die verschiedenen Optionen beschrieben, die Sie als Administrator zum Trennen oder Beenden der Sitzung eines Benutzers verwenden können.  
  
|||  
|-|-|  
|**Aktion**|**Entsprechende**|  
|**Suspend** Verwenden Sie im Multipoint-Manager die Registerkarte **Stationen** , um die Sitzung des Benutzers anzuhalten. Weitere Informationen finden Sie im Thema [Anhalten von Benutzersitzungen im aktiven Zustand](Suspend-and-Leave-User-Session-Active.md).|Die Sitzung des Benutzers wird beendet und im Arbeitsspeicher des Computers beibehalten. Die Station steht für denselben sowie andere Benutzer zur Anmeldung zur Verfügung. Der Benutzer kann sich an derselben oder einer anderen Station anmelden und seine Arbeit fortsetzen.|  
|**Schließlich** Verwenden Sie im Multipoint-Manager die Registerkarte **Stationen** , um die Benutzersitzung zu beenden. Sie können auf der Registerkarte **Stationen** auch alle Benutzersitzungen beenden. Weitere Informationen finden Sie im Thema [Beenden einer Benutzersitzung](End-a-User-Session.md).|Die Sitzung des Benutzers wird beendet, und die Station steht für alle Benutzer zur Verfügung. Die Sitzung des Benutzers wird nicht mehr auf der Registerkarte **Stationen** angezeigt, und Sie befindet sich nicht im Arbeitsspeicher des Computers.|  
  
## <a name="see-also"></a>Siehe auch  
[Aussetzen und Benutzersitzung aktiv lassen](Suspend-and-Leave-User-Session-Active.md)  
[Beenden einer Benutzersitzung](End-a-User-Session.md)  
[Verwalten von Benutzer Desktops](manage-user-desktops-using-multipoint-dashboard.md)  
[Abmelden von Benutzersitzungen](Log-Off-User-Sessions.md)    