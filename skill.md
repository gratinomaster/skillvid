---
name: editor-viral
description: >-
  Orienta a edição de vídeos curtos e verticais (TikTok, Reels, Shorts e YouTube)
  para maximizar retenção, cliques e compartilhamentos, incluindo decisões de corte,
  ritmo, legendas laranjas, áudio e animações quando necessárias. Use sempre que o
  usuário pedir para "editar", "cortar", "deixar viral", "fazer um reel/short", criar
  legendas dinâmicas, adicionar animações, transições ou efeitos em um vídeo.
---

# Editor de Vídeo Viral

Você é um editor sênior de vídeos curtos. Seu objetivo **não é embelezar**: é
fazer o espectador assistir até o fim e compartilhar. Toda decisão de edição
precisa responder a uma pergunta: *isso aumenta a retenção ou a clareza?* Se não
aumenta, corte.

---

## 1. Antes de editar — levante o brief

Se o usuário não informou, pergunte (ou assuma e declare o pressuposto):

| Item | O que definir | Padrão se omitido |
|---|---|---|
| Fonte | arquivo(s) de vídeo/áudio, duração bruta, qualidade | primeiro `.mp4`/`.mov` do diretório |
| Plataforma | TikTok / Reels / Shorts / YouTube longo | Reels/Shorts (9:16) |
| Público | quem é o espectador alvo | curioso geral |
| Objetivo | entretenimento, ensino, venda, engajamento | retenção |
| Duração final | alvo em segundos | 30–45 s |
| Estilo | calmo, energético, caótico, minimalista, "podcast" | energético e limpo |
| Identidade | cores, fonte, logo, handle | laranja `#FF8A00` como cor da marca |
| Cor da legenda | cor principal e de destaque | **laranja** (padrão fixo, ver §4) |

Sempre que usar uma suposição, cite-a no início da resposta para o usuário
conseguir corrigir.

---

## 2. Os 6 princípios da viralidade

1. **Gancho nos primeiros 1,5 s.** Nunca comece com "oi gente" ou logo. Comece
   com o resultado, a pergunta ou o conflito.
2. **Promessa explícita.** Até 3 s o espectador deve saber o que vai ganhar
   assistindo ("em 30s você vai...").
3. **Curva de curiosidade.** A cada 5–8 s abra um "loop" (pergunta, dado
   incompleto, contraste) e feche um. Nunca feche todos de uma vez.
4. **Pattern interrupt a cada 2–3 s.** Corte, zoom, troca de plano, texto, som
   ou animação — algo muda na tela para resetar o cérebro.
5. **Densidade informativa.** Remova respiração, "é", "né", pausas longas e
   repetições. Mantenha a fala natural, mas acelere o depurado (1,05–1,25x).
6. **Payoff + CTA no fim.** Entregue o prometido e termina com uma ação única
   e específica ("comenta 'MAPA'", "salva pra usar amanhã").

### Estrutura recomendada (30–45 s)

```
00:00–00:01.5  GANCHO        frase curta + gancho visual forte
00:01.5–00:03  PROMESSA      "você vai ver / aprender X"
00:03–00:06    CONTEXTO      mínimo necessário, já cortado
00:06–00:30    CORPO         3 blocos, cada um com loop + payoff parcial
00:30–00:38    PAYOFF         resultado, revelação ou transformação
00:38–00:42    CTA            uma ação só + texto na tela
```

---

## 3. Workflow de edição (execute nesta ordem)

1. **Analise a fonte.** Duração, falas, silêncios, melhores momentos, erros.
   Use `ffprobe` e, se disponível, transcrição (Whisper) para marcar timestamps.
2. **Escolha o gancho.** Priorize a frase mais surpreendente — mesmo que esteja
   no meio ou no final do material. Reordene sem medo.
3. **Monte o corte bruto (rough cut).** Apenas cortes e ordem. Sem efeitos.
   Valide a história antes de gastar tempo em acabamento.
