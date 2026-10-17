# Second-hand marketplace

A place to sell the things you no longer want. Sellers put them up with
photographs, buyers ask about them in a thread attached to the item,
and the moment one is sold it stops wasting everybody else's time.

Both sides are members of the public. Neither has any power over the
other, either of them can behave badly, and the product is the only
thing standing between them. That is what makes this different from a
shop.

## What finished looks like

A stranger can open the URL, make an account, and put something they no
longer want up for sale with photographs of it. Somebody else finds it
among everything else, asks about it in a thread only the two of them
can read, and is told there is a reply without sitting on the page. The
seller marks it sold, it stops showing to everybody, and the second
buyer hears that from the product rather than from silence. Either of
them can report the other, and what is reported comes down.

Finished does not mean running on a laptop. It means two people who
have never met the person who built it can use it to sell each other a
bicycle.

## The road map

Eight sprints. Each one makes a different part of that sentence true,
and the order is not arbitrary: take any sprint out and the sentence
stops being true.

| # | Sprint | What it makes possible |
|---|---|---|
| 1 | Who you are dealing with | An account, and a name a stranger can judge |
| 2 | Something to sell | A listing with real photographs, and a way to take it down |
| 3 | Finding it | Somebody else's item, found among everything else for sale |
| 4 | Asking about it | A private thread about one item, between two people |
| 5 | Telling the other person | Nobody has to sit on the page waiting for a reply |
| 6 | Sold | A sold item stops showing, and only one buyer can be the one who got it |
| 7 | Behaving badly | Reporting a listing, a message or a person, and having it come down |
| 8 | In front of strangers | It is on the internet, and a bad release can be undone |

## The hard part

Two buyers in two separate conversations about the last one. The seller
agrees with both, or the product lets them, and now two strangers are
travelling to the same address for the same bicycle. Sprint six is
where that is solved, and the fix is not a status column and an `if`.

The second hard part is quieter. Every conversation here is between two
people who have something to lose, and the product can only protect
what it can see. Sprint seven is about the cases where somebody has
already been hurt.

## Working on it

The sprints, their briefs and the tickets under them are in Blacksmith.
Start with sprint one; each sprint opens as the one before it closes.

The reading attached to a sprint is worth opening before its first
ticket rather than after. It carries what a ticket deliberately does
not: what the alternatives were, and which one you are choosing
between.

## What this is built with

The whole product: an API and the screens that use it.

- **Django** with **Django REST Framework** for the API.
- **SimpleJWT** for authentication, against a custom user model in `apps/users`.
- **drf-spectacular** for the OpenAPI schema, served at `/api/schema/` and browsable at `/api/docs/`.
- **React** with **Vite** for the dev server and the build.
- **Chakra UI** for components, and **React Router** for routes.
- **TanStack Query** for every call to the API, so caching and refetching are decided in one place.

## Setting it up

You need the CLI once: `npm install -g blacksmith-cli`.

```bash
blacksmith setup     # dependencies, database, migrations
blacksmith dev       # start it
```

The API answers on `http://localhost:8000`, and the app on `http://localhost:5173`.

Copy `backend/.env.example` to `backend/.env` before the first run. It is ignored by git and holds the secret key, the database URL and anything else this project should not carry in its history.

## Where the code lives

```
backend/
├── config/
│   ├── settings/        # base, development, production
│   └── urls.py          # where routes are mounted
├── apps/
│   └── users/           # the custom user model, and auth
├── utils/               # shared helpers, base model
├── manage.py
└── requirements.txt

frontend/
└── src/
    ├── api/
    │   ├── generated/   # written by `blacksmith sync` — do not edit
    │   └── hooks/       # your queries and mutations
    ├── pages/           # one folder per page
    ├── features/        # auth, and anything else that spans pages
    ├── router/          # routes and layouts
    ├── shared/          # components and hooks used across pages
    └── styles/
```

## Day to day

| Command | What it does |
| --- | --- |
| `blacksmith dev` | Run it locally. |
| `blacksmith sync` | Regenerate the frontend API types and hooks from the backend schema. Run it after changing a serializer or a route. |
| `blacksmith make:resource Post` | Scaffold a model, serializer, viewset and routes, plus the hooks and pages that use them. |
| `blacksmith backend <command>` | Run a Django management command, e.g. `blacksmith backend createsuperuser`. |
| `blacksmith frontend <command>` | Run an npm command in the frontend, e.g. `blacksmith frontend install axios`. |
| `blacksmith eject` | Remove Blacksmith and keep a plain Django and React project. Nothing here is a dependency on us. |
