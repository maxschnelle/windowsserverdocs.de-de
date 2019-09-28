---
ms.assetid: 77aa61bf-9c04-4889-a5d2-6f45bc1b8bd2
title: Wann sollten Sie eine Transformationsanspruchsregel verwenden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b7cdf68783db1b6b775209e4e42dc6b6ccf0e1b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385420"
---
# <a name="when-to-use-a-transform-claim-rule"></a>Wann sollten Sie eine Transformationsanspruchsregel verwenden?
Sie können diese Regel in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 verwenden, wenn Sie einem ausgehenden Anspruchstyp einen eingehenden Anspruchstyp zuordnen und dann eine Aktion anwenden, die bestimmt, welche Ausgabe basierend auf den Werten, die aus dem eingehender Anspruch. Wenn Sie diese Regel verwenden, leiten Sie Ansprüche weiter bzw. transformieren Sie Ansprüche, die der folgenden Regellogik entsprechen. Dies geschieht auf Basis der Optionen, die Sie in der Regel konfigurieren, wie in der folgenden Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle eingehenden Ansprüche weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *beliebigen Wert* entspricht, leiten Sie den Anspruch mit einem ausgehenden Anspruchstyp weiter, der dem *angegebenen Anspruchstyp* entspricht.|  
|Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert dem *angegebenen Anspruchswert* entspricht, transformieren Sie den Anspruch mit einem neuen ausgehenden Anspruchswert, der dem *angegebenen Anspruchswert* entspricht, und mit einem ausgehenden Anspruchstyp, der dem *angegebenen Anspruchstyp* entspricht.|  
|Ersetzen eingehender e @ no__t-0mail-suffixansprüche durch ein neues e @ no__t-1mail-Suffix|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *beliebigen Suffixwert* entspricht, transformieren Sie den Anspruch mit einem neuen ausgehenden Anspruchswert, der dem *angegebenen Suffixwert* entspricht, und mit einem ausgehenden Anspruchstyp, der dem *angegebenen Anspruchstyp* entspricht.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Details zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchs Regel stellt eine Instanz der Geschäftslogik dar, die einen eingehenden Anspruch annimmt, eine Bedingung darauf \(anwendet, wenn x\) und y ist, und einen ausgehenden Anspruch basierend auf den Bedingungs Parametern erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im Snap\--in "AD FS-Verwaltung" können Anspruchs Regeln nur mithilfe von Anspruchs Regel Vorlagen erstellt werden.  
  
