# SPFx Web Parts

A collection of SharePoint Framework web parts, built to be dropped into a modern SharePoint site and shared with the community.

Each folder under [`samples/`](./samples) is a self-contained SPFx project with its own `package.json`, build and README. There is no shared build at the root — `cd` into the sample you want and work there.

## Components

| Sample | Description | SPFx |
| ------ | ----------- | ---- |
| [birthday-calendar](./samples/birthday-calendar) | Team birthdays on a month calendar, with person cards showing department, job title and office, and one-click email or Teams greetings. | 1.23.2 |

## Getting started with any sample

```bash
cd samples/<sample-name>
npm install
heft start            # local workbench
heft test             # lint + unit tests
npm run build         # production .sppkg in sharepoint/solution
```

Requires Node.js `>=22.14.0 <23.0.0` and `@rushstack/heft` installed globally (`npm install -g @rushstack/heft`).

Each sample's own README covers its prerequisites, list schema and web part settings.

## Deploying a sample

1. Run `npm run build` in the sample folder.
2. Upload the `.sppkg` from `sharepoint/solution/` to your tenant or site collection App Catalog.
3. Trust the solution when prompted, then add the web part to a page.

## Author

Alexandr Abdulca — [github.com/Niacrisss](https://github.com/Niacrisss)

## License

[MIT](./LICENSE)

## Disclaimer

**THIS CODE IS PROVIDED _AS IS_ WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**
