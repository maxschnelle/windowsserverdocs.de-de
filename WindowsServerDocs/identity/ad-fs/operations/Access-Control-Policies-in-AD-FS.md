---
ms.assetid: 102eeeb1-6c55-42a2-b321-71a7dab46146
title: Zugriffssteuerungsrichtlinien in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 27eb5b4b52dd727afae5cffc60e7d9749dd5d59f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407766"
---
# <a name="access-control-policies-in-windows-server-2016-ad-fs"></a>Zugriffsrichtlinien in für Windows Server 2016 AD FS

  
## <a name="access-control-policy-templates-in-ad-fs"></a>Access Control Richtlinien Vorlagen in AD FS  
Active Directory-Verbunddienste (AD FS) unterstützt jetzt die Verwendung von Richtlinien Vorlagen für die Zugriffs Steuerung.  Mithilfe von Richtlinien Vorlagen für die Zugriffs Steuerung kann ein Administrator Richtlinien Einstellungen erzwingen, indem er die Richtlinien Vorlage einer Gruppe von vertrauenden Seiten (RPS) zuweist. Der Administrator kann auch Aktualisierungen an der Richtlinien Vorlage vornehmen, und die Änderungen werden automatisch auf die vertrauenden Seiten angewendet, wenn keine Benutzerinteraktion erforderlich ist.  
  
## <a name="what-are-access-control-policy-templates"></a>Was sind Access Control Richtlinien Vorlagen?  
Die AD FS Core-Pipeline für die Richtlinien Verarbeitung umfasst drei Phasen: Authentifizierung, Autorisierung und Anspruchs Ausstellung. Derzeit müssen AD FS Administratoren eine Richtlinie für jede dieser Phasen separat konfigurieren.  Dies umfasst auch das Verständnis der Auswirkungen dieser Richtlinien und, wenn diese Richtlinien eine gegenseitige Abhängigkeit aufweisen. Außerdem müssen Administratoren die Anspruchs Regel Sprache verstehen und benutzerdefinierte Regeln erstellen, um eine einfache/allgemeine Richtlinie zu aktivieren (z.b. externen Zugriff blockieren).  
  
Welche Zugriffs Steuerungs-Richtlinien Vorlagen sind das alte Modell, in dem Administratoren Ausstellungs Autorisierungs Regeln mithilfe der Anspruchs Sprache konfigurieren müssen.  Die alten PowerShell-Cmdlets der Ausstellungs Autorisierungs Regeln gelten weiterhin, aber Sie schließen das neue Modell gegenseitig aus. Administratoren können wählen, ob Sie das neue Modell oder das alte Modell verwenden möchten.  Mit dem neuen Modell können Administratoren steuern, wann der Zugriff gewährt werden soll, einschließlich der Durchsetzung der Multi-Factor Authentication.  
  
Zugriffs Steuerungs-Richtlinien Vorlagen verwenden ein Zulassungs Modell.  Dies bedeutet standardmäßig, dass niemand Zugriff hat und dass der Zugriff explizit erteilt werden muss.  Dabei handelt es sich jedoch nicht nur um eine all-oder Nothing-Berechtigung.  Administratoren können der Zulassungs Regel Ausnahmen hinzufügen.  Ein Administrator möchte z. b. möglicherweise den Zugriff auf Grundlage eines bestimmten Netzwerks gewähren, indem er diese Option auswählt und den IP-Adressbereich angibt.  Der Administrator kann beispielsweise hinzufügen und eine Ausnahme hinzufügen, der Administrator kann beispielsweise eine Ausnahme von einem bestimmten Netzwerk hinzufügen und diesen IP-Adressbereich angeben.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP2.PNG)  
  
## <a name="built-in-access-control-policy-templates-vs-custom-access-control-policy-templates"></a>Integrierte Zugriffs Steuerungs Richtlinien Vorlagen im Vergleich zu benutzerdefinierten Zugriffs Steuerungs Richtlinien Vorlagen  
AD FS umfasst mehrere integrierte Zugriffs Steuerungs Richtlinien Vorlagen.  Diese zielen auf einige gängige Szenarien ab, die über die gleichen Richtlinien Anforderungen verfügen, z. b. Client Zugriffsrichtlinien für Office 365.  Diese Vorlagen können nicht geändert werden.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP3.PNG)  
  
Um höhere Flexibilität bei der Bewältigung ihrer geschäftlichen Anforderungen zu bieten, können Administratoren eigene Zugriffsrichtlinien Vorlagen erstellen.  Diese können nach der Erstellung geändert werden, und Änderungen an der benutzerdefinierten Richtlinien Vorlage gelten für alle RPS, die von diesen Richtlinien Vorlagen gesteuert werden.  Um eine benutzerdefinierte Richtlinien Vorlage hinzuzufügen, klicken Sie in AD FS Verwaltung einfach auf Access Control Richtlinie hinzufügen.  
  
