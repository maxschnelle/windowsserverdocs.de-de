---
ms.assetid: ad3f0480-99f7-428a-ab33-6d165a440840
title: Szenario-Get-Einsicht in Ihre Daten mittels Klassifizierung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2e5248b5fd5e20b7436de9f796367c018d8ef16e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881481"
---
# <a name="scenario-get-insight-into-your-data-by-using-classification"></a>Szenario: Erhalten von Einblicken in Ihre Daten mittels Klassifizierung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Abhängigkeit von Daten- und Speicherressourcen wird für die meisten Organisationen immer bedeutender. IT-Administratoren sind mit der wachsenden Herausforderung konfrontiert, immer größere und komplexere Speicherinfrastrukturen zu überwachen und sind gleichzeitig dafür verantwortlich, dass die Gesamtbetriebskosten ein vernünftiges Maß nicht überschreiten. Beim Verwalten von Speicherressourcen geht es nicht mehr nur um das Volumen oder die Verfügbarkeit von Daten, sondern auch um das Erzwingen von Unternehmensrichtlinien und Informationen zum Speicherverbrauch, um eine effiziente Nutzung und Kompatibilität zu ermöglichen und dadurch wiederum Risiken einzudämmen. Die Dateiklassifizierungsinfrastruktur bietet Einsicht in Ihre Daten, indem Klassifizierungsvorgänge automatisiert werden, damit Sie Ihre Daten effektiver verwalten können. Mit der Dateiklassifizierungsinfrastruktur werden folgende Klassifizierungsmethoden bereitgestellt: manuell, programmgesteuert und automatisch. In diesem Thema liegt der Schwerpunkt auf der automatischen Dateiklassifizierungsmethode.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Die Dateiklassifizierungsinfrastruktur verwendet Klassifizierungsregeln zum automatischen Prüfen und Klassifizieren von Dateien entsprechend den Inhalten der Datei. Klassifizierungseigenschaften werden zentral in Active Directory definiert, sodass diese Definitionen dateiserverübergreifend in der Organisation freigegeben werden können. Sie können Klassifizierungsregeln erstellen, die Dateien auf eine standardmäßige Zeichenfolge hin oder auf eine Zeichenfolge hin überprüfen, die mit einem Muster (regulärer Ausdruck) übereinstimmt. Wird ein konfigurierter Klassifizierungsparameter in einer Datei gefunden, wird diese Datei in der Klassifizierungsregel als konfiguriert klassifiziert. Zu einigen Klassifizierungsregelbeispielen zählen:  
  
-   Jede Datei, die die Zeichenfolge "Contoso vertraulich" enthält als mit hoher unternehmensauswirkung klassifiziert  
  
-   Klassifizierung einer beliebigen Datei, die mindestens zehn Sozialversicherungsnummern mit persönlich identifizierbaren Informationen enthält  
  
Wenn eine Datei klassifiziert wird, können Sie eine Dateiverwaltungsaufgabe verwenden, um Maßnahmen für die auf eine bestimmte Art und Weise klassifizierten Dateien einzuleiten. Zu den Maßnahmen in einer Dateiverwaltungsaufgabe zählen das Schützen der mit der Datei verknüpften Rechte, das Ablaufen der Datei sowie das Ausführen einer benutzerdefinierten Aktion (wie das Veröffentlichen von Informationen in einem Webdienst).  
  
Planungsinformationen für das Konfigurieren der automatischen Dateiklassifizierung finden Sie unter [Planen der automatischen Dateiklassifizierung](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955).  
  
Finden Sie schrittweise Anleitung zum automatischen Klassifizieren von Dateien in [Bereitstellen der automatischen Dateiklassifizierung &#40;Demonstrationsschritte&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Dateiklassifizierungsinfrastruktur unter Windows Server 2012 unterstützt dynamische Zugriffssteuerung, indem unternehmensdatenbesitzer Daten einfach klassifizieren und bezeichnen können. Die in der zentralen Zugriffsrichtlinie gespeicherten Klassifizierungsinformationen ermöglichen Ihnen das Definieren von Zugriffsrichtlinien für Datenklassen, die für das Unternehmen entscheidend sind.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features  
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------|---------------------------------|  
|[Übersicht über die Ressourcen-Manager](https://technet.microsoft.com/library/hh831701.aspx)|Die Dateiklassifizierungsinfrastruktur ist ein im Ressourcen-Manager für Dateiserver enthaltenes Feature.|  
|[Datei- und Speicherdienste: Übersicht](https://technet.microsoft.com/library/hh831487.aspx)|Der Ressourcen-Manager für Dateiserver ist ein in der Serverrolle „Dateidienste“ enthaltenes Feature.|  
  


