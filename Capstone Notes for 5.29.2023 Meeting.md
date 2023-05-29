Aidan Capaldi

#### Research Items and Questions: 
- Learn more about HVM including but not limited to:
	- What is it and how does it work? --> Answered by Eli, but I should do my own reading to understand it better. 
		- Interaction nets and how they work
	- Is it feasible to use this for the skating project? In what ways could we use the proposed processor / executor to handily process IMU and accelerometer data? 

##### What is HVM? 
HVM (Higher-order Virtual Machine) is a functional language which compiles to a novel runtime. HVM is lazy and massively parallel, and does not have a garbage collector. Generally, this runtime aims to turn functional programs into far more efficient versions of the same program. 

##### Interaction Combinators
Interaction nets represent a new model for computation. There exist several models for computation (Turing machines, Cellular automata, and Rewrite systems).
- Turing machines --> register machines and stack machines, simple, powerful, but sequential. 
- Cellular automata --> approximations of physical processes, globally synchronrized.
- Rewrite systems --> λ calculus 
- ```latex     (\theta x.u)v \xrightarrow v[u/x]```
The two fundamental laws of computation are commutation and annihilation. 

Brief explanation of Interaction Nets as introduced by the paper's cited theory:
Alpha is used to represent a call with arity n greater than 0. Cells get to have auxiliary ports and principal ports. 
Nets are graphs of a finite number of cells and an extra set of free ports. Ports are connected by wires. Cells which exist in a finite alphabet with respective arbitrary arities can be shown to be reduced to single cells with given rules proved in the paper. 

The paper moves on to show parallel examples for rules in Turing machines and Cellular automata. Using unary arithmetic as an example, we can see that nets can be irreducible or reducible. 

Principal path of length `n` consists of cells `c_1 \ldots c_n` such that the principal port of `c_i` is connected to an auxiliary port `c_{i+1}`. Vicious circle of length `n` is a closed principal path of length `n`. 

Section 2 gets into the allowed interaction rules for the combinators, which is the important part.

TBA to be continued with research continuing, but the meeting is soon.



###### Sources 
[Interaction Nets Research Paper](https://pdf.sciencedirectassets.com/272575/1-s2.0-S0890540100X00600/1-s2.0-S0890540197926432/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEEEaCXVzLWVhc3QtMSJHMEUCIAT1JRvRk8MOgQS2jIr09jU3eWVtDPXgHwhcxBDMorrDAiEA9JGz6EIz1Kx%2F5cEVEPCmFoRqz1MNOQMVyLr1Ftx6OD0qswUIeRAFGgwwNTkwMDM1NDY4NjUiDFQyMAsdGV%2B9jmICWiqQBbOkuIiuCpXb%2BTpAOYnRhDXqha80bloDCaJ%2B8fEvSmS2W8qED4sI7CQMZonm64uh1KEEHduEj7Zxq4Is6wzz8U5PI0mEveI7RsS%2BLucBQV08GvIBcXJ6PnkFjq8SG3pIaBM4DDJT4YQURM703VDj1epL7i3RIAp6PBmxV%2BpeFMQ8cXlaDGNf6g9XLuDx3K%2B5z%2BpnArRzlFF1FJuO50C83h1Y4Vef5qw7PjkXqCcixqjppihd7QGf4pVs99%2FzIxPHQIjYK6t19T2XGt5F73L%2FB3ZDj3A%2Bba9PHWcmD80Cuow5V0TOihR5gX7WjY0sbH%2FeWu44cjVusE7vhzFCLWfjuc8KdN%2FTzihOOuqtTxTEslNI2grzakJopay10sMcBfB1NOxzogqdXN%2BZSa3w%2FQOkLP7Ue1NYZkUFstjI1jCiO9gPSEyAJRNzcJ%2FiqIDkFa%2Fd7c0swMpm%2F8FKGq8Ails%2FqBwRXRz68ztQ%2Fhft7koQS6%2FjstZb6IOsoZ5SOu0FafOZQg4zN2wH0iF6VI%2BXJ3WokVS9M9F2HFha9G5govpw1J9EZyKaBVFVB0KaORajLG1nXmaJMlRr%2BedgPuLgPHfEcmMqxrxakwAPpXRq3cv14fczwSCeTiXVnMcYiqSf5ZmK46Pc3xn0sUAZ3e6Q862jJpaDjgSsHmZMEttLq4eTybzUc3hOY6pwsJ%2B8JS%2F4%2FuZja%2BbpDF0Hth4hREchuUVWDH6yag8OluuX9i0ABP4g6B7E8r7GB%2FSIWNQAZNqVUlYi5zYpiuGkcCxHRs4U79Hw8OpzysqJtvpKCExUluieYLmjrjge7ogyxITk8HKm1R9v6U3jcwEHckDj4TY4kkiEuH6f9URXxRHgkTmzwQNABstYMPOb06MGOrEBln5JB8dvG%2F3VWPRxvek19W8o%2BMBc7LeFs%2BlRiQiAlxDz9IVnf3oOT1L5f9OapAKlW4kuAuQkollXigrrwkX6qZHuL%2Bjt76gjYLleIdURpe3BKwcKB5nmy7YNnzMsItHIgRwggPY8eyUUpr5aNOFASuR%2F9Wti%2Fjnvj5OzNuq2LkF8k5ERyz53vti06x3%2BRXzPH%2F5bpHFJOfbJLYFry5JLhLPk902VM%2F9SFo94hMSNTldH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230529T171542Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYUOE2TMER%2F20230529%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=9a82bc9a449ea6d3903a8ccd300fc69be4d0a34c5775b157ec67144a582a4f1a&hash=ad0eaf87d95662f9549abd5e7d2832481323157fa45412f290c9e5ffd77508d1&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S0890540197926432&tid=spdf-7aab465a-2ab5-4b3d-846e-3d39312cb13f&sid=31a9fd2e2ac9f54e9c5b2e9963692c98d76bgxrqa&type=client&tsoh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&ua=131d5103015754555a5d&rr=7cf06188da7aff88&cc=us)

[HVM README](https://github.com/HigherOrderCO/HVM)
