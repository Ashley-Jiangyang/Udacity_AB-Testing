# A/B Testing Walkthrough - Udacity A/B Testing Final Project
Refer this [Jupyter notebok](https://github.com/Ashley-Jiangyang/Udacity_ABTesting/blob/master/Udacity_AB_Testing_Final_Project.ipynb) for more detail.

## Key Results

### Experiment Design

__Metirc Choice__
| Metrics | Dmin | Metircs Type |
| :---: | :---: | :---: |
| Number of Cookies in Course Overview Page | 3000 | Invariate Metric |
| Number of Clicks on Free Trial Button | 240 | Invariate Metric |
| Free Trial button Click-Through-Probability | 0.01 | Invariate Metric |
| Gross Conversion | 0.01 | Evaluation Metric |
| Retention | 0.01 | Evaluation Metric |
| Net Conversion| 0.0075 | Evaluation Metric |

__Measuring Variability__
| Evaluation Metrics | Standard Deviation |
| :---: | :---: |
| Gross Conversion | 0.202 | 
| Retention | 0.0549 | 
| Net Conversion| 0.0156 | 

### Experiment Design - Sizing 

__Sample vs. Power__
| Metrics | Dmin | Beseline Conversion | Alpha | Beta | Sample Size(2) | Pageviews Required |
| :---: | :---: | :---: |:---:| :---: | :---: | :---: |
| Gross Conversion | 20.625% | 1% | 5% | 20% | 51,760 enrollments | 645,875 |
| Net Conversion| 10.9313% | 0.75% | 5% | 20% | 54,826 enrollments | 685,325|

__Duration vs. Exposure__
| Traffic | Duration | Sample Size |
| :---: | :---: | :---: |
|100%| 18 days| 685,325 |
|50%| 35 days| 685,325 |

## Experiment Analysis

__Sanity Checks__
| Metrics | Expected Value | Observed Value | CI Lower Bound | CI Upper Bound | Results |
| :---: | :---: | :---: |:---:| :---: | :---: | 
|Number of Cookies	|0.5000	|0.5006	|0.4988	|0.5012	|Pass|
|Number of clicks on "start free trial"	|0.5000	|0.5005	|0.4959	|0.5042	|Pass|
|Click-through-probability|	0.0821	|0.0822	|0.0812	|0.0830	|Pass|

__Results Analysis__
| Metrics | Dmin| Observed Difference | CI Lower Bound | CI Upper Bound | Results |
| :---: | :---: | :---: |:---:| :---: | :---: | 
|Gross Conversion	|0.01|-0.0205|	-.0291	|-.0120	|Satistically and Practically Significant|
|Net Conversion	|0.0075| 	-0.0048	| -0.0116	| 0.0019| 	Neither Statistically nor Practically Significant| 

__Sign Tests__
|Metric|	p-value for sign test	|Statistically Significant @ alpha .05?|
| :---: | :---: | :---: |
|Gross Conversion|	0.0026	|Yes|
|Net Conversion	|0.6776	|No|

## Follow-Up Experiment: How to Reduce Early Cancelation

