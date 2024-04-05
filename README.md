# Instalação do Fedora Linux
Instalação do Fedora Linux

# INSTALAÇÃO

Ao instalar o Linux, escolha não instalar o driver proprietário NVIDIA durante a instalação, no final do processo será instalado o driver nouveau, um driver livre para as placas nVIDIA. Isso foi importante nos últimos dois anos!
Uma consideração especial sobre este driver é que ele é razoavelmente suficiente para resolução 1920x1080(fullhd), porém impraticável em resoluções superiores se sua intenção for aplicar dimensão das frações (125%, 150%, …). Usar fraçõs é muito útil em resoluções 4K onde as letras ficam tão pequenas que é preciso aumentar a dimensão.
Depois que o sistema estiver completamente instalado e após o boot, poderá optar por instalar o driver proprietário. Algo que precisa saber é que o driver proprietário NVIDIA não é compatível com o Wayland, se você quiser usufruir deste servidor gráfico terá de optar pelo driver intel ou noveau.

Serão muitas instruções a seguir, mas vale a pena ir até o final, mas fique ligue para pular as opções que podem não ser necessárias para você. E quando finalmente chegar ao final você será recompensado por não precisar ficar reinstalado o sistema todas as vezes como no Windows e tudo sempre funcionará exatamente como planejado.
