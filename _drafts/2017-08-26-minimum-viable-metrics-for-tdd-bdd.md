---
published: false
layout: post
section-type: post
comments: true
date: '2017-08-26 12:23:21 +0530'
title: "Minimum Viable Metrics for TDD and\_BDD"
---
# Minimum Viable Metrics for TDD and BDD
If you have recently started Test Driven Development and/or Behavior Driven Development and would like to know how you can improve or showcase the benefits to the management, you have reached the right place.

This article is a deep-dive at three Minimum Viable Metrics (MVM — I invented this term :D )for the evaluation of TDD and BDD. This article will give you a list of metrics, how to measure them, how to use the metrics and most importantly, how not to use them, along with what an ideal observation looks like.
Lets dive in, right away!


# Metric — 1: No. of Regression Defects Caught in Production
## What does this measure?
Effectiveness of tests. Are automated tests (irrespective of whether they are due to TDD or BDD) helping us?
## Type of measure
Trend (Individual numbers without a trend don’t convey anything)
## Ideal Observation
Decreasing trend
## How to measure?
1. For any defect entry that gets created in production environment in the issue tracking system, have a checkbox/flag to denote if the defect broke an already working functionality. In short, use a checkbox to denote if the defect is a regression.
2. Record the count of regression issues tagged to a specific timeline/release.

## How not to use?
* Don’t track this metric per person. This moves the focus away from managing the system and towards managing the person. The per-person metric becomes obsolete the moment the concerned person leaves the team and doesn’t prevent any new regression bugs after a new person joins.
* Don’t track this metric per sprint. Track this only with production releases. If your teams are still having Work-in-progress stories in sprint boundaries, these numbers will dilute the metric’s core purpose.
* Don’t track this metric for minor/patch releases. This will create a pointless trend with local maxima and minima.

## How to use?
* Track this metric per product, as a whole.
* Track this metric for planned releases, which generally happen at duration with equal gaps. If a regression bug is found just after a minor/patch release, add it to the next release’s account.
* You may wish to track different metrics for regression bugs of different severity. However, I would urge you to consider all regression defects as critical.
* Don’t expect meaningful variations before at least 3 data points are gathered.
* Publish this number to the developers at the end of every release and challenge them to write tests to make sure the same defect does not arise again.


# Metric — 2: No. of Regression Defects Caught before Production Deployment
## What does this measure?
Effectiveness of tests. Are automated tests (irrespective of whether they are due to TDD or BDD) helping us?
## Type of measure
Individual number. No trend required.
## Ideal Observation
≥ 1 per release. However, for increased stress on quality of a system with already high number of regression defects, we can aim for this to be ≥ N,where N is the minimum number of regression defects that the team commits to avoid every release.
## How to measure?
1. All developers anonymously record, in a common wiki per release, the number of times their code failed the tests written during previous releases.
2. With each record, at least one failed test’s URL in CI or build system is quoted.
3. Before every release, discard any entry without CI system link and report the total count of records.
4. In case of a high-trust team, one can just rely on developer’s records, without any URL, as they might also have failed the tests in their local system before it reaches the CI server.

## How not to use?
* Don’t track this metric per person or sprint. Earlier justifications apply here too.
* Don’t trend this metric over time.

## How to use?
* Use this metric as a single-dip acid-test for the utility of your tests. That’s all.
* If this metric’s value is negligible over a very long time and the previous metric (# of regression bugs in production) is growing or stagnant, then you know that your tests are not comprehensive enough.
* At the end of every major release, report this number to the management as the number of regression bugs in production avoided, highlighting the cost savings.


# Metric — 3: No. of Non-Regression Defects Caught after development
## What does this measure?
Effectiveness of our BDD practice. Are we writing enough scenarios before developing? Is our 3-Amigos meeting helping us?
## Type of measure
Threshold achievement, with trend
## Ideal Observation
≤ X consistently over 3 or more releases, where X is the number of re-works that the team can tolerate in a release, without impact to quality and sustainability.
## How to measure?
1. Record the any defect/re-work entry that gets created in the issue tracking system during UAT phase or during product owner acceptance, tag to a specific timeline/release and report this number.
2. Start with an arbitrary value of X based on yesterday’s weather and then  reduce X once 3 consecutive periods have achieved this measure ≤X.

## How not to use?
* Don’t track this metric per person or sprint. Earlier justifications apply here too.
* Don’t trend this metric over time.

## How to use?
* Use this metric as a single-dip acid-test for the utility of your BDD practice. That’s all.
* You can demonstrate this trended graph with decreasing thresholds to the management to show that you are reducing re-work costs.

The above 3 metrics are minimum viable metrics that directly link to the customer goal of reduced defects and developer goal of reduced rework. We could choose to track the following additional metrics to put more challenge on the system, or in case, the above metrics are not directly measurable because of a reason.
* Lead time of bug resolution — Should reduce over a period of time
* No. of extra scenarios identified in 3 amigos — Not equal to 0 — Acid test for meaningfulness of 3 Amigos meetings.
* Cyclomatic Complexity of code — Should reduce over a period of time — Tests make the design better and easily maintainable.
* Total Build red time — Should reduce over a period of time but not in a linear way — becomes constant near zero — Checks responsiveness of team and utility of tests— If tests are good, build gets fixed easily. Else, it takes more time.
* Code coverage — Helps in initial stages to check if the team is writing tests or not
* Mutation Coverage — Checks if tests are meaningful. May not be possible in some technologies.