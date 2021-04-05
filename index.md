# Suridata: Documentação para integração com a API

A Suridata provê uma API para integração dos relatórios de empresas de sua seguradora e cliente.

## URL para requisição:
```
https://portal.suridata.com.br/api/auth/
```

## Requisição

### Exemplos de requisição:
`CURL`

      curl --request POST \
      --url https://portal.suridata.com.br/api/auth/ \
      --header 'Content-Type: application/json' \
      --data '{
      "cliente": "Nome do cliente",
      "seguradora": "Nome da seguradora",
      "token": "Token passado pela Suridata"
     }'
     
`Laravel`

      <?php
      namespace App\Classes;
      
      use Exception;
      
      class Suridata
      {
        // url do API
        private $url = 'https://portal.suridata.com.br/api/auth/';
        // variaveis
        private $client, $provider;
    
        public function __construct($client, $provider)
        {
            $this->client = $client;
            $this->provider = $provider;      
        }

        public function getFrame(){        
            // dados da requisição
            $data = array(
                'token' => $this->token,
                'cliente' => $this->client,
                'seguradora' => $this->provider
            );        

            // inicia e configura sessão
            $curl_handle = curl_init();
            curl_setopt($curl_handle, CURLOPT_URL, $this->url);
            curl_setopt($curl_handle, CURLOPT_POST, 1);
            curl_setopt($curl_handle, CURLOPT_POSTFIELDS, $data);
            curl_setopt($curl_handle, CURLOPT_RETURNTRANSFER, true);
            // executa comando
            $result = curl_exec($curl_handle);

            // retorna erro se houve algum erro
            if ($result === false) {
                return ("Erro " . curl_error($curl_handle));
            }

            return $result;
        }
    }
     
     
### Corpo da requisição:  
`POST /`

    {
      "cliente": "Nome do cliente",
      "seguradora": "Nome da seguradora",
      "token": "Token passado pela Suridata"
    }

### Exemplo de resposta

A resposta vai retornar apenas a string com a url para embedar no portal terceiro

| Campo       | Tipo            | Descrição        |
| ----------- | --------------- | -----------------|
| URL         | String          | URL para embedar | 


### Suporte ou contato

[![Badge](https://img.shields.io/static/v1?label=Site&message=Acesse%20o%20site&color=lightgrey)](https://www.suridata.com.br/)
[![Gmail Badge](https://img.shields.io/badge/-desenvolvimento@suridata.com.br-c14438?style=flat-square&logo=Gmail&logoColor=white&link=mailto:desenvolvimento@suridata.com.br)](desenvolvimento@suridata.com.br)
