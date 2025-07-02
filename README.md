# YAYIN-name: ATV Yayın Botu

on:
  schedule:
    - cron: '0 */6 * * *' # Her 6 saatte bir
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - name: Repo'yu klonla
        uses: actions/checkout@v3

      - name: Node.js kur
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Paketleri kur
        run: npm install

      - name: Botu çalıştır
        run: npm start

      - name: Değişiklikleri GitHub'a geri yükle
        run: |
          git config user.name "ATV Bot"
          git config user.email "bot@example.com"
          git add atv.json
          git commit -m "Yayın linki güncellendi"
          git push
