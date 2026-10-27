# CONTEXTO DO PROJETO — Coleção Biológica Interativa

Atualização: 26/10/2026. Documento para continuidade do desenvolvimento no Codex/VS Code e no ChatGPT.

## 1. Objetivo
Criar uma exposição educativa de exemplares reais da coleção biológica, apresentada por estudantes em uma feira de ciências. Cada exemplar possui um QR Code físico que abre, no celular do visitante, sua ficha individual com fotografia real, classificação, informações do acervo, morfologia, ecologia, curiosidades e uma pergunta investigativa. Este piloto poderá futuramente integrar o projeto maior **Laboratório de Biologia** e dialogar com a Exsicata Virtual e a Coleção de Zoologia.

## 2. Repositório, produção e implantação
- Repositório GitHub: https://github.com/flaviosal-create/feira-colecao-biologica
- Site publicado na Vercel: https://feira-colecao-biologica.vercel.app/
- Branch principal: `main`.
- Projeto atual: **site estático**, concentrado no arquivo `index.html`, com CSS e JavaScript incorporados e fotografias codificadas em data URIs/base64. Não pressupor que haja React, Next.js ou build.
- A Vercel está conectada ao GitHub; confirmar o deploy após alterações.
- É essencial preservar a correspondência entre `?exemplar=<slug>` e cada etiqueta impressa: os QR Codes já produzidos dependem dessas URLs.

## 3. Exemplares e links estáveis
| Nome popular | Identificação fornecida | Ordem / família | Slug do QR Code |
| --- | --- | --- | --- |
| Barata-d'água | *Lethocerus* sp. | Hemiptera / Belostomatidae | `lethocerus` |
| Mosca-assassina | *Mallophora* sp. | Diptera / Asilidae | `mallophora` |
| Barbeiro | *Panstrongylus tibiamaculatus* | Hemiptera / Reduviidae (Triatominae) | `panstrongylus` |
| Arrebenta-boi | *Cissites maculata* | Coleoptera / Meloidae | `cissites` |
| Borboleta-estaladeira | *Hamadryas feronia* | Lepidoptera / Nymphalidae | `hamadryas` |

Padrão de URL: `https://feira-colecao-biologica.vercel.app/?exemplar=lethocerus`, trocando o slug pelos demais. **Não alterar os slugs sem planejar a substituição de todos os QR Codes impressos.**

## 4. Dados dos exemplares
**Barata-d'água:** os dados de coleta foram informados diretamente pelo responsável e atualizados no GitHub:
- Data: **17/04/2026**.
- Local: **Unamar, Cabo Frio, RJ, Brasil**.
- Coletor: **Lucas Vasconcellos Araújo**.
- Preservação indicada no protótipo: exemplar seco/alfinetado.

Dados lidos inicialmente de rótulos fotografados (revisar transcrição contra os originais antes de uso definitivo):
- **Mosca-assassina:** rótulo com indicação IFF-CF, RJ; 17-X-2024; Araújo, L. V. col.
- **Barbeiro:** Cabo Frio, RJ; 22-X-2024; Araújo, L. V. col.
- **Borboleta-estaladeira:** Cabo Frio, RJ; 23.VIII.2018; Oliveira, F. P.; Gomes, T. C.
- **Arrebenta-boi:** dados de coleta ainda não confirmados.

Não inventar números de tombo, localidades, datas ou características não observadas. Registrar dúvidas taxonômicas quando a foto não permitir confirmação.

## 5. Fotografias — cuidado obrigatório
Foram recebidas fotografias do acervo e ocorreram trocas de associação entre imagens do **barbeiro/percevejo** e do **arrebenta-boi**. O usuário corrigiu essas associações mais de uma vez e indicou explicitamente a imagem a usar na ficha do arrebenta-boi. **Conferir visualmente as galerias com o responsável antes de considerar a identificação definitiva.** Evitar substituir fotos reais por imagens geradas. Preservar vistas dorsal, frontal e lateral apenas quando realmente correspondem ao espécime.

