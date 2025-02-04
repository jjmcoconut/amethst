by [Linbo Luo](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Luo/Linbo), [Suiping Zhou](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Zhou/Suiping), [Wentong Cai](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Cai/Wentong), [Malcolm Yoke Hean Low](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Low/Malcolm+Yoke+Hean), [Feng Tian](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Tian/Feng), [Yongwei Wang](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Wang/Yongwei), [Xian Xiao](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Xiao/Xian), [Dan Chen](https://onlinelibrary-wiley-com.libra.kaist.ac.kr/authored-by/Chen/Dan)
https://onlinelibrary-wiley-com.libra.kaist.ac.kr/doi/abs/10.1002/cav.238

__Goal of this paper__
- Develop a model/simulation framework that efficiently generates real human action for crowded people by making the model think as the way human does

![[Pasted image 20240728220553.png|300]]
__Design__
- Splits into 3 modules
	- Upper layer: Crowd behavior module, Individual behavior
		- Make inference about current situation
		- Select proper action for each agent
	- Lower layer: Physical behavior
		- Put inputs into Upper layer
		- Execute selected behavior by decomposing into sequences of basic actions

![[Pasted image 20240728220532.png|300]]
__Development__
- Crowd population: first generated & initiated by crowd initializer
	- Distribution of different types of agents
		- Based on roles, ages, social relationships, personalities
- _Agent instance_ access the shared state in _virtual world database_ each step
- _Agent instance_ has _situation awareness_ module that collects observations in surroundings and virtual world
- _Global event generator_ generates events that significantly impacts the environment and some agents
- _Situation awareness_ module can keep track of global events
- _Agent attribute_ is agent's internal attributes and can be affected by situational changes
- _Inference engine_ analyzes info from _agent attributes_ and _situational awareness_ then makes inference about the next behavior according to decision rules
- _Behavior repository_ receives the selected behavior
- _Behavior Execution_ module executes the selected behavior
- Agents can interact with each other by exchanging control information & neighborhood states
- _Visualization_ platform receives agent's actions and renders it

__Situation Awareness__
