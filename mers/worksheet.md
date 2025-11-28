# Assignment 1 - MERS
---
Written by Luis Felipe Montemayor, sometime around November of 2025.

https://open.spotify.com/track/5nc6jwPfSnVcsxCQSizAaO?si=694cb2ac8ab243a2
---

We will be working with data from the 2015 MERS (Middle East respiratory syndrome) outbreak, caused by a viral infection. It's quite rare, but it can be very serious. It paints a more severe clinical picture than COVID-19 or SARS, two other common respiratory diseases.

We will be using the `outbreaks` R package: a great curated learning dataset containing epidemiological data from diseases which have seen well-documented outbreaks in past years, like Ebola, SARS and MERS. The MERS dataset is called `mers_korea_2015`, and it can be accessed by:
```R
# Loading the package with the data 
library("outbreaks")

# Exposing the dataset. 
# It can now be accessed as a variable called `mers_korea_2015`
data(mers_korea_2015)
```

### Data exploration: 
Once you have loaded the MERS dataset with `data()`, it becomes a variable in the global scope. This means you can just call it anywhere in our code. 

#### Quick questions:
a) What object class is `mers_korea_2015` in R? Describe what this class is like, and how is it different from a simple atomic type in R (like a `string` like "hello world!" or a `logical` value like `true`) or a vector type defined with `c()`

b) How can one access the sub-items within the `mers_korea_2015`? 

c) What sub-items exist within this item?

The "sub-items" within `mers_korea_2015` are different data sets within our project. Play with them! Open them, plot graphs, get your hands dirty. The questions won't always tell you what dataset to use! So know what you're starting with, to make sure that you can 


## 1. Demographics 
a) Calculate the **average age** for patients with the outcome "Death" and patients with the outcome "Recovered/Survived."

b) Based on first impressions, does age seem to be a determinant of mortality in this outbreak? How might the social status of the elderly in South Korea contribute to exposure risks (e.g., care homes, hospital frequency)?

c) Name two social factors or behaviours you would expect from the sampled demographic that would increase the likelihood of exposure to MERS-CoV (particularly for the elderly population). Am example could be "hospital hopping" where patients visit multiple hospitals to see different medical professionals.

d) Synthesize your statistical finding with your identified social factors and behaviours to explain how **social status and norms** acted as an **amplifier** of the biological risk posed by age. Maybe it's a good time to look into Korean culture too!

e) Repeat task (d) but with the following points: saturated emergency rooms and family caregiving, common in Korea, where there is a cultural expectation for family members (usually younger women or older teens) to stay in the patient's room providing simple emotional and practical support.

## 2. Institutional Analysis
a) Calculate the median reporting lag from the original variables provided. On average, how many days were people sick and potentially interacting with their social networks before the institution 'captured' them?

b) Analyse your new variable as a function of time. What does the trend tell you about the institution's ability to 'learn' and mobilize resources over time?

c) In MERS outbreaks in the Middle East, men were infected much more often. In this South Korean outbreak, is there a gender imbalance? What could this imply about the gender demographics of caregiving in Korean hospitals?

*Bonus* - investigate why there were more male than female cases in the middle east spread of MERS. Why would this not apply in Korea?

## 3. The Super-Spreader
a) Using the appropriate dataset, calculate the number of infections attributed to each case. Calculate the mean and the maximum of this variable. What is the ratio between the maximum "infector" and the average?

b) Visualise the distribution of secondary cases. What does the shape of your plot imply about how "democratic" or "equal" disease transmission was in this specific sample? 

c) Summarise the demographic profile of the "super spreader" using both datasets. Based on where they were infected and their demographic profile, hypothesize a social reason why this specific individual had such a high number of secondary cases.

_Bonus_ - Test the "Pareto Principle" (the 20/80 rule) on this data. Calculate what percentage of the total infections were caused by the top 20% of infectors. Does this outbreak fit the rule?


<details close>
	<summary>Notes for the curious - read once you have finished the assignment!</summary>

### Reproduction parameters
The "secondary cases" mentioned in the third seciton is referred to in epidemiology as the 
*reproduction index* or Ri. It's a super fundamental parameter in compartmental and network models, used in dynamic modelling of disease spreads. 

The [basic reproduction number](en.wikipedia.org/wiki/Basic_reproduction_number) or R0 is related: it's how many secondary cases you would expect to come directly from an infection in a completely susceptible population (with no immunity). It's used for estimating herd immunity thresholds.

In this worksheet, we treated the data as absolute truth. However, real-world epidemiology relies on several heavy assumptions. Here are a few we made today:

### The Assumption of Perfect Contact Tracing
We calculated the "Super Spreader" numbers based on the `contacts` list. This assumes that *every* transmission event was identified and recorded. They definitely missed contacts when looking at this spread, especially casual ones (like standing next to someone on a bus). Our data most likely *underestimates* the true scale of the transmission network...

### The "Date of Onset" Proxy
In Section 2, we used `dt_onset` (when they felt symptoms) to calculate lag. However, patients are often infectious before symptoms appear (the incubation period). Basing conclusions on symptom onset might be missing several days of "silent spread" where patients were socially active but not yet feeling sick (sounds like a déjà vu?).

### Directionality of Transmission
The `contacts` dataset assumes we know exactly who infected whom. In a crowded hospital ward, it is often impossible to know if "Patient A" infected "Patient B", or if they were both infected by a contaminated surface. The network is likely more complex and "looped" than our simple tree suggests.

### Independence of Observations
Standard statistics (like t-tests or linear regressions) assume data points are independent. Infectious disease data is **dependent**, eg.: if I am sick, my family is more likely to be sick. This clustering means standard p-values can sometimes be misleading, requiring specialized spatial or network models to get more accurate representations of reality.

</details>
