# install-Qbtorrent-Web---Server-Ubuntu-22
Instalação do Qb Torrent no servidor Ubuntu Server 22

Instalando o qBittorrent no Ubuntu Server 22 com Acesso Web: Guia Completo

Para instalar e configurar o qBittorrent com acesso web no Ubuntu Server 22, siga estes passos:

Pré-requisitos:

    Ubuntu Server 22.04 LTS (Jammy Jellyfish) instalado e atualizado.
    Acesso ao terminal com privilégios de root ou sudo.
    Conexão com a internet ativa.

Etapas de instalação:

    Adicione o repositório qBittorrent: Adicione o repositório oficial do qBittorrent usando o seguinte comando:

sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable

    Atualize a lista de pacotes: Atualize a lista de pacotes disponíveis com o comando:

sudo apt update

    Instale o qBittorrent: Instale o qBittorrent e seus pacotes de dependências usando o comando:

sudo apt install qbittorrent-nox qbittorrent-webconfig

    Configure o acesso web: Acesse o arquivo de configuração do qBittorrent-webconfig com o comando:

sudo nano /etc/qbittorrent-webconfig/config.py

    Edite as configurações: Edite as seguintes configurações no arquivo:
        WEBUI_ADMIN_USERNAME: Altere o nome de usuário padrão para o acesso web (ex: "admin").
        WEBUI_ADMIN_PASSWORD: Altere a senha padrão para o acesso web (recomenda-se uma senha forte).
        WEBUI_PORT: Altere a porta padrão da interface web (ex: 8080).

    Salve o arquivo e feche o editor.

    Reinicie o qBittorrent: Reinicie o serviço qBittorrent para aplicar as alterações:

sudo systemctl restart qbittorrent-nox

    Acesse a interface web: Abra um navegador web e acesse a URL:

http://<endereço-IP-do-seu-servidor>:<porta-definida-na-configuração>

Observações importantes:

    Substitua <endereço-IP-do-seu-servidor> pelo endereço IP real do seu servidor Ubuntu.
    Use o nome de usuário e senha definidos na configuração do arquivo config.py para acessar a interface web.
    Por padrão, o qBittorrent usa a porta 8080 para a interface web. Você pode alterar essa porta na etapa 5 da instalação.
    Acesse a documentação oficial do qBittorrent para mais informações sobre a configuração da interface web: https://www.reddit.com/r/qBittorrent/comments/zvxe5w/web_ui_setup/

Dicas extras:

    Configure o firewall: Permita o acesso à porta definida para a interface web no firewall do seu servidor para que ela seja acessível externamente.
    Proteja seu acesso web: Use uma senha forte para o acesso web e considere habilitar autenticação de dois fatores para maior segurança.
    Mantenha o qBittorrent atualizado: Execute atualizações regularmente para garantir a segurança e estabilidade do software.

Recursos adicionais:

    Documentação oficial do Ubuntu Server: https://ubuntu.com/server/docs
    Documentação oficial do qBittorrent: https://www.reddit.com/r/qBittorrent/comments/zvxe5w/web_ui_setup/
    Fórum da comunidade do qBittorrent: https://forum.qbittorrent.org/

Espero que este guia completo tenha ajudado você a instalar e configurar o qBittorrent com acesso web no seu Ubuntu Server 22 de forma segura e eficiente!
