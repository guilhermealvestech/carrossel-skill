# Assets com image gen

O Claude não gera imagem. Monte o prompt e o usuário gera no Codex (que salva direto na pasta do projeto) ou no ChatGPT. Quem aprova é sempre o usuário.

**Image gen é só para assets**: um objeto ou uma composição com ambiente. Nunca a peça pronta (texto, layout e marca são feitos em HTML) e nunca pessoa real (personagem estilizado sem rosto pode).

## 1. Antes de gerar, descartar nesta ordem
1. Print ou markup real do produto.
2. Asset já existente em `carrosseis/assets/*/manifest.json`.
3. Composição em HTML/CSS (cards, chips, formas).

## 2. Tipos
| Tipo | Uso | Fundo |
|---|---|---|
| Objeto | metáfora num slide | transparente |
| Personagem | pessoa em situação, sem rosto | transparente |
| Cena | capa com contexto, área livre para título | cheio, 4:5 |
| Cenário | personagem dentro do ambiente, a série inteira | cheio, 4:5 |
| Ícone | chips e listas, legível em 64px | transparente |

O estilo padrão recomendado é **3D editorial fosco**: consistente, sem cara de banco de imagem e fácil de manter em série. Objeto realista (fotográfico) só em caso bem específico, quando o tema pede aquele objeto real.

### Cenário (cena com personagem)
Quando o roteiro é uma situação vivida, o asset é a **cena inteira**: personagem sem rosto dentro do ambiente, gerado de uma vez (nunca personagem e cenário separados para montar depois). Conceito ou metáfora continua com objeto.
- Texto no terço superior; cena embaixo, de borda a borda, sem card.
- Uma cena por série: mesmo personagem, set e luz. Muda enquadramento, pose e objetos, e o ambiente acompanha o texto.
- A primeira cena aprovada é a âncora das seguintes.
- Pessoa real nunca; personagem estilizado pode.

## 3. Anatomia do prompt
Uma linha por bloco, nesta ordem:
1. **Sujeito** concreto.
2. **Função:** onde entra e o que comunica.
3. **Âncora:** anexe a imagem aprovada da série ("siga exatamente o estilo da imagem anexada").
4. **Material e luz:** 3D fosco, plástico macio, cantos arredondados, luz de estúdio suave do alto à esquerda, sombra de contato leve.
5. **Paleta** em hex, de `marca.json`. No máximo um acento extra.
6. **Composição:** centralizado, ângulo 3/4, ~70% do quadro, margem livre.
7. **Fundo e tamanho:** transparente, PNG, 2048×2048 ou mais.
8. **Restrições:** sem texto, letras, logos, rosto, glossy, cromado, neon, sparkles.

## 4. Fluxo
1. **Uma imagem primeiro** (a âncora). O usuário aprova ou recusa.
2. Recusa: pergunte o que incomodou, mude **um** bloco do prompt e registre no `GOSTO.md`.
3. Aprovada: vira a âncora da série. As variações usam o mesmo prompt trocando só o sujeito.
4. Lote de até 10, sempre com a âncora anexada.
5. Checagem: fundo transparente de verdade, sem texto ou objeto estranho, mesma luz e ângulo, legível pequeno, 2048px ou mais.
6. Salvar em `carrosseis/assets/3d/<serie>/NN-nome.png` e registrar no `manifest.json` com o campo `use`.

## 5. Modelo
```
Crie um objeto 3D: [SUJEITO].
Uso: asset de carrossel da [MARCA] para comunicar [IDEIA].
Siga exatamente o estilo da imagem de referência anexada.
Estilo: 3D editorial fosco, plástico macio, cantos arredondados, luz de estúdio suave do alto à esquerda, sombra de contato leve.
Paleta: [PRIMÁRIA], [APOIO 1], [APOIO 2] e branco.
Composição: centralizado, ângulo 3/4, ocupando ~70% do quadro.
Fundo transparente, PNG, 2048x2048.
Não incluir: texto, letras, logos, rostos, brilho glossy, cromado, neon, sparkles.
```
Personagem: acrescente "pessoa sem traços faciais, proporções levemente estilizadas, roupa nas cores da marca, pose que mostra [AÇÃO]".
Cena: troque o fundo por "fundo cheio claro, proporção 4:5, área livre no terço superior para o título".
Cenário: "Crie uma cena 3D: [PERSONAGEM] [AÇÃO] em [AMBIENTE], com [OBJETOS QUE CONTAM A HISTÓRIA]. Personagem sem traços faciais, roupa nas cores da marca. Siga o personagem, o ambiente e a luz da imagem anexada. 4:5, terço superior livre, cena encostando nas bordas laterais e inferior."

No Codex, peça também: "salve em carrosseis/assets/3d/<serie>/NN-nome.png e me mostre".
