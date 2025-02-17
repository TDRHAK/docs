---
title: Cambiar tu dirección principal de correo electrónico
intro: You can change the email address associated with your personal account at any time.
redirect_from:
- /articles/changing-your-primary-email-address
- /github/setting-up-and-managing-your-github-user-account/changing-your-primary-email-address
- /github/setting-up-and-managing-your-github-user-account/managing-email-preferences/changing-your-primary-email-address
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
- Accounts
- Notifications
shortTitle: Primary email address
ms.openlocfilehash: af1443f1f23b8038d2cf1f4e42a1ab0a83214edb
ms.sourcegitcommit: 67064b14c9d4d18819db8f6398358b77a1c8002a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2022
ms.locfileid: "145093159"
---
{% note %}

**Nota:** No puede cambiar la dirección de correo electrónico principal por una que ya se haya configurado como dirección de correo electrónico de respaldo.

{% endnote %}

{% data reusables.user-settings.access_settings %} {% data reusables.user-settings.emails %}
3. Si quiere agregar una dirección de correo electrónico nueva para que sea la principal, en "Agregar dirección de correo electrónico", escriba una dirección nueva y haga clic en **Agregar**.
   ![Botón para agregar otra dirección de correo electrónico](/assets/images/help/settings/add_another_email_address.png)
4. En "Dirección de correo electrónico principal", use el menú desplegable para hacer clic en la dirección que quiera establecer como principal y haga clic en **Guardar**.
   ![Botón Establecer como principal](/assets/images/help/settings/set_as_primary_email.png)
5. Para quitar la dirección de correo electrónico antigua de la cuenta, haga clic en {% octicon "trash" aria-label="The trash symbol" %} junto al correo electrónico antiguo.
{% ifversion fpt or ghec %}
6. Verifica tu nueva dirección principal de correo electrónico. Sin una dirección de correo electrónico verificada, no podrás usar todas las características de {% data variables.product.product_name %}. Para más información, vea "[Comprobación de la dirección de correo electrónico](/articles/verifying-your-email-address)".
{% endif %}
