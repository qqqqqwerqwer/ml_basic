```python
date_977 = org_date[0:2092]
time_977 = date_983['time']
time_977_un = time_983.unique()
dic_977 = {}  # 将每个工作站的结果放在字典里，键为时间段，值为列表，元素为每个订单在该时间段内对应的工作时间

for i in range(0,2092):
    for j in time_977_un:
        if date_77['time'][i] == j:
            b=pd.to_datetime(j)
            if org_date['end_time'][i] < (b+datetime.timedelta(hours=1)): # 将工作结束时间与开始时间的相对差作为判断条件
                 # 将订单对应的工作时间添加到对应的列表中
                dic_977.setdefault(b,[]).append((org_date['end_time'][i]-org_date['start_time'][i]).seconds/3600)
            elif org_date['end_time'][i] < (b+datetime.timedelta(hours=2)):
                dic_977.setdefault(b,[]).append(1 -(org_date['start_time'][i]-b).seconds/3600 )
                dic_977.setdefault(b+datetime.timedelta(hours=1),[]).append((org_date['end_time'][i]
                                                                             -(b+datetime.timedelta(hours=1))).seconds/3600)
            elif org_date['end_time'][i] < (b+datetime.timedelta(hours=3)):
                dic_977.setdefault(b,[]).append(1 -(org_date['start_time'][i]-b).seconds/3600 )
                dic_977.setdefault(b+datetime.timedelta(hours=1),[]).append(1)
                dic_977.setdefault(b+datetime.timedelta(hours=2),[]).append((org_date['end_time'][i]
                                                                             -(b+datetime.timedelta(hours=2))).seconds/3600)
            else:
                dic_977.setdefault(b,[]).append(1 -(org_date['start_time'][i]-b).seconds/3600 )
                dic_977.setdefault(b+datetime.timedelta(hours=1),[]).append(1)
                dic_977.setdefault(b+datetime.timedelta(hours=2),[]).append(1)
                dic_977.setdefault(b+datetime.timedelta(hours=3),[]).append((org_date['end_time'][i]
                                                                             -(b+datetime.timedelta(hours=2))).seconds/3600)

final_977 = pd.DataFrame()
work_977 = [sum(i) for i in dic_977.values()] # 对字典中的各个列表分别求和
final_977['时间段'] = dic_977.keys()
final_977['terminal_id'] = ['T-977']*len(work_977)
final_977['work_time'] = work_977
final_977['utilization_rate'] = ['{:.2%}'.format(i/24) for i in work_977]
```
