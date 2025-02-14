---
title: Exibir e atualizar dependências vulneráveis no repositório
intro: 'Se o {% data variables.product.product_name %} descobrir dependências vulneráveis no seu projeto, você poderá visualizá-las na aba de alertas do Dependabot no seu repositório. Em seguida, você pode atualizar seu projeto para resolver ou descartar a vulnerabilidade.'
redirect_from:
  - /articles/viewing-and-updating-vulnerable-dependencies-in-your-repository
  - /github/managing-security-vulnerabilities/viewing-and-updating-vulnerable-dependencies-in-your-repository
  - /code-security/supply-chain-security/viewing-and-updating-vulnerable-dependencies-in-your-repository
permissions: Repository administrators and organization owners can view and update dependencies.
shortTitle: Visualizar as dependências vulneráveis
versions:
  fpt: '*'
  ghes: '*'
  ghae: issue-4864
  ghec: '*'
type: how_to
topics:
  - Dependabot
  - Security updates
  - Alerts
  - Dependencies
  - Pull requests
  - Repositories
---

{% data reusables.dependabot.beta-security-and-version-updates %}
{% data reusables.dependabot.enterprise-enable-dependabot %}

Your repository's {% data variables.product.prodname_dependabot_alerts %} tab lists all open and closed {% data variables.product.prodname_dependabot_alerts %}{% ifversion fpt or ghec or ghes > 3.2 %} and corresponding {% data variables.product.prodname_dependabot_security_updates %}{% endif %}. You can{% ifversion fpt or ghec or ghes > 3.4 or ghae-issue-5638 %} filter alerts by package, ecosystem, or manifest. You can also{% endif %} sort the list of alerts, and you can click into specific alerts for more details. Para obter mais informações, consulte "[Sobre alertas para dependências vulneráveis](/code-security/supply-chain-security/about-alerts-for-vulnerable-dependencies)"

{% ifversion fpt or ghec or ghes > 3.2 %}
É possível habilitar atualizações de segurança automáticas para qualquer repositório que usa o {% data variables.product.prodname_dependabot_alerts %} e o gráfico de dependências. Para obter mais informações, consulte "[Sobre {% data variables.product.prodname_dependabot_security_updates %}](/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/about-dependabot-security-updates)."
{% endif %}

{% data reusables.repositories.dependency-review %}

{% ifversion fpt or ghec or ghes > 3.2 %}
## Sobre atualizações para dependências vulneráveis no seu repositório

{% data variables.product.product_name %} gera {% data variables.product.prodname_dependabot_alerts %} quando detectamos que sua base de código está usando dependências com vulnerabilidades conhecidas. Para repositórios em que {% data variables.product.prodname_dependabot_security_updates %} estão habilitados, quando {% data variables.product.product_name %} detecta uma dependência vulnerável no branch padrão, {% data variables.product.prodname_dependabot %} cria um pull request para corrigi-la. O pull request irá atualizar a dependência para a versão minimamente segura possível, o que é necessário para evitar a vulnerabilidade.

{% ifversion fpt or ghec or ghes > 3.4 or ghae-issue-5638 %}You can sort and filter {% data variables.product.prodname_dependabot_alerts %} with the dropdown menus in the {% data variables.product.prodname_dependabot_alerts %} tab or by typing filters as `key:value` pairs into the search bar. The available filters are repository (for example, `repo:my-repository`), package (for example, `package:django`), ecosystem (for example, `ecosystem:npm`), manifest (for example, `manifest:webwolf/pom.xml`), state (for example, `is:open`), and whether an advisory has a patch (for example, `has: patch`).

Each {% data variables.product.prodname_dependabot %} alert has a unique numeric identifier and the {% data variables.product.prodname_dependabot_alerts %} tab lists an alert for every detected vulnerability. Legacy {% data variables.product.prodname_dependabot_alerts %} grouped vulnerabilities by dependency and generated a single alert per dependency. If you navigate to a legacy {% data variables.product.prodname_dependabot %} alert, you will be redirected to a {% data variables.product.prodname_dependabot_alerts %} tab filtered for that package. {% endif %}
{% endif %}

## Visualizar e atualizar dependências vulneráveis

{% ifversion fpt or ghec or ghes > 3.4 or ghae-issue-5638 %}
{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-security %}
{% data reusables.repositories.sidebar-dependabot-alerts %}
1. Optionally, to filter alerts, select the **Repository**, **Package**, **Ecosystem**, or **Manifest** dropdown menu then click the filter that you would like to apply. You can also type filters into the search bar. For example, `ecosystem:npm` or `has:patch`. To sort alerts, select the **Sort** dropdown menu then click the option that you would like to sort by. ![Screenshot of the filter and sort menus in the {% data variables.product.prodname_dependabot_alerts %} tab](/assets/images/help/graphs/dependabot-alerts-filters.png)
1. Click the alert that you would like to view. ![Alerta selecionado na lista de alertas](/assets/images/help/graphs/click-alert-in-alerts-list-ungrouped.png)
1. Revise as informações da vulnerabilidade e, se disponível, o pull request que contém a atualização de segurança automatizada.
1. Opcionalmente, se ainda não houver uma atualização de {% data variables.product.prodname_dependabot_security_updates %} para o alerta, crie um pull request para resolver a vulnerabilidade. Clique em **Criar uma atualização de segurança de {% data variables.product.prodname_dependabot %}**. ![Crie um botão de atualização de segurança do {% data variables.product.prodname_dependabot %}](/assets/images/help/repository/create-dependabot-security-update-button-ungrouped.png)
1. Quando estiver pronto para atualizar a dependência e resolver a vulnerabilidade, faça merge da pull request. Cada pull request criado por {% data variables.product.prodname_dependabot %} inclui informações sobre os comandos que você pode usar para controlar {% data variables.product.prodname_dependabot %}. Para obter mais informações, consulte "[Gerenciar pull requests para atualizações de dependências](/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/managing-pull-requests-for-dependency-updates#managing-dependabot-pull-requests-with-comment-commands)".
1. Opcionalmente, se o alerta estiver sendo corrigido, se estiver incorreto, ou localizado em um código não utilizado, selecione o menu suspenso "Ignorar" e clique em um motivo para ignorar o alerta. ![Escolher o motivo para ignorar o alerta a partir do menu suspenso "Ignorar"down](/assets/images/help/repository/dependabot-alert-dismiss-drop-down-ungrouped.png)

