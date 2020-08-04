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

## Follow-Up Experiment: How to Reduce Early Cancellations

