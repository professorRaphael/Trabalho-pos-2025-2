# Avaliação — Mini-Projeto Integrado em Python

* **Disciplina**: Linguagem Python
* **Professor**: Raphael Mauricio Sanches de Jesus
* **E-mail**: [raphael.jesus@estacio.br](mailto:raphael.jesus@estacio.br)
* **Período**: Pós-Graduação
* **Data de Entrega**: *26/10/2025*

---

## 😁 Exemplos para consulta, materia de aula no SAVA e:
    https://colab.research.google.com/drive/1zDGpev-fxv0rLcNEGymadpjpPZYhZIFD?usp=sharing 
    https://github.com/professorRaphael/exemplo-streamlit
    https://github.com/professorRaphael/streamlit_flask


## 🎯 Objetivo

Construir uma aplicação **enxuta** que una três pilares vistos em aula:

1. **Pandas** para ler um CSV e calcular estatísticas simples;
2. **FP (map/filter/reduce)** em um mini-desafio;
3. **API com FastAPI** para expor resultados.

> **Opcional (+)**: adicionar **POO (classes)** e uma **interface Streamlit** consumindo a API.

---

## ✅ Escopo mínimo (obrigatório)

### 1) Dados

* Use um CSV pequeno (pode ser o exemplo `produto,preco,qtd` ou outro com pelo menos **100 linhas** pode gerar aleatoriamente como visto em aula).
* Gere a coluna `receita = preco * qtd`.

### 2) Estatísticas (Pandas)

Calcule e salve em `stats.json` pelo menos:

* `qtd_total`, `receita_total`, `preco_medio`.

### 3) Mini-desafio FP (sem `for/while`, `sum`, `len`)

Implemente uma função:

```py
analisar(lista, limite) -> {"soma_quadrados": int, "contagem": int, "media_inteira": int}
```

Regras:

* filtre **pares > limite**,
* **eleve ao quadrado**,
* reduza acumulando **(soma, contagem)**,
* retorne a **média inteira** `soma // contagem` (0 se contagem=0).
  Use **apenas** `map`, `filter`, `reduce`.

> Aplique o desafio sobre uma coluna numérica do seu CSV (ex.: `qtd` com `limite=2`) e inclua o resultado dentro do `stats.json`.

### 4) API com FastAPI

Implemente:

* `GET /health` → `{"status": "ok"}`
* `GET /stats` → retorna o conteúdo de `stats.json`
* `POST /soma` → recebe `{"x": float, "y": float}` e retorna `{"resultado": x+y}`

> Dica: gere o `stats.json` com um script simples (`python src/make_stats.py`) **antes** de subir a API.

---

## 🧱 Organização sugerida do projeto

```
seu_projeto/
  data/
    dados.csv
  src/
    core/
      metrics.py         # função 'analisar' (FP)
      (opcional) modelos.py  # classes para POO (ver abaixo)
    make_stats.py        # lê CSV, calcula estatísticas e grava stats.json
    app.py               # FastAPI com /health, /stats, /soma
  stats.json             # gerado pelo make_stats.py
  requirements.txt
  README.md
```

---

## 🧠 OOP — Orientação a Objetos (opcional + recomendado)

Implemente **duas classes simples** (com *type hints* e docstrings):

* `DataLoader`: caminhos de arquivo, `load()` e validação das colunas mínimas;
* `StatsService`: recebe um `DataFrame` e expõe métodos: `qtd_total()`, `receita_total()`, `preco_medio()`, `desafio_fp(coluna, limite)` (reuso de `analisar`).

> Objetivo: mostrar **coesão** (cada classe cuida do seu papel) e facilitar testes.

---

## 🖥️ Streamlit (opcional)

Crie um app Streamlit que:

* Chame a API (`/stats`) e mostre os números na tela;
* Renderize 1 gráfico simples (histograma de `preco` ou `receita`);
* Permita testar o `/soma` via formulário.

> Você pode rodar **API** e **Streamlit** em terminais separados:
>
> ```bash
> # terminal 1
> python -m uvicorn src.app:app --reload
> # terminal 2
> streamlit run ui/app.py
> ```

---

## 🧪 Requisitos de entrega

* Repositório (GitHub/GitLab) com:

  * `data/dados.csv`, `src/` completo, `stats.json`, `requirements.txt`;
  * `README.md` com **como instalar**, **como gerar stats**, **como subir a API** e (se houver) **como rodar o Streamlit**;
  * 1 print da página **/docs** e 1 print do retorno de **/stats**.
* Código executando sem erros com `pip install -r requirements.txt`.

---

## 📝 Rubrica de avaliação (100 pts)

* **Funcionalidade básica (35 pts)**
  Estatísticas corretas em `stats.json` + API `/health` e `/stats` OK.
* **Desafio FP (map/filter/reduce) (20 pts)**
  Implementação correta, sem `for/while`, `sum`, `len`.
* **Qualidade/Organização (15 pts)**
  Estrutura mínima, nomes claros, README objetivo.
* **API — contrato e respostas (20 pts)**
  Endpoints respondendo JSON válido, mensagens de erro amigáveis.
* **POO (10 pts, bônus se opcional)**
  Pontos extras pela presença e bom uso de classes (`DataLoader`, `StatsService`).

### Pontos opcionais (+ até 10 pts)

* **Streamlit consumindo a API** (+5)
* **Gráfico simples (Matplotlib/Seaborn)** (+3)
* **Teste rápido (ex.: `pytest` para `analisar`)** (+2)

---

## 🚀 Passo a passo sugerido

1. Criar `requirements.txt` com: `fastapi`, `uvicorn`, `pandas`, `pydantic` (e opcional `streamlit`, `matplotlib`).
2. Implementar `analisar()` em `src/core/metrics.py`.
3. Fazer `src/make_stats.py` ler o CSV, calcular estatísticas e gravar `stats.json`.
4. Implementar `src/app.py` com `/health`, `/stats`, `/soma`.
5. (Opcional) Criar `src/core/modelos.py` com as classes de POO e adaptar `make_stats.py` para usá-las.
6. (Opcional) Criar `ui/app.py` (Streamlit) consumindo `http://127.0.0.1:8000/stats`.

---

## 📦 Exemplo de `requirements.txt`

```
fastapi
uvicorn
pandas
pydantic
# opcionais
streamlit
matplotlib
seaborn
```

---

## 🤝 Observações

* Trabalho **individual**.
* Dúvidas: por e-mail ou tel.
* Projetos fora do prazo seguem o regulamento da disciplina.

Boa prática e bom código!
