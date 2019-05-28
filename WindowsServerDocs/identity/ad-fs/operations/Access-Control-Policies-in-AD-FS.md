---
ms.assetid: 102eeeb1-6c55-42a2-b321-71a7dab46146
title: Zugriffssteuerungsrichtlinien in AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c690f81620f97622a2f068b07c36e0a6c59e90d4
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190336"
---
# <a name="access-control-policies-in-windows-server-2016-ad-fs"></a>Zugriffsrichtlinien in für Windows Server 2016 AD FS

  
## <a name="access-control-policy-templates-in-ad-fs"></a>Access Control-Richtlinienvorlagen in AD FS  
Active Directory Federation Services unterstützt jetzt die Verwendung von Vorlagen für Access Control.  Mithilfe von Access Control-Richtlinienvorlagen kann Administrator Richtlinieneinstellungen erzwingen, durch die Richtlinienvorlage auf eine Gruppe von vertrauenden Seiten (RPs) zuweisen. Administrator kann auch Updates an der Vorlage vornehmen und die Änderungen gelten für die vertrauenden Seiten automatisch, wenn es kein Benutzereingriff erforderlich ist.  
  
## <a name="what-are-access-control-policy-templates"></a>Was sind die Access Control-Richtlinienvorlagen?  
Die AD FS-Core-Pipeline für die Verarbeitung der Gruppenrichtlinie erfolgt in drei Phasen: Authentifizierung, Autorisierung und Anspruch Ausstellung. Derzeit müssen AD FS-Administratoren eine Richtlinie für jede dieser Phasen separat zu konfigurieren.  Dies umfasst auch die Kenntnis der Auswirkungen dieser Richtlinien, und wenn diese Richtlinien zwischen Abhängigkeiten verfügen. Darüber hinaus müssen Administratoren verstehen die Regel Sprache und Autor von benutzerdefinierten Anspruchsregeln So aktivieren Sie einige einfache/allgemeine Richtlinie (z.B.) externen Zugriff blockieren).  
  
Welche Access Control-Richtlinie, die Vorlagen sind, ersetzen Sie dies wird Anspruchsanbieter dieses alte Modell, in dem Administratoren haben, so konfigurieren Sie mithilfe von Regeln für Ausstellungsautorisierung-Sprache.  Die alte PowerShell-Cmdlets von Ausstellungsautorisierungsregeln weiterhin gültig, aber schließen sich gegenseitig aus und das neue Modell. Administratoren können entweder auf das neue Modell oder dem alten Modell verwenden.  Das neue Modell kann Administratoren steuern, wann das Gewähren von Zugriff, einschließlich Multi-Factor Authentication zu erzwingen.  
  
Access Control-Richtlinienvorlagen verwenden ein Modell gewähren.  Dies bedeutet in der Standardeinstellung, hat Zugriff und den Zugriff explizit erteilt werden muss.  Allerdings ist dies nicht einfach alles oder nichts ermöglichen.  Administratoren können Ausnahmen für die IPSec Zulassungsregel hinzufügen.  Beispielsweise kann ein Administrator möchten Zugriff basierend auf einem bestimmten Netzwerk diese Option aus, und geben den IP-Adressbereich zu gewähren.  Jedoch der Administrator hinzufügen kann und die Ausnahme, z. B. der Administrator kann eine Ausnahme aus einem bestimmten Netzwerk hinzufügen und diese IP-Adressbereich angeben.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP2.PNG)  
  
## <a name="built-in-access-control-policy-templates-vs-custom-access-control-policy-templates"></a>Integrierten Zugriff Steuerelement Vorlagen Vs benutzerdefinierten Zugriff Steuerelement Richtlinie Richtlinienvorlagen  
AD FS umfasst mehrere integrierte Access Control-Richtlinienvorlagen.  Diese einige häufig verwendete Szenarien mit den gleichen Satz von Anforderungen, z. B. Clientzugriffsrichtlinie für Office 365 als Ziel.  Diese Vorlagen werden nicht geändert.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP3.PNG)  
  
Um mehr Flexibilität, um Ihre geschäftlichen Anforderungen zu ermöglichen, können Administratoren ihren eigenen Zugriff Vorlagen erstellen.  Diese können nach der Erstellung geändert werden, und Änderungen an benutzerdefinierten Richtlinienvorlage gelten für alle der RPS-Wert die von diesen Richtlinienvorlagen kontrolliert werden.  Zum Hinzufügen eine benutzerdefinierten Vorlage klicken Sie einfach Hinzufügen von Access Control-Richtlinie aus in AD FS-Verwaltung.  
  
