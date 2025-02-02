## Instalação do QBittorrent Web Server no Ubuntu 22.04

Este tutorial irá guiá-lo na instalação do qBittorrent com interface web no Ubuntu 22.04 e configurá-lo para acesso remoto.

**Pré-requisitos:**

* Um servidor rodando Ubuntu 22.04 com privilégios de root ou sudo.

**Instalação:**

1. **Atualize as listas de pacotes:**

```bash
sudo apt update
```

2. **Adicione o repositório QBittorrent:**

```bash
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
```

3. **Atualize as listas de pacotes novamente:**

```bash
sudo apt update
```

4. **Instale o qBittorrent-nox (sem interface gráfica):**

```bash
sudo apt install qbittorrent-nox
```

**Acesso à Interface Web:**

O qBittorrent-nox inclui uma interface web acessível por padrão em:

```
http://localhost:8080
```

**Login Padrão:**

Usuário: admin
Senha: adminadmin

**Segurança:**

* **Altere a senha padrão imediatamente!** Isso é crucial para proteger sua instalação do qBittorrent.
* Considere medidas de segurança adicionais, como usar uma senha forte e restringir o acesso por endereço IP nas configurações da interface da web.

**Serviço Systemd (Opcional):**

Esta etapa cria um serviço systemd para iniciar e gerenciar automaticamente o qBittorrent na inicialização:

1. **Crie um arquivo de serviço systemd:**

```bash
sudo nano /etc/systemd/system/qbittorrent-nox.service
```

2. **Copie e cole o seguinte conteúdo, ajustando a porta se necessário (padrão 8080):**

```
[Unit]
Description=qBittorrent-nox
After=network.target

[Service]
Type=forking
ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8080 (Substitua 8080 pela porta desejada se outro serviço a usar)
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

3. **Salve o arquivo (Ctrl+O) e saia (Ctrl+X).**

4. **Recarregue o systemd:**

```bash
sudo systemctl daemon-reload
```

5. **Habilite o serviço qBittorrent:**

```bash
sudo systemctl enable qbittorrent-nox
```

6. **Inicie o serviço qBittorrent:**

```bash
sudo systemctl start qbittorrent-nox
```

7. **Verifique o status do serviço:**

```bash
sudo systemctl status qbittorrent-nox
```

**Acesso Remoto à Interface Web (Opcional):**

Se você deseja acessar a interface web de outro dispositivo em sua rede, pode configurar um proxy reverso com um servidor como o Nginx.

**Observações Adicionais:**

* Este guia fornece uma instalação básica. Consulte a documentação oficial do qBittorrent para opções de configuração mais avançadas: [https://www.qbittorrent.org/download](https://www.qbittorrent.org/download)
* Lembre-se de alterar a senha padrão o mais rápido possível para garantir a segurança da sua instalação.
* Para um guia mais detalhado sobre a configuração do Nginx como proxy reverso, consulte a documentação do Nginx ou tutoriais específicos.

* REMOVER
  
1. Remover instalação
* sudo apt remove --purge qbittorrent-nox -y

2. Apagar arquivos de configuração

Os arquivos de configuração podem estar em vários locais, dependendo de como foi executado. Apague todos:

sudo rm -rf /home/*/.config/qBittorrent
sudo rm -rf /root/.config/qBittorrent
sudo rm -rf /var/lib/qbittorrent
sudo rm -rf /etc/systemd/system/qbittorrent-nox.service

3. Apagar diretórios de downloads (opcional)

Se quiser remover também os arquivos baixados, apague os diretórios onde o qBittorrent salvava os torrents:

sudo rm -rf /mnt/DOWNLOADS
sudo rm -rf /mnt/Torrents
sudo rm -rf /home/*/Downloads/qBittorrent

⚠️ Atenção: Se houver arquivos importantes nos diretórios de download, faça backup antes de rodar os comandos acima.

FIZ MERDA UERO RESETAR A SENHA ADM

nano /.config/qBittorrent/qBittorrent.conf

Agora, localize e remova as seguintes linhas se existirem:

WebUI\Password_PBKDF2=@ByteArray(...)
WebUI\Password_ha1=@ByteArray(...)

Se quiser redefinir o nome de usuário para admin, edite ou adicione esta linha:

WebUI\Username=admin

Salve e saia (Ctrl + X, Y, Enter).
