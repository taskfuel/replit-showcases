# TaskFuel showcases for Replit

Small, working Replit templates that call paid APIs through
[TaskFuel](https://taskfuel.ai/?utm_source=replit&utm_medium=referral&utm_campaign=2026-09-replit-templates&utm_content=showcase-index).

Each one opens in Replit with a single click, runs on your own key, and costs
cents per use. No provider accounts, no per-API keys, no subscriptions.

## The showcases

### One brief, four image models

[![Run on Replit](https://replit.com/badge/github/taskfuel/one-brief-four-image-models)](https://replit.com/github.com/taskfuel/one-brief-four-image-models)

Type one brief. It goes to four image models at once and you get four takes
back, each labelled with the price it actually charged. Around 48 cents for the
set.

[Repo](https://github.com/taskfuel/one-brief-four-image-models) ·
[Open in Replit](https://replit.com/github.com/taskfuel/one-brief-four-image-models)

### One search, twenty X posts

[![Run on Replit](https://replit.com/badge/github/taskfuel/one-search-twenty-x-posts)](https://replit.com/github.com/taskfuel/one-search-twenty-x-posts)

Search X by person, phrase or ticker. Twenty posts come back with their full
text, long ones included, plus likes, replies and a link to each original. Half
a cent a search, and no X developer account.

[Repo](https://github.com/taskfuel/one-search-twenty-x-posts) ·
[Open in Replit](https://replit.com/github.com/taskfuel/one-search-twenty-x-posts)

## How these work

Every paid call goes to one endpoint. TaskFuel pays the provider's HTTP-402
charge from your prepaid balance and passes the response straight back:

```js
await fetch("https://app.taskfuel.ai/v1/call", {
  method: "POST",
  headers: {
    Authorization: `Bearer ${process.env.TASKFUEL_API_KEY}`,
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    url: "https://some-provider.example/endpoint",
    method: "POST",
    body: { /* the provider's own parameters */ },
    maxAmountUsd: 0.25,
  }),
});
```

The response headers say what it cost (`x-taskfuel-cost`) and what is left
(`x-taskfuel-balance`). `GET /v1/discover?q=...` searches every provider in the
catalog, around 90 of them, covering search, market data, email, phone calls,
images and more.

Full guide: [app.taskfuel.ai/building-apps.md](https://app.taskfuel.ai/building-apps.md)

## Getting a key

Get one at
[app.taskfuel.ai](https://app.taskfuel.ai/?utm_source=replit&utm_medium=referral&utm_campaign=2026-09-replit-templates&utm_content=showcase-index).
The first $5 is on the house.

In Replit, put it in the **Secrets** tab as `TASKFUEL_API_KEY` rather than in a
file. Secrets are not copied when someone else imports your project.

## Spending safely

These templates run on your own key, and a key can spend the whole balance with
nobody watching at call time. Every showcase here sets two limits in code, and
you should keep them when you adapt one:

- **A per-call ceiling** (`maxAmountUsd`), so a single call cannot run away.
- **A daily budget** that fails closed once it is reached.

If you make a project public and let strangers trigger paid calls, they are
spending your balance. Keep the budget low, or have each visitor bring their
own key.

## Adding a showcase

One repo per showcase, because Replit's import URL takes a whole repository and
`.replit` names a single entrypoint. A repo holding several templates would
hand every importer all of them, with only one of them running.

So: create `taskfuel/<showcase-name>`, make it public, and add a section here
pointing at it.
