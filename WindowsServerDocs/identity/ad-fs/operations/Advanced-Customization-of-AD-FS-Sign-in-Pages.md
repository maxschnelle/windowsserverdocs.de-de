---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: Erweiterte Anpassung des AD FS-Anmeldeseiten
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/13/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ea01d0ff2a38c4fef2f68091608d777d8412e91b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Erweiterte Anpassung des AD FS-Anmeldeseiten

>Gilt für: Windows Server 2016, Windows Server2012 R2
  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Erweiterte Anpassung des AD FS-Standardparameter-in Pages  
AD FS unter Windows Server 2012 R2 bietet integrierten Unterstützung für die Anpassung der Standardparameter in Verbindung. Für die meisten Szenarien sind die integrierten Windows PowerShell-Cmdlets erforderlich ist.  Es wird empfohlen, dass Sie die integrierten Windows PowerShell-Befehle verwenden, um Standardelemente für AD FS Standardparameter Anmeldeoberfläche möglichst anzupassen.  Finden Sie unter [AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md) Weitere Informationen.  
  
In einigen Fällen können AD FS-Administratoren zusätzliche Standardparameter in Funktionen bereitstellen möchten, die nicht über die vorhandene PowerShell-Befehle möglich sind, die ausführliche-Box mit AD FS enthalten sind. In bestimmten Fällen ist es möglich \ (innerhalb der bereitgestellten Richtlinien Below\) für Administratoren, die Standardparameter in weiter anpassen, indem zusätzliche Logik, um hinzufügen **onload.js** , die von AD FS bereitgestellt wird und auf allen Seiten der AD FS ausgeführt wird.  
  
## <a name="things-to-know-before-you-start"></a>Wichtige Informationen, bevor Sie beginnen  
  
-   Alle Änderungen, die wirkt sich auf die Umleitung Flüsse oder ändert Protokollparameter, denen mit AD FS funktioniert wird nicht unterstützt.
  
-   Die ursprüngliche onload.js, das Element, das das standardwebdesign geringeren enthält Code zum Rendern von Seiten für unterschiedliche Formfaktoren. Es wird empfohlen, nicht, ändern Sie den ursprünglichen onload.js Inhalt jedoch fügen Sie Ihren Code nur an den vorhandenen onload.js, der benutzerdefinierten Logik behandelt.  
  
-   AD FS wird mit einer integrierten Design die standardmäßige aufgerufen wird. Die onload.js für das standardwebdesign kann nicht geändert werden. Um onload.js zu aktualisieren, müssen Sie zum Erstellen und verwenden ein benutzerdefiniertes Webdesign für AD FS Standardparameter in Seiten.  Finden Sie unter [AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md) Informationen zum Erstellen einer benutzerdefinierten Webdesigns.  
  
-   Die gleichen onload.js wird auf alle AD FS-Seiten \(ex. ausgeführt. formularerstellungsfunktionen-basierte Anmeldeseite, Seite zur startbereichsermittlung und usw.. \). Sie müssen Sie sicherstellen, dass der Code in Ihr Skript nur ausgeführt wird, wie sie ist und nicht unerwartet ausgeführt.  
  
-   Wenn Sie jedes HTML-Element zu verweisen, stellen Sie sicher, dass Sie immer das Vorhandensein des Elements vor auf das Element überprüfen. Dies bietet Stabilität und stellt sicher, dass die benutzerdefinierte Logik auf Seiten, die dieses Element nicht enthalten, nicht ausgeführt werden würde. Sie können den HTML-Quellcode einfach auf den AD FS Standardparameter in Seiten an die vorhandenen Elemente anzeigen.  
  
-   Es wird dringend empfohlen, um Ihre Anpassungen in einer anderen Umgebung überprüfen und Testen sie vor einem umfassenden Rollout, auf die Produktion AD FS-Server. Dies reduziert die Wahrscheinlichkeit, dass Endbenutzer diese Anpassungen vor der Überprüfung verfügbar gemacht werden.  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Anpassen der AD FS-Standardparameter können mithilfe von onload.js  
Verwenden Sie die folgenden Schritte aus, wenn die onload.js für den AD FS-Dienst anpassen.  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>Anpassen von onload.js für den AD FS-Dienst  
  
