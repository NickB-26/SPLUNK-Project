# 🛡️ Splunk SIEM Project — SOC Analyst Fundamentals

A hands-on project demonstrating the fundamentals of working with Splunk Enterprise as a Security Information and Event Management (SIEM) platform — covering installation, data ingestion, dashboard creation, and writing Search Processing Language (SPL) queries to analyse Windows Event Logs.

---

## 🎯 Project Overview

This project showcases practical SIEM skills by deploying Splunk Enterprise locally, ingesting Windows Event Log data, and building dashboards and queries that an entry-level SOC analyst would use day-to-day. The goal is to demonstrate analytical thinking, tool fluency, and the ability to translate raw log data into actionable security insight.

---

## 🖥️ Environment

- **Operating System:** Windows
- **SIEM Platform:** Splunk Enterprise
- **Data Source:** Local directory containing Windows Event Logs
- **Events Ingested:** 28,617 WinEventLog events

---

## 📥 Splunk Installation

**Step 1** — Go to [Splunk](https://www.splunk.com) and create an account.

**Step 2** — Download the corresponding Splunk Enterprise software for your operating system (Windows in my case).

**Step 3** — Install Splunk and accept the Terms & Conditions.

---

## 📊 Data Ingestion

**Step 1** — Once the installation process is finished, data sources can be added to provide data we can analyse. Click **Settings** in the top right corner, then **Add Data**.

**Step 2** — Select a data source from the various options available (Local Event Logs, Remote Event Logs, Files and Directories, etc.). I chose a directory from my local machine.

**Step 3** — Work through the remaining steps to finish adding the data source.

Once the data has been loaded into Splunk, searching and analysis can begin. Splunk identified **28,617 WinEventLog events** from the provided source (visible in the top left corner of the search interface). A wide range of filter options can be used to display only the data relevant to the current investigation.

---

## 📈 Dashboard Setup

Splunk offers two main dashboarding options:

- **Classic Dashboards** — built using XML
- **Dashboard Studio** — a modern, customisable framework using JSON

A wide range of metrics can be visualised, categorised broadly into **infrastructure**, **application**, and **network health**. As an example, I configured a panel to display **median CPU usage over the last 30 minutes**.

Dashboards support multiple chart types, each suited to different analytical purposes:

- **Column & bar charts** — comparing values across categories
- **Line & area charts** — showing changes or trends over time
- **Pie & donut charts** — displaying proportional breakdowns of a whole

Different fields can be selected from the left pane to tailor the view to specific analytical needs.

---

## 🔍 SPL — Search Processing Language

The Splunk search bar accepts **Search Processing Language (SPL)** — Splunk's proprietary query language for filtering and analysing data.

SPL accepts several input types:

- **Search terms & keywords** — e.g. `error`, `failed`, `login`
- **Field-value pairs** — e.g. `host=webserver`, `sourcetype=access_combined`
- **Boolean operators** — `AND`, `OR`, `NOT`
- **Wildcards** — e.g. `fail*` matches *failure*, *failed*, etc.
- **Quoted phrases** — e.g. `"database error"` for exact matches

Multiple commands can be **chained using the pipe symbol (`|`)**. This means commands following the pipe take the output from the previous command and process it further, allowing the analyst to fine-tune results by progressively filtering and transforming the data.

---

## 🎓 Lessons Learned

### Technical insights
- **SPL is more powerful than expected.** What initially looked like a simple search bar is actually a full pipeline language. Understanding the `|` operator and how each command transforms the previous output was a turning point in writing effective queries.
- **Data volume changes everything.** With over 28,000 Windows events ingested, I quickly realised that unfiltered searches return overwhelming noise. Effective analysis depends on knowing *what* to filter for — which means understanding the relevant Windows Event IDs before you even start typing.
- **Dashboards are storytelling tools.** A well-designed dashboard isn't just a collection of charts — it should answer the specific questions an analyst would ask during triage.

### SOC analyst mindset
- **Detection requires hypothesis-driven thinking.** Rather than asking "what does this data show?", I learned to ask "what would an attacker look like in this data?" — which led to far more meaningful searches.
- **Context matters more than alerts.** A single failed login is meaningless on its own; five failed logins followed by a success from the same source is a potential incident. Building queries that capture *patterns*, not just events, is the core skill.

### Challenges & how I overcame them
- **The SPL syntax took time to click.** I initially tried to write SQL-style queries, which doesn't translate to Splunk. Switching my mental model to "pipeline of transformations" made everything easier.
- **Choosing what to monitor was overwhelming.** With dozens of possible Event IDs, I focused on detections relevant to early-stage attacker behaviour and worked backwards from there.

### What I would do differently next time
- **Set up alerts earlier in the process.** I built dashboards before configuring alerts — but in a real SOC, automated alerting is the foundation, and dashboards support investigation rather than replacing it.
- **Document queries as I go.** Retracing my steps to write this README highlighted the value of keeping a running notebook of every SPL query alongside what it taught me.
- **Test against known-bad data.** Splunk's *Boss of the SOC* dataset would provide realistic attack scenarios to practise against — that's my next project.

---

## 🚀 What's Next

- Complete a **Splunk Boss of the SOC (BOTS)** challenge for hands-on detection experience against realistic attack data.
- Build SPL detections mapped to **MITRE ATT&CK** techniques (initial access, credential access, privilege escalation).
- Configure **automated alerting** with tuned thresholds and document a basic incident response playbook.

---

## 📚 References

- [Splunk Official Site](https://www.splunk.com)
- [Splunk Search Reference](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/WhatsInThisManual)
- [Splunk Search Tutorial](https://docs.splunk.com/Documentation/Splunk/latest/SearchTutorial/WelcometotheSearchTutorial)
- [Boss of the SOC v3](https://github.com/splunk/botsv3)
