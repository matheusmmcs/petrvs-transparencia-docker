# PETRVS - Transparência Docker Configs (PGD)

Projeto auxiliar para execução da API e do Frontend da Transparência PGD - Petrvs.


## 💻 1 - Ambiente de Teste

Em ambiente de teste, basta configurar:

- .env:
 
```ini
TRANSPARENCIA_FRONTEND_IMAGE=ghcr.io/matheusmmcs/petrvs-transparencia-frontend:latest #versão desejada do front-end
TRANSPARENCIA_API_IMAGE=ghcr.io/matheusmmcs/petrvs-transparencia:latest #versão desejada do front-backend
TRANSPARENCIA_FRONTEND_PORT=3001 #porta que o frontend executará
TRANSPARENCIA_API_PORT=8881 #porta que a API executará
```
  Lembrete: a API_PORT deve ser replicada na configuração do ./transparencia/frontend/.env e no config do Nginx.

- ./transparencia/frontend/.env:
 
```ini
VITE_API_URL=http://localhost:8881 #porta deve ser igual à configurada no .env
VITE_HEADER_TITLE=Transparência PGD #titulo da página
VITE_FOOTER_TEXT=Rodapé #texto do rodapé
```

- ./transparencia/api/.env:
 
```ini
DB_USER=user
DB_PASSWORD="pass"
DB_HOST=1.2.3.4
DB_PORT=3306
DB_NAME=petrvs_tenant
```

Na pasta ./nginx há duas configurações, uma com SSL e outra sem. Recomenda-se utilizar a versão com SSL, e apenas em caso de desenvolvimento e testes, pode-se utilizar a outra configuração. 

As configurações contidas nesta pasta são sugestões, então pode-se utilizar outra configuração que melhor se adeque à sua realidade. No exemplo SSL, deve-se criar uma pasta ./nginx/ssl contendo fullchain.pem e privkey.pem.

Para executa o projeto, basta executar o comando:

```sh
docker-compose up
```

OBS: ao testar, abrir um navegador com CORS desabilitado. No MacOS pode-se utilizar o seguinte comando:

```sh
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
```

A aplicação ficará disponível em **[http://0.0.0.0:3001](http://0.0.0.0:3001)** ou, caso a porta do front seja alterada, na porta informada no .env! 🚀