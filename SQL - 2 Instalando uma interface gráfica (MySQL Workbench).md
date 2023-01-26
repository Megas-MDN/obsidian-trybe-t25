[[Banco de Dados]]
[[Docker]]
[[SQL]]
[[SQL - 1 Instalando MySQL Server com Docker 🐋]]

Ainda que haja uma grande adesão de ferramentas não gráficas no mundo back-end, é possível “visualizar” as nossas queries com o auxílio de alguns softwares. Aqui, vamos fazer a instalação do **MySQL Workbench**, a interface gráfica mais utilizada para o **MySQL**.

## Linux

**Observação:** Em função das diversas distribuições do Linux, é recomendado pesquisar as instruções de instalação específicas para sua distribuição. Exemplo: “Install MySQL Workbench on {Nome da sua distribuição}”. Nosso curso dá preferência para utilização das últimas versões [**LTS** _(Long-term Support, Suporte de longo prazo)_ do **Ubuntu**](https://wiki.ubuntu.com/Releases) _(Assim como das variantes descritas no manual da pessoa estudante)_ ainda suportadas. Verifique o suporte do seu S.O. [na pagina oficial](https://www.mysql.com/support/supportedplatforms/database.html).

1.  Por exemplo, para fazer essa instalação no **Ubuntu 20.04 LTS**, basta ir até [este link](https://dev.mysql.com/downloads/workbench/) e selecionar a opção “Ubuntu Linux”.
    
2.  Em seguida, **selecionando a versão correspondente da distribuição**, no caso, a 20.04 e, na lista a seguir, clicar em “Download”.
    
    ![Opção de download para Ubuntu Linux](https://content-assets.betrybe.com/prod/5e9c67af-8f0b-4874-8c50-62f492e7fa71-Op%C3%A7%C3%A3o%20de%20download%20para%20Ubuntu%20Linux.gif)
    
    Opção de download para Ubuntu Linux
    
    _Caso em algum momento surja uma página pedindo por login, não é necessário criar uma conta. Procure pelo link “No thanks, just start my download” e faça o download._
    
3.  Navegue até a pasta onde foi feito o download, rode o comando a seguir e aceite a instalação:
    

Copiar

```bash
1 sudo apt install ./nome-do-arquivo
2 #ex no Ubuntu 20.04: sudo apt install ./mysql-workbench-community_8.0.21-1ubuntu20.04_amd64.deb
```

## macOS

O processo de instalação no macOS é bastante simples, acesse [este link](https://downloads.mysql.com/archives/workbench) e selecione a versão correspondente:

![Fluxo de download macOS](https://content-assets.betrybe.com/prod/5e9c67af-8f0b-4874-8c50-62f492e7fa71-Fluxo%20de%20download%20macOS.gif)

Fluxo de download macOS

_Caso em algum momento surja uma página pedindo por login, não é necessário criar uma conta. Procure pelo link “No thanks, just start my download” e faça o download._

O fluxo de instalação no macOS segue conforme ilustrado:

![Fluxo de instalação macOS](https://content-assets.betrybe.com/prod/5e9c67af-8f0b-4874-8c50-62f492e7fa71-Fluxo%20de%20instala%C3%A7%C3%A3o%20macOS.gif)

Fluxo de instalação macOS

## Inicialização do aplicativo

Pronto, agora abra o **MySQL Workbench** através do seu menu de aplicativos. Após abri-lo, você estará na tela inicial, na qual você deverá selecionar o servidor em que quer entrar.

_Em geral, o workbench identifica seu server instalado, retornando um “Local instance” referente a ele, no nosso caso aqui, por termos apenas um server instalado, ele retorna um “Local instance” na porta padrão 3306._

Como ilustrado no _gif_ abaixo, ao clicar na instância uma senha será solicitada. Você deve digitar sua **password do servidor, definido anteriormente**, e pode marcar a opção _Save password in keychain_ para não precisar repetir sua senha novamente a cada conexão.

![Tela inicial do Workbench](https://content-assets.betrybe.com/prod/5e9c67af-8f0b-4874-8c50-62f492e7fa71-Tela%20inicial%20do%20Workbench.gif)

Tela inicial do Workbench

## Solução de problemas _(Ubuntu-based distros)_

Caso se depare com a situação ilustrada na imagem abaixo, em que pode-se ver uma aba com o texto _unconnected_ e os botões com ícone de _raio_ apagados, significa que seu servidor não está conectado e por isso essas opções estão desabilitadas. Para solucionar este problema é necessário realizar o passo mostrado no _gif_ anterior.

Se este ou algum outro erro persistir, peça ajuda às pessoas instrutoras no slack ou durante os plantões.

![Tela Workbench não conectado](https://content-assets.betrybe.com/prod/5e9c67af-8f0b-4874-8c50-62f492e7fa71-Tela%20Workbench%20n%C3%A3o%20conectado.png)

Tela Workbench não conectado

É possível que algumas [**flavours**](https://ubuntu.com/download/flavours) _(“sabores”, as variantes)_ do Ubuntu não contenham o pacote `gnome-keyring` por padrão (como o caso do Kubuntu). Esse pacote é requerido pelo workbench nas distros baseadas em ubuntu para gerenciamento de senhas. Caso, nessas condições, seu workbench apresente problemas durante a configuração de usuário/senha, execute o comando `sudo apt install gnome-keyring` e tente novamente.



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/fa69c314-da3c-46e0-bcdb-43297772a43e/day/89e3203d-18e4-4329-9c8d-a3f40f2e4248/lesson/4c92bf82-4e5e-49dd-b8c9-4695c79ca33e)