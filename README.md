CIVE 202 - Project1

Question 1
nebraska_summary = nebraska_data.groupby(['pws_type','contaminant']).size().reset_index(name = 'n')
print(nebraska_summary)
nebraska_summary.to_csv('contaminants in water.csv', index=False)
stat_summary = nebraska_summary.groupby('pws_type').agg(max=('n','max'),
                                                                    min=('n','max'),
                                                                    mean=('n','mean'),
                                                                    median=('n','median'))
print(stat_summary)
stat_summary.to_csv('violations.csv', index=False)

Question 2
def assign_category(x):
    if x<=500:
       return "very small"
    elif 501<=x<=3300:
       return "small"
    elif 3301<x<=10000:
       return "medium"
    elif 10001<=x<=100000:
       return "large"
    else: 
       return "very large"
nebraska_data['population_category'] = nebraska_data['population'].apply(assign_category)
subset1 = nebraska_data[(nebraska_data['activity_status']=="Active")]
summary2 = subset1.groupby(['pws_type','contaminant','pop_category']).size().reset_index(name='quantity')
print(summary2)
summary2.to_csv('Final Summary Question02.csv',index=False)

Question 3
subset3 = nebraska_data[(nebraska_data['activity_status']=="Active") &
(nebraska_data['violation_type']== "Maximum Contaminant Level Violation, Single Sample") |
(nebraska_data['violation_type']== "Maximum Contaminant Level Violation, Average") |
(nebraska_data['violation_type']== "Maximum Contaminant Level Violation, E. coli (RTCR)") |
(nebraska_data['violation_type']== "Maximum Contaminant Level Violation, Monthly (TCR)") |
(nebraska_data['violation_type']== "Maximum Contaminant Level Violation, Acute (TCR)")]
summary3 = subset3.groupby(['primary_source', 'violation_type','pop_category','pws_type',"contaminant"]).size().reset_index(name='quantity')
summary4 = summary3[(summary3['pop_category']=="small")]
summary5 = summary4[(summary4['pws_type']=="CWS")]
print(summary5)
summary5.to_csv("Request4.csv", index=False)
![image](https://github.com/user-attachments/assets/8894ad59-5c39-4b0b-9b06-043aaef825e2)
