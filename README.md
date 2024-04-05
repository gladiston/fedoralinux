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

## HABILITANDO SESSÃO REMOTA
Carregue o programa “Configurações”, então procure por “host” ou “compartilhamento” e então encontre a seção “Compartilhamento”. Queremos no momento ativar o compartilhamento de sessão remota, isto é, permitir que outras pessoas na rede possam abrir uma sessão via ssh ou display grafico (ssh -X) neste computador:

![Habilitando sessão remota](./sessao_remota_ativar.png)

Note que na imagem é mostrado um exemplo de como posso usar o ssh para abrir uma sessão.

## ATUALIZAÇÃO DE REPOSITÓRIO
(todo)

## HABILITANDO O DELTA RPM
(todo)


## COMPLETANDO O IDIOMA PORTUGUÊS
(todo)

## INSTALANDO PROGRAMAS BASICOS
Estes programas considero essenciais no sistema, são programas utilitários que ajudam a resolver problemas:
```
sudo dnf install -y the_silver_searcher dconf-editor gnome-tweaks 
sudo dnf install -y wget curl tar unzip squashfs-tools
sudo dnf install -y cabextract lzip p7zip p7zip-plugins 
sudo dnf install -y unrar dkms
```

## INSTALANDO PROGRAMAS BASICOS PARA RECOMPILAR
Os pacotes a seguir servem para quem pretende compilar algo no ambiente Linux. Se você pretende instalar o driver proprietário da NVIDIA fornecido pela NVIDIA você também precisará deles:
```
sudo dnf groupinstall "Development Tools" "Development Libraries"
sudo dnf install -y make automake gcc gcc-c++ kernel-devel binutils libX11-devel 
sudo dnf install -y libglvnd-opengl libglvnd-devel pkgconfig
sudo dnf install -y qt5pas qt5pas-devel
sudo dnf install -y wxGTK-devel wxGTK cmake
sudo dnf install -y openal openal-devel
```


## PARTIÇÕES NTFS NO SISTEMA
Se utiliza uma partição Windows (NTFS) para gravar seus arquivos e dados a partir do Linux, você pode simplesmente não fazer nada e usar o gerenciador de arquivos do GNOME para entrar e sair do disco NTFS quando quiser. Contudo, se você tem que ir para o terminal e acessá-lo dali então lhe seria conveniente criar uma pasta vazia que ao entrar nela você já observasse o conteúdo dessa partição, se você gostou da idéia então vamos implementá-la:
Identifique qual é o seu disco, execute no terminal:
```
sudo blkid |grep ntfs
/dev/nvme1n1p2: LABEL="Windows" BLOCK_SIZE="512" UUID="389083EB9083AE46" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="f8ff4bca-3ef8-4ba7-b1b1-6e0b00689aab"
/dev/nvme1n1p3: LABEL="DADOS" BLOCK_SIZE="512" UUID="1EB4CCF2B4CCCE09" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="0acfc054-4ac1-46f6-83e3-c90bb5e79f12"
```
No exemplo anterior, o disco desejado tem o LABEL=DADOS e UUID="1EB4CCF2B4CCCE09" , então vamos criar uma pasta vazia, preferencialmente com o nome da label do disco na $HOME ou /media (ou /mnt), ex: /home/usuario/label_dados ou /media/label_dados, a vantagem de ficar em $HOME é que com os cuidados necessários apenas você terá acesso a ela, mas se prefere disponibilizar a partição para todos então tente:
```
sudo mkdir -p /media/label_dados
sudo chmod 1777 /media/label_dados
sudo chmod +s /bin/ntfs-3g
sudo usermod -aG disk $USER 
```

Estamos deixando claro que /media/label_dados estará disponível a todos os usuários. Se escolher criar uma pasta em $HOME, não há a necessidade das linhas acima, apenas criar a pasta vazia.

Execute no terminal:
```
sudo vim /etc/fstab
```
Agora vamos editar o arquivo /etc/fstab e então acrescentar após a última linha:
```
# Minha partição NTFS de label “DADOS”
UUID="1EB4CCF2B4CCCE09" /media/label_dados ntfs-3g windows_names,nosuid,nodev,nofail,rw,user,gid=users,noauto 0 0
```
Explicando os demais parâmetros:
nosuid: Bloqueia a operação de bits suid e sgid
nodev: Não interpreta dispositivos especiais de bloco no sistema de arquivos.
nofail: faz com que o dispositivo seja montado mesmo que tenha sido marcado com erro. Um drive é marcado com ‘erro’ quando o computador é desligado abruptamente ou quando qualquer unidade listada no fstab não está presente ou falhou na montagem.
zero e zero no final da linha: todo


Uma outra forma de escrever essa linha no fstab seria:
```
UUID="1EB4CCF2B4CCCE09" /media/label_dados ntfs nls-utf8,rw,nosuid,nodev,nofail 0 0
```
A diferença é que ao usar driver “ntfs-3g” você estará usando um driver do tipo userspace(pacote ntfs-3g precisa estar instalado) considerado o método mais moderno e seguro, enquanto “ntfs” está ligado a um módulo diretamente no kernel do linux que geralmente recomendamos usar apenas no modo de leitura que impede qualquer gravação na unidade. Mas pode-se habilitar o modo de leitura e escrita se desejar, já testei ambos no modo leitura/escrita e prefiro o “ntfs-3g” que além de ser mais seguro, possui outros parâmetros que nos ajudam a evitar nomes de arquivos que podemos criar usando Linux, mas que o Windows terá problemas com eles, por exemplo o uso de caracteres como  “:” e “?” em nomes de arquivos.

Salve e após o boot, a pasta indicada servirá de acesso a partição NTFS.
Se você não quiser auto montá-la no boot, mas mantê-la apenas quando executar no terminal:
```
mount /media/label_dados
```
Então troque “auto” para “noauto”. O “noauto” é mais seguro por impedir que programas instalados ou scripts maliciosos tenham acesso a esta partição ou disco.
Caso precise reparar a unidade NTFS, execute:
```
sudo ntfsfix /dev/disk/by-uuid/34F84B57F84B1690
```
ou se souber o label do disco:
```
sudo ntfsfix /dev/disk/by-label/DADOS
```
Alternativas: Existe um serviço chamado AutoFS, ele implementa uma solução onde você indica pastas e apenas quando você acessá-las, ele as monta. Serve para discos externos, partições internas e também para compartilhamentos remotos. Esta última, é o motivo pelo qual é mais usado visto que auto-montar pastas que já estão em nosso domínio é mais fácil usando o fstab. AutoFS é um pouco mais complicado que usar /etc/fstab, mas nem tanto depois que você entende como ele funciona. Eu tenho receio de utilizá-lo em ambientes com pouco controle porque se houver programas que vasculhem discos eles irão montar todas as pastas que encontrarem na configuração para auto montar, talvez  voce pense na situação de vírus de computador, mas ocorreria algo similar em softwares de backups que podem erroneamente incluir pastas que não deveriam. Se quiser estudar o AutoFS:

https://devconnected.com/how-to-install-autofs-on-linux/

## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)


## xxxx
(todo)