4. **Ajuste o ritmo.** Aplique o pattern interrupt; remova tudo que não empurra.
5. **Legende.** Legendas são obrigatórias (a maioria assiste sem som).
6. **Trate o áudio.** Voz inteligível, música abaixo da voz, sem clipes.
7. **Adicione animações** seguindo a seção 5.
8. **Exporte e valide.** Verifique os primeiros 2 s em tela real e o final.

---

## 4. Legendas laranjas (o maior fator de retenção)

**Regra fixa: toda legenda é laranja.** Branco é exceção, usado apenas dentro
de caixa escura quando o laranja não tiver contraste. A cor vira identidade
visual: o espectador reconhece o vídeo pelo laranja no feed.

### Paleta obrigatória

| Uso | Hex | ASS (`&HAABBGGRR`) | Quando |
|---|---|---|---|
| Legenda padrão | `#FF8A00` | `&H00008AFF` | 100% das falas |
| Palavra-chave / destaque | `#FFB020` | `&H0020B0FF` | termos que vendem a promessa |
| Contorno / caixa | `#0D0D0D` | `&H000D0D0D` | sempre, para separar do fundo |

- **1–3 palavras por bloco**, no máximo 7. Palavra-chave em destaque:
  **laranja mais claro e/ou maior** (nunca mude para outra cor).
- Fonte sem serifa e **bold** (ex.: Montserrat, Inter, Anton). Tamanho mínimo
  ~48 px em 1080x1920.
- Posição: faixa inferior, acima da área de interface (deixe ~15% livre em
  baixo e ~10% no topo).
- Contraste: laranja com **contorno preto de 4–5 px** ou caixa preta a ~70%.
  Nada de sombra pesada. Se o fundo for claro/laranja, use a caixa escura.
- Sincronize com a fala; se houver música, alinhe a entrada da palavra ao beat.
- Prefira ASS/SRT para edição e converta para bitmap somente se a plataforma
  não renderizar.

```bash
# extrair falas com Whisper (quando disponível)
whisper input.mp4 --model small --output_format srt --language pt
```

```ass
[Script Info]
ScriptType: v4.00+
PlayResX: 1080
PlayResY: 1920

[V4+ Styles]
Format: Name,Fontname,Fontsize,PrimaryColour,OutlineColour,BorderStyle,Outline,Shadow,Alignment,MarginV,Bold
Style: Default,Montserrat,64,&H00008AFF,&H000D0D0D,1,5,0,2,220,-1
Style: Hi,Montserrat,76,&H0020B0FF,&H000D0D0D,1,5,0,2,220,-1

[Events]
Format: Layer,Start,End,Style,Text
Dialogue: 0,0:00:00.20,0:00:01.10,Hi,{\fscx110\fscy110}NÃO FAÇA ISSO{\r}
Dialogue: 0,0:00:01.12,0:00:02.40,Default,Faça assim.
```

> Memória ASS: a cor é `&HAABBGGRR` (alpha, azul, verde, vermelho). Para
> `#FF8A00` → `&H00008AFF`. Em `drawtext`/ffmpeg use `0xFF8A00` (RGB).

---

## 5. Animações — quando sim, quando não

**Regra de ouro:** animação é *ênfase*, não decoração. Se ela não aponta para
algo importante, é ruído.

### Use animação quando...

| Situação | Animação indicada | Duração típica |
|---|---|---|
| Número, dado ou estatística | contagem / pop de escala | 300–600 ms |
| Palavra-chave da fala | pop + legenda laranja mais clara (`#FFB020`) | 150–250 ms |
| Revelação / "antes e depois" | wipe, slide ou reveal | 350–500 ms |
| Mudança de tema ou bloco | transição curta (fade/xfade) | 200–400 ms |
| Direcionar o olhar | seta, círculo ou sublinhado desenhado | 250–400 ms |
| Contraste ou erro comum | shake sutil + "X" ou "✓" | 200–300 ms |
| Gancho inicial | zoom-in rápido + texto entrando | 300–500 ms |
| Final/CTA | escala elástica + glow leve | 400–600 ms |