{% elsif ghes = 3.3 %}
{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-security %}
{% data reusables.repositories.sidebar-dependabot-alerts %}
1. Clique no alerta que deseja exibir. ![Alerta selecionado na lista de alertas](/assets/images/help/graphs/click-alert-in-alerts-list.png)
1. Revise as informações da vulnerabilidade e, se disponível, o pull request que contém a atualização de segurança automatizada.
1. Opcionalmente, se ainda não houver uma atualização de {% data variables.product.prodname_dependabot_security_updates %} para o alerta, crie um pull request para resolver a vulnerabilidade. Clique em **Criar uma atualização de segurança de {% data variables.product.prodname_dependabot %}**. ![Crie um botão de atualização de segurança do {% data variables.product.prodname_dependabot %}](/assets/images/help/repository/create-dependabot-security-update-button.png)
1. Quando estiver pronto para atualizar a dependência e resolver a vulnerabilidade, faça merge da pull request. Cada pull request criado por {% data variables.product.prodname_dependabot %} inclui informações sobre os comandos que você pode usar para controlar {% data variables.product.prodname_dependabot %}. Para obter mais informações, consulte "[Gerenciar pull requests para atualizações de dependências](/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/managing-pull-requests-for-dependency-updates#managing-dependabot-pull-requests-with-comment-commands)".
1. Opcionalmente, se o alerta estiver sendo corrigido, se estiver incorreto, ou localizado em um código não utilizado, selecione o menu suspenso "Ignorar" e clique em um motivo para ignorar o alerta. ![Escolher o motivo para ignorar o alerta a partir do menu suspenso "Ignorar"down](/assets/images/help/repository/dependabot-alert-dismiss-drop-down.png)

{% elsif ghes = 3.1 or ghes = 3.2 or ghae-issue-4864 %}
{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-security %}
{% data reusables.repositories.sidebar-dependabot-alerts %}
1. Clique no alerta que deseja exibir. ![Alerta selecionado na lista de alertas](/assets/images/enterprise/graphs/click-alert-in-alerts-list.png)
1. Revise os detalhes da vulnerabilidade e determine se você precisa atualizar a dependência.
1. Ao fazer merge de um pull request que atualiza o manifesto ou arquivo de bloqueio para uma versão segura da dependência, isso resolverá o alerta. Como alternativa, se você decidir não atualizar a dependência, selecione a lista suspensa **Ignorar** e clique em um motivo para ignorar o alerta. ![Escolher o motivo para ignorar o alerta a partir do menu suspenso "Ignorar"down](/assets/images/enterprise/repository/dependabot-alert-dismiss-drop-down.png)

{% else %}
{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.accessing-repository-graphs %}
{% data reusables.repositories.click-dependency-graph %}
1. Clique no número da versão da dependência vulnerável para exibir informações detalhadas. ![Informações detalhadas sobre a dependência vulnerável](/assets/images/enterprise/3.0/dependabot-alert-info.png)
1. Revise os detalhes da vulnerabilidade e determine se você precisa atualizar a dependência. Ao fazer merge de um pull request que atualiza o manifesto ou arquivo de bloqueio para uma versão segura da dependência, isso resolverá o alerta.
1. O banner na parte superior da aba **Dependências** é exibido até que todas as dependências vulneráveis sejam resolvidas ou até que você o ignore. Clique em **Ignorar** no canto superior direito do banner e selecione uma razão para ignorar o alerta. ![Ignorar banner de segurança](/assets/images/enterprise/3.0/dependabot-alert-dismiss.png)
{% endif %}

## Leia mais

- "[Sobre alertas para dependências vulneráveis](/code-security/supply-chain-security/about-alerts-for-vulnerable-dependencies)"{% ifversion fpt or ghec or ghes > 3.2 %}
- "[Configurar {% data variables.product.prodname_dependabot_security_updates %}](/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/configuring-dependabot-security-updates)"{% endif %}
- "[Gerenciar as configurações de segurança e análise para o seu repositório](/github/administering-a-repository/managing-security-and-analysis-settings-for-your-repository)"
- "[Solução de problemas na detecção de dependências vulneráveis](/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/troubleshooting-the-detection-of-vulnerable-dependencies)"{% ifversion fpt or ghec or ghes > 3.2 %}
- "[Solucionar problemas de {% data variables.product.prodname_dependabot %}](/github/managing-security-vulnerabilities/troubleshooting-dependabot-errors)"{% endif %}
