1. 급식소 음식물 쓰래기 양 데이터
2. 모델에서 사용할 것 같은 parameter 조사
3. 그리고 각 parameter에 해당되는 회사 이름 조사해오기
4. 연간 재활용되는 음식물 쓰래기 양 조사
5. 연간 태워지는 음식물 쓰래기 양 조사
6. 각 회사 수익

GOAL: Minimize the amount of food waste sent to landfills

Korea is not a good country to do this analysis because already 98% of the food waste is recycled.
[Washington Post - How South Korea recycles 98% of its food waste](https://www.washingtonpost.com/world/2024/08/09/south-korea-food-waste-composting/)
[한국음식물류폐기물수집운반업협회](http://fwcta.co.kr/)

국내 폐기물 처리기업의 점유율 (2018)
- TSK 코퍼레이션 17.1%
- EMC홀딩스 12.4%
- 보람씨에스 12.4%
- 동양에코 7.7%
- 부산그린파워 6.8%
- ESG그룹 6.7%
- 코엔텍 3%
- 유니큰 2.5%

[비환경적·비경제적 음식물류폐기물 정책 바뀌어야](https://www.waterjournal.co.kr/news/articleView.html?idxno=62748)

![[Pasted image 20241119124131.png|500]]
![[Pasted image 20241119124147.png|500]]

---
## New York?

## Scale of the Problem

- About one-third of New York City's 24 million pounds of daily garbage is food and other organic waste[5](https://news.climate.columbia.edu/2022/12/05/new-york-citys-food-waste-and-the-circular-economy/).
- Each year, approximately 3.9 million tons of wasted food from New York ends up in landfills[2](https://www.nycfoodpolicy.org/food-waste-food-by-the-numbers/).
- Food waste represents 20 percent of New York City's overall greenhouse gas emissions, making it the third largest contributor behind buildings and transportation[1](https://news.climate.columbia.edu/2023/06/20/food-waste-and-the-complexity-of-new-york-citys-garbage/).

[Food Waste: Food by the Numbers](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=http://www.nycfoodpolicy.org/food-waste-food-by-the-numbers/&ved=2ahUKEwjXgsa5wueJAxUydvUHHV0NG50QFnoECAkQAQ&usg=AOvVaw2hPKrdSQ8ed_-_O2BRtRF8)

[2023 NYC Waste Characterization Study](https://www.nyc.gov/assets/dsny/downloads/resources/reports/waste-characterization-studies/2023/wcs-2023.pdf)
- The 2023 Study reveals that 75% of New York City residential waste is made of up materials that can be diverted from landfill with currently available DSNY-managed programs and private recycling operations. In FY23, DSNY’s diversion rate was 20.2%
- Food Waste: In 2022, New York City residents disposed of 1.2 billion pounds of food. More than 86 million pounds were encased in intact packaging. This represents a substantial opportunity to remove useable food from our waste stream through donation.
	- ![[Pasted image 20241119131349.png|500]]



[NYC Needs Common Sense Waste Management Now](https://nylcv.org/news/nyc-needs-common-sense-waste-management-now/)
- New York City residents produce nearly 13,000 tons of [waste](https://www.grownyc.org/recycling/facts) every single day. 81% of this waste ends up in landfills and incinerators throughout the Northeast region
- As the garbage decomposes, it releases methane, a greenhouse gas 30 times more potent than carbon dioxide. The diesel trucks that transport this waste carry it a distance equivalent to driving more than 312 times around the Earth.


[REGIONAL ORGANIC WASTE PROCESSING CAPACITY](https://cbcny.org/sites/default/files/media/files/Appendix%20B%20-%20Organic%20Waste%20Report_0.pdf)
- ![[Pasted image 20241119134458.png|500]]
- Why aren't they fully utilizing all the capapcity?
	- They process all the food waste that is collected by the companies
	- However most of the food waste is disposed with the normal wastes. Therefore it is hard to recycle food wastes.
	- 회사 이익 문제라기 보다는 제도적으로 사람들이 음식물 쓰레기를 분리배출하지 않는게 문제

Curbside Compost 
- 퇴비를 판매 [Curbside Compost Delivers Premium Compost, Garden Soil, Top Soil and Mulch](https://www.curbcompost.org/compost-delivery.html):
	- 1야드: $243.60/야드
	- 2-3야드: $157.50/야드
	- 4야드: $135.45/야드
- 음식물 수거(코네티컷과 뉴욕 지역)
	- ![[Pasted image 20241119135843.png|400]]
	- 수거한 모든 음식물 쓰레기 재활용 - __여기도 다 사용하는데...__
	- 이유: 환경 측면, 퇴비 배달 서비스

Natural Upcycling - Noblehurst Farms
1. Natural Upcycling은 현재 7개 주에서 운영되며, 연간 100,000톤 이상의 음식물 쓰레기를 수거합니다.
2. 수거된 음식물 쓰레기의 75%는 혐기성 소화로 처리되고, 25%는 퇴비화, 동물 사료, 또는 토지 적용에 사용됩니다.
3. Noblehurst Farms는 하루에 약 100톤의 음식물 쓰레기를 처리하며, 이는 소의 분뇨와 함께 혐기성 소화조에서 처리됩니다.
4. 소화조에서 생산된 바이오가스는 전기 생산에 사용되며, 농장과 인근 크리머리에 전력을 공급합니다.

Royal Waste Services - McEnroe Organic Farm (in Millerton NY)

---

__모델링 - 쓰레기 수거 업체가 매립하거나 재활용 업체에 보내는 것 중에 선택할 수 있는 경우__
- 2023년 기준으로 미국의 평균 매립 비용은 톤당 $56.8
	- [ANALYZING MUNICIPAL SOLID WASTE LANDFILL TIPPING FEES](https://erefdn.org/analyzing-municipal-solid-waste-landfill-tipping-fees/)
- 음식물 쓰레기 1톤을 동물 사료로 생산하는 데 드는 비용은 약 $93.8
	- [Triple Bottom-Line Evaluation of the Production of Animal Feed from Food Waste: A Life Cycle Assessment](https://link.springer.com/article/10.1007/s12649-022-01914-7).
- $c$: 소비자 비용 -> 쓰레기 수거 회사 (if 쓰래기 매립)
- $c+r$: 소비자 비용 -> 쓰레기 수거 회사 (if 쓰래기 재활용)
- $\$56.8/ton$: 쓰래기 수거회사 -> 쓰래기 매립
- $\$93.8/ton$: 쓰래기 수거회사 -> 쓰래기 재활용
- $\$p/ton$: 쓰래기 재활용으로 만들어진 비료를 팔았을 때 이익
- $\$d$: 정부에서 음식물 쓰래기 매립을 적발 했을 때 벌금 + 소비자 punishment 
- $\alpha$: 적발 확률(?)
	- 너무 똑같은데...

---

__Parameters__
- $\alpha$: Parameter that needs to be optimized
- $\rho\sim N(0.88~0.92,?)$ 
	- [Percentage of non-compostable food waste](https://cemonitor.be/en/indicator/food/waste/share-of-food-waste-in-residual-household-waste/)
	- [“Non-compostable materials (**NCM**) reach percentages between 8 and 12% of organic waste disposed](https://resoilfoundation.org/en/circular-bioeconomy/compost-non-compostable-materials/)
- $w$ = 108 $/ton
	- 0.425 kg/L
		- [# Community Fund: Volume to Kgs](https://www.merseysidewda.gov.uk/volume-to-kgs/)
	- 49.09 $/month, 65 gallon/week
		- [# Commercial Franchise Garbage & Recycling Rates](https://www.villageofgrayslake.com/466/Commercial-Garbage-Recycling-Rates)
	- $49.09\frac{dollars}{month} 0.230137\frac{month}{week} 1/65 \frac{week}{gallon} 0.264172\frac{gallon}{L} 1/0.425\frac{L}{kg}1000\frac{kg}{ton}=108\frac{kg}{ton}$
- $D = 13000$ $tons/day$
- $P$: Calculated profit
- $Cost$: Calculated cost
- $p = 150\frac{dollars}{yard^3}\cdot 1.4 \frac{yard^3}{ton_{compost}} \cdot 0.4 \frac{ton_{compost}}{ton_{food waste}} = 84\frac{dollars}{ton_{food waste}}$
	- 1ton of food waste $\rightarrow$ 360~544kg of compost
		- [How Many Compost Make From 1 Ton of Organic Waste](https://fertilizerequipmentmanufacturer.com/how-many-compost-make-from-1-ton-of-organic-waste/)
	- Average $150$ $dollars/yard^3$
		- [Curside Compost](https://www.curbcompost.org/compost-delivery.html)
	- Average $1.4ton/yard^3$
		- [# Soil Calculator](https://www.inchcalculator.com/soil-calculator/)
	- Percentage compost sold: ?
		- 어디서 보긴 했는데
- $c$: cost per capacity
	- At least $c<p$?
	- $93.8/ton
	- [Triple Bottom-Line Evaluation of the Production of Animal Feed from Food Waste: A Life Cycle Assessment](https://link.springer.com/article/10.1007/s12649-022-01914-7).
- $l$(landfill cost):  $56.8/ton
	- [ANALYZING MUNICIPAL SOLID WASTE LANDFILL TIPPING FEES](https://erefdn.org/analyzing-municipal-solid-waste-landfill-tipping-fees/)
- $d$: Contract information - at least larger than the interest rate
	- Interest rate in US: 4.75%
	- I do think 10~20% is the reasonable discount percentage

Parameters
- $\alpha$: Parameter that needs to be optimized
- $\rho\sim N(0.8,?)$
- $w$ = 110 $/ton
- $D = 1000$ $tons/day$
- $p = 80\frac{dollars}{ton_{food waste}}$
- $c$ = $90/ton
- $l$ = $50/ton
- $d$ = 0.1