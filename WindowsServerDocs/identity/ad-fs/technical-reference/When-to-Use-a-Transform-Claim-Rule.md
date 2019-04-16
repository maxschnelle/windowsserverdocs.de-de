---
ms.assetid: 77aa61bf-9c04-4889-a5d2-6f45bc1b8bd2
title: Wann sollte eine Transformationsanspruchsregel verwenden?
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c7b7ea2c8d9a08a4cbf6c89c2de2482043efe25b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="when-to-use-a-transform-claim-rule"></a>Wann sollte eine Transformationsanspruchsregel verwenden?
Sie können diese Regel in Active Directory Federation Services \(AD FS\) müssen Sie einen eingehenden Anspruchstyp einem ausgehenden Anspruchstyp zugeordnet, und klicken Sie dann eine Aktion anwenden, die bestimmen, welche Ausgabe auf der Grundlage der Werte erfolgen soll, die in den eingehenden Anspruch stammen. Wenn Sie diese Regel verwenden, weitergeleitet bzw. transformieren Ansprüche, die basierend auf eine der Optionen, die Sie in der Regel konfigurieren, wie in der folgenden Tabelle beschrieben der folgenden Regellogik entsprechen.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle eingehenden Ansprüche weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *einen beliebigen Wert*, den Anspruch weiterleiten mit ausgehenden Anspruchs Weiter *angegebenen Anspruchstyp*|  
|Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*, transformieren Sie den Anspruch mit einem neuen ausgehenden Anspruchswert *angegebenen Anspruchswert* und mit einem ausgehenden Anspruchstyp *angegebenen Anspruchstyp*|  
|Eingehende E\ E-Mail-Suffixansprüche ersetzen durch ein neues E\ E-Mail-Suffix|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *eine Suffix-Wert*, transformieren Sie den Anspruch mit einem neuen ausgehenden Anspruchswert *angegebenen Suffixwert* und mit einem ausgehenden Anspruchstyp *angegebenen Anspruchstyp*|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Detail zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \ (wenn x dann Y\) und erstellen Sie einen ausgehenden Anspruch auf Grundlage der Bedingung-Parameter. Die folgende Liste enthält wichtige Tipps, die Sie kennen sollten Anspruchsregeln bevor Sie weiter lesen in diesem Thema:  
  
-   In der AD FS-Verwaltungs-Snap-In können Anspruchsregeln nur erstellt werden mithilfe von anspruchsregelvorlagen  
  
