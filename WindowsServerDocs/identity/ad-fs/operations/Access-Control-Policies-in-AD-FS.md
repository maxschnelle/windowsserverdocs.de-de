---
ms.assetid: 102eeeb1-6c55-42a2-b321-71a7dab46146
title: Zugriffssteuerungsrichtlinien in AD FS
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 101cab68d7c79bb107f1d6ef73900d9a4475b6ea
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="access-control-policies-in-windows-server-2016-ad-fs"></a>Zugriffssteuerungsrichtlinien in Windows Server 2016 AD FS

>Gilt für: Windows Server 2016

  
## <a name="access-control-policy-templates-in-ad-fs"></a>Access Policy Steuerelementvorlagen in AD FS  
Active Directory Federation Services unterstützt jetzt die Verwendung von Vorlagen für Access-Steuerelement.  Mithilfe von Vorlagen für Access-Steuerelement kann ein Administrator Richtlinieneinstellungen erzwingen, durch die Vorlage für eine Gruppe von vertrauenden Seiten (RPs) zuweisen. Administratoren kann Updates in der Richtlinienvorlage und auch die Änderungen werden automatisch angewendet, um die vertrauenden Seiten ist kein Benutzereingriff erforderlich.  
  
## <a name="what-are-access-control-policy-templates"></a>Was sind Vorlagen für Access-Steuerelement?  
Die AD FS-Core-Pipeline für die Verarbeitung der Gruppenrichtlinie umfasst drei Phasen: Authentifizierung, Autorisierung und Anspruch Ausstellung. AD FS-Administratoren müssen derzeit eine Richtlinie für die einzelnen Phasen separat zu konfigurieren.  Dies beinhaltet auch das Verständnis der Auswirkungen dieser Richtlinien und diese Richtlinien zwischen Abhängigkeitseigenschaften verfügen. Darüber hinaus müssen Administratoren verstehen, die Regel Sprache und Autor benutzerdefinierte Anspruchsregeln So aktivieren Sie einige einfache/allgemeine Richtlinie (z. b. Blockieren von externen Zugriff).  
  
Welche Vorlagen Zugriffssteuerungsrichtlinie ersetzen ist angeblich dieses alte Modell, in dem Administratoren haben, so konfigurieren Sie mithilfe von Ausstellungsautorisierungsregeln, Sprache.  Die alte PowerShell-Cmdlets von Ausstellungsautorisierungsregeln gelten weiterhin, aber es schließen sich gegenseitig aus das neue Modell. Administratoren können entweder das neue Modell oder der alte Modell verwendet.  Das neue Modell kann Administratoren steuern, wann zum Gewähren von Zugriff, einschließlich der Durchsetzung von Multi-Factor Authentication.  
  
Access Policy Steuerelementvorlagen verwenden ein Modell zulassen.  Dies bedeutet standardmäßig, hat kein Benutzer zugreifen und müssen explizit gewährt werden.  Allerdings ist dies nicht einfach All oder nichts zulassen.  Administratoren können die Zulassungsregel Ausnahmen hinzufügen.  Beispielsweise kann ein Administrator Zugriff basierend auf einem bestimmten Netzwerk durch diese Option, und geben Sie den IP-Adressbereich gewähren möchten.  Jedoch der Administrator hinzufügen kann und eine Ausnahme aus, z. B. der Administrator möglicherweise eine Ausnahme aus einem bestimmten Netzwerk hinzufügen und die IP-Adressbereich angeben.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP2.PNG)  
  
## <a name="built-in-access-control-policy-templates-vs-custom-access-control-policy-templates"></a>Integrierten Zugriff Steuerelement Richtlinie Vorlagen oder benutzerdefinierten Zugriff Richtlinie Steuerelementvorlagen  
AD FS umfasst mehrere integrierte Access Policy Steuerelementvorlagen.  Diese Zielen einige häufige Szenarien, die den gleichen Satz von Anforderungen, z. B. Client Zugriffsrichtlinie für Office 365 haben.  Diese Vorlagen werden nicht geändert.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP3.PNG)  
  
Um mehr Flexibilität, um Ihren geschäftlichen Anforderungen beheben bereitzustellen, können Administratoren ihren Zugriff Vorlagen erstellen.  Diese können geändert werden, nach der Erstellung und Änderungen an der benutzerdefinierten Vorlage gelten für alle RPs die durch diese Vorlagen gesteuert werden.  Zum Hinzufügen eine benutzerdefinierten Vorlage klicken Sie einfach hinzufügen Zugriffssteuerungsrichtlinie aus in AD FS-Verwaltungs.  
  
