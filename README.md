# Percursos curriculares do MEFT

Site bilingue (PT/EN) com os percursos curriculares informais ("tracks") do
Mestrado em Engenharia Física Tecnológica do Instituto Superior Técnico.

O site é gerado automaticamente pelo **GitHub Pages** a partir dos ficheiros deste
repositório. Não há servidor nem software a instalar: tudo se edita no browser.

**Princípio:** cada informação está escrita **uma só vez**, com o português e o inglês
lado a lado. As páginas das duas línguas são geradas a partir dos mesmos dados.

---

## Onde está cada coisa

| Quero mudar…                                   | Ficheiro                                   |
|------------------------------------------------|--------------------------------------------|
| Coordenador/a, ano letivo, emails, data de revisão | `_data/coordination.yml`               |
| Lista de UCs (nome, ECTS, período, ligação Fénix, se funciona) | `_data/courses.yml`        |
| Percurso de uma área (UCs, responsável, textos) | `_data/areas/<área>.yml`                  |
| Texto da página inicial                        | `pt/index.md` e `en/index.md`              |
| Perguntas frequentes                           | `pt/contactos.md` e `en/contacts.md`       |
| Página "Sobre este site" (texto)               | `pt/sobre.md` e `en/about.md`              |
| Histórico das coordenações                     | `_data/coordination.yml` (lista `history`) |
| Menus e títulos das secções                    | `_data/i18n.yml` (raramente necessário)    |
| Logótipos (Técnico, MEFT)                      | ficheiros em `assets/img/` + `_data/logos.yml` |
| Imagem de cada área                            | `assets/img/areas/` + campo `image` em `_data/areas/<área>.yml` |
| Imagem de topo da página inicial               | `assets/img/home/` + `_data/home.yml`      |
| Ligações para o Técnico, Departamento, Fénix   | `_data/coordination.yml` (secção `links`)  |
| Cores e aspeto                                 | `assets/css/style.css`                     |
| Endereço do site                               | `_config.yml` (só na primeira publicação)  |

As pastas `_layouts/` e `_includes/` contêm os modelos das páginas. Não é preciso mexer nelas
para atualizar conteúdo.

---

## Tarefas habituais

### Quando muda a equipa de coordenação
1. Editar `_data/coordination.yml` (nome, email, ano letivo, data de revisão) e acrescentar
   a nova equipa **no topo** da lista `history` (aparece na página "Sobre este site").
2. Na organização do GitHub: **Settings → Members** → adicionar a nova equipa como *Owner*
   (e, se for o caso, retirar quem sai).

