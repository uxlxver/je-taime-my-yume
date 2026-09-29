# Je t'aime! My Yume!

Site estático de RPG romântico em tons pastéis com Groq. Até cinco histórias por navegador, 80 turnos enviados por dia (horário local do dispositivo), criação de protagonistas e pares românticos, editor Markdown e exportação JSON. Tudo fica no `localStorage` do navegador; não há conta nem sincronização.

## Publicar no GitHub Pages

1. Crie um repositório público no GitHub e envie `index.html`, `style.css`, `app.js` e `README.md` para a raiz da branch `main`.
2. No repositório, abra **Settings → Pages**. Em **Build and deployment**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`, e salve.
3. Acesse a URL informada pelo GitHub Pages após a publicação. Não envie sua chave Groq ao repositório; cada usuário a insere nas configurações do site.

## Observações

- O limite de 80 é aplicado localmente por dia civil do dispositivo, somado entre histórias. Sem servidor/autenticação, pode ser contornado ao limpar dados, mudar relógio ou usar outro navegador. Não acompanha o momento exato de renovação das cotas da Groq, que variam por conta/modelo.
- A chave da API fica legível para quem tiver acesso ao armazenamento do navegador. Em um site estático, requisições saem diretamente do navegador; para uma garantia robusta de cotas ou proteção de credenciais seria necessário um backend.
- O prompt restringe o papel da IA, mas modelos generativos podem falhar. O usuário deve revisar respostas antes de tratá-las como cânone.
- Exporte o JSON da história para backup. A chave não é incluída.

## Romance e personagens

Je t'aime! My Yume! exige idade de 18 a 120 anos para cada protagonista. O aniversário é opcional, no formato MM-DD. É possível informar identidade de gênero, pronomes, ícones, passados individuais e compartilhado e acontecimentos planejados. Estes planos são enviados ao modelo como contexto futuro, sem autorização para introduzi-los até o usuário fazê-lo.

A opção de intimidade adulta só solicita conteúdo consensual quando a política da Groq e o modelo permitirem. Restrições ou recusas do provedor prevalecem. O prompt exige consentimento atual para contato, respeito a recusas e nenhuma ação, fala ou pensamento do personagem do usuário. Essas são instruções ao modelo, não garantias absolutas.

A evolução da relação é guardada internamente como proximidade e confiança, atualizada a partir de um metadado gerado na mesma resposta; somente um sentimento breve aparece na interface. O modelo pode omitir o metadado, caso em que o estado permanece como estava. Nenhum marcador numérico é exibido.

## Revisão das respostas

A resposta gerada fica como prévia editável e não entra no histórico canônico até o usuário aceitá-la. É possível descartá-la; o turno enviado permanece e conta para o limite diário. Um detector bloqueia a aceitação de alguns formatos explícitos de fala atribuída ao protagonista e de metadados indevidos. Revise também ações, pensamentos, consentimento, NPCs, fatos e cronologia: nenhum detector local pode provar que uma resposta em linguagem natural cumpre todas as regras. Os sentimentos e o estado interno só são atualizados após aceitação.

## Memória, backup e controles de cena

A memória canônica contém resumo e fatos confirmados editados pelo usuário; acompanha cada chamada à Groq mesmo quando o histórico recente é recortado. Não é preenchida automaticamente para evitar transformar inferências do modelo em fatos. O botão de fato rápido acrescenta uma linha. Eventos futuros permanecem separados.

Configurações permite exportar todas as histórias em um arquivo JSON e importar backup individual ou conjunto (até cinco histórias no total, 5 MB por arquivo). A chave da API nunca é exportada. Backups importados são validados, recebem IDs novos e entram sem prévias pendentes. Faça cópias antes de limpar os dados do navegador.

Pausar impede novos envios. Voltar um turno aceito remove a última resposta e o turno anterior e restaura o estado interno da relação; o envio à Groq e a mensagem do dia não são devolvidos. Alertas na revisão marcam falas atribuídas ao protagonista, idades divergentes, possíveis falas de NPCs e datas ou horários sem confirmação; os demais itens exigem leitura humana.

A chamada à Groq usa JSON Schema estrito nos modelos GPT OSS oferecidos no seletor, separando resposta narrativa, sentimento, proximidade e confiança. O esquema garante a estrutura dos campos, não a veracidade ou obediência semântica. Configurações antigas com Llama são migradas para GPT OSS 120B. O painel da Groq registra localmente requisições e tokens retornados hoje e, quando o navegador puder ler os cabeçalhos, mostra cotas restantes de requisições por dia e tokens por minuto. Estes números pertencem à organização na Groq e independem das 80 mensagens do site.

## Limites técnicos verificados

O site reage a alterações do armazenamento em outra aba, mas duas requisições exatamente simultâneas ainda podem concorrer; uma cota inviolável e sincronização entre dispositivos exigem servidor. Quando o armazenamento local se esgota, o chat cancela o envio antes da API; se o espaço acabar após a resposta, mantém a prévia na aba e avisa para exportar antes de fechá-la.

## Uso em Android e iOS

O layout móvel usa alvos de toque maiores, campos de 16 px, ações do chat com rolagem horizontal, área segura inferior e ajuste de altura pelo VisualViewport quando o teclado está aberto. Há fallback de `vh` para navegadores sem `dvh`. O projeto foi verificado por análise de CSS e simulação do evento de viewport; antes da publicação, confirme em Chrome para Android e Safari para iOS reais a abertura do teclado, a rolagem do formulário e o envio de uma mensagem à Groq.
