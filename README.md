# Your First Snowflake Dashboards Dashboard

Source and companion files for Part 1 of the Snowflake Dashboards developer guides, by Chanin Nantasenamat. Run one SQL file, open one dashboard file, and explore a working revenue dashboard in about a minute. All data is synthetic.

- Guide: [`quickstart/first-dashboard-with-snowflake-dashboards-2-0/first-dashboard-with-snowflake-dashboards-2-0.md`](quickstart/first-dashboard-with-snowflake-dashboards-2-0/first-dashboard-with-snowflake-dashboards-2-0.md)
- [`sql/setup.sql`](sql/setup.sql): creates `REVENUE_PULSE_DB.DASHBOARD_DEMO` with three tables (54 customers, 3 products, 3,888 revenue rows) and `REVENUE_SEMANTIC_VIEW`. Self-contained, with no stage or Git integration.
- [`dashboards/revenue_pulse.dash`](dashboards/revenue_pulse.dash): the finished Revenue Pulse dashboard. Upload it to Snowsight Workspaces and open it.

Part 2, where you build this dashboard from scratch with Cortex Code, is [Getting Started with Snowflake Dashboards](https://github.com/sfc-gh-cnantasenamat/sfguide-getting-started-with-snowflake-dashboards-2-0).

Clean up with `DROP DATABASE IF EXISTS REVENUE_PULSE_DB;`.
