---
title: エンタープライズ マネージド ユーザーの SAML シングル サインオンの構成
shortTitle: SAML for managed users
intro: 'Security Assertion Markup Language (SAML) シングル サインオン (SSO) を構成することで、{% data variables.product.prodname_dotcom %} の Enterprise アカウントへのアクセスを自動的に管理できます。'
product: '{% data reusables.gated-features.emus %}'
redirect_from:
  - /github/setting-up-and-managing-your-enterprise/managing-your-enterprise-users-with-your-identity-provider/configuring-saml-single-sign-on-for-enterprise-managed-users
  - /admin/authentication/managing-your-enterprise-users-with-your-identity-provider/configuring-saml-single-sign-on-for-enterprise-managed-users
  - /admin/identity-and-access-management/managing-iam-with-enterprise-managed-users/configuring-saml-single-sign-on-for-enterprise-managed-users
  - /admin/identity-and-access-management/using-enterprise-managed-users-and-saml-for-iam/configuring-saml-single-sign-on-for-enterprise-managed-users
versions:
  ghec: '*'
type: tutorial
topics:
  - Authentication
  - Enterprise
  - SSO
ms.openlocfilehash: d83c6ea74ae6a27fc5f91ebdc5dcae83e0c22eb2
ms.sourcegitcommit: c562c85cc75ffe1eb4e9595d8adc09ec71697ab1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2022
ms.locfileid: '148180054'
---
## {% data variables.product.prodname_emus %} の SAML シングル サインオンについて

{% data variables.product.prodname_emus %} を使用すると、エンタープライズは企業の ID プロバイダーを使用してすべてのメンバーを認証します。 {% data variables.product.prodname_dotcom %} ユーザー名とパスワードを使用して {% data variables.product.prodname_dotcom %} にサインインする代わりに、エンタープライズのメンバーは IdP を介してサインインします。

{% data variables.product.prodname_emus %} では、次の IdP がサポートされています。

{% data reusables.enterprise-accounts.emu-supported-idps %}

SAML SSO を構成した後は、ID プロバイダーが利用できない場合にエンタープライズへのアクセスを回復できるように、回復用コードを格納することをお勧めします。


{% data reusables.enterprise_user_management.SAML-to-OIDC-migration-for-EMU %}

{% note %}

**注:** SAML SSO が有効になっている場合、既存の SAML 構成の {% data variables.product.prodname_dotcom %} に対して更新できる唯一の設定は SAML 証明書です。 サインオン URL または発行者を更新する必要がある場合は、まず SAML SSO を無効にしてから、新しい設定で SAML SSO を再構成する必要があります。

{% endnote %}

## {% data variables.product.prodname_emus %} の SAML シングル サインオンの構成

{% data variables.enterprise.prodname_emu_enterprise %} の SAML SSO を構成するには、IdP でアプリケーションを構成してから、GitHub.com でエンタープライズを構成する必要があります。 SAML SSO を構成したら、ユーザー プロビジョニングを構成できます。 

IdP に {% data variables.product.prodname_emu_idp_application %} アプリケーションをインストールして構成するには、サポートされている IdP に対するテナントと管理アクセス権が必要です。

{% note %}

{% data reusables.enterprise-accounts.emu-password-reset-session %}

{% endnote %}