Um eine Vorlage zu erstellen, muss ein Administrator zunächst angeben, unter welchen Umständen für tokenausstellungs und/oder Delegierung eine Anforderung genehmigt wird. Bedingung und Aktion Optionen werden in der folgenden Tabelle angezeigt.   Bedingungen fett können vom Administrator mit anderen oder neue Werte weiter konfiguriert werden. Administrator kann auch Ausnahmen angeben, wenn einer vorhanden ist. Wenn eine Bedingung erfüllt ist, wird eine Zulassungsaktion wird nicht ausgelöst werden, wenn eine angegeben Ausnahme und die eingehende Anforderung entspricht, die in der Ausnahme angegebene Bedingung.  
  
|Benutzer zulassen|Mit Ausnahme von| 
| --- | --- | 
 |Von **bestimmten** Netzwerk|Von **bestimmten** Netzwerk<br /><br />Von **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauensebenen<br /><br />Mit **bestimmten** Ansprüche in der Anforderung|  
|Von **bestimmten** Gruppen|Von **bestimmten** Netzwerk<br /><br />Von **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauensebenen<br /><br />Mit **bestimmten** Ansprüche in der Anforderung|  
|Von Geräten mit **bestimmten** Vertrauensebenen|Von **bestimmten** Netzwerk<br /><br />Von **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauensebenen<br /><br />Mit **bestimmten** Ansprüche in der Anforderung|  
|Mit **bestimmten** Ansprüche in der Anforderung|Von **bestimmten** Netzwerk<br /><br />Von **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauensebenen<br /><br />Mit **bestimmten** Ansprüche in der Anforderung|  
|Und eine mehrstufige Authentifizierung|Von **bestimmten** Netzwerk<br /><br />Von **bestimmten** Gruppen<br /><br />Von Geräten mit **bestimmten** Vertrauensebenen<br /><br />Mit **bestimmten** Ansprüche in der Anforderung|  
  
Wenn ein Administrator mehrere Bedingungen auswählt, werden sie von **und** Beziehung. Aktionen schließen sich gegenseitig aus, und für eine Regel können Sie nur dann eine Aktion auswählen. Wenn Admin mehrere Ausnahmen auswählt, werden sie von einer **oder** Beziehung. Einige Beispiele Regel Richtlinie sind unten aufgeführt:  
  
|**Richtlinie**|**Regeln für**|
| --- | --- |  
|Extranet-Zugriff erfordert MFA<br /><br />Alle Benutzer sind zulässig.|**Regel #1**<br /><br />von **extranet**<br /><br />und mit der MFA<br /><br />Zulassen<br /><br />**Regel 2**<br /><br />von **Intranet**<br /><br />Zulassen|  
|Externer Zugriff sind nicht zulässig, mit Ausnahme von nicht-FTE<br /><br />Intranetzugriff für FTE auf Gerät dem Arbeitsplatz beigetreten sind zulässig.|**Regel #1**<br /><br />Von **extranet**<br /><br />und von **nicht FTE** Gruppe<br /><br />Zulassen<br /><br />**Regel #2**<br /><br />von **Intranet**<br /><br />und von **mit dem Arbeitsplatz verbundene** Gerät<br /><br />und von **FTE** Gruppe<br /><br />Zulassen|  
|Extranet-Zugriff erfordert MFA mit Ausnahme von "Admin Service"<br /><br />Alle Benutzer sind zulässig, für den Zugriff auf|**Regel #1**<br /><br />von **extranet**<br /><br />und mit der MFA<br /><br />Zulassen<br /><br />Mit Ausnahme von **Admin-Service-Servergruppe**<br /><br />**Regel #2**<br /><br />immer<br /><br />Zulassen|  
|nicht-Arbeitsplatz verbundenen Gerät zugreifen extranet erfordert MFA<br /><br />AD-Fabric für Intranet- und extranet-Zugriff zulassen|**Regel #1**<br /><br />von **Intranet**<br /><br />Und von **AD-Fabric** Gruppe<br /><br />Zulassen<br /><br />**Regel #2**<br /><br />von **extranet**<br /><br />und von **nicht mit dem Arbeitsplatz beigetreten** Gerät<br /><br />und von **AD-Fabric** Gruppe<br /><br />und mit der MFA<br /><br />Zulassen<br /><br />**Regel #3**<br /><br />von **extranet**<br /><br />und von **mit dem Arbeitsplatz verbundene** Gerät<br /><br />und von **AD-Fabric** Gruppe<br /><br />Zulassen|  
  
## <a name="parameterized-policy-template-vs-non-parameterized-policy-template"></a>Parametrisierte Vorlage Vs-Richtlinie nicht parametrisierten Richtlinienvorlage  
Zugriffsrichtlinien werden können  
  