Um eine Vorlage zu erstellen, muss ein Administrator zunächst angeben, unter welchen Bedingungen eine Anforderung für die tokenausstellung und/oder autorisiert wird. In der folgenden Tabelle werden die Bedingung und Aktion Optionen angezeigt.   Bedingungen in Fettschrift können vom Administrator mit verschiedenen oder neue Werte weiter konfiguriert werden. Administratoren kann auch Ausnahmen angeben, falls vorhanden. Wenn eine Bedingung erfüllt ist, wird eine IPSec Zulassungsaktion wird nicht ausgelöst, wenn eine angegebene Ausnahme vorhanden ist, und der eingehenden Anforderung passt, die in der Ausnahme angegebene Bedingung.  
  
|Benutzer zulassen|Mit der Ausnahme| 
| --- | --- | 
 |Von **bestimmte** Netzwerk|Von **bestimmte** Netzwerk<br /><br />Von **bestimmte** Gruppen<br /><br />Von Geräten mit **bestimmte** Vertrauensebenen<br /><br />Mit **bestimmte** Ansprüche in der Anforderung|  
|Von **bestimmte** Gruppen|Von **bestimmte** Netzwerk<br /><br />Von **bestimmte** Gruppen<br /><br />Von Geräten mit **bestimmte** Vertrauensebenen<br /><br />Mit **bestimmte** Ansprüche in der Anforderung|  
|Von Geräten mit **bestimmte** Vertrauensebenen|Von **bestimmte** Netzwerk<br /><br />Von **bestimmte** Gruppen<br /><br />Von Geräten mit **bestimmte** Vertrauensebenen<br /><br />Mit **bestimmte** Ansprüche in der Anforderung|  
|Mit **bestimmte** Ansprüche in der Anforderung|Von **bestimmte** Netzwerk<br /><br />Von **bestimmte** Gruppen<br /><br />Von Geräten mit **bestimmte** Vertrauensebenen<br /><br />Mit **bestimmte** Ansprüche in der Anforderung|  
|Und Multi-Factor Authentication anfordern|Von **bestimmte** Netzwerk<br /><br />Von **bestimmte** Gruppen<br /><br />Von Geräten mit **bestimmte** Vertrauensebenen<br /><br />Mit **bestimmte** Ansprüche in der Anforderung|  
  
Wenn ein Administrator mehrere Bedingungen auswählt, werden sie von **und** Beziehung. Aktionen schließen sich gegenseitig aus, und für eine Richtlinienregel können Sie nur eine Aktion auswählen. Wenn ein Administrator mehrere Ausnahmen auswählt, werden sie von einem **oder** Beziehung. Ein paar Beispiele für Richtlinien sind im folgenden dargestellt:  
  
|**Richtlinie**|**Die Regeln**|
| --- | --- |  
|Extranet-Zugriff erfordert MFA<br /><br />Alle Benutzer sind zulässig.|**Regel #1**<br /><br />von **extranet**<br /><br />und mit der MFA<br /><br />Zulassen<br /><br />**Regel Nr. 2**<br /><br />von **Intranet**<br /><br />Zulassen|  
|Externer Zugriff sind nicht zulässig, außer den nicht-FTE<br /><br />Intranetzugriff für FTE auf Gerät mit dem Arbeitsplatz beigetreten sind zulässig.|**Regel #1**<br /><br />von **extranet**<br /><br />daraus **nicht: FTE** Gruppe<br /><br />Zulassen<br /><br />**Regel #2**<br /><br />von **Intranet**<br /><br />daraus **Arbeitsplatz** Gerät<br /><br />daraus **FTE** Gruppe<br /><br />Zulassen|  
|Extranet-Zugriff ist MFA mit Ausnahme von "Dienstadministrator" erforderlich.<br /><br />Alle Benutzer zugreifen dürfen|**Regel #1**<br /><br />von **extranet**<br /><br />und mit der MFA<br /><br />Zulassen<br /><br />Mit Ausnahme von **Gruppe "Administratoren"**<br /><br />**Regel #2**<br /><br />Immer<br /><br />Zulassen|  
|nicht arbeiten für ein direktes eingebundenes Gerät den Zugriff auf über extranet erfordert MFA<br /><br />AD-Fabrics für Intranet- und extranet-Zugriff zulassen|**Regel #1**<br /><br />von **Intranet**<br /><br />Daraus **AD-Fabrics** Gruppe<br /><br />Zulassen<br /><br />**Regel #2**<br /><br />von **extranet**<br /><br />daraus **nicht mit dem Arbeitsplatz beigetreten** Gerät<br /><br />Daraus **AD-Fabrics** Gruppe<br /><br />und mit der MFA<br /><br />Zulassen<br /><br />**Regel #3**<br /><br />von **extranet**<br /><br />daraus **Arbeitsplatz** Gerät<br /><br />Daraus **AD-Fabrics** Gruppe<br /><br />Zulassen|  
  