Zum Erstellen einer Richtlinien Vorlage muss ein Administrator zuerst festlegen, unter welchen Bedingungen eine Anforderung für die Tokenausstellung und/oder Delegierung autorisiert wird. Bedingungs-und Aktions Optionen sind in der folgenden Tabelle aufgeführt.   Fett formatierte Bedingungen können vom Administrator mit unterschiedlichen oder neuen Werten weiter konfiguriert werden. Der Administrator kann ggf. auch Ausnahmen angeben. Wenn eine Bedingung erfüllt ist, wird eine Zulassungs Aktion nicht ausgelöst, wenn eine Ausnahme angegeben wird und die eingehende Anforderung mit der in der Ausnahme angegebenen Bedingung übereinstimmt.  
  
|Benutzern gestatten|Davon| 
| --- | --- | 
 |Aus **spezifischem** Netzwerk|Aus **spezifischem** Netzwerk<br /><br />Aus **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauens Stufen<br /><br />Mit **bestimmten** Ansprüchen in der Anforderung|  
|Aus **bestimmten** Gruppen|Aus **spezifischem** Netzwerk<br /><br />Aus **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauens Stufen<br /><br />Mit **bestimmten** Ansprüchen in der Anforderung|  
|Von Geräten mit **bestimmten** Vertrauens Stufen|Aus **spezifischem** Netzwerk<br /><br />Aus **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauens Stufen<br /><br />Mit **bestimmten** Ansprüchen in der Anforderung|  
|Mit **bestimmten** Ansprüchen in der Anforderung|Aus **spezifischem** Netzwerk<br /><br />Aus **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauens Stufen<br /><br />Mit **bestimmten** Ansprüchen in der Anforderung|  
|Und erfordern die Multi-Factor Authentication|Aus **spezifischem** Netzwerk<br /><br />Aus **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauens Stufen<br /><br />Mit **bestimmten** Ansprüchen in der Anforderung|  
  
Wenn ein Administrator mehrere Bedingungen auswählt, bestehen diese aus der Beziehung **und** . Aktionen schließen sich gegenseitig aus, und für eine Richtlinien Regel können Sie nur eine Aktion auswählen. Wenn der Administrator mehrere Ausnahmen auswählt, handelt es sich um eine- **oder** -Beziehung. Unten sind einige Beispiele für Richtlinien Regeln aufgeführt:  
  
|**Richtlinie**|**Richtlinien Regeln**|
| --- | --- |  
|Der Extranetzugriff erfordert MFA.<br /><br />Alle Benutzer sind zulässig.|**Regel #1**<br /><br />aus **Extranet**<br /><br />und mit MFA<br /><br />Aufenthal<br /><br />**Regel 2**<br /><br />aus **Intranet**<br /><br />Aufenthal|  
|Externer Zugriff ist außer nicht-FTE nicht zulässig.<br /><br />Intranetzugriff für FTE auf Arbeitsplatz verknüpften Geräten ist zulässig.|**Regel #1**<br /><br />Aus **Extranet**<br /><br />und aus **nicht-FTE-** Gruppe<br /><br />Aufenthal<br /><br />**Regel #2**<br /><br />aus **Intranet**<br /><br />und vom mit dem **Arbeitsplatz verbundenen** Gerät<br /><br />und aus der Gruppe " **FTE** "<br /><br />Aufenthal|  
|Für den Extranetzugriff ist MFA außer "Service Admin" erforderlich.<br /><br />Alle Benutzer sind berechtigt, auf zuzugreifen.|**Regel #1**<br /><br />aus **Extranet**<br /><br />und mit MFA<br /><br />Aufenthal<br /><br />Mit Ausnahme der **Dienst Administrator Gruppe**<br /><br />**Regel #2**<br /><br />Immer<br /><br />Aufenthal|  
|für den Zugriff auf das Extranet nicht in den Arbeitsplatz eingebundenes Gerät erfordert MFA<br /><br />Zulassen von AD Fabric für Intranet-und Extranetzugriff|**Regel #1**<br /><br />aus **Intranet**<br /><br />Und aus der **AD Fabric** -Gruppe<br /><br />Aufenthal<br /><br />**Regel #2**<br /><br />aus **Extranet**<br /><br />und von **nicht mit dem Arbeitsplatz verknüpften** Geräten<br /><br />und aus der **AD Fabric** -Gruppe<br /><br />und mit MFA<br /><br />Aufenthal<br /><br />**Regel #3**<br /><br />aus **Extranet**<br /><br />und vom mit dem **Arbeitsplatz verbundenen** Gerät<br /><br />und aus der **AD Fabric** -Gruppe<br /><br />Aufenthal|  
  