1. [ID プロバイダーの構成](#configuring-your-identity-provider)
2. [エンタープライズの構成](#configuring-your-enterprise)
3. [プロビジョニングの有効化](#enabling-provisioning)

### ID プロバイダーの構成

IdP を構成するには、IdP で {% data variables.product.prodname_emu_idp_application %} アプリケーションを構成するための指示に従います。

1. {% data variables.product.prodname_emu_idp_application %} アプリケーションをインストールするには、以下の IdP のリンクをクリックします。

     - [Azure Active Directory の {% data variables.product.prodname_emu_idp_application %} アプリケーション](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/aad.githubenterprisemanageduser?tab=Overview)
     - [Okta の {% data variables.product.prodname_emu_idp_application %} アプリケーション](https://www.okta.com/integrations/github-enterprise-managed-user)

1. {% data variables.product.prodname_emu_idp_application %} アプリケーションと IdP を構成するには、以下のリンクをクリックし、IdP によって提供される指示に従います。

     - [{% data variables.product.prodname_emus %} の Azure Active Directory チュートリアル](https://docs.microsoft.com/en-us/azure/active-directory/saas-apps/github-enterprise-managed-user-tutorial)
     - [{% data variables.product.prodname_emus %} の Okta ドキュメント](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-GitHub-Enterprise-Managed-User.html)

1. そのため、エンタープライズをテストして構成し、自分自身または {% data variables.product.prodname_dotcom %} で SAML SSO を構成するユーザーを IdP 上の {% data variables.product.prodname_emu_idp_application %} アプリケーションに割り当てることができます。

1. {% data variables.product.prodname_dotcom %} でエンタープライズを引き続き構成できるようにするには、IdP にインストールしたアプリケーションから次の情報を見つけてメモします。

    | 値 | その他の名前 | 説明 |
    | :- | :- | :- |
    | IdP のサインオン URL | ログイン URL、IdP URL | IdP 上のアプリケーションの URL |
    | IdP 識別子 URL | 発行者 | SAML 認証用のサービス プロバイダーに対する IdP 識別子 |
    | 署名証明書 (Base64 エンコード) | 公開証明書 | IdP が認証要求に署名するために使用する公開証明書 |

### Enterprise を設定する

ID プロバイダーに {% data variables.product.prodname_emu_idp_application %} アプリケーションをインストールして構成した後、エンタープライズを構成できます。 

1. ユーザー名 **@<em>SHORT-CODE</em>_admin** を使用して、新しいエンタープライズのセットアップ ユーザーとして {% data variables.product.prodname_dotcom_the_website %} にサインインします。

{% data reusables.enterprise-accounts.access-enterprise %} {% data reusables.enterprise-accounts.settings-tab %} {% data reusables.enterprise-accounts.security-tab %}

1. [SAML シングル サインオン] で、 **[Require SAML authentication]\(SAML 認証が必要\)** を選択します。
  ![SAML SSO を有効化するためのチェックボックス](/assets/images/help/business-accounts/enable-saml-auth-enterprise.png)

1. **[サインオン URL]** に、IdP の構成時にメモしたシングル サインオン要求の IdP の HTTPS エンドポイントを入力します。
![メンバーがサインインする際にリダイレクトされる URL のフィールド](/assets/images/help/saml/saml_sign_on_url_business.png)

1. **[発行者]** に、IdP の構成時にメモした SAML 発行者 URL を入力して、送信されたメッセージの信頼性を確認します。
![SAML 発行者の名前のフィールド](/assets/images/help/saml/saml_issuer.png)

1. **[公開証明書]** で、IdP の構成時にメモした証明書を貼り付けて、SAML 応答を確認します。
![ID プロバイダーからの公開証明書のフィールド](/assets/images/help/saml/saml_public_certificate.png)

1. SAML 発行者からの要求のデータ整合性を確認するには、{% octicon "pencil" aria-label="The edit icon" %} をクリックします。 次に、[署名方法] および [Digest Method]\(ダイジェスト方法\) ドロップダウンで、SAML 発行者が使用するハッシュ アルゴリズムを選択します。
![SAML 発行者が使用する署名方法とダイジェスト方法のハッシュ アルゴリズム用のドロップダウン](/assets/images/help/saml/saml_hashing_method.png)

1. エンタープライズで SAML SSO を有効化する前に、 **[Test SAML configuration]\(SAML 構成のテスト\)** をクリックして、入力した情報が正しいか確認します。 ![適用する前に SAML 構成をテストするボタン](/assets/images/help/saml/saml_test.png)

1. **[保存]** をクリックします。

    {% note %}

    **注:** エンタープライズに SAML SSO が必要な場合、セットアップ ユーザーはエンタープライズにアクセスできなくなりますが、GitHub にはサインインしたままになります。 IdP によってプロビジョニングされた {% data variables.enterprise.prodname_managed_users %} のみがエンタープライズにアクセスできます。

    {% endnote %}

{% data reusables.enterprise-accounts.download-recovery-codes %}


### プロビジョニングの有効化

SAML SSO を有効にした後、プロビジョニングを有効にします。 詳細については、「[エンタープライズ マネージド ユーザーの SCIM プロビジョニングの構成](//admin/identity-and-access-management/managing-iam-with-enterprise-managed-users/configuring-scim-provisioning-for-enterprise-managed-users)」を参照してください。

