---
ms.assetid: 606df285-259c-4c6b-8583-9aca1d614c43
title: Verwenden einer Anspruchsregel vom Typ "Weiterleiten" oder "Filtern"
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 803d939aeaa640e2a8411da156f74f505a2f89d4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444041"
---
# <a name="when-to-use-a-pass-through-or-filter-claim-rule"></a>Verwenden einer Anspruchsregel vom Typ "Weiterleiten" oder "Filtern"
Sie können diese Regel in Active Directory-Verbunddienste \(AD FS\) Wenn müssen Sie einen eingehenden Anspruchstyp und wenden Sie dann eine Aktion, die bestimmt, welche Ausgabe erfolgen soll basierend auf den Werten aus dem eingehenden Anspruch. Wenn Sie diese Regel verwenden, werden Ansprüche weitergeleitet bzw. gefiltert, die der Regellogik in der folgenden Tabelle entsprechen. Dies geschieht auf Grundlage der Optionen, die Sie in der Regel konfigurieren.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle Anspruchswerte weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *beliebigen Wert* entspricht, den Anspruch weiterleiten|  
|Nur einen bestimmten Anspruchswert weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert* entspricht, den Anspruch weiterleiten|  
|Pass-through-nur Anspruchswerte durchalufen, die einen bestimmten e entsprechen\-e-Mail-Suffix-Wert|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Suffixwert* entspricht, den Anspruch weiterleiten|  
|Nur Anspruchswerte weiterleiten, die mit einem bestimmten Wert anfangen|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert mit einem *angegebenen Anspruchswert* beginnt, den Anspruch weiterleiten|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Details zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \(If x, dann y\) und Grundlage, auf der Bedingungsparameter einen ausgehenden Anspruch erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS-Verwaltungs-Snap-\-in Anspruch Regeln können nur mit anspruchsregelvorlagen erstellt werden  
  
