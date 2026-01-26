# COMANDO PARA NOVO PROJETO

## 📋 Instalação das Regras

### Opção 1: Se você tem o repositório local

**Copie todos os arquivos `.mdc` de:**
```
[seu-caminho]\__START__\00 - CURSOR - REGRAS\
```

**Cole em:**
```
[seu-projeto]\.cursor\rules\
```

**Nota:** Ajuste `[seu-caminho]` para o caminho onde você tem o repositório do framework.

### Opção 2: Em outro computador (via GitHub)

1. Baixe o repositório:
   ```bash
   git clone https://github.com/wilscot/METAPROMPT.git
   ```

2. Copie os arquivos `.mdc` de:
   ```
   METAPROMPT/00 - CURSOR - REGRAS/
   ```

3. Cole em:
   ```
   [seu-projeto]/.cursor/rules/
   ```

### Opção 3: Download manual do GitHub

1. Acesse: https://github.com/wilscot/METAPROMPT/tree/main/00%20-%20CURSOR%20-%20REGRAS
2. Baixe cada arquivo `.mdc` clicando nele e depois em "Raw" → Salvar
3. Salve todos em `[seu-projeto]/.cursor/rules/`

---

## ✅ Arquivos que devem ser copiados:

- 00-universal-code-standards.mdc
- 01-ask-first.mdc
- 02-dependencies.mdc
- 03-tool-selection.mdc
- 04-file-size.mdc
- 05-external-database.mdc

**Total: 6 regras**

---

## ⚠️ IMPORTANTE

**Quando instalar:**
- ✅ Pode ser a qualquer momento após ter `escopo.md`
- ✅ **DEVE estar completo ANTES de começar a codar no Cursor**
- ⚠️ Regras são só para Cursor, não afetam geração de artifacts na Web

**Validação:**
Após copiar, verifique:
```bash
ls .cursor/rules/*.mdc | wc -l
# Deve retornar: 6
```

**Nota:** Crie a pasta `.cursor/rules/` se não existir.

Pronto! As regras estarão ativas no projeto.
