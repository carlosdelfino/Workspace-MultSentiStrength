# Como Montar o Projeto

Faça o clone deste repositório e tome conhecimento dos projetos envolvidos na construção do sofware.

Abra o Eclipse e faça um fork de cada projeto em um repositório privado, use as instruições a seguir caso não tenha um servidor privado para fazer o clone de cada módulo.

# Criando um repositório local Privado

- Crie um diretório onde irá aguardar os repositórios;
- Crie um diretório para cada módulo dentro desse novo dirório;
- Execute o comando a seguir para criar o repostório dentro de cada diretório para cada módulo.

      git init --bare

O comando acima irá inicializar um repositório vazio do tipo bare, veja a documentação do git par amais detalhes.

# Configurando cada Módulo.

O projeto SocialSLA é dividido em módulos, devido a natureza de pesquisa, o projeto sofre constantes ajustes e mudanças sem seus módulos, porém é facil perceber que sua modularização se divide nas seguintes partes mais improtantes:

 * Ponto de Entrada (Desktop no caso)
 * Camada de Persistencia (a camada de persistencia tem módulos relativos que depende diretamente e contribui com novos recursos mas são serviços de outros módulos
 * Serviços NLP (Serviços NLP são por exemplo o WEKA e este por sua vez tem serviços especializados como o WEKA-JPA que está relacionado diretamente com a camada de Persistencia)
 * Serviços WEKA - JPA (este serviço é um submódulo do módulo Serviços NLP, mais especificamente do módulo WEKA (NLP-WEKA) é responsável por atender o WEKA nas requisições relativas a camada de persiência, abstraindo do WEKA todos os códigos e depências necessárias)
 * Serviços SocialStream (Este serviços é responsável por definir o protoclo de comunicação com as redes sociais, abstraindo de toda a aplicação as depências e códigos necessários para obtenção de dados nas Redes Sociais)

 Os módulos são configurandos usando o Maven, portanto com a útilização da IDE Eclipse e o plugin adequado para integração com o Maven será todas as depênciais automáticamente ajustadas.

 Caso encontre dificuldades ai já é uma demanda importante para o projeto como facilitar e melhorar os scripts de construção dos projetos.

 Depois de criar seu fork crie um branch com seu nome e direcione-o para que seja feito o push diretamente no branch "master" do seu repositório privado, caso deseje criar um novo recurso faça um novo branch por exemplo "seunome_novorecurso" e configure o push para que este branch seja enviado para o branch do repositório privado como sendo "novorecurso" consulte o manual do git em caso de dúvidas ou solicite mais detalhes usando a seção Issue deste projeto

Ao terminar sua codificação gere um arquivo DIFF com relação ao branch do programador que deseja enviar, "delfino", "aminadabe" "carlosbarros" ou mesmo com relação ao branch "master", envie para o programador em questão e detalhe as alterações realizadas procure dar o máximo de detalhes como o ponto de inicio da codificação (quando o fizer procure informar aos programadores que inciou este novo trabalho, não deixe de manter sincronizado com eles tal situação.

O programador no qual for destinado o DIFF deverá criar um branch com o meesmo nome no qual está recebendo as alterações e deverá fazer finalmente o MERGE depois que tudo estiver testado e ajustado, se necessário deverá retornar um DIFF para o programador que propós a alteração para que este ajuste seu repositório.

Caso ambos os programadores tenham possibilidade de acessar o mesmo repositório privado ou o repositório individualmente de cdada um deverá parametrizar suas instalações para isso, então não irão precisar fazer a troca de arquivos DIFF, procurando apenas manter os Branchs conforme sugerido para que possam fazer os Merges.

Estes poderão negociar formas de se criar o Branch adaptando a sugestão acima, mas dexando bem claro o trabalho em conjunto.

# Dificuldades que precisam ser sanadas imediatamente

## Script de ATualização dos projetos
 O projeto hoje está com 17 módulos, alguns muito simples possuem apenas um arquivo pom.xml para parametrizar o Maven, um arquivo beans.xml para o CDI e uma classe, isso se faz necessário para manter as camadas o mais desacopladas possível das dependências e das demais camadas.

Cada projeto possui pelo menos dois branchs, o "master", branch principal, onde está o código final aprovado por todos, e um brach do programador com o seu nome, este branch é o branch de trabalho do programador e não deve ser enviado para os repositórios centrais, apenas para os privados, e preferncialmente o prvado não deve fazer referencia ao master do repositorio central a não ser por referencia remota "remote/github/master" ou "remote/gitbucket/master"

Portanto é preciso um script onde se facilite a montagem do projeto e sua atualização, ao se executar este script deverá ser informado o nome do programador que o executa e o nome do programador a que se deseja enviar ou receber atualizações, a ausência do nome deste programador fará com que o script use o repositório "BitBucket" podendo também ser informadoo repositorio GitHub como opção ou outro caso se deseja um terceiro (desnecessário).

## Politica de atualização das versões

Com o crescimento do projeto e a multiplicação dos módulos está sendo preciso definir um modelo de versionamento para os módulos e todo o projeto.

## Optimização do CDI

Hoje o CDI parece estar com um desempenho abaixo do ideal, as vezes demora muito a retornar uma instancia e principalmente para inicializar.

É preciso ajustar principalmente a carga das classes durante os processos.

## Optimização da Camada e Persistência.

É preciso rever todos os processos e se preciso criar classes de serviços que encapsule os processos removendo-os de dentro dos controllers, em especial da camada GUI (Controllers dos Viewers no JavaFX).

Há algumas consultas que entram em uma recursividade chamando a mesma consulta diversas vezes antes de voltar, isso é preciso ser corrigido urgentemente.

Veja nos Issues tanto do repositório "Workspace" como "Persistencia" se não algo relativo aberto e consolide estes Issues em um único que será relativo a Optimização da Persistência.

## Melhoria do Design e Responsividade da Aplicação

Mais importante queo design é a questão de Responsividade e interação com o usuário. É preciso adicioanr a aplicação um serviço de Log mais elaborado e especifico integrado ao que usamos hoje baseado no SLF4J, e também adicionar no rodapé das telas na camada Gui, uma barra que informe o status das tarefas que estão sendo executadas.

Icones especiais, e melhoria do visual é muito importante principalmente dando uma visão mais moderna para a aplicação.