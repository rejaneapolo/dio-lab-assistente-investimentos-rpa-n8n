# Decisões do Desafio Assistente de Investimento	
O Objetivo do projeto é com base nos dados fornecidos de clientes e opções de investimento, enviar sugestões de aplicações personalizadas com maior rentabilidade conforme perfil de risco de cada cliente.

## Arquitetura
O workflow foi concebido com os seguintes nós:
- Webhook - Clientes: ponto de entrada que recebe os dados cadastrais via requisição POST.
- HttpRequest - BuscarInvestimento: consulta a API externa especificada para obter o catálogo de investimentos disponíveis.
- Code - NormalizaDados: processa e une os dados clientes e investimento com base na chave perfil, preparando a estrutura em formato tabular para a etapa seguinte
- AI Agent (com Google Gemini Chat Model): utilizado para analisar o perfil do cliente e redigir uma mensagem de recomendação personalizada e empática.
  - Prompt utilizado:
    <img width="1503" height="514" alt="image" src="https://github.com/user-attachments/assets/63a6139e-e512-4f27-99ad-81648a4dfb3f" />
- Code Javascript (Normalização e Parse JSON): executa o tratamento e a limpeza da saída do agente de IA (removendo blocos de marcação markdown como ````json), garantindo a conversão segura para um objeto estruturado com os campos assunto` e `body_html`.
- Send a message (Gmail): envia o e-mail formatado em HTML diretamente pela conta autenticada via OAuth2
- Wait: inserido estrategicamente após o envio para introduzir uma pausa de 5 segundos entre cada iteração, prevenindo bloqueios de rate limiting por parte do Gmail em listas maiores
- Imagem do Worflow final:
<img width="1529" height="416" alt="image" src="https://github.com/user-attachments/assets/b11e19e5-be92-49da-b5a8-7406176b7a3b" />