-   Anspruch Regeln Prozess eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \ (z.B. Active Directory oder einem anderen Verbundservern Service\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Durch die Rangfolge der Regeln festlegen, können Sie optimieren oder Filtern Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden.  
  
-   Anspruchsregelvorlagen werden immer müssen Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie anspruchsregelsätzen verarbeitet werden, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="pass-through-all-claim-values"></a>Alle Anspruchswerte weiterleiten  
Wenn Sie diese Aktion verwenden, werden alle eingehenden Anspruchswerte, die auf einen angegebenen eingehenden Anspruchstyp abgestimmt sind auf einem angegebenen ausgehenden Anspruchstyp zugeordnet, bevor sie als ausgehende Ansprüche in Tokens gesendet werden, die durch den Verbunddienst signiert sind.  
  
Wenn beispielsweise eine Regel mit eingerichtet wurde die **Pass-through alle Anspruchswerte** optionslogik und der eingehende Anspruchstyp der Gruppe und der ausgehende Anspruchstyp "Rolle" angegeben ist, werden alle eingehenden Anspruchswerte, die in aus der Aussteller einzeln in neue ausgehende Ansprüche mit Anspruchstyp "Rolle" kopiert.  
  
## <a name="transforming-a-claim"></a>Transformieren eines Anspruchs  
In AD FS, der Begriff *Ansprüche Transformation* Mittel zum Ersetzen eines eingehenden anspruchswerts durch einen anderen ausgehenden Anspruchswert. Es ist die Transformation einer eingehenden Anspruchs-Regel, die diese Funktion ermöglicht. In den Eigenschaften der Regel können Sie Bedingungen zum Transformieren eines eingehenden Werts mit einem anderen ausgehenden Anspruchswert basierend auf den angegebenen Typ des eingehenden Anspruchs festlegen.  
  
Wie in der folgenden Abbildungangezeigt, wenn eine Regel mit der Bedingung festgelegt ist, um einen eingehenden Wert durch einen anderen ausgehenden Anspruchswert zu ersetzen, werden alle eingehenden Anspruchstypen Gruppe zum neuen ausgehenden Anspruchstypen "Role" zugeordnet. In diesem Fall wird der Wert des eingehenden Anspruchs Käufer mit der neuen ausgehenden Anspruchswert Admin ersetzt  
  
![Bei Verwendung eine Transformation](media/adfs2_transform.gif)  
  
Mit dieser Regel können auch eine Bedingung anwenden, die alle eingehenden Ansprüche mit einem angegebenen E\ E-Mail-Suffixwert durch einen neuen Wert ersetzt. Sie könnten z.B. eine Bedingung in dieser Regel alle Anspruchswerte mit dem Suffix sales.corp.fabrikam.com in fabrikam.com ändern festlegen.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel auf eine Anspruchsanbieter-Vertrauensstellung  
Wenn Sie eine Anspruchsanbieter-Vertrauensstellung verwenden, kann diese Regel zum Transformieren eingehender Ansprüche vom Anspruchsanbieter in vertrauenswürdige äquivalente konfiguriert werden. Anspruchstypen Sie oder Werte eine andere Bedeutung in Ihrer Organisation als in den Organisationen der Anspruchsanbieter haben können. Mit dieser Regel können Sie um die Anspruchstypen und Werte, die vom Anspruchsanbieter stammen, sodass ihre ausgehenden anspruchsäquivalente von der vertrauenden Seite verstanden werden zu normalisieren.  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>Konfigurieren diese Regel für eine Vertrauensstellung der vertrauenden Seite  
Wenn Sie eine Vertrauensstellung der vertrauenden Seite verwenden, kann diese Regel zum Transformieren von Ansprüchen für die bestimmte vertrauende Seite konfiguriert werden. Anspruchstypen Sie oder Werte möglicherweise eine andere Bedeutung für eine bestimmte vertrauende Seite, und diese Regel ermöglicht Ihnen die ausgehenden Anspruchstypen und -Werte für eine einzelne vertrauende Seite zu ändern.  
  
## <a name="how-to-create-this-rule"></a>Vorgehensweise beim Erstellen dieser Regel  
Sie erstellen diese Regel entweder die anspruchsregelsprache oder der **Transformieren eines eingehenden Anspruchs** Regelvorlage in AD FS-Verwaltungs-Snap-In. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Transformieren eines bestimmten eingehenden anspruchstyps zu einem angegebenen ausgehenden Anspruchstyp  
  
-   Alle Anspruchswerte weiterleiten  
  
-   Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert  
  
-   Ersetzen Sie eingehende E\ E-Mail-Suffixansprüche durch ein neues E\ E-Mail-Suffix  
  
Weitere Informationen zum Erstellen dieser Vorlage finden Sie unter [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](https://technet.microsoft.com/library/dd807068.aspx) in AD FS-Bereitstellungshandbuch.  
  
## <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
Wenn der ausgehende Anspruch aus dem Inhalt von mehr als einem eingehenden Anspruch erstellt werden muss, müssen Sie stattdessen eine benutzerdefinierte Regel verwenden. Wenn der Anspruchswert des ausgehenden Anspruchs auf dem Wert des eingehenden Anspruchs basieren muss – jedoch mit zusätzlichem Inhalt – müssen Sie auch eine benutzerdefinierte Regel verwenden, in diesem Kontext. Weitere Informationen finden Sie unter [verwenden eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
### <a name="examples-of-how-to-construct-a-transform-rule-syntax"></a>Beispiele zum Erstellen einer transformationsregelsyntax Regel syntax  
Wenn die Syntax der anspruchsregelsprache zum Transformieren von Ansprüchen, können Sie eine Eigenschaft des transformierten Anspruchs einen neuen literalen Wert festlegen. Beispielsweise ändert die folgende Regel den Wert der Rollenansprüche von "Administrators" in "Root" Beibehaltung des anspruchstyps:  
  
```  
c:[type == “https://schemas.microsoft.com/ws/2008/06/identity/claims/role”, value == “Administrators”]  => issue(type = c.type, value = “root”);  
```  
  
Reguläre Ausdrücke können auch für Anspruchstransformationen verwendet werden. Die folgende Regel wird z.B. die Domäne in der Windows-benutzernamenansprüchen im Format "Domäne\\Benutzer" auf FABRIKAM festgelegt:  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => issue(type = c.type, value = regexreplace(c.value, "(?<domain>[^\\]+)\\(?<user>.+)", "FABRIKAM\${user}"));  
```  
  
### <a name="best-practices-for-creating-custom-rules"></a>Bewährte Methoden zum Erstellen benutzerdefinierter Regeln  
Anspruchstransformationen können selektiv auf ausgewählte mithilfe grundlegender Filterfunktionen Ansprüche angewendet werden. Jede zum Filtern verwendeten anspruchseigenschaften kann Werte, die mit folgenden Vorsichtsmaßnahmen zugewiesen werden:  
  
|Anspruchs-Eigenschaft|Beschreibung|  
|------------------|---------------|  
|Typ, Wert, ValueType|Diese Eigenschaften werden am häufigsten für Zuweisungen verwendet werden. Für den resultierenden transformierten Anspruch müssen zumindest Typ und Wert angegeben werden.|  
|Aussteller|Während die anspruchsregelsprache ermöglicht das Festlegen des Ausstellers eines Anspruchs, wird dies im Allgemeinen nicht empfohlen. Der Aussteller eines Anspruchs im Token nicht serialisiert. Beim Empfang eines Tokens wird die "Issuer"-Eigenschaft aller Ansprüche auf den Bezeichner des Verbundservers festgelegt, die das Token signiert hat. Folglich Festlegen des Ausstellers eines Anspruchs in den Regeln keinen Einfluss auf den Inhalt des Tokens, und die Einstellung verloren, sobald der Anspruch in einem Token verpackt wird. Ist das einzige Szenario, in dem Festlegen des Ausstellers eines Anspruchs sinnvoll ist, es festgelegt ist, auf einen bestimmten Wert in der Anspruchsanbieter-Regelsatz und relying Party Regel Satz mit Regeln erstellt ist, die auf diesen bestimmten Wert verweisen. Wenn die "Issuer"-Eigenschaft nicht explizit auf einen Wert in einer Anspruchsregel festgelegt ist, das anspruchsausstellungsmodul sie auf "LOCAL AUTHORITY" festgelegt.|  
|OriginalIssuer|Ebenso sollte Aussteller, OriginalIssuer in der Regel nicht explizit einen Wert zugewiesen werden. Im Gegensatz zu Aussteller, ist die Eigenschaft OriginalIssuer im Token serialisiert, aber die Erwartung tokennutzer besteht darin, dass wenn festgelegt, den Bezeichner des Verbundservers enthalten, die ursprünglich einen Anspruch ausgestellt hat.|  
|Eigenschaften|Wie im vorherigen Abschnittbeschrieben, wird die Eigenschaftensammlung eines Anspruchs im Token nicht beibehalten, sodass Zuweisungen zu Eigenschaften nur erfolgen sollten, wenn die nachfolgende lokale Richtlinien in der Eigenschaft gespeicherte Informationen verweisen möchten.|  
  
Weitere Informationen zur Verwendung die anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  