-   Anspruchs Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchs \(Anbieter (z. b.\) Active Directory oder einem anderen Verbunddienst oder von der Ausgabe der Akzeptanz Transformationsregeln für eine Anspruchs Anbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchs Regeln und Anspruchs Regelsätzen finden Sie [unter Rolle der Anspruchs Regeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie [unter The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen zur Verarbeitung von Anspruchs Regelsätzen finden Sie [unter der Rolle der Anspruchs Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="pass-through-all-claim-values"></a>Alle Anspruchswerte weiterleiten  
Wenn Sie diese Aktion verwenden, werden alle eingehenden Anspruchswerte, die auf einen angegebenen eingehenden Anspruchstyp abgestimmt sind, einem angegebenen ausgehenden Anspruchstyp zugeordnet, bevor sie als ausgehende Ansprüche in Tokens gesendet werden, die durch den Verbunddienst signiert sind.  
  
Wenn eine Regel z. B. mit der Optionslogik **Alle Anspruchswerte weiterleiten** festgelegt und der eingehende Anspruchstyp "Gruppe" und der ausgehende Anspruchstyp "Rolle" angegeben ist, werden alle eingehenden Anspruchswerte, die vom Aussteller einfließen, einzeln mit dem Anspruchstyp "Rolle" in neue ausgehende Ansprüche kopiert.  
  
## <a name="transforming-a-claim"></a>Transformieren eines Anspruchs  
In AD FS bedeutet der Begriff " *Anspruchs Transformation* ", dass ein eingehender Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzt wird. Die Regel zum Transformieren eines eingehenden Anspruchs macht diese Funktion möglich. Im Rahmen der Eigenschaften dieser Regel können Sie Bedingungen zum Transformieren eines eingehenden Werts mit einem anderen ausgehenden Anspruchswert auf der Basis des angegebenen eingehenden Anspruchstyps festlegen.  
  
Wenn beispielsweise, wie in der folgenden Abbildung gezeigt, eine Regel mit der Bedingung festgelegt wird, einen eingehenden Wert durch einen anderen ausgehenden Anspruchswert zu ersetzen, werden alle eingehenden Anspruchstypen "Group" neuen ausgehenden Anspruchstypen "Role" zugeordnet. In diesem Fall wird der eingehenden Anspruchswert "Purchaser" durch den neuen ausgehenden Anspruchswert "Admin" ersetzt.  
  
![Verwendung einer Transformation](media/adfs2_transform.gif)  
  
Sie können diese Regel auch verwenden, um eine Bedingung anzuwenden, die alle eingehenden Ansprüche durch einen angegebenen e @ no__t-e-Mail-suffixwert durch einen neuen Wert ersetzt. Sie könnten z. B. in dieser Regel eine Bedingung zum Ändern aller Anspruchswerte mit dem Suffix "sales.corp.fabrikam.com" in "fabrikam.com" festlegen.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel in einer Anspruchsanbietervertrauensstellung  
Bei Verwendung einer Anspruchsanbietervertrauensstellung kann diese Regel zum Transformieren eingehender Ansprüche vom Anspruchsanbieter in vertrauenswürdige Äquivalente konfiguriert werden. Anspruchstypen oder Anspruchswerte können in Ihrer Organisation eine andere Bedeutung als in den Organisationen der Anspruchsanbieter haben. Mit dieser Regel können Sie die Anspruchstypen und -Werte normalisieren, die vom Anspruchsanbieter stammen, sodass ihre ausgehenden Anspruchsäquivalente von der vertrauenden Seite verstanden werden.  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>Konfigurieren diese Regel in einer Vertrauensstellung der vertrauenden Seite  
Wenn Sie eine Vertrauensstellung der vertrauenden Seite verwenden, kann diese Regel zum Transformieren von Ansprüchen für die bestimmte vertrauende Seite konfiguriert werden. Anspruchstypen oder -werte können für eine bestimmte vertrauende Seite eine andere Bedeutung haben, und diese Regel ermöglicht Ihnen, die ausgehenden Anspruchstypen und -werte für eine einzelne vertrauende Seite zu ändern.  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel entweder mithilfe der Anspruchs Regel Sprache oder mithilfe der Regel Vorlage zum **Transformieren eines eingehenden Anspruchs** im AD FS Verwaltungs-Snap @ no__t-1In. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Transformieren eines bestimmten eingehenden Anspruchstyps in einen bestimmten ausgehenden Anspruchstyp  
  
-   Alle Anspruchswerte weiterleiten  
  
-   Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert  
  
-   Ersetzen eingehender e @ no__t-e-Mail-suffixansprüche durch ein neues e @ no__t-1mail-Suffix  
  
Weitere Anweisungen zum Erstellen dieser Vorlage finden Sie unter [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](https://technet.microsoft.com/library/dd807068.aspx) im AD FS Bereitstellungs Handbuch.  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Wenn der ausgehende Anspruch aus dem Inhalt mehrerer eingehender Ansprüche erstellt werden muss, müssen Sie stattdessen eine benutzerdefinierte Regel verwenden. Wenn der Anspruchswert des ausgehenden Anspruchs auf dem Wert des eingehenden Anspruchs basieren muss – jedoch mit zusätzlichem Inhalt – müssen Sie auch in diesem Kontext eine benutzerdefinierte Regel verwenden. Weitere Informationen finden Sie unter [verwenden Sie eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
### <a name="examples-of-how-to-construct-a-transform-rule-syntax"></a>Beispiele zum Erstellen einer Transformationsregelsyntax  
Bei Verwendung der Anspruchsregel-Sprachsyntax zum Transformieren von Ansprüchen können Sie für eine Eigenschaft des transformierten Anspruchs einen neuen literalen Wert festlegen. Beispielsweise ändert die folgende Regel unter Beibehaltung des Anspruchstyps den Wert der Rollenansprüche von "Administrators" in "Root":  
  
```  
c:[type == “https://schemas.microsoft.com/ws/2008/06/identity/claims/role”, value == “Administrators”]  => issue(type = c.type, value = “root”);  
```  
  
Reguläre Ausdrücke können auch für Anspruchstransformationen verwendet werden. Mit der folgenden Regel wird beispielsweise die Domäne in Windows-Benutzernamen Ansprüchen im @ no__t-0User-Format auf Fabrikam festgelegt:  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => issue(type = c.type, value = regexreplace(c.value, "(?<domain>[^\\]+)\\(?<user>.+)", "FABRIKAM\${user}"));  
```  
  
### <a name="best-practices-for-creating-custom-rules"></a>Bewährte Methoden zum Erstellen benutzerdefinierter Regeln  
Anspruchstransformationen können mithilfe grundlegender Filterfunktionen selektiv auf ausgewählte Ansprüche angewendet werden. Jeder der zum Filtern verwendeten Anspruchseigenschaften können Werte zugewiesen werden, jedoch mit folgenden Vorsichtsmaßnahmen:  
  
|Anspruchseigenschaft|Beschreibung|  
|------------------|---------------|  
|Type, Value, ValueType|Diese Eigenschaften werden am häufigsten für Zuweisungen verwendet. Für den resultierenden transformierten Anspruch müssen zumindest Typ und Wert angegeben werden.|  
|Aussteller|Die Anspruchsregelsprache erlaubt zwar, den Aussteller eines Anspruchs festzulegen, jedoch wird dies im Allgemeinen nicht empfohlen. Der Aussteller eines Anspruchs ist im Token nicht serialisiert. Beim Empfang eines Tokens wird die Eigenschaft "Issuer" aller Ansprüche auf den Bezeichner des Verbundservers festgelegt, der das Token signiert hat. Folglich hat das Festlegen des Ausstellers eines Anspruchs in den Regeln keinen Einfluss auf den Inhalt des Tokens, und die Einstellung geht verloren, sobald der Anspruch in einem Token verpackt wird. Das einzige Szenario, in dem das Festlegen des Ausstellers eines Anspruchs sinnvoll ist, liegt vor, wenn er im Anspruchsanbieter-Regelsatz auf einen bestimmten Wert gesetzt ist, und der Regelsatz der vertrauenden Seite mit Regeln erstellt ist, die auf diesen bestimmten Wert verweisen. Wenn die Eigenschaft "Issuer" nicht explizit auf einen Wert in einer Anspruchsregel festgelegt ist, setzt das Anspruchsausstellungsmodul sie auf "LOCAL AUTHORITY".|  
|OriginalIssuer|Genau wie "Issuer" sollte "OriginalIssuer" im Allgemeinen nicht explizit ein Wert zugewiesen werden. Im Gegensatz zu "Issuer" wird die Eigenschaft "OriginalIssuer" im Token serialisiert, aber Tokennutzer gehen davon aus, dass sie, sofern festgelegt, den Bezeichner des Verbundservers enthält, der ursprünglich einen Anspruch ausgestellt hat.|  
|Eigenschaften|Wie im vorherigen Abschnitt beschrieben, wird die Eigenschaftensammlung eines Anspruchs im Token nicht beibehalten, sodass Zuweisungen zu Eigenschaften nur erfolgen sollten, wenn die nachfolgenden lokalen Richtlinien auf die in der Eigenschaft gespeicherten Informationen verweisen.|  
  
Weitere Informationen zum Verwenden der Anspruchs Regel Sprache finden Sie [unter der Rolle der Anspruchs Regel Sprache](The-Role-of-the-Claim-Rule-Language.md).  
  

