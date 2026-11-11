# Roll The Dice

Aplicação mobile (PWA) para lançar dados: d4, d6, d8, d10, d12, d20 e d100, de 1 a 99 dados de cada vez.
Sem dependências nem passo de build: tudo o que é publicado está em `public/`.

## Estrutura

```
public/
  index.html             app (HTML + CSS + JS)
  manifest.webmanifest   instalação no ecrã principal
  sw.js                  funcionamento offline
  icon.svg               ícone
firebase.json            configuração do Firebase Hosting
.firebaserc              ID do projeto Firebase (substituir)
.github/workflows/       deploy automático
```

## Correr localmente

```bash
npx serve public
```

## 1. GitHub

```bash
git init -b main
git add .
git commit -m "Roll The Dice"
git remote add origin https://github.com/UTILIZADOR/roll-the-dice.git
git push -u origin main
```

## 2. Firebase

1. Criar um projeto em https://console.firebase.google.com
2. Em `.firebaserc`, trocar `YOUR_FIREBASE_PROJECT_ID` pelo ID do projeto.
3. Primeiro deploy manual:

```bash
npm install -g firebase-tools
firebase login
firebase deploy --only hosting
```

## 3. Deploy automático (GitHub -> Firebase)

O workflow `.github/workflows/firebase-hosting.yml` publica no site a cada push para `main`
e cria um URL de pré-visualização em cada pull request. Precisa de duas definições no
repositório (Settings > Secrets and variables > Actions):

| Tipo     | Nome                       | Valor                                             |
|----------|----------------------------|---------------------------------------------------|
| Secret   | `FIREBASE_SERVICE_ACCOUNT` | JSON da conta de serviço do projeto Firebase      |
| Variable | `FIREBASE_PROJECT_ID`      | ID do projeto Firebase                            |

A conta de serviço cria-se na consola Firebase em Project settings > Service accounts >
Generate new private key. Em alternativa, `firebase init hosting:github` cria o secret
automaticamente (nesse caso, recuse substituir os ficheiros existentes ou ajuste o nome
do secret no workflow).

## Atualizações

Ao alterar ficheiros em `public/`, incremente `CACHE` em `public/sw.js`
(`roll-the-dice-v2`, ...) para que as apps já instaladas recebam a nova versão.
