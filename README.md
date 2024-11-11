# Atividade 7 - Fundamentos de Programação de Sistemas
## Calculadora em Bash e CGI

Este projeto é uma calculadora simples desenvolvida em Bash e CGI, permitindo ao usuário inserir dois números e escolher uma operação (adição, subtração, multiplicação ou divisão). O resultado da operação é exibido em uma página HTML gerada dinamicamente.

[Vídeo exemplificando a execução](https://drive.google.com/file/d/1xMMN90z8OkmnKQUAZwW-vgRXn1s5rSfd/view?usp=drive_link)

## Estrutura do Projeto

- **calculadora.html**: Página HTML com o formulário para o usuário inserir os números e escolher a operação.
- **calculadora.cgi**: Script Bash que processa os dados do formulário e retorna o resultado.

## Configuração de CGI no Ubuntu com Apache

Este guia explica como configurar o **Common Gateway Interface (CGI)** no Ubuntu, usando o servidor web **Apache**.

### Pré-requisitos

- Ubuntu com privilégios de superusuário (root ou sudo).
- Apache instalado.

### Passo a Passo para Configuração

#### 1. Instalar o Apache

Se o Apache ainda não estiver instalado, execute os comandos abaixo:

```bash
sudo apt update
sudo apt install apache2
```

2. Habilitar o Módulo CGI no Apache
Para que o Apache suporte scripts CGI, é necessário habilitar o módulo mod_cgi:

```bash
sudo a2enmod cgi
```
Em seguida, reinicie o Apache para aplicar as alterações:

```bash
sudo systemctl restart apache2
```

3. Configurar o Diretório para Scripts CGI
Por padrão, o Apache usa o diretório /usr/lib/cgi-bin/ para scripts CGI. Edite o arquivo de configuração do Apache para garantir que este diretório esteja configurado corretamente:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

No arquivo, adicione a linha abaixo dentro do bloco <VirtualHost>:

```apache
ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
```

4. Permitir Execução de CGI no Diretório
Ainda no arquivo de configuração, defina as permissões para que o Apache possa executar scripts CGI dentro do diretório:

```apache
<Directory "/usr/lib/cgi-bin">
    Options +ExecCGI
    AddHandler cgi-script .cgi .pl .sh
    Require all granted
</Directory>
```

5. Mover os Arquivos para os Diretórios Corretos
```bash
sudo mv calculadora.html /var/www/html/
sudo mv calculadora.cgi /usr/lib/cgi-bin/
```

6. Tornar o Script Executável
Dê permissão de execução ao script criado:

```bash
sudo chmod +x /usr/lib/cgi-bin/calculadora.cgi
```

7. Reiniciar o Apache
Para aplicar todas as configurações, reinicie o Apache:

```bash
sudo systemctl restart apache2
```

8. Executar o Script CGI
Para verificar o funcionamento do script:

```bash
sudo /usr/lib/cgi-bin/calculadora.cgi
```

9. Executar o calculadora.html
Abra o navegador e acesse a página HTML:

```arduino
http://localhost/calculadora.html
```
