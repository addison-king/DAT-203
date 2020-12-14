# Visualize Yourself Project

## Abstract


##  Assigned Project Goals
1.  Engage in a full-lifecycle data project (from planning through analysis and sharing) with highly relevant data: data about yourself!
2.  Create visualizations of data which facilitate discovery of trends that would otherwise be obscured by the quantity or type of data gathered
3.  Reflect on an aspect of your life that you might wish to change or adjust somehow and create a customized tool for exploring such changes

For more, see: https://technologyrediscovery.net/data/vis/mod-visualizeyourself.html
##  Primary Question
Does auditory stimulus affect the speed of which I solve the rubik's cube? 

##  Initial Planning
* Daily, solve the cube 25 times
* Each day use different auditory stimulation (cycle through each type)
* Three types of audio:
    * White noise (or only ear plugs)
    * Mozart (or general classical music)
    * Metalcore (high BPM core music)
  
## Factor Model
 In order to account for variables in the experimental design, a "factor model" was created. This chart illustrates 4 different independent variables and 4 ways of controlling for them.
 
### Legend
 ![enter image description here](https://github.com/brandyn-gilbert/DAT-203/blob/master/VisualizeYourself/Images/Legend.png?raw=true)
 
### Factor Model
![enter image description here](https://github.com/brandyn-gilbert/DAT-203/blob/master/VisualizeYourself/Images/Factor%20Model.png?raw=true)

##  Peer Evaluation (Revision)
After presenting to a group of peers, some changes were made to the overall project. Audio stimulus was expanded to include a TV Show, an audiobook, and a disliked genre of music (Country). \
The population sizes for these 3 categories are smaller than the original 3 due to time constraints. \
Datetime examinations were excluded from further analysis. No change in performance over time was found. No new moves or finger tricks were practiced during overall test.


## Data Formatting
(Public) Data is contained in separate .csv files, one for each audio condition. Inside the .csv is a column containing a sample (n=75) of values from the population (private) data. 

## Analysis
Analysis began by looking for patterns/normality with a histogram. A quick glance at the data would suggest that all forms of audio created normally distributed data. Knowing that they are all roughly normal, we can use these datasets further to see if there is statistical differences in them. \
<img src="https://raw.githubusercontent.com/brandyn-gilbert/DAT-203/master/VisualizeYourself/Images/Hist_Small_Multiple.png" width="1000">

To help us further visually analyze our data, we'll create a box and whisker plot. We can now see how spread the data is and where our medians lie in relation to each other. What stands out the most is that listening to nothing (Silence) performed worse than all other forms of audio stimuli.

\
<img src="https://raw.githubusercontent.com/brandyn-gilbert/DAT-203/master/VisualizeYourself/Images/BoxPlot_Outliers.png" width="750">

---
The remaining question to answer: is silence statistically different from all other forms of audio? Can I say that listening to something (anything) is better than listening to nothing?

To do this we will need establish a null hypothesis, an alternative hypothesis, and perform a T Test (independent samples).

Using our Silence mean as our basis:\
H<sub>0</sub> : μ ≥ 28.843694 \
H<sub>1</sub> : μ < 28.843694

Before a T Test is performed, a sample (n=75) of the data needs to be taken and the sample data needs to be checked for normality. If our sample is not normally distributed, a new sample needs to be taken:

    sample_list = [metalcore_sample, classical_sample, silence_sample, tv_sample, audiobook_sample, country_sample]
    j=0
    for i in sample_list:
        stat, p = stats.shapiro(i)
        if p > .05:
            print(labels[j],'good: p=%.3f' % (p))
        else:
            print(labels[j],'not good.')
        j -=- 1

    ## Output ##
    Metalcore good: p=0.830
    Classical good: p=0.184
    Silence good: p=0.214
    TV Show good: p=0.096
    Audiobook good: p=0.071
    Country good: p=0.077

Knowing our sample data is normal, we will perform an independent sample T Test at different significance levels.

### Confidence 95% (α = 0.05)
| Genre | p-value | H<sub>0</sub> Result |
|--|--|--|
|Metalcore  |0.000000  |Reject H<sub>0</sub> |
|Classical  | 0.000000 |Reject H<sub>0</sub>  |
|TV Show  |0.000013  | Reject H<sub>0</sub> |
|Audiobook  |0.006095  |Reject H<sub>0</sub>  |
|Country  |0.040489  |Reject H<sub>0</sub>  |

### Confidence 98% (α = 0.02)
| Genre | p-value | H<sub>0</sub> Result |
|--|--|--|
|Metalcore  |0.000000  |Reject H<sub>0</sub> |
|Classical  | 0.000000 |Reject H<sub>0</sub>  |
|TV Show  |0.000013  | Reject H<sub>0</sub> |
|Audiobook  |0.006095  |Reject H<sub>0</sub>  |
|Country  |0.040489  |Fail to reject H<sub>0</sub>  |

### Confidence 99.5% (α = 0.005)
| Genre | p-value | H<sub>0</sub> Result |
|--|--|--|
|Metalcore  |0.000000  |Reject H<sub>0</sub> |
|Classical  | 0.000000 |Reject H<sub>0</sub>  |
|TV Show  |0.000013  | Reject H<sub>0</sub> |
|Audiobook  |0.006095  |Fail to reject H<sub>0</sub>  |
|Country  |0.040489  |Fail to reject H<sub>0</sub>  |

## Conclusions

* Listening to something improves my solve times (confidence 95%). 
* Listening to music I enjoy improves my solve time with greater confidence (99.5%).

I believe that what my results are saying is that having background noise of your choosing improves focus. Even when I was listening to music I dislike (country), my times were still better than when I had silence. My hypothesis to explain this is that giving your auditory cortex something to focus on helps focus (rather than letting it pick up all the little sounds and try and analyze them).

## To Future Students
