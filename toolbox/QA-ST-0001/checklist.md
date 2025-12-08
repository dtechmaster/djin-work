# ✔ CHECKLIST IMPRIMÍVEL — QA-ST-0001

**[← Voltar ao Standard Completo](../../standards/pt-BR/QA/QA-ST-0001.md)**

---

### **ANTES DE COMEÇAR**

☐ Ambiente declarado (in-house-preview / customer-preview / production)
☐ Credenciais anotadas (ID + senha)
☐ Nome exibido verificado (para testes de ordem de nome)

---

## **1. Traduções**

☐ Textos completos validados no DeepL
☐ Palavras soltas validadas no Takoboto
☐ Ordem dos nomes conforme idioma da UI
☐ Avatar + Nome exibidos corretamente

---

## **2. Spellcheck**

☐ Nenhum typo na UI
☐ Nenhum typo visível de backend
☐ Traduções x→JA conferidas no DeepL
☐ Palavras soltas conferidas no Takoboto

---

## **3. Dados Básicos**

☐ Nenhum placeholder (“aaa”, “test”, lorem ipsum)
☐ Nada ofensivo
☐ Nomes fictícios adequados (JP/BR)

---

## **4. Tradução da Interface**

☐ Botões no idioma correto
☐ Nada perdido em pt-BR
☐ Nada perdido em inglês
☐ Ordem do nome ok

---

## **5. Vazamentos (Leaks)**

☐ Nenhum UUID aparecendo
☐ Nenhum ID interno
☐ Nenhum stacktrace
☐ Nada como undefined/null/[object Object]
☐ Sem erro de API cru
☐ Sem mensagens técnicas expostas

---

## **6. Layout**

Testes em:

* ☐ Desktop
* ☐ iPhone-width (~390px)

Checar:
☐ Nada estoura container
☐ Nenhum scroll lateral
☐ Botões clicam
☐ Listas carregam

---

## **7. Fluxo Principal**

Para cada tela:
☐ Entrar no fluxo principal (CTA)
☐ Criar 1 item
☐ Editar
☐ Apagar
☐ Fluxo não trava
☐ Layout não quebra
☐ Navegação ok
☐ Nenhum alerta feio

---

## **8. Ortografia e Mensagens**

☐ Mensagens claras
☐ Sem vergonha de mostrar ao cliente
☐ Títulos e descrições minimamente profissionais

---

## **9. Cores e Branding**

☐ Sem cores fora do padrão
☐ Sem Vuetify cru
☐ Sem contraste ruim

---

## **10. Evidências**

☐ 1 screenshot por tela
☐ 1 vídeo curto do fluxo principal
☐ Teste final:

> “Eu mostraria isso ao cliente sem medo?”
> ☐ Se não → corrigir / reportar

---

## **11. Escopo**

☐ O que foi corrigido está **dentro** do escopo
☐ Tudo que está **fora** do escopo foi listado como
**“Itens fora do escopo identificados”**
☐ Nada crítico deixado sem aviso

---

## **12. Recipes (se aplicável)**

☐ Verifiquei se existe recipe útil no repo / local permitidos
☐ Se não tenho acesso → segui manual
☐ Se existe recipe → executei dentro do escopo

---

# **RESULTADO FINAL**

### Escolher UM:

### ✔ Output 1 — Documentação + Passagem

☐ Problemas listados
☐ Evidências anexadas
☐ Task criada no Jira
☐ Aviso no Slack / Task
☐ Itens fora do escopo listados

### ✔ Output 2 — Correção + Registro

☐ Problemas corrigidos
☐ Evidências anexadas
☐ Aviso no Slack / Task
☐ Itens fora do escopo listados
