---
ms.assetid: 606df285-259c-4c6b-8583-9aca1d614c43
title: Verwendung von Pass-Through or Filter Claim Rule
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aa205c46bf67dc25a55232b799bdd39fee4ac3c6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="when-to-use-a-pass-through-or-filter-claim-rule"></a>Verwendung von Pass-Through or Filter Claim Rule
Diese Regel können in Active Directory Federation Services die Werte im eingehenden Anspruch \(AD FS\) bei müssen Sie einen bestimmten Typ des eingehenden Anspruchs aufnehmen und dann eine Aktion anwenden, die bestimmen, welche Ausgabe erfolgen soll abhängig. Wenn Sie diese Regel verwenden, Sie weiterleiten oder Filtern Ansprüche, die der Regellogik in der folgenden Tabelle, die auf Grundlage der Optionen, die Sie, in der Regel konfigurieren entsprechen.  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle Anspruchswerte weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *einen beliebigen Wert*, den Anspruch weiterleiten|  
|Nur einen bestimmten Anspruchswert weiterleiten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*, den Anspruch weiterleiten|  
|Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E\ E-Mail-Suffixwert entsprechen|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Suffixwert*, den Anspruch weiterleiten|  
|Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert beginnt mit *angegebenen Anspruchswert*, den Anspruch weiterleiten|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Detail zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \ (wenn x dann Y\) und erstellen Sie einen ausgehenden Anspruch auf Grundlage der Bedingung-Parameter. Die folgende Liste enthält wichtige Tipps, die Sie kennen sollten Anspruchsregeln bevor Sie weiter lesen in diesem Thema:  
  
-   In der AD FS-Verwaltungs-Snap-In können Anspruchsregeln nur erstellt werden mithilfe von anspruchsregelvorlagen  
  
