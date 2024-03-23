# Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados

### Índice

1. [Objetivos desse contéudo](#objetivos-desse-contéudo)
2. [O que é AI Search - Azure](#o-que-é-ai-search---azure)
3. [Criando um recurso do Azure AI Search](#como-configurar-sua-ai-search---azure)
4. [Criando um recurso de serviços da IA Azure](#criando-um-recurso-de-serviços-da-ia-azure)
5. [Criando uma conta de armazenamento](#criando-uma-conta-de-armazenamento)
6. [Carregando documentos para o armazenamento do Azure](#carregando-documentos-para-o-armazenamento-do-azure)
7. [Indexando os documentos](#indexando-os-documentos)
8. [Consultando o índice](#consultando-o-índice)
9. [Pesquisando todos os documentos](#pesquisando-todos-os-documentos)
10. [Pesquisando por localização](#pesquisando-por-localização)
11. [Pesquisando por sentimento](#pesquisando-por-sentimento)
12. [Revisando o armazenamento de conhecimento](#revisando-o-armazenamento-de-conhecimento)
13. [Visualizando em tabelas](#visualizando-em-tabelas)

### Objetivos desse contéudo

* Mostrar o passo a passo para configurar e utilizar o Azure AI Search;
* Completar o desafio proposto pelo BOOTCAMP da DIO sobre Azure.

### O que é AI Search - Azure

Uma plataforma de recuperação de informações que ajuda os desenvolvedores a criar experências de pesquisas avançadas, reduzindo a complexidade da ingestão de dados e da criação do índice de pesquisa por meio da integração com soluções de armazenamento do AZURE e APIs e SDKs RESTful simples.<br>
AI Search exibe as principais métricas de desempenho, tendências e relatórios para uso de AI Search em sua página principal. Sua página Consultas exibe informações adicionais sobre as consultas de pesquisa. Filtros interativos permitem que os analistas exibam a análise de desempenho para aplicações de pesquisa individuais e selecionem o intervalo de tempo para analisar.<br>
A Pesquisa de IA do Azure é uma funcionalidade importante nos aplicativos. A capacidade de localizar dados relevantes rapidamente é essencial para a experiência e os resultados do usuário final. O mecanismo de Pesquisa de IA do Azure usa a funcionalidade de IA que ajuda os aplicativos a trabalhar de maneira mais humana e fazer associações que vão além da mera correspondência de palavras-chave. Os zervices de IA do Azure podem ajudar seus usuários finais a encontrar o que precisam saber, mais rapidamente.

> **Saiba mais em:**
>
> * [Pesquisa do IA do AZURE](https://azure.microsoft.com/pt-br/products/ai-services/ai-search)
>* [O que é a IA do Azure Search?](https://learn.microsoft.com/pt-br/azure/cloud-adoption-framework/innovate/best-practices/cognitive-search)

## Como configurar sua AI Search - Azure

Você precisará ter uma conta no Azure (pode ser uma conta experimental por 30 dias) para seguir com esse laboratório.

### Criando um recurso do Azure AI Search

* acesse o [portal do Azure](https://portal.azure.com/)
* clique no botão **+ Criar um recurso** 
* Pesquise por Azure AI Search
* agora crie um recurso com as configurações abaixo

> **Assinatura**: Sua Assinatura Azure<br>
> **Grupo de recursos**: Selecione ou crie um grupo de recursos com um nome exclusivo.<br>
> **Nome do serviço**: Um nome exclusivo<br>
> **Localização**: Escolha qualquer localização disponível (lembrando que não é recomendado utilizar o Brazil devido os valores serem bem altos.)<br>
> **Nível de preço**: Básico

![resource_search](/img/resurce%20search.png)

* Selecione **Revisar + criar**
* Depois que aparecer a resposta de validação clique em **Criar**

### Criando um recurso de serviços da IA Azure
 Será necessário provisionar um recurso de **serviços de AI do Azure** que esteja no mesmo local do recurso criado anteriormente.

 * Retorno a página inicial do [portal do Azure](https://portal.azure.com/)
 * Clique no botão **+ criar um recurso**
 * Pesquise os serviços de AI do Azure
 * Selecione criar um plano de **Serviços do AI Azure**
 * Configure com as informações abaixo:

> **Assinatura**: Sua assinatura do Azure<br>
> **Grupo de recursos**: Selecione o mesmo grupo de recurso selecionado no Azure AI Search <br>
> **Região**: Selecione a mesma região selecionada no Azure AI Search<br>
> **Nome**: Coloque um nome exclusivo<br>
> **Nível de preços**: Padrão S0
> **Ao marcar essa caixa, confirmo que li e compreendi todos os termos abaixo**: Selecionado

![resource_search2](/img/resurce%20search2.png)

* Selecione **Revisar + criar**
* Validado clique em **Criar**

Aguarde a conclusão e visualize os detalhes da implatação.

### Criando uma conta de armazenamento

* Retorne novamente a página inicial do [portal do Azure](https://portal.azure.com/)
* Selecione o botão **+ Criar um recurso**
* Procure por conta de armazenamento
* Crie um recurso de conta de armazenamento com as informações abaixo:

> **Assinatura**: Sua assinatura do Azure<br>
> **Grupo de recursos**: O mesmo grupo de recurso utilizado na criação dos dois recursos anteriores.<br>
> **Nome da conta de armazenamento**: um nome exclusivo<br>
> **Localização**: Qualquer uma que esteja disponível<br>
Padrão **de desempenho**<br>
> **Redundância**: Armazenamento localmente redundante (LRS)

![resource_search2](/img/resurce%20search3.png)

* Clique em **Revisar + Criar** e depois **Criar**.
* Clique em ir para recurso
* No painel do menu esquerdo clique em configurações
* Depois clique com configuração
* Altere a configuração de *Permitir acesso anônimo de Blob* para **Habilitado** e salve.

![video](/gif/Configuration.gif)

> IMPORTANTE - **NÃO ESQUEÇA DE CLICAR EM SALVAR**

### Carregando documentos para o armazenamento do Azure

#### Proposta da documentação - [Link](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html)

Vamos imaginar que você trabalha para a Fourth Coffee, uma rede nacional de cafés. Você foi solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a busca de insights sobre as experiências dos clientes. Você decide criar um índice do Azure AI Search usando dados extraídos de avaliações de clientes.

Primeiro precisamos alimentar a nossa IA, então baixe as [avaliações de café compactadas](https://aka.ms/mslearn-coffee-reviews).

* Clique em **Containers** no painel a esquerda
* Selecione **+ Container** no painel que ficará a direita

![container](/img/container.png)

* Clique em criar após preencher com as informações abaixo:

> **Nome**: coffee-reviews<br>
> **Nível de acesso público**: Container (acesso de leitura anônimo para containers e blobs)<br>
> **Avançado**: sem alterações<br>

![new container](/img/newContainer.png)

* No portal do Azure, selecione o container de *"coffee-reviews"*
* Clique em carregar e faça o upload dos arquivos baixados

![upload](/img/upload.png)

* No painel **Carregar blob**
* Selecione **Selecionar um arquivo**
* Vá até a pasta onde consta o arquivo baixado
* Selecione todos os arquivo
* Clique em **abrir** e depois em **carregar**

![upload_video](/gif/upload.gif)

Agora você pode fechar o seu painel de **Carregar o Blob**!

### Indexando os documentos

Agora vamos utilizar a **Azure AI Search** para extrair *insights* dos documentos. Com o *Assistente de importação de dados*, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Vamos lá!

* Na página **Visão geral**
* Vá até o recurso da **Azure AI Search**

![indexar](/gif/index.gif)

* Depois selecione **Importar dados**
* Na lista de **Fonte de Dados**, selecione **Armazenamento de Blobs do Azure**
* Preencha os demais campos com os dados abaixo

> **Fonte de dados**: Armazenamento de Blobs do Azure<br>
> **Nome da fonte de dados**: coffee-customer-data<br>
> **Dados a extrair**: Conteúdo e metadados<br>
> **Modo de análise**: Padrão<br>
> **Cadeia de conexão**: Selecione Escolha uma conexão existente . Selecione sua conta de armazenamento, selecione o contêiner de avaliações de café e clique em Selecionar.<br>
> **Autenticação de identidade gerenciada**: Nenhuma<br>
> **Nome do contêiner**: esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente.<br>
> **Pasta Blob**: deixe em branco.<br>
> **Descrição**: Avaliações sobre Fourth Coffee Shops.<br>

![Import data](/img/import%20data.png)

* Selecione Próximo: **Adicionar habilidades cognitivas (opcional)**.
* Em **Anexar serviços cognitivos**, selecione o recurso de serviços Azure AI.
* Altere o nome da qualificação para *coffee-skillset*.
* Marque a caixa de seleção **Habilitar OCR e mesclar todo o texto no campo merged_content**
* Certifique-se de que o campo Dados de origem esteja configurado como *merged_content.*
* Altere o **nível de granularidade de enriquecimento** para **Páginas (blocos de 5.000 caracteres)**.
* Não selecione *Habilitar enriquecimento incremental*
* Selecione os compos de enriquecidos abaixo:
    - Extraia nomes de locais
    - Extraia frases-chave
    - Detectar sentimentos
    - Gerar tags de imagens
    - Gere legendas de imagns
* Já em **Salvar enriquecimentos em um armazenamento de conhecimento**, você irá selecionar:
    - Projeções de imagem
    - Documentos
    - Páginas
    - Frases Chave
    - Entidades
    - Detalhes da imagem
    - Referências de imagem
> NOTA: Se aparecer um erro em vermelho, siga o processo da imagem abaixo. 
![warning](/img/warning.png)
Você também pode consultar na [documentação](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html#index-the-documents).

Na próxima tela faça as seguintes configirações:

* Altere o nome do índice para: **coffee-index**
* A chave deve estar configurada como: **metadata_storage_path**
* O nome do sugeridor deixe em branco
* O modo de pesquisa será preenchido automaticamente, não faça alterações
* Selecione **Filtrável* para todos os itens que já estiverem pré-selecionados.
* Agora clique em **Próximo: Criar um indexador**

Será direcionado para a próxima tela, onde você fará as seguintes alterações:

* Mude o nome do indexador para **coffee-indexer**
* Programação definida como **Once**

Expanda as configurações avanças e vamos para mais algumas configurações - está acabando!! 

* Verifique se a opção **Base-64 Encode Keys** esteja selecionada.
* Selecione **Enviar**

O indexador é executado automaticamente e executa o pipeline de indexação, que:
 - Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
 - Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
 - Mapeia os campos extraídos para o índice.

 Agora volte para a página de recursos do Azure AI Search

 * Clique em **Gerenciamento de pesquisa**
 * Selecione **indexadores**
 * Selecione o **indexador de café**<br>
 Espere alguns minutos
 * Clique em **Atualizar** até o **status** indicar **sucesso**<br>
 Selecionando o nome do indexador você terá acesso a mais detalhes. Abaixo imagem dos detalhes apresentados no laboratório que executei:

 ![details](/img/coffee-indexer-details.png)

 ### Consultando o índice

  O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search Explorer para escrever consultas e revisar resultados em JSON.

 Bora lá!!

 #### Pesquisando todos os documentos

 * Volte para a página de **Visão geral**
 * Selecione **Explorador de pesquisa**
 * Altere a visualização para **JSON view**
 * Edite o código para:

```
{
    "search": "*",
    "count": true
}
```

Observe na figura abaixo que ele trará todas as informações contidas nos arquivos inseridos, no campo **@odata.count** exibe a contagem de documentos incluidos na pesquisa.<br>
Ali podemos abservar que ele nos trás o número 9, que foi o número de arquivos que importamos para alimentar nossa fonte de dados.

![datacount](/img/odata.count.png)

#### Pesquisando por localização

Substitua o código pelo informado abaixo e clique em pesquisar:

```
{
    "search": "locations:'Washington'",
    "count": true
}
```
Na documentação é utilizado "Chicago" Mas eu alterei para ter um resultado diferente, você pode substituir por outro nome se preferir.<br>
Dentro da pesquisa foram encontradas 4 opniões registradas em "Washington", que foi a localização que eu informei na pesquisa. Veja abaixo o resultado:

![locations](/img/odata.count2.png)

#### Pesquisando por sentimento

A Partir do código inserido irá filtrar as visões com o sentimento desejado. No código abaixo vamos filtrar os resultados positivos.

```
{
    "search": "sentiment:'positive'",
    "count": true
}
```
Na imagem abaixo podemos ver mais uma vez no item **@odata.count** o número de "comentários" positivos que o café recebeu.
![sentiment](/img/sentiment.png)

Para um melhor aproveitamento da ferramenta, você pode realizar a pesquisa em relação aos sentimentos "Negativos" e elaborar uma melhoria para não receber mais comentários desse tipo.

### Revisando o armazenamento de conhecimento

Quando importamos os arquivos criamos também um *armazenamento de conhecimento* e dentro dele você encontrará os dados enriquecidos extraídos pelas habilidades da IA.

* Volte para sua conta de armazenamento do Azure.
* Clique em **Containers** 
* Selecione o container de **armazenamento de conhecimento**

![Review](/img/Review.png)

* Selecione qualquer um dos itens
* depois clique no arquivo **objectprojection.json**

![object](/img/object.png)

* Depois clique em editar para ter acesso ao arquivo **JSON**

Depois de visualizado, volte para a tela de containers, vamos dar uma olhadinha nas imagens armazenadas.

* Na página de containers
* Clique em *coffee-skillset-image-projection*
* Selecione qualquer um dos arquivos .jpg
* Clique na aba **Editar** e verá a imagem armazenada no documento.

![image](/img/image.png)

#### Visualizando em tabelas

* Volte para a tela *conta de armazenamento Containers*
* Clique em **Navegador de armazenamento**
* Depois selecione **Tabelas**

![table](/img/Table.png)

Você verá que existe uma tabela para cada entidade no índice.

* Selecione *coffeeSkillsetKeyPhrases*

> Observe as frases-chave que o armazenamento de conhecimento conseguiu capturar do conteúdo das avaliações. Muitos dos campos são chaves, portanto você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.


