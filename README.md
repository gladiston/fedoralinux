# Instalação do Fedora Linux
Instalação do Fedora Linux

## INSTALAÇÃO

Ao instalar o Linux, escolha não instalar o driver proprietário NVIDIA durante a instalação, no final do processo será instalado o driver nouveau, um driver livre para as placas nVIDIA. Isso foi importante nos últimos dois anos!
Uma consideração especial sobre este driver é que ele é razoavelmente suficiente para resolução 1920x1080(fullhd), porém impraticável em resoluções superiores se sua intenção for aplicar dimensão das frações (125%, 150%, …). Usar fraçõs é muito útil em resoluções 4K onde as letras ficam tão pequenas que é preciso aumentar a dimensão.
Depois que o sistema estiver completamente instalado e após o boot, poderá optar por instalar o driver proprietário. Algo que precisa saber é que o driver proprietário NVIDIA não é compatível com o Wayland, se você quiser usufruir deste servidor gráfico terá de optar pelo driver intel ou noveau.

Serão muitas instruções a seguir, mas vale a pena ir até o final, mas fique ligue para pular as opções que podem não ser necessárias para você. E quando finalmente chegar ao final você será recompensado por não precisar ficar reinstalado o sistema todas as vezes como no Windows e tudo sempre funcionará exatamente como planejado.

O ambiente aqui trata-se dum notebook Acer, no entanto, boa parte deste documento aplica-se a qualquer hardware. Quando for especíco para um hardware, colocarei numa seção especial.

## MUDANDO O NOME DO HOST
Carregue o programa “Configurações”, então procure por “host” ou “compartilhamento” e então encontre a seção “Compartilhamento”. Não queremos no momento ativar o compartilhamento arquivos, mas desejamos apenas modificar o nome do computador por algo que represente melhor o nome do nosso computador que “fedora”:

![Mudando o nome do host](./mudando_nome_do_host.png)

## HABILITANDO O COMPARTILHAMENTO DE ARQUIVOS 
Ainda no programa “Configurações”, então procure por “host” ou “compartilhamento” e então encontre a seção “Compartilhamento”. Neste momento queremos ativar o compartilhamento arquivos:

![Habilitando o compartilhamento de arquivos](./compartilhar_arquivos_ativar.png)

Quando precisar acessar arquivos neste computador a partir de outro computador, basta ter acesso ao navegador e indicar a URL que aparece na imagem e digitar a senha que você forneceu. Simples assim.

## HABILITANDO AREA DE TRABALHO REMOTA
Ainda no programa “Configurações”, então procure por “host” ou “compartilhamento” e então encontre a seção “Compartilhamento”. Neste momento queremos ativar o compartilhamento arquivos:

![Habilitando area de trabalho remota](./area_trabalho_remota.png)

Quando precisar acessar sua estação de trabalho remota você poderá usar aplicativos como o remmina. Bastará fornecer a URL que indica seu computador como mostrado acima em destaque e então fornecer as credenciais fornecidas.

## COMPARTILHAMENTO DE MULTIMEDIA
Ainda no programa “Configurações”, então procure por “host” ou “compartilhamento” e então encontre a seção “Compartilhamento”. Neste momento queremos ativar o compartilhamento de multimedia, que na verdade é uma seção para escolher o que devo compartilhar, enquanto a seção HABILITANDO O COMPARTILHAMENTO DE ARQUIVOS habilita o compartilhamento de arquivos, a seção COMPARTILHAMENTO DE MULTIMEDIA determina o que deve ser compartilhado:

![Escolhendo o que devo compartilhar](./compartilhar_arquivos_selecionar_pastas.png)

Note na imagem que também é possivel acrescentar outras pastas.
Normalmente, estes compartilhamento são visiveis a partir de outras estações linux e também estações windows. A partir de estações Windows basta chamar como \\computador e os compartilhamentos que houverem no computador serão exibidos.
