---
ms.assetid: 77aa61bf-9c04-4889-a5d2-6f45bc1b8bd2
title: Wann sollten Sie eine Transformationsanspruchsregel verwenden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5ed8ee500582e0e687a2b52e83d99fc3cb8f147f
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188340"
---
# <a name="when-to-use-a-transform-claim-rule"></a>Wann sollten Sie eine Transformationsanspruchsregel verwenden?
Sie können diese Regel in Active Directory-Verbunddienste \(AD FS\) Wenn müssen Sie einen eingehenden Anspruchstyp einem ausgehenden Anspruchstyp zugeordnet, und klicken Sie dann eine Aktion anwenden, die bestimmen, welche Ausgabe erfolgen soll, basierend auf den Werten, die stammt aus dem eingehenden Anspruch. Wenn Sie diese Regel verwenden, leiten Sie Ansprüche weiter bzw. transformieren Sie Ansprüche, die der folgenden Regellogik entsprechen. Dies geschieht auf Basis der Optionen, die Sie in der Regel konfigurieren, wie in der folgenden Tabelle beschrieben.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle eingehenden Ansprüche weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *beliebigen Wert* entspricht, leiten Sie den Anspruch mit einem ausgehenden Anspruchstyp weiter, der dem *angegebenen Anspruchstyp* entspricht.|  
|Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert dem *angegebenen Anspruchswert* entspricht, transformieren Sie den Anspruch mit einem neuen ausgehenden Anspruchswert, der dem *angegebenen Anspruchswert* entspricht, und mit einem ausgehenden Anspruchstyp, der dem *angegebenen Anspruchstyp* entspricht.|  
|Ersetzen eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *beliebigen Suffixwert* entspricht, transformieren Sie den Anspruch mit einem neuen ausgehenden Anspruchswert, der dem *angegebenen Suffixwert* entspricht, und mit einem ausgehenden Anspruchstyp, der dem *angegebenen Anspruchstyp* entspricht.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Details zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \(If x, dann y\) und Grundlage, auf der Bedingungsparameter einen ausgehenden Anspruch erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS-Verwaltungs-Snap-\-in Anspruch Regeln können nur mit anspruchsregelvorlagen erstellt werden  
  
