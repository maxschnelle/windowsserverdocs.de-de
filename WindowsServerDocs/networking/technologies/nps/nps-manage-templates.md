---
title: Verwalten von NPS-Vorlagen
description: Dieses Thema enthält Anweisungen zum Erstellen, anwenden, exportieren und Importieren von NPS-Vorlagen für den Netzwerk Richtlinien Server in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 989b00c5-4767-4081-ace5-6321f8b2c55e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7380f5a712294b1583a7d552ef695811f8cebef4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952116"
---
# <a name="manage-nps-templates"></a>Verwalten von NPS-Vorlagen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können Netzwerk Richtlinien Server- \( NPS \) -Vorlagen verwenden, um Konfigurationselemente zu erstellen, z. b. Remote Authentication Dial-in User Service \( RADIUS \) -Clients oder gemeinsame geheime Schlüssel, die Sie für den lokalen NPS wieder verwenden und für die Verwendung auf anderen NPSS verwenden können.

Die Vorlagen Verwaltung bietet einen Knoten in der NPS-Konsole, in dem Sie die Verwendung von NPS-Vorlagen erstellen, ändern, löschen, duplizieren und anzeigen können. NPS-Vorlagen sind so konzipiert, dass der Zeit-und Kostenaufwand für die Konfiguration von NPS auf einem oder mehreren Servern reduziert wird.

Die folgenden NPS-Vorlagen Typen sind für die Konfiguration in der Vorlagen Verwaltung verfügbar.

- **Gemeinsame**geheime Schlüssel. Dieser Vorlagentyp ermöglicht es Ihnen, einen gemeinsamen geheimen Schlüssel anzugeben, den Sie wieder verwenden können (indem Sie die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen), wenn Sie RADIUS-Clients und-Server konfigurieren.

- **RADIUS-Clients**. Dieser Vorlagentyp ermöglicht Ihnen das Konfigurieren von RADIUS-Client Einstellungen, die Sie wieder verwenden können, indem Sie die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen.

- **Remote-RADIUS-Server**. Diese Vorlage ermöglicht es Ihnen, Remote-RADIUS-Servereinstellungen zu konfigurieren, die Sie wieder verwenden können, indem Sie die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen.

- **IP-Filter**. Diese Vorlage ermöglicht Ihnen das Erstellen von IPv6-und Internetprotokoll Version 6- \( IPv6- \) Filtern, die Sie wieder verwenden können, indem Sie \( die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen, \) Wenn Sie Netzwerk Richtlinien konfigurieren.

## <a name="create-an-nps-template"></a>Erstellen einer NPS-Vorlage

Das Konfigurieren einer Vorlage unterscheidet sich von der direkten Konfiguration des NPS. Das Erstellen einer Vorlage wirkt sich nicht auf die Funktionalität von NPS aus. Dies ist nur der Fall, wenn Sie die Vorlage an der entsprechenden Stelle in der NPS-Konsole auswählen und die Vorlage anwenden, dass sich die Vorlage auf die NPS-Funktionalität auswirkt.

Wenn Sie z. b. einen RADIUS-Client in der NPS-Konsole unter **RADIUS-Clients und-Server**konfigurieren, ändern Sie die NPS-Konfiguration, und führen Sie einen Schritt aus, um die NPS für die Kommunikation mit einem Ihrer Netzwerk Zugriffs Server zu konfigurieren. \(Der nächste Schritt besteht darin, den Netzwerk Zugriffs Server- \( NAS \) für die Kommunikation mit NPS zu konfigurieren.\)

Wenn Sie jedoch eine neue **RADIUS** -Client Vorlage in der NPS-Konsole unter **Vorlagen Verwaltung** konfigurieren, anstatt einen neuen RADIUS-Client unter **RADIUS-Clients und-Server zu**erstellen, haben Sie eine Vorlage erstellt, aber Sie haben die NPS-Funktionalität noch nicht geändert. Um die NPS-Funktionalität zu ändern, müssen Sie die Vorlage an der richtigen Stelle in der NPS-Konsole anwenden.

Das folgende Verfahren enthält Anweisungen zum Erstellen einer neuen Vorlage.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-create-an-nps-template"></a>So erstellen Sie eine NPS-Vorlage


1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.

2. Erweitern Sie in der NPS-Konsole den Eintrag **Vorlagen Verwaltung**, klicken Sie mit der rechten Maustaste auf einen Vorlagentyp, **z. b**. **RADIUS-Clients**, und klicken Sie

3. Das Dialogfeld neue Vorlagen Eigenschaften wird geöffnet, mit dem Sie Ihre Vorlage konfigurieren können.

## <a name="apply-an-nps-template"></a>Anwenden einer NPS-Vorlage

Sie können eine Vorlage verwenden, die Sie in der **Vorlagen Verwaltung** erstellt haben, indem Sie zu einem Speicherort in der NPS-Konsole navigieren, auf dem Sie die Vorlage anwenden können. Wenn Sie z. b. eine Vorlage für freigegebene Geheimnisse auf eine RADIUS-Client Konfiguration anwenden möchten, können Sie das folgende Verfahren verwenden.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-apply-an-nps-template"></a>So wenden Sie eine NPS-Vorlage an

1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die NPS-Konsole wird geöffnet.

2. Erweitern Sie in der NPS-Konsole **RADIUS-Clients und-Server**, und erweitern Sie dann RADIUS- **Clients**.

3.in **RADIUS-Clients**, klicken Sie im Detailbereich mit der rechten Maustaste auf den RADIUS-Client, auf den Sie die NPS-Vorlage anwenden möchten, und klicken Sie dann auf **Eigenschaften**.

4. Wählen Sie im Dialogfeld Eigenschaften für den RADIUS-Client unter **vorhandene freigegebene**geheime Schlüssel auswählen die Vorlage aus, die Sie aus der Liste der Vorlagen anwenden möchten.

## <a name="export-or-import-nps-templates"></a>Exportieren oder Importieren von NPS-Vorlagen

Sie können Vorlagen für die Verwendung auf anderen NPSS exportieren, oder Sie können Vorlagen für die Verwendung auf dem lokalen Computer in die **Vorlagen Verwaltung** importieren.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

### <a name="to-export-or-import-nps-templates"></a>So exportieren oder importieren Sie NPS-Vorlagen

1. Um NPS-Vorlagen zu exportieren, klicken Sie in der NPS-Konsole mit der rechten Maustaste auf **Vorlagen Verwaltung**, und klicken Sie dann auf **Vorlagen in eine Datei exportieren**.

2. Um NPS-Vorlagen zu importieren, klicken Sie in der NPS-Konsole mit der rechten Maustaste auf **Vorlagen Verwaltung**, und klicken Sie dann auf **Vorlagen von einem Computer importieren** oder **Vorlagen aus einer Datei importieren**.