Eine Vorlage für parametrisierte ist eine Vorlage, die Parameter verfügt. Der Administrator muss den Wert für diesen Parameter eingeben, wenn RPs.An Administrator Zuweisen dieser Vorlage vornehmen kann nicht parametrisierte Richtlinienvorlage nachdem es erstellt wurde.  Ein Beispiel für eine parametrisierte Richtlinie ist die integrierte Richtlinie, die bestimmte Gruppe zulassen.  Wenn diese Richtlinie auf eine RP angewendet wird, muss dieser Parameter angegeben werden.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP5.PNG)  
  
Eine Vorlage nicht parametrisierten ist eine Vorlage, die nicht über Parameter verfügt. Ein Administrator kann diese Vorlage RPS zuweisen, ohne alle erforderlichen Eingaben und kann Änderungen an einer Vorlage nicht parametrisierten vornehmen, nachdem es erstellt wurde.  Ein Beispiel hierfür ist die integrierte Richtlinie, alle Benutzer zulassen und MFA erfordern.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP4.PNG)  
  
## <a name="how-to-create-a-non-parameterized-access-control-policy"></a>Vorgehensweise beim Erstellen einer nicht parametrisierten Zugriffssteuerungsrichtlinie  
Zum Erstellen einer nicht parametrisierten Access Control-Richtlinie mithilfe des folgenden Verfahrens  
  
#### <a name="to-create-a-non-parameterized-access-control-policy"></a>Erstellen Sie eine nicht parametrisierten Zugriffssteuerungsrichtlinie  
  
1.  Wählen Sie Zugriffsrichtlinien, und klicken Sie auf der rechten Seite auf Zugriffssteuerungsrichtlinie hinzufügen, aus der AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Beispiel: Benutzer mit authentifizierten Geräte zulassen.  
  
3.  Klicken Sie unter **Zugriff gewähren, wenn eine der folgenden Regeln erfüllt sind**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, aktivieren Sie das Kontrollkästchen neben **von Geräten mit bestimmten Vertrauensebene**  
  
5.  Wählen Sie Sie unten auf den unterstrichenen **bestimmte**  
  
6.  Wählen Sie im Fenster mit von diesem Knacken **authentifiziert** aus der Dropdownliste aus.  Klicken Sie auf **Ok**.  
  
    ![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP6.PNG)  
  
7.  Klicken Sie auf **Ok**. Klicken Sie auf **Ok**.  
  
    ![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP7.PNG)  
  
## <a name="how-to-create-a-parameterized-access-control-policy"></a>Vorgehensweise beim Erstellen einer parametrisierte Zugriffssteuerungsrichtlinie  
Zum Erstellen eines Steuerelements parametrisierte Zugriff Richtlinie mithilfe des folgenden Verfahrens  
  
#### <a name="to-create-a-parameterized-access-control-policy"></a>Erstellen Sie eine parametrisierte Zugriffssteuerungsrichtlinie  
  
1.  Wählen Sie Zugriffsrichtlinien, und klicken Sie auf der rechten Seite auf Zugriffssteuerungsrichtlinie hinzufügen, aus der AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Beispiel: ermöglichen Sie Benutzern mit einer bestimmten Anspruch.  
  
3.  Klicken Sie unter **Zugriff gewähren, wenn eine der folgenden Regeln erfüllt sind**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, aktivieren Sie das Kontrollkästchen neben **mit bestimmten Ansprüche in der Anforderung**  
  
5.  Wählen Sie Sie unten auf den unterstrichenen **bestimmte**  
  
6.  Wählen Sie im Fenster mit von diesem Knacken **-Parameter angegeben, wenn der Zugriffssteuerungsrichtlinie zugewiesen ist**.  Klicken Sie auf **Ok**.  
  
    ![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP8.PNG)  
  
7.  Klicken Sie auf **Ok**. Klicken Sie auf **Ok**.  
  
    ![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP9.PNG)  
  
## <a name="how-to-create-a-custom-access-control-policy-with-an-exception"></a>Vorgehensweise beim Erstellen einer benutzerdefinierten Zugriffssteuerungsrichtlinie mit einer Ausnahme  
Zum Erstellen eines Steuerelements Zugriff-Richtlinie mit einer Ausnahme mithilfe des folgenden Verfahrens.  
  
#### <a name="to-create-a-custom-access-control-policy-with-an-exception"></a>Erstellen Sie eine benutzerdefinierte Zugriffssteuerungsrichtlinie mit einer Ausnahme  
  