## <a name="parameterized-policy-template-vs-non-parameterized-policy-template"></a>Parametrisierte Richtlinien Vorlage im Vergleich zu nicht parametrisierten Richtlinien Vorlagen  
Zugriffs Steuerungs Richtlinien können  
  
Eine parametrisierte Richtlinien Vorlage ist eine Richtlinien Vorlage, die über Parameter verfügt. Ein Administrator muss beim Zuweisen dieser Vorlage zu RPS.an den Wert für diese Parameter eingeben, wenn der Administrator keine Änderungen an der parametrisierten Richtlinien Vorlage vornehmen kann, nachdem er erstellt wurde.  Ein Beispiel für eine parametrisierte Richtlinie ist die integrierte Richtlinie, eine bestimmte Gruppe zulassen.  Wenn diese Richtlinie auf eine RP angewendet wird, muss dieser Parameter angegeben werden.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP5.PNG)  
  
Eine nicht parametrisierte Richtlinien Vorlage ist eine Richtlinien Vorlage, die keine Parameter enthält. Ein Administrator kann diese Vorlage RPS zuweisen, ohne dass eine Eingabe erforderlich ist, und kann Änderungen an einer nicht parametrisierten Richtlinien Vorlage vornehmen, nachdem Sie erstellt wurde.  Ein Beispiel hierfür ist die integrierte Richtlinie, alle zulassen und MFA erforderlich.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP4.PNG)  
  
## <a name="how-to-create-a-non-parameterized-access-control-policy"></a>Erstellen einer nicht parametrisierten Zugriffs Steuerungs Richtlinie  
Verwenden Sie das folgende Verfahren, um eine nicht parametrisierte Zugriffs Steuerungs Richtlinie zu erstellen:  
  
#### <a name="to-create-a-non-parameterized-access-control-policy"></a>So erstellen Sie eine nicht parametrisierte Zugriffs Steuerungs Richtlinie  
  
1.  Wählen Sie in AD FS Verwaltung auf der linken Seite Access Control Richtlinien aus, und klicken Sie mit der rechten Maustaste auf Access Control Richtlinie  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Erlauben Sie Benutzern mit authentifizierten Geräten.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt**ist auf **Hinzufügen**.  
  
4.  Aktivieren Sie unter Zulassen das Kontrollkästchen neben **Geräte mit spezifischer Vertrauens Ebene** .  
  
5.  Wählen Sie unten das unterstrichene **spezifische**  
  
6.  Wählen Sie im angezeigten Fenster in der Dropdown-Dropdown-Dropdown-Option **authentifiziert** aus.  Klicken Sie auf **OK**.  
  
    ![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP6.PNG)  
  
7.  Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
    ![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP7.PNG)  
  
## <a name="how-to-create-a-parameterized-access-control-policy"></a>Erstellen einer parametrisierten Zugriffs Steuerungs Richtlinie  
Verwenden Sie das folgende Verfahren, um eine parametrisierte Zugriffs Steuerungs Richtlinie zu erstellen:  
  
#### <a name="to-create-a-parameterized-access-control-policy"></a>So erstellen Sie eine parametrisierte Zugriffs Steuerungs Richtlinie  
  
1.  Wählen Sie in AD FS Verwaltung auf der linken Seite Access Control Richtlinien aus, und klicken Sie mit der rechten Maustaste auf Access Control Richtlinie  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Erlauben Sie Benutzern mit einem bestimmten Anspruch.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt**ist auf **Hinzufügen**.  
  
4.  Aktivieren Sie unter Zulassen das Kontrollkästchen neben **bestimmte Ansprüche in der Anforderung** .  
  
5.  Wählen Sie unten das unterstrichene **spezifische**  
  
6.  Wählen Sie im Fenster, das angezeigt wird, **den Parameter aus, der angegeben wird, wenn die Zugriffs Steuerungs Richtlinie zugewiesen wird**.  Klicken Sie auf **OK**.  
  
    ![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP8.PNG)  
  
7.  Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
    ![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP9.PNG)  
  
## <a name="how-to-create-a-custom-access-control-policy-with-an-exception"></a>Erstellen einer benutzerdefinierten Zugriffs Steuerungs Richtlinie mit einer Ausnahme  
Verwenden Sie das folgende Verfahren, um eine Zugriffs Steuerungs Richtlinie mit einer Ausnahme zu erstellen.  
  
