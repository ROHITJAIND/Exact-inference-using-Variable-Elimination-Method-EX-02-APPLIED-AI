# EX-02 Implementation of Exact Inference Method of Bayesian Network
### Aim:
<table>
<tr>
<td width=80%>

To implement the Inference Burglary P(B|j,⥗m) in alarm problem by using Variable Elimination method.
</td> 
<td>
  
**DATE : 00.00.2024**
</td>
</tr> 
</table>
 
### Algorithm:
Step 1: Define the Bayesian Network structure for alarm problem with 5 random variables,Burglary, Earthquake, John Call, Mary Call and Alarm.<br>
Step 2: Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class.<br>
Step 3: Add the CPDs to the network.<br>
Step 4: Initialize the inference engine using the VariableElimination class from the pgmpy library.<br>
Step 5: Define the evidence (observed variables) and query variables.<br>
Step 6: Perform exact inference using the defined evidence and query variables,and print the results<br>

### Program :
##### IMPORTING LIBRARIES
```Python
from pgmpy.models import BayesianNetwork
from pgmpy.inference import VariableElimination
from pgmpy.factors.discrete import TabularCPD
```
##### DEFINING MODEL STRUCTURE
```Python 
alarm_model = BayesianNetwork([("Burglary", "Alarm"),("Earthquake", "Alarm"),
                               ("Alarm", "JohnCalls"),("Alarm", "MaryCalls"),])
```
##### DEFINING PARAMETERS USING CPT
```Python
cpd_burglary=TabularCPD(variable="Burglary", variable_card=2,values=[[0.999], [0.001]])
cpd_earthquake=TabularCPD(variable="Earthquake", variable_card=2,values=[[0.998], [0.002]])
cpd_alarm=TabularCPD(variable="Alarm",variable_card=2,
                       values=[[0.999,0.71,0.06,0.05],[0.001,0.29,0.94,0.95]],
                       evidence=["Burglary","Earthquake"],evidence_card=[2,2],)
cpd_johncalls=TabularCPD(variable="JohnCalls",variable_card=2,values=[[0.95, 0.1], [0.05, 0.9]],
                           evidence=["Alarm"],evidence_card=[2],)
cpd_marycalls=TabularCPD(variable="MaryCalls",variable_card=2,values=[[0.99, 0.3], [0.01, 0.7]],
                           evidence=["Alarm"],evidence_card=[2],)
```
##### Associating the parameters with the model structure
```Python
alarm_model.add_cpds(cpd_burglary, cpd_earthquake, cpd_alarm,cpd_johncalls, cpd_marycalls)
```
##### Checking Result:

```Python
inference=VariableElimination(alarm_model)
evidence={"JohnCalls":1,"MaryCalls":0}
query='Burglary'
res=inference.query(variables=[query],evidence=evidence)
print(res)
```

### Output :
![image](https://github.com/user-attachments/assets/7dc257d5-b393-4d23-bfed-e60355663991)

### Result :
Thus, Bayesian Inference was successfully determined using Variable Elimination Method

**Developed By: ROHIT JAIN D - 212222230120**
