---
layout: post
title: "Flygskam and o caminho da Corunha"
tags: igalia
---

## Prolegomenon

Early next June, I'm traveling from Paris to A Coruña for the [Web Engines Hackfest](https://webengineshackfest.org/) and other internal Igalia events.
In recent years I've done it by train, as [previously](https://frederic-wang.fr/2019/12/10/review-of-my-year-2019-at-igalia/#paris---a-coru%C3%B1a-by-train) [mentioned](https://frederic-wang.fr/2022/06/17/short-blog-post-from-madrid-s-hotel-room/).
Some colleagues at Igalia were curious about it so I decided to write this blog post, investigating possible ways to do it from various European places.
I wish this can also motivate more people at Igalia and beyond, who are still hesistant to give up alternatives with heavier carbon footprint.

In addition to various trip planners, I've also used this nice map from Wikipedia, which gives a good overview of high-speed rail in Europe:

<div style="max-width: 512px; margin-left: auto; margin-right: auto">
     <a title="Original PNG : User:Bernese media, User:BIL 2011 SVG version: User:Akwa and others (see the history &amp; the source file), CC BY-SA 3.0 &lt;https://creativecommons.org/licenses/by-sa/3.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:High_Speed_Railroad_Map_of_Europe.svg"><img width="512" alt="High Speed Railroad Map of Europe" src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/High_Speed_Railroad_Map_of_Europe.svg/512px-High_Speed_Railroad_Map_of_Europe.svg.png?20240202110242"></a>
</div>

