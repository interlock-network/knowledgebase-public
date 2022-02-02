While risk scores tend to be magical numbers with little comprehension
value to customers, I do think providing funnel analysis and cohorts can
succeed where compound scores too often fall short (due to scaling and
assumptions).

For example, Gitlab shows my Cycle Analytics without assigning any sort of
Cycle Score. I would never care about a Cycle Score, but seeing things move
through a pipeline provides insights into various stages where development
can be more streamlined, like if builds are taking too long.

In our product, I propose the following:

   - A funnel graph , for point-in-time risk with comparative value.
   - A standard cohort analysis for aggregate risk overtime (Stage x Week1,
   Week2, etc=E2=80=A6)

The funnel would consist of the following stages:
```
------------ PEOPLE -------------
  -------- REACHABILITY -------
    -----    EXPOSURE --------
      ---- SUCEPTIBILITY --
       ------ RISK ------
           ---PWN---
```

------------------------------
# Summary

The intuitive description of this funnel is 'Someone who is easy to reach
online, often visits sites they have never been to and frequently uploads
and downloads information from those sites, especially outdated phony
looking ones. This is the person who is most likely to get pwned.

Below you can see the funnel stages and how each stage provides an
organization with where security optimizations should be made.
------------------------------
## 5. People (and/or Devices)

Raw number of people. Simply put, you need to start somewhere.

Actionable Insight: High people or devices requires dedicated security staff
## 4. Reachability

Things like communication habits and online duration. If a person is online
more they are more likely to be reachable. I know this is not 100% true,
but I think it=E2=80=99s good enough. As the product grows we should track =
time
spent inside specific Cloud Services to make this more precise. For
example, social media, email and other communication sites are a great
example of more precise reachability.

Actionable Insight: High reachability requires strong awareness training.
## 3. Exposure (TOFU or Anomaly)

Exposure is part of our TOFU model consisting of websites the person does
not have a relationship with. The rate of exposure is what matters here. If
I only visited new URLs every day for 30 years I am more likely to
encounter dangerous parts of the internet. Exposure in our product is well
established through personal user history and aggregate history on the
platform.

Actionable Insight: High Exposure requires greater filtering.
## 2. Susceptibility (or Risky Behavior)

This is the behavior of a person on the site that would lead to a breach,
if the site were malicious. For example, did they click a link, fill out a
form, upload or download a file. Traditional phishing simulation did this
with JUST email, we can do it with sites, adverts, or sampling through our
extension or integration with phishing campaign tools. Even tracking
downloads and form submissions could be sufficient.

Actionable Insight: High susceptibility requires strategic blocking and
access restrictions.
## 1. Risk (or Encounter)

This is the technical risk of the site. Does it use outdated frameworks
(retire.js), does it look like other websites (our visual ID) , does it
appear in threat lists etc. We primarily determine risk by visual ID, but
could use a softer metric like security alerts.

Actionable Insight: High encounters requires greater isolation and minimum
viable access.
## 0. Zero-Day

Someone got owned.

Actionable Insight: Requires incident response and investigation.
Foreward

As a segue into BI the tracking of cloud service usage, duration and
activity could enable us to sell to companies wanting to improve their
products or understand engagement. Traditional proxies cannot track this
data. We can actually compute this on the backend by analyzing navigation
history or we can track it separately
