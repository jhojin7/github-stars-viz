# GitHub Stars Visualization
Visualize my 600+ starred repositories worth of data to get insights.

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

## Resources
- https://docs.github.com/en/rest/activity/starring?apiVersion=2022-11-28#list-repositories-starred-by-a-user
- https://docs.github.com/en/rest/overview/authenticating-to-the-rest-api?apiVersion=2022-11-28
- https://pandas.pydata.org/docs/reference/api/pandas.json_normalize.html
- https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html

## TODO
- [ ] What was I interested in?
- [ ] What am I interested in now?
- [ ] python script to automate api calls for a user
- [ ] web interface for viz
- [ ] database? 
- [ ] other metrics
- [ ] good metris for pinned gist?
