---
ms.openlocfilehash: 1447b6a0f63bcfd6e54954545541808debcb3091
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: "147062368"
---
### 解决对话

如果您打开了拉取请求或者您对被打开拉取请求的仓库具有写入权限，您可以解决拉取请求中的对话。

要指示“文件已更改”选项卡上的对话已完成，请单击“解决对话” 。

![带解决对话按钮的拉取请求对话](/assets/images/help/pull_requests/conversation-with-resolve-button.png)

整个对话将被折叠并标记为已解决，以便您更容易找到仍需解决的对话。

![已解决对话](/assets/images/help/pull_requests/resolved-conversation.png)

如果评论中的建议超出您的拉取请求范围，您可以打开一个新的议题，追踪反馈并链接到原始评论。 有关详细信息，请参阅“[从评论创建问题](/github/managing-your-work-on-github/opening-an-issue-from-a-comment)”。

{% ifversion fpt or ghes or ghae-issue-4382 or ghec %}
#### 发现和导航对话

可以使用显示于“更改的文件”选项卡顶部的“对话”菜单发现和导航到拉取请求中的所有对话 。

从此视图中，您可以看到哪些对话未解决、已解决和过时。 这使得很容易发现和解决对话。

![显示对话菜单](/assets/images/help/pull_requests/conversations-menu.png) {% endif %}
