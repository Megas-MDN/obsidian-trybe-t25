
-   O Unix é um sistema operacional que inspirou muitos outros sistemas, como macOS, Linux, Solaris etc.;
-   O Unix é composto basicamente de Shell, Kernel e programas;
-   A estrutura de diretórios do Unix é organizada no formato de uma árvore invertida, hierarquicamente, iniciando pelo _root_ (raiz);
-   Tudo no Unix é um arquivo ou um processo;
-   O terminal é seu principal aliado para ter produtividade em um ambiente Unix.
    

Um bom exercício para praticar os comandos aprendidos até agora é descrever, mentalmente, o que cada comando faz. Não se preocupe, pois a seguir há uma breve explicação sobre eles. Consulte-a sempre que sentir necessidade.

| Comando                | Significado                                        |
| ---------------------- | -------------------------------------------------- |
| `touch arquivo.extensao` | Cria um arquivo com o nome e a extensão desejados. |
|	``	ls	``	|	Lista arquivos e diretórios.	|
|	``	ls -a	``	|	Lista arquivos e diretórios, incluindo os ocultos.	|
|	``	mkdir nome-diretorio	``	|	Cria um diretório com um nome especificado.	|
|	``	cd diretorio	``	|	Muda para o diretório nomeado. Aqui você pode navegar por múltiplos diretórios com o uso da /, como em cd Documentos/exercicios.	|
|	``	cd	``	|	Muda para o diretório inicial.	|
|	``	cd ~	``	|	Muda para o diretório inicial.	|
|	``	cd ..	``	|	Muda para o diretório-pai do diretório atual.	|
|	``	pwd	``	|	Mostra o caminho do diretório atual.	|
|	``	cp arquivo1 arquivo2	``	|	Copia arquivo1 para o mesmo diretório, chamando-o de arquivo2.	|
|	``	mv arquivo1 arquivo2	``	|	Renomeia arquivo1 para arquivo2.	|
|	``	mv arquivo 1 /diretorio	``	|	Move arquivo1 para o diretório especificado.	|
|	``	rm arquivo	``	|	Remove um arquivo.	|
|	``	rmdir diretorio	``	|	Remove um diretório.	|
|	``	cat arquivo	``	|	Sem nenhuma opção, o conteúdo do arquivo é exibido no terminal.	|
|	``	cat > arquivo.txt	``	|	O operador de redirecionamento cria novos arquivos de texto. Para quebrar linha, pressione enter; para finalizar a edição, utilize CTRL + D. Você pode editar arquivos, mas irá sobrescrever o conteúdo.	|
|	``	less arquivo	``	|	Exibe o conteúdo do arquivo no terminal, uma página por vez. Para sair do terminal, aperte a tecla Q.	|
|	``	head arquivo	``	|	Exibe, por padrão, as 10 primeiras linhas do arquivo informado.	|
|	``	head -5 arquivo	``	|	Exibe as 5 primeiras linhas do arquivo informado. Você pode utilizar qualquer valor numérico para exibir a quantidade de linhas que desejar.	|
|	``	tail arquivo	``	|	Exibe, por padrão, as 10 últimas linhas do arquivo informado.	|
|	``	tail -5 arquivo	``	|	Exibe as 5 últimas linhas do arquivo informado. Você pode utilizar qualquer valor numérico para exibir a quantidade de linhas que desejar.	|
|	``	grep 'palavra-chave' arquivo	``	|	Procura por palavras-chave no arquivo informado. O retorno é exibido no terminal.	|
|	``	wc arquivo	``	|	Conta o número de linhas, palavras, caracteres ou bytes no arquivo, dependendo da tag usada (-l, -w, -m e -c, respectivamente), e exibe o resultado no terminal.	|
|	``	*	``	|	Corresponde a qualquer número de caracteres.	|
|	``	?	``	|	Corresponde a um caractere qualquer.	|
|	``	man comando	``	|	Exibe a página do manual on-line do comando informado.	|
|	``	whatis comando	``	|	Exibe uma breve descrição do comando informado.	|
|	``	apropos 'palavra-chave'	``	|	Exibe comandos correspondentes à palavra-chave informada.	|
|	``	comando > arquivo	``	|	Redireciona a saída padrão do comando para o arquivo e sobrescreve o conteúdo existente, se o arquivo já existir.	|
|	``	comando >> arquivo	``	|	Adiciona a saída padrão do comando ao final do arquivo.	|
|	``	comando < arquivo	``	|	Direciona o comando para um arquivo, sem alterar esse arquivo.	|
|	`comando1` \| `comando2`	|	Envia a saída do comando1 como entrada para o comando2.	|
|	``	cat arquivo1 arquivo2 > arquivo3	``	|	Une os conteúdos dos arquivos 1 e 2 no arquivo3.	|
|	``	sort	``	|	Ordena dados.	|
|	``	who	``	|	Lista as pessoas usuárias logadas atualmente.	|


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/fe827a71-3222-4b4d-a66f-ed98e09961af/day/e1567f20-ee53-41b4-9054-b2d026a5af8e/lesson/08b5311f-f36e-4e30-9688-a52b4a43f9e1)
