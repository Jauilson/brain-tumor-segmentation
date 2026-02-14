# 🚀 GUIA RÁPIDO: PUBLICAR PROJETO NO GITHUB

## 📋 PRÉ-REQUISITOS

- [ ] Conta no GitHub criada
- [ ] Git instalado no computador
- [ ] Todos os arquivos do projeto baixados

---

## 🎯 PASSO A PASSO COMPLETO

### 1️⃣ CRIAR REPOSITÓRIO NO GITHUB

1. Acesse [github.com](https://github.com)
2. Clique no botão **"+"** no canto superior direito
3. Selecione **"New repository"**
4. Preencha:
   - **Repository name:** `brain-tumor-segmentation`
   - **Description:** `Automated brain tumor segmentation in MRI images using U-Net deep learning architecture`
   - **Public** (deixe público para portfolio)
   - ✅ **Add a README file** (desmarque, pois já temos um)
   - **Add .gitignore:** None (já temos um)
   - **Choose a license:** MIT License (ou deixe vazio, já temos um)
5. Clique em **"Create repository"**

---

### 2️⃣ PREPARAR ARQUIVOS LOCALMENTE

```bash
# 1. Abra o terminal na pasta onde estão os arquivos
cd /caminho/para/brain-tumor-segmentation

# 2. Inicialize o repositório Git
git init

# 3. Adicione todos os arquivos
git add .

# 4. Faça o primeiro commit
git commit -m "Initial commit: Brain tumor segmentation project"

# 5. Renomeie a branch principal para 'main' (padrão do GitHub)
git branch -M main
```

---

### 3️⃣ CONECTAR AO GITHUB E FAZER UPLOAD

```bash
# Substitua 'SEU-USUARIO' pelo seu nome de usuário do GitHub
git remote add origin https://github.com/SEU-USUARIO/brain-tumor-segmentation.git

# Faça o push dos arquivos
git push -u origin main
```

**Se pedir autenticação:**
- Use seu **username** do GitHub
- Como senha, use um **Personal Access Token** (não a senha da conta)

---

### 4️⃣ CRIAR PERSONAL ACCESS TOKEN (se necessário)

1. GitHub → **Settings** (ícone do seu perfil)
2. No menu lateral, clique em **Developer settings**
3. Clique em **Personal access tokens** → **Tokens (classic)**
4. Clique em **Generate new token** → **Generate new token (classic)**
5. Preencha:
   - **Note:** `Brain Tumor Segmentation Upload`
   - **Expiration:** 90 days (ou customize)
   - **Scopes:** ✅ `repo` (marque todas as opções de repo)
6. Clique em **Generate token**
7. **COPIE O TOKEN** (você só verá uma vez!)
8. Use esse token como "senha" ao fazer push

---

### 5️⃣ VERIFICAR SE DEU CERTO

1. Acesse: `https://github.com/SEU-USUARIO/brain-tumor-segmentation`
2. Você deve ver todos os arquivos:
   - ✅ README.md
   - ✅ brain_tumor_segmentation.ipynb
   - ✅ requirements.txt
   - ✅ LICENSE
   - ✅ .gitignore
   - ✅ DOCUMENTATION_LATTES_LINKEDIN.md

---

## 📁 ESTRUTURA FINAL DO REPOSITÓRIO

```
brain-tumor-segmentation/
│
├── README.md                           # Documentação principal
├── brain_tumor_segmentation.ipynb     # Notebook principal
├── requirements.txt                    # Dependências
├── LICENSE                             # Licença MIT
├── .gitignore                          # Arquivos ignorados
├── DOCUMENTATION_LATTES_LINKEDIN.md    # Guia para currículo
│
└── results/                            # (opcional) Pasta para resultados
    ├── training_history.png
    ├── segmentation_results.png
    └── sample_data.png
```

---

## 🎨 MELHORAR O REPOSITÓRIO (OPCIONAL)

### Adicionar Imagens ao README

1. Crie uma pasta `images/` no repositório
2. Adicione capturas de tela dos resultados
3. No README.md, adicione:

```markdown
## Results

![Training History](images/training_history.png)
![Segmentation Results](images/segmentation_results.png)
```

### Adicionar Badges

No topo do README.md, você pode adicionar badges coloridos:

```markdown
![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
```

### Criar um GitHub Pages (Site)

1. Settings → Pages
2. Source: `main` branch
3. Seu projeto terá uma URL: `https://SEU-USUARIO.github.io/brain-tumor-segmentation/`

---

## 🔄 ATUALIZAR O REPOSITÓRIO (DEPOIS)

Se você fizer alterações nos arquivos:

```bash
# 1. Adicione as mudanças
git add .

# 2. Faça commit
git commit -m "Update: descrição do que mudou"

# 3. Envie para GitHub
git push
```

---

## ⚠️ PROBLEMAS COMUNS E SOLUÇÕES

### Problema 1: "Authentication failed"

**Solução:** Você está usando a senha da conta. Use o Personal Access Token!

### Problema 2: "Repository already exists"

**Solução:** Delete o repositório no GitHub e crie novamente, ou use outro nome.

### Problema 3: "Failed to push some refs"

**Solução:**
```bash
git pull origin main --rebase
git push origin main
```

### Problema 4: Arquivo muito grande

**Solução:** O dataset não deve ser enviado! O .gitignore já está configurado para ignorar.

Se já adicionou por engano:
```bash
git rm --cached arquivo-grande.nii.gz
git commit -m "Remove large file"
git push
```

---

## ✅ CHECKLIST FINAL

Antes de publicar, verifique:

- [ ] README.md está bem formatado
- [ ] Notebook funciona (rode todas as células)
- [ ] Não há dados sensíveis (senhas, tokens, etc.)
- [ ] .gitignore está configurado
- [ ] requirements.txt está completo
- [ ] LICENSE está incluído
- [ ] Links no README estão corretos

---

## 📱 PRÓXIMOS PASSOS

Depois de publicar:

1. **Copie a URL do repositório**
2. **Adicione ao Lattes** (na seção de Produção Técnica)
3. **Compartilhe no LinkedIn** (veja DOCUMENTATION_LATTES_LINKEDIN.md)
4. **Adicione ao seu perfil GitHub** como repositório fixado (pin)

---

## 💡 DICAS IMPORTANTES

1. **Não envie o dataset** - É muito grande e já está no .gitignore
2. **Adicione um README visual** - Imagens ajudam muito
3. **Mantenha commits descritivos** - Facilita o histórico
4. **Atualize regularmente** - Mostre que o projeto está vivo
5. **Responda issues** - Se alguém abrir, responda profissionalmente

---

## 🆘 PRECISA DE AJUDA?

- **Documentação Git:** https://git-scm.com/doc
- **Documentação GitHub:** https://docs.github.com
- **Tutorial Git em português:** https://www.atlassian.com/br/git/tutorials

---

**Boa sorte com a publicação! 🚀**

Qualquer dúvida, consulte a documentação ou me procure!
