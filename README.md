# 🚀 WSL, Ubuntu 24.04, Docker e Laravel 🌍

Este guia aborda a instalação e configuração do ambiente de desenvolvimento utilizando **WSL**, **Ubuntu 24.04**, **Docker** e **Laravel**, com base no Windows 11.

## 1️⃣ Instalação do WSL e Ubuntu 24.04

Primeiro, ative o **WSL** e adicione uma distribuição Linux **Ubuntu 24.04**.

### 🔍 Verificando distribuições disponíveis

Abra o **Windows PowerShell** como administrador e execute:

```bash
wsl --list --online
```

### 📥 Instalando o Ubuntu 24.04

Para instalar a versão desejada, execute:

```bash
wsl --install -d Ubuntu-24.04
```

Após a instalação, crie um usuário e senha conforme solicitado.

---

## 2️⃣ Instalação do Docker 🐳

### 🔄 Atualizando os pacotes

```bash
sudo apt update && sudo apt upgrade -y
```

### 📦 Instalando pacotes necessários

```bash
sudo apt install -y ca-certificates curl gnupg
```

### 🔑 Adicionando a chave GPG oficial do Docker

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### 📌 Adicionando o repositório do Docker

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 🏗️ Instalando o Docker

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### ✅ Verificando a instalação

```bash
docker --version
```

### ⚙️ Habilitando o Docker no WSL

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Inicie o serviço do Docker:

```bash
sudo service docker start
```

---

## 3️⃣ Instalação do Docker Compose 📦

O Docker Compose já vem como um plugin do Docker. Caso precise da versão standalone, utilize:

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### 🔎 Verificando a instalação

```bash
docker-compose --version
```

---

## 4️⃣ Instalando PHP, Composer e SSH 🛠️

### ⚡ Instalando PHP e Composer

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl php-cli php-mbstring unzip -y
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

### 🔍 Verificando a instalação do Composer

```bash
composer -V
```

### 🔐 Instalando e configurando o SSH

```bash
sudo apt update && sudo apt install openssh-server -y
sudo systemctl status ssh
sudo systemctl start ssh
sudo systemctl enable ssh
```

Acesse a distribuição Linux via SSH para continuar com a instalação do Laravel.

---

## 5️⃣ Instalação do Laravel 🌐

Para instalar o Laravel, siga a documentação oficial:
[📖 Documentação Laravel](https://laravel.com/docs/11.x/installation)

### 📦 Instalando o PHP e o Laravel Installer

```bash
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
composer global require laravel/installer
```

### 🚀 Criando um novo projeto Laravel

```bash
laravel new example-app
cd example-app
```

Instale as dependências:

```bash
npm install && npm run build
composer install
```

---

## 6️⃣ Configuração do ambiente de desenvolvimento 🖥️

O ambiente foi baseado no [Curso Completo e Gratuito de Laravel 11](https://academy.especializati.com.br/curso/laravel-11-completo-e-gratuito) da [Especializa Ti Academy](https://academy.especializati.com.br/).

### 🌍 Criando e configurando a rede no Docker

```bash
docker network create laravel
```

### 📌 Subindo os containers do projeto

```bash
docker compose up -d
```

### 🔑 Acessando o container

```bash
docker compose exec app bash
```

### ⚡ Configuração do Laravel

Instale as dependências:

```bash
composer install
```

Gere a chave do projeto Laravel:

```bash
php artisan key:generate
```

Crie as tabelas no MySQL:

```bash
php artisan migrate
```

Inicie o ambiente de desenvolvimento:

```bash
npm run dev
```

Ou construa os assets para produção:

```bash
npm run build
```

Acesse a aplicação em: **[http://localhost:8000](http://localhost:8000)**

---

## 7️⃣ Tradução para PT-BR 🇧🇷

Caso queira instalar a tradução **PT-BR** no Laravel, siga o passo a passo: [🔗 Laravel PT-BR Localization](https://github.com/lucascudo/laravel-pt-BR-localization)

O repositório já vem com a tradução ativada. Para alterar o idioma, modifique a variável `APP_LOCALE` no arquivo `.env`.

---

## 🎯 Conclusão 🎉

Agora seu ambiente está pronto para o desenvolvimento com **WSL, Ubuntu 24.04, Docker e Laravel**. 🚀

Caso tenha dúvidas, consulte a documentação oficial de cada tecnologia utilizada:

- 📖 [WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
- 🐳 [Docker](https://docs.docker.com/get-docker/)
- 🌍 [Laravel](https://laravel.com/docs/11.x/installation)

Happy coding! 💻✨