## <a name="parameterized-policy-template-vs-non-parameterized-policy-template"></a>Parametrisierte Richtlinie Vorlage Vs nicht parametrisierten Richtlinienvorlage  
Access Control-Richtlinien werden können  
  
Eine parametrisierte Richtlinienvorlage ist eine Richtlinienvorlage aus, die über Parameter verfügt. Ein Administrator muss für die Eingabe, dass der Wert für diese Parameter beim Zuweisen von dieser Vorlage zu RPs.An Administrator Änderungen an parametrisierte Richtlinienvorlage vornehmen kann nicht, nachdem es erstellt wurde.  Ein Beispiel für eine parametrisierte Richtlinie ist die integrierte Richtlinie, eine bestimmte Gruppe zulassen.  Wenn diese Richtlinie auf eine RP angewendet wird, muss dieser Parameter angegeben werden.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP5.PNG)  
  
Eine Vorlage für nicht parametrisierte ist eine Richtlinienvorlage aus, die nicht über Parameter verfügt. Ein Administrator kann diese Vorlage in RPs zuweisen, ohne irgendwelche Eingaben erforderlich und kann Änderungen an einer Vorlage für nicht parametrisierte vornehmen, nachdem es erstellt wurde.  Ein Beispiel hierfür ist die integrierte Richtlinie, alle zulassen und MFA anfordern.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP4.PNG)  
  
## <a name="how-to-create-a-non-parameterized-access-control-policy"></a>Vorgehensweise: Erstellen Sie eine nicht parametrisierte Access-Control-Richtlinie  
Zum Erstellen von einer nicht parametrisierten Zugriffs Control-Richtlinie gehen Sie folgendermaßen vor  
  
#### <a name="to-create-a-non-parameterized-access-control-policy"></a>Um eine nicht parametrisierte Access-Control-Richtlinie zu erstellen.  
  
1.  Wählen Sie Access Control-Richtlinien, und klicken Sie auf der rechten Seite auf Access Control-Richtlinie hinzufügen, von AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Benutzer mit authentifizierten Geräten zulassen.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt ist**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, und setzen Sie ein Häkchen im Feld neben **von Geräten mit bestimmten Vertrauensebene**  
  
5.  Wählen Sie im unteren Bereich das unterstrichene **bestimmte**  
  
6.  Wählen Sie im Fenster oben, Pops **authentifiziert** aus der Dropdownliste aus.  Klicken Sie auf **OK**.  
  
    ![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP6.PNG)  
  
7.  Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
    ![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP7.PNG)  
  
## <a name="how-to-create-a-parameterized-access-control-policy"></a>Vorgehensweise: erstellen eine parametrisierten Access-Control-Richtlinie  
Erstellen Sie eine parametrisierte Zugriffssteuerung Richtlinie gehen Sie folgendermaßen vor  
  
#### <a name="to-create-a-parameterized-access-control-policy"></a>Um eine parametrisierte Access-Control-Richtlinie zu erstellen.  
  
1.  Wählen Sie Access Control-Richtlinien, und klicken Sie auf der rechten Seite auf Access Control-Richtlinie hinzufügen, von AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Ermöglichen Sie Benutzern mit einem bestimmten Anspruch.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt ist**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, und setzen Sie ein Häkchen im Feld neben **mit bestimmten Ansprüchen in der Anforderung**  
  
5.  Wählen Sie im unteren Bereich das unterstrichene **bestimmte**  
  
6.  Wählen Sie im Fenster oben, Pops **-Parameter angegeben, wenn die Access-Control-Richtlinie zugewiesen wird**.  Klicken Sie auf **OK**.  
  
    ![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP8.PNG)  
  
7.  Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
    ![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP9.PNG)  
  
## <a name="how-to-create-a-custom-access-control-policy-with-an-exception"></a>Vorgehensweise: erstellen eine benutzerdefinierten Access-Control-Richtlinie mit einer Ausnahme  
Klicken Sie zum Erstellen eines Steuerelements Zugriff Richtlinie mit einer Ausnahme das folgende Verfahren verwenden.  
  
#### <a name="to-create-a-custom-access-control-policy-with-an-exception"></a>Erstellen Sie eine benutzerdefinierte Access-Control-Richtlinie mit einer Ausnahme  
  
