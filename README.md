# Diretório S3

Bem-vindo ao projeto **S3-Directory-Listing**! Está cansado das listagens genéricas e entediantes dos buckets do S3? 🥱 Bem, não procure mais! 😎 Este pequeno e elegante script JS e combo HTML transformará seu bucket S3 em uma lista de arquivos e pastas com uma interface bonita e funcionalidade de pesquisa. Ah, e eu mencionei que também tem um modo escuro? 🌙

## Uso 🚀

Para usar o S3-Directory-Listing, siga estes passos simples:

1. Clone este repositório ou copie o conteúdo de `dark-mode.css`, `s3.js` e `index.html` para o seu bucket S3.
2. Atualize as variáveis `bucketName` e `s3Domain` em `s3.js` com o nome do seu bucket e o domínio do seu provedor S3.
3. Configure as configurações do seu bucket S3 (veja a seção abaixo).
4. Acesse o arquivo `index.html` no seu navegador e voilà! 🎩✨ Você agora tem uma lista de diretórios S3 elegante.

## Configurações do Bucket S3 (AWS) 🔧

Para fazer essa mágica funcionar, você precisa configurar corretamente as configurações do seu bucket S3. Os seguintes passos se aplicam aos buckets S3 da AWS, mas podem ser diferentes dependendo do seu provedor S3:

1. Certifique-se de que seu bucket S3 é acessível publicamente (ou pelo menos acessível aos usuários com quem deseja compartilhar a lista de diretórios).
2. Defina a política do bucket para permitir acesso de leitura pública aos seus objetos. Use a seguinte política, substituindo `<nome-do-seu-bucket>` pelo nome real do seu bucket:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "S3DirectoryListing",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::<nome-do-seu-bucket>/*",
                "arn:aws:s3:::<nome-do-seu-bucket>"
            ]
        }
    ]
}
Ou você pode usar uma Política de IP para o seu bucket, se precisar.

json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "S3DirectoryListing",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::<nome-do-seu-bucket>/*",
                "arn:aws:s3:::<nome-do-seu-bucket>"
            ],
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": "<seu-endereço-ip>"
                }
            }
        }
    ]
}
Substitua <seu-endereço-ip> pelo endereço IP desejado ou um bloco CIDR para restringir o acesso a endereços IP específicos.

Ative o hospedagem de site estático para o seu bucket:
Acesse as configurações do seu bucket S3 no Console de Gerenciamento da AWS.
Selecione a guia "Propriedades".
Role para baixo até "Hospedagem de site estático" e clique em "Editar".
Escolha "Ativar" e defina o "Documento de índice" e "Documento de erro" como index.html.
Salve suas alterações.
Atualize suas configurações de Cross-origin resource sharing (CORS) como abaixo.
css
Copy code
[    {        "AllowedHeaders": [            "*"        ],
        "AllowedMethods": [
            "GET"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]
Anote o endpoint do site estático do bucket (por exemplo, http://<nome-do-seu-bucket>.s3-website-<sua-região>.amazonaws.com/index.html ou https://<nome-do-seu-bucket>.s3.amazonaws.com/index.html para conexão segura). Aqui é onde você pode acessar sua elegante lista de diretórios.
É isso! Agora você pode desfrutar da sua nova e elegante lista de diretórios S3!

Um Pouco Mais 
Você pode personalizar o número de itens mostrados por página modificando a variável itemsPerPage em s3.js.

arduino
Copy code
const itemsPerPage = 10; // Altere este número para o número desejado de itens por página
Demonstração
http://petrosystemarchives.s3-website-sa-east-1.amazonaws.com