# GitHub Stars Visualization
Visualize my 600+ starred repositories with data to get insights.

## Note to self
- Use `github.star+json` for `starred_at` timestamp.
```sh
gh api -H "Accept: application/vnd.github.star+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  "/user/starred?per_page=100&page=8" | jq > stars8.json
```

```py
import pandas as pd

stars = pd.DataFrame()
for i in range(1,8):
    tmp = pd.read_json(f"stars{i}.json")
    # pd.read_json(tmp.repo)
    tmp2 = pd.json_normalize(tmp.repo)
    tmp2["starred_at"] = tmp["starred_at"]
    stars = pd.concat([stars,tmp2])
stars
stars.to_csv("stars_final.csv")
```

## TODO
- [] python script to automate api calls for a user
- [] web interface for viz
- [] database? 
- [] other metrics?