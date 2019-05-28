---
title: Fügen Sie die erforderlichen Metadaten-Tags auf Ihr Windows Server-Artikel
description: Eine Liste mit den Informationen müssen Sie als Tags für Metadaten und dem oberen Rand von Windows Server-bezogenen Artikeln hinzufügen. Die erforderlichen Tags unterliegen, basierend auf Anforderungen von sowohl aufgrund Ihrer Berichte und -Team.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: f7c514def1353d44386b1bc53c8cabffe1e31fda
ms.sourcegitcommit: 7e54a1bcd31cd2c6b18fd1f21b03f5cfb6165bf3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461646"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>Fügen Sie die erforderlichen Metadaten-Tags auf Ihr Windows Server-Artikel

Am oberen Rand jedes Artikels gibt es spezifische Metadaten, der für die nachverfolgung und SEO-Zwecke eingeschlossen werden muss. Die erforderlichen Tags unterliegen ändern sich je nach Anforderungen ab. Allerdings sollten Sie benachrichtigt werden, wenn Sie Felder hinzufügen oder entfernen möchten.

Es sollte folgendermaßen aussehen, einschließlich der drei Bindestrichen (-) am oberen und unteren:

```markdown

---
title: The title of the article should go here. This is used in SEO and search results.

description: A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they’re looking for.

ms.prod: Use this specific text, windows-server-threshold

ms.reviewer: The Microsoft alias for the primary PM for the feature/functionality

author: Your GitHub alias

ms.author: Your Microsoft alias

manager: Your manager’s Microsoft alias

ms.topic: Type of article, including article, landing-page, get-started-article, or reference

ms.date: Date of change (MM/DD/YYYY)

---

```

## <a name="example"></a>Beispiel

```markdown

---
title: What is Windows Admin Center?
description: Learn about the Windows Admin Center, a locally-deployed, browser-based management tool set that lets you manage your Windows Servers with no Azure or cloud dependency.
ms.prod: windows-server-threshold
ms.reviewer: alainch
author: danielle-github
ms.author: danielle
manager: alainch
ms.topic: article
ms.date: 07/06/2019
---

```