1.  Wählen Sie Zugriffsrichtlinien, und klicken Sie auf der rechten Seite auf Zugriffssteuerungsrichtlinie hinzufügen, aus der AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Beispiel: erlaubt Benutzern mit Geräten authentifiziert, aber nicht verwaltet.  
  
3.  Klicken Sie unter **Zugriff gewähren, wenn eine der folgenden Regeln erfüllt sind**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, aktivieren Sie das Kontrollkästchen neben **von Geräten mit bestimmten Vertrauensebene**  
  
5.  Wählen Sie Sie unten auf den unterstrichenen **bestimmte**  
  
6.  Wählen Sie im Fenster mit von diesem Knacken **authentifiziert** aus der Dropdownliste aus.  Klicken Sie auf **Ok**.  
  
7.  Unter außer, aktivieren Sie das Kontrollkästchen neben **von Geräten mit bestimmten Vertrauensebene**  
  
8.  Im unteren Bereich unter, es sei denn, wählen Sie den unterstrichenen **bestimmte**  
  
9. Wählen Sie im Fenster mit von diesem Knacken **verwaltet** aus der Dropdownliste aus.  Klicken Sie auf **Ok**.  
  
10. Klicken Sie auf **Ok**. Klicken Sie auf **Ok**.  
  
    ![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP10.PNG)  
  
## <a name="how-to-create-a-custom-access-control-policy-with-multiple-permit-conditions"></a>Vorgehensweise beim Erstellen einer benutzerdefinierten Zugriffssteuerungsrichtlinie mit mehreren zulassen  
Zum Erstellen einer Zugriffsrichtlinie für das Steuerelement mit mehreren zulassen gehen Bedingungen  
  
#### <a name="to-create-a-parameterized-access-control-policy"></a>Erstellen Sie eine parametrisierte Zugriffssteuerungsrichtlinie  
  
1.  Wählen Sie Zugriffsrichtlinien, und klicken Sie auf der rechten Seite auf Zugriffssteuerungsrichtlinie hinzufügen, aus der AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Beispiel: ermöglichen es Benutzern mit einem bestimmten Anspruch und bestimmten Gruppe.  
  
3.  Klicken Sie unter **Zugriff gewähren, wenn eine der folgenden Regeln erfüllt sind**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, aktivieren Sie das Kontrollkästchen neben **aus einer bestimmten Gruppe** und **mit bestimmten Ansprüche in der Anforderung**  
  
5.  Wählen Sie Sie unten auf den unterstrichenen **bestimmten** für die erste Bedingung, neben Gruppen  
  
6.  Wählen Sie im Fenster mit von diesem Knacken **-Parameter angegeben, wenn die Richtlinie zugewiesen ist**.  Klicken Sie auf **Ok**.  
  
7.  Wählen Sie Sie unten auf den unterstrichenen **bestimmten** für die zweite Bedingung, neben Ansprüche  
  
8.  Wählen Sie im Fenster mit von diesem Knacken **-Parameter angegeben, wenn der Zugriffssteuerungsrichtlinie zugewiesen ist**.  Klicken Sie auf **Ok**.  
  
9. Klicken Sie auf **Ok**. Klicken Sie auf **Ok**.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP12.PNG)  
  
## <a name="how-to-assign-an-access-control-policy-to-a-new-application"></a>Zuweisen eine Zugriffsrichtlinie für das Steuerelement zu einer neuen Anwendung  
Zuweisen einer Zugriffsrichtlinie für das Steuerelement zu einer neuen Anwendung ist ziemlich einfach und hat nun in den Assistenten zum Hinzufügen einer RP integriert wurde.  Aus dem Assistenten für Vertrauensstellungen der vertrauenden Seite Party können Sie der Zugriffssteuerungsrichtlinie auswählen, die Sie zuweisen möchten.  Dies ist erforderlich, wenn eine neue Vertrauensstellung zu erstellen.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP13.PNG)  
  
## <a name="how-to-assign-an-access-control-policy-to-an-existing-application"></a>Zuweisen eine Zugriffsrichtlinie für das Steuerelement zu einer vorhandenen Anwendung  
Zuweisen einer Zugriffsrichtlinie für das Steuerelement zu einer vorhandenen Anwendung wählen Sie einfach die Anwendung von Vertrauensstellungen der vertrauenden Seite und auf der rechten Maustaste auf **Zugriffssteuerungsrichtlinie bearbeiten**.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP14.PNG)  
  
Von hier aus können Sie auswählen der Zugriffssteuerungsrichtlinie und wenden Sie sie auf die Anwendung.  
  
![Zugriffsrichtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP15.PNG)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 

