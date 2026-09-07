# Birthday Calendar View

## Summary

A SharePoint Framework web part that shows your team's birthdays on a month calendar. Each birthday appears as a pill in its day cell; clicking one opens a person card with department, job title, office and phone pulled from the SharePoint user profile, plus one-click **Email** and **Teams** buttons to send a greeting.

A "Coming up" strip above the calendar lists the next five birthdays so people don't have to go looking for them.

![picture of the solution in action](./assets/screenshot.png)

## Used SharePoint Framework Version

![version](https://img.shields.io/badge/version-1.23.2-green.svg)

## Applies to

- [SharePoint Framework](https://aka.ms/spfx)
- [Microsoft 365 tenant](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)

> Get your own free development tenant by subscribing to [Microsoft 365 developer program](http://aka.ms/o365devprogram)

## Prerequisites

A SharePoint list holding the birthdays. By default the web part looks for a list named **BDay** with:

| Column     | Type             | Required | Notes                                                                       |
| ---------- | ---------------- | -------- | --------------------------------------------------------------------------- |
| `Title`    | Single line text | Yes      | Fallback display name, used when no person is linked.                       |
| `BDate`    | Date             | Yes      | Only the month and day are used — the year is ignored.                      |
| `Person`   | Person or Group  | No       | Links the entry to a real user so the person card can show profile details. |

Every column name is configurable in the property pane, so an existing list can be used as-is.

No Microsoft Graph permissions and no tenant-admin API approval are needed. Profile details come from the SharePoint user profile service (`SP.UserProfiles.PeopleManager`), which the signed-in user can already read.

## Web part settings

**List settings**

| Setting                | Default | Description                                                                                          |
| ---------------------- | ------- | ---------------------------------------------------------------------------------------------------- |
| Site URL               | current | Absolute URL of the site holding the list. Leave blank to use the current site.                      |
| List name              | `BDay`  | Title of the birthday list.                                                                           |
| Birthday date column   | `BDate` | Internal name of the date column.                                                                     |
| Person column          | `Person`| Internal name of the Person or Group column. Leave blank to show names only, with no profile lookup.  |

**Display**

| Setting                  | Default             | Description                                            |
| ------------------------ | ------------------- | ------------------------------------------------------ |
| Start the week on Monday | off (Sunday first)  | Switches the grid and the weekday header row.          |
| Colour mode              | Match the site theme| Pin the birthday palette to light or dark if you'd rather not follow the site. |

If the person column name is wrong, the calendar still renders — it falls back to a plain query, logs a warning to the browser console, and each person card explains that no profile is linked.

## Placement

> **Use this web part in a full-width or one-column section.** The calendar is a seven-column grid with fixed-height cells; in a narrow column the day cells become too small to read names. A responsive list view for narrow columns is a possible future addition.

## Solution

| Solution                | Author(s)          |
| ----------------------- | ------------------ |
| SPFx-Bday-CalendarView  | Alexandr Abdulca   |

## Version history

| Version | Date              | Comments                                                                                                             |
| ------- | ----------------- | -------------------------------------------------------------------------------------------------------------------- |
| 1.0     | September 6, 2026 | Initial release: month grid, person cards, "Coming up" strip, Email/Teams greetings, Monday start, light/dark palette. |

## Disclaimer

**THIS CODE IS PROVIDED _AS IS_ WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**

---

## Minimal Path to Awesome

- Clone this repository
- Ensure that you are at the solution folder
- in the command-line run:
  - `npm install -g @rushstack/heft`
  - `npm install`
  - `heft start`

To run the unit tests:

- `heft test`

To produce the deployable package:

- `npm run build` — writes `sharepoint/solution/sp-fx-bday-calendar-view.sppkg`

Other build commands can be listed using `heft --help`.

## Features

This web part illustrates the following concepts:

- Reading a SharePoint list with `SPHttpClient`, including `$expand` on a Person column and paging via `odata.nextLink`
- Reading user profile properties (department, job title, office) without any Graph permission grant, using `SP.UserProfiles.PeopleManager`
- Fluent UI `Callout`, `Persona` and `MessageBar` in a React 17 SPFx web part
- Theme-aware styling with CSS custom properties and an author override in the property pane
- Deep links that start an Outlook email or a Teams chat with a pre-filled greeting
- Keeping date arithmetic in a pure, unit-tested module (`utils/calendarUtils.ts`)

## Notes

- Only the month and day of each date are used, so entries never need updating and no ages are shown or stored.
- Birthdays on 29 February are shown on 28 February in common years rather than disappearing.
- Birthdays are read from a list people opt into, rather than from Entra ID. `user.birthday` in Microsoft Graph cannot be queried in bulk, needs tenant-wide `User.Read.All`, and is empty for most users because it is a self-service Delve profile field.

> Share your web part with others through Microsoft 365 Patterns and Practices program to get visibility and exposure. More details on the community, open-source projects and other activities from http://aka.ms/m365pnp.

## References

- [Getting started with SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)
- [Building for Microsoft teams](https://docs.microsoft.com/sharepoint/dev/spfx/build-for-teams-overview)
- [Use Microsoft Graph in your solution](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-microsoft-graph-apis)
- [Publish SharePoint Framework applications to the Marketplace](https://docs.microsoft.com/sharepoint/dev/spfx/publish-to-marketplace-overview)
- [Microsoft 365 Patterns and Practices](https://aka.ms/m365pnp) - Guidance, tooling, samples and open-source controls for your Microsoft 365 development
- [Heft Documentation](https://heft.rushstack.io/)
