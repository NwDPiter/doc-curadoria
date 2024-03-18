# O que é github actions?
    
É uma plataforma do gituhub que faz integração contínua e entrega contínua (CI/CD) que permite automatizar tarefas, build, teste e implantação. 

## Intuito da criação

Fazer um protótico no qual demonstrasse como funcionaria uma automatização para envio dos arquivos da aplicação para um servido externo. 

### Preparando ambiente 

Suponde que você já esteja no espaço de código do github, crie dois diretório.

    .github/workflows

e dentro de **/workflows** crie um arquivo chamado **main.yml**, assim:

![Ambiente](/Fotos-github-ations/workflows.png)

**OBS:** A linguagem usada e Yaml que tem a dinâmica de chave e valor. 

### Agora vamos instalar as dependências 

Primeiro vamos criar o arquivo de configuração

    npm init -y

Vai gerar um arquivo chamdo 
    
    package.json

Foi utilizado os seguites módulos:

* **Express:** Para subir uma aplicação

* **Jest:** Para testar a aplicação

A instalação foi feita usando o npm:

    npm install express jest


## Etapa 1 (Iniciando workflow)

Agora que temos nosso ambiente, vamos editar nosso arquivo **main.yml**.

![Etapa 1](/Fotos-github-ations/Nome-Branche.png)

**Linha 1:** _Escolhemos o nome do que sera feito nessa automatização._ 

**Linha 3,4:** _Ativamos o opção de que ao realizar um push na branche "main" o script será ativo._

## Etapa 2 (Criando jobs)

Nessa etapa vamos escolher uma vm que o github vai disponibilizar para testarmos nossa aplicação.

![jobs](/Fotos-github-ations/jobs-staps.png)

**Linha 8,9,10:** _Define um trabalho chamado teste-build-deploy no qual escolhe a ultima versão do ubuntu para fazer o teste._

**Linha 12,13,14:** _Começa a criação das etapas do que vai acontecer nesse script como o nome "Checkout code com uma ação que vai clonar o reposutório para o vm ubuntu"_

## Etapa 3 (Estruturando os testes)

Agora faremos o teste unitário para garantir que nosso código está realmente funcionado.

![teste-unitário](/Fotos-github-ations/teste-unitário.png)

**Linhas 18,19,20,21:** _Descreve o nome da ação o tipo de ação e sua versão, nesse caso será feito a instalação do node da versão escolhida na vm._

**Linhas 23,24:** _Após informar o nome da ação será feito a instala as dependências utilizando o npm._

**Linha 26,27:** _Após Informar o nome executamos com o npm um script chamado "test" que foi feito especificamente para o teste da aplicação._

## Etapa 4 (Configurando script)

Esse script deve ser especificado no arquivo "package.json" na sessão de script

![script](/Fotos-github-ations/script.png)

**Linha 7:** _Nomeamos o nosso script de teste como "test" e informamos o caminho que ele está._

**Linha 8:** _Nesse caso por ser apenas um protótipo caso tenha um codigo antigo será convertino para o mais recente._   

## Etapa 5 (Build)

Nessa etapa ocorrerar o build.

![build](/Fotos-github-ations/build.png)

**Linha 31,32:** _Depois de inserir o nome utilizamos o npm para rodar o script de build._


## Etapa 6 (Deploy)

Para finalinzar, vamos enviar para o servidor de destino, nesse caso estavamos usando a vm da azure, por isso os métodos e voltado para essa plataforma.

![deploy](/Fotos-github-ations/deploy.png)

**Linha 36,36:** _Informamos o nome da etapa e escolhemos a ação_

**Linha 39,40,41,42,43,44:** _São os parametros que vamos usar para enviar para o destino_

* **host:** "Ip do servidor"

* **username:** "Nome do usuário de login"

* **key:** "Chave privada"

* **port:** "Porta utilizada para envio"

* **source:** "Local que está armazenado seu arquivos"

* **target:** "Onde os arquivos serão salvo na vm"

OBS: Esses ${{ secrets.**** }} e uma forma de segurança do github na qual e informado nas configurações as variáveis mais sensíveis para não ser mostradas de fato.
