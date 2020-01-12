# Traffic Light Control Assistance for an Isolated Intersection in Dhaka City

According to the habitants, traffic congestion is a severe , if not the most severe problem in Dhaka’s urban life[3]. RSTP, 2015 says that average daily speed of traffic is 6.8 kmph in Dhaka which is slightly above average walking speed[1]. A 2017 press release by World Bank blamed the infamous traffic congestion of killing 3.2 million working hours a day[12]. It also has horrendous economic consequences. RSTP for Dhaka estimated the cost to be 11.4 Billion USD on the 2014[1]. 

Different methodologies can be applied to tackle the traffic congestion prob- lem. Bart De Schutter and B De Moor pointed out four specific methods[5]: 
		
 - Construction of new infrastructures, i.e., roads, flyovers, etc. 
 - Promoting public transports. 
 - Reducing demand by introducing taxes and tolls for using specific infras- tructure. 
 - Ensuring optimized usage of existing resources. 

The first three strategies are only useful when the fourth is present. if the optimal usage of resources can not be ensured, adding new resource can not assure the solution to the problem rather than creating a bottleneck in the overall system.

The amount of car on the road is the main key factor of traffic congestion in Dhaka city. And According to Bangladesh Road Transport Authority (BRTA) data, until April 2018, there were 11,15,654 vehicles in Dhaka City in total[4]. A study by Mahmudul and Haque shows there are only 5% primary roads in Bangladesh[9]. So, our traffic intersections need to regulate a quite larger number of vehicles than those were originally designed for. And thus a real-time adaptive traffic control assistance system is required in this city.

The government tried introducing fixed-time based automated traffic light controlling systems back in 2015 but, that caused massive traffic congestion in the city[10]. The fixed-time control system does not consider the present traffic situation. So, in these scenarios, an real-time adaptive system can analyze the traffic and take near-optimal decisions[11]. But, due to ill-thought road design and socio-political aspects, fully automated systems will have a lower success rate.

This paper proposes a system which is real-time adaptive and also will require human involvement. The proposed system uses Google Maps traffic data for its real-time analysis. Using an efficient and comparatively simple implementation the near-optimal solution is obtained which is passed on to a handheld device of the responsible person to provide a suggestion about the optimal green light duration for each entry roads of an intersection. This duration is calculated to minimize the average waiting time for each vehicles using mathematical models derived by S. Lämmer et al. [7, 8] This system also logs its findings in a database server for future use.

# Implementation
## Scenario

For this study, SAARC Fountain intersection (N 23.819 144 1 ◦ , E 90.452 595 4 ◦ ) was chosen because of its homogenous and near-saturated traffic flow. This in- tersection has 5 entry roads. The road section length has been set to 500 meter.
## System Structure
![enter image description here](https://i.imgur.com/c7cjq8F.jpg)
**Handheld Device** This can be any mobile device that supports a web browser, e.g., Android, iOS or KaiOS phones. A native or web application chronologically sends request to server using RESTful API and receives JSON response with near-optimal green time for each entry points of the intersection.

**Application Server** Application server hosts the RESTful API endpoints. On arrival of the requests from the client, this server runs its headless browser module that returns the screenshot of the intersection with the traffic data layer from Google Maps JS API. The application server has an image processing program developed with C++ and OpenCV library that scans the screenshot image and after calculating near-optimal solution using an equation, it returns the optimal green time for each entry roads in JSON format.

**Database Server** Application server logs all extracted data into this database server for future usage. Advanced Artificial Intelligences could be trained to solve this type of problems even with more accuracy and efficiency with these data in the future.

	
## References
1. Almec Corporation Global Oriental Consultants International Katahira & Engi-
neers. The Project on the Revision and Updating of the Strategic Transport Plan
for Dhaka(Draft). (November):1–509, 2015.
2. Erik Björck. A comparison of algorithms used in traffic control systems A com-
parison of algorithms used in traffic control systems. 2018.
3. BRAC Institute of Governance and Development. The State of Cities 2016: Traffic
Congestion in Dhaka City- Governance Perspectives. Number January. 2016.
4. BRTA. Number of registered Motor Vehicles in Dhaka (year wise). (1):20, 2018.
5. B. De Schutter and B. De Moor. Optimal Traffic Light Control for a Single Inter-
section. European Journal of Control, 4(3):260–276, jan 1998.
6. F.V.Webster and Technical Paper. Traffic Signals Webster. Road Research Tech-
nical Paper, (39):1–44, 1958.
7. S. Lämmer, R. Donner, and D. Helbing. Anticipative control of switched queueing
systems. The European Physical Journal B, 63(3):341–347, jun 2008.
8. Stefan Lämmer and Dirk Helbing. Self-control of traffic lights and vehicle flows in
urban road networks. Journal of Statistical Mechanics: Theory and Experiment,
2008(04):P04019, apr 2008.
9. SMS Mahmud, MS Hoque, and GMM Bashir. Deficiencies of Existing Road Net-
work in Dhaka Metropolitan City. Publication in 10th Pacific . . . , 2008.
10. Suliman Niloy. Use of modern automated traffic signalling system causes gridlocks
in Dhaka, may 2015.
11. Steven G. Shelby. Single-intersection evaluation of real-time adaptive traffic signal
control algorithms. Transportation Research Record, (1867):183–192, 2004.
12. World Bank. A Modern Dhaka is Key to Bangladesh’s Upper-Middle Income
Country Vision, 2017.

[This documentation is adapted from [this paper](https://www.academia.edu/40986160/Traffic_Light_Control_Assistance_for_an_Isolated_Intersection_in_Dhaka_City).]