-   Anspruch Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \(wie Active Directory oder einem anderen Verbunddienst\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie die Regel von Anspruchssätze verarbeitet werden, finden Sie unter [die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="pass-through-all-claim-values"></a>Alle Anspruchswerte weiterleiten  
Wenn Sie diese Aktion verwenden, werden alle eingehenden Anspruchswerte für den angegebenen Anspruchstyp als ausgehende Ansprüche weitergeleitet. Wenn der Typ des eingehenden Anspruchs als Anspruchstyp "Rolle" angegeben wird, werden alle eingehenden Anspruchswerte z. B. einzeln in neue ausgehende Ansprüche mit dem ausgehenden Anspruchstyp "Rolle" kopiert.  
  
## <a name="filtering-a-claim"></a>Filtern eines Anspruchs  
In AD FS den Begriff *Ansprüche filtern* Möglichkeit zum Filtern bzw. einschränken eingehender Anspruchswerte, damit nur bestimmte Werte weitergeleitet bzw. als ausgehende Ansprüche gesendet werden. Diese Funktion wird durch die Regelvorlage **Eingehenden Anspruch weiterleiten oder filtern** ermöglicht. In den Eigenschaften der Regel können Sie Bedingungen festlegen, um eingehende Werte so zu filtern, dass nur die Werte weitergeleitet werden, die die angegebenen Kriterien erfüllen.  
  
Mithilfe dieser Regel können Sie z. B. nur Ansprüche weiterleiten, die dem Anspruchswert "Käufer" entsprechen, wenn der Typ des eingehenden Anspruchs dem Anspruchstyp "Rolle" entspricht. Sie können mit dieser Regel auch ausschließlich Ansprüche zum Namen des Benutzers, aber keine Ansprüche ausstellen, die die Sozialversicherungsnummer des Benutzers enthalten.  
  
Wenn Sie eine Filterbedingung mit dieser Regel verwenden, werden alle eingehenden Ansprüche untersucht, um zu bestimmen, welche Ansprüche den von der Regel festgelegten Kriterien entsprechen. Alle anderen Ansprüche werden ignoriert, sodass nur angegebene Anspruchswerte, die einem ausgewählten Anspruchstyp entsprechen, weitergeleitet werden.  
  
Z. B. wie in der folgenden Abbildung gezeigt, Anspruchstyp und mit auch beenden, wenn eine Regel mit der Bedingung festgelegt ist, um nur eingehende Ansprüche zu filtern, die auf den Benutzerprinzipalnamen abgestimmt sind @fabrikam.com, alle anderen eingehenden Ansprüche werden ignoriert, es sei denn, sie diese Kriterien erfüllen. Dies schließt den eingehenden Anspruch mit dem Anspruchstyp E\-e-Mail-Adresse, obwohl der Anspruchswert endet @fabrikam.com. In diesem Fall ist nur mit dem Wert des Anspruchs Nick@fabrikam.com wird an die vertrauende Seite gesendet.  
  
![Verwendung von Pass über](media/adfs2_filter.gif)  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel in einer Anspruchsanbietervertrauensstellung  
Bei Verwendung einer Anspruchsanbieter-Vertrauensstellung kann diese Regel zum Weiterleiten von ausschließlich eingehenden Ansprüchen vom Anspruchsanbieter konfiguriert werden, die bestimmten Einschränkungen entsprechen. Angenommen, Sie möchten nur e akzeptiert\-e-Mail-Ansprüche vom Anspruchsanbieter; aus diesem Grund würden Sie diese Regelvorlage verwenden, um e akzeptieren\-e-Mail-Anspruchstypen, die auf DNS des Anspruchsanbieters enden \(DNS\) Name.  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>Konfigurieren diese Regel in einer Vertrauensstellung der vertrauenden Seite  
Wenn Sie eine Vertrauensstellung der vertrauenden Seite verwenden, kann diese Regel so konfiguriert werden, dass an die vertrauende Seite zu sendende ausgehende Ansprüche weitergeleitet oder gefiltert werden. Einige vertrauende Seiten können bestimmte Anspruchstypen ggf. nicht verstehen, oder bestimmte Ansprüche enthalten möglicherweise vertrauliche Informationen, der nicht an bestimmte vertrauende Seiten gesendet werden sollen. Diese Regelvorlage kann helfen, diese Richtlinien für eine bestimmte Vertrauensstellung der vertrauenden Seite zu erzwingen.  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie erstellen diese Regel entweder die anspruchsregelsprache oder der Pass-Through oder Filtern von einer Vorlage des eingehenden Anspruchs-Regel im AD FS-Verwaltungs-Snap-\-in. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Angeben eines eingehenden Anspruchstyps  
  
-   Alle Anspruchswerte weiterleiten  
  
-   Nur einen bestimmten Anspruchswert weiterleiten  
  
-   Pass-through-nur Anspruchswerte durchalufen, die einen bestimmten e entsprechen\-e-Mail-Suffix-Wert  
  
-   Nur Anspruchswerte weiterleiten, die mit einem bestimmten Wert anfangen  
  
Weitere Anweisungen zum Erstellen dieser Vorlage finden Sie [erstellen eine Regel für Pass-Through oder Filtern eines eingehenden Anspruchs](https://technet.microsoft.com/library/dd807060.aspx) in AD FS-Bereitstellungshandbuch.  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Falls ein Anspruch nur gesendet werden soll, wenn der Wert des Anspruchs mit einem benutzerdefinierten Muster übereinstimmt, müssen Sie eine benutzerdefinierte Regel verwenden. Weitere Informationen finden Sie unter "Wann sollte eine benutzerdefinierte Anspruchsregel verwendet werden?".  
  
### <a name="examples-of-how-to-construct-a-pass-through-or-filter-rule-syntax"></a>Beispiele für das Erstellen der Syntax einer Weiterleitungs- oder Filterregel  
Eine einfache Filterregel filtert Ansprüche basierend auf einer der oben beschriebenen Eigenschaften. Die folgende Regel wird z. B. pass-through-alle e\-e-Mail-Ansprüche:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”]  => issue(claim  = c);  
```  
  
Filter können logisch werden und\-verbunden. Die folgende Regel akzeptiert z. B. alle e\-e-Mail-Ansprüche mit dem Wert johndoe@fabrikam.com:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”, value == “johndoe@fabrikam.com “]  => issue(claim  = c);  
```  
  
In den obigen Beispielen wurde bei den Filtern stets ein Gleichheitsoperator verwendet. Die Anspruchsregelsprache unterstützt die folgenden Operatoren:  
  
-   \=\= \- ist gleich \(Fall\-vertrauliche\)  
  
-   \!\= \- entspricht nicht \(Fall\-vertrauliche\)  
  
-   \=~\- Übereinstimmung eines regulären Ausdrucks  
  
-   \!~ \- reguläre Ausdrücke nicht\-übereinstimmen  
  
Die folgende Regel akzeptiert z. B. alle e\-e-Mail-Ansprüche, die nicht von den lokalen Verbundserver ausgestellt, die ein Suffix "Boeing.com" haben:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”, value =~ “^.*@boeing\.com$” , issuer != “LOCAL AUTHORITY”]  => issue(claim  = c);  
```  
  
### <a name="best-practices-for-creating-custom-rules"></a>Bewährte Methoden zum Erstellen benutzerdefinierter Regeln  
Wie in der folgenden Tabelle beschrieben, kann ein Filter auf eine oder mehrere der Eigenschaften jedes Anspruchs angewendet werden.  
  

| Anspruchseigenschaft |                                                                                                                                                                                                                                                                                                                                                  Beschreibung                                                                                                                                                                                                                                                                                                                                                  |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      Typ      |                                                                                                                                                                                        Der Typ des Anspruchs \(in der Regel als Uri dargestellt\) gibt eine implizite Vereinbarung zwischen Partnern in einem Verbund dazu, welche Art von Informationen im Anspruch weitergegeben wird. Z. B. die Ansprüche des Type-http-:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/Identität\/Ansprüche\/e-Mail-Adresse enthält die e\-e-Mail-Adresse des Benutzers.                                                                                                                                                                                         |
|     Wert      |                                                                                                                                                                                                                                                                   Der Wert des Anspruchs. Beispielsweise einen Anspruch vom Typ http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/Identität\/Ansprüche\/Emailaddress möglicherweise einen Wert von johndoe@fabrikam.com                                                                                                                                                                                                                                                                    |
|   ValueType    |                                                                                                                                                                                                  "ValueType" stellt dar, wie die Informationen im Anspruchswert interpretiert werden. In der Regel ValueType wird auf http festgelegt werden:\/\/www.w3.org\/2001\/XMLSchema\#Zeichenfolge, aber der Wert des Anspruchs kann Base64Binary-codierte Daten enthalten \(z. B. ein Bild \) oder eine Datums-, boolescher Wert, und So weiter.                                                                                                                                                                                                  |
|     Aussteller     | "Issuer" ist der Aussteller, der zuletzt die Ansprüche zum Benutzer ausgestellt hat. Wenn die Ansprüche vom Verbundserver eines Anspruchsanbieters bezogen werden, wird der Aussteller aller Ansprüche auf "LOCAL AUTHORITY" festgelegt. Wenn die Ansprüche vom Verbundserver eines Verbundanbieters empfangen wurden, wird der Aussteller der Ansprüche auf die Anspruchsanbieter-ID des Anspruchsanbieters festgelegt, der das Token signiert hat. Wenn anschließend Regeln für Ansprüche verarbeitet werden, die von einem Anspruchsanbieter empfangen wurden, wird der Aussteller der Ansprüche auf denselben Wert festgelegt. Bei der Erstellung von Regeln für eine vertrauende Seite kann die "Issuer"-Eigenschaft verwendet werden, um zwischen Ansprüchen zu unterscheiden, die von verschiedenen Anspruchsanbietern stammen. |
| OriginalIssuer |                                                                                                   Diese Anspruchseigenschaft dient zum Angeben, von welchem Verbundserver der Anspruch ursprünglich ausgestellt wurde. Da die "Issuer"-Eigenschaft der Ansprüche mit dem letzten Verbundserver, die das Token signiert festgelegt ist, wird der ursprüngliche Aussteller nützlich in Szenarien, in denen ein Anspruch über mehr als einen Verbundserver übertragen wurde \(z. B. eine vertrauende Seite, die ein Token erhält. von einem verbundanbieter Verbundserver kann u. interessant sind Ansprüche von welcher bestimmte Verbundserver authentifiziert den Benutzer\)                                                                                                   |
|   Eigenschaften   |                                                                                                                             Neben den oben beschriebenen fünf Eigenschaften hat jeder Anspruch auch einen Eigenschaftenbehälter, in dem benannte Eigenschaften gespeichert werden können. Diese Eigenschaften werden nicht im Token serialisiert und sind nur sinnvoll für die Übergabe von Informationen zwischen Komponenten der Anspruchsausstellungs-Pipeline innerhalb des Zuständigkeitsbereichs eines einzelnen Verbundservers. Beispiel: Festlegen einer Eigenschaft während der Verarbeitung von Anspruchsanbieterregeln und das anschließende Verweisen darauf in den Regeln der vertrauenden Seite.                                                                                                                              |

