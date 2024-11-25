<h1 align="center" style="font-weight: bold;">Encurtador de URL Serverless com AWS 💻</h1>

<p align="center">
 <a href="#sobre">Descrição do Projeto</a> •
 <a href="#tecnologias">Tecnologias</a> • 
 <a href="#endpoints">Funcionalidades</a> •
 <a href="#anotacoes">Anotações</a>
</p>

<h2 id="sobre">Sobre o projeto</h2>
<h3>Este projeto é um sistema de encurtamento de URL utilizando a infraestrutura serverless da AWS.   
  
O objetivo é permitir que os usuários criem URLs curtas que redirecionem para URLs originais, com um tempo de expiração configurável.   </h3>
O sistema é composto por duas funções Lambda:   

Função de Criação de URL: Responsável por gerar e armazenar os links encurtados em um bucket S3, junto com informações como a URL original e o tempo de expiração.   

Função de Redirecionamento: Gerencia o redirecionamento, verificando o código da URL curta e validando se a URL ainda está dentro do prazo de expiração antes de redirecionar o usuário.</h3>

<h2 id="tecnologias">🛠 Tecnologias</h2>
<ul>
  <li>Java: Linguagem de programação utilizada para desenvolver as funções Lambda.</li>
  <li>AWS Lambda: Serviço de computação serverless da AWS utilizado para executar as funções de criação e redirecionamento de URLs.</li>
  <li>AWS S3: Serviço de armazenamento da AWS utilizado para armazenar os dados das URLs encurtadas.</li>
  <li>API Gateway: Serviço da AWS utilizado para expor as funções Lambda como APIs RESTful.</li>
</ul>

<h2 id="endpoints">🗃Funcionalidades</h2>

<p>Função de Criação de URL</p>
<ul>
  <li>Gera um código único para a URL curta</li>
  <li>Armazena a URL original e o tempo de expiração no bucket S3</li>
  <li>Retorna o código da URL curta para o usuário</li>
</ul>

<p> Função de Redirecionamento</p>
<ul>
  <li>Recebe o código da URL curta</li>
  <li>Verifica se a URL ainda está dentro do prazo de expiração</li>
  <li>Redireciona o usuário para a URL original se a URL não estiver expirada</li>
  <li>Retorna um erro se a URL estiver expirada</li>
</ul>


### Componentes Principais

#### Função CreateUrlLambda
<li>Main.java: Contém a lógica para gerar o código da URL curta, criar o objeto UrlData e armazená-lo no S3.    </li>

<li>UrlData.java: Classe que representa os dados da URL, incluindo a URL original, o código da URL curta e o tempo de expiração.    </li>

#### Função RedirectUrlShortener
<li>Main.java: Contém a lógica para recuperar o objeto UrlData do S3, verificar a expiração e redirecionar o usuário.    </li>

<li>UrlData.java: Classe que representa os dados da URL, incluindo a URL original, o código da URL curta e o tempo de expiração.     </li>

#### Integração com AWS
<li>AWS Lambda: Utilizado para executar as funções de criação e redirecionamento de URLs.    </li>

<li>AWS S3: Utilizado para armazenar os dados das URLs encurtadas.    </li>

<li>API Gateway: Utilizado para expor as funções Lambda como APIs RESTful, permitindo que os usuários interajam com o sistema.</li>


<h2 id="anotacoes">📝 Anotações Gerais sobre o Projeto e Fluxo de Dados</h2>


### O projeto é dividido em duas funções principais, cada uma com seu próprio diretório e código fonte:
<ul>
  <li><a href=https://github.com/manuverso/encurtador-createURL>CreateUrlLambda</a>: Responsável pela criação e armazenamento das URLs encurtadas</li>
  <li>RedirectUrlShortener: Responsável pelo redirecionamento das URLs encurtadas</li>
</ul>


### Fluxo de Dados
#### Criação de URL Curta
Entrada: O usuário envia uma solicitação para criar uma URL curta, fornecendo a URL original e o tempo de expiração desejado.
<ul>
  <li>A função CreateUrlLambda gera um código único para a URL curta</li>
  <li>Cria um objeto UrlData contendo a URL original, o código da URL curta e o tempo de expiração.</li>
  <li>Armazena o objeto UrlData em um bucket S3</li>
  <li>Saída: A função retorna o código da URL curta para o usuário</li>
</ul>


#### Redirecionamento de URL Curta
Entrada: O usuário acessa a URL curta.
<ul>
  <li>A função RedirectUrlShortener recebe o código da URL curta.</li>
  <li>Recupera o objeto UrlData correspondente do bucket S3.</li>
  <li>Se a URL não estiver expirada, redireciona o usuário para a URL original</li>
  <li>Se a URL estiver expirada, retorna um erro indicando que a URL não é mais válida</li>
  <li>Saída: Redirecionamento para a URL original ou mensagem de erro</li>
</ul>

### Integração com AWS   

AWS Lambda: Utilizado para executar as funções de criação e redirecionamento de URLs.   

AWS S3: Utilizado para armazenar os dados das URLs encurtadas.   

API Gateway: Utilizado para expor as funções Lambda como APIs RESTful, permitindo que os usuários interajam com o sistema.


### Escalabilidade
Serverless: A utilização de AWS Lambda e S3 permite que o sistema escale automaticamente com a demanda, sem a necessidade de gerenciamento de servidores