#### <a name="to-create-a-custom-access-control-policy-with-an-exception"></a>So erstellen Sie eine benutzerdefinierte Zugriffs Steuerungs Richtlinie mit einer Ausnahme  
  
1.  Wählen Sie in AD FS Verwaltung auf der linken Seite Access Control Richtlinien aus, und klicken Sie mit der rechten Maustaste auf Access Control Richtlinie  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Benutzer mit authentifizierten Geräten zulassen, aber nicht verwaltet.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt**ist auf **Hinzufügen**.  
  
4.  Aktivieren Sie unter Zulassen das Kontrollkästchen neben **Geräte mit spezifischer Vertrauens Ebene** .  
  
5.  Wählen Sie unten das unterstrichene **spezifische**  
  
6.  Wählen Sie im angezeigten Fenster in der Dropdown-Dropdown-Dropdown-Option **authentifiziert** aus.  Klicken Sie auf **OK**.  
  
7.  Aktivieren Sie unter außer eine Kontrollkästchen neben **Geräte mit spezifischer Vertrauens Ebene** .  
  
8.  Wählen Sie unten unter außer die unterstrichene **spezifische**  
  
9. Wählen Sie im daraufhin angezeigten Fenster in der Dropdown-Dropdown-Dropdown-Option **verwaltet** aus.  Klicken Sie auf **OK**.  
  
10. Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
    ![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP10.PNG)  
  
## <a name="how-to-create-a-custom-access-control-policy-with-multiple-permit-conditions"></a>Erstellen einer benutzerdefinierten Zugriffs Steuerungs Richtlinie mit mehreren Zulassungsbedingungen  
Verwenden Sie das folgende Verfahren, um eine Zugriffs Steuerungs Richtlinie mit mehreren Zulassungsbedingungen zu erstellen.  
  
#### <a name="to-create-a-parameterized-access-control-policy"></a>So erstellen Sie eine parametrisierte Zugriffs Steuerungs Richtlinie  
  
1.  Wählen Sie in AD FS Verwaltung auf der linken Seite Access Control Richtlinien aus, und klicken Sie mit der rechten Maustaste auf Access Control Richtlinie  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Erlauben Sie Benutzern mit einem bestimmten Anspruch und einer bestimmten Gruppe.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt**ist auf **Hinzufügen**.  
  
4.  Aktivieren Sie unter Zulassen das Kontrollkästchen neben einer **bestimmten Gruppe** und **mit bestimmten Ansprüchen in der Anforderung** .  
  
5.  Wählen Sie unten die unterstrichene **spezifische** Bedingung für die erste Bedingung neben Gruppen aus.  
  
6.  Wählen Sie im Fenster, das angezeigt wird, **den Parameter aus, der angegeben wird, wenn die Richtlinie zugewiesen wird**.  Klicken Sie auf **OK**.  
  
7.  Wählen Sie unten die unterstrichene **spezifische** Bedingung für die zweite Bedingung nebenansprüche aus.  
  
8.  Wählen Sie im Fenster, das angezeigt wird, **den Parameter aus, der angegeben wird, wenn die Zugriffs Steuerungs Richtlinie zugewiesen wird**.  Klicken Sie auf **OK**.  
  
9. Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP12.PNG)  
  
## <a name="how-to-assign-an-access-control-policy-to-a-new-application"></a>Zuweisen einer Zugriffs Steuerungs Richtlinie zu einer neuen Anwendung  
Das Zuweisen einer Zugriffs Steuerungs Richtlinie zu einer neuen Anwendung ist recht unkompliziert und wurde nun in den Assistenten integriert, um eine RP hinzuzufügen.  Im Assistenten für Vertrauens Stellungen der vertrauenden Seite können Sie die Zugriffs Steuerungs Richtlinie auswählen, die Sie zuweisen möchten.  Dies ist eine Voraussetzung für das Erstellen einer neuen Vertrauensstellung der vertrauenden Seite.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP13.PNG)  
  
## <a name="how-to-assign-an-access-control-policy-to-an-existing-application"></a>Zuweisen einer Zugriffs Steuerungs Richtlinie zu einer vorhandenen Anwendung  
Wenn Sie einer vorhandenen Anwendung eine Zugriffs Steuerungs Richtlinie zuweisen, wählen Sie einfach die Anwendung aus den Vertrauens Stellungen der vertrauenden Seite aus, und klicken Sie auf der rechten Seite auf **Access Control**  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP14.PNG)  
  
Von hier aus können Sie die Zugriffs Steuerungs Richtlinie auswählen und Sie auf die Anwendung anwenden.  
  
![Zugriffs Steuerungs Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP15.PNG)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 

