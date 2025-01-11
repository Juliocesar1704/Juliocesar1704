<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=VT323&size=33&pause=&color=41B8D5&center=falso&vCenter=falso&repeat=falso&random=falso&width=435&lines=Olá,+bem+vindo(a)+ao+meu+GitHub+!" alt="Typing SVG" /></a>

![Banner JC](https://github.com/user-attachments/assets/b00c1eb8-8393-4e85-98e6-3dfc1605eb0d)


name: Generate snake animation

on:
  schedule: # execute every 12 hours
    - cron: "* */12 * * *"

  workflow_dispatch:

  push:
    branches:
    - master

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: dist/snake.svg?palette=github-dark


      - name: push snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