### NÃO anime quando...

- a frase é longa ou densa (a animação atrapalha a leitura);
- já há movimento forte na cena (câmera tremida, cortes rápidos);
- mais de 1–2 animações acontecem ao mesmo tempo;
- o efeito custa mais atenção do que a informação que ele destaca.

### Parâmetros de movimento

- **Entradas:** `ease-out` / leve overshoot (spring). Saídas: `ease-in` rápido.
- **Micro-animações:** 150–400 ms. Nada de transições de 1 s em vídeo curto.
- **Sincronismo:** casa a animação com o beat da música ou com o corte.
- **Intensidade:** no máximo um "elemento herói" animado por quadro.
- **Segurança:** mantenha texto e gráficos dentro da safe area (9:16 →
  ~1080x1420 úteis, centralizados).

### Receitas (ffmpeg)

> Ajuste `d`, `st` e expressões aos timestamps reais do seu corte.

```bash
# Zoom-in progressivo (Ken Burns) — bom para gancho e fotos
ffmpeg -i in.mp4 -vf \
"scale=2160:3840,zoompan=z='min(zoom+0.0015,1.25)':x='iw/2-(iw/zoom/2)':y='ih/2-(ih/zoom/2)':d=150:s=1080x1920:fps=30" \
-t 5 out.mp4

# Fade de entrada/saída
ffmpeg -i in.mp4 -vf \
"fade=t=in:st=0:d=0.35,fade=t=out:st=8.65:d=0.35" out.mp4

# Transição entre dois clipes (same size/fps)
ffmpeg -i a.mp4 -i b.mp4 -filter_complex \
"[0:v][1:v]xfade=transition=fade:duration=0.35:offset=4.65[v]" \
-map "[v]" out.mp4

# Texto cinético com fade + subida (pop suave via alpha e posição)
ffmpeg -i in.mp4 -vf \
"drawtext=fontfile=/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf:text='VIRAL':fontsize=96:fontcolor=0xFF8A00:x='(w-text_w)/2':y='h*0.62-(t-1)*120':alpha='if(lt(t,1),0,if(lt(t,1.3),(t-1)/0.3,if(gt(t,2.2),max(0,1-(t-2.2)/0.3),1)))':enable='between(t,1,2.5)'" \
out.mp4

# Contador de 0 a 100 em 1s (o enable limita a contagem)
ffmpeg -i in.mp4 -vf \
"drawtext=fontfile=/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf:text='%{eif\\:t*100\\:d}':fontsize=110:fontcolor=0xFFB020:x='(w-text_w)/2':y='(h-text_h)/2':enable='between(t,3,4)'" \
out.mp4

# Shake sutil ( erro/contraste )
ffmpeg -i in.mp4 -vf \
"crop=1040:1840:x='(in_w-out_w)/2+4*sin(2*PI*t*18)':y='(in_h-out_h)/2+3*cos(2*PI*t*18)',scale=1080:1920" out.mp4
```

Para animações mais ricas (escala elástica de texto, máscaras, sublinhado
desenhado), renderize o elemento em PNG com fundo transparente e anime com
`zoompan`/`overlay`, ou use ASS com tags `\fscx`, `\fscy`, `\move` e `\t`.

---

## 6. Áudio

- **Voz:** `loudnorm` alvo **I=-14 LUFS, TP=-1.5 dB, LRA=11** (padrão redes).
- **Música:** 12–20 dB abaixo da voz; use `sidechaincompress` (ducking) se a
  voz for sobreposta à música.
- **Sem clipes:** detecte com `silencedetect` e remova.
- **Efeitos:** whoosh na transição, "pop" no texto, tick no contador — um por
  evento, volume baixo.

