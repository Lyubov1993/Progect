##  Портфолио  
Данные проекты были выполнены в ходе обучения в Яндекс.Практикуме, профессии  "Специалист по Data Science".

# Проекты 
name: Best_tarif Delete_bad_comment  
в работе использовала:  python, pandas, numpy, scipy, sklearn, matplotlib  
 сылка на проект: [[https://github.com/Lyubov1993/Progect/tree/main/Internet%20magazine  ](https://github.com/Lyubov1993/Best-tarif/tree/main) ](https://github.com/Lyubov1993/yandex_practicum/tree/main/Best_tarif%20) 
2.	Поиск модели ,которая будет убирать плохие комметрарии  
    в работе использовала: python, pandas, numpy, statsmodels, sklearn, matplotlib  
   сылка на проект:[ [https://github.com/Lyubov1993/Progect/blob/main/Internet%20magazine/Поиск%20модели%2C%20которая%20будет%20убирать%20плохие%20комментариии%20интернет%20магазине](https://github.com/Lyubov1993/Poisk-bad-commintariev/tree/main)https://github.com/Lyubov1993/Poisk-bad-commintariev/tree/main](https://github.com/Lyubov1993/yandex_practicum/tree/main/Delete_bad_comment)https://github.com/Lyubov1993/yandex_practicum/tree/main/Delete_bad_comment

name: Latest blog post workflow
on:
  schedule: # Run workflow automatically
    - cron: '0 * * * *' # Runs every hour, on the hour
  workflow_dispatch: # Run workflow manually (without waiting for the cron to be called), through the GitHub Actions Workflow page directly

jobs:
  update-readme-with-blog:
    name: Update this repo's README with latest blog posts
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Pull in dev.to posts
        uses: gautamkrishnar/blog-post-workflow@v1
        with:
          feed_list: "https://dev.to/feed/gautamkrishnar,https://www.gautamkrishnar.com/feed/"
