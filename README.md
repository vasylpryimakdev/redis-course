# RedisMarket

RedisMarket is a SvelteKit auction application backed by Redis. It supports users,
items, likes, bids, search, view counters and Redis-based item indexes.

## Stack

- SvelteKit with the Node adapter
- TypeScript and Svelte
- Redis 4 client
- Tailwind CSS
- Chart.js for bid history

## Requirements

- Node.js and npm
- A Redis instance with RediSearch support

Install dependencies:

```bash
npm install
```

## Environment

Create a local `.env` file. It is ignored by Git and must not be committed.

```env
REDIS_HOST=your-redis-host
REDIS_PORT=6379
REDIS_PW=your-redis-password
COOKIE_KEY=use-a-long-random-secret
```

The application connects to Redis when the SvelteKit server starts and creates
the item search index if it does not exist. Redis credentials should be stored
in the deployment platform's secret manager.

## Local development

Start the development server:

```bash
npm run dev
```

The application is available at `http://localhost:3000`.

Load the sample data into Redis when needed:

```bash
npm run seed
```

Warning: the seed script calls `FLUSHALL` and removes all data from the
configured Redis database. Use a dedicated development database.

## Available scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the SvelteKit development server |
| `npm run build` | Build the application for Node |
| `npm run preview` | Preview the production build |
| `npm run check` | Run Svelte and TypeScript diagnostics |
| `npm run lint` | Check formatting with Prettier |
| `npm run format` | Format project files |
| `npm run seed` | Replace Redis data with sample data |
| `npm run worker` | Start the background worker, when implemented |

## Project structure

- `src/routes` contains pages and API endpoints.
- `src/lib/components` contains reusable Svelte components.
- `src/services/redis` contains the Redis client and index setup.
- `src/services/queries` contains Redis queries and domain logic.
- `seeds` contains sample data and the Redis seeding script.
- `worker` is reserved for background jobs.

## Current status

The project is currently suitable for local development, but is not yet ready
for production deployment. Before deploying, fix the failing type checks and
the server-side `chart.js` import, add a production `start` command, and finish
the background worker and remaining stubbed queries. Also configure a strong
`COOKIE_KEY` and production cookie security options.
