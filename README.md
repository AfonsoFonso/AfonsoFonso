name: Metrics

on:
  schedule: [{cron: "0 3 * * *"}]   # atualiza todo dia às 03:00 UTC (~00:00 em Curitiba)
  workflow_dispatch: {}             # permite rodar manualmente pela aba Actions
  push:
    branches: ["main"]

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          template: terminal
          filename: metrics.terminal.svg
          base: header, metadata

          # Comentários no terminal (linhas que aparecem antes do "whoami")
          config_timezone: America/Sao_Paulo

          # Gráfico de contribuições (o "calendário colorido" tipo GitHub)
          plugin_isocalendar: yes
          plugin_isocalendar_duration: half-year

          # Repos/linguagens mais usadas (opcional, remova se não quiser)
          plugin_languages: yes
          plugin_languages_limit: 4
          plugin_languages_ignored: html, css