I also sought advice from [Nicolò Ribaudo](https://www.igalia.com/team/nribaudo) who is quite familiar with train traveling and provided useful recommendations.
In particular, he mentioned the [ÖBB trip planner](https://fahrplan.oebb.at/), which seems quite efficient combining trains from multiple operators.

I've focused on big european cities (with airports) that are close to Spain but this is definitely not exhaustive.
There is probably a lot more to discuss beyong trip planning, but hopefully that can be a good starting point.

## Paris as a departure or connection

Based on my experience traveling from Paris, I found these direct trains between big cities:

* Renfe offers several [AVE](https://en.wikipedia.org/wiki/AVE) and [Alvia](https://en.wikipedia.org/wiki/Alvia) trains traveling every days between A Coruña and Madrid, with a duration 3h30-4h [^1]. There are two important thing to note:
  1. These local trains are only avalailble for sell maybe 2 months in advance at best.
  2. These trains are connecting to [Madrid Chamartín](https://en.wikipedia.org/wiki/Madrid_Chamart%C3%ADn_railway_station) which is maybe 30 minutes away from [Madrid Atocha](https://en.wikipedia.org/wiki/Madrid_Atocha_railway_station) by the [Madrid metro](https://en.wikipedia.org/wiki/Line_1_(Madrid_Metro)).
* Renfe also proposes even more options (say one each half hour during the day) between Barcelona and Madrid Atocha, with a duration of 2h30-3h [^2].
* The [SNCF](https://www.sncf-connect.com) proposes [two or three direct trains during the day](https://www.sncf-connect.com/en-en/train/timetables/paris/barcelona) between [Paris Gare de Lyon](https://en.wikipedia.org/wiki/Gare_de_Lyon) and Barcelona, with a duration of 6h30-7h. If you are coming from Paris and want to to take a train to Madrid, you will likely have to cross the station and pass some x-ray baggage scanner, so be sure to keep enough time for the connection.
* The [Eurostar](https://www.eurostar.com/) offers several options during the day to connect Paris with cities below. They connect to [Gare du Nord](https://en.wikipedia.org/wiki/Gare_du_Nord) or [Gare de l'Est](https://en.wikipedia.org/wiki/Gare_de_l%27Est), which are very close to each other but ~30 minutes away from Gare de Lyon by public transport.
  - [Brussels](https://www.sncf-connect.com/en-en/train/timetables/brussels/paris) (duration ~1h30)
  - [Amsterdam](https://www.sncf-connect.com/en-en/train/timetables/amsterdam/paris) (duration ~3h30)
  - [London](https://www.sncf-connect.com/en-en/train/timetables/london/paris) (duration ~2h30)
  - [Cologne](https://www.sncf-connect.com/en-en/train/timetables/cologne/paris) (duration ~3h30)

Personally, I'm doing this one-day-and-half trip (inbound trip is similar):
  1. Take the train from Paris (9:42 AM) to Barcelona (4:33 PM).
  2. Keep enough time for the Barcelona Sants connection.
  3. Take a train from Barcelona to Madrid in the evening.
  4. Stay one night in Madrid.
  5. Take a train from Madrid to A Coruña in the morning.

From London, Amsterdam, Brussels, Berlin one could instead do a two-days trip:
  1. Travel to Paris in the morning [^3].
  2. Keep enough time for the Paris connection.
  3. Take the train from Paris (2:42PM) to Barcelona (9:27PM).
  4. Stay one night in Barcelona.
  6. Travel from Barcelona to Madrid Atocha.
  7. Keep enough time for the Madrid Metro connection.
  8. Travel from Madrid Chamartín to A Coruña.

I also looked at the trip with the minimum number of connections to go to Barcelona from big cities in Switzerland and a a similar traject is possible. See later for alternatives.

Finally, Nicolò mentioned that [ÖBB](https://www.oebb.at/) recently started running a night train from Berlin to Paris, which you can probably use to do a similar trip as mine.

## Estimate of CO<sub>2</sub> emissions

In order to estimate CO<sub>2</sub> emission for the trips suggested in the previous section, I compiled information from different sources:

- [Eurostar sustainability 2023](https://www.eurostar.com/us-en/sustainability),  independent study carried out by EcoRes SCRL in July 2023.
- [The own data provided by SNCF](https://ressources.data.sncf.com/explore/dataset/emission-co2-tgv/information/).
- [Ecopassenger](https://ecopassenger.hafas.de), developed in cooperation with the International Railways Union, the Sustainable Development Foundation and the German Institute for Environment and Energy.
- [Ecotree](https://ecotree.green/en/no-more-offsetting) a company for tree planating providing a CO<sub>2</sub> emission calculator.

There would be a lot to discuss about the methodology but the goal here is only to give a rough idea. Anyway, below is an estimate of kilograms of CO<sub>2</sub> per passenger for some of the train trips previously mentioned:

|  | Eurostar | SNCF | Ecopassenger [^4] | Ecotree |
| - | - |  - |  - |  - |
| Berlin ↔ Cologne   | - |  - |  17-19 | 1-3 |
| Cologne ↔ Paris   | 5.2 | 5.2 | 7.4 | 1-3 |
| London ↔ Paris  | 2.4 |  2.4 | 1.7 | 1-3 |
| Brussels ↔ Paris  | 1.6 |  1.8 | 1.8 | 1-2 |
| Amsterdam ↔ Paris | 2.6 |  2.9 |  9.3-9.5 | 1-3 |
| Paris ↔ Barcelona   | - |  3.8 |  - |  1-6 |
| Barcelona ↔ Madrid   | - |  - |  17-20 |  1-6 |
| Madrid ↔ A Coruña   | - |  - |  - | 1-3 |

The best/worst cases are compiled into the following table and compared with a flight to A Coruña (with a connection by Madrid) as calculated by Ecotree. If we follow these data, a train from Berlin, London, Paris, Brussels and Amsterdam won't at worst be around 50kg of CO<sub>2</sub> per passenger and represent at least a reduction of around 90% compared to using a plane:

| Departure | Flight by Madrid (Ecotree) | Train [^5] | CO<sub>2</sub> reduction |
| - | - | - | - |
| Berlin | 448 | 6-55.4 | ≥87% |
| London | 388 | 4-32 | ≥91% |
| Brussels | 396 | 4-30.8 | ≥92% |
| Amsterdam | 396 | 4-38.5 | ≥90%|
| Paris | 368 | 3-29 | ≥92%|
| Madrid | 244 | 1-3 | ≥98%|

## More cities and trains

**Disclaimer: This section is essentially based on information provided by Nicolò and what I found on internet.**

In addition to the SNCF train previously mentioned, [Renfe](https://www.renfe.com/content/dam/renfe/es/Viajeros/Secciones/Prepara-tu-viaje/ave-francia/pdf/ave-francia-horarios-2023-2024-en.pdf) proposes two trains that are quite important for traveling from France to Spain:

* One train between Lyon and Barcelona per day (duration ~5h)
* One train between Marseille and Madrid per day (duration ~8h)

From Switzerland, you can pass by the south of France using more trains/connections to arrive faster in Barcelone than what was previously proposed. For example, taking a local train to go from Genève to Lyon followed by the Lyon to Barcelona train mentioned above can be done in around 7h. From Zurich, with connection at Genève and Lyon, it takes around 10h as opposed to 12h for a single connection in Paris.

From the Netherlands, Belgium or Germany it makes sense to consider the night trains from Paris to the border with Spain. Those trains do not have a fixed schedule, but vary depending on the weekday. Most of them arrive in [Portbou](https://en.wikipedia.org/wiki/Portbou_railway_station) and from there you can take a regional train to Barcelona. Some of them arrive to [Latour-de-Carol](https://en.wikipedia.org/wiki/Latour-de-Carol-Enveitg_station), and from there it's three hours on a regional train to Barcelona. In any case, you'll be early enough at the border so that it's possible to then arrive to A Coruña in the afternoon or evening. Rarely the night train arrives at the border on the west coast, and continuing from there to A Coruña with the regional trains that go on the northern coast might be a good experience.

From Belgium it's also possible to take a TGV from Brussels to Lyon, and then from there take the train to Barcelona. This avoids a stressful connection in Paris, where you need to move between the two stations Gare du Nord and Gare de Lyon.

From Italy, the main trouble is to deal with connections. The [Turin–Lyon high-speed railway](https://en.wikipedia.org/wiki/Turin%E2%80%93Lyon_high-speed_railway) contruction may help in the future but it's not running yet. The alternatives are either to go on the coast through Genova-Ventimiglia-Nice, or with the [Eurocity](https://www.raileurope.com/en/trains/eurocity) from Milan to Switzerland finally get to France.

From Portugal, which is so close geographically and culturally to Galicia, we could think there should be an easy way to travel to A Coruña. But apparently neither [Comboios de Portugal](https://www.cp.pt) nor [Renfe](https://venta.renfe.com) provides any direct train:
- From Porto, the ÖBB trip planner suggests connection at [Vigo-Guixar](https://en.wikipedia.org/wiki/Vigo-Guixar_railway_station) for a total duration of 6h30. As a comparison, the website of the [Web Engines Hackfest](https://webengineshackfest.org/) indicates a 3-hours trip by car and a 5-hours trip by bus.
- Between Libon and Porto, Comboios de Portugal seems to propose trains taking 2h30-3h. You can combine that with the other trains to do the trip to A Coruña with one night at Porto or Vigo.

Last but not least, [A Coruña railway station](https://en.wikipedia.org/wiki/A_Coru%C3%B1a_railway_station) is a one-quarter walk away from the Igalia office and a three-quarter walks away from Palexco (Web Engines Hackfest's venue). This is more convenient than the A Coruña airport which is around 10 km away from A Coruña.

## Notes and references

* [Flygskam](https://en.wikipedia.org/wiki/Flight_shame): anti-flying social movement started in Sweden, with the aim of reducing the environmental impact of aviation.
* [O Caminho de Santiago](https://en.wikipedia.org/wiki/Camino_de_Santiago): The Way of St. James, a network of pilgrims' ways leading to Santiago de Compostela (whose [railway station](https://en.wikipedia.org/wiki/Santiago_de_Compostela_railway_station) you will likely stop at if you take a train to A Coruña).

[^1]: Incidentally, people travelling from far away are unlikely to find a direct flight to the A Coruña airport. In that case, using local trains from bigger airports like Madrid or Porto may be a better option.
[^2]: Direct train between A Coruña and Barcelona seems to be rarer, slower and no longer available as night train. So a connection or night stay in Madrid seems the best option.
[^3]: [Deutsche Bahn](https://int.bahn.de/) offers a lot of Berlin to Cologne trains per day with a duration of 4h-4h30, including early/late trains or night trains, that you can combine with the Cologne-Paris Eurostar. Deutsche Bahn also offers (non-direct) ICE trains to go from Paris to Berlin.
[^4]: Ecopassenger gives information per train, so I'm provided some lower/upper bounds based on different trains.
[^5]: Based on the previous data from Eurostar, SNCF, Ecopassenger, Ecotree, trying to find the lowest/highest sum for each individual segment.