-   Anspruch Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \(wie Active Directory oder einem anderen Verbunddienst\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie die Regel von Anspruchssätze verarbeitet werden, finden Sie unter [die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="pass-through-all-claim-values"></a>Alle Anspruchswerte weiterleiten  
Wenn Sie diese Aktion verwenden, werden alle eingehenden Anspruchswerte, die auf einen angegebenen eingehenden Anspruchstyp abgestimmt sind, einem angegebenen ausgehenden Anspruchstyp zugeordnet, bevor sie als ausgehende Ansprüche in Tokens gesendet werden, die durch den Verbunddienst signiert sind.  
  
Wenn eine Regel z. B. mit der Optionslogik **Alle Anspruchswerte weiterleiten** festgelegt und der eingehende Anspruchstyp "Gruppe" und der ausgehende Anspruchstyp "Rolle" angegeben ist, werden alle eingehenden Anspruchswerte, die vom Aussteller einfließen, einzeln mit dem Anspruchstyp "Rolle" in neue ausgehende Ansprüche kopiert.  
  
## <a name="transforming-a-claim"></a>Transformieren eines Anspruchs  
In AD FS den Begriff *Anspruchstransformation* Mittel zum Ersetzen eines eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert. Die Regel zum Transformieren eines eingehenden Anspruchs macht diese Funktion möglich. Im Rahmen der Eigenschaften dieser Regel können Sie Bedingungen zum Transformieren eines eingehenden Werts mit einem anderen ausgehenden Anspruchswert auf der Basis des angegebenen eingehenden Anspruchstyps festlegen.  
  
Wenn beispielsweise, wie in der folgenden Abbildung gezeigt, eine Regel mit der Bedingung festgelegt wird, einen eingehenden Wert durch einen anderen ausgehenden Anspruchswert zu ersetzen, werden alle eingehenden Anspruchstypen "Group" neuen ausgehenden Anspruchstypen "Role" zugeordnet. In diesem Fall wird der eingehenden Anspruchswert "Purchaser" durch den neuen ausgehenden Anspruchswert "Admin" ersetzt.  
  
![Beim verwenden eine Transformation](media/adfs2_transform.gif)  
  
Sie können auch mit dieser Regel verwenden, um eine Bedingung anwenden, die alle eingehenden Ansprüche mit einem angegebenen e ersetzt\-e-Mail-Suffixwert durch einen neuen Wert. Sie könnten z. B. in dieser Regel eine Bedingung zum Ändern aller Anspruchswerte mit dem Suffix "sales.corp.fabrikam.com" in "fabrikam.com" festlegen.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel in einer Anspruchsanbietervertrauensstellung  
Bei Verwendung einer Anspruchsanbietervertrauensstellung kann diese Regel zum Transformieren eingehender Ansprüche vom Anspruchsanbieter in vertrauenswürdige Äquivalente konfiguriert werden. Anspruchstypen oder Anspruchswerte können in Ihrer Organisation eine andere Bedeutung als in den Organisationen der Anspruchsanbieter haben. Mit dieser Regel können Sie die Anspruchstypen und -Werte normalisieren, die vom Anspruchsanbieter stammen, sodass ihre ausgehenden Anspruchsäquivalente von der vertrauenden Seite verstanden werden.  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>Konfigurieren diese Regel in einer Vertrauensstellung der vertrauenden Seite  
Wenn Sie eine Vertrauensstellung der vertrauenden Seite verwenden, kann diese Regel zum Transformieren von Ansprüchen für die bestimmte vertrauende Seite konfiguriert werden. Anspruchstypen oder -werte können für eine bestimmte vertrauende Seite eine andere Bedeutung haben, und diese Regel ermöglicht Ihnen, die ausgehenden Anspruchstypen und -werte für eine einzelne vertrauende Seite zu ändern.  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel entweder die anspruchsregelsprache oder der **Transformieren eines eingehenden Anspruchs** Regelvorlage im AD FS-Verwaltungs-Snap-\-in. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Transformieren eines bestimmten eingehenden Anspruchstyps in einen bestimmten ausgehenden Anspruchstyp  
  
-   Alle Anspruchswerte weiterleiten  
  
-   Ersetzen Sie einen eingehenden Anspruchswert durch einen anderen ausgehenden Anspruchswert  
  
-   Ersetzen Sie eingehende e\-e-Mail-suffixansprüche mit einer neuen e\-e-Mail-Suffix  
  
Weitere Anweisungen zum Erstellen dieser Vorlage finden Sie [erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs](https://technet.microsoft.com/library/dd807068.aspx) in AD FS-Bereitstellungshandbuch.  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Wenn der ausgehende Anspruch aus dem Inhalt mehrerer eingehender Ansprüche erstellt werden muss, müssen Sie stattdessen eine benutzerdefinierte Regel verwenden. Wenn der Anspruchswert des ausgehenden Anspruchs auf dem Wert des eingehenden Anspruchs basieren muss – jedoch mit zusätzlichem Inhalt – müssen Sie auch in diesem Kontext eine benutzerdefinierte Regel verwenden. Weitere Informationen finden Sie unter [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md).  
  
### <a name="examples-of-how-to-construct-a-transform-rule-syntax"></a>Beispiele zum Erstellen einer Transformationsregelsyntax  
Bei Verwendung der Anspruchsregel-Sprachsyntax zum Transformieren von Ansprüchen können Sie für eine Eigenschaft des transformierten Anspruchs einen neuen literalen Wert festlegen. Beispielsweise ändert die folgende Regel unter Beibehaltung des Anspruchstyps den Wert der Rollenansprüche von "Administrators" in "Root":  
  
```  
c:[type == “https://schemas.microsoft.com/ws/2008/06/identity/claims/role”, value == “Administrators”]  => issue(type = c.type, value = “root”);  
```  
  
Reguläre Ausdrücke können auch für Anspruchstransformationen verwendet werden. Z. B. die folgende Regel wird die Domäne fest in Windows-benutzernamenansprüchen in Domäne\\Format an FABRIKAM Benutzer:  
  
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
  
Weitere Informationen zur Verwendung die anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  

