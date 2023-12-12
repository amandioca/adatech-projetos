<p align="center">
    <img src="https://i.imgur.com/LTnwRR7.jpg" alt="Header AdaTech e Potência Tech - iFood">
</p>

# Projeto Ada: Sistemas Operacionais Linux

Baseado em todo o conhecimento adquirido durante o módulo, realize as práticas sugeridas e em seguida, documente todo o processo realizado usando _printscreens_ sempre que possível.

**Assuntos que abordados:**
-   Gestão de usuários
-   Permissionamento
-   Configuração de Serviços

## Problema  1

Imagine que a Vanessa é uma administradora de sistemas em uma empresa de tecnologia. Ela recebeu a tarefa de criar uma nova conta de usuário para um novo membro da equipe. Vanessa precisa demonstrar seu conhecimento ao explicar o processo para seus colegas de trabalho.

Descreva o processo para criar um novo usuário no Linux, incluindo os comandos e opções utilizadas de forma mais detalhada possível.

### Resposta:

 **1.** Antes de mais nada, é necessário **abrir o terminal**. É possível fazer isso usando o atalho `Ctrl + Alt + T`.

![q1-image1](https://imgur.com/xyNbKzf.png)

**2.**  No terminal, o primeiro passo é incluir o seguinte comando, **substituindo *“nome-usuario”* pelo nome do usuário a ser criado** e teclar *Enter*.

``` linux
sudo adduser nome-usuario
```

 - O comando `sudo` (*superuser do*) é necessário para que você garanta os privilégios de superusuário (*root* ou *admin*). Observe o que acontece quando os privilégios não estão garantidos:

![q1-image2](https://imgur.com/Vogtkhn.png)

**3.**  Nesse momento, se a senha do usuário atual for solicitada, informe-a e tecle *Enter*.
Prossiga com a criação e confirmação da senha do novo usuário:

![q1-image3](https://imgur.com/0n2ttzC.png)

Opcionalmente, adicione mais dados ao usuário: 
    
![q1-image4](https://imgur.com/fxSztqH.png)

**4.** Se precisar alterar algum campo, tecle "**N**". Caso contrário, tecle "**S**" para efetivar criação e finalizar. 

![q1-image5](https://imgur.com/9ZOUc10.png)

**5.** Verifique a criação do usuário utilizando comando `cat` (_concatenate_) para exibir o conteúdo do arquivo: 

``` linux
cat /etc/passwd
```
![q1-image6](https://imgur.com/GwfI93Z.png)

Como alternativa, você pode validar a criação fazendo _login_ com o novo usuário utilizando o comando `su` (_substitute user_) seguido do nome do usuário:	

![q1-image7](https://imgur.com/weImjE9.png)

## Problema  2

Em uma pequena cidade chamada Linuxville, vive o Lucas, um entusiasta de tecnologia. Ele está ajudando seu amigo Rafael a entender o funcionamento das permissões de arquivo no sistema Linux. Lucas decide contar uma história, explicando que os arquivos em Linux são como valiosos tesouros guardados em cofres. Cada cofre possui uma combinação única de permissões, representadas por símbolos especiais. Lucas usa essa analogia para explicar como as permissões de arquivo são representadas e qual o acesso que cada símbolo representa. 

Crie uma Pasta qualquer e 5 arquivos de texto. Em seguida define as permissões 400 para a pasta e todos os arquivos recursivamente. Use esse exemplo para explicar o que são as permissões de arquivo no Linux e como elas são representadas de forma mais detalhada possível. 

### Resposta:
1. **Cofre:**

No terminal, utilize o comando `mkdir` (*make directory*) para criar uma nova pasta, seguido pelo nome da pasta a ser criada. 
Logo após, utilize o comando `cd` (*change directory*) seguido pelo nome da pasta para poder acessá-la. 

![q2-image1](https://imgur.com/7FPd5M9.png)

2. **Tesouro:**

Utilize o comando `touch` para criar novos arquivos dentro do diretório atual. Em seguida do comando deve ser informado o título e extensão de cada arquivo, com um espaço entre cada um deles para fazer a separação. 
 
![q2-image2](https://imgur.com/Lrbwrll.png)

3. **Símbolo especial:** 

Primeiramente, use o comando `cd ..` para retornar um nível de pasta e permitir que a pasta a ser configurada seja encontrada. 

Agora, para fazer o controle de permissão na pasta e arquivos de forma recursiva, utilize comando `chmod` (*change mode*) juntamente com a opção `-R` (*recursive*), seguidos pela notação numérica e nome da pasta, respectivamente: 

![q2-image3](https://imgur.com/Up9E7ue.png)

O exemplo de notação numérica “400” significa que apenas o proprietário possui a permissão única de leitura. 

***⚠️ Para entender melhor sobre notação numérica, siga para o próximo tópico (4).***

Verifique as permissões utilizando o comando e opção `ls -l`, como a seguir: 

![q2-image4](https://imgur.com/01Qu5rv.png)

4. **Notação Numérica:**

A notação numérica é composta por um conjunto de três números. Cada algarismo representa permissões específicas:  

- O primeiro algarismo representa o proprietário.  
- O segundo algarismo representa o grupo ao qual o arquivo pertence.  
- O terceiro algarismo representa outros usuários. 

Esses algarismos são o resultado da soma de permissões individuais: 

- 4 = Read (r) 
- 2 = Write (w) 
- 1 = Execute (x) 

Logo, o exemplo “755” significa que o proprietário tem todos os acessos (4+2+1) e os demais possuem acesso de escrita e execução (4+1). De uma forma mais ilustrativa: 

|             |  Proprietário  |     Grupos    |  Outros Usuários  |
|------------:|:--------------:|:-------------:|:-----------------:|
|**Read** 	  |        4       |       4       |          4        |
|**Write** 	  |        2       |       0       |          0        |
|**Execute**  |        1       |       1       |          1        |
|***Total da Soma:*** |        7       |       5       |          5        |

## Problema  3

Em uma cidade futurística chamada Adalandia, existe uma equipe de jovens DevOps liderada pela Andreza. Eles estão trabalhando em um novo projeto e precisam configurar um servidor web para hospedar sua aplicação. Andreza, como líder do time, guia seus colegas pelo processo de instalação e configuração do servidor Nginx, compartilhando suas experiências passadas com a ferramenta e fornecendo orientações detalhadas para garantir uma configuração correta. 

Descreva o processo para instalar e configurar o servidor Web Nginx no Linux. O Objetivo é alterar a página Default do Nginx para os seguintes caracteres: 

`` ADA + AdaTech + seu_nome = Sucesso! ``

Apenas esse texto deve ser renderizado na página padrão do servidor. Não esqueça de tirar um print e documentar tudo que foi feito até chegar a esse resultado. 

> Orientação do professor: considerar Apache no lugar de Nginx. 

### Resposta:

1. **Instalando o Apache:**

Para instalar o Apache, será utilizado o gerenciador de pacotes e dependências "**APT**" (_Advanced Package Tool_).  

Para realizar a instalação, insira o seguinte comando no terminal Linux: 

``` linux
sudo apt-get install apache2 
```

O `sudo` servirá para garantir os privilégios de superusuário; `apt-get install` servirá para fazer a instalação do pacote ou dependência no gerenciador APT; `apache2` é o pacote a ser instalado, onde o “2” representa a versão que será adquirida. 

Se neste momento a senha for solicitada, informe-a e tecle _Enter_.	 

![q3-image1](https://imgur.com/07AWs7x.png)

Quando essa mensagem aparecer, tecle "**S**" e _Enter_ para confirmar a instalação: 

![q3-image2](https://imgur.com/3roj5wj.png)

Utilize o comando `systemctl` (_system control_) para verificar o status do `apache2`. O retorno deverá ser algo como: 

![q3-image3](https://imgur.com/Qfboc1l.png)

Tecle “**q**” (_quit_) para sair.

Caso seja necessário, substitua o comando de unidade “**status**” pelo “**restart**” para iniciar ou reiniciar o serviço. 

Com o serviço Apache iniciado, digite “_localhost_” na barra de endereço do seu navegador e você terá acesso à página padrão: 

![q3-image4](https://imgur.com/e6DasSO.png)

2. **Alterando página default do Apache:** 

Na documentação da página padrão, é informado o caminho raiz do documento a ser alterado. 

![q3-image5](https://imgur.com/JEv53PS.png)

Utilize o editor “**vim**” para acessar o arquivo a ser editado. Como no comando abaixo:

``` linux
sudo vim /var/www/html/index.html 
```

Ao acessar o documento, digite o “ggVGdi”, para selecionar todo o conteúdo (**ggVG**), excluí-lo (**d**) de uma só vez e entrar no modo de inserção (**i**).  

Agora, é só inserir o seguinte trecho, substituindo “**seu-nome**” pelo seu nome. 

``` html
<!DOCTYPE html> 
<html lang="pt-BR"> 
  <head> 
    <meta charset="UTF-8"> 
    <title>AdaTech</title> 
  </head> 
    <body> 
      <h1>ADA + AdaTech + seu-nome = Sucesso!</h1> 
    </body> 
</html> 
```

Feito isso, tecle **_Esc_** para sair do modo de inserção e em seguida “**:wq**” para salvar e sair do editor vim. 

Por fim, recarregue a página _Localhost_ para visualizar as alterações. 

![q3-image6](https://imgur.com/FjvHSzL.png)
