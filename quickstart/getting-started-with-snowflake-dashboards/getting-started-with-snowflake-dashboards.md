author: Chanin Nantasenamat
id: getting-started-with-snowflake-dashboards
categories: snowflake-site:taxonomy/solution-center/certification/quickstart, snowflake-site:taxonomy/product/analytics
language: en
summary: Load a synthetic revenue dataset with one SQL file, open a pre-made Snowflake Dashboards file, and explore filters, drilldown, and chart actions in under a minute.
environments: web
status: Draft
feedback link: https://github.com/Snowflake-Labs/sfquickstarts/issues
fork repo link: https://github.com/sfc-gh-cnantasenamat/sfguide-getting-started-with-snowflake-dashboards

# Getting Started with Snowflake Dashboards

## Overview

Most dashboard tutorials make you build something before you see anything. This one works the other way round. You run one SQL file and open one dashboard file, and within a minute you're clicking through a working revenue dashboard. Once you've seen what [Snowflake Dashboards](https://docs.snowflake.com/en/LIMITEDACCESS/cowork-dashboards) can do, Part 2 shows you how to build the same dashboard from scratch.

The dashboard is **Revenue Pulse**. It runs on synthetic data for a fictional B2B software company: 54 accounts, 3 product lines, and 24 months of revenue through September 30, 2026. The data has a story built in. Q3 2026 revenue is $1.09M behind target, and most of the gap sits in EMEA Enterprise.

![Overview tab of the Revenue Pulse dashboard with KPI sparklines, a monthly trend, regional bars, a heatmap, and driver and account charts](assets/dashboard-complete.png)

### What You'll Learn
- How to load a small demo dataset and semantic view with one SQL file
- How to open a `.dash` file in Snowsight Workspaces
- How filters, brushing, click-to-filter, and hierarchy drilldown work in a dashboard
- How to publish a dashboard so others can open it in Snowflake CoWork

### What You'll Build
You'll have a four-tab Revenue Pulse dashboard running on live queries in your own account. The tabs are **Overview**, **Hierarchical Chart**, **Hierarchical Table**, and **Data Source**.

### What You'll Need
- Access to a [Snowflake account](https://signup.snowflake.com/?utm_source=snowflake-devrel&utm_medium=developer-guides&utm_cta=developer-guides)
- A role that can create a database and a semantic view (for example, `SYSADMIN` or `ACCOUNTADMIN`), and a warehouse you can use
- Access to [Snowflake Dashboards](https://docs.snowflake.com/en/LIMITEDACCESS/cowork-dashboards) (public preview) in Snowsight Workspaces

Everything runs in Snowsight. You don't need Python, a CLI, or a Git integration.

## Get the Two Files

Download these two files from the [companion repository](https://github.com/sfc-gh-cnantasenamat/getting-started-with-snowflake-dashboards):

| File | What it does |
|---|---|
| [`sql/quick_setup.sql`](https://github.com/sfc-gh-cnantasenamat/getting-started-with-snowflake-dashboards/blob/main/sql/quick_setup.sql) | Creates `REVENUE_PULSE_DB.DASHBOARD_DEMO`, three tables of synthetic data, and the `REVENUE_SEMANTIC_VIEW` semantic view |
| [`dashboards/revenue_pulse.dash`](https://github.com/sfc-gh-cnantasenamat/getting-started-with-snowflake-dashboards/blob/main/dashboards/revenue_pulse.dash) | The finished dashboard: tiles, filters, layout, and SQL in one file |

On each file's GitHub page, select **Download raw file**.

## Load the Data

1. In Snowsight, go to **Projects » Workspaces**.
2. In **My Workspace**, select **+ Add New » Upload Files** and upload `quick_setup.sql`.
3. Open `quick_setup.sql`. In the editor, pick your role and a warehouse.
4. Select **Run All**.

The script finishes in about 10 seconds. Its last statement returns one row:

| CUSTOMERS | PRODUCTS | REVENUE_ROWS |
|---|---|---|
| 54 | 3 | 3888 |

If you see those numbers, the data is ready. The script is safe to run again: it replaces the tables each time.

> **Note:** The revenue rows are packed into one `INSERT` to keep the file small. You don't need to read it. The table definitions at the top and the semantic view at the bottom are the parts worth a look.

## Open the Dashboard

1. Select **+ Add New » Upload Files** again and upload `revenue_pulse.dash`.
2. Open `revenue_pulse.dash`. Snowsight renders it as a dashboard rather than as text.
3. Select **Run all** if the tiles don't load on their own.

The KPI row shows the Q3 2026 headline: net revenue of **$6.9M**, up 0.8% year over year, **86.3%** target attainment, a variance of about **−$1.09M** (the card rounds it to −$1M), and 71% gross margin.

That's the whole setup. Everything from here is exploring.

## Explore the Dashboard

Try each of these on the **Overview** tab, and clear the selection before the next one.

### Brush the Trend
Drag across a range of months on **Monthly Net Revenue vs Target**. The chart zooms to those months, and the KPI cards, regional bars, and heatmap recalculate for the range. Clear the **Filtering** chip on the tile to undo it.

![Trend brushed across several months: the tile shows a Filtering chip and the other charts recalculate](assets/trend-brush-active.png)

### Click a Region
Click the **EMEA** bar on **Variance to Target by Region**. The other tiles filter to EMEA, where attainment drops to about 70%. Clear **Drill: region path** at the top to reset.

![Regional variance bars after clicking EMEA, with the other tiles filtered to that region](assets/regional-bar-filter-emea.png)

### Click a Heatmap Cell
On **Target Attainment**, the darkest cell is EMEA Enterprise at **57.9%**. Click it to filter the rest of the dashboard to that region and segment.

### Drill the Hierarchy
Open the **Hierarchical Chart** tab. Click **EMEA**, then **Enterprise**, to reach its six accounts. The largest miss is Demo EMEA Enterprise 05, at about −$349K. Use the level trail to return to the top.

![Hierarchical Chart tab at the region level, with EMEA furthest below target and the account table sorted by variance](assets/hierarchy-drill-region.png)

The **Hierarchical Table** tab shows the same region › segment › account path as an expandable grid.

![Hierarchical Table tab at the region level, with EMEA at 70.1% attainment, APAC at 83%, and Americas at 106.1%](assets/hierarchy-table.png)

### Use the Header Filters
Set **Region = EMEA** and **Segment = Enterprise** from the filter bar. These filters apply across every tab, which makes them the quickest way to compare one slice against another.

## Share It in CoWork (Optional)

To let someone else open the dashboard:

1. With `revenue_pulse.dash` open, select **Share**.
2. Add the role that should see it, with **Can view** access, then publish.
3. Open **Artifacts** in [Snowflake CoWork](https://docs.snowflake.com/en/user-guide/snowflake-cortex/snowflake-cowork) and select **Revenue Pulse**.

Viewers run the dashboard with their own privileges, so their role needs `SELECT` on the three tables and the semantic view, plus a warehouse. Publishing needs the `MANAGE ACCESS ON DASHBOARD ARTIFACTS` privilege, which is [granted to `PUBLIC` by default](https://docs.snowflake.com/en/release-notes/bcr-bundles/un-bundled/bcr-manage-access-dashboard-artifacts).

In CoWork you can type follow-up questions about the dashboard in the box below it.

![Revenue Pulse artifact in CoWork with filters, page tabs, KPI sparklines, and the follow-up box](assets/cowork-artifact.png)

## Clean Up

When you're done, remove the demo objects:

```sql
DROP DATABASE IF EXISTS REVENUE_PULSE_DB;
```

Delete `quick_setup.sql` and `revenue_pulse.dash` from your workspace. If you published the dashboard, remove its roles in **Share** and delete the artifact in CoWork.

## Conclusion And Resources

You loaded a dataset, opened a dashboard file, and traced a $1.09M revenue gap to EMEA Enterprise, with no building required. The `.dash` file you opened holds every tile, filter, chart action, and SQL query, so it's easy to version, share, and reuse.

### What You Learned
- One SQL file can set up the tables and semantic view a dashboard needs
- A `.dash` file opens in Workspaces as a working dashboard
- Brushing, click-to-filter, and hierarchy drilldown let you move from a headline number to the accounts behind it
- Published dashboards run with each viewer's own privileges

### Next: Build It Yourself
In Part 2, [Build Snowflake Dashboards with CoCo](https://github.com/sfc-gh-cnantasenamat/sfguide-build-snowflake-dashboards-with-coco), you build this dashboard from scratch with Cortex Code prompts. Along the way you also add a Cortex Agent, publish to a least-privilege role, and ask CoWork why the numbers moved.

### Related Resources
- [Dashboards in Snowflake CoWork](https://docs.snowflake.com/en/LIMITEDACCESS/cowork-dashboards)
- [Workspaces](https://docs.snowflake.com/en/user-guide/ui-snowsight/workspaces)
- [Snowflake semantic views](https://docs.snowflake.com/en/user-guide/views-semantic/overview)
- [Artifacts in Snowflake CoWork](https://docs.snowflake.com/en/user-guide/snowflake-cortex/snowflake-cowork/artifacts)