### No início de cada ano letivo
1. Em `_data/coordination.yml`, atualizar `academic_year` (ex.: `"2027/2028"`) e `last_review`.
2. Comparar `_data/courses.yml` com o
   [plano curricular no Fénix](https://fenix.tecnico.ulisboa.pt/cursos/meft21/curriculo):
   - períodos (`P1`…`P4`, ou `S1`/`S2` para UCs semestrais);
   - UCs que não funcionam nesse ano: acrescentar o ano em `not_offered`, por exemplo
     `not_offered: ["2027/2028"]`. Estas UCs aparecem automaticamente assinaladas.
3. Pedir às áreas científicas que revejam o seu ficheiro em `_data/areas/`.

### Uma área quer alterar o seu percurso
Editar `_data/areas/<área>.yml`. O comentário no início de `astro-gravitacao.yml` explica
todos os campos. As UCs são indicadas pelo identificador usado em `_data/courses.yml`:

```yaml
core:
  items:
    - course: fp                 # uma UC
    - one_of: [tqc, tnfp]        # escolher uma de várias
      note: { pt: "…", en: "…" } # nota opcional
tracks:
  - name: { pt: "Teoria", en: "Theory" }
    rule: { pt: "12 ECTS.", en: "12 ECTS." }
    items:
      - course: ms
      - free: { pt: "UC a escolher com o orientador", en: "A course chosen with the supervisor" }
```

A grelha por períodos e o índice de UCs são gerados automaticamente — não é preciso
desenhá-los.

### Acrescentar uma UC nova
1. Acrescentar uma entrada em `_data/courses.yml` (copiar uma existente e mudar os valores).
2. Referi-la no ficheiro da área com `- course: <identificador>`.

Se um identificador estiver mal escrito, a página mostra a vermelho
"UC desconhecida em _data/courses.yml".

### Acrescentar uma área nova
1. Copiar um ficheiro de `_data/areas/`, dar-lhe um nome novo (ex.: `interdisciplinar.yml`) e
   pôr o mesmo nome no campo `id`. Ajustar `order` e `color`.
2. Copiar `pt/areas/plasmas.md` para `pt/areas/interdisciplinar.md` e mudar as três linhas
   onde aparece `plasmas`. Fazer o mesmo em `en/areas/`.

### Logótipos e tipo de letra
Os logótipos do cabeçalho estão na pasta `assets/img/` e são configurados em `_data/logos.yml`:
- `logo-tecnico-df-pt.svg` / `logo-tecnico-df-en.svg` — identidade do Departamento de Física
  (em uso; versão portuguesa nas páginas PT e inglesa nas páginas EN);
- `logo-tecnico.svg` — logótipo principal do Técnico (alternativa; as instruções para trocar
  estão em `_data/logos.yml`);
- `logo-meft.png` — logótipo do MEFT.

Para trocar um logótipo, basta substituir o ficheiro (ou mudar o nome em `_data/logos.yml`).
Se o ficheiro não existir, o logótipo não aparece e o resto do site continua a funcionar.
Os logótipos do Técnico seguem a identidade de 2026 (tamanho mínimo em ecrã: 120 × 53 px):
<https://tecnico.ulisboa.pt/en/about-tecnico/institutional/logo-identity-standards/>

O tipo de letra é o Source Sans 3 (alternativa oficial da identidade do Técnico, licença OFL),
incluído em `assets/fonts/`.

### Imagens
- Cada área tem uma imagem em `assets/img/areas/` (ex.: `plasmas.jpg`), definida no campo `image`
  do ficheiro da área, com texto alternativo (`alt`), crédito e ligação para a origem.
- A imagem de topo da página inicial está em `assets/img/home/` e é definida em `_data/home.yml`.
- Se um ficheiro de imagem não existir, a imagem simplesmente não aparece.
- Usar imagens largas (paisagem), com pelo menos 1200 px de largura, e indicar sempre o crédito.

### Traduções
Todos os textos têm a forma `{ pt: "…", en: "…" }`. Se faltar o inglês, a versão inglesa
mostra o texto em português (nunca fica vazia).

---

## Como editar no GitHub (sem instalar nada)

1. Abrir o ficheiro no repositório e carregar no ícone do **lápis** (*Edit this file*).
2. Fazer a alteração.
3. Carregar em **Commit changes…** e escrever uma frase a descrever a mudança.
4. Esperar 1–2 minutos e recarregar o site.

Se o site não mudar, abrir o separador **Actions** do repositório:
- ✔ verde: está publicado (pode ser cache do browser — recarregar a página);
- ✘ vermelho: a alteração tem um erro e **a versão anterior continua online**. Normalmente é
  indentação no YAML. Corrigir, ou desfazer em **History** (ícone do relógio no ficheiro).

Regras básicas de YAML:
- indentar sempre com **espaços** (nunca tabulações), mantendo o alinhamento das linhas vizinhas;
- pôr textos entre aspas `"…"` (obrigatório se tiverem `:` ou `#`);
- elementos de listas começam por `- `.

Cada página de área tem no fundo a ligação **"Editar os dados desta área no GitHub"**, que
abre diretamente o ficheiro certo (é preciso ter acesso ao repositório). Os responsáveis das
áreas podem ser adicionados como colaboradores, ou propor alterações que a coordenação aprova.

---

## Primeira publicação

1. **Criar a organização no GitHub** (github.com → *+* → *New organization* → plano *Free*),
   registada com um email institucional da coordenação, e não com uma conta pessoal.
   Adicionar 2–3 *Owners* (ex.: coordenador/a e secretariado), para que o acesso nunca dependa
   de uma só pessoa.
2. **Criar um repositório público** chamado `tracks` dentro da organização.
3. **Carregar os ficheiros:** *Add file → Upload files* e arrastar **o conteúdo** desta pasta
   (as pastas `_data`, `_includes`, `_layouts`, `assets`, `pt`, `en` e os ficheiros soltos), não
   a pasta em si. Carregar em *Commit changes*.
4. **Ativar o GitHub Pages:** *Settings → Pages → Build and deployment → Source: Deploy from a
   branch*, escolher `main` e `/ (root)`, *Save*.
5. Ao fim de 1–2 minutos o site fica em `https://<organizacao>.github.io/tracks/`.
6. **Se usou outros nomes** de organização ou de repositório, editar em `_config.yml` os campos
   `url`, `baseurl` e `repository_url` (as instruções estão no próprio ficheiro).
7. **Divulgar:** pôr a ligação na página de descrição do MEFT no Fénix.

### Endereço tecnico.ulisboa.pt (opcional)
Pode pedir-se ao SI (si@tecnico.ulisboa.pt) um nome do tipo `percursos.meft.tecnico.ulisboa.pt`
com um registo **CNAME** a apontar para `<organizacao>.github.io`. Depois: *Settings → Pages →
Custom domain*, e em `_config.yml` mudar `url` para o novo endereço e `baseurl` para `""`.

### Alternativa: alojar no Técnico
O site é estático: a pasta gerada pelo Jekyll (`_site/`) pode ser copiada para uma página de
grupo do SI (`groups.tecnico.ulisboa.pt/<grupo>/`). Perde-se, no entanto, a edição no browser
e o histórico de alterações, por isso o GitHub é a opção recomendada.

---

## Notas técnicas

- Gerador: Jekyll, tal como é executado nativamente pelo GitHub Pages (sem plugins).
- Línguas: cada página tem `lang: pt|en` e um `ref` comum às duas versões, usado pelo botão
  de mudança de língua.
- Fonte dos dados iniciais (novembro de 2026): documentos enviados pelos coordenadores das
  áreas científicas e plano curricular MEFT21 no Fénix.
