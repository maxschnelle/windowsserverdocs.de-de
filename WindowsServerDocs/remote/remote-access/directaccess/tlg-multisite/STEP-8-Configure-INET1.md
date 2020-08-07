---
title: Schritt 8 Konfigurieren von INET1
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: 2e53eb8af7327932123fde8eb138611e5ae65242
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953676"
---
# <a name="step-8-configure-inet1"></a>SCHRITT 8: Konfigurieren von INET1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Damit Client Computer eine Verbindung mit RAS-Servern über das Internet herstellen können, müssen Sie einen DNS-Eintrag für 2-Edge1 auf INET1 konfigurieren.

### <a name="to-create-the-2-edge1-dns-entry"></a>So erstellen Sie den 2 Edge1-DNS-Eintrag

1.  Geben Sie auf der **Start** Seite**dnsmgmt. msc**ein, und drücken Sie dann die EINGABETASTE.

2.  Öffnen Sie in der Konsolen Struktur **Forward-Lookupzonen**, klicken Sie auf **contoso.com**, klicken Sie mit der rechten Maustaste auf **contoso.com**, und klicken Sie dann auf **neuer Host (A oder AAAA)**.

3.  Geben Sie unter **Name den Namen** **2-Edge1**ein. Geben Sie unter **IP-Adresse**den Namen **131.107.0.20**ein. Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.



