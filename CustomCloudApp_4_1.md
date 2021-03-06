# OAuth 2.0 (three-legged) 認証タイプを使うクラウド・アプリケーション・インスタンスの作成

クラウド・アプリケーション・インスタンスを作成する際に、OAuth 2.0（three-legged）認証タイプを使用するように設定できます。

## OAuth 2.0（three-legged）認証を使用するための準備

クラウド・アプリケーションから必要な情報を取得するには、そのクラウド・アプリケーションで利用する開発者アカウントを作成します。アカウントを作成すると、クラウド・アプリケーション・インスタンスを作成するために必要な情報が送信されます。

- 目的のクラウド・アプリケーションを使ってSSIをアプリケーションとして登録します。
- クライアントIDとシークレットを入手します。
- 有効な認証コールバックおよびリダイレクトURIを取得します。

クラウド・アプリケーションから収集した情報を使って、エンドユーザーが使用するアクセス許可ダイアログを作成します。下図は、ユーザーに表示されるイメージを表しています。

  ![third-partylogin1](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/third-partylogin1.png)

詳細は、[Preparing to Create a Cloud App Definition and Instance](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/preparing-create-cloud-app-definition-and-instance.html)をご覧ください。

  1. ダッシュボードのクラウド・アプリケーション・インスタンスのタブで、 **新規クラウド・アプリケーション・インスタンスの作成** をクリック
  2. 新規クラウド・アプリケーション・インスタンスの画面で、**クラウド・アプリケーション定義の選択**をクリックすると、クラウド・アプリケーション定義の選択画面が開く

        ![selectcloudappdef](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/selectcloudappdef.png)

  3. カスタムビルドの定義もしくはOracleが作成した定義を選択すると、クラウド・アプリケーション定義が新規クラウド・アプリケーション・インスタンスエディタで開く

        ![newclouappinstance](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/newclouappinstance.png)

  4. クラウド・アプリケーション・インスタンスの表示名を指定。この名前がクラウド・アプリケーションカタログに表示される。
  5. 必要であれば、クラウド・アプリケーション・インスタンスにベースURLを追加する。ここで追加したベースURLはクラウド・アプリケーション定義のベースURLをオーバーライドする。
  6. 認証タイプでは、**OAuth 2.0 (three-legged)**をクリックする。**OAuth 2.0 (three-legged)**認証タイプの設定画面が開く。

        ![3-leggedoauthnourl](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/3-leggedoauthnourl.png)

  7. **クライアントID** と **クライアントシークレット** を指定する。この情報は利用するクラウド・アプリケーションの開発者アカウントに基づく。
  8. **リダイレクトURI** をコピーするため、 **クリップボードにコピー(Copy to Clipboard)** をクリック

        ![copyuriinstancenourl](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/copyuriinstancenourl.png)

  9. ベースURLを指定
  10. **スコープ**はオプション。説明を入力する場合、構文はカンマ区切りで<i>category:action</i>を並べる。
  11. Grant Typeとして **認可コード(authorization_code)** もしくは **カスタム(custom)** を選択する。
        - authorization_codeの場合
            <ol type="a">
            <li>認可セクションのパスにURLを設定</li>
            <li>必要であれば、 <b>ベースURLのオーバーライド</b> にURLを設定</li>
            <img src="https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/authorizetoken.png"/>
            <li>トークン取得セクションのパスにURLを設定</li>
            <li>必要であれば、 <b>ベースURL上書き</b> にURLを設定</li>
            <img src="https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/gettoken1.png"/>
            <li>必要であれば、追加情報を設定</li>
            </ol>
        - customの場合

            必要にあわせて、 **カスタムグラントタイプ** を作成する。カスタムグラントタイプではユーザー名とパスワードが必要で、```URI```は以下のような形式でなければならない。
            ```URL
            https://login2.responsys.net/rest/api/v1.1/auth/token
            ```

  12. **リフレッシュ(Refresh)**を指定することも可能（オプション）。
  13. **クライアント認証にヘッダーではなく本体を使用**を使い、クライアント認証のためにヘッダではなくメッセージ本体を使うことも可能（オプション）
  14. **アクセストークンのカスタマイズ**を使うと、アクセストークンをカスタマイズ可能（オプション）
        - **トークンパラメータ名** : authorization
        - **場所** : queryもしくはheaders
  15. 対象タイプ(Include Type)を選択することも可能（オプション）

        ![optionalfields](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/optionalfields.png)

  16. **API Key**を選択することも可能（オプション）
        <ol type="a">
        <li>名前を指定</li>
        <li>場所を設定</li>
        <li><b>各ユーザーが値を設定(Each user will provide a value)</b>か、<b>すべてのユーザー用に指定済(Authorize a single Shared Account for all users)</b>を選択</li>
        </ol>
  17. **クラウド・アプリケーションアカウント**を選択
        - **ユーザーが独自のアカウントを作成** : デフォルト
        - **すべてのユーザー用に単一の共有アカウントを認可**
  18. ページの最上部までスクロールして **Create（作成）** をクリック

構成が完了すると、新しいクラウド・アプリケーション・インスタンスがクラウド・アプリケーション・インスタンスに表示され、**アクティブ化**されていることがわかります。何かエラーがある場合は、**下書き**のままです。

![newinstancecatalog](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/newinstancecatalog.png)
