# step_functions_aula_aws
**Projeto AWS Step Functions**

O objetivo deste projeto é criar um exemplo de workflow automatizado utilizando o AWS Step Functions que recebe arquivos armazenados no Amazon S3, verifica se são do tipo CSV e realiza ações diferentes conforme o resultado da validação. O fluxo também envia notificações automáticas via Amazon SNS em caso de falha no processamento.



**Serviços Utilizados no Projeto:**

| Serviço AWS           | Função no Projeto                                                      |
|----------------------|------------------------------------------------------------------------|
| AWS Step Functions   | Responsável pela orquestração de todas as etapas do fluxo.            |
| Amazon S3            | Utilizado para listar e armazenar os arquivos processados.            |
| Amazon SNS           | Responsável por enviar notificações em caso de erro ou falha no processamento. |


<p align="center">
<img width="544" height="500" alt="stepfunctions_aula_aws" src="https://github.com/user-attachments/assets/6e0cef15-60d2-44d2-b1e8-75841a463c2a" />
</p>


Fluxo das Funções:

1. ListObjectsV2

Descrição: Essa etapa simula o recebimento e leitura de arquivos em um bucket S3. Ela obtém as informações dos arquivos armazenados e encaminha o resultado para o próximo estado, onde será feita a verificação do tipo de arquivo

2. VerificarTipoArquivo

Descrição: Este é o ponto de decisão condicional do workflow. O Step Functions avalia o tipo do arquivo e define o caminho a seguir.

3. PutObject

Descrição: Essa etapa representa o armazenamento do arquivo processado ou validado. Utiliza o método putObject da API do S3 para enviar o conteúdo ao bucket MyData. 
Após essa etapa, o fluxo é finalizado com sucesso.

4. NotificarFalha

Descrição: Caso o arquivo analisado não seja CSV, o Step Functions publica uma notificação no SNS informando a falha. Isso é útil para alertar equipes de suporte ou sistemas de monitoramento sobre problemas no fluxo.

5. EncerrarComSucesso

É o estado final em caso de sucesso, encerrando o fluxo sem erros.

6. EncerrarComFalha

Descrição: É o estado final de falha, acionado quando o arquivo não atende à condição esperada (tipo diferente de CSV).

Obs: O código do projeto está anexado ao repositório.


