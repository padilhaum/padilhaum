👋 Olá!

- 🟦 **Lua**
- 🟨 **JavaScript**
- 🟧 **Svelte**
- ⚛️ **React.js**


![Contador de Visualizações](https://profile-counter.glitch.me/DanielPadilha/count.svg)


name: Views Counter

on:
  push:
    branches:
      - main

jobs:
  counter:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Update Views Counter
      run: |
        # Simula um contador de visualizações
        count=$(curl -s https://api.github.com/repos/padilhaum/padilhaum/views | jq '.count')
        echo "views=$count" >> $GITHUB_ENV

    - name: Update Badge
      run: |
        # Atualiza o badge com o contador de visualizações
        curl -s "https://img.shields.io/badge/views-${{ env.views }}-blue" > ./views-badge.svg
        mv ./views-badge.svg ./badge/views-badge.svg
