# Exercício 6 - Unidade I: Manipulação de arquivos (texto e binário)

**Disciplina:** Algoritmo e Estrutura de Dados I - UFERSA - 2026.2
**Professora:** Rosana Rego
**Aluno:** Gabriel Duarte Martins

---

## Exercício 1 - Salvando o nome do jogador

```c
char nomeJogador[16] = "";
int tamNome = 0;
bool nomeConfirmado = false;

while (!nomeConfirmado && !WindowShouldClose()) {
    int c = GetCharPressed();
    while (c > 0) {
        if (c > 32 && c < 127 && tamNome < 15) {
            nomeJogador[tamNome++] = (char)c;
            nomeJogador[tamNome] = '\0';
        }
        c = GetCharPressed();
    }
    if (IsKeyPressed(KEY_BACKSPACE) && tamNome > 0) {
        nomeJogador[--tamNome] = '\0';
    }
    if (IsKeyPressed(KEY_ENTER) && tamNome > 0) {
        nomeConfirmado = true;
    }

    BeginDrawing();
    ClearBackground(RAYWHITE);
    DrawText("Digite seu nome e pressione ENTER:", 200, 200, 24, DARKGRAY);
    DrawText(nomeJogador, 200, 250, 30, MAROON);
    EndDrawing();
}
```

```c
void salvarPlacarTexto(const char *nome, int pontuacao) {
    FILE *arquivo = fopen(ARQUIVO_PLACAR, "a");
    if (arquivo == NULL) return;

    fprintf(arquivo, "%s %d\n", nome, pontuacao);
    fclose(arquivo);
}
```

```c
int lerMelhorPontuacao(void) {
    FILE *arquivo = fopen(ARQUIVO_PLACAR, "r");
    if (arquivo == NULL) return 0;

    char nomeLido[16];
    int melhor = 0, valor = 0;
    while (fscanf(arquivo, "%15s %d", nomeLido, &valor) == 2) {
        if (valor > melhor) melhor = valor;
    }
    fclose(arquivo);
    return melhor;
}
```

---

## Exercício 2 - Apagando o jogo salvo

```c
if (IsKeyPressed(KEY_DELETE)) {
    if (remove(ARQUIVO_SAVE) == 0) {
        snprintf(mensagem, sizeof(mensagem), "Save apagado com sucesso!");
    } else {
        snprintf(mensagem, sizeof(mensagem), "Nenhum save encontrado");
    }
    tempoMensagem = 3.0f;
}
```

```c
if (tempoMensagem > 0) {
    DrawText(mensagem, 20, 560, 20, DARKGREEN);
    tempoMensagem -= GetFrameTime();
}
```