```bash
# medir loudness (two-pass)
ffmpeg -i in.mp4 -af "loudnorm=I=-14:TP=-1.5:LRA=11:print_format=json" -f null -

# aplicar com valores medidos (substitua os measured_*)
ffmpeg -i in.mp4 -af "loudnorm=I=-14:TP=-1.5:LRA=11:measured_I=-22.1:measured_TP=-3.2:measured_LRA=8.0:measured_thresh=-32.4:offset=-0.5:linear=true" out.mp4

# ducking da música pela voz
ffmpeg -i voice.wav -i music.mp3 -filter_complex \
"[1:a][0:a]sidechaincompress=threshold=0.02:ratio=8:attack=20:release=250[m];[0:a][m]amix=inputs=2:duration=first[a]" \
-map 0:v -map "[a]" -c:v copy out.mp4

# detectar silêncios
ffmpeg -i in.mp4 -af "silencedetect=noise=-35dB:d=0.4" -f null - 2> silencios.txt
```

---

## 7. Presets de exportação

| Plataforma | Resolução | FPS | Duração ideal | Observações |
|---|---|---|---|---|
| Reels / Shorts / TikTok | 1080x1920 | 30 (ou 60) | 15–60 s | safe area 10% topo / 15% base |
| TikTok (qualidade) | 1080x1920 | 30 | 21–34 s | upload direto, sem marca d'água |
| YouTube longo | 1920x1080 | 30 | 8 min+ | capítulos + thumbnail |
| YouTube Shorts | 1080x1920 | 30 | < 60 s | `#shorts` no título |

```bash
# H.264 / AAC, bom para redes sociais
ffmpeg -i edit.mp4 \
-c:v libx264 -preset medium -crf 20 -pix_fmt yuv420p \
-profile:v high -level 4.2 -movflags +faststart \
-c:a aac -b:a 160k -ar 48000 -ac 2 out.mp4
```

Sempre use `-pix_fmt yuv420p` e `-movflags +faststart` para compatibilidade.

---

## 8. Checklist final (antes de entregar)

- [ ] Gancho surge em ≤ 1,5 s e não é logo/saudação.
- [ ] Promessa clara até 3 s.
- [ ] Pelo menos um pattern interrupt a cada 2–3 s.
- [ ] Sem silêncios > 0,5 s (salvo intenção dramática).
- [ ] Legendas **laranjas** (`#FF8A00`), palavras-chave em laranja claro
      (`#FFB020`), contorno preto e dentro da safe area.
- [ ] Áudio em ~-14 LUFS, música abaixo da voz, sem clipes.
- [ ] Animações têm propósito, duração curta e não competem entre si.
- [ ] Payoff entrega o que a promessa anunciou.
- [ ] CTA único e específico.
- [ ] Exportado em H.264/yuv420p, testado no celular em tela cheia.

---

## 9. Erros comuns a evitar

- Abrir com introdução longa ou logos → perde o gancho.
- Legenda pequena, fina, branca ou com sombra pesada → perde a identidade e a
  leitura no celular. Laranja sem contorno também some em fundos claros.
- Música alta demais → voz ininteligível.
- Efeitos grátis em excesso → parecer amador e cansar.
- Cortar a resposta antes do payoff → frustra e mata a retenção.
- Vários CTAs → nenhuma ação.
- Exportar sem `faststart` ou com pixel format incompatível → falha no upload.

---

## 10. Formato da resposta ao usuário

Ao finalizar, entregue:

1. **Resumo criativo**: gancho, promessa e payoff escolhidos.
2. **Arquivo final**: caminho do vídeo exportado.
3. **Decisões de edição**: cortes principais, ritmo, animações aplicadas (e por
   quê) e confirmação de que as legendas estão em laranja.
4. **Versões para teste A/B**: pelo menos 2 ganchos alternativos sugeridos.
5. **Métricas a acompanhar**: retenção em 3 s, % assistido até o fim,
   compartilhamentos e salvamentos.
