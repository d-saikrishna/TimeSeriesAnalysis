# Bed capacity management during COVID-19 in Mumbai

One of the major problems surfaced during the COVID-19 pandemic is the collapse of health systems in the event of a disaster. The sudden patient load on under-resourced health systems of India, led to inequities in access to critical healthcare, immense stress to the healthcare workers and anxiety in the population. In such circumstances, the ability to forecast bed-capacity needs would have given enough time for public health officials and hospitals to plan people, resources and infrastructure to provide a sustainable healthcare.

In this project, I take the COVID-19 related data of Mumbai from June 2020 to August 2021. Along with data on case loads, hospital bed capacity data released by Brihanmumbai Municipal Corporation (BMC) is used in the analysis and forecasting.

The IDFC Institute has already analyzed this data in detail [1]. A short summary of their findings is as follows:

![By Nikita Kwatra and Rajeswari Parasa[1]](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled.png)

By Nikita Kwatra and Rajeswari Parasa[1]

1. There is a strong correlation between test positivity rate (TPR) and bed occupancy highlighting the role of TPR as an important predictor for hospital admissions.
2. A lag was observed between the rise in TPR and the rise in bed-capacity to meet the growing demand. It is during this period of lag that most healthcare inequities would occur.
3. High occupancy rates (upto 95%) were observed in the critical health care category (ICUs)
4. Compared to the first wave, official response to the second wave has been better. The bed capacity has been increased by 3 times during the second wave.

In this project, I further build on the above analysis. Firstly, I provide more analysis on how the increase in bed-capacities has been. And finally, I develop a multi-variate forecasting model to predict the occupancy rates across different bed category levels. This model will be useful for public health officials and hospitals in health care management.

### 1. Bed-capacities

There are different kinds of health capacities that were augmented during the pandemic: Dedicated COVID-19 Health Centres (DCHC), Dedicated COVID-19 Hospitals (DCH) and COVID-19 Care Centres (CCCs). Among this, CCCs are more of a temporary arrangement set up in hotels, schools etc., and played immense role during the peak of COVID-19. 

![Untitled](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled%201.png)

While there has been a stagnancy during the beginning of the second wave in ramping up CCC facilities, a small data sample during early August shows how quickly Mumbai could ramp-up CCC facilities. This highlights that the city officials are more prepared to handle sudden peaks in health care demand.

However, when compared to the private health systems, public health systems seems to have underperformed in managing sudden patient load. Within the same period of stagnancy, it can be observed that private health system responded quickly.

![Untitled](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled%202.png)

Moreover, the concern with critical health care is still persistent. ICU Beds (that includes ventilators) saw a very small increase during the second wave. The private health systems responded better here as well during the second wave.

![Untitled](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled%203.png)

### 2. Multi-variate forecast model

Tavakoli M et al. [3] used a SARIMA forecasting model to predict patient loads. I compared SARIMA and fbprophet model and finalised on fbprophet for its better performance. I use the fbprophet timeseries model to forecast the bed-occupancy based on the TPR and number of symptomatic cases. While TPR is suggested as a strong predictor for hospital admissions [1], Römmele C et al [2] suggested that TPR alone is not sufficient as other symptomatic cases would also have to be isolated and treated as per COVID-19 protocols. Thus, I use both TPR and symptomatic cases data to forecast bed occupancy. The model performance is better when compared to the model that used TPR alone.

Data till March 2021 (before second wave) is considered as the training dataset and data during April-August 2021 is considered as the test dataset. My model predicted the peak in bed-occupancy levels at its lower-boundary limit. The model performance is at its optimum when I consider a lag of 7 days in TPR, Symptomatic cases, which is obvious as there would be a lag between getting positively tested and taking a hospital admission. While the confidence bands become broader at longer forecast periods, the model performs better at shorter forecast periods, which is crucial for managing sudden spike in health-care demand.

![Untitled](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled%204.png)

 

![Untitled](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled%205.png)

![Untitled](Bed%20capacity%20management%20during%20COVID-19%20in%20Mumbai%2083ed489f513e4d3193e5df7614e8c5a4/Untitled%206.png)

## Policy implications and future work

A robust short-period forecasts will greatly enable the public officials in planning people, resources and infrastructure for health care management. To further strengthen this model, it has to be tested across other geographies and time periods. Data systems should also be strengthened to improve the model. Deschepper et al. [4] added more features like length of patient stay in the hospital in their model to predict hospital admissions. This data should also be captured.

Moreover, this model can also be applied at hospital level, enabling the hospital management better plan for exigencies. The model can be piloted at various hospitals for validation.

Finally, the model will serve its purpose only when there is government capacity to quickly ramp-up health facilities to meet spike in demand. While the Mumbai city officials were successful in increasing healthcare capacity, the response is slower when compared to private health systems. More collaboration and knowledge transfer between the public and private health systems is thus required for a robust and resilient public health system.

## References

1. [Nikita Kwatra, Rajeswari Parasa. “HOW WELL DID BED CAPACITY RESPOND TO PATIENT NEEDS IN MUMBAI?” July 2021. IDFC Institute.](https://www.idfcinstitute.org/blog/2021/july/covid-19-bed-management-in-mumbai/)
2. [Römmele C et al. “Bed-capacity management in the times of COVID-19 pandemic: A simulation-based prognosis of normal and intensive care beds using the descriptive data of University Hospital Augsburg” August 2021. Anaesthesist.](https://pubmed.ncbi.nlm.nih.gov/32821955/) 
3. [Tavakoli M et al. “Simulation of the COVID-19 patient flow and investigation of the future patient arrival using a time-series prediction model: a real-case study.” February 2022. Medical & biological engineering & computing.](https://pubmed.ncbi.nlm.nih.gov/35152366/)
4. [Deschepper M et al. “Prediction of hospital bed capacity during the COVID− 19 pandemic.” May 2021. BMC Health Services Research.](https://bmchealthservres.biomedcentral.com/articles/10.1186/s12913-021-06492-3)

## Dataset and Python code

Cleaned dataset: [Link](https://github.com/d-saikrishna/TimeSeriesAnalysis/blob/master/Bed%20capacity%20management/master1.csv)

Code for analysis: [Link](https://github.com/d-saikrishna/TimeSeriesAnalysis/blob/master/Bed%20capacity%20management/Bed_capacity_management%20-%20Bed%20capacity%20analysis.ipynb)

Code for multi-variate modelling: [Link](https://github.com/d-saikrishna/TimeSeriesAnalysis/blob/master/Bed%20capacity%20management/Bed_capacity_management%20-%20Forecasting.ipynb)