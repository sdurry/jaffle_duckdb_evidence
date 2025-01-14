---
title: Welcome to Evidence
---

_Build polished data products with SQL and Markdown_

Data in this demo is from the local DuckDB file `jaffle_shop.duckdb`.

<LineChart
  data={orders_by_month}
  y=sales
  yFmt=usd0k
  title = "Sales by Month, USD"
/>

## Write in Markdown

Evidence renders markdown files into web pages. This page is:
`[project]/pages/index.md`.

## Run SQL using Code Fences

```sql orders_by_month
select
  date_trunc('month', order_date) as order_month,
  count(order_id) as number_of_orders,
  sum(amount) as sales,
  sum(amount)/count(order_id) as average_order_value
from orders
group by 1 order by 1 desc
```

In your markdown file, you can include SQL queries in code fences. Evidence will run these queries through your database and return the results to the page.

To see the queries on a page, click the 3-dot menu at the top right of the page and Show Queries. You can see both the SQL and the query results by interacting with the query above.


## Visualize Data with Components

### Value in Text

Last month customers placed **<Value data={orders_by_month} column=number_of_orders/>** orders. The AOV was **<Value data={orders_by_month} column=average_order_value fmt=usd2/>**.

### Big Value 
<BigValue data={orders_by_month} value=sales fmt=usd0/>
<BigValue data={orders_by_month} value=number_of_orders />


### Bar Chart

<BarChart 
  data={orders_by_month} 
  y=number_of_orders 
  fillColor="#488f96"
>
  <ReferenceArea xMin="2020-03-15" xMax="2021-05-15" label="COVID Impacted" color=red/>
</BarChart>

> **Try:** Change the chart to a `<LineChart>`.

### Data Table

<DataTable data={orders_by_month} rows=6>
  <Column id=order_month fmt=mmmm-yy title="Month"/>
  <Column id=sales fmt=usd0 />
  <Column id=number_of_orders />
  <Column id=average_order_value fmt=usd2 title="Avg. Order Value"/>
</DataTable>

> **More:** See [all components](https://docs.evidence.dev/components/all-components)

## Control Output With If and Loops

[Use `{#if}` statements and `{#each}` loops](/control-statements) to dynamically choose what text and data is displayed.

# Share with Evidence Cloud

Evidence Cloud is the easiest way to securely share your project. 
- Get your project online
- Authenticate users
- Schedule data refreshes

<BigLink href=/settings#deployment>Deploy to Evidence Cloud &rarr;</BigLink>

You can use Netlify, Vercel or another static hosting provider to [self-host Evidence](https://docs.evidence.dev/deployment/overview).

# Get Support

- Message us on [Slack](https://join.slack.com/t/evidencedev/shared_invite/zt-uda6wp6a-hP6Qyz0LUOddwpXW5qG03Q)
- Read the [Docs](https://docs.evidence.dev/)
- Open an issue on [Github](https://github.com/evidence-dev/evidence)
