# A/B Testing Walkthrough - Udacity A/B Testing Final Project
Refer this [Jupyter notebok](https://github.com/Ashley-Jiangyang/Udacity_ABTesting/blob/master/Udacity_AB_Testing_Final_Project.ipynb) for more detail.

## Experiment Description
At the time of this experiment, Udacity courses currently have two options on the course overview page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead. This screenshot shows what the experiment looks like.

The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.

The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.

### Experiment Design

__Metirc Choice__: Invariant Metrics are what we usually use for sanity checks - checking whether the distribution in control and experiment group is similar or not - It performing some consistent checking across all of our experiment. Evaluation Metrics are performance Indicators.

| Metrics | Dmin | Metircs Type |
| :---: | :---: | :---: |
| Number of Cookies in Course Overview Page | 3000 | Invariate Metric |
| Number of Clicks on Free Trial Button | 240 | Invariate Metric |
| Free Trial button Click-Through-Probability | 0.01 | Invariate Metric |
| Gross Conversion | 0.01 | Evaluation Metric |
| Retention | 0.01 | Evaluation Metric |
| Net Conversion| 0.0075 | Evaluation Metric |

__Measuring Variability__: Standard deviation of a metric is what we use to accee the variability.

| Evaluation Metrics | Standard Deviation |
| :---: | :---: |
| Gross Conversion | 0.202 | 
| Retention | 0.0549 | 
| Net Conversion| 0.0156 | 

### Launch Criteria

1. Gross conversion is both statistically and practically significant lower in the experiment group.
2. Net conversion is not lower than our practical limit (-0.75%).

### Experiment Design - Sizing 

__Samples vs. Power__ : The pageviews we will need to power the experiment appropriately.

| Metrics | Dmin | Beseline Conversion | Alpha | Beta | Sample Size(2) | Pageviews Required |
| :---: | :---: | :---: |:---:| :---: | :---: | :---: |
| Gross Conversion | 20.625% | 1% | 5% | 20% | 51,760 enrollments | 645,875 |
| Net Conversion| 10.9313% | 0.75% | 5% | 20% | 54,826 enrollments | 685,325|

__Duration vs. Exposure__: The days we would need to run the experiment based on the traffic we would divert to the experiment.
| Traffic | Duration | Sample Size |
| :---: | :---: | :---: |
|100%| 18 days| 685,325 |
|50%| 35 days| 685,325 |

## Experiment Analysis

__Sanity Checks__: For each of our invariant metrics, give the 95% confidence interval for the value we expect to observe, the actual observed value, and whether the metric passes our sanity check. 
| Metrics | Expected Value | Observed Value | CI Lower Bound | CI Upper Bound | Results |
| :---: | :---: | :---: |:---:| :---: | :---: | 
|Number of Cookies	|0.5000	|0.5006	|0.4988	|0.5012	|Pass|
|Number of clicks on "start free trial"	|0.5000	|0.5005	|0.4959	|0.5042	|Pass|
|Click-through-probability|	0.0821	|0.0822	|0.0812	|0.0830	|Pass|

__Results Analysis - Effect Size Tests__: For each of out evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.
| Metrics | Dmin| Observed Difference | CI Lower Bound | CI Upper Bound | Results |
| :---: | :---: | :---: |:---:| :---: | :---: | 
|Gross Conversion	|0.01|-0.0205|	-.0291	|-.0120	|Satistically and Practically Significant|
|Net Conversion	|0.0075| 	-0.0048	| -0.0116	| 0.0019| 	Neither Statistically nor Practically Significant| 

__Results Analysis - Sign Tests__: For each of our evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.
|Metric|	p-value for sign test	|Statistically Significant @ alpha .05?|
| :---: | :---: | :---: |
|Gross Conversion|	0.0026	|Yes|
|Net Conversion	|0.6776	|No|

__Summary__: 

We will recommend launching the new feature when both evaluation metrics match our criteria, our chance for false positive is already low. Using Bonferroni would further reduce the chance of false positive. However, this is too conservative so I will not use Bonferroni correction in our case, remember we only have two metrics here - if we would need only one of them to meet our criteria to launch, we would face the risk that a single metric could meet criteria by pure chance, by mistake. Bonferroni correction would decrease type I error (false positive). However, since we would need all the metrics to meet our criteria to launch, we would face the risk that a single metric could not meet criteria by pure chance, by mistake. We call that type II error (false negative). In this case, Bonferroni correction might even make it worse, since it potentially increased the type II error or made no difference. Therefore, we won't use Bonferroni correction in this problem. The effect size test and sign test result met.


__Recommendation__:
The experiment wanted to find whether the change filtered out the students left the free trial without enough time to commit the course, while not decrease those who enrolled in the free trial and can stick to the end. The Gross conversion showed us numbers of students try free trial decreased as we expected, but the Net conversion showed us numbers of students actual paid potentially decreased whereas we hope it wouldn't change. We can find the net conversion confidence interval lower boundary is -0.0116 is below the lower practical significance as -0.0075. Due to these, my recommendation is not to launch the experiments.


## Follow-Up Experiment: How to Reduce Early Cancellations
The feature was designed to explore the time commitment to filter out that students likely to become frustrated - it focuses on time commitment rather than other reasons that students can get frustrated and cancel early. Even if students were able to spend the time as required, they still can get frustrated, maybe they don't meet the pre-request to follow up with the course - adding a checklist of the pre-requisite skills in the course may be informative. The follow-up experiment will leverage the infrastructure and data pipeline of the original experiment and be set up in the same way. If the students' answers both meet the time and pre-request skills, they will be directed to the free-trail enrollment, otherwise, they are encouraged to access the course for free. 

A variety of approaches could be used to intervene post-enrollment but pre-payment and could be deployed concurrently with pre-enrollment intervention. An ideal approach would be one that minimizes the use of additional coaching resources to best meet the original intent of the intervention. An effective approach may be to employ peer coaching/guidance using team formation. If a student has a team of other students which they could consult, discuss coursework and frustrations with, and be accountable to, they may be more likely to stick out the growing pains and stay for the long term. The experiment would function in the following manner.

__Setup__: Upon enrollment, students will either be randomly assigned to a control group in which they are not funneled into a team or an experimental group in which they are.

__Null Hypothesis__: Participation in a team will not increase the number of students enrolled beyond the 14 days free trial period by a significant amount.

__Unit of Diversion__: The unit of diversion will be user-id as the change takes place after a student creates an account and enrolls in a course.

__Invariant Metrics__: The invariant metric will be user-id since an equal distribution between experiment and control would be expected as a property of the setup.

__Evaluation Metrics__: The evaluation metric will be Retention. A statistically and practically significant increase in Retention would indicate that the change is successful.

If a statistically and practically significant positive change in Retention is observed, assuming an acceptable impact on overall Udacity resources (setting up and maintaining teams will require resource use), the experiment will be launched.