-   Anspruch Regeln Prozess eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \ (z.B. Active Directory oder einem anderen Verbundservern Service\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Durch die Rangfolge der Regeln festlegen, können Sie optimieren oder Filtern Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden.  
  
-   Anspruchsregelvorlagen werden immer müssen Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie anspruchsregelsätzen verarbeitet werden, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="pass-through-all-claim-values"></a>Alle Anspruchswerte weiterleiten  
Wenn Sie diese Aktion verwenden, werden alle eingehenden Anspruchswerte für den angegebenen Anspruchstyp als ausgehende Ansprüche weitergereicht. Wenn der Typ des eingehenden Anspruchs als Anspruchstyp "Rolle" angegeben wird, werden alle eingehenden Anspruchswerte z.B. einzeln in neue ausgehende Ansprüche mit dem ausgehenden Anspruchstyp "Rolle" kopiert.  
  
## <a name="filtering-a-claim"></a>Filtern eines Anspruchs  
In AD FS, der Begriff *Ansprüche Filterung* Mittel zum Filtern bzw. einschränken eingehender Anspruchswerte, sodass nur bestimmte Werte weitergeleitet bzw. als ausgehende Ansprüche gesendet werden. Es ist die **weiterleiten oder Filtern eines eingehenden Anspruchs** -Vorlage, die diese Funktion ermöglicht. In den Eigenschaften der Regel können Sie festlegen, Bedingungen für eine eingehende Werte so filtern, dass nur die Werte, die die angegebenen Kriterien erfüllen weitergeleitet werden.  
  
Mit dieser Regel können Sie z.B. nur Ansprüche, die den Wert des Anspruchs Käufer entsprechen, wenn die des eingehenden Anspruchs der Anspruchstyp Rollen- oder Sie ausschließlich Ansprüche zum Namen des Benutzers ausstellen möchten übereinstimmt, aber keine Ansprüche, die die Sozialversicherungsnummer des Benutzers mit durchlaufen.  
  
Wenn Sie eine filterbedingung mit dieser Regel verwenden, werden alle eingehenden Ansprüche untersucht, um zu bestimmen, welche Ansprüche, die von der Regel festgelegten Kriterien entsprechen. Alle anderen Ansprüche werden ignoriert, sodass nur angegebene Anspruchswerte, die einen ausgewählten Anspruchstyp entsprechen, weitergeleitet werden.  
  
Z.B. wie in der folgenden Abbildunggezeigt, wenn eine Regel mit der Bedingung festgelegt ist, um nur eingehende Ansprüche gefiltert werden, die auf den Benutzerprinzipalnamen abgestimmt sind Anspruchstyp arbeiten und auch enden mit @fabrikam.com, alle anderen eingehenden Ansprüche werden ignoriert, es sei denn, sie diese Kriterien erfüllen. Dies schließt den eingehenden Anspruch mit dem Anspruchstyp E\ E-Mail-Adresse, obwohl der Anspruchswert endet @fabrikam.com. In diesem Fall mit dem Wert des Anspruchs Nick@fabrikam.coman die vertrauende Seite gesendet wird.  
  
![Verwendung von Pass über](media/adfs2_filter.gif)  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>Konfigurieren diese Regel auf eine Anspruchsanbieter-Vertrauensstellung  
Bei Verwendung eine Anspruchsanbieter-Vertrauensstellung diese Regel so konfiguriert werden, durchlaufen ausschließlich eingehenden Ansprüche vom Anspruchsanbieter, die bestimmten Einschränkungen entsprechen. Sie möchten z.B. nur E\ E-Mail-Ansprüche vom Anspruchsanbieter akzeptieren; Daher verwenden Sie diese Regelvorlage E\ E-Mail-Anspruchstypen zu akzeptieren, die im Domain Name System \(DNS\)-Namen des Anspruchsanbieters enden.  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>Konfigurieren diese Regel für eine Vertrauensstellung der vertrauenden Seite  
Wenn Sie eine Vertrauensstellung der vertrauenden Seite verwenden, kann diese Regel zum Weiterleiten oder Filtern ausgehende Ansprüche, die auf die vertrauende Seite gesendet werden, konfiguriert werden. Einige vertrauenden Seiten können bestimmte Anspruchstypen nicht verstehen, oder bestimmte Ansprüche enthalten möglicherweise vertrauliche Informationen, die nicht an bestimmte vertrauenden Seiten gesendet werden soll. Diese Regelvorlage kann helfen, diese Richtlinien für eine bestimmte Vertrauensstellung einer vertrauenden Seite erzwingen.  
  
## <a name="how-to-create-this-rule"></a>Vorgehensweise beim Erstellen dieser Regel  
Sie erstellen diese Regel entweder mithilfe der anspruchsregelsprache oder weiterleiten oder Filtern einer eingehenden Anspruchs Regelvorlage in AD FS-Verwaltungs-Snap-In. Diese Regelvorlage bietet die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Geben Sie einen Typ des eingehenden Anspruchs  
  
-   Alle Anspruchswerte weiterleiten  
  
-   Nur einen bestimmten Anspruchswert weiterleiten  
  
-   Nur Anspruchswerte weiterleiten Sie, die einem bestimmten E\ E-Mail-Suffixwert entsprechen  
  
-   Nur Anspruchswerte weiterleiten Sie, die mit einem bestimmten Wert starten  
  
Weitere Informationen zum Erstellen dieser Vorlage finden Sie unter [Erstellen einer Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs](https://technet.microsoft.com/library/dd807060.aspx) in AD FS-Bereitstellungshandbuch.  
  
## <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
Wenn ein Anspruch gesendet werden soll, nur, wenn der Wert des Anspruchs mit einem benutzerdefinierten Muster übereinstimmt, müssen Sie eine benutzerdefinierte Regel verwenden. Weitere Informationen finden Sie unter Verwendung einer benutzerdefinierten Regel.  
  
### <a name="examples-of-how-to-construct-a-pass-through-or-filter-rule-syntax"></a>Beispiele zum Erstellen von Pass-through oder Filtern Regel syntax  
Eine einfache Filterregel würde Ansprüche basierend auf einer der oben beschriebenen Eigenschaften filtern. Die folgende Regel wird z.B. alle E\ E-Mail-Ansprüche passieren:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”]  => issue(claim  = c);  
```  
  
Filter können logisch AND\ verknüpft werden. Die folgende Regel wird z.B. alle E\ E-Mail-Ansprüche mit Wert akzeptiert.johndoe@fabrikam.com:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”, value == “johndoe@fabrikam.com “]  => issue(claim  = c);  
```  
  
In den obigen Beispielen verwendet die Filtern stets einen Gleichheitsoperator. Die anspruchsregelsprache unterstützt die folgenden Operatoren:  
  
-   \ = \ = \-\(case\-sensitive\) entspricht  
  
-   \! \ = \-nicht gleich \(case\-sensitive\)  
  
-   \ = ~ \-regulären Ausdruck übereinstimmen  
  
-   \! ~ \--Übereinstimmung regulären Ausdruck  
  
Die folgende Regel akzeptiert z.B., alle E\ E-Mail-Ansprüche, die nicht von den lokalen Verbundserver ausgestellt, die als Suffix boeing.com haben:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”, value =~ “^.*@boeing\.com$” , issuer != “LOCAL AUTHORITY”]  => issue(claim  = c);  
```  
  
### <a name="best-practices-for-creating-custom-rules"></a>Bewährte Methoden zum Erstellen benutzerdefinierter Regeln  
Ein Filter kann auf eine oder mehrere der Eigenschaften jedes Anspruchs angewendet werden, wie in der folgenden Tabelle beschrieben.  
  
|Anspruchs-Eigenschaft|Beschreibung|  
|------------------|---------------|  
|Typ|Der Typ des Anspruchs \ (in der Regel als eine Uri\ dargestellt) gibt eine implizite Vereinbarung zwischen Partnern in einem Verbund dazu, welche Art von Informationen im Anspruch weitergegeben wird. Ansprüche des Typs http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/emailaddress werden z.B. die E\-Mail-Adresse des Benutzers enthalten.|  
|Wert|Der Wert des Anspruchs. Ein Anspruchs des Typs http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/emailaddress kann z.B. der Wert haben.johndoe@fabrikam.com|  
|ValueType|"ValueType" darstellt, wie die Informationen im Anspruchswert interpretiert werden. In der Regel wird "ValueType" auf http:///\/www.w3.org\/2001\/XMLSchema\#string festgelegt, aber der Wert des Anspruchs kann Base64Binary-codierte Daten enthalten \ (z.B. Image\) oder Datum, Boolean und So weiter.|  
|Aussteller|Die "Issuer" ist die Partei, die zuletzt die Ansprüche zum Benutzer ausgestellt hat. Wenn die Ansprüche an einen Ansprüche vom Verbundserver, die der Aussteller aller Ansprüche auf "LOCAL AUTHORITY" festgelegt werden soll abgerufen werden. Wenn die Ansprüche von einem verbundanbieters empfangen wurden, geht der Aussteller der Ansprüche auf die Anspruchsanbieter-ID des Anspruchsanbieters festgelegt werden, die das Token signiert hat. Daher wird bei der Verarbeitung von Regeln für Ansprüche, die von einem Anspruchsanbieter empfangen der Aussteller aller Ansprüche soll auf denselben Wert festgelegt werden. Beim Erstellen von Regeln für eine vertrauende Seite kann die "Issuer"-Eigenschaft verwendet werden, unterscheiden, Ansprüche, die von verschiedenen Anspruchsanbietern stammen.|  
|OriginalIssuer|Diese anspruchseigenschaft dient zum Übermitteln von welchem Verbundserver den Anspruch ursprünglich ausgestellt. Da die "Issuer"-Eigenschaft der Ansprüche mit dem letzten Verbundserver, die das Token signiert hat festgelegt ist, ist der ursprüngliche Aussteller nützlich in Szenarien, in denen ein Anspruch über mehr als einen Verbundserver übertragen wurde \ (z.B. eine vertrauende Seite, die ein Token aus einer verbundanbieters empfängt möglicherweise daran interessiert, welcher bestimmte Ansprüche vom Verbundserver authentifiziert, die durch den Benutzer)|  
|Eigenschaften|Zusätzlich zu den oben beschriebenen fünf Eigenschaften hat jeder Anspruch auch einen Eigenschaftenbehälter, in dem benannte Eigenschaften gespeichert werden können. Diese Eigenschaften werden nicht im Token serialisiert und nur sinnvoll für die Übergabe von Informationen zwischen Komponenten der anspruchsausstellungs-Pipeline innerhalb des Zuständigkeitsbereichs eines einzelnen Verbundservers. Z.B. Festlegen einer Eigenschaft während der Ansprüche Anbieter Regeln verarbeitet und anschließende verweisen darauf in der vertrauenden Seite Regeln.|  
  

