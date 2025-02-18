
# WSL, Ubuntu-24.04, Docker e Laravel.

Instalação realizada com Windows 11.

Com WSL ativado, adicionar uma distribuição do Linux Ubuntu.

Abrir o Windows Power Shell como administrador.

Digite o comando para identificar as distribuições disponíveis: 


```bash
 wsl --list --online
```

Estarei utilizando o Ubuntu-24.04, para isso, no Power Shell digite:

```bash
wsl --install -d Ubuntu-24.04
```
Com a isntalação finalizada, entre com um usuário e senha.

## Instalação do Docker

Primeiro, atualize os pacotes:
```bash
sudo apt update && sudo apt upgrade -y
```
Em seguida, instale os pacotes necessários:
```bash
sudo apt install -y ca-certificates curl gnupg
```
Adicione a chave GPG oficial do Docker:
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
Adicione o repositório do Docker:
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Atualize os pacotes e instale o Docker:
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verifique a instalação:
```bash
docker --version
```
### Habilitar o Docker no WSL
Por padrão, o Docker no WSL precisa ser configurado para rodar sem o Docker Desktop. Para isso, execute:
```bash
sudo usermod -aG docker $USER
newgrp docker

```
Agora, habilite o daemon do Docker no WSL:
```bash
sudo service docker start

```
## Instalar o Docker Compose
O Docker Compose já vem como um plugin do Docker, mas caso precise da versão standalone:

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Verifique a instalação:

```bash
docker-compose --version

```
## Instalando o PHP e o Instalador do Laravel

Antes de instalar o Framework, realizo a instalação do php, composer e habilito o acesso ssh na distribuição Linux.

#### PHP e Composer

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl php-cli php-mbstring unzip -y
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer

```
Para verificar a versão do composer instalada:

```bash
composer -V
```

#### SSH
```bash
sudo apt update && sudo apt install openssh-server -y
sudo systemctl status ssh
sudo systemctl start ssh
sudo systemctl enable ssh
```

Via SSH acesso a distribuição instalada via terminal e sigo a instalação conforme a documentação do Laravel em:

[Documentação para instalação do Laravel](https://laravel.com/docs/11.x/installation)

Comandos para instalação do PHP e do Framework:

```bash
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
composer global require laravel/installer
```
Após realizada a as intalações, já é possivel criar uma aplicação com o comando:
```bash
laravel new example-app
```

```bash
cd example-app
npm install && npm run build
composer run dev
```

## Ambiente de desenvolvimento

O ambiente foi desenvolvido com base no [Curso Completo e Gratuito de Laravel 11](https://academy.especializati.com.br/curso/laravel-11-completo-e-gratuito) da [Especializa Ti Academy](https://academy.especializati.com.br/) onde foi realizado algumas alterações disponiveis neste repositório.

Com tudo pronto, suba os containers do projeto
```bash
docker-compose up -d
```
Acesse o container
```bash
docker-compose exec app bash
```
Instale as dependências do projeto
```bash
composer install
```
Gere a key do projeto Laravel
```bash
php artisan key:generate
```
Acesse o projeto em http://localhost:8000