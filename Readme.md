## Problem Statement:
* Create a Machine learning application which predicts the estimated time and date for the final closure of a opened ticket based on the given attributes.

## Dataset Information:
* This is an event log of an incident management process extracted from data gathered from the audit system of a platform used by an IT company. Information was anonymized for privacy.

* Number of instances: 141,712 events (24,918 incidents) /Each even corresponds to an update that is made to the incident.
* Number of attributes: 36 attributes.

## Steps:
* Data is cleaned by replacing all the missing values with 'unknown'.
* For this project I have kept only the incidents that are already closed.
* Some incidents are removed by using outlier identification methods using z scores.
* I have kept only those features that are available at the begining of the incident creation. The idea is to use only the information available to us at the time of incident creation and predict the closure time of the incident.
* I have treated this problem as a regression problem. I have taken minimum opened time as a fixed time stamp from opened_at feature of the incident and converted opened_at and closed_at as time differences in seconds.
* The target is to predict the time of completion as seconds and add them to the fixed time stamp to get exatc date and time of ticket closure.

## Inputs:
* Some of the inputs that are used are:
    - caller_id: identifier of the user affected;
    - opened_by: identifier of the user who reported the incident;
    - opened_at: incident user opening date and time;
    - sys_created_by: identifier of the user who registered the incident;
    - contact_type: categorical attribute that shows by what means the incident was reported;
    - location: identifier of the location of the place affected;
    - category: first-level description of the affected service;
    - subcategory: second-level description of the affected service (related to the first level description, i.e., to category);
    - u_symptom: description of the user perception about service availability;
    - impact: description of the impact caused by the incident (values: High; Medium; Low);
    - urgency: description of the urgency informed by the user for the incident resolution (values: High; Medium; Low);
    - priority: calculated by the system based on 'impact' and 'urgency';
    - assignment_group: identifier of the support group in charge of the incident;
    - assigned_to: identifier of the user in charge of the incident;
    - knowledge: boolean attribute that shows whether a knowledge base document was used to resolve the incident;
    - u_priority_confirmation: boolean attribute that shows whether the priority field has been double-checked;
    - notify: categorical attribute that shows whether notifications were generated for the incident;
## Results:
* Using XGBoost I could predict the closure time in
    - Train: Mean absolute Deviation of 7.0 H: 3.0 M: 27.18 S
    - Validation: Mean absolute Deviation of 1.0 D: 5.0 H: 18.0 M: 22.78 S