## 6. Experiência de visita escolhida
A experiência NÃO deve funcionar como um catálogo com abas para navegar livremente entre os insetos:
1. O visitante escaneia o QR Code físico na exposição.
2. Abre **somente a ficha desse exemplar**.
3. Ao terminar, seleciona **“Ver próximo inseto”**.
4. O site abre um leitor de QR Code e o visitante aponta a câmera para o próximo exemplar.
5. Após leitura válida, o leitor fecha e aparece a próxima ficha.
6. Há uma opção discreta **“Sair”** para encerrar a visita e mostrar agradecimento. Ela não deve tentar fechar a aba do navegador.
7. Quando aberto sem slug, mostrar uma tela inicial convidando à leitura de um QR Code, sem permitir navegação por lista.

Não voltar a colocar menus de espécies ou os três quadros informativos removidos (“Espécies já ilustradas”, “Arrebenta-boi”, “Uso na feira”).

## 7. Estado e problemas da câmera
Problemas reportados pelo usuário:
- Leitor de câmera inicialmente não conseguia ler os códigos em determinados celulares.
- Câmera era exibida abaixo do conteúdo, fora da área visível.

Última alteração aplicada ao `index.html` no GitHub:
- Leitor QR em **sobreposição de tela inteira**, em primeiro plano, com botão **“Fechar leitor”**.
- Troca do uso exclusivo da API `BarcodeDetector` pela biblioteca **html5-qrcode 2.3.8**, carregada via CDN (`cdn.jsdelivr.net`) quando o leitor é acionado.
- Uso de câmera traseira quando disponível; mensagens de permissão/falha; controle para liberar o stream.
- A leitura deve aceitar **somente QR Codes cujo endereço pertença ao próprio site** e cujo `exemplar` seja um dos cinco slugs válidos.
- A correção foi enviada ao GitHub, **mas ainda não foi validada em teste real no celular do usuário**. Não afirmar que o problema está definitivamente resolvido sem esse teste.
- Se falhar: verificar permissões, HTTPS, iOS/Safari e Android/Chrome, carregamento da biblioteca CDN, erros de console e funcionamento do encerramento do stream; oferecer câmera nativa do celular como alternativa.

## 8. Conteúdo e abordagem didática
- Textos científicos claros para visitantes, rigorosos para uso escolar, sem afirmar além dos dados disponíveis.
- Ficha inclui nome popular, nome científico, ordem, família, dados de coleta/preservação, morfologia, ecologia, curiosidades, pergunta “Observe e investigue”.
- Barbeiro: distinguir potencial vetorial da presença efetiva de *Trypanosoma cruzi*; jamais presumir infecção do exemplar.
- Arrebenta-boi: meloídeos podem apresentar defesa química; evitar incentivo ao manuseio.
- Em nomes científicos, utilizar grafia taxonômica correta (*Lethocerus*, não “Lethoceros”).
- Revisar português e formatação em todas as interfaces e materiais impressos.
- Creditar corretamente a participação docente e o apoio de IA, sem atribuir ao sistema uma validação científica não realizada.

## 9. Materiais de QR Code
Foram produzidas pranchas A4 e imagens individuais para impressão. Versões preliminares apresentaram QR Codes achatados e legendas pequenas; posteriormente foram refeitos mantendo códigos **quadrados** e fonte legível. Verificar legibilidade, ortografia e links com o celular antes de imprimir. Nenhuma alteração dos cinco slugs deve invalidar os códigos existentes.

## 10. Próximas tarefas sugeridas ao Codex
1. Examinar `index.html` no estado atual, sem sobrescrever fichas ou fotos.
2. Testar a experiência de leitura QR em aparelhos reais, especialmente abertura em primeiro plano, autorização da câmera, reconhecimento e encerramento do stream.
3. Corrigir defeitos com pequenas alterações verificáveis e responsivas; não depender exclusivamente de uma API experimental.
4. Verificar a associação foto/exemplar com o professor.
5. Validar a exibição dos novos dados da barata-d'água e dos demais rótulos.
6. Opcionalmente refatorar para CSS/JS/dados em arquivos separados, **preservando as URLs e a funcionalidade existente**, somente após testes.

## 11. Instrução para retomar no Codex
> Leia integralmente `CONTEXTO_PROJETO.md` e depois examine `index.html`. O projeto já está publicado na Vercel, possui cinco QR Codes físicos e precisa manter as URLs. Priorize correções do leitor de QR Code no celular e a fidelidade das fotos e dos dados científicos. Antes de mudanças substanciais, mostre quais arquivos e comportamentos serão modificados. Não reinicie o projeto nem remova funcionalidades já estabelecidas.
