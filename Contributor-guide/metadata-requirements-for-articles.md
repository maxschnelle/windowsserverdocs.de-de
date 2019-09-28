---
title: Hinzufügen der erforderlichen Metadatentags zu Ihrem Windows Server-bezogenen Artikel
description: Eine Liste der Informationen, die Sie als Metadatentags am Anfang Ihrer Windows Server-bezogenen Artikel hinzufügen müssen. Die erforderlichen Tags können je nach Berichterstellung und Teamanforderungen geändert werden.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 9bedc7ec13aedab9cfaa655f537d5e431d20cccb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363957"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>Hinzufügen der erforderlichen Metadatentags zu Ihrem Windows Server-bezogenen Artikel

Am Anfang jedes Artikels gibt es bestimmte Metadaten, die für die Nachverfolgung und SEO verwendet werden müssen. Die erforderlichen Tags können basierend auf den Berichterstattungs Anforderungen geändert werden. Sie sollten jedoch benachrichtigt werden, wenn Sie Felder hinzufügen bzw. entfernen müssen.

Es sollte wie folgt aussehen, einschließlich der drei Bindestriche (---) oben und unten:

```markdown

---
title: The title of the article should go here. This is used in SEO and search results.

description: A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they're looking for.

ms.prod: Use this specific text, windows-server-threshold

ms.reviewer: The Microsoft alias for the primary PM for the feature/functionality

author: Your GitHub alias

ms.author: Your Microsoft alias

manager: Your manager's Microsoft alias

ms.topic: Type of article, including article, landing-page, get-started-article, or reference

ms.date: Date of change (MM/DD/YYYY)

---

```

## <a name="example"></a>Beispiel

```markdown

---
title: What is Windows Admin Center?
description: Learn about the Windows Admin Center, a locally-deployed, browser-based management tool set that lets you manage your Windows Servers with no Azure or cloud dependency.
ms.prod: windows-server
ms.reviewer: alainch
author: danielle-github
ms.author: danielle
manager: alainch
ms.topic: article
ms.date: 07/06/2019
---

```