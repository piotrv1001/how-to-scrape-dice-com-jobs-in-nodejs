# How to Scrape Dice.com Jobs in Node.js

This example shows how to scrape Dice.com job listings in Node.js using the [Dice.com Jobs Scraper](https://apify.com/piotrv1001/dice-com-jobs-scraper) actor on Apify. No need to deal with headless browsers or anti-bot measures — just call the actor with your search parameters and get structured job data back.

## What this example does

- Calls the Dice.com Jobs Scraper actor via the Apify API
- Passes a search query and optional filters (state, max results)
- Waits for the run to complete
- Fetches all results from the actor's dataset
- Prints each job listing to the console

## Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- An [Apify account](https://console.apify.com/) (free tier available)
- An [Apify API token](https://console.apify.com/account/integrations)

## Installation

```bash
npm install
```

## Environment setup

Copy `.env.example` to `.env` and add your Apify API token:

```bash
cp .env.example .env
```

Then edit `.env`:

```env
APIFY_TOKEN=your_apify_token_here
```

## Usage

```bash
npm start
```

## Code example

```js
import { ApifyClient } from 'apify-client';
import 'dotenv/config';

// Initialize the ApifyClient with your Apify API token
// Set APIFY_TOKEN in your .env file (copy .env.example to get started)
const client = new ApifyClient({
    token: process.env.APIFY_TOKEN,
});

// Prepare Actor input
const input = {
    "search": "Senior Frontend Developer",
    "stateCode": "TX",
    "maxResults": 100
};

// Run the Actor and wait for it to finish
const run = await client.actor("piotrv1001/dice-com-jobs-scraper").call(input);

// Fetch and print Actor results from the run's dataset (if any)
console.log('Results from dataset');
console.log(`💾 Check your data here: https://console.apify.com/storage/datasets/${run.defaultDatasetId}`);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach((item) => {
    console.dir(item);
});

// 📚 Want to learn more 📖? Go to → https://docs.apify.com/api/client/js/docs
```

## Example output

See [`sample-output.json`](./sample-output.json) for a full example. Each job listing includes:

| Field | Description |
|---|---|
| `id` | Unique job identifier |
| `title` | Job title |
| `companyName` | Hiring company name |
| `salary` | Salary range (when available) |
| `employmentType` | Full-time, Part-time, Contract, etc. |
| `jobLocation` | City, state, country |
| `isRemote` | Whether the role is remote |
| `workplaceTypes` | `Remote`, `Hybrid`, or `On-Site` |
| `postedDate` | ISO 8601 timestamp of when the job was posted |
| `modifiedDate` | ISO 8601 timestamp of the last update |
| `detailsPageUrl` | Direct link to the job listing on Dice.com |
| `companyPageUrl` | Link to the company's Dice.com profile |
| `easyApply` | Whether one-click apply is available |
| `willingToSponsor` | Whether the employer sponsors visas |
| `employerType` | `Direct Hire` or `Recruiter` |
| `summary` | Short description of the role |

## Use cases

- **Job market research** — track demand for specific tech skills across states or cities
- **Salary benchmarking** — aggregate salary ranges for roles you're hiring or applying for
- **Recruiting automation** — build pipelines that surface new listings matching your criteria
- **Job board aggregation** — combine Dice.com data with other sources into a unified feed
- **Trend analysis** — monitor how job postings for a technology grow or decline over time

## Try the actor on Apify

**[Open the Dice.com Jobs Scraper on Apify](https://apify.com/piotrv1001/dice-com-jobs-scraper)**

## License

MIT
