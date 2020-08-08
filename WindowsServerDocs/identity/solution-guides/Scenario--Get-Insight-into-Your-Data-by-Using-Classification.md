---
ms.assetid: ad3f0480-99f7-428a-ab33-6d165a440840
title: Szenario erhalten Sie Einblicke in Ihre Daten mithilfe der Klassifizierung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 7c06cc4bbca7e21ffa5ef58ec6e33fc43b3f9e49
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940243"
---
# <a name="scenario-get-insight-into-your-data-by-using-classification"></a>Szenario: Erhalten von Einblicken in Ihre Daten mittels Klassifizierung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Abhängigkeit von Daten- und Speicherressourcen wird für die meisten Organisationen immer bedeutender. IT-Administratoren sind mit der wachsenden Herausforderung konfrontiert, immer größere und komplexere Speicherinfrastrukturen zu überwachen und sind gleichzeitig dafür verantwortlich, dass die Gesamtbetriebskosten ein vernünftiges Maß nicht überschreiten. Beim Verwalten von Speicherressourcen geht es nicht mehr nur um das Volumen oder die Verfügbarkeit von Daten, sondern auch um das Erzwingen von Unternehmensrichtlinien und Informationen zum Speicherverbrauch, um eine effiziente Nutzung und Kompatibilität zu ermöglichen und dadurch wiederum Risiken einzudämmen. Die Dateiklassifizierungsinfrastruktur bietet Einsicht in Ihre Daten, indem Klassifizierungsvorgänge automatisiert werden, damit Sie Ihre Daten effektiver verwalten können. Mit der Dateiklassifizierungsinfrastruktur werden folgende Klassifizierungsmethoden bereitgestellt: manuell, programmgesteuert und automatisch. In diesem Thema liegt der Schwerpunkt auf der automatischen Dateiklassifizierungsmethode.

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Beschreibung des Szenarios
Die Dateiklassifizierungsinfrastruktur verwendet Klassifizierungsregeln zum automatischen Prüfen und Klassifizieren von Dateien entsprechend den Inhalten der Datei. Klassifizierungseigenschaften werden zentral in Active Directory definiert, sodass diese Definitionen dateiserverübergreifend in der Organisation freigegeben werden können. Sie können Klassifizierungsregeln erstellen, die Dateien auf eine standardmäßige Zeichenfolge hin oder auf eine Zeichenfolge hin überprüfen, die mit einem Muster (regulärer Ausdruck) übereinstimmt. Wird ein konfigurierter Klassifizierungsparameter in einer Datei gefunden, wird diese Datei in der Klassifizierungsregel als konfiguriert klassifiziert. Zu einigen Klassifizierungsregelbeispielen zählen:

-   Klassifizieren Sie jede Datei mit der Zeichenfolge "", die die Zeichenfolge "" enthält, als hohe geschäftliche Auswirkung.

-   Klassifizierung einer beliebigen Datei, die mindestens zehn Sozialversicherungsnummern mit persönlich identifizierbaren Informationen enthält

Wenn eine Datei klassifiziert wird, können Sie eine Dateiverwaltungsaufgabe verwenden, um Maßnahmen für die auf eine bestimmte Art und Weise klassifizierten Dateien einzuleiten. Zu den Maßnahmen in einer Dateiverwaltungsaufgabe zählen das Schützen der mit der Datei verknüpften Rechte, das Ablaufen der Datei sowie das Ausführen einer benutzerdefinierten Aktion (wie das Veröffentlichen von Informationen in einem Webdienst).

Planungsinformationen für das Konfigurieren der automatischen Dateiklassifizierung finden Sie unter [Planen der automatischen Dateiklassifizierung](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955).

Schritte zum automatischen klassifizieren von Dateien finden Sie unter Bereitstellen der [automatischen Datei Klassifizierung &#40;Demonstrations Schritte&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md).

## <a name="in-this-scenario"></a>Inhalt dieses Szenarios
Dieses Szenario ist ein Bestandteil des Szenarios für die dynamische Zugriffssteuerung. Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter:

-   [Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Die Datei Klassifizierungs Infrastruktur in Windows Server 2012 trägt zu dynamischen Access Control bei, indem Geschäftsdaten Besitzern das einfache klassifizieren und bezeichnen von Daten ermöglicht wird. Die in der zentralen Zugriffsrichtlinie gespeicherten Klassifizierungsinformationen ermöglichen Ihnen das Definieren von Zugriffsrichtlinien für Datenklassen, die für das Unternehmen entscheidend sind.

## <a name="features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Features
In der folgenden Tabelle werden die Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.

|Feature|Auf welche Weise dieses Szenario unterstützt wird|
|-----------|---------------------------------|
|[File Server Resource Manager Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11))|Die Dateiklassifizierungsinfrastruktur ist ein im Ressourcen-Manager für Dateiserver enthaltenes Feature.|
|[Datei- und Speicherdienste: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831487(v=ws.11))|Der Ressourcen-Manager für Dateiserver ist ein in der Serverrolle „Dateidienste“ enthaltenes Feature.|

