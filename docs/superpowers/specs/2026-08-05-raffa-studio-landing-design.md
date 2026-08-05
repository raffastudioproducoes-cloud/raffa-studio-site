# EspecificaÃ§Ã£o da landing page da Raffa Studio

## Objetivo

Apresentar os aplicativos da Raffa Studio, a empresa e sua filosofia de desenvolvimento. A pÃ¡gina serÃ¡ o ponto central para downloads, contato, credibilidade e novos produtos.

## Escopo da primeira versÃ£o

1. Hero com marca, mensagem principal e links para aplicativos e contato.
2. Aplicativos em destaque. O MinhaRota entra como produto em desenvolvimento, com campos prontos para imagem, descriÃ§Ã£o, plataformas, recursos e links.
3. Ecossistema Raffa Studio: apps, IA, automaÃ§Ã£o, ferramentas e produtos digitais.
4. ApresentaÃ§Ã£o do desenvolvedor e da visÃ£o de produto.
5. Compromissos tÃ©cnicos: privacidade, seguranÃ§a, estabilidade, desempenho, qualidade e acessibilidade.
6. Tecnologias usadas.
7. Contato por links externos. Um formulÃ¡rio prÃ³prio sÃ³ entra quando houver um serviÃ§o de envio definido.
8. RodapÃ© com polÃ­tica de privacidade, termos, LGPD e copyright.

## Posicionamento e tom

Mensagem-base: "Aplicativos inteligentes. AutomaÃ§Ãµes Ãºteis. SoluÃ§Ãµes digitais construÃ­das com engenharia de software profissional."

O texto deve ser direto, tÃ©cnico quando necessÃ¡rio e sem promessas que nÃ£o possam ser verificadas. Campos sem informaÃ§Ã£o devem ser omitidos, nÃ£o preenchidos com conteÃºdo genÃ©rico.

## Identidade visual

| Elemento | Valor |
| --- | --- |
| Fundo principal | `#050505` |
| SuperfÃ­cies | `#0B0B0B` |
| Bordas | `#1E1E1E` |
| Verde principal | `#00E676` |
| Verde secundÃ¡rio | `#00C853` |
| Texto | `#FFFFFF` |
| Texto secundÃ¡rio | `#BDBDBD` |

Sora serÃ¡ usada em tÃ­tulos e Inter em textos longos. O preto domina a composiÃ§Ã£o; o verde indica foco, links e aÃ§Ãµes principais.

## Arquitetura

- Next.js com App Router, TypeScript strict e Tailwind CSS.
- Dados de aplicativos em arquivos TypeScript tipados, separados da interface.
- Componentes por responsabilidade: navegaÃ§Ã£o, hero, card de aplicativo, ecossistema, apresentaÃ§Ã£o, compromissos tÃ©cnicos, tecnologias, contato e rodapÃ©.
- Imagens otimizadas com `next/image`. AnimaÃ§Ãµes sutis respeitam `prefers-reduced-motion`.
- GitHub Ã© a fonte do cÃ³digo e Vercel Ã© a plataforma de preview e publicaÃ§Ã£o.

## SeguranÃ§a e qualidade

- Sem segredos no repositÃ³rio ou no cÃ³digo do navegador.
- Headers de seguranÃ§a configurados na Vercel, incluindo CSP compatÃ­vel com os recursos usados.
- Links externos com `rel="noreferrer"` quando abrirem uma nova aba.
- FormulÃ¡rios validam e sanitizam entradas no servidor quando forem implementados.
- HTML semÃ¢ntico, contraste adequado, foco visÃ­vel e navegaÃ§Ã£o por teclado.
- Metas de desempenho: Lighthouse acima de 95 em produÃ§Ã£o, sujeito Ã  validaÃ§Ã£o apÃ³s o primeiro deploy.

## Escalabilidade

O catÃ¡logo de aplicativos serÃ¡ a fonte de dados inicial. Quando o conteÃºdo crescer, ele poderÃ¡ migrar para CMS sem reescrever a interface. As futuras rotas previstas sÃ£o `/apps/[slug]`, `/docs`, `/blog`, `/changelog` e `/suporte`.