1.  Wählen Sie Access Control-Richtlinien, und klicken Sie auf der rechten Seite auf Access Control-Richtlinie hinzufügen, von AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  IPSec-Zulassungs-Benutzer mit Geräten authentifiziert, aber nicht verwaltet.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt ist**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, und setzen Sie ein Häkchen im Feld neben **von Geräten mit bestimmten Vertrauensebene**  
  
5.  Wählen Sie im unteren Bereich das unterstrichene **bestimmte**  
  
6.  Wählen Sie im Fenster oben, Pops **authentifiziert** aus der Dropdownliste aus.  Klicken Sie auf **OK**.  
  
7.  Unter außer, setzen Sie ein Häkchen im Feld neben **von Geräten mit bestimmten Vertrauensebene**  
  
8.  Klicken Sie unten unter außer, wählen Sie das unterstrichene **bestimmte**  
  
9. Wählen Sie im Fenster oben, Pops **verwaltet** aus der Dropdownliste aus.  Klicken Sie auf **OK**.  
  
10. Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
    ![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP10.PNG)  
  
## <a name="how-to-create-a-custom-access-control-policy-with-multiple-permit-conditions"></a>Vorgehensweise: erstellen eine benutzerdefinierten Access-Control-Richtlinie mit mehreren IPSec-Zulassungs-Bedingungen  
Verwenden zum Erstellen einer Access-Control-Richtlinie mit mehreren zulassen Bedingungen wie folgt vor  
  
#### <a name="to-create-a-parameterized-access-control-policy"></a>Um eine parametrisierte Access-Control-Richtlinie zu erstellen.  
  
1.  Wählen Sie Access Control-Richtlinien, und klicken Sie auf der rechten Seite auf Access Control-Richtlinie hinzufügen, von AD FS-Verwaltung auf der linken Seite.  
  
2.  Geben Sie einen Namen und eine Beschreibung ein.  Zum Beispiel:  Ermöglichen Sie Benutzern mit der ein bestimmter Anspruch und aus einer bestimmten Gruppe.  
  
3.  Klicken Sie unter **Zugriff zulassen, wenn eine der folgenden Regeln erfüllt ist**, klicken Sie auf **hinzufügen**.  
  
4.  Unter zulassen, und setzen Sie ein Häkchen im Feld neben **aus einer bestimmten Gruppe** und **mit bestimmten Ansprüchen in der Anforderung**  
  
5.  Wählen Sie im unteren Bereich das unterstrichene **bestimmte** für die erste Bedingung, neben Gruppen  
  
6.  Wählen Sie im Fenster oben, Pops **-Parameter angegeben, wenn die Richtlinie zugewiesen ist**.  Klicken Sie auf **OK**.  
  
7.  Wählen Sie im unteren Bereich das unterstrichene **bestimmte** für die zweite Bedingung an, neben Ansprüchen  
  
8.  Wählen Sie im Fenster oben, Pops **-Parameter angegeben, wenn die Access-Control-Richtlinie zugewiesen wird**.  Klicken Sie auf **OK**.  
  
9. Klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP12.PNG)  
  
## <a name="how-to-assign-an-access-control-policy-to-a-new-application"></a>Wie Sie eine neue Anwendung eine Access-Control-Richtlinie zuweisen  
Zuweisen einer Access-Control-Richtlinie in eine neue Anwendung ist sehr einfach aufgebaut und hat nun in den Assistenten zum Hinzufügen von einer RP integriert wurde.  Mit dem Assistenten für Vertrauensstellungen der Relying Party können Sie die Access-Control-Richtlinie auswählen, die Sie zuweisen möchten.  Dies ist eine Anforderung, wenn neue Anspruchsanbieter-Vertrauensstellung zu erstellen.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP13.PNG)  
  
## <a name="how-to-assign-an-access-control-policy-to-an-existing-application"></a>Zuweisen eine Access-Control-Richtlinie zu einer vorhandenen Anwendung  
Zuweisen einer Access-Control-Richtlinie zu einer vorhandenen Anwendung wählen Sie einfach die Anwendung von Vertrauensstellungen für vertrauende Seiten und mit der rechten Maustaste auf **Access-Control-Richtlinie bearbeiten**.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP14.PNG)  
  
Von hier aus können Sie wählen Sie die Access-Control-Richtlinie und wenden es an die Anwendung.  
  
![Access Control-Richtlinien](media/Access-Control-Policies-in-AD-FS/ADFSACP15.PNG)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 