1.  Um eine benutzerdefinierte Logik onload.js hinzuzufügen, müssen Sie zunächst ein benutzerdefiniertes Webdesign erstellen. Das Design, das ausgeliefert Out-Of\-The\-Feld ist standardmäßig aufgerufen. Sie können das Standarddesign exportieren und verwenden Sie es, damit Sie schnell beginnen können. Das folgende Cmdlet erstellt ein benutzerdefiniertes Webdesign, das das standardwebdesign dupliziert:  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  Anschließend können Sie exportieren die benutzerdefinierte oder Standard-Design onload.js Datei abgerufen. Verwenden Sie zum Exportieren eines Webdesigns das folgende Cmdlet aus:  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    Finden Sie onload.js unterhalb des Skript-Ordners in das Verzeichnis, dass Sie im obigen Cmdlet Export angeben, und fügen eine benutzerdefinierte Logik für das Skript \ (Siehe Anwendungsfälle in der Beispiel-Abschnitt Below\).  
  
3.  Nehmen Sie die erforderliche Änderung onload.js basierend auf Ihren Bedürfnissen anpassen.  
  
4.  Aktualisieren Sie das Design, mit der geänderten onload.js. Verwenden Sie das folgende Cmdlet, um die benutzerdefinierten Webdesigns für das Update onload.js zuweisen:  
  
    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}  
  
    ```  
  
5.  Verwenden Sie zum Anwenden des benutzerdefinierten Webdesigns auf AD FS das folgende Cmdlet aus:  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>Beispiele für die weitere Anpassung  
Im folgenden sind die Beispiele für benutzerdefinierte Code onload.js für andere Fine\-Antwort Zwecke hinzugefügt. Wenn Sie den benutzerdefinierten Code hinzufügen, finden Sie immer fügen Sie den benutzerdefinierten Code an den unteren Rand der onload.js.  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>Beispiel 1: Ändern Sie Zeichenfolge "Melden Sie sich mit Organisations-Konto"  
Die standardmäßige AD FS-basierte formularerstellungsfunktionen Anmeldeseite hat den Titel "Melden Sie sich mit Ihrem Organisations-Konto" über Felder für Benutzereingaben.  
  
Wenn Sie diese Zeichenfolge durch eigene ersetzen möchten, können Sie den folgenden Code onload.js hinzufügen.  
  
```  
// Sample code to change “Sign in with organizational account” string.  
  
// Check whether the loginMessage element is present on this page.  
var loginMessage = document.getElementById('loginMessage');  
if (loginMessage)  
{  
       // loginMessage element is present, modify its properties.  
       loginMessage.innerHTML = 'Your company description text';  
}  
  
```  
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>Beispiel 2: akzeptieren Sie SAM\-Kontonamen als Format melden Sie sich auf eine AD FS-basierte formularerstellungsfunktionen Anmeldeseite  
Das Standardformat AD FS Anmeldeseite formularerstellungsfunktionen-basierte unterstützt Anmeldung der Benutzerprinzipalnamen \(UPNs\) \(for example, ** johndoe@contoso.com **\) oder Domäne qualifizierten Sam\-Kontonamen \ (**Contoso\\johndoe** oder **contoso.com\\johndoe**\). Fall, dass alle Benutzer aus der gleichen Domäne stammen, und sie nur über Sam\-Kontonamen wissen, sollten Sie diese Sam\-Namen nur verwenden, unterstützen das Szenario, in dem der Benutzer sich anmelden können. Sie können den folgenden Code hinzufügen, um onload.js dieses Szenario unterstützt, ersetzen die Domäne "contoso.com" im Beispiel unten nur mit der Domäne, die Sie verwenden möchten.  
  
```  
if (typeof Login != 'undefined'){  
    Login.submitLoginRequest = function () {   
    var u = new InputUtil();  
    var e = new LoginErrors();  
    var userName = document.getElementById(Login.userNameInput);  
    var password = document.getElementById(Login.passwordInput);  
    if (userName.value && !userName.value.match('[@\\\\]'))   
    {  
        var userNameValue = 'contoso.com\\' + userName.value;  
        document.forms['loginForm'].UserName.value = userNameValue;  
    }  
  
    if (!userName.value) {  
       u.setError(userName, e.userNameFormatError);  
       return false;  
    }  
  
    if (!password.value)   
    {  
        u.setError(password, e.passwordEmpty);  
        return false;  
    }  
    document.forms['loginForm'].submit();  
    return false;  
};  
}  
  
```  
  
## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Anpassung durch den Benutzer](AD-FS-user-sign-in-customization.md)  
  

