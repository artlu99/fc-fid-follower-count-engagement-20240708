# Farcaster FIDs + following + engagement analysis 20240708
### by @artlu aka fafo.artlu.eth

Data analysis triggered by [proxystudio.eth](https://farcaster.id/proxystudio.eth)'s [observations](https://www.supercast.xyz/c/0xf3e610a26f7e2ad0d5292c954e943b8c948b3b39) about possibility of growing an account from scratch.

# Opinionated Conclusions

- ~40 accounts reached Proxy's raw following count
    - ~25% appear to be clearly individual humans
    - significant portion are brands or projects
    - reasonable people may [ask](https://www.supercast.xyz/c/0x9f218147c7773669eaa5543a7cf6bb4059ba2536) whether the Proxy account is a pure human, or strongly attached to a project

- **ZERO** accounts of similar engagement arrived after Proxy. (Bitfloorsghost.eth was about the same time.)

- Notable:

    - a cohort of 5~25 accounts of similar engagement arrived slightly earlier. See original thread for shoutouts

    - significant numbers of accounts at 5k-15k followers, with somewhat lower engagement ranks

# Background

My [iniitial claim](https://supercast) that fewer than 5 accounts had been able to achieve the same growth. No data yet at the time.

Proxy [challenged me](https://www.supercast.xyz/c/0x1e2202562db14c0152913b6224effd300cb619bf) for data.

3 [testable hypotheses](https://www.supercast.xyz/c/0xe83784612d24196de3cd41d07a4c40441d55602c):
1. "Proxy Studio grew from 0 to top 300 users by engagement, between Feb 5, 2024 and July 5th, 2024."

2. "fewer than 5 accounts grew from [0] to [Proxy's current follower count, which is 16.3~16.5k] over that same time period"

3. "The market expected 500 accounts to grow to >5k followers over that time period." Suggesting that the number that actually did is a disappointing number

Pre-registered my data approach [here](https://www.supercast.xyz/c/0x4c598f965626eea19551df74555e1e15ee216918).

 # Data

 1. FIDs and Follower Count

 2. OpenRank Engagement Rank (global)

 3. OpenRank Following Rank (global)

---

  N.B. about OpenRank data, see [@rjs](https://www.supercast.xyz/c/0x03f69d614f4028c81d914745ed96a231200b9a85)'s illuminative discussion including the *normative* claim that `OpenRank "Engagement" Ranking is
 *ridiculously heavily* skewed towards the earliest users of Farcast`

---

## FIDs and Follower Count

A public Neynar query https://data.hubs.neynar.com/queries/756

```
SELECT l.target_fid, ud.value, count(1) AS followers
FROM links l
  LEFT JOIN user_data ud ON l.target_fid = ud.fid AND ud.type = 6
WHERE l.type = 'follow' AND l.deleted_at IS NULL AND ud.deleted_at IS NULL
  AND (target_fid > 20939 OR target_fid IN (6546))
GROUP BY target_fid, ud.value
HAVING count(1) > 4500
ORDER BY count(1) DESC
```

---

## Engagement Rank (global)

A public OpenRank [query](https://docs.openrank.com/integrations/farcaster/global-profile-ranking/top-profiles-based-on-engagement)

```
curl 'https://graph.cast.k3l.io/scores/global/engagement/rankings?limit=1000' | jq -r '["rank", "fid", "fname"], (.result.[] | [.rank, .fid, .fname]) | @csv' > openrank_engagement_20240706.csv
```

---

## Following Rank (global)

A public OpenRank [query](https://docs.openrank.com/integrations/farcaster/global-profile-ranking/top-profiles-based-on-following)

```
curl 'https://graph.cast.k3l.io/scores/global/following/rankings?limit=1000' | jq -r '["rank", "fid", "fname"], (.result.[] | [.rank, .fid, .fname]) | @csv' > openrank_following_20240707.csv
```